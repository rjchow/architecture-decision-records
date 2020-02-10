# Rationally API

# Barcode Resource

Example:

```json
[
  {
    "sku": "6001106119225",
    "category": "product-x",
    "unit": "ml",
    "quantity": 200,
    "name": "Dettol Hand Sanitiser 200ml"
  },
  {
    "sku": "608912992255",
    "category": "product-y",
    "unit": "piece",
    "quantity": 50,
    "name": "Filter Mask - 50 Count 3-Ply Disposable Face Mask"
  }
]
```

# Backend API

### GET: /quota/:id

Example:

```sh
GET: /transactions/S0000001I
```

Returns:

```json
[
  {
    "category": "product-1",
    "remainingQuota": 1
  },
  {
    "category": "product-2",
    "remainingQuota": 0
  }
]
```

### POST: /transactions/:id

Example:

```sh
POST: /transactions/S0000001I

body: {
  "quantity": 5
}
```

Returns:

```json
[
  {
    "quantity": 5,
    "transactionTime": 1580330642589
  }
]
```

### GET: /auth

Example:

```sh
GET: /transactions/S0000001I
```

Returns:

```json
[
  {
    "category": "product-1",
    "name": "Product 1",
    "unit": "piece",
    "quantityPerPeriod": 1,
    "period": 604800
  },
  {
    "category": "product-2",
    "name": "Product 2",
    "unit": "ml",
    "quantityPerPeriod": 500,
    "period": 604800
  }
]
```

### POST: /auth

This endpoint is protected by AWS_IAM, if you are using Postman please use AWS Signature for authorization method.
If you are using this from the commandline using `sls invoke`, you can invoke it like this if you have the right IAM permissions:

```
sls invoke -f postAuthorisationToken -d '{ "body": "{\"authToken\": \"93b7d487-8935-493b-8bde-d8954e48b3be\",\"role\": \"OPERATOR\",\"userReference\": \"S0000003E\"}" }'
```
