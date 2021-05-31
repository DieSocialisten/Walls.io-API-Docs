# GET `/posts/changed.rss`

#### Get an RSS feed with the wall's posts, ordered by the time they were updated

This endpoint should be used if you need to know about all updates to existing posts, as well as new posts. 
Every time an existing post is updated, it rises to the top of this endpoint's response.

## Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `since` *(required)*: A timestamp used for pagination of results. You will only receive posts that have been updated since this date and time. Please use the `current_time` field of the response and pass it as the `since` field of the next request.
- `limit`: The maximum number of posts you would like to receive. The maximum limit is `1000`. Default: `50`.
- `fields`: A comma-separated list of fields you would like to receive for each post. [Common Post Fields]
- `types`: A comma-separated list of the types of posts you would like to receive. [Post Types]
- `media_types`: A comma-separated list of media types. Use this if you want to limit your query to text-only posts, or video posts, or image posts, or any combination of those. [Media Types]
- `languages`: A comma-separated list of ISO 639-1 language codes. Only posts with a `comment` in one of these languages will be included in the response. [Languages]
- `highlighted_only`: Set this to `1` if you would only like to receive posts that have been highlighted by a moderator.
- `include_inactive`: Per default, only active posts are returned. If you want to receive all posts, regardless of status, set this to `1`.
- `include_source`: Set this to `1` if you want each post to include the source that it came from.

[Common Post Fields]: Common_Post_Fields.md "List of fields common to all posts endpoints"
[GET /posts/changed.rss]: GET_posts-changed.md
[Languages]: ../Languages.md "List of possible languages and language codes"
[Media Types]: ../Media_Types.md "List of media types"
[Post Types]: ../Post_Types.md "List of possible post types"
