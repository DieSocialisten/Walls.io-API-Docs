Walls.io API Documentation
==========================

API to access a Walls.io wall

## General

This is Walls.io API version `v1`.

It's available to Walls.io premium users. [Premium plan](https://walls.io/features-and-pricing)

All endpoints are prefixed with `https://api.walls.io/v1`.
> **Example**: `/posts` would become `https://api.walls.io/v1/posts`

All endpoints require a valid API access token. [Access Token](Access_Token.md)

The API generally returns JSON result, but all endpoints also support the `.xml` extension.


## Rate limit

We are rate limiting our API, but have very reasonable limits.
Calling our API 1-2 times per second is fine.

## Endpoints


#### Posts

  * [__GET__ `/posts`](endpoints/GET_posts.md) Get a list of posts
  * [__GET__ `/posts/changed`](endpoints/GET_posts-changed.md) Get a list of posts, ordered by the time they were updated
  * [__GET__ `/posts/{postId}`](endpoints/GET_posts-postid.md) Get a single post
  * [__POST__ `/posts`](endpoints/POST_posts.md) Add a new Native Post
  * [__PUT__ `/posts/{postId}`](endpoints/PUT_posts-postid.md) Change a single post's visibility status, highlighting, language, or spam status


#### Post as RSS

* [__GET__ `/posts.rss`](endpoints/GET_posts.rss.md) Get an RSS feed with the wall's posts
* [__GET__ `/posts/changed.rss`](endpoints/GET_posts-changed.rss.md) Get an RSS feed with the wall's posts, ordered by the time they were updated


#### Media Upload

  * [__POST__ `/posts/media_upload`](endpoints/POST_media_upload.md) Upload an image or video which can then be used in [__POST__ `/posts`]

[__POST__ `/posts`]: endpoints/POST_posts.md "Add a new Native Post"


#### Blacklist or whitelist users

  * [__POST__ `/user_blacklist`](endpoints/POST_user_blacklist.md) Add a user to this wall's blacklist
  * [__DELETE__ `/user_blacklist`](endpoints/DELETE_user_blacklist.md) Remove a user from this wall's blacklist
  * [__POST__ `/user_whitelist`](endpoints/POST_user_whitelist.md) Add a user to this wall's whitelist
  * [__DELETE__ `/user_whitelist`](endpoints/DELETE_user_whitelist.md) Remove a user from this wall's whitelist


#### Analytics

  * [__GET__ `/analytics/posts`](endpoints/GET_analytics-posts.md) Get the number of posts per social network on a wall
  * [__GET__ `/analytics/users`](endpoints/GET_analytics-users.md) Get the number of unique users that have posted on a wall


#### Ads / Sponsored Posts

  * [__GET__ `/ads`](endpoints/GET_ads.md) Get a list of ads (Sponsored Posts) for a wall
