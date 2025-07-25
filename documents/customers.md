## Customer


### Create customer
```go

data := map[string]interface{}{
    "name": "Gaurav Kumar",
    "contact": 9123456780,
    "email": "gaurav.kumar@example.com",
    "fail_existing": "1",
    "gstin": "29XAbbA4369J1PA",
    "notes": map[string]interface{}{
      "notes_key_1": "Tea, Earl Grey, Hot",
      "notes_key_2": "Tea, Earl Grey… decaf.",
	},
}

body, err := client.Customer.Create(data, nil)
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| name*          | string      | Name of the customer                        |
| email        | string      | Email of the customer                       |
| fail_existing | string | If a customer with the same details already exists, the request throws an exception by default. Possible value is `1` or `0`|
| contact      | string      | Contact number of the customer              |
| gstin         | string      | Customer's GST number, if available. For example, 29XAbbA4369J1PA  |
| notes         | object      | A key-value pair                            |

**Response:**
```json
{
  "id" : "cust_1Aa00000000004",
  "entity": "customer",
  "name" : "Gaurav Kumar",
  "email" : "gaurav.kumar@example.com",
  "contact" : "9123456780",
  "gstin": "29XAbbA4369J1PA",
  "notes":{
    "notes_key_1":"Tea, Earl Grey, Hot",
    "notes_key_2":"Tea, Earl Grey… decaf."
  },
  "created_at ": 1234567890
}
```

-------------------------------------------------------------------------------------------------------

### Edit customer
```go
customerId := "cust_1Aa00000000003"

data := map[string]interface{}{
  "name": "Gaurav Kumar",
  "email": "Gaurav.Kumar@example.com",
  "contact": 9000000000,
}
body, err := client.Customer.Edit(customerId, data, nil)
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| customerId*          | string      | The id of the customer to be updated  |
| email        | string      | Email of the customer                       |
| name        | string      | Name of the customer                        |
| contact      | string      | Contact number of the customer              |

**Response:**
```json
{
  "id": "cust_1Aa00000000003",
  "entity": "customer",
  "name": "Gaurav Kumar",
  "email": "Gaurav.Kumar@example.com",
  "contact": "9000000000",
  "gstin": null,
  "notes": {
    "notes_key_1": "Tea, Earl Grey, Hot",
    "notes_key_2": "Tea, Earl Grey… decaf."
  },
  "created_at": 1582033731
}
```
-------------------------------------------------------------------------------------------------------

### Fetch all customer
```go
optional := map[string]interface{}{
	  "count":1,
	}

body, err := client.Customer.All(optional, nil)
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| count | integer   | number of payments to fetch (default: 10)        |
| skip  | integer   | number of payments to be skipped (default: 0)    |

**Response:**
```json
{
  "entity":"collection",
  "count":1,
  "items":[
    {
      "id":"cust_1Aa00000000001",
      "entity":"customer",
      "name":"Gaurav Kumar",
      "email":"gaurav.kumar@example.com",
      "contact":"9876543210",
      "gstin":"29XAbbA4369J1PA",
      "notes":{
        "note_key_1":"September",
        "note_key_2":"Make it so."
      },
      "created_at ":1234567890
    }
  ]
}
```

-------------------------------------------------------------------------------------------------------

### Fetch a customer
```go
customerId := "cust_1Aa00000000003"

body, err := client.Customer.Fetch(customerId, nil, nil)
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| customerId*          | string      | The id of the customer to be fetched  |

**Response:**
```json
{
  "id" : "cust_1Aa00000000001",
  "entity": "customer",
  "name" : "Saurav Kumar",
  "email" : "Saurav.kumar@example.com",
  "contact" : "+919000000000",
  "gstin":"29XAbbA4369J1PA",
  "notes" : [],
  "created_at ": 1234567890
}
```

-------------------------------------------------------------------------------------------------------

### Add Bank Account of Customer

```go
customerId := "cust_N5mywh91sXB69O"

body, err := client.Customer.AddBankAccount(customerId, data, nil)
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| customerId*  | string      | Unique identifier of the customer. |
| account_number | string      | Customer's bank account number. For example, `0002020000304030434`. |
| beneficiary_name | string  | The name of the beneficiary associated with the bank account.  |
| beneficiary_address1 | string      | The virtual payment address.  |
| beneficiary_email  | string      | Email address of the beneficiary. For example, `gaurav.kumar@example.com`. |
| beneficiary_mobile | integer      | Mobile number of the beneficiary.  |
| beneficiary_city  | string      | The name of the city of the beneficiary.  |
| beneficiary_state | string      | The state of the beneficiary.  |
| beneficiary_country | string      | The country of the beneficiary.  |
| beneficiary_pin   | interger    | The pin code of the beneficiary's address.  |
| ifsc_code          | string      | The IFSC code of the bank branch associated with the account.  |

**Response:**
```json
{
  "id" : "cust_1Aa00000000001",
  "entity": "customer",
  "name" : "Saurav Kumar",
  "email" : "Saurav.kumar@example.com",
  "contact" : "+919000000000",
  "gstin":"29XAbbA4369J1PA",
  "notes" : [],
  "created_at ": 1234567890
}
```

-------------------------------------------------------------------------------------------------------

### Delete Bank Account of Customer

```go
bankAccountId := "ba_N6aM8uo64IzxHu"

