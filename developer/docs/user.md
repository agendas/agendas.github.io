---
layout: docs
---

# User
A collection of API endpoints that allow you to retrieve information about a user.

## GET `email`
Retrieves the user's email. Requires the `email` scope.

### Request Parameters
This endpoint does not accept any parameters.

### Response
A JSON object with these parameters:

| Key | Type | Description |
| `email` | string | The user's email. |

### Example

#### Request
```
GET https://api.agendas.co/api/v1/email
```

#### Response
```javascript
{
  "email": "generic.user@example.com"
}
```

## GET `username`
Retrieves the user's Agendas username. Requires the `username-read` scope.

### Request Parameters
This endpoint does not accept any parameters.

### Response
A JSON object with these parameters:

| Key | Type | Description |
| `username` | string | The user's username. May not be present if the user does not have a username. |

### Example

#### Request
```
GET https://api.agendas.co/api/v1/email
```

#### Response
```javascript
{
  "username": "genericuser"
}
```

## Next Steps
[Manage a user's agendas](agendas).
