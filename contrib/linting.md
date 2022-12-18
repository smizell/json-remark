# JSON Remark for Linting

**WORK IN PROGRESS. THIS IS EXPERIMENTAL. WILL CREATE A BETTER PLACE FOR THESE LATER**

Type URL: `https://github.com/smizell/json-remark/blob/main/contrib/linting.md`

This defines a JSON Remark Type to be used by JSON linters. A linter should define a URL for `origin` for the full JSON Remark document so consumers can follow the link to understand how the linter works.

## Data definition

- `level` (enum: `error`, `warn`, `info`, `hint`) (default: `warn`) - the severity level of the linting remark
- `rule_name` - the name of the rule
- `line` (optional) - the optional line number of the item with the linting issue
- `column` (optional) - the optional column number of the item with the linting issue
- `rule_docs` (optional) - an optional URL to the docs for the rule

## Example

This describes one of the errors shown in the [Spectral docs](https://docs.stoplight.io/docs/spectral/038632fdf0d1a-continuous-integration#circleci).

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
