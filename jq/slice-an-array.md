# Slice an array

I have an array with three items and I want to pick only the first two elements.

## Example

```shell
$ axios --output-format json grades list
[
  {
    "date": "23/03/2023",
    "subject": "ARTE E IMMAGINE",
    "kind": "Grafico",
    "value": "9",
    "teacher": "Pagliarulo Veronica",
    "comment": "Concorso LAV"
  },
  {
    "date": "20/03/2023",
    "subject": "STORIA",
    "kind": "Orale",
    "value": "10",
    "teacher": "Novelli Cristina",
    "comment": ""
  },
  {
    "date": "17/03/2023",
    "subject": "ITALIANO",
    "kind": "Orale",
    "value": "8",
    "teacher": "Rapalino Lara",
    "comment": "Presentazione orale del libro letto"
  }
]
```

```shell
$ axios --output-format json grades list | jq '.[:2]'
[
  {
    "date": "23/03/2023",
    "subject": "ARTE E IMMAGINE",
    "kind": "Grafico",
    "value": "9",
    "teacher": "Pagliarulo Veronica",
    "comment": "Concorso LAV"
  },
  {
    "date": "20/03/2023",
    "subject": "STORIA",
    "kind": "Orale",
    "value": "10",
    "teacher": "Novelli Cristina",
    "comment": ""
  }
]
```

## References

- https://stackoverflow.com/questions/56028679/how-to-filter-array-and-slice-results-with-jq
