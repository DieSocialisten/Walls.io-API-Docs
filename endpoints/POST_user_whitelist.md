# POST `/user_whitelist`

#### Add a user to this wall's whitelist 

All posts of whitelisted users are approved automatically and instantly appear on the wall, even if the wall is set to manual moderation.

## Example request
```bash
curl -X POST \
  https://api.walls.io/v1/user_whitelist \
  -H 'content-type: application/x-www-form-urlencoded' \
  -d 'access_token=<ACCESS_TOKEN>&network=facebook&external_user_id=123456'
```

## Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `network` *(required)*: The social network of the user. Find it in any [__GET__ `/posts`][GET /posts] response in the `type` field. [Post Types]
- `external_user_id` *(required)*: The user's ID on the social network. Find it in any [__GET__ `/posts`][GET /posts] in the `external_user_id` field.

[GET /posts]: GET_posts.md
[Post Types]: ../Post_Types.md "List of possible post types"
