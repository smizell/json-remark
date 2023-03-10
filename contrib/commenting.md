# JSON Remark for Commenting

**WORK IN PROGRESS. THIS IS EXPERIMENTAL. WILL CREATE A BETTER PLACE FOR THESE LATER**

Type URL: `https://github.com/smizell/json-remark/blob/main/contrib/commenting.md`

This defines a JSON Remark Type to be used to comments to JSON documents. The `text` acts as the content of the comment.

## Data definition

- `name` - the name of the commentor
- `id` (optional) - an ID for the comment, which may be any value but should be a URL
- `user_profile` (optional) - a URL to the user profile of the commentor
- `avatar` (optional) - a URL to the avatar for the user
- `replying_to` (optional) - an ID for the parent comment when this comment is a reply

## Example

This example shows a thread of comments for an OpenAPI document found at `http://example.com/openapi-docs/1234`. These comments were produced by a service at `https://example.com/commenting-tool`. There are two comments: the first is a parent comment and the second is a reply to that comment. Each comment has a URL as the `id`.

```json
{
  "version": "2022-12-17-draft",
  "author": "https://example.com/commenting-tool",
  "origin": "http://example.com/openapi-docs/1234",
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
