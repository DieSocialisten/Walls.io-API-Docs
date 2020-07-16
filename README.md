Walls.io API Documentation
==========================

## Contents
- [Posts Endpoints](#posts-endpoints)
  - [Common Post fields](#common-post-fields)
  - [Media types](#media-types)
  - [GET api/posts.*{format}*](#get-apipostsformat)
  - [GET api/posts/changed.*{format}*](#get-apipostschangedformat)
  - [GET api/posts/*{postId}*.*{format}*](#get-apipostspostidformat)
  - [PUT api/posts/*{postId}*.*{format}*](#put-apipostspostidformat)
  - [POST api/posts.*{format}*](#post-apipostsformat)
  - [POST api/media_upload.*{format}*](#post-apimedia_uploadformat)
  - [POST api/user_blacklist.*{format}*](#post-apiuser_blacklistformat)
  - [DELETE api/user_blacklist.*{format}*](#delete-apiuser_blacklistformat)
  - [POST api/user_whitelist.*{format}*](#post-apiuser_whitelistformat)
  - [DELETE api/user_whitelist.*{format}*](#delete-apiuser_whitelistformat)
  - [GET api/analytics/posts.*{format}*](#get-apianalyticspostsformat)
  - [GET api/analytics/users.*{format}*](#get-apianalyticsusersformat)
  - [GET api/ads.*{format}*](#get-apiadsformat)


All endpoints require a valid API access token. Find out how to get one in the [FAQs].

> **Note**: It is not permitted to access our API directly from the browser, because this would expose your secret access token to the public. 
>
> Instead, call the API from your server and cache the posts there.


All endpoints, if called with a `GET` request, support the following response formats:
- **JSON**: Expample request: `api/posts.json`
- **XML**: Example request: `api/posts.xml`
- **RSS**: Example request: `api/posts.rss` (This format is available on the posts-endpoint only!)


## Posts Endpoints

### Common Post fields

All responses from the `/posts` endpoints share the same set of fields:

- `id`: The unique Walls.io ID of this post.
- `comment`: The user-generated text content of this post.
- `language`: Language of the post as an ISO 639-1 language code
- `type`: The post type. Possible types are:
  - `"facebook"`
  - `"flickr"`
  - `"instagram"`
  - `"messenger"`
  - `"pinterest"`
  - `"reddit"`
  - `"rss"`
  - `"tumblr"`
  - `"twitter"`
  - `"vimeo"`
  - `"vkontakte"`
  - `"wallsio"`
  - `"youtube"`
- `external_post_id`: The post's id in the social network it originated from.
- `external_image`: The user's profile pic.
- `external_name`: The user's screen name or handle.
- `external_fullname`: Some networks offer a "full name" or "display name" field in addition to the handle. This field contains this display name.
- `external_user_id`: The user's ID in the social network.
- `post_image`: The (user-generated) image that was added to this post. If there is also a `post_video`, the `post_image` is usually a preview image of the video.
- `post_image_cdn`: Same as `post_image`, but served by our content delivery network.
- `post_video`: The video that was added to this post.
- `post_video_cdn`: Same as `post_video`, but served by our content delivery network.
- `permalink`: The permalink of this post on the social network it was posted to.
- `post_link`: Same as `permalink`.
- `twitter_entities`: If the post type is `twitter`, this field contains an array of Twitter entities. For a discription of the Twitter entity format, see the [Twitter API docs].
- `twitter_retweet`: If the post type is `twitter` and the post is a retweet, this field contains `true`.
- `is_crosspost`: If this post was posted to multiple social networks at the same time, all posts that came after the original one contain `true` for this field. The original post contains `false`.
- `is_highlighted`: `true` if the post has been highlighted by a moderator; `false` otherwise.
- `status`: Whether this post is active (visible) or inactive (invisible) on the Wall. Contains `true` if it is active.
- `created`: The date and time when this post was created in the social network it was posted to. The timezone is UTC.
- `created_timestamp`: Same as `created`, but as a UNIX timestamp.
- `modified`: Ths date and time of the last modification of this `Post` object. This can be used to update existing posts, for example if their status was changed on Walls.io. The timezone is UTC.
- `modified_timestamp`: Same as `modified`, but as a UNIX timestamp.
- `userlink`: A link to the user's profile on the social network the post was posted to.
- `location`: The name of the geographic position this post was created at, or `null` if none was set.
- `latitude`: The latitude this post was created at, or `null` if the position was not set.
- `longitude`: The longitude this post was created at, or `null` if the position was not set.

### Media types

Walls.io posts have different media types and you can limit your search to these types using the `media_types` parameter. Valid media types are:
- `text`: Posts that contain a `comment`, but no image or video.
- `image`: Posts that contain a `post_image`, but no video. However, the `comment` field is still allowed in this media type.
- `video`: Posts that contain a `post_video`. All other fields are also allowed in this media type, as long as it has a video.


### GET api/posts.*{format}*

Returns a list of posts for a wall. The wall is determined by the `access_token` that must be passed with the request.

> **Note**: This endpoint does **not** sort the posts by the date they were posted on their social networks, but in the order they arrive on the Walls.io server. Those sortings can differ greatly, especially after you add a new hashtag or other source in your wall settings.
>
> This is done deliberately so you can never miss any "old" postings that arrive on this endpoint. However, this order of posts is usually not what you want to display in your frontend, so make sure to implement your own post sorting logic.

#### Example request
`GET https://walls.io/api/posts.json?access_token=<YOUR_ACCESS_TOKEN>&fields=id,comment,type&limit=10&include_inactive=1`

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

### GET api/posts/changed.*{format}*

Returns a list of posts for a wall, ordered by the time they were updated. The wall is determined by the `access_token` that must be passed with the request.

This endpoint should be used if you need to know about all updates to existing posts, as well as new posts. Every time an existing post is updated, it rises to the top of this endpoint's response.

#### Example request
`GET https://walls.io/api/posts/changed.json?access_token=<YOUR_ACCESS_TOKEN>&since=1404996397`

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
      "external_fullname": null,
      "external_image": "http:\/\/images.ak.instagram.com\/profiles\/profile_372993670_75sq_1398301155.jpg",
      "external_name": "getfitgenes",
      "external_post_id": "769415235382107591_372993670",
      "external_user_id": "372993670",
      "is_crosspost": false,
      "is_highlighted": false,
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


### GET api/posts/*{postId}*.*{format}*

Returns a single post, specified by its Walls.io post id.

#### Example request
`GET https://walls.io/api/posts/17824236.json?access_token=<YOUR_ACCESS_TOKEN>`

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

### PUT api/posts/*{postId}*.*{format}*

Changes a single post's visibility status, highlighting, language, or spam status. The post is identified by its Walls.io post id.

This endpoint allows you to perform most actions you can do in the "Posts" tab of your Wall's "Moderation" page. One notable exception is the "Block user" (or "Whitelist user") feature which is done via the [POST api/user_blacklist](#post-apiuser_blacklistformat) (or [POST api/user_whitelist](#post-apiuser_whitelistformat)) endpoint.

You can perform multiple actions at once by setting multipe parameters.

#### Example request
```bash
curl -X PUT \
  https://walls.io/api/posts/17181206.json \
  -H 'content-type: application/x-www-form-urlencoded' \
  -d 'access_token=<YOUR_ACCESS_TOKEN>&is_highlighted=1&status=1&language=en'
```

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `is_highlighted`: Set this to `1` if the post should be highlighted, or `0` to remove an existing highlight flag.
- `status`: Set this to `1` to show a hidden post, or `0` to hide a visible post.
- `language`: Set this to change the language of a post. The language is passed as a two-letter ISO 639-1 language code. You can also remove a post's language completely by passing an empty string. To find out which languages are supported by the Walls.io API simply set this to a random value; the response will contain a list of all valid language codes.
- `report_spam`: Set this to `1` to report this post for spam, or `0` to remove the spam status from a post that was incorrectly reported as spam.


#### Example response

```json
{
  "status": "success",
  "query": {
    "postId": 17181206
  },
  "current_time": 1408954568,
  "data": {
    // ... the full updated post
  }
}
```


### POST api/posts.*{format}*

Adds a new Native Post to the Wall.

Native Posts can be posted to the Wall right away, or scheduled to be posted later. You can add an image or video to your post by specifying a publicly available URL, or by uploading it via [POST api/media_upload.*{format}*](#post-apimedia_uploadformat).

It is allowed to omit the `text` parameter if an `image` or `video` is added, and vice versa. It is not allowed to omit all three of those fields at the same time. Same goes for `user_name` and `user_image`.

If you add a `video` **and** an `image` then the latter will be uses as a preview image for the video. If only a `video` is set then a preview image will be automatically generated.

The response contains date strings in UTC and numeric UNIX timestamps in seconds.

#### Example request
```bash
curl -X POST \
  https://walls.io/api/posts.json \
  -H 'content-type: application/x-www-form-urlencoded' \
  -d 'access_token=<YOUR_ACCESS_TOKEN>&text=Picture%20of%20a%20cat&image=https%3A%2F%2Furl.of.some%2Fother%2Fimage&video=5bac9959-4b0c-4916-bc0e-00faac12000b&user_name=Cat%20Facts&user_image=https%3A%2F%2Furl.of.some%2Fimage'
```

#### Parameters

- `text` *(required if `image` and `video` are omitted)*: Text content of the post.
- `video` *(required if `text` and `image` are omitted)*: Video of the post.
  - Must be in MP4 format
  - This can either be a full URL to a video, or an ID returned by [POST api/media_upload.*{format}*](#post-apimedia_uploadformat)
- `image` *(required if `text` and `video` are omitted)*: Main image of the post. If `video` is also set then this image is only used as a preview for the video.
  - Allowed formats: JPG, PNG, GIF
  - This can either be a full URL to an image, or an ID returned by [POST api/media_upload.*{format}*](#post-apimedia_uploadformat)
- `user_name` *(required if `user_image` is omitted)*: Name of the user who created the post.
- `user_image` *(required if `user_name` is omitted)*: User image of the user who created the post.
- `link`: The URL that a click on the posts timestamp or the image in the post detail view leads to.
- `location`: Name of the location where this post was created, e.g. "Vienna, Austria". If no latlong data is added to the post then this location name is used to create geographic data via geocoding.
- `latitude`: Latitude of the location where this post was created, as a `float`, e.g. `48.208`
- `longitude`: Longitude of the location where this post was created, as a `float`, e.g. `16.367`
- `scheduled_timestamp`: If set, the post is not added to the Wall's frontend right away but scheduled to be posted later. Must be a UNIX timestamp in seconds and must not be in the past.
- `is_highlighted`: Set this to `1` if the post should be highlighted.
- `status`: Set this to `1` or `0` to force the visibility (a.k.a. "status") of the new post. Usually the status is determined by checking the post against the language filter, spam filter, and several blacklists and whitelists. All of those checks can be bypassed by explicitly setting the `status` field in this call.

#### Example response

```json
{
  "status": "success",
  "info": [],
  "current_time": 1505470103,
  "data": {
    "image": "https://url.of.some/other/image",
    "video": "https://walls.io/path/to/uploaded_video.mp4",
    "text": "Picture of a cat",
    "user_image": "https://url.of.some/image",
    "user_name": "Cat Facts",
    "posted_at": "2017-09-15 10:08:23",
    "posted_timestamp": 1505470103
  }
}
```

### POST api/media_upload.*{format}*

Uploads an image or video which can then be used in [POST api/posts.*{format}*](#post-apipostsformat).

It is possible to add an image and video to the same post in [POST api/posts.*{format}*](#post-apipostsformat). However, the files must be uploaded individually.

Please make sure you add the HTTP header `Content-Type: multipart/form-data`.

> **Note**: The maximum file size for uploads is 25MB for images and 50MB for videos.

Upon successful upload this method will return an ID (see example response) which can then be used instead of a URL in [POST api/posts.*{format}*](#post-apipostsformat).

#### Example request
```bash
curl -X POST \
  https://walls.io/api/media_upload.json \
  -H 'Content-Type: multipart/form-data' \
  -F access_token=<YOUR_ACCESS_TOKEN> \
  -F 'image=@/path/to/file/on/local/filesystem.jpg'
```

#### Parameters

- `image`: Image file to be uploaded
- `video`: Video file to be uploaded

#### Example response

```json
{
  "status": "success",
  "info": [],
  "current_time": 1538038106,
  "data": {
    "id": "5bac9959-4b0c-4916-bc0e-00fbac18000b"
  }
}
```

### POST api/user_blacklist.*{format}*

Adds a user to this Wall's blacklist. This essentially blocks a user from posting to this Wall. All existing posts are automatically hidden (unless a moderator set the post's status to "visible") and no future posts will come in.

#### Example request
```bash
curl -X POST \
  https://walls.io/api/user_blacklist.json \
  -H 'content-type: application/x-www-form-urlencoded' \
  -d 'access_token=<YOUR_ACCESS_TOKEN>&network=twitter&post_user=123456'
```

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `network` *(required)*: The social network of the user. Find it in any `/api/posts` response under the field name `type`.
- `external_user_id` *(required)*: The user's ID on the social network. Find it in any `/api/posts` response under the same field name.

### DELETE api/user_blacklist.*{format}*

Removes a user from this Wall's blacklist. This is an undo of the [POST api/user_blacklist](#post-apiuser_blacklistformat) method.

#### Example request
```bash
curl -X DELETE \
  https://walls.io/api/user_blacklist.json \
  -H 'content-type: application/x-www-form-urlencoded' \
  -d 'access_token=<YOUR_ACCESS_TOKEN>&network=twitter&post_user=123456'
```

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `network` *(required)*: The social network of the user. Find it in any `/api/posts` response under the field name `type`.
- `external_user_id` *(required)*: The user's ID on the social network. Find it in any `/api/posts` response under the same field name.

### POST api/user_whitelist.*{format}*

Adds a user to this Wall's whitelist. All posts of whitelisted users are approved automatically and instantly appear on the Wall's frontend, even if the Wall is set to manual moderation.

#### Example request
```bash
curl -X POST \
  https://walls.io/api/user_whitelist.json \
  -H 'content-type: application/x-www-form-urlencoded' \
  -d 'access_token=<YOUR_ACCESS_TOKEN>&network=twitter&post_user=123456'
```

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `network` *(required)*: The social network of the user. Find it in any `/api/posts` response under the field name `type`.
- `external_user_id` *(required)*: The user's ID on the social network. Find it in any `/api/posts` response under the same field name.

### DELETE api/user_whitelist.*{format}*

Removes a user from this Wall's whitelist. This is an undo of the [POST api/user_whitelist](#post-apiuser_whitelistformat) method.

#### Example request
```bash
curl -X DELETE \
  https://walls.io/api/user_whitelist.json \
  -H 'content-type: application/x-www-form-urlencoded' \
  -d 'access_token=<YOUR_ACCESS_TOKEN>&network=twitter&post_user=123456'
```

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `network` *(required)*: The social network of the user. Find it in any `/api/posts` response under the field name `type`.
- `external_user_id` *(required)*: The user's ID on the social network. Find it in any `/api/posts` response under the same field name.


### GET api/analytics/posts.*{format}*

Returns the number of posts per social networks on your wall. Also returns the total number of posts.

Inactive posts (e.g. blacklisted posts or posts that were hidden via your wall moderation backend) are ignored.

#### Example request
`GET https://walls.io/api/analytics/posts.json?access_token=<YOUR_ACCESS_TOKEN>`

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `types`: A comma-separated list of the types of posts you would like to receive. For a full list of possible types see the `type` field in the  [list of common fields](#common-post-fields).
- `since`: Pass a UNIX timestamp to limit the result to posts that were posted after this time.
- `media_types`: A comma-separated list of media types. Use this if you want to limit your query to text-only posts, or video posts, or image posts, or any combination of those. For a full list of media types see the `media_type` field in the  [list of media types](#media-types).
- `languages`: A comma-separated list of ISO 639-1 language codes. Only posts with a `comment` in one of these languages will be included in the response.
- `highlighted_only`: Set this to `1` if you would only like to receive posts that have been highlighted by a moderator.
- `include_inactive`: Per default, only active posts are returned. If you want to receive all posts, regardless of status, set this to `1`.


#### Example response

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


### GET api/analytics/users.*{format}*

Returns the number of unique users that have posted on your wall, grouped by social network. Also returns the total number of unique users.

Users who only have inactive posts (e.g. blacklisted posts or posts that were hidden via your wall moderation backend) on your wall are ignored.

#### Example request
`GET https://walls.io/api/analytics/users.json?access_token=<YOUR_ACCESS_TOKEN>`

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `types`: A comma-separated list of the types of posts you would like to receive. For a full list of possible types see the `type` field in the  [list of common fields](#common-post-fields).
- `since`: Pass a UNIX timestamp to limit the result to posts that were posted after this time.
- `media_types`: A comma-separated list of media types. Use this if you want to limit your query to text-only posts, or video posts, or image posts, or any combination of those. For a full list of media types see the `media_type` field in the  [list of media types](#media-types).
- `languages`: A comma-separated list of ISO 639-1 language codes. Only posts with a `comment` in one of these languages will be included in the response.
- `highlighted_only`: Set this to `1` if you would only like to receive posts that have been highlighted by a moderator.
- `include_inactive`: Per default, only active posts are returned. If you want to receive all posts, regardless of status, set this to `1`.

#### Example response

```json
{
  "status": "success",
  "data": {
    "twitter": 425,
    "instagram": 386,
    "facebook": 83,
    "youtube": 49,
    "googleplus": 35,
    "flickr": 24,
    "total": 1002
  }
}
```

### GET api/ads.*{format}*

Returns a list of ads for a wall. Ads are uploaded and managed in the Walls.io settings. The Wall is determined by the `access_token` that must be passed with the request.

#### Example request
`GET https://walls.io/api/ads.json?access_token=<YOUR_ACCESS_TOKEN>`

#### Parameters
- `access_token` *(required)*: Your Walls.io access token.

#### Example response
```json
{
    "status": "success",
    "data": [
        {
            "id": "5767ed0e-290c-4926-ad42-042cac1facad",
            "image": "https:\/\/walls.io\/link\/to\/image.jpg",
            "imageAspectRatio": 1.6,
            "link": "https:\/\/www.facebook.com"
        }
    ]
}
```


[Twitter API docs]:https://dev.twitter.com/docs/entities
[FAQs]:https://github.com/DieSocialisten/Walls.io-API-Docs/blob/master/FAQ.md
