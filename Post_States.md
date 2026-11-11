# Post States

Every post is in exactly one moderation state. Use the `state` parameter to choose which states an endpoint returns or counts. Default: `visible`. The parameter and the `state` and `state_reason` fields are available on walls with the new moderation.

- `visible`: Shown on the Wall.
- `review`: Held back until a moderator decides.
- `hidden`: Not shown on the Wall, hidden by a filter or by a moderator.
- `trashed`: Moved to the trash by a moderator.

`state` is also a parameter of the write endpoints, where it takes one value and sets it: [PUT `/posts/{postId}`][PUT /posts/{postId}] accepts all four states, [POST `/posts`][POST /posts] accepts `visible`, `hidden` and `review`. A state you set is a moderator's decision and stays until you change it.

The `status` field of a post is `true` only for `visible` posts. It is deprecated and will be removed on March 1, 2027, together with the `status` and `include_inactive` parameters. Use `state` instead.

[PUT /posts/{postId}]: endpoints/PUT_posts-postid.md "Set the state of a single post, pin it, or change its language"
[POST /posts]: endpoints/POST_posts.md "Add a new Native Post"
