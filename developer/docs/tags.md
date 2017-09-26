---
layout: docs
---
# Tags

## GET `tags/{agenda}`
Retrieves the list of tags in an agenda.

### Request Parameters
This endpoint does not accept any parameters.

### Response
A JSON array with objects representing [tags](#get-tagsagendaid).

**_NOTE:_** This endpoint does not include tasks in the response.

### Example

#### Request
```
GET https://api.agendas.co/api/v1/tags/-abcdefgh00
```

#### Response
```javascript
[
  {
    "id": "-a123456000",
    "name": "Tag",
    "color": "blue-A700"
  },
  {
    "id": "-a123456001",
    "name": "Another Tag",
    "color": "red"
  }
]
```

## POST `tags/{agenda}`
Creates a new tag in an agenda.

### Request Parameters
This endpoint does not accept any parameters.

### Request Body

| Key | Type | Required? | Description |
| --- | --- | --- | --- |
| `name` | string | Yes | The name of the tag. |
| `color` | string | No | The color of the tag. [See the colors](#colors) |

### Response
A JSON object with these parameters:

| Key | Type | Description |
| --- | --- | --- |
| `ok` | bool | Whether the operation succeeded. |
| `id` | string | The ID of the new tag. |

### Example

#### Request
```
POST https://api.agendas.co/api/v1/tags/-abcdefgh00
```
```javascript
{
  "name": "New Tag"
}
```

#### Response
```javascript
{
  "ok": true,
  "id": "-abcdefghijk"
}
```

## GET `tags/{agenda}/{id}`
Gets the tag with a specified ID.

### Request Parameters
This endpoint does not accept any parameters.

### Response
A JSON object with these paramters:

| Key | Type | Description |
| --- | --- | --- |
| `name` | string | The name of the tag. |
| `color` | string | The color of the tag. [See the colors](#colors) |
| `tasks` | array | A list of this tag's [tasks](tasks#get-tasksagendaid). |

### Example

#### Request
```
GET https://api.agendas.co/api/v1/tags/-abcdefgh00/-a123456000
```

#### Response
```javascript
{
  "id": "-a123456000",
  "name": "Tag",
  "color": "blue-A700",
  "tasks": [
    {
      "id": "-a123456789",
      "name": "Task 1",
      "completed": true,
      "deadline": "1984-01-24T05:00:00.000Z",
      "deadlineTime": true,
      "repeat": "day",
      "repeatEnds": "1984-01-25T05:00:00.000Z",
      "tags": ["-a123456000"],
      "priority": 1,
      "notes": "Hello, world!"
    }
  ]
}
```

## PUT `tags/{agenda}/{id}`
Overwrites the tag with a specified ID.

This endpoint will remove any properties that are not in the request body.

### Request Parameters
This endpoint does not accept any parameters.

### Request Body

| Key | Type | Required? | Description |
| --- | --- | --- | --- |
| `name` | string | Yes | The name of the tag. |
| `color` | string | No | The color of the tag. [See the colors](#colors) |

### Response
A JSON object with these parameters:

| Key | Type | Description |
| --- | --- | --- |
| `ok` | string | Whether the operation succeeded. |

### Example

#### Request
```
PUT https://api.agendas.co/api/v1/tags/-abcdefgh00/-a123456000
```
```javascript
{
  "name": "A Tag",
  "color": "blue"
}
```

#### Response
```javascript
{
  "ok": true
}
```

## PATCH `tags/{agenda}/{id}`
Updates the tag with a specified ID.

This API endpoint only updates properties defined in the request body. To remove a property using this endpoint, set it to `null`.

### Request Parameters
This endpoint does not accept any parameters.

### Request Body

| Key | Type | Required? | Description |
| --- | --- | --- | --- |
| `name` | string | Yes | The name of the tag. |
| `color` | string | No | The color of the tag. [See the colors](#colors) |

### Response
A JSON object with these parameters:

| Key | Type | Description |
| --- | --- | --- |
| `ok` | string | Whether the operation succeeded. |

### Example

#### Request
```
PATCH https://api.agendas.co/api/v1/tags/-abcdefgh00/-a123456000
```
```javascript
{
  "color": "indigo-A400"
}
```

#### Response
```javascript
{
  "ok": true
}
```

## DELETE `tags/{agenda}/{id}`
Deletes the tag with a specified ID.

This endpoint will not delete the tag's tasks.

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
DELETE https://api.agendas.co/api/v1/tags/-abcdefgh00/-a123456000
```

#### Response
```javascript
{
  "ok": true
}
```

## Colors

Colors are based on the [Material Design color palettes](https://material.io/guidelines/style/color.html#color-color-palette).

Here's a list of the colors Agendas supports:
* `red`
* `pink`
* `purple`
* `deep-purple`
* `indigo`
* `blue`
* `light-blue`
* `cyan`
* `teal`
* `green`
* `light-green`
* `lime`
* `yellow`
* `amber`
* `orange`
* `deep-orange`
* `brown`
* `grey`
* `blue-grey`
* `black`

## See also

[Create, update, and delete tasks.](tasks)
