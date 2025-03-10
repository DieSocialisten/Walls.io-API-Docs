## Common Post fields

All responses from the `/posts` endpoints share the same set of fields:

- `id`: The unique Walls.io ID of this post.
- `comment`: The user-generated text content of this post.
- `cta`: The call to action set for this post
  - `text`: The selected text. Possible values are `"APPLY_NOW"`, `"BOOK_NOW"`, `"CONTACT_US"`, `"DOWNLOAD"`, `"LEARN_MORE"`, `"SHOP_NOW"`, and `"SIGN_UP"`. 
  - `url`: The URL/link of this CTA button
- `language`: Language of the post as an ISO 639-1 language code
- `type`: The post type, e.g. `facebook` or `youtube` [Post Types]
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
- `post_link_wallsio`: The link of this post on the Wall.
- `is_pinned`: `true` if the post has been pinned to top by a moderator; `false` otherwise.
- `sentiment`: The sentiment of the post. Possible values are `"positive"`, `"neutral"`, `"negative"`, and `null`.
- `status`: Whether this post is active (visible) or inactive (invisible) on the Wall. Contains `true` if it is active.
- `created`: The date and time when this post was created in the social network it was posted to. The timezone is UTC.
- `created_timestamp`: Same as `created`, but as a UNIX timestamp.
- `modified`: The date and time of the last modification of this `Post` object. This can be used to update existing posts, for example if their status was changed on Walls.io. The timezone is UTC.
- `modified_timestamp`: Same as `modified`, but as a UNIX timestamp.
- `userlink`: A link to the user's profile on the social network the post was posted to.
- `location`: The name of the geographic position this post was created at, or `null` if none was set.
- `latitude`: The latitude this post was created at, or `null` if the position was not set.
- `longitude`: The longitude this post was created at, or `null` if the position was not set.
- `album_hash`: The value is the same for posts, which are coming from the same album (carousel)

[Post Types]: /Post_Types.md "List of possible post types"
