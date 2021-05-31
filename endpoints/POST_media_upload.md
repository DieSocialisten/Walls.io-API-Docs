# POST `/media_upload`

#### Upload an image or video which can then be used in [**POST** `/posts`][POST /posts]

It is possible to add an image and video to the same post in [**POST** `/posts`][POST /posts]. 
However, the files must be uploaded individually.

Please make sure you add the HTTP header `Content-Type: multipart/form-data`.

The maximum file size for uploads is 25MB for images and 50MB for videos.

Upon successful upload this method will return an ID (see example response) which can then be used instead of a URL in [**POST** `/posts`][POST /posts].

## Example request
```bash
curl -X POST \
  https://api.walls.io/v1/media_upload \
  -H 'Content-Type: multipart/form-data' \
  -F access_token=<ACCESS_TOKEN> \
  -F 'image=@/path/to/file/on/local/filesystem.jpg'
```

## Parameters

- `image`: Image file to be uploaded
- `video`: Video file to be uploaded

## Example response

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

[POST /posts]: POST_posts.md "Add a new Native Post"