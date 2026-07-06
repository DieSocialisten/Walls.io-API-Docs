# GET `/leads`

#### Get a list of collected leads

Returns the leads collected through your wall's lead-generation forms, ordered by `id` in ascending order.

This endpoint requires a wall with **API access** and the **Interactivity Pack** (which includes lead collection).

## Parameters
- `access_token` *(required)*: Your Walls.io access token.
- `limit`: The maximum number of leads you would like to receive. The maximum limit is `1000`. Default: `50`.
- `after`: A lead id used for pagination of results. You will only receive leads that have a higher ID than this.
- `before`: A lead id used for pagination of results. You will only receive leads that have a lower ID than this.
- `fields`: A comma-separated list of fields you would like to receive for each lead.
- `verified`: Set this to `true` if you would only like to receive leads whose email address has been verified.

## Response fields
- `id`: The unique id of the lead. Use this value for `after` / `before` pagination.
- `email`: The email address the lead submitted.
- `name`: The name the lead submitted.
- `location`: The location the lead submitted.
- `verified`: `true` if the lead's email address has been verified, otherwise `false`.
- `created`: The date and time at which the lead was collected, in ISO 8601 format (UTC), e.g. `2026-06-30T14:22:10+00:00`.
- `custom_fields`: An object containing any custom lead-form fields configured for the wall, keyed by field name, with the value submitted by the lead.

## Example request
```
GET https://api.walls.io/v1/leads?access_token=<ACCESS_TOKEN>&limit=50
GET https://api.walls.io/v1/leads?access_token=<ACCESS_TOKEN>&fields=id,email,name,verified&verified=true&after=146670
```

## Example response

```json
{
  "status": "success",
  "data": [
    {
      "id": "146671",
      "email": "jane.doe@example.com",
      "name": "Jane Doe",
      "location": "Vienna, Austria",
      "verified": true,
      "created": "2026-06-30T14:22:10+00:00",
      "custom_fields": {
        "company": "Example GmbH",
        "newsletter_opt_in": "yes"
      }
    },
    {
      "id": "146672",
      "email": "john.smith@example.com",
      "name": "John Smith",
      "location": "Berlin, Germany",
      "verified": false,
      "created": "2026-06-30T15:03:41+00:00",
      "custom_fields": {
        "company": "Acme Inc.",
        "newsletter_opt_in": "no"
      }
    }
  ]
}
```

[GET /posts]: GET_posts.md "Get a list of posts for a wall"
