# PUT `/posts/{postId}`

#### Set the state of a single post, pin it, or change its language

The post is identified by its Walls.io post id.

This endpoint allows you to perform most actions you can do in the “Posts” tab of your Wall's “Moderation” page. 
One notable exception are the “Block user” and “Whitelist user” features, which are done via the [**POST** `/user_blacklist`][POST /user_blacklist] and [**POST** `/user_whitelist`][POST /user_whitelist]) endpoints.

You can perform multiple actions at once by setting multiple parameters.

## Example request
```bash
curl -X PUT \
  https://api.walls.io/v1/posts/17181206 \
  -H 'content-type: application/x-www-form-urlencoded' \
  -d 'access_token=<ACCESS_TOKEN>&is_pinned=1&state=visible&language=en'
```

## Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `is_pinned`: Set this to `1` if the post should be pinned to top, or `0` to remove that flag.
- `state`: The state to put the post into, like the buttons in the Moderation page. [Post States] Only on walls with the new moderation.
  - `visible` shows the post, `hidden` hides it. This is your decision as a moderator: it stays until you change it, whatever the Wall's filters say.
  - `review` moves the post to "Needs review" until you decide.
  - `trashed` moves the post to the trash. If the Wall deletes trashed posts after 30 days, this deletes the post for good. Posts created via [**POST** `/posts`][POST /posts] and polls can't be trashed; the call returns a `400`.
  - Setting `visible`, `hidden` or `review` on a trashed post takes it out of the trash.
- `status` *(deprecated, removed on March 1, 2027)*: The old spelling of `state`: `1` is `state=visible`, `0` is `state=hidden`. Use `state` instead. Sending both with different meanings returns a `400`.
- `language`: Set this to change the language of a post. The language is passed as a two-letter ISO 639-1 language code. You can also remove a post's language completely by passing an empty string. To find out which languages are supported by the Walls.io API simply set this to a random value; the response will contain a list of all valid language codes.


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
[POST /posts]: POST_posts.md "Add a new Native Post"
[Post States]: ../Post_States.md "List of possible post states"
