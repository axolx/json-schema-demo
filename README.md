# A minimal demo for using JSON Schema to validate JSON and YAML

## Sample JSON document

```JSON
{
  "productId": 123,
  "productName": "Boomerang",
  "price": 12.50,
  "tags": [ "australia", "fun" ]
}
```

## Sample JSON Schema

```JSON
{
    "$schema": "http://json-schema.org/draft-06/schema#",
    "title": "Product",
    "description": "A product in the catalog",
    "type": "object",
    "properties": {
        "productId": {
            "description": "The unique identifier for a product",
            "type": "integer"
        },
        "productName": {
            "description": "Name of the product",
            "type": "string"
        },
        "price": {
            "description": "The price of the product",
            "type": "number",
            "exclusiveMinimum": 0
        },
        "tags": {
            "description": "Tags for the product",
            "type": "array",
            "items": {
                "type": "string"
            },
            "minItems": 1,
            "uniqueItems": true
        }
    },
    "required": [ "productId", "productName", "tags" ]
}
```

## Validating JSON against a schema in the command line

```console
npm install pajv
alias pajv=./node_modules/.bin/pajv
pajv validate -s schema.json -d document.json
```

## Validating YAML documents

pajv also validates YAML documents:

```YAML
---
productId: 123
productName: "Boomerang"
price: 12.5
tags:
  - "australia"
  - "fun"
```

```console
    pajv validate -s schema.json -d document.yaml
```

## Reference

- [Understanding JSON Schema](https://json-schema.org/understanding-json-schema/index.html)
