# Map an array of objects

Given this source array:

```json
[
  {
    "evtId": 757725,
    "evtCode": "AGNT",
    "evtDatetimeBegin": "2023-04-24T08:00:00+02:00",
    "evtDatetimeEnd": "2023-04-25T21:00:00+02:00",
    "notes": "NO LEZIONE",
    "authorName": "DICEMBRE ELISA",
    "subjectDesc": ""
  }
]
```

I want to turn it into the following:

```json
{
  "items": [
    {
      "evtDate": "2023-04-25",
      "notes": "NO LEZIONE",
      "authorName": "DICEMBRE ELISA",
      "subjectDesc": ""
    }
  ]
}
```

Here's the jq expression to do it (pasting the JSON document from the macOS pasteboard with the `pbpaste` command):

```shell
$ pbpaste | jq 'map({evtDate: .evtDatetimeEnd[:10], notes, authorName, subjectDesc}) | {"agenda": . | .[:5]}'
{
  "agenda": [
    {
      "evtDate": "2023-04-25",
      "notes": "NO LEZIONE",
      "authorName": "DICEMBRE ELISA",
      "subjectDesc": ""
    }
  ]
}
```

The `map()` function is powerful and lets you define your result with precision and no effort. In this case, I dropped a few fields and added `evtData` using the `.evtDatetimeEnd[:10]` as its value.

In the last part, I wrap the array in an `agenda` field, picking only the first five items.

I love this tool so much.
