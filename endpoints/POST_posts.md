## POST api/posts.json

Adds a new Native Post to the Wall.

Native Posts can be posted to the Wall right away, or scheduled to be posted later. You can add an image or video to your post by specifying a publicly available URL, or by uploading it via [POST api/media_upload.json](#post-apimedia_uploadjson).

It is allowed to omit the `text` parameter if an `image` or `video` is added, and vice versa. It is not allowed to omit all three of those fields at the same time. Same goes for `user_name` and `user_image`.

If you add a `video` **and** an `image` then the latter will be uses as a preview image for the video. If only a `video` is set then a preview image will be automatically generated.

The response contains date strings in UTC and numeric UNIX timestamps in seconds.

#### Example request
```bash
curl -X POST \
  https://api.walls.io/v1/posts.json \
  -H 'content-type: application/x-www-form-urlencoded' \
  -d 'access_token=<YOUR_ACCESS_TOKEN>&text=Picture%20of%20a%20cat&image=https%3A%2F%2Furl.of.some%2Fother%2Fimage&video=5bac9959-4b0c-4916-bc0e-00faac12000b&user_name=Cat%20Facts&user_image=https%3A%2F%2Furl.of.some%2Fimage'
```

#### Parameters

- `text` *(required if `image` and `video` are omitted)*: Text content of the post.
- `video` *(required if `text` and `image` are omitted)*: Video of the post.
  - Must be in MP4 format
  - This can either be a full URL to a video, or an ID returned by [POST api/media_upload.json](#post-apimedia_uploadjson)
- `image` *(required if `text` and `video` are omitted)*: Main image of the post. If `video` is also set then this image is only used as a preview for the video.
  - Allowed formats: JPG, PNG, GIF
  - This can either be a full URL to an image, or an ID returned by [POST api/media_upload.json](#post-apimedia_uploadjson)
- `user_name` *(required if `user_image` is omitted)*: Name of the user who created the post.
- `user_image` *(required if `user_name` is omitted)*: User image of the user who created the post.
- `link`: The URL that a click on the posts timestamp or the image in the post detail view leads to.
- `language` The post's language. If no value is given, we try to detect the language from the `text` field.
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
