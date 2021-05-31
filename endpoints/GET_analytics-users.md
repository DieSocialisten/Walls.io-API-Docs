## GET api/analytics/users.json

Returns the number of unique users that have posted on your wall, grouped by social network. Also returns the total number of unique users.

Users who only have inactive posts (e.g. blacklisted posts or posts that were hidden via your wall moderation backend) on your wall are ignored.

#### Example request
`GET https://api.walls.io/v1/analytics/users.json?access_token=<YOUR_ACCESS_TOKEN>`

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
    "twitter": 425,
    "instagram": 386,
    "facebook": 83,
    "youtube": 49,
    "googleplus": 35,
    "flickr": 24,
    "total": 1002
  }
}
```