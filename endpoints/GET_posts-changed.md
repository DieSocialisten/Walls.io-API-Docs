# GET `/posts/changed`

#### Get a list of posts for a wall, ordered by the time they were updated

This endpoint should be used if you need to know about all updates to existing posts, as well as new posts. 
Every time an existing post is updated, it rises to the top of this endpoint's response.

## Example request
```
GET https://api.walls.io/v1/posts/changed?access_token=<ACCESS_TOKEN>&since=1404996397
```

## Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `since` *(required)*: A timestamp used for pagination of results. You will only receive posts that have been updated since this date and time. Please use the `current_time` field of the response and pass it as the `since` field of the next request.
- `limit`: The maximum number of posts you would like to receive. The maximum limit is `1000`. Default: `50`.
- `fields`: A comma-separated list of fields you would like to receive for each post. [Common Post Fields]
- `types`: A comma-separated list of the types of posts you would like to receive. [Post Types]
- `media_types`: A comma-separated list of media types. Use this if you want to limit your query to text-only posts, or video posts, or image posts, or any combination of those. [Media Types]
- `languages`: A comma-separated list of ISO 639-1 language codes. Only posts with a `comment` in one of these languages will be included in the response. [Languages]
- `pinned_only`: Set this to `1` if you would only like to receive only posts that have been pinned to top by a moderator.
- `include_inactive`: Per default, only active posts are returned. If you want to receive all posts, regardless of status, set this to `1`.
- `include_source`: Set this to `1` if you want each post to include the source that it came from.

#### Example response

```json
{
  "status":"success",
  "current_time":1408954107,
  "count":50,
  "data":[
    {
      "id": "17181205",
      "comment": "Oooh, it's a #Venti #Pike kinda day!! Can't even set the alarm \"later\" my internal clock is set.. That & my lovely roommates alarm blasting at 5:30 woke ME up (he's still sleeping).. lol. Bueno, laundry done, off to the gym before a meeting & getting the day started..",
      "cta": null,
      "external_fullname": null,
      "external_image": "http:\/\/images.ak.instagram.com\/profiles\/profile_372993670_75sq_1398301155.jpg",
      "external_name": "getfitgenes",
      "external_post_id": "769415235382107591_372993670",
      "external_user_id": "372993670",
      "is_pinned": false,
      "permalink": "http:\/\/instagram.com\/p\/qtgxR9uV3H\/",
      "post_image": "http:\/\/scontent-a.cdninstagram.com\/hphotos-xfp1\/t51.2885-15\/10560907_307861969392635_1595149027_n.jpg",
      "post_link": "http:\/\/instagram.com\/p\/qtgxR9uV3H\/",
      "post_video":null,
      "status": true,
      "type": "instagram",
      "userlink": "http:\/\/instagram.com\/getfitgenes",
      "location": null,
      "latitude": "25.75100000000000",
      "longitude": "-80.23633333300000",
      "created": "2014-07-21 13:17:45",
      "modified": "2014-07-21 13:19:35"
    }
  ]
}
```

[Common Post Fields]: /Common_Post_Fields.md "List of fields common to all posts endpoints"
[Languages]: ../Languages.md "List of possible languages and language codes"
[Media Types]: ../Media_Types.md "List of media types"
[Post Types]: ../Post_Types.md "List of possible post types"
