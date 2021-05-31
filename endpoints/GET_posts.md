## GET api/posts.json

Returns a list of posts for a wall. The wall is determined by the `access_token` that must be passed with the request.

> **Note**: This endpoint does **not** sort the posts by the date they were posted on their social networks, but in the order they arrive on the Walls.io server. Those sortings can differ greatly, especially after you add a new hashtag or other source in your wall settings.
>
> This is done deliberately so you can never miss any "old" postings that arrive on this endpoint. However, this order of posts is usually not what you want to display in your frontend, so make sure to implement your own post sorting logic.

#### Example request
`GET https://api.walls.io/v1/posts.json?access_token=<YOUR_ACCESS_TOKEN>&fields=id,comment,type&limit=10&include_inactive=1`

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `limit`: The maximum number of posts you would like to receive. The maximum limit is `1000`. If this parameter is not passed, the limit will be set to `50`.
- `after`: A post id used for pagination of results. You will only receive posts that have a higher ID than this.
- `before`: A post id used for pagination of results. You will only receive posts that have a lower ID than this.
- `fields`: A comma-separated list of fields you would like to receive for each post. For a full list of possible fields see [the list of common fields](#common-post-fields).
- `types`: A comma-separated list of the types of posts you would like to receive. For a full list of possible types see the `type` field in the  [list of common fields](#common-post-fields).
- `media_types`: A comma-separated list of media types. Use this if you want to limit your query to text-only posts, or video posts, or image posts, or any combination of those. For a full list of media types see the `media_type` field in the  [list of media types](#media-types).
- `languages`: A comma-separated list of ISO 639-1 language codes. Only posts with a `comment` in one of these languages will be included in the response.
- `highlighted_only`: Set this to `1` if you would only like to receive posts that have been highlighted by a moderator.
- `include_inactive`: Per default, only active posts are returned. If you want to receive all posts, regardless of status, set this to `1`.
- `include_source`: Set this to `1` if you want each post to include the source that it came from.

#### Example response

```json
{
  "status":"success",
  "data":[
    {
      "id":"146670",
      "comment":"3 days and no #Starbucks \n\n#feinding",
      "cta": {
        "text": "SHOP_NOW",
        "url": "https://walls.io"
      },
      "type":"twitter",
      "external_image":"http:\/\/pbs.twimg.com\/profile_images\/471635099977408512\/cWPhJJWz_normal.jpeg",
      "external_name":"LOWERERWICK",
      "external_fullname":"Marko 9TOOTH",
      "external_user_id":"123456",
      "post_image":"",
      "post_link":"https:\/\/twitter.com\/LOWERERWICK\/status\/487213557436518400",
      "post_video":null,
      "twitter_entities":"{\"hashtags\":[{\"text\":\"Starbucks\",\"indices\":[14,24]},{\"text\":\"feinding\",\"indices\":[27,36]}],\"trends\":[],\"urls\":[],\"user_mentions\":[],\"symbols\":[]}",
      "twitter_retweet":false,
      "is_highlighted":false,
      "status":true,
      "created":"2014-07-10 14:35:38",
      "modified":"2014-07-10 14:35:39",
      "permalink":"https:\/\/twitter.com\/LOWERERWICK\/status\/487213557436518400",
      "userlink":"https:\/\/www.twitter.com\/LOWERERWICK",
      "location": "Knottingley",
      "latitude": "53.69547100000000",
      "longitude": "-1.25397500000000"
    },
    {
      "id":"146661",
      "comment":"According to #starbucks my name is #howard... #thatsnotmyname #starbucksfail",
      "type":"twitter",
      "external_image":"http:\/\/pbs.twimg.com\/profile_images\/378800000483014192\/cc7de90a32652e99b6716bda6e656481_normal.jpeg",
      "external_name":"TakeMe2TheRyan",
      "external_fullname":"Ryan Caruso",
      "external_user_id":"234567",
      "post_image":"",
      "post_link":"https:\/\/twitter.com\/TakeMe2TheRyan\/status\/487213383762989056",
      "post_video":null,
      "twitter_entities":"{\"hashtags\":[{\"text\":\"starbucks\",\"indices\":[13,23]},{\"text\":\"howard\",\"indices\":[35,42]},{\"text\":\"thatsnotmyname\",\"indices\":[46,61]},{\"text\":\"starbucksfail\",\"indices\":[62,76]}],\"trends\":[],\"urls\":[],\"user_mentions\":[],\"symbols\":[]}",
      "twitter_retweet":false,
      "is_highlighted":false,
      "status":true,
      "created":"2014-07-10 14:34:57",
      "modified":"2014-07-10 14:34:57",
      "permalink":"https:\/\/twitter.com\/TakeMe2TheRyan\/status\/487213383762989056",
      "userlink":"https:\/\/www.twitter.com\/TakeMe2TheRyan",
      "location": null,
      "latitude": null,
      "longitude": null
    }
  ]
}
```