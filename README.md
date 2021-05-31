Walls.io API Documentation
==========================

## Endpoints
- Posts
  * [__GET__ `/posts`] Get a list of posts
  * [__GET__ `/posts/changed`] Get a list of posts, ordered by the time they were updated


[__GET__ `/posts`]: endpoints/GET_posts.md
[__GET__ `/posts/changed`]: endpoints/GET_posts-changed.md

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

