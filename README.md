Walls.io API Documentation
==========================

## Endpoints
- Posts
  * [__GET__ `/posts`] Get a list of posts
  * [__GET__ `/posts/changed`] Get a list of posts, ordered by the time they were updated
  * [__GET__ `/posts/{postId}`] Get a single post
  * [__POST__ `/posts`] Add a new Native Post
  * [__PUT__ `/posts/{postId}`] Change a single post's visibility status, highlighting, language, or spam status

- Media Upload
  * [__POST__ `/posts/media_upload`] Upload an image or video which can then be used in [__POST__ `/posts`]

- Post as RSS
  * [__GET__ `/posts.rss`] Get an RSS feed with the wall's posts
  * [__GET__ `/posts/changed.rss`] Get an RSS feed with the wall's posts, ordered by the time they were updated

- Blacklist or whitelist users
  * [__POST__ `/user_blacklist`](endpoints/POST_user_blacklist.md)
    Add a user to this wall's blacklist

  * [__DELETE__ `/user_blacklist`](endpoints/DELETE_user_blacklist.md)
    Remove a user from this wall's blacklist

  * [__POST__ `/user_whitelist`](endpoints/POST_user_whitelist.md)
    Add a user to this wall's whitelist
    
  * [__DELETE__ `/user_whitelist`](endpoints/DELETE_user_whitelist.md)
    Remove a user from this wall's whitelist

### Analytics
  * [__GET__ `/analytics/posts`](endpoints/GET_analytics-posts.md)
    Get the number of posts per social network on a wall

  * [__GET__ `/analytics/users`](endpoints/GET_analytics-users.md)
    Get the number of unique users that have posted on a wall

### Ads / Sponsored Posts

  * [__GET__ `/ads`](endpoints/GET_ads.md)
    Get a list of ads (Sponsored Posts) for a wall

[__GET__ `/posts`]: endpoints/GET_posts.md
[__GET__ `/posts/changed`]: endpoints/GET_posts-changed.md
[__GET__ `/posts/{postId}`]: endpoints/GET_posts-postid.md
[__POST__ `/posts`]: endpoints/POST_posts.md
[__PUT__ `/posts/{postId}`]: endpoints/PUT_posts-postid.md

[__POST__ `/posts/media_upload`]: endpoints/POST_media_upload.md

[__GET__ `/posts.rss`]: endpoints/GET_posts.rss.md
[__GET__ `/posts/changed.rss`]: endpoints/GET_posts-changed.rss.md

## Contents
- [Posts Endpoints](#posts-endpoints)
  - [Common Post fields](#common-post-fields)
  - [Media types](#media-types)
  - [GET api/posts.json](#get-apipostsjson)
  - [GET api/posts.rss](#get-apipostsrss)
  - [GET api/posts/changed.json](#get-apipostschangedjson)
  - [GET api/posts/changed.rss](#get-apipostschangedrss)
  - [GET api/posts/*{postId}*.json](#get-apipostspostidjson)
  - [PUT api/posts/*{postId}*.json](#put-apipostspostidjson)
  - [POST api/posts.json](#post-apipostsjson)
  - [POST api/media_upload.json](#post-apimedia_uploadjson)
  - [POST api/user_blacklist.json](#post-apiuser_blacklistjson)
  - [DELETE api/user_blacklist.json](#delete-apiuser_blacklistjson)
  - [POST api/user_whitelist.json](#post-apiuser_whitelistjson)
  - [DELETE api/user_whitelist.json](#delete-apiuser_whitelistjson)
  - [GET api/analytics/posts.json](#get-apianalyticspostsjson)
  - [GET api/analytics/users.json](#get-apianalyticsusersjson)
  - [GET api/ads.json](#get-apiadsjson)


All endpoints require a valid API access token. Find out how to get one in the [FAQs].

> **Note**: It is not permitted to access our API directly from the browser, because this would expose your secret access token to the public. 
>
> Instead, call the API from your server and cache the posts there.

All JSON endpoints also support the `.xml` extension.

