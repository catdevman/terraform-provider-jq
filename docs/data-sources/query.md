---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "jq_query Data Source - terraform-provider-jq"
subcategory: ""
description: |-
  Use this data source to execute a jq query against a JSON formatted string.
---

# jq_query (Data Source)

Use this data source to execute a jq query against a JSON formatted string.

## Example Usage
```hcl
data "jq_query" "example" {
    data = "{\"a\": \"b\"}"
    query = ".a"
}

output "example" {
    value = data.jq_query.example.result
}
```

This will output:
```sh
Outputs:

example = "\"b\""
```

### HCL Compatibility

The jq operates on json formatted strings. Fortunately, terraform provides the `jsonencode()` and `jsondecode()` functions for easily converting back and forth between HCL and json strings.

The above example in pure HCL:

```hcl
data "jq_query" "example" {
    data = jsonencode({a = "b"})
    query = ".a"
}

output "example" {
    value = jsondecode(data.jq_query.example.result)
}
```

This will output:
```sh
Outputs:

example = "b"
```

## Argument Reference

- `data` - (Required) A JSON formatted string containing the data you would like to query. You can use jsonencode() to convert an HCL map or object into a queryable string.
- `query` - (Required) A jq query string.

## Attributes Reference

- `result` - A JSON formatted string containing the result of the query.

