# JSON Remark

**Version**: `2022-12-17-draft`

This is currently a draft and may change considerably. Please do not use yet.

## Overview

JSON Remark provides a standard way to annotate JSON documents with additional data. When we use formats like OpenAPI and AsyncAPI, we often have tools that need to provide additional data about those documents. This includes adding comments and feedback, providing linting feedback using tools like Spectral, including parser errors, and adding test results. JSON Remark tries to standard this so all of these tools can use the same format.

## Specification

### Examples

#### Linting error example

Here we see remarks from a made-up linting tool. The tool provides an `origin` URL that identifies itself as `https://example.com/linting-tool`. The `type` defines what can be found in `data`. The `more` URL links back to the full linting report. The `data` is shows this is a linting remark with a level of `error` for a given path, which in this case is the property of a schema.

```json
{
  "version": "2022-12-17-draft",
  "origin": "https://stoplight.io/open-source/spectral",
  "remarks": [
    {
      "path": "#/paths/~1services~1/{addonName}/get/responses/200/schema",
      "for": "value",
      "type": "https://github.com/smizell/json-remark/main/contrib/linting.md",
      "text": "$ref cannot be placed next to any other properties",
      "data": {
        "level": "error",
        "rule_name": "org.spectral.no-$ref-siblings",
        "line": "891",
        "column": "19"
      }
    }
  ]
}
```

#### Comment example

This shows remarks from a tool that allows for commenting on an OpenAPI document. The remark includes the comment `text` and information about the commentor. In this example, the person is commenting on an HTTP method in the OpenAPI document. The `type` defines what can be found in `data`.

Note: the slashes in the URL path are converted to `~1` according to the [JSON Pointer specification](https://www.rfc-editor.org/rfc/rfc6901)

```json
{
  "version": "2022-12-17-draft",
  "origin": "https://example.com/commenting-tool",
  "remarks": [
    {
      "type": "https://github.com/smizell/json-remark/blob/main/contrib/commenting.md",
      "path": "#/paths/~1customers~1{id}/put",
      "text": "Should this be a PATCH instead of a PUT?",
      "data": {
        "id": "https://example.com/comments/1234",
        "user_profile": "https://example.com/profiles/smizell",
        "name": "Stephen Mizell"
      }
    },
    {
      "type": "https://github.com/smizell/json-remark/blob/main/contrib/commenting.md",
      "path": "#/paths/~1customers~1{id}/put",
      "text": "Let's leave it as PUT.",
      "data": {
        "id": "https://example.com/comments/5678",
        "user_profile": "https://example.com/profiles/jdoe",
        "name": "Jane Doe",
        "replying_to": "https://example.com/comments/1234"
      }
    }
  ]
}
```

### Schema

#### JSON Remark Document

- `version` - the version of the JSON Remark document.
- `origin` - a URL specifying the origin of the remarks. This MUST act as an ID for the origin and a MAY act as a resolvable URL that defines documentation about the originating tool.
- `more` - a URL linking to a place that provides additional data for the entire JSON Remark document
- `remarks` (Array[Remark]) - an array of [Remark](#Remark) objects

#### Remark

- `type` - a URL specifying the type of the remark, which provides a specification for what can be found in `data`. This must act as an ID for the remark type and may act as a resolvable URL that defines documentation about the type itself.
- `path` - a [JSON Pointer](https://www.rfc-editor.org/rfc/rfc6901) to the item in the JSON document to which the remark pertains
- `text` (optional) - human-readable text for the remark
- `for` (optional) (enum: `key`, `value`, `all`) (default: `key`) - the specific part of the path to which the remark pertains. This may be the `key`, the `value` found at the path, or the full key-value.
- `data` (object, optional) - an object that contains remark data as defined by the `type`

## Contributed JSON Remark Types

- [Linting](./contrib/linting.md)
- [Commenting](./contrib/commenting.md)
