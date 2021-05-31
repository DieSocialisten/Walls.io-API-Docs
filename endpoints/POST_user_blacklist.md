## POST api/user_blacklist.json

Adds a user to this Wall's blacklist. This essentially blocks a user from posting to this Wall. All existing posts are automatically hidden (unless a moderator set the post's status to "visible") and no future posts will come in.

#### Example request
```bash
curl -X POST \
  https://api.walls.io/v1/user_blacklist.json \
  -H 'content-type: application/x-www-form-urlencoded' \
  -d 'access_token=<ACCESS_TOKEN>&network=twitter&post_user=123456'
```

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `network` *(required)*: The social network of the user. Find it in any `/api/posts` response under the field name `type`.
- `external_user_id` *(required)*: The user's ID on the social network. Find it in any `/api/posts` response under the same field name.