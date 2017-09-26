---
layout: docs
---
# Agendas

## GET `agendas`
Retrieves the list of agendas that the user has access to, in JSON format.

### Request Parameters
This endpoint does not accept any parameters.

### Response
A JSON array with objects representing [agendas](#get-agendasid).

### Example

#### Request
```
GET https://api.agendas.co/api/v1/agendas
```

#### Response
```javascript
[
  {
    "id": "-abcdefgh00",
    "name": "Agenda 1"
  },
  {
    "id": "-abcdefgh42",
    "name": "Agenda 2"
  }
]
```

## POST `agendas`
Creates a new agenda.

### Request Parameters
This endpoint does not accept any parameters.

### Request Body

| Key | Type | Required? | Description |
| --- | --- | --- | --- |
| `name` | string | Yes | The name of the agenda. |

### Response
A JSON object with these paramters:

| Key | Type | Description |
| --- | --- | --- |
| `ok` | bool | Whether the operation succeeded. |
| `id` | string | The ID of the new agenda. |

### Example

#### Request
```
POST https://api.agendas.co/api/v1/agendas
```
```javascript
{
  "name": "New Agenda"
}
```

#### Response
```javascript
{
  "ok": true,
  "id": "-abcdefghijk"
}
```

## GET `agendas/{id}`
Gets the agenda with a specified ID.

### Request Parameters
This endpoint does not accept any parameters.

### Response
A JSON object with these paramters:

| Key | Type | Description |
| --- | --- | --- |
| `id` | string | The agenda's ID. |
| `name` | string | The name of the agenda. |

### Example

#### Request
```
GET https://api.agendas.co/api/v1/agendas/-abcdefgh00
```

#### Response
```javascript
{
  "id": "-abcdefgh00",
  "name": "Agenda 1"
}
```

## PUT `agendas/{id}`
Overwrites the agenda with a specified ID.

This endpoint will remove any properties that are not in the request body.

### Request Parameters
This endpoint does not accept any parameters.

### Request Body

| Key | Type | Required? | Description |
| --- | --- | --- | --- |
| `name` | string | Yes | The name of the agenda. |

### Response
A JSON object with these parameters:

| Key | Type | Description |
| --- | --- | --- |
| `ok` | string | Whether the operation succeeded. |

### Example

#### Request
```
PUT https://api.agendas.co/api/v1/agendas/-abcdefgh00
```
```javascript
{
  "name": "An Agenda"
}
```

#### Response
```javascript
{
  "ok": true
}
```

## PATCH `agendas/{id}`
Updates the agenda with a specified ID.

This API endpoint only updates properties defined in the request body. To remove a property using this endpoint, set it to `null`.

### Request Parameters
This endpoint does not accept any parameters.

### Request Body

| Key | Type | Required? | Description |
| --- | --- | --- | --- |
| `name` | string | No | The name of the agenda. |

### Response
A JSON object with these parameters:

| Key | Type | Description |
| --- | --- | --- |
| `ok` | string | Whether the operation succeeded. |

### Example

#### Request
```
PATCH https://api.agendas.co/api/v1/agendas/-abcdefgh00
```
```javascript
{
  "name": "Another Agenda"
}
```

#### Response
```javascript
{
  "ok": true
}
```

## DELETE `agendas/{id}`
Deletes the agenda with a specified ID.

This API endpoint will delete **all** tasks and tags in the agenda.

### Request Parameters
This endpoint does not accept any parameters.

### Response
A JSON object with these parameters:

| Key | Type | Description |
| --- | --- | --- |
| `ok` | string | Whether the operation succeeded. |

### Example

#### Request
```
DELETE https://api.agendas.co/api/v1/agendas/-abcdefgh00
```

#### Response
```javascript
{
  "ok": true
}
```

## Next Steps
* [Create, update, and delete tasks.](tasks)
* [Organize tasks with tags.](tags)
