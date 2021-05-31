## DELETE api/user_whitelist.json

Removes a user from this Wall's whitelist. This is an undo of the [POST api/user_whitelist](#post-apiuser_whitelistjson) method.

#### Example request
```bash
curl -X DELETE \
  https://api.walls.io/v1/user_whitelist.json \
  -H 'content-type: application/x-www-form-urlencoded' \
  -d 'access_token=<ACCESS_TOKEN>&network=twitter&post_user=123456'
```

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `network` *(required)*: The social network of the user. Find it in any `/api/posts` response under the field name `type`.
- `external_user_id` *(required)*: The user's ID on the social network. Find it in any `/api/posts` response under the same field name.