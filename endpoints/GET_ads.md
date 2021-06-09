# GET `/ads`

Get a list of ads (Sponsored Posts) for a wall

Sponsored Posts are uploaded and managed in the Walls.io settings (Content / Sponsored Posts).

## Example request
```
GET https://api.walls.io/v1/ads?access_token=<ACCESS_TOKEN>
```

## Parameters
- `access_token` *(required)*: Your Walls.io access token.

## Example response
```json
{
    "status": "success",
    "count": 1,
    "data": [
        {
            "id": "1234567890",
            "image": "https:\/\/walls.io\/link\/to\/image.jpg",
            "imageWidth": 2000,
            "imageHeight": 1335,
            "imageAspectRatio": 1.4981273408239701,
            "link": "https:\/\/www.facebook.com",
            "text": "Hello World",
            "userImage": null,
            "userName": "My Name"
        }
    ]
}
```
