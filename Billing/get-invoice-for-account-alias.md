{{{
  "title": "Get Invoice Data for an Account Alias",
  "date": "8-11-2015",
  "author": "Jared Ruckle",
  "attachments": []
}}}

Gets a list of invoicing data for a given account alias for a given month. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

**NOTE: THE DATA RETURNED IN THIS API ARE USAGE ESTIMATES ONLY, AND DOES NOT REPRESENT AN ACTUAL BILL.**

### When to Use It

Use this API operation when you want to get invoicing data for a given account for a given month.

## URL

### Structure

    GET https://api.ctl.io/v2/invoice/{accountAlias}/{year}/{month}

### Example

    GET https://api.ctl.io/v2/invoice/ALIAS/2015/7/?pricingAccount=PALIAS

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| year | integer | Year of usage, in YYYY format. | Yes |
| month | integer | Monthly period of usage, in M format. | Yes |
| pricingAccountAlias | string | Short code of the account that sends the invoice for the accountAlias | No |

## Response

The response includes a JSON object containing an array with invoicing data.

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the account alias being queried |
| terms | string | payment terms associated with the account |
| companyName | string | Description of the account name |
| accountAlias | string | Short code for a particular account |
| pricingAccountAlias | string | Short code for a particular account that receives the bill for the accountAlias usage |
| parentAccountAlias | string | Short code for the parent account alias associated with the account alias being queried |
| address1 | string | First line of the address associated with accountAlias |
| address2 | string | Second line of the address associated with accountAlias |
| city | string | City associated with the accountAlias |
| stateProvince | string | State or province associated with the accountAlias |
| postalCode | string | Postal code associated with the accountAlias |
| billingContactEmail | string | Billing email address associated with the accountAlias |
| invoiceCCEmail | string | Additional billing email address associated with the accountAlias |
| totalAmount | decimal | Invoice amount in dollars |
| invoiceDate | string | Date the invoice is finalized |
| poNumber | string | Purchase Order associated with the Invoice |
| lineItems | array | Usage details of a resource or collection of similar resources |

### Line Items Definition

| Name | Type | Description |
| --- | --- | --- |
| quantity | integer | Quantity of the line item |
| description | string | Text description of the line item |
| unitCost | decimal | Unit cost of the line item |
| itemTotal | decimal | Total cost of the line item |
| serviceLocation | string | Location of the line item |
| itemDetails | complex | Details about the line item |

### Examples

#### JSON
```json
{
    "id": "ALIAS69849A66",
    "terms": "Net 15",
    "companyName": "CTL Cloud Solutions",
    "accountAlias": "ALIAS",
    "pricingAccountAlias": "ALIAS",
    "parentAccountAlias": "PALIAS",
    "address1": "1100 112th Ave NE",
    "address2": "Suite 400",
    "city": "Bellevue",
    "stateProvince": "WA",
    "postalCode": "98004",
    "billingContactEmail": "billing@domain.com",
    "invoiceCCEmail": "",
    "totalAmount": 0,
    "invoiceDate": "2015-08-01T00:00:00Z",
    "poNumber": "",
    "lineItems": [
        {
            "quantity": 1,
            "description": "Server Group: DEMO - VA1",
            "unitCost": 153.93,
            "itemTotal": 153.93,
            "serviceLocation": "VA1",
            "itemDetails": [
                {
                    "description": "VA1ALIASJMB01",
                    "cost": 153.93
                }
            ]
        },
        {
            "quantity": 1,
            "description": "Shared Load Balancer - CA1",
            "unitCost": 29.76,
            "itemTotal": 29.76,
            "serviceLocation": "CA1",
            "itemDetails": []
        },
        {
            "quantity": 1,
            "description": "Additional Networks - GB3",
            "unitCost": 45,
            "itemTotal": 45,
            "serviceLocation": "GB3",
            "itemDetails": []
        },
    ]
}
```
