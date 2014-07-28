![Walls.io API](http://walls.io/img/visuals/api-diagram.png)

Walls.io API Documentation
==========================

All endpoints, if called with a `GET` request, support the following response formats:
- **JSON**: Expample request: `api/posts.json`
- **XML**: Example request: `api/posts.xml`
- **JSONP**: Like the JSON request, but pass a `callback` parameter, e.g.: `api/posts.json?callback=someCallbackName`


## Posts Endpoints

### Common Post fields

All responses from the `/posts` endpoints share the same set of fields:

- `id`: The unique Walls.io ID of this post.
- `comment`: The user-generated text content of this post.
- `type`: The post type. Possible types are:
 - `"twitter"`
 - `"facebook"`
 - `"instagram"`
 - `"googleplus"`
 - `"foursquare"`
 - `"youtube"`
 - `"flickr"`
 - `"appdotnet"`
 - `"tumblr"`
 - `"reddit"`
 - `"rss"`
- `external_image`: The user's profile pic.
- `external_name`: The user's screen name or handle.
- `external_fullname`: Some networks offer a "full name" or "display name" field in addition to the handle. This field contains this display name.
- `external_user_id`: The user's ID in the social network.
- `post_image`: The (user-generated) image that was added to this post.
- `post_link`: The (user-generated) link that was added to this post.
- `twitter_entities`: If the post type is `twitter`, this field contains an array of Twitter entities. For a discription of the Twitter entity format, see the [Twitter API docs].
- `twitter_retweet`: If the post type is `twitter` and the post is a retweet, this field contains `true`.
- `is_crosspost`: If this post was posted to multiple social networks at the same time, all posts that came after the original one contain `true` for this field. The original post contains `false`.
- `status`: Whether this post is active (visible) or inactive (invisible) on the Wall. Contains `true` if it is active.
- `created`: The date and time when this post was created in the social network it was posted to.
- `modified`: Ths date and time of the last modification of this `Post` object. This can be used to update existing posts, for example if their status was changed on Walls.io.
- `permalink`: The permalink of this post on the social network it was posted to.
- `userlink`: A link to the user's profile on the social network the post was posted to.


### GET api/posts.*{format}*

Returns a list of posts for a wall. The wall is determined by the `access_token` that must be passed with the request.

#### Example request
`GET https://walls.io/api/posts.json?access_token=<YOUR_ACCESS_TOKEN>&fields=id,comment,type&limit=10`

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `limit`: The maximum number of posts you would like to receive. The maximum limit is `1000`. If this parameter is not passed, the limit will be set to `50`.
- `after`: A post id used for pagination of results. You will only receive posts that have a higher ID than this.
- `before`: A post id used for pagination of results. You will only receive posts that have a lower ID than this.
- `fields`: A comma-separated list of fields you would like to receive for each post. For a full list of possible fields see [the list of common fields](#common-post-fields).
- `types`: A comma-separated list of the types of posts you would like to receive. For a full list of possible types see the `type` field in the  [list of common fields](#common-post-fields).

#### Example response

```json
{
  "status":"SUCCESS",
  "data":[
    {
      "id":"146670",
      "comment":"3 days and no #Starbucks \n\n#feinding",
      "type":"twitter",
      "external_image":"http:\/\/pbs.twimg.com\/profile_images\/471635099977408512\/cWPhJJWz_normal.jpeg",
      "external_name":"LOWERERWICK",
      "external_fullname":"Marko 9TOOTH",
      "external_user_id":null,
      "post_image":"",
      "post_link":"https:\/\/twitter.com\/LOWERERWICK\/status\/487213557436518400",
      "twitter_entities":"{\"hashtags\":[{\"text\":\"Starbucks\",\"indices\":[14,24]},{\"text\":\"feinding\",\"indices\":[27,36]}],\"trends\":[],\"urls\":[],\"user_mentions\":[],\"symbols\":[]}",
      "twitter_retweet":false,
      "status":true,
      "created":"2014-07-10 14:35:38",
      "modified":"2014-07-10 14:35:39",
      "permalink":"https:\/\/twitter.com\/LOWERERWICK\/status\/487213557436518400",
      "userlink":"https:\/\/www.twitter.com\/LOWERERWICK"
    },
    {
      "id":"146661",
      "comment":"According to #starbucks my name is #howard... #thatsnotmyname #starbucksfail",
      "type":"twitter",
      "external_image":"http:\/\/pbs.twimg.com\/profile_images\/378800000483014192\/cc7de90a32652e99b6716bda6e656481_normal.jpeg",
      "external_name":"TakeMe2TheRyan",
      "external_fullname":"Ryan Caruso",
      "external_user_id":null,
      "post_image":"",
      "post_link":"https:\/\/twitter.com\/TakeMe2TheRyan\/status\/487213383762989056",
      "twitter_entities":"{\"hashtags\":[{\"text\":\"starbucks\",\"indices\":[13,23]},{\"text\":\"howard\",\"indices\":[35,42]},{\"text\":\"thatsnotmyname\",\"indices\":[46,61]},{\"text\":\"starbucksfail\",\"indices\":[62,76]}],\"trends\":[],\"urls\":[],\"user_mentions\":[],\"symbols\":[]}",
      "twitter_retweet":false,
      "status":true,
      "created":"2014-07-10 14:34:57",
      "modified":"2014-07-10 14:34:57",
      "permalink":"https:\/\/twitter.com\/TakeMe2TheRyan\/status\/487213383762989056",
      "userlink":"https:\/\/www.twitter.com\/TakeMe2TheRyan"
    },
    ...
  }
}
```

### GET api/posts/changed.*{format}*

Returns a list of posts for a wall, ordered by the time they were updated. The wall is determined by the `access_token` that must be passed with the request.

This endpoint should be used if you need to know about all updates to existing posts, as well as new posts. Every time an existing post is updated, it rises to the top of this endpoint's response.

#### Example request
`GET https://walls.io/api/posts/changed.json?access_token=<YOUR_ACCESS_TOKEN>&since=1404996397`

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `limit`: The maximum number of posts you would like to receive. The maximum limit is `1000`. If this parameter is not passed, the limit will be set to `50`.
- `since`: A timestamp used for pagination of results. You will only receive posts that have been updated since this date and time. Please use the `current_time` field of the response and pass it as the `since` field of the next request.
- `until`: A UNIX timestamp used for pagination of results. You will only receive posts that have been updated before this date and time.
- `fields`: A comma-separated list of fields you would like to receive for each post. For a full list of possible fields see [the list of common fields](#common-post-fields).
- `types`: A comma-separated list of the types of posts you would like to receive. For a full list of possible types see the `type` field in the  [list of common fields](#common-post-fields).

#### Example response

```json
{
  "status":"SUCCESS",
  "current_time":1404996723,
  "count":50,
  "data":[
    {
      "id":"17824337",
      "comment":"I'm a happy girl! Here comes the long weekend! #starbucks #yums #simplepleasures http:\/\/t.co\/2dqTPO1J4Y",
      "type":"twitter",
      "external_image":"http:\/\/pbs.twimg.com\/profile_images\/440170681599152129\/gU-hicOp_normal.jpeg",
      "external_name":"AnchorintheS",
      "external_fullname":"Alison",
      "external_user_id":null,
      "post_image":"https:\/\/instagram.com\/p\/p_xmwIhtk8\/media\/?size=l",
      "post_link":"https:\/\/twitter.com\/AnchorintheS\/status\/484743321307185152",
      "twitter_entities":"{\"hashtags\":[{\"text\":\"starbucks\",\"indices\":[47,57]},{\"text\":\"yums\",\"indices\":[58,63]},{\"text\":\"simplepleasures\",\"indices\":[64,80]}],\"trends\":[],\"urls\":[{\"url\":\"http:\\\/\\\/t.co\\\/2dqTPO1J4Y\",\"expanded_url\":\"http:\\\/\\\/instagram.com\\\/p\\\/p_xmwIhtk8\\\/\",\"display_url\":\"instagram.com\\\/p\\\/p_xmwIhtk8\\\/\",\"indices\":[81,103]}],\"user_mentions\":[],\"symbols\":[]}",
      "twitter_retweet":false,
      "status":true,
      "created":"2014-07-03 18:59:48",
      "modified":"2014-07-03 18:59:49",
      "is_crosspost":false,
      "permalink":"https:\/\/twitter.com\/AnchorintheS\/status\/484743321307185152",
      "userlink":"https:\/\/www.twitter.com\/AnchorintheS"
    },
    ...
  ]
}
```


### GET api/posts/*{postId}*.*{format}*

Returns a single post, specified by its Walls.io post id.

#### Example request
`GET https://walls.io/api/posts/17824236.json?access_token=<YOUR_ACCESS_TOKEN>`

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `fields`: A comma-separated list of fields you would like to receive for each post. For a full list of possible fields see [the list of common fields](#common-post-fields).
- `types`: A comma-separated list of the types of posts you would like to receive. For a full list of possible types see the `type` field in the  [list of common fields](#common-post-fields).


#### Example response

```json
{
    "status": "SUCCESS",
    "current_time": 1404996936,
    "data": {
        "id": "17824236",
        "comment": "Celebrating, I made the U13 3x3 BC Summer Games Team!?",
        "type": "instagram",
        "external_image": "http:\/\/photos-c.ak.instagram.com\/hphotos-ak-xfa1\/917152_867472236614002_2112064981_a.jpg",
        "external_name": "kenzie_perry12",
        "external_fullname": null,
        "external_user_id": "231099956",
        "post_image": "http:\/\/scontent-a.cdninstagram.com\/hphotos-xfa1\/t51.2885-15\/914416_490993951032613_435314366_n.jpg",
        "post_link": "http:\/\/instagram.com\/p\/phY4abTXc0\/",
        "twitter_entities": null,
        "twitter_retweet": false,
        "status": false,
        "created": "2014-06-21 23:46:32",
        "modified": "2014-07-03 18:56:43",
        "permalink": "http:\/\/instagram.com\/p\/phY4abTXc0\/",
        "userlink": "http:\/\/instagram.com\/kenzie_perry12"
    }
}
```



[Twitter API docs]:https://dev.twitter.com/docs/entities
