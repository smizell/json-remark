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
