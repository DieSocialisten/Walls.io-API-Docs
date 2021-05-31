# PUT `/posts/*{postId}*`

Changes a single post's visibility status, highlighting, language, or spam status. The post is identified by its Walls.io post id.

This endpoint allows you to perform most actions you can do in the "Posts" tab of your Wall's "Moderation" page. One notable exception is the "Block user" (or "Whitelist user") feature which is done via the [POST api/user_blacklist](#post-apiuser_blacklistjson) (or [POST api/user_whitelist](#post-apiuser_whitelistjson)) endpoint.

You can perform multiple actions at once by setting multipe parameters.

#### Example request
```bash
curl -X PUT \
  https://api.walls.io/v1/posts/17181206.json \
  -H 'content-type: application/x-www-form-urlencoded' \
  -d 'access_token=<ACCESS_TOKEN>&is_highlighted=1&status=1&language=en'
```

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `is_highlighted`: Set this to `1` if the post should be highlighted, or `0` to remove an existing highlight flag.
- `status`: Set this to `1` to show a hidden post, or `0` to hide a visible post.
- `language`: Set this to change the language of a post. The language is passed as a two-letter ISO 639-1 language code. You can also remove a post's language completely by passing an empty string. To find out which languages are supported by the Walls.io API simply set this to a random value; the response will contain a list of all valid language codes.
- `report_spam`: Set this to `1` to report this post for spam, or `0` to remove the spam status from a post that was incorrectly reported as spam.


#### Example response

```json
{
  "status": "success",
  "query": {
    "postId": 17181206
  },
  "current_time": 1408954568,
  "data": {
    // ... the full updated post
  }
}
```
