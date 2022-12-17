# JSON Remark

**Version**: 2022-12-17-draft

This is currently a draft and may change considerably.

## Overview

JSON Remark provides a standard way to annotate JSON documents with additional data. When we use formats like OpenAPI and AsyncAPI, we often have tools that need to provide additional data about those documents. This includes adding comments and feedback, providing linting feedback using tools like Spectral, including parser errors, and adding test results. JSON Remark tries to standard this so all of these tools can use the same format.

## Specification

### Example

Here we see an example that includes remarks from a made-up linting tool. The tool provides a URL that identifies itself as `https://example.com/linting-tool`. It includes remarks with types that defining what can be found in `data`. This example has a linting remark with a level of `error` for a given path, which in this case is the property of a schema.

```json
{
  "version": "2022-12-17-draft",
  "origin": "https://example.com/linting-tool",
  "remarks": [
    {
      "path": "#/components/schemas/Person/properties/firstName",
      "for": "key",
      "type": "https://example.com/definition/linting",
      "data": {
        "description": "Property name MUST be snake case",
        "level": "error",
        "rule": "json-property-snake-case"
      }
    }
  ]
}
```

### Schema

#### JSON Remark Document

- `version` - the version of the JSON Remark document.
- `origin` - a URL specifying the origin of the remarks. This MUST act as an ID for the origin and a MAY act as a resolvable URL that defines documentation about the originating tool.
- `remarks` (Array[Remark]) - an array of [Remark](#Remark) objects

#### Remark

- `path` - a [JSON Pointer](https://www.rfc-editor.org/rfc/rfc6901) to the item in the JSON document to which the remark pertains
- `for` (optional) (enum: `key`, `value`, `all`) (default: `value`) - the specific part of the path to which the remark pertains. This may be the `key`, the `value` found at the path, or the full key-value.
- `type` - a URL specifying the type of the remark, which provides a specification for what can be found in `data`. This MUST act as an ID for the remark type and a MAY act as a resolvable URL that defines documentation about the type itself.
- `data` (object) - an object that contains remark data as defined by the `type`
