# ADR

## API Specification

GET /auth
Header:
api-key:b2e5e88c-1473-4afc-9c02-3aba73340456

Response:
`OK`

GET /quota/{nric}

Header:
api-key:b2e5e88c-1473-4afc-9c02-3aba73340456

Response:

```json
{
  "quota": 20,
  "history": [
    { "timestamp": 123, "quantity": 20 },
    { "timestamp": 123, "quantity": 20 },
    { "timestamp": 123, "quantity": 20 }
  ]
}
```

GET /quota/{nric}

Header:
api-key:b2e5e88c-1473-4afc-9c02-3aba73340456

Response:

```json
{
  "quota": 20,
  "history": [
    { "timestamp": 123, "quantity": 20 },
    { "timestamp": 123, "quantity": 20 },
    { "timestamp": 123, "quantity": 20 }
  ]
}
```

or

```json
{
  "quota": 20,
  "nextPurchaseTime": 123
}
```

POST /transactions/{nric}

Header:
api-key:b2e5e88c-1473-4afc-9c02-3aba73340456

Request:

```json
{
  "quantity": 20
}
```

Response:

```json
{
  "quota": 20,
  "history": [
    { "timestamp": 123, "quantity": 20 },
    { "timestamp": 123, "quantity": 20 },
    { "timestamp": 123, "quantity": 20 }
  ]
}
```
