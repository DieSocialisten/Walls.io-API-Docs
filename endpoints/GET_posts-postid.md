## GET api/posts/*{postId}*.json

Returns a single post, specified by its Walls.io post id.

#### Example request
`GET https://api.walls.io/v1/posts/17824236.json?access_token=<YOUR_ACCESS_TOKEN>`

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `fields`: A comma-separated list of fields you would like to receive for each post. For a full list of possible fields see [the list of common fields](#common-post-fields).
- `include_source`: Set this to `1` if you want the post to include the source that it came from.


#### Example response

```json
{
  "status": "success",
  "query": {
    "postId": 17181206
  },
  "current_time": 1408954568,
  "data": {
    "id": "17181206",
    "comment": "A heart on my cup and a wink! #ivepulled #guiltypleasure #starbucks",
    "cta": null,
    "type": "instagram",
    "external_image": "http:\/\/photos-f.ak.instagram.com\/hphotos-ak-xpf1\/10369543_654365497965469_839887771_a.jpg",
    "external_name": "mferrari1",
    "external_fullname": null,
    "external_user_id": "22059933",
    "post_image": "http:\/\/scontent-b.cdninstagram.com\/hphotos-xpa1\/t51.2885-15\/10499125_748994368486318_763693636_n.jpg",
    "post_link": "http:\/\/instagram.com\/p\/qtg9jrTRtz\/",
    "post_video":null,
    "twitter_entities": null,
    "twitter_retweet": false,
    "is_highlighted": false,
    "status": true,
    "location": null,
    "latitude": "51.48247833300000",
    "longitude": "-0.00957778300000",
    "created": "2014-07-21 13:19:25",
    "modified": "2014-07-21 13:19:35",
    "permalink": "http:\/\/instagram.com\/p\/qtg9jrTRtz\/",
    "userlink": "http:\/\/instagram.com\/mferrari1"
  }
}
```