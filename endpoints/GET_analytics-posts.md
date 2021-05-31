## GET api/analytics/posts.json

Returns the number of posts per social networks on your wall. Also returns the total number of posts.

Inactive posts (e.g. blacklisted posts or posts that were hidden via your wall moderation backend) are ignored.

#### Example request
`GET https://api.walls.io/v1/analytics/posts.json?access_token=<ACCESS_TOKEN>`

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `types`: A comma-separated list of the types of posts you would like to receive. For a full list of possible types see the `type` field in the  [list of common fields](#common-post-fields).
- `since`: Pass a UNIX timestamp to limit the result to posts that were posted after this time.
- `media_types`: A comma-separated list of media types. Use this if you want to limit your query to text-only posts, or video posts, or image posts, or any combination of those. For a full list of media types see the `media_type` field in the  [list of media types](#media-types).
- `languages`: A comma-separated list of ISO 639-1 language codes. Only posts with a `comment` in one of these languages will be included in the response.
- `highlighted_only`: Set this to `1` if you would only like to receive posts that have been highlighted by a moderator.
- `include_inactive`: Per default, only active posts are returned. If you want to receive all posts, regardless of status, set this to `1`.


#### Example response

```json
{
  "status": "success",
  "data": {
    "twitter": 463,
    "instagram": 395,
    "flickr": 125,
    "facebook": 83,
    "youtube": 72,
    "googleplus": 60,
    "total": 1198
  }
}
```