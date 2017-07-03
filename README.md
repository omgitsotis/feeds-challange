# Feeds Coding Challenge

## Rules

* Write in Golang
* Use any libraries but please justify their use
* Use any dependancy management tool (if required)
* Only spend a maximum of 2 hours on this task

## The challenge

Import all of the valid events and markets from the feed API taking into account
inconsistent data.

To run the feed server `make run-feed`. Read the [documentation](feed/README.md).

POST the formatted events to a customisable endpoint which is passed through as
the following environment variable: `STORE_ADDR`.

For example you might start the program with:
```
STORE_ADDR=localhost:8001/event/add ./bin/event_importer
```

if your compile binary is called `event_importer` and is in the `/bin` folder.

Before POSTing the data to the store, validate that it is correct. The same
validation will be run at the store and incorrect data will rejected.

Some data will be formatted inconsistently so ensure your program can handle this.

Not all ID's will exist.

## Feed Server

Check out the [documentation](feed/README.md)

## Models

### Event

All fields are required

| Field | Json Field | Format               |
| ----- | ---------- | -------------------- |
| ID    | id         | string               |
| Name  | name       | string               |
| Time  | time       | timestamp (RFC 3339) |
| Markets | markets | Array |

### Market

All fields are required

| Field | Json Field | Format               |
| ----- | ---------- | -------------------- |
| ID    | id         | string               |
| Type  | type       | string               |
| Options | options | Array |

### Options

All fields are required.

| Field | Json Field | Format               |
| ----- | ---------- | -------------------- |
| ID    | id         | string               |
| Name  | name       | string               |
| Numerator | num | int |
| Denominator | den | int |

### Example
The following example is formatted correctly to be accepted by the store.
```json
{
  "id": "1",
  "name": "Southampton v Bournemouth",
  "time": "2006-01-02T15:04:05Z07:00",
  "markets": [
    {
      "id": "101",
      "type": "win-draw-win",
      "options": [
        {
          "id": "10101",
          "name": "Southampton",
          "num": 1,
          "den": 5
        },
        {
          "id": "10102",
          "name": "Draw",
          "num": 3,
          "den": 5
        },
        {
          "id": "10103",
          "name": "Bournemouth",
          "num": 4,
          "den": 5
        }
      ]
    }
  ]
}
```
