---
layout: docs
---
# Tasks

## GET `tasks/{agenda}`
Retrieves the list of tasks in an agenda.

### Request Parameters
This endpoint does not accept any parameters.

### Response
A JSON array with objects representing [tasks](#get-tasksagendaid).

**_NOTE:_** This endpoint represents tags using their IDs (see the example).

### Example

#### Request
```
GET https://api.agendas.co/api/v1/tasks/-abcdefgh00
```

#### Response
```javascript
[
  {
    "id": "-a123456789",
    "name": "Task 1",
    "completed": true,
    "deadline": "1984-01-24T05:00:00.000Z",
    "deadlineTime": true,
    "repeat": "day",
    "repeatEnds": "1984-01-25T05:00:00.000Z",
    "tags": {
      "-a123456000": true
    },
    "priority": 1,
    "notes": "Hello, world!"
  },
  {
    "id": "-a123456800",
    "name": "Task 2"
  }
]
```

## POST `tasks/{agenda}`
Creates a new task in an agenda.

### Request Parameters
This endpoint does not accept any parameters.

### Request Body

| Key | Type | Required? | Description |
| --- | --- | --- | --- |
| `name` | string | No | The name of the task. |
| `completed` | bool | No | `true` if the task has been completed. |
| `deadline` | date | No | The deadline of the task. |
| `deadlineTime` | bool | No | `true` if the task's deadline has a time. |
| `repeat` | string | No | A string corresponding to a [repeat](#repeats). |
| `repeatEnds` | date | No | The date when the task should stop repeating. |
| `tags` | array | No | An array containing the IDs of the tags this task belongs to. |
| `priority` | number | No | The priority of the task. |
| `notes` | string | No | The notes for the task. |

### Response
A JSON object with these parameters:

| Key | Type | Description |
| --- | --- | --- |
| `ok` | bool | Whether the operation succeeded. |
| `id` | string | The ID of the new task. |

### Example

#### Request
```
POST https://api.agendas.co/api/v1/tasks/-abcdefgh00
```
```javascript
{
  "name": "New Task"
}
```

#### Response
```javascript
{
  "ok": true,
  "id": "-abcdefghijk"
}
```

## GET `tasks/{agenda}/{id}`
Gets the task with a specified ID.

### Request Parameters
This endpoint does not accept any parameters.

### Response
A JSON object with these paramters:

| Key | Type | Description |
| --- | --- | --- |
| `name` | string | The name of the task. |
| `completed` | bool | `true` if the task has been completed. |
| `deadline` | date | The deadline of the task. |
| `deadlineTime` | bool | `true` if the task's deadline has a time. |
| `repeat` | string | A string corresponding to a [repeat](#repeats). |
| `repeatEnds` | date | The date when the task should stop repeating. |
| `tags` | array | An array containing the tags this task belongs to. *See [Tags](tags#get-tagsagendaid)* |
| `priority` | number | The priority of the task. |
| `notes` | string | The notes for the task. |

### Example

#### Request
```
GET https://api.agendas.co/api/v1/tasks/-abcdefgh00/-a123456789
```

#### Response
```javascript
{
  "id": "-a123456789",
  "name": "Task 1",
  "completed": true,
  "deadline": "1984-01-24T05:00:00.000Z",
  "deadlineTime": true,
  "repeat": "day",
  "repeatEnds": "1984-01-25T05:00:00.000Z",
  "tags": [{
    "id": "-a123456000",
    "name": "Tag",
    "color": "blue-A700"
  }],
  "priority": 1,
  "notes": "Hello, world!"
}
```

## PUT `tasks/{agenda}/{id}`
Overwrites the task with a specified ID.

This endpoint will remove any properties that are not in the request body.

### Request Parameters
This endpoint does not accept any parameters.

### Request Body

| Key | Type | Required? | Description |
| --- | --- | --- | --- |
| `name` | string | No | The name of the task. |
| `completed` | bool | No | `true` if the task has been completed. |
| `deadline` | date | No | The deadline of the task. |
| `deadlineTime` | bool | No | `true` if the task's deadline has a time. |
| `repeat` | string | No | A string corresponding to a [repeat](#repeats). |
| `repeatEnds` | date | No | The date when the task should stop repeating. |
| `tags` | array | No | An array containing the IDs of the tags this task belongs to. |
| `priority` | number | No | The priority of the task. |
| `notes` | string | No | The notes for the task. |

### Response
A JSON object with these parameters:

| Key | Type | Description |
| --- | --- | --- |
| `ok` | string | Whether the operation succeeded. |

### Example

#### Request
```
PUT https://api.agendas.co/api/v1/tasks/-abcdefgh00/-a123456789
```
```javascript
{
  "name": "A Task",
  "tags": ["-a123456000"]
}
```

#### Response
```javascript
{
  "ok": true
}
```

## PATCH `tasks/{agenda}/{id}`
Updates the task with a specified ID.

This API endpoint only updates properties defined in the request body. To remove a property using this endpoint, set it to `null`.

### Request Parameters
This endpoint does not accept any parameters.

### Request Body

| Key | Type | Required? | Description |
| --- | --- | --- | --- |
| `name` | string | No | The name of the task. |
| `completed` | bool | No | `true` if the task has been completed. |
| `deadline` | date | No | The deadline of the task. |
| `deadlineTime` | bool | No | `true` if the task's deadline has a time. |
| `repeat` | string | No | A string corresponding to a [repeat](#repeats). |
| `repeatEnds` | date | No | The date when the task should stop repeating. |
| `tags` | array | No | An array containing the IDs of the tags this task belongs to. |
| `priority` | number | No | The priority of the task. |
| `notes` | string | No | The notes for the task. |

### Response
A JSON object with these parameters:

| Key | Type | Description |
| --- | --- | --- |
| `ok` | string | Whether the operation succeeded. |

### Example

#### Request
```
PATCH https://api.agendas.co/api/v1/tasks/-abcdefgh00/-a123456789
```
```javascript
{
  "name": "Generic Task",
  "deadlineTime": false,
  "repeatEnds": null
}
```

#### Response
```javascript
{
  "ok": true
}
```

## DELETE `tasks/{agenda}/{id}`
Deletes the task with a specified ID.

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
DELETE https://api.agendas.co/api/v1/tasks/-abcdefgh00/-a123456789
```

#### Response
```javascript
{
  "ok": true
}
```

## Repeats

| `repeats` | Repeat Every |
| --- | --- |
| undefined | No Repeat |
| `day` | Day |
| `weekday` | Weekday (Monday-Friday) |
| `week` | Week |
| `2-weeks` | Other Week |
| `month` | Month |
| `year` | Year |

## Next Steps
[Organize tasks using tags.](tags)