customerId := "cust_N5mywh91sXB69O"

body, err := client.Customer.DeleteBankAccount(customerId, bankAccountId, nil, nil)
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| customerId*  | string      |  Customer id of the customer whose bank account is to be deleted.  |
| bankAccountId  | string      | The bank_id that needs to be deleted.  |

**Response:**
```json
{
    "id": "ba_Evg09Ll05SIPSD",
    "ifsc": "ICIC0001207",
    "bank_name": "ICICI Bank",
    "name": "Test R4zorpay",
    "account_number": "XXXXXXXXXXXXXXX0434",
    "status": "deleted"
}
```

-------------------------------------------------------------------------------------------------------

### Eligibility Check API

```go

data := map[string]interface{}{
  "inquiry":  "affordability",
  "amount":   500000,
  "currency": "INR",
  "customer": map[string]interface{}{
    "id":         "cust_KhP5dO1dKmc0Rm",
    "contact":    "+918220276214",
    "ip":         "105.106.107.108",
    "referrer":   "https://merchansite.com/example/paybill",
    "user_agent": "Mozilla/5.0",
  },
}

body, err := client.Customer.RequestEligibilityCheck(data, nil)
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| inquiry  | string      | List of methods or instruments on which eligibility check is required. Possible value is `affordability`. |
| amount*  | integer      | The amount for which the order was created, in currency subunits. For example, for an amount of ₹295, enter `29500`. The user makes a payment for this amount against the order; hence, eligibility is checked for the amount. |
| currency*  | string      | A three-letter ISO code for the currency in which you want to accept the payment. Possible value is `INR`.  |
| customer*  | object      | Customer details. [here](https://razorpay.com/docs/payments/payment-gateway/affordability/eligibility-check/#eligibility-check-api)  |
| instruments  | object | Payment instruments on which an eligibility check is required. [here](https://razorpay.com/docs/payments/payment-gateway/affordability/eligibility-check/#eligibility-check-api)  |


**Response:**
```json
{
  "amount": "500000",
  "customer": {
    "id": "KkBhM9EC1Y0HTm",
    "contact": "+919999999999"
  },
  "instruments": [
    {
      "method": "emi",
      "issuer": "HDFC",
      "type": "debit",
      "eligibility_req_id": "elig_xxxxxxxxxxxxx",
      "eligibility": {
        "status": "eligible"
      }
    },
    {
      "method": "paylater",
      "provider": "getsimpl",
      "eligibility_req_id": "elig_xxxxxxxxxxxxx",
      "eligibility": {
        "status": "eligible"
      }
    },
    {
      "method": "paylater",
      "provider": "icic",
      "eligibility_req_id": "elig_xxxxxxxxxxxxx",
      "eligibility": {
        "status": "eligible"
      }
    },
    {
      "method": "cardless_emi",
      "provider": "walnut369",
      "eligibility_req_id": "elig_xxxxxxxxxxxxx",
      "eligibility": {
        "status": "ineligible",
        "error": {
          "code": "GATEWAY_ERROR",
          "description": "The customer has not been approved by the partner.",
          "source": "business",
          "step": "inquiry",
          "reason": "user_not_approved"
        }
      }
    },
    {
      "method": "cardless_emi",
      "provider": "zestmoney",
      "eligibility_req_id": "elig_xxxxxxxxxxxxx",
      "eligibility": {
        "status": "ineligible",
        "error": {
          "code": "GATEWAY_ERROR",
          "description": "The customer has exhausted their credit limit.",
          "source": "business",
          "step": "inquiry",
          "reason": "credit_limit_exhausted"
        }
      }
    },
    {
      "method": "paylater",
      "provider": "lazypay",
      "eligibility_req_id": "elig_xxxxxxxxxxxxx",
      "eligibility": {
        "status": "ineligible",
        "error": {
          "code": "GATEWAY_ERROR",
          "description": "The order amount is less than the minimum transaction amount.",
          "source": "business",
          "step": "inquiry",
          "reason": "min_amt_required"
        }
      }
    }
  ]
}
```

-------------------------------------------------------------------------------------------------------

### Fetch Eligibility by id

```go
eligibilityId := "elig_xxxxxxxxxxxxx"
body, err := client.Customer.FetchEligibility(eligibilityId, nil, nil)
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| eligibilityId  | string      | The unique identifier of the eligibility request to be retrieved.  |

**Response:**
```json
{
  "instruments": [
    {
      "method": "paylater",
      "provider": "lazypay",
      "eligibility_req_id": "elig_xxxxxxxxxxxxx",
      "eligibility": {
        "status": "eligible"
      }
    },
    {
      "method": "paylater",
      "provider": "getsimpl",
      "eligibility_req_id": "elig_xxxxxxxxxxxxx",
      "eligibility": {
        "status": "ineligible",
        "error": {
          "code": "GATEWAY_ERROR",
          "description": "The customer has exhausted their credit limit",
          "source": "gateway",
          "step": "inquiry",
          "reason": "credit_limit_exhausted"
        }
      }
    }
  ]
}
```

-------------------------------------------------------------------------------------------------------

**PN: * indicates mandatory fields**
<br>
<br>
**For reference click [here](https://razorpay.com/docs/api/customers/)**