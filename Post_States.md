# Post States

Every post is in exactly one moderation state. Use the `state` parameter to choose which states an endpoint returns or counts. Default: `visible`. The parameter and the `state` and `state_reason` fields are available on walls with the new moderation.

- `visible`: Shown on the Wall.
- `review`: Held back until a moderator decides.
- `hidden`: Not shown on the Wall, hidden by a filter or by a moderator.
- `trashed`: Moved to the trash by a moderator.

The `status` field of a post is `true` only for `visible` posts.
