## GET api/posts/changed.rss

Returns an RSS feed with the wall's posts, ordered by the time they were updated. The wall is determined by the `access_token` that must be passed with the request.

This endpoint should be used if you need to know about all updates to existing posts, as well as new posts. Every time an existing post is updated, it rises to the top of this endpoint's response.

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `since` *(required)*: A timestamp used for pagination of results. You will only receive posts that have been updated since this date and time. Please use the `current_time` field of the response and pass it as the `since` field of the next request.
- `limit`: The maximum number of posts you would like to receive. The maximum limit is `1000`. If this parameter is not passed, the limit will be set to `50`.
- `fields`: A comma-separated list of fields you would like to receive for each post. For a full list of possible fields see [the list of common fields](#common-post-fields).
- `types`: A comma-separated list of the types of posts you would like to receive. For a full list of possible types see the `type` field in the  [list of common fields](#common-post-fields).
- `media_types`: A comma-separated list of media types. Use this if you want to limit your query to text-only posts, or video posts, or image posts, or any combination of those. For a full list of media types see the `media_type` field in the  [list of media types](#media-types).
- `languages`: A comma-separated list of ISO 639-1 language codes. Only posts with a `comment` in one of these languages will be included in the response.
- `highlighted_only`: Set this to `1` if you would only like to receive posts that have been highlighted by a moderator.
- `include_inactive`: Per default, only active posts are returned. If you want to receive all posts, regardless of status, set this to `1`.
- `include_source`: Set this to `1` if you want each post to include the source that it came from.
