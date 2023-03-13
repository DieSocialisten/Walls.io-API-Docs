# DELETE `/user_whitelist`

#### Remove a user from this wall's whitelist 

This is an undo of the [__POST__ `/user_whitelist`][POST /user_whitelist] method.


## Example request
```bash
curl -X DELETE \
  https://api.walls.io/v1/user_whitelist \
  -H 'content-type: application/x-www-form-urlencoded' \
  -d 'access_token=<ACCESS_TOKEN>&network=facebook&external_user_id=123456'
```

## Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `network` *(required)*: The social network of the user. Find it in any [__GET__ `/posts`][GET /posts] response in the `type` field. [Post Types]
- `external_user_id` *(required)*: The user's ID on the social network. Find it in any [__GET__ `/posts`][GET /posts] in the `external_user_id` field.


[POST /user_whitelist]: POST_user_whitelist.md "Add a user to this wall's whitelist"
[GET /posts]: GET_posts.md
[Post Types]: ../Post_Types.md "List of possible post types"
