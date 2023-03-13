# GET `/posts`

#### Get a list of posts

These posts are ordered by `id` in descending order (which corresponds to the time the posts arrive at the Walls.io server). If you need to access recently updated posts, use the [**GET** `/posts/changed`][GET /posts/changed] endpoint.

This endpoint does **not** sort the posts by the date they were posted on their social networks, but in the order they arrive at the Walls.io server. 
Those sorting can differ greatly, especially after you add a new hashtag or other source in your wall settings. 
This is done deliberately, so you can never miss any “old” postings that arrive at this endpoint. 
However, this order of posts is usually not what you want to display in your frontend, so make sure to implement your own post sorting logic.

>The API will not include data from social networks that prohibit redistribution of API data via their terms of service.

## Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `limit`: The maximum number of posts you would like to receive. The maximum limit is `1000`. Default: `50`.
- `after`: A post id used for pagination of results. You will only receive posts that have a higher ID than this.
- `before`: A post id used for pagination of results. You will only receive posts that have a lower ID than this.
- `fields`: A comma-separated list of fields you would like to receive for each post. [Common Post Fields]
- `types`: A comma-separated list of the types of posts you would like to receive. [Post Types]
- `media_types`: A comma-separated list of media types. Use this if you want to limit your query to text-only posts, or video posts, or image posts, or any combination of those. [Media Types]
- `languages`: A comma-separated list of ISO 639-1 language codes. Only posts with a `comment` in one of these languages will be included in the response. [Languages]
- `pinned_only`: Set this to `1` if you would only like to receive posts that have been pinned to top by a moderator.
- `include_inactive`: Per default, only active posts are returned. If you want to receive all posts, regardless of status, set this to `1`.
- `include_source`: Set this to `1` if you want each post to include the source that it came from.
- `sort`: Order the result by any field, according to the [JSON:API specification]. You may provide several comma-separated fields. The sort order is ascending unless it's prefixed with a minus, in which case it is descending. E.g. `?sort=-external_fullname,comment` first sort by `external_fullname` in descending order, then by `comment` in ascending order. Default: `-id`.


## Example request
```
GET https://api.walls.io/v1/posts?access_token=<ACCESS_TOKEN>&fields=id,comment,type&limit=10&include_inactive=1
GET https://api.walls.io/v1/posts?access_token=<ACCESS_TOKEN>&fields=id,comment,type&limit=10&include_inactive=1&sort=-created,-id
```


## Example response

```json
{
  "status":"success",
  "data":[
    {
      "id": "146670",
      "type": "facebook",
      "album_hash": "d6a080f55dede1112d63975645646Vfr",
      "comment": "Spring means coffee and nursery dates. 🌿",
      "cta": {
        "text": "SHOP_NOW",
        "url": "https://walls.io"
      },
      "external_fullname": "Starbucks",
      "external_image": "https:\/\/scontent.fist6-2.fna.fbcdn.net\/v\/t1.6435-1\/123456_1234567_4295515389661544448_n.png",
      "external_image_cdn": "https:\/\/d3pelj80y5v5k4.cloudfront.net\/35bce284-321b-4dfb-b9c9-782a51251c92",
      "external_post_id": "123456",
      "external_user_id": "123456",
      "is_marked_as_spam": false,
      "is_pinned": false,
      "permalink": "https:\/\/www.facebook.com\/123456\/posts\/123456",
      "post_image": "https:\/\/scontent-fra5-2.xx.fbcdn.net\/v\/t39.30808-6\/123456_123456_2587047266154587271_n.png",
      "post_image_cdn": "https:\/\/d3pelj80y5v5k4.cloudfront.net\/139219be-5d11-42f1-8ce8-8bff39ba293f",
      "post_link": "https:\/\/www.facebook.com\/123456\/posts\/123456",
      "status": true,
      "userlink": "https:\/\/www.facebook.com\/123456",
      "created": "2023-03-09 16:00:00",
      "created_timestamp": 1678377600,
      "modified": "2023-03-10 13:12:21",
      "modified_timestamp": 1678453941
    },
    {
      "id": "1466705",
      "type": "facebook",
      "comment": "FYI just because it's not the holidays anymore doesn't mean you still can't get a little treat with your coffee. 😉🍪",
      "external_fullname": "Starbucks",
      "external_image": "https:\/\/scontent-sea1-1.xx.fbcdn.net\/v\/t1.6435-1\/55680146_123456_123456_n.png",
      "external_image_cdn": "https:\/\/d3pelj80y5v5k4.cloudfront.net\/926fc6e1-2dbe-49b5-a785-0b343e052218",
      "external_post_id": "123456",
      "external_user_id": "123456",
      "is_marked_as_spam": false,
      "is_pinned": false,
      "language": "en",
      "permalink": "https:\/\/www.facebook.com\/123456\/posts\/123456",
      "post_link": "https:\/\/www.facebook.com\/123456\/posts\/123456",
      "status": true,
      "userlink": "https:\/\/www.facebook.com\/123456",
      "created": "2023-01-11 16:00:05",
      "created_timestamp": 1673452805,
      "modified": "2023-03-10 12:42:29",
      "modified_timestamp": 1678452149
    }
  ]
}
```

[Common Post Fields]: /Common_Post_Fields.md "List of fields common to all posts endpoints"
[GET /posts/changed]: GET_posts-changed.md "Get a list of posts for a wall, ordered by the time they were updated"
[Languages]: ../Languages.md "List of possible languages and language codes"
[Media Types]: ../Media_Types.md "List of media types"
[Post Types]: /Post_Types.md "List of possible post types"
[JSON:API specification]: https://jsonapi.org/format/#fetching-sorting
