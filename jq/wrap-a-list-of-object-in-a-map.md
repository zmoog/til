# Wrap a list of object in a map

The source document contains a list of objects:

```shell
$ cat iphones.json
[
  {
    "name": "iPhone 13 Pro Max 512GB ricondizionato - Grafite (senza SIM)",
    "family": "iphone",
    "store": "it",
    "url": "https://www.apple.com/it/shop/product/FLLF3QL/A/iphone-13-pro-max-512gb-ricondizionato-grafite-senza-sim",
    "price": 1389,
    "previous_price": 1639,
    "savings_price": 250,
    "saving_percentage": 0.1525320317266626,
    "model": "FLLF3QL"
  },
  {
    "name": "iPhone 13 Pro Max 1TB ricondizionato - Grafite (senza SIM)",
    "family": "iphone",
    "store": "it",
    "url": "https://www.apple.com/it/shop/product/FLLK3QL/A/iphone-13-pro-max-1tb-ricondizionato-grafite-senza-sim",
    "price": 1589,
    "previous_price": 1869,
    "savings_price": 280,
    "saving_percentage": 0.149812734082397,
    "model": "FLLK3QL"
  }
]
```

But I need a map because I want to use the data with jinja-cli.

Let's wrap it!

```shell
$ jq '{"entries": .}' iphones.json
{
  "entries": [
    {
      "name": "iPhone 13 Pro Max 512GB ricondizionato - Grafite (senza SIM)",
      "family": "iphone",
      "store": "it",
      "url": "https://www.apple.com/it/shop/product/FLLF3QL/A/iphone-13-pro-max-512gb-ricondizionato-grafite-senza-sim",
      "price": 1389,
      "previous_price": 1639,
      "savings_price": 250,
      "saving_percentage": 0.1525320317266626,
      "model": "FLLF3QL"
    },
    {
      "name": "iPhone 13 Pro Max 1TB ricondizionato - Grafite (senza SIM)",
      "family": "iphone",
      "store": "it",
      "url": "https://www.apple.com/it/shop/product/FLLK3QL/A/iphone-13-pro-max-1tb-ricondizionato-grafite-senza-sim",
      "price": 1589,
      "previous_price": 1869,
      "savings_price": 280,
      "saving_percentage": 0.149812734082397,
      "model": "FLLK3QL"
    }
  ]
}
```
