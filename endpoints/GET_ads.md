## GET api/ads.json

Returns a list of ads (Sponsored Posts) for a wall. Sponsored Posts are uploaded and managed in the Walls.io settings (Content / Sponsored Posts). The Wall is determined by the `access_token` that must be passed with the request.

#### Example request
`GET https://api.walls.io/v1/ads.json?access_token=<ACCESS_TOKEN>`

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
