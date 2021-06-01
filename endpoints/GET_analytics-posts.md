# GET `/analytics/posts`

#### Get the number of posts per social network on a wall

Also contains the total number of posts.

Inactive posts (e.g. blacklisted posts or posts that were hidden via your wall moderation backend) are ignored.

## Example request
```
GET https://api.walls.io/v1/analytics/posts?access_token=<ACCESS_TOKEN>
```

## Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `types`: A comma-separated list of the types of posts you would like to be counted. [Post Types]
- `since`: Pass a UNIX timestamp to limit the result to posts that were posted after this time.
- `media_types`: A comma-separated list of media types. Use this if you want to limit your query to text-only posts, or video posts, or image posts, or any combination of those. [Media Types]
- `languages`: A comma-separated list of ISO 639-1 language codes. Only posts with a `comment` in one of these languages will be included in the response. [Languages]
- `highlighted_only`: Set this to `1` if you would only like to count posts that have been highlighted by a moderator.
- `include_inactive`: Per default, only active posts are counted. If you want to receive all posts, regardless of status, set this to `1`.


## Example response

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

[Languages]: ../Languages.md "List of possible languages and language codes"
[Media Types]: ../Media_Types.md "List of media types"
[Post Types]: ../Post_Types.md "List of possible post types"
