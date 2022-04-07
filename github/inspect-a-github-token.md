# Inspect a GitHub Token

Sometimes you stuble upon a GitHub token you don't know where it's coming, from or who it belongs to.

Here's how to discover the owner:

```shell
$ curl -H "Authorization: bearer <token>" -i https://api.github.com/user
HTTP/2 200
server: GitHub.com
date: Thu, 07 Apr 2022 09:13:25 GMT
content-type: application/json; charset=utf-8
content-length: 1587
<snip> a lot of headers
{
  "login": "zmoog",
  "id": 25941,
  "node_id": "MDQ6VXNlcjI1OTQx",
  "avatar_url": "https://avatars.githubusercontent.com/u/25941?v=4",
  "gravatar_id": "",
  "url": "https://api.github.com/users/zmoog",
  "html_url": "https://github.com/zmoog",
  "followers_url": "https://api.github.com/users/zmoog/followers",
  "following_url": "https://api.github.com/users/zmoog/following{/other_user}",
  "gists_url": "https://api.github.com/users/zmoog/gists{/gist_id}",
  "starred_url": "https://api.github.com/users/zmoog/starred{/owner}{/repo}",
  "subscriptions_url": "https://api.github.com/users/zmoog/subscriptions",
  "organizations_url": "https://api.github.com/users/zmoog/orgs",
  "repos_url": "https://api.github.com/users/zmoog/repos",
  "events_url": "https://api.github.com/users/zmoog/events{/privacy}",
  "received_events_url": "https://api.github.com/users/zmoog/received_events",
  "type": "User",
  "site_admin": false,
  "name": "Maurizio Branca",
  "blog": "https://zmoog.dev",
  "location": "Turin,Italy",
  "hireable": null,
  "bio": null,
  "twitter_username": "zmoog",
  "public_repos": 56,
  "public_gists": 6,
  "followers": 20,
  "following": 29,
  "created_at": "2008-09-23T17:16:36Z",
  "updated_at": "2022-04-06T21:49:50Z",
  "private_gists": 2,
  "total_private_repos": 9,
  "owned_private_repos": 9,
  "disk_usage": 44593,
  "collaborators": 2,
  "two_factor_authentication": true,
  "plan": {
    "name": "free",
    "space": 976562499,
    "collaborators": 0,
    "private_repos": 10000
  }
}
```
