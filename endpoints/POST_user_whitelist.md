## POST api/user_whitelist.json

Adds a user to this Wall's whitelist. All posts of whitelisted users are approved automatically and instantly appear on the Wall's frontend, even if the Wall is set to manual moderation.

#### Example request
```bash
curl -X POST \
  https://api.walls.io/v1/user_whitelist.json \
  -H 'content-type: application/x-www-form-urlencoded' \
  -d 'access_token=<YOUR_ACCESS_TOKEN>&network=twitter&post_user=123456'
```

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `network` *(required)*: The social network of the user. Find it in any `/api/posts` response under the field name `type`.
- `external_user_id` *(required)*: The user's ID on the social network. Find it in any `/api/posts` response under the same field name.