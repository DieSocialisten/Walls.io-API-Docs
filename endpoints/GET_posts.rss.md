# GET `/posts.rss`

#### Get an RSS feed with the wall's posts

These posts are ordered by `created`. If you need to access recently updated posts, use the [**GET** `/posts/changed.rss`][GET /posts/changed.rss] endpoint.

This endpoint does **not** sort the posts by the date they were posted on their social networks, but in the order they arrive at the Walls.io server.
Those sorting can differ greatly, especially after you add a new hashtag or other source in your wall settings.
This is done deliberately, so you can never miss any “old” postings that arrive at this endpoint.
However, this order of posts is usually not what you want to display in your frontend, so make sure to implement your own post sorting logic.

## Example request
```
GET https://api.walls.io/v1/posts.rss?access_token=<ACCESS_TOKEN>`
```

## Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `limit`: The maximum number of posts you would like to receive. The maximum limit is `1000`. Default: `50`.
- `after`: A post id used for pagination of results. You will only receive posts that have a higher ID than this.
- `before`: A post id used for pagination of results. You will only receive posts that have a lower ID than this.
- `fields`: A comma-separated list of fields you would like to receive for each post. [Common Post Fields]
- `types`: A comma-separated list of the types of posts you would like to receive. [Post Types]
- `media_types`: A comma-separated list of media types. Use this if you want to limit your query to text-only posts, or video posts, or image posts, or any combination of those. [Media Types]
- `languages`: A comma-separated list of ISO 639-1 language codes. Only posts with a `comment` in one of these languages will be included in the response. [Languages]
- `pinned_only`: Set this to `1` if you would only like to receive only posts that have been pinned to top by a moderator.
- `include_inactive`: Per default, only active posts are returned. If you want to receive all posts, regardless of status, set this to `1`.
- `include_source`: Set this to `1` if you want each post to include the source that it came from.

[Common Post Fields]: /Common_Post_Fields.md "List of fields common to all posts endpoints"
[GET /posts/changed.rss]: GET_posts-changed.md
[Languages]: ../Languages.md "List of possible languages and language codes"
[Media Types]: ../Media_Types.md "List of media types"
[Post Types]: ../Post_Types.md "List of possible post types"
