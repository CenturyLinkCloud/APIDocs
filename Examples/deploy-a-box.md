{{{
"title": "Deploy a Box",
"date": "09-01-2016",
"author": "",
"date": "12-26-2018",
"author": "Virginia Sierra",
"attachments": [],
"contentIsHTML": false,
"keywords": ["api", "example", "authentication", "deployment", "box", "MongoDB", "Box", "Instance", "Terminate" ]
}}}

## Overview

This guide shows **how to deploy a mongoDB instance using the Cloud Application Manager API**. In this sample, we deploy a MongoDB instance using the existing MongoDB public box, the steps you need are:

 * [Authenticate with Cloud Application Manager](#authenticate-with-cloud-application-manager)
 * [Declare Deployment Arguments](#declare-deployment-arguments)
 * [Register a Provider in Cloud Application Manager](#register-a-provider-in-cloud-application-manager)
 * [Create a Deployment Policy Box](#create-a-deployment-policy-box)
 * [Deploy a MongoDB Instance](#deploy-a-mongodb-instance)
 * [Terminate the Instance](#terminate-the-instance)


**Note:** We use cURL commands to send HTTP requests to the API objects in JSON. JSON is the required format for all API requests and responses.

Now let’s look at the script in sections to understand how you can make API calls from any code you like.

## Authenticate with Cloud Application Manager

First of all, you should be Administrator on the target workspace or have [Administrator access](https://www.ctl.io/knowledge-base/cloud-application-manager/administering-your-organization/admin-access/) to your organization in Cloud Application Manager. 
Before calling to the API you have to log in into the Cloud Application Manager website and [get an authentication token](https://www.ctl.io/api-docs/cam/#getting-started). You will use this token later as an http header to perform every call to the Cloud Application Manager API.

## Declare Deployment Arguments

Next variables are set with script calling parameters. This way, each time you run the script, you can pass different deployment arguments. These declared variables are referenced later in your script as request parameter values.

| Variable |     Type    |  Description  |
|----------|-------------|---------------|
| provider_key<br>provider_secret | string | We will need the provider account key and secret to register a provider.<br>See below how to [register a provider](#Register-a-Provider-in-Cloud-Application-Manager) and get its parameters. |
| json_web_token | string | This is the [authentication token](#Authenticate-with-Cloud-Application-Manager) obtained before.<br>An example is *eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJvcGVyYb25z...* |
| environment | string | Set your URL organization hostname or your appliance IP, where API calls are sent.<br>Examples are:  *your-organization.cam.ctl.io*, *centurylink.cam.ctl.io*,  *192.168.1.10*. |
| owner | string | Specify the user ID in Cloud Application Manager who owns the provider account. |
| username | string | Name of the admin user. |
| password | string | Password of the admin user. |

Start your script with the following lines:
```
# Deployment common variables
provider_key=$1
provider_secret=$2

json_web_token=$3
environment=$4
owner=$5

username=$6
password=$7
```

There are other variables obtained during the script execution and necessary in next script steps.

| Variable |     Type    | Description |
|----------|-------------|-------------|
| provider_id | string | Obtained when registering a provider. |
| policy_box_id | string | Obtained when creating a deployment policy box. |
| instance_id | string | Obtained when deployin a box instance. |

## Register a Provider in Cloud Application Manager

A provider is a public or private cloud account you can register in Cloud Application Manager. 

To register a provider we send a POST request to the [Provider object](https://www.ctl.io/api-docs/cam/#cam-platform-providers-api) with the required parameters.

In this case, we choose to create an AWS as provider in the appliance. From the AWS account credentials we will need the key and the secret right now. Creating it in an organization service requires ARN code as credential. You can obtain the required parameters for other providers in [Provider object](https://www.ctl.io/api-docs/cam/#cam-platform-providers-api) API doc.

If there’s an error registering the provider, we output the error. Else, we output the provider ID and save it in *provider_id* variable.

Add the following lines to your script:
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
    -A "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8) AppleWebKit/534.30 (KHTML, like Gecko) Chrome/12.0.742.112 Safari/534.30" \
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

### Create a Deployment Policy Box

A deployment policy box is where you specify settings to deploy applications in a specific virtual environment.

To create a deployment policy box we send a POST request to the [Box object](https://www.ctl.io/api-docs/cam/#application-lifecycle-management-boxes-api) with the provider ID obtained when registering the provider in the *provider_id* variable. 

If there’s an error in creating the deployment policy box, we output the error. Else, we output the created deployment policy box ID and save it in *policy_box_id* variable.

Add the following lines to your script:

```
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
        \"name\": \"Deployment Policy Box Example\",
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
        -A "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8) AppleWebKit/534.30 (KHTML, like Gecko) Chrome/12.0.742.112 Safari/534.30" \
        -H "Accept: application/json" \
        -H "Content-Type: application/json;charset=UTF-8" \
        -d "$payload" https://$environment/services/boxes)
policy_box_id=$(echo $policy_box | python -c 'import json,sys; print json.load(sys.stdin)["id"]')
if [ -z != $policy_box_id ]; then
        echo "Created Deployment Policy Box $policy_box_id"
else
        echo "Error launching the Deployment Policy Box: $policy_box"
        exit 1
fi;
```

### Deploy a MongoDB Instance

To deploy a MongoDB instance using the existing MongoDB public box, we send a POST request to the [Instances object](https://www.ctl.io/api-docs/cam/#application-lifecycle-management-instances-api) with the box ID of the MongoDB box  *mongo_box_id* variable and the policy box ID obtained when creating the policy box in the *policy_box_id* variable.

If there’s an error deploying instance, we output the error. Else, we output the deployed instance ID and save it in *instance_id* variable.

Add the following lines to your script:

```
#Deploy the instance
payload="{
    \"schema\": \"http://elasticbox.net/schemas/deploy-instance-request\",
    \"owner\": \"$owner\",
    \"name\": \"ScriptBoxSample\",
    \"box\": {
        \"id\": \"$mongo_box_id\",
        \"variables\": [
            {
              \"name\": \"username\",
              \"type\": \"Text\",
              \"value\": \"$username\",
              \"required\": true
            },
            {
              \"name\": \"password\",
              \"type\": \"Password\",
              \"value\": \"$password\",
              \"required\": true
            }
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
    -H "elasticbox-release:4.0" \
    -A "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8) AppleWebKit/534.30 (KHTML, like Gecko) Chrome/12.0.742.112 Safari/534.30" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json;charset=UTF-8" \
    -d "$payload" https://$environment/services/instances)
instance_id=$(echo $instance | python -c 'import json,sys; print json.load(sys.stdin)["id"]')
if [ -z != $instance_id ]; then
    echo "Deployed Instance $instance_id"
else
    echo "Error deploying the Instance: $instance_id"
    exit 1
fi;
```

We store the response and check if the instance launched. If it failed to launch, we output an error or say that the instance is available and give its ID.

While the instance is launching, we check its state every 30 seconds with a GET request to the Instances object by passing the instance ID. Then we evaluate whether to wait or continue: If it’s still processing, we say so and wait or we output the current instance state and move to the next task.

```
COUNTER=0
while [ $COUNTER -lt $cycles_to_wait ]; do
  instance=$(curl -k -s \
    -X GET\
    -H "Authorization:Bearer $json_web_token" \
    -H "elasticbox-release:4.0" \
    -A "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8) AppleWebKit/534.30 (KHTML, like Gecko) Chrome/12.0.742.112 Safari/534.30" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    https://$environment/services/instances/${instance_id})
  instance_state=$(echo $instance | python -c 'import json,sys; print json.load(sys.stdin)["state"]')
  instance_operation=$(echo $instance | python -c 'import json,sys; print json.load(sys.stdin)["operation"]')
  if [[ "$instance_state" == "processing" ]]; then
    echo "The state of the Instance is $instance_state $instance_operation Waiting for it to be done or unavailable"
    let COUNTER=COUNTER+1
    sleep 30
  else
    echo "The state of the Instance is $instance_state $instance_operation. Process completed"
    break
  fi
done
```

### Terminate the Instance

To remove the instance from the virtual machine, we send a DELETE request to the Instances object with the instance ID. Then we check its response status. If it’s 200, we say that the specific instance is terminated. Else, we output the error state from the response.

```
status=$(curl -s -k \
  -X DELETE \
  -H "Accept: application/json" \
  -A "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8) AppleWebKit/534.30 (KHTML, like Gecko) Chrome/12.0.742.112 Safari/534.30" \
  -H "Content-Type:application/json" \
  -H "Authorization:Bearer $json_web_token" \
  -H "elasticbox-release:4.0" \
  -w '%{http_code}' \
  -o /dev/null \
  https://$environment/services/instances/${instance_id}?operation=terminate)
if [[ ! $status -eq 202 ]]; then
  echo "Error terminating the instance: Error $status"
  exit 1
else
  echo "Terminated Instance $instance_id"
fi
```

While waiting for the instance to terminate, we do a GET on the Instances object with the instance ID to know the operation running on the instance and its current state. If it’s processing, we say so and wait for it to complete or we output the operation that was run and the instance state.

```
#Wait for the instance to be terminated
COUNTER=0
while [[ $COUNTER -lt 30 ]]; do
  instance=$(curl -k -s \
    -X GET \
    -H "Accept: application/json" \
    -A "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8) AppleWebKit/534.30 (KHTML, like Gecko) Chrome/12.0.742.112 Safari/534.30" \
    -H "Content-Type:application/json" \
    -H "Authorization:Bearer $json_web_token" \
    -H "elasticbox-release:4.0" \
    https://$environment/services/instances/${instance_id})
  instance_state=$(echo $instance | python -c 'import json,sys; print json.load(sys.stdin)["state"]')
  instance_operation=$(echo $instance | python -c 'import json,sys; print json.load(sys.stdin)["operation"]')
  if [[ "$instance_state" == "processing" ]]; then
    echo "The state of the instance is $instance_state $instance_operation Waiting for it to be done or unavailable"
    let COUNTER=COUNTER+1
    sleep 30
  else
    echo "The state of the Instance is $instance_state $instance_operation"
    break
  fi
done
```

Lastly, we delete the instance and its logs from Cloud Application Manager by sending a DELETE request with the instance ID to the Instances object. Once done, we say that the instance is deleted. Similarly we delete the deployment policy box with a DELETE request to the Profiles object and confirm that it’s done.

```
#Remove the deployment policy box
status=$(curl -s -k \
  -X DELETE \
  -H "Accept: application/json" \
  -A "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8) AppleWebKit/534.30 (KHTML, like Gecko) Chrome/12.0.742.112 Safari/534.30" \
  -H "Content-Type:application/json" \
  -H "Authorization:Bearer $json_web_token" \
  -H "elasticbox-release:4.0" \
  -w '%{http_code}' \
  -o /dev/null \
  https://$environment/services/boxes/${policy_box_id})
if [[ ! $status -eq 204 ]]; then
  echo "Error terminating the Deployment Policy Box: Error $status"
  exit 1
else
  echo "Terminated Deployment Policy Box $policy_box_id"
fi
```

### Contacting Cloud Application Manager Support

We’re sorry you’re having an issue in [Cloud Application Manager](https://www.ctl.io/cloud-application-manager/). Please review the [troubleshooting tips](https://www.ctl.io/knowledge-base/cloud-application-manager/troubleshooting/troubleshooting-tips/), or contact [Cloud Application Manager support](mailto:incident@CenturyLink.com) with details and screenshots where possible.

For issues related to API calls, send the request body along with details related to the issue.

In the case of a box error, share the box in the workspace that your organization and Cloud Application Manager can access and attach the logs.
* Linux: SSH and locate the log at /var/log/elasticbox/elasticbox-agent.log
* Windows:  RDP into the instance to locate the log at \ProgramData\ElasticBox\Logs\elasticbox-agent.log
