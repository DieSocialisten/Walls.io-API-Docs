# GET `/analytics/users`

#### Get the number of unique users that have posted on a wall

The numbers are grouped by social network. Also contains the total number of unique users.

Per default only users with visible posts are counted. Users who only have posts in other states (e.g. blacklisted posts or posts that were hidden via your wall moderation backend) are counted only if you ask for that state with the `state` parameter.

## Example request
```
GET https://api.walls.io/v1/analytics/users?access_token=<ACCESS_TOKEN>
```

## Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `types`: A comma-separated list of the types of posts you would like to be counted. [Post Types]
- `since`: Pass a UNIX timestamp to limit the result to posts that were posted after this time.
- `media_types`: A comma-separated list of media types. Use this if you want to limit your query to text-only posts, or video posts, or image posts, or any combination of those. [Media Types]
- `languages`: A comma-separated list of ISO 639-1 language codes. Only posts with a `comment` in one of these languages will be included in the response. [Languages]
- `pinned_only`: Set this to `1` if you would only like to count posts that have been pinned to top by a moderator.
- `state`: A comma-separated list of the states of posts you would like to be counted. Default: `visible`. [Post States]
- `include_inactive` *(deprecated, removed on March 1, 2027)*: Set this to `1` to count posts in every state. Use `state` instead, e.g. `state=visible,review,hidden,trashed`.

## Example response

```json
{
  "status": "success",
  "data": {
    "instagram": 386,
    "facebook": 83,
    "youtube": 49,
    "googleplus": 35,
    "flickr": 24,
    "total": 577
  }
}
```

[Languages]: ../Languages.md "List of possible languages and language codes"
[Media Types]: ../Media_Types.md "List of media types"
[Post Types]: ../Post_Types.md "List of possible post types"
[Post States]: ../Post_States.md "List of possible post states"
