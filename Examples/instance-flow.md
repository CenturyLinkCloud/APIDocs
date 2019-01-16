{{{
"title": "Instance Flow",
"date": "12-19-2018",
"author": "Julio Castanar",
"attachments": [],
"contentIsHTML": false,
"keywords": ["api", "example", "authentication", "deployment", "provider", "policy box", "box", "instance", "terminate" ]
}}}

**In this article**

* [Overview](#overview)
* [Authenticate with Cloud Application Manager](#authenticate-with-cloud-application-manager)
* [Obtain Deployment Variables](#obtain-deployment-variables)
* [Register a Provider in Cloud Application Manager](#register-a-provider-in-cloud-application-manager)
* [Create a Deployment Policy Box](#create-a-deployment-policy-box)
* [Create a Custom Box](#create-a-custom-box)
* [Deploy the Instance](#deploy-the-instance)
* [Terminate and Delete the Instance](#terminate-and-delete-the-instance)
* [Contacting Cloud Application Manager Support](#contacting-cloud-application-manager-support)

## Overview

This guide shows **how to use Cloud Application Manager API from Registering a Provider to the Deployment of an Instance**.


**Notes:** 
1. You will use cURL commands to send HTTP requests to the API objects in JSON. JSON is the required format for all API requests and responses.

2. cURL commands in examples use -k parameter for convenience allowing curl to proceed and operate even for server connections considered insecure. Don't use it in production.

3. When executing a command, it takes a while for the resources to be ready, and calling the next step before the previous is completed may lead to error (i.e. right after creating the provider it will start the synchronization, and the deployment box cannot be created until the first sync completes).

Now let’s look at the script in sections to understand how you can make API calls from any code you like.

## Authenticate with Cloud Application Manager

First of all, you need to hold the administrator role on a workspace to be able to run these steps. You must obtain [Administrator access](https://www.ctl.io/knowledge-base/cloud-application-manager/administering-your-organization/admin-access/) to Cloud Application Manager. 
Before calling to the API you have to sign in into the Cloud Application Manager website and [get an authentication token](https://www.ctl.io/api-docs/cam/#getting-started).You will use this token as an authentication HTTP header to perform every call to the Cloud Application Manager API.

## Obtain Deployment Variables

Next, define the variables that will contain the parameters of the script. This way, each time you run the script, you can pass different deployment arguments. These declared variables are referenced later in your script as request parameter values.

| Variable | Description |
|----------|-------------|
| provider_key | You need the provider account key and secret to register a provider. |
| provider_secret | See below how to [register a provider](#Register-a-Provider-in-Cloud-Application-Manager) and get its parameters. |
| json_web_token | This is the [authentication token](#Authenticate-with-Cloud-Application-Manager) obtained before.<br>It's a long BASE64 encoded string that starts with something like:<br/>  *eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJvcGVyYb25z...* |
| environment | Set your URL organization hostname or your appliance IP, where API calls are sent.<br>Examples are:  *your-organization.cam.ctl.io*, *centurylink.cam.ctl.io*,  *192.168.1.10*. |
| owner | Specify the user ID in Cloud Application Manager who owns the provider account. |

Start with your script with the following lines:
```
# Deployment common variables
provider_key=$1
provider_secret=$2
json_web_token=$3
environment=$4
owner=$5
```

There are other variables obtained during the script execution and necessary in next script steps.
| Variable | Description |
|----------|-------------|
| provider_id | Obtained when registering a provider. |
| policy_box_id | Obtained when creating a deployment policy box. |
| box_id | Obtained when creating a custom box. |
| instance_id | Obtained when deployin a box instance. |


## Register a Provider in Cloud Application Manager

A provider is a public or private cloud account you can register in Cloud Application Manager. 

To register a provider send a POST request to the [Providers endpoint](https://www.ctl.io/api-docs/cam/#cam-platform-providers-api) with the requiered parameters.

In this case choose create an AWS as provider in an appliance. It will be necessary a key and the secret pair.  
Creating it in an oragnization service requieres a role ARN as credential instance of a key pair.  
Other provider types require different credential sets that you can obtain check in the [Providers endpoint](https://www.ctl.io/api-docs/cam/#cam-platform-providers-api) API doc.

If there’s an error registering the provider, it outputs the error. Else, it outputs the provider ID and saves it in *provider_id* variable.

Add the following lines to the script:
```
# Register the provider AWS in Cloud Application Manager script
payload="{
  \"icon\": \"images/platform/aws.png\",
  \"type\": \"Amazon Web Services\",
  \"description\": \"Manage EC2, ECS and Cloudformation instances\",
  \"schema\": \"http://elasticbox.net/schemas/aws/provider\",
  \"name\": \"AWS Provider example via API\",
  \"credentials\": {
    \"key\": \"$provider_key\",
    \"secret\": \"$provider_secret\"
  },
  \"owner\": \"$owner\"
}"
provider=$(curl -k -s \
    -X POST \
    -H "Authorization:Bearer $json_web_token" \
    -H "elasticbox-release:4.0" \
    -H "Accept: application/json, text/plain, */*" \
    -H "Accept-encoding: gzip, deflate" \
    -H "Content-Type: application/json" \
    -d "$payload" https://$environment/services/providers)
provider_id=$(echo $provider | python -c 'import json,sys; print json.load(sys.stdin)["id"]')
if [ -z != $provider_id ]; then
    echo "Created provider $provider_id"
else
    echo "Error creating the provider: $provider"
fi;
```

## Create a Deployment Policy Box

A deployment policy box contains the settings to deploy applications in a specific virtual environment. For AWS, it contains details about the region, VPC, security groups, etc.

To create a deployment policy box send a POST request to the [Boxes endpoint](https://www.ctl.io/api-docs/cam/#application-lifecycle-management-boxes-api) with the provider ID obtained when registering the provider in the *provider_id* variable. 

If there’s an error in creating the deployment policy box, it outputs the error. Else, it outputs the created deployment policy box ID and saves it in *policy_box_id* variable.

Add the following lines to the script:
```
# Once the provider has been created, the proper policy box can be set
payload="{
  \"owner\": \"$owner\",
  \"schema\": \"http://elasticbox.net/schemas/boxes/policy\",
  \"claims\": [
    \"linux\"
  ],
  \"lifespan\": {
    \"operation\": \"none\"
  },
  \"automatic_updates\": \"off\",
  \"provider_id\": \"$provider_id\",
  \"name\": \"Deployment Policy Box example via API\",
  \"description\": \"Just one example of deployment policy box creation via API\",
  \"profile\": {
    \"schema\": \"http://elasticbox.net/schemas/aws/ec2/profile\",
    \"flavor\": \"t1.micro\",
    \"location\": \"us-east-1\",
    \"instances\": 1,
    \"image\": \"Linux Compute\",
    \"keypair\": \"None\",
    \"cloud\": \"EC2\",
    \"security_groups\": [

    ],
    \"subnet\": \"us-east-1a\"
  }
}"
policy_box=$(curl -k -s \
    -X POST \
    -H "Content-Type:application/json" \
    -H "Authorization:Bearer $json_web_token" \
    -H "elasticbox-release:4.0" \
    -H "Accept: application/json, text/plain, */*" \
    -H "Accept-encoding: gzip, deflate" \
    -H "Content-Type: application/json;charset=UTF-8" \
    -d "$payload" https://$environment/services/boxes)
policy_box_id=$(echo $policy_box | python -c 'import json,sys; print json.load(sys.stdin)["id"]')
if [ -z != $policy_box_id ]; then
    echo "Created policy_box $policy_box_id"
else
    echo "Error launching the policy_box: $policy_box"
fi;
```

## Create a Custom Box

A script box defines the behavior of your application during deployment, reconfiguration and termination.

To create a box send a POST request to the [Boxes endpoint](https://www.ctl.io/api-docs/cam/#application-lifecycle-management-boxes-api). 

Also use two already created blobs. You can take a look to the [Blobs endpoint](https://www.ctl.io/api-docs/cam/#application-lifecycle-management-blobs-api), API documentation if you need to know how you can create them.

If there’s an error creating this box, it outputs the error. Else, it outputs the box ID and saves it in *box_id* variable.

Add the following lines to the script:
```
# Create a box to deploy with that policy box. In this case use a previously uploaded scripts.
payload="{
  \"automatic_updates\": \"off\",
  \"requirements\": [

  ],
  \"description\": \"create box example via API\",
  \"name\": \"ScriptBoxSample\",
  \"deleted\": null,
  \"variables\": [
    {
      \"required\": true,
      \"type\": \"Text\",
      \"name\": \"variable_name\",
      \"value\": \"variable_value\",
      \"visibility\": \"public\"
    }
  ],
  \"visibility\": \"workspace\",
  \"members\": [

  ],
  \"owner\": \"$owner\",
  \"organization\": \"elasticbox\",
  \"events\": {
    \"configure\": {
      \"url\": \"/services/blobs/download/5631fa7614841250525226cc/configure\",
      \"length\": 5,
      \"destination_path\": \"scripts\",
      \"content_type\": \"text/x-shellscript\"
    },
    \"install\": {
      \"url\": \"/services/blobs/download/5631fa6614841250525226ca/install\",
      \"length\": 5,
      \"destination_path\": \"scripts\",
      \"content_type\": \"text/x-shellscript\"
    }
  },
  \"schema\": \"http://elasticbox.net/schemas/boxes/script\"
}"
box=$(curl -k -s \
    -X POST \
    -H "Content-Type:application/json" \
    -H "Authorization:Bearer $json_web_token" \
    -H "elasticbox-release:4.0" \
    -H "Accept: application/json, text/plain, */*" \
    -H "Accept-encoding: gzip, deflate" \
    -H "Content-Type: application/json;charset=UTF-8" \
    -d "$payload" https://$environment/services/boxes) \
box_id=$(echo $box | python -c 'import json,sys; print json.load(sys.stdin)["id"]')
if [ -z != $box_id ]; then
    echo "Created box $box_id"
else
    echo "Error launching the box: $box"
fi;
```

## Deploy the Instance

To deploy an instance of the previous box, send a POST request to the [Instances endpoint](https://www.ctl.io/api-docs/cam/#application-lifecycle-management-instances-api) with the box ID obtained when creating the box in the *box_id* variable and the policy box ID obtained when creating the policy box in the *policy_box_id* variable.

If there’s an error deploying the instance, it outputs the error. Else, it outputs the deployed instance ID and saves it in *instance_id* variable.

Add the following lines to the script:
```
# Finally, deploy the instance
payload="{
    \"schema\": \"http://elasticbox.net/schemas/deploy-instance-request\",
    \"owner\": \"$owner\",
    \"name\": \"ScriptBoxSample\",
    \"box\": {
        \"id\": \"$box_id\",
        \"variables\": [
        ]
    },
    \"instance_tags\": [

    ],
    \"automatic_updates\": \"off\",
    \"policy_box\": {
        \"id\": \"$policy_box_id\",
        \"variables\": [

        ]
     }
}"
instance=$(curl -k -s \
    -X POST \
    -H "Content-Type:application/json" \
    -H "Authorization:Bearer $json_web_token" \
    -H "elasticbox-release:4.0" 
    -H "Accept: application/json, text/plain, */*" \
    -H "Accept-encoding: gzip, deflate" \
    -H "Content-Type: application/json;charset=UTF-8" \
    -d "$payload" https://$environment/services/instances)
instance_id=$(echo $instance | python -c 'import json,sys; print json.load(sys.stdin)["id"]')
if [ -z != $instance_id ]; then
    echo "Deployed instance $instance_id"
else
    echo "Error deploying the instance: $instance_id"
fi;
```

## Terminate and Delete the Instance

Removing the instance from the virtual machine must be done into two steps: first, terminate the instance and second, delete it.

Terminate runs the stop and terminate events scripts, and then removes the cloud resources, but does not remove the instance from the Cloud Application Manager database. Send a DELETE request to the [Instances endpoint](https://www.ctl.io/api-docs/cam/#application-lifecycle-management-instances-api) with the instance ID obtained when deploying the instance in the *instance_id* variable and with an `operation=terminate` URL parameter.

 Then check its response status. If it’s 200, the specific instance has been terminated. Else, check the error state from the response.

 You can force terminate it using `operation=force_terminate` URL parameter. See detailed [DELETE API command](https://www.ctl.io/api-docs/cam/#application-lifecycle-management-instances-api-delete--services-instances--instance_id-) in Instances API.

Add the following lines to the script:
```
curl -k -s \
-X DELETE \
-H "Authorization:Bearer $json_web_token" \
-H "elasticbox-release:4.0" \
-H "Accept: application/json, text/plain, */*" \
-H "Accept-encoding: gzip, deflate" \
 https://$environment/services/instances/$instance_id??operation=terminate

echo "Undeployed box instance: $instance_id"
```
Afterwards, send a DELETE command again with an `operation=delete` URL parameter to remove definitely the instance from Cloud Application Manager.

 Copy previous script lines again and override the last two lines with these new ones:
```
   https://$environment/services/instances/$instance_id??operation=delete

 echo "Removed box instance: $instance_id"
```


## Contacting Cloud Application Manager Support

We’re sorry you’re having an issue in [Cloud Application Manager](https://www.ctl.io/cloud-application-manager/). Please review the [troubleshooting tips](https://www.ctl.io/knowledge-base/cloud-application-manager/troubleshooting/troubleshooting-tips/), or contact [Cloud Application Manager support](mailto:incident@CenturyLink.com) with details and screenshots where possible.

For issues related to API calls, send the request body along with details related to the issue.

In the case of a box error, share the box in the workspace that your organization and Cloud Application Manager can access and attach the logs.
* Linux: SSH and locate the log at /var/log/elasticbox/elasticbox-agent.log
* Windows: RDP into the instance to locate the log at \ProgramData\ElasticBox\Logs\elasticbox-agent.log
