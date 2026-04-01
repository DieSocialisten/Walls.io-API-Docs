# PUT `/posts/{postId}`

#### Change a single post's visibility status, pinned, language, or spam status

The post is identified by its Walls.io post id.

This endpoint allows you to perform most actions you can do in the “Posts” tab of your Wall's “Moderation” page. 
One notable exception are the “Block user” and “Whitelist user” features, which are done via the [**POST** `/user_blacklist`][POST /user_blacklist] and [**POST** `/user_whitelist`][POST /user_whitelist]) endpoints.

You can perform multiple actions at once by setting multiple parameters.

## Example request
```bash
curl -X PUT \
  https://api.walls.io/v1/posts/17181206 \
  -H 'content-type: application/x-www-form-urlencoded' \
  -d 'access_token=<ACCESS_TOKEN>&is_pinned=1&status=1&language=en'
```

## Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `is_pinned`: Set this to `1` if the post should be pinned to top, or `0` to remove that flag.
- `status`: Set this to `1` to show a hidden post, or `0` to hide a visible post.
- `language`: Set this to change the language of a post. The language is passed as a two-letter ISO 639-1 language code. You can also remove a post's language completely by passing an empty string. To find out which languages are supported by the Walls.io API simply set this to a random value; the response will contain a list of all valid language codes.
- `report_spam`: Set this to `1` to report this post for spam, or `0` to remove the spam status from a post that was incorrectly reported as spam.


## Example response

```JsonC
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

[POST /user_blacklist]: POST_user_blacklist.md "Blacklist a user"
[POST /user_whitelist]: POST_user_whitelist.md "Whitelist a user"
