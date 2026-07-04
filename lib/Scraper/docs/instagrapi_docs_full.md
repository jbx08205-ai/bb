

# Source: https://subzeroid.github.io/instagrapi/usage-guide/fundamentals.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Usage Guide
This section provides detailed descriptions of all the ways `instagrapi` can be used. If you are new to `instagrapi`, the [Getting Started](https://subzeroid.github.io/instagrapi/getting-started.html) page provides a gradual introduction of the basic functionality with examples.
## Public vs Private Requests
  * `Public` web methods have a suffix `_gql` (Instagram `GraphQL`). Some `_gql` helpers use newer `doc_id` queries when Instagram disables legacy `query_hash` endpoints. Legacy `?__a=1` helpers were removed because that public web response is no longer reliable.
  * `Private` (authorized request via mobile api) methods have `_v1` suffix


Public web flows are opportunistic, not guaranteed. Instagram can change or block them independently of the library.
Many high-level helpers try a public/web path first and then use a private/authenticated fallback when that makes sense for the current session.
Not every high-level helper has a public and private twin. Some newer flows are private-only, while some lookup helpers use an internal fallback chain and choose the best currently working path for the session.
## Detailed Sections
  * [Index](https://subzeroid.github.io/instagrapi/)
  * [Getting Started](https://subzeroid.github.io/instagrapi/getting-started.html)
  * [Interactions](https://subzeroid.github.io/instagrapi/usage-guide/interactions.html)
    * [`Media`](https://subzeroid.github.io/instagrapi/usage-guide/media.html) - Publication (also called post): Photo, Video, Album, IGTV and Reels
    * [`Resource`](https://subzeroid.github.io/instagrapi/usage-guide/media.html) - Part of Media (for albums)
    * [`MediaOembed`](https://subzeroid.github.io/instagrapi/usage-guide/media.html) - Short version of Media
    * [`Account`](https://subzeroid.github.io/instagrapi/usage-guide/account.html) - Full private info for your account (e.g. email, phone_number)
    * [`User`](https://subzeroid.github.io/instagrapi/usage-guide/user.html) - Full public user data
    * [`UserShort`](https://subzeroid.github.io/instagrapi/usage-guide/user.html) - Short public user data (used in Usertag, Comment, Media, Direct Message)
    * [`Usertag`](https://subzeroid.github.io/instagrapi/usage-guide/user.html) - Tag user in Media (coordinates + UserShort)
    * [`Location`](https://subzeroid.github.io/instagrapi/usage-guide/location.html) - GEO location (GEO coordinates, name, address)
    * [`Hashtag`](https://subzeroid.github.io/instagrapi/usage-guide/hashtag.html) - Hashtag object (id, name, picture)
    * [`Collection`](https://subzeroid.github.io/instagrapi/usage-guide/collection.html) - Collection of medias (name, picture and list of medias)
    * [`Comment`](https://subzeroid.github.io/instagrapi/usage-guide/comment.html) - Comments to Media
    * [`Highlight`](https://subzeroid.github.io/instagrapi/usage-guide/highlight.html) - Highlights
    * [`Notes`](https://subzeroid.github.io/instagrapi/usage-guide/notes.html) - Direct Notes
    * [`Realtime MQTT`](https://subzeroid.github.io/instagrapi/usage-guide/realtime.html) - Direct sync, lightweight Direct MQTT actions, and FBNS push callbacks
    * [`Pydroid and ffmpeg`](https://subzeroid.github.io/instagrapi/usage-guide/pydroid.html) - Android/Pydroid video upload setup
    * [`Termux`](https://subzeroid.github.io/instagrapi/usage-guide/termux.html) - Termux install notes and optional video helpers
    * [`Story`](https://subzeroid.github.io/instagrapi/usage-guide/story.html) - Story
    * [`StoryArchiveDay`](https://subzeroid.github.io/instagrapi/usage-guide/story.html) - Story archive day shell
    * [`StoryLink`](https://subzeroid.github.io/instagrapi/usage-guide/story.html) - Story link sticker
    * [`StoryLocation`](https://subzeroid.github.io/instagrapi/usage-guide/story.html) - Tag Location in Story (as sticker)
    * [`StoryMention`](https://subzeroid.github.io/instagrapi/usage-guide/story.html) - Mention users in Story (user, coordinates and dimensions)
    * [`StoryHashtag`](https://subzeroid.github.io/instagrapi/usage-guide/story.html) - Hashtag for story (as sticker)
    * [`StorySticker`](https://subzeroid.github.io/instagrapi/usage-guide/story.html) - Tag sticker to story (for example from giphy)
    * [`StoryBuild`](https://subzeroid.github.io/instagrapi/usage-guide/story.html) - [StoryBuilder](https://github.com/subzeroid/instagrapi/blob/master/instagrapi/story.py) return path to photo/video and mention co-ordinates
    * [`DirectThread`](https://subzeroid.github.io/instagrapi/usage-guide/direct.html) - Thread (topic) with messages in Direct Message
    * [`DirectMessage`](https://subzeroid.github.io/instagrapi/usage-guide/direct.html) - Message in Direct Message
    * [`Insight`](https://subzeroid.github.io/instagrapi/usage-guide/insight.html) - Insights for a post
    * [`Track`](https://subzeroid.github.io/instagrapi/usage-guide/track.html) - Music track (for Reels/Clips)
  * [Best Practices](https://subzeroid.github.io/instagrapi/usage-guide/best-practices.html)
  * [Development Guide](https://subzeroid.github.io/instagrapi/development-guide.html)
  * [Handle Exceptions](https://subzeroid.github.io/instagrapi/usage-guide/handle_exception.html)
  * [Exceptions](https://subzeroid.github.io/instagrapi/exceptions.html)




---


# Source: https://subzeroid.github.io/instagrapi/getting-started.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Getting Started
## Installation
Install `instagrapi` with pip:

```
python -m pip install instagrapi

```

Supported runtime:
  * `Python 3.10+`
  * `Python 3.9` support was dropped in `2.5.0` — pin to `instagrapi==2.4.5` if you need it.


## Introduction
`instagrapi` is an unofficial Instagram API wrapper for Python. It combines public web and private mobile flows, supports session persistence and challenge handling, and exposes a broad set of primitives for users, media, stories, direct messages, notes, uploads, and insights.
A good first production habit is to avoid password login on every run. Prefer:

```
from instagrapi import Client

cl = Client()
cl.login(USERNAME, PASSWORD)
cl.dump_settings("session.json")

```

Then on the next run:

```
from instagrapi import Client

cl = Client()
cl.load_settings("session.json")
cl.login(USERNAME, PASSWORD)

```

## What’s Next?
  * [Runnable examples](https://subzeroid.github.io/instagrapi/usage-guide/examples.html)
  * [Fundamentals](https://subzeroid.github.io/instagrapi/usage-guide/fundamentals.html)
  * [Interactions](https://subzeroid.github.io/instagrapi/usage-guide/interactions.html)
  * [Best Practices](https://subzeroid.github.io/instagrapi/usage-guide/best-practices.html)
  * [Handle Exceptions](https://subzeroid.github.io/instagrapi/usage-guide/handle_exception.html)
  * [Challenge Resolver](https://subzeroid.github.io/instagrapi/usage-guide/challenge_resolver.html)
  * [Exceptions](https://subzeroid.github.io/instagrapi/exceptions.html)




---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/interactions.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Interactions
`instagrapi` provides various types of `Interactions` that can be used to control how the program will interact with the `Instagram`:
  * [`Media`](https://subzeroid.github.io/instagrapi/usage-guide/media.html) - Media (Photo, Video, Album, IGTV, Reels or Story)
  * [Types](https://subzeroid.github.io/instagrapi/usage-guide/types.html) - Field reference for public `instagrapi.types` models
  * [`Resource`](https://subzeroid.github.io/instagrapi/usage-guide/media.html) - Part of Media (for albums)
  * [`MediaOembed`](https://subzeroid.github.io/instagrapi/usage-guide/media.html) - Short version of Media
  * [`Account`](https://subzeroid.github.io/instagrapi/usage-guide/account.html) - Full private info for your account (e.g. email, phone_number)
  * [`TOTP`](https://subzeroid.github.io/instagrapi/usage-guide/totp.html) - 2FA TOTP helpers (generate seed, enable/disable TOTP, generate code as Google Authenticator)
  * [`User`](https://subzeroid.github.io/instagrapi/usage-guide/user.html) - Full public user data
  * [`UserShort`](https://subzeroid.github.io/instagrapi/usage-guide/user.html) - Short public user data (used in Usertag, Comment, Media, Direct)
  * [`Usertag`](https://subzeroid.github.io/instagrapi/usage-guide/user.html) - Tag user in Media (coordinates + UserShort)
  * [`Location`](https://subzeroid.github.io/instagrapi/usage-guide/location.html) - GEO location (GEO coordinates, name, address)
  * [`Hashtag`](https://subzeroid.github.io/instagrapi/usage-guide/hashtag.html) - Hashtag object (id, name, picture)
  * [`Collection`](https://subzeroid.github.io/instagrapi/usage-guide/collection.html) - Collection of medias (name, picture and list of medias)
  * [`Comment`](https://subzeroid.github.io/instagrapi/usage-guide/comment.html) - Comments to Media
  * [`Highlight`](https://subzeroid.github.io/instagrapi/usage-guide/highlight.html) - Highlights
  * [`Story`](https://subzeroid.github.io/instagrapi/usage-guide/story.html) - Story
  * [`StoryArchiveDay`](https://subzeroid.github.io/instagrapi/usage-guide/story.html) - Story archive day shell
  * [`StoryLink`](https://subzeroid.github.io/instagrapi/usage-guide/story.html) - Story link sticker
  * [`StoryLocation`](https://subzeroid.github.io/instagrapi/usage-guide/story.html) - Tag Location in Story (as sticker)
  * [`StoryMention`](https://subzeroid.github.io/instagrapi/usage-guide/story.html) - Mention users in Story (user, coordinates and dimensions)
  * [`StoryHashtag`](https://subzeroid.github.io/instagrapi/usage-guide/story.html) - Hashtag for story (as sticker)
  * [`StorySticker`](https://subzeroid.github.io/instagrapi/usage-guide/story.html) - Tag sticker to story (for example from giphy)
  * [`StoryBuild`](https://subzeroid.github.io/instagrapi/usage-guide/story.html) - [StoryBuilder](https://github.com/subzeroid/instagrapi/blob/master/instagrapi/story.py) return path to photo/video and mention co-ordinates
  * [`DirectThread`](https://subzeroid.github.io/instagrapi/usage-guide/direct.html) - Thread (topic) with messages in Direct
  * [`DirectMessage`](https://subzeroid.github.io/instagrapi/usage-guide/direct.html) - Message in Direct
  * [`Insight`](https://subzeroid.github.io/instagrapi/usage-guide/insight.html) - Insights for a post
  * [`Track`](https://subzeroid.github.io/instagrapi/usage-guide/track.html) - Music track (for Reels/Clips)
  * [`Note`](https://subzeroid.github.io/instagrapi/usage-guide/notes.html) - Direct Notes


## Interacting with Instagram Account
`instagrapi` provides the following `Interactions` that can be used to control and get the information about your `Instagram` account:
  * `Client(settings: dict = {}, proxy: str = "", tls_verify: Union[bool, str] = True)` - Init `instagrapi` client



```
cl.login("instagrapi", "42")
# cl.login("instagrapi", "42", verification_code="123456")  # with 2FA verification_code
# cl.login_by_sessionid("peiWooShooghahdi2Eip7phohph0eeng")
cl.set_proxy("socks5://127.0.0.1:30235")
# cl.set_proxy("http://username:password@127.0.0.1:8080")
# cl.set_proxy("socks5://username:password@127.0.0.1:30235")
# when addressing the proxy via hostname:
# cl.set_proxy("socks5h://username:password@exampleproxy.tld:30235")

print(cl.get_settings())
print(cl.user_info(cl.user_id))

```

### Request  
| Property  | Description  |  
| --- | --- |  
| request_logger  | Logger in which various actions from Instagram are registered  |  
| request_timeout  | Timeout in seconds between requests (1 second by default)  |  
| public_request_retries_count  | Default retry count for `public_request()`  |  
| public_request_retries_timeout  | Delay between `public_request()` retries  |  
| session_retry_total  | Transport-level retry count for `public` and `private` sessions  |  
| session_retry_backoff_factor  | Backoff factor for transport-level retries  |  
| public_transport  | Public web transport: `requests` by default, or `curl` when `instagrapi[curl]` is installed  |  
| public_transport_impersonate  | Browser fingerprint used by the optional curl public transport  |  
| tls_verify  | TLS certificate verification: `True` by default, `False` for temporary trusted MITM debugging, or a CA bundle path  |  
### Login  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| login(username: str, password: str)  | bool  | Login by username and password (get new cookies if it does not exist in settings)  |  
| login(username: str, password: str, verification_code: str)  | bool  | Login by username and password with 2FA verification code (use Google Authenticator or something similar to generate TOTP code, not work with SMS)  |  
| relogin()  | bool  | Re-login with clean cookies (required cl.username and cl.password)  |  
| login_by_sessionid(sessionid: str)  | bool  | Lightweight compatibility login using a session cookie value  |  
| inject_sessionid_to_public()  | bool  | Inject sessionid from Private Session to Public Session  |  
| logout()  | bool  | Logout  |  
`login_by_sessionid()` only works when Instagram accepts that `sessionid` for the private mobile API. A browser/web `sessionid` can be rejected with `login_required` or invalidated server-side; for long-lived automation, prefer `login()` once, then `dump_settings()` and reuse the saved settings.
When `login_by_sessionid()` needs to recover the account username after a private profile lookup failure, it tries the private mobile profile stream before falling back to public/web GraphQL.
You can pass settings to the Client (and save cookies), it has the following format:

```
settings = {
   "uuids": {
      "phone_id": "57d64c41-a916-3fa5-bd7a-3796c1dab122",
      "uuid": "8aa373c6-f316-44d7-b49e-d74563f4a8f3",
      "client_session_id": "6c296d0a-3534-4dce-b5aa-a6a6ab017443",
      "advertising_id": "8dc88b76-dfbc-44dc-abbc-31a6f1d54b04",
      "device_id": "android-e021b636049dc0e9"
   },
   "authorization_data": {},  # sessionid / ds_user_id / authorization values
   "cookies":  {},  # saved cookies
   "last_login": 1596069420.0000145,
   "device_settings": {
      "cpu": "h1",
      "dpi": "640dpi",
      "model": "h1",
      "device": "RS988",
      "resolution": "1440x2392",
      "manufacturer": "LGE/lge",
      "android_release": "6.0.1",
      "android_version": 23
   },
   "user_agent": "Instagram 385.0.0.47.74 Android (...)",
   "country": "US",
   "country_code": 1,
   "locale": "en_US",
   "timezone_offset": -14400,
   "request_timeout": 1,
   "public_request_retries_count": 3,
   "public_request_retries_timeout": 2,
   "session_retry_total": 3,
   "session_retry_backoff_factor": 2,
   "session_retry_statuses": [429, 500, 502, 503, 504],
   "public_transport": "requests",
   "public_transport_impersonate": "chrome136",
   "tls_verify": True
}

cl = Client(settings)

```

### Settings
Store and manage uuids, device configuration, user agent, authorization data (aka cookies) and other session settings  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| get_settings()  | dict  | Return settings dict  |  
| set_settings(settings: dict)  | bool  | Set session settings  |  
| load_settings(path: Path)  | dict  | Load session settings from file  |  
| dump_settings(path: Path)  | bool  | Serialize and save session settings to file  |  
In order for Instagram [to trust you more](https://github.com/subzeroid/instagrapi/discussions/220), use one stable device profile and one stable IP (or subnet) per account whenever possible:

```
cl = Client()
cl.login(USERNAME, PASSWORD)
cl.dump_settings('/tmp/dump.json')

```

Next time:

```
cl = Client()
cl.set_settings(cl.load_settings('/tmp/dump.json'))
cl.login(USERNAME, PASSWORD)
cl.get_timeline_feed()  # check session

```

### Manage device, proxy and other account settings  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| set_proxy(dsn: str)  | dict  | Support socks and http/https proxy `scheme://username:password@host:port`  |  
| private.proxies  | dict  | Stores used proxy servers for private (mobile, v1) requests  |  
| public.proxies  | dict  | Stores used proxy servers for public (web, graphql) requests  |  
| set_device(device: dict)  | bool  | Change device settings ([Android Device Information Generator Online](https://www.myfakeinfo.com/mobile/get-android-device-information.php))  |  
| set_app(app: Union[str, Dict] = None)  | bool  | Apply a supported Instagram app version profile (`app_version`, `version_code`, `bloks_versioning_id`)  |  
| device  | dict  | Return device dict which we pass to Instagram  |  
| set_user_agent(user_agent: str = “”)  | bool  | Change User-Agent header ([User Agents](https://user-agents.net/applications/instagram-app))  |  
| cookie_dict  | dict  | Return cookies  |  
| user_id  | int  | Return your user_id (after login)  |  
| base_headers  | dict  | Base headers for Instagram  |  
| set_country(country: str = “US”)  | bool  | Set country (advice: use the country of your proxy)  |  
| set_country_code(country_code: int = 1)  | bool  | Set country calling code. Default: +1 (USA)  |  
| set_locale(locale: str = “en_US”)  | bool  | Set locale (advice: use the locale of your proxy)  |  
| set_timezone_offset(seconds: int)  | bool  | Set timezone offset in seconds  |  
| set_retry_config(…)  | bool  | Configure request timeout plus public/manual and session/transport retry settings  |  
| set_tls_verify(tls_verify: bool | str)  | bool  | Update TLS certificate verification for existing public, private and GraphQL sessions  |  
Example:

```
cl = Client(
    request_timeout=0,
    public_request_retries_count=4,
    public_request_retries_timeout=1,
    session_retry_total=5,
    session_retry_backoff_factor=1,
)

cl.set_retry_config(
    public_request_retries_count=2,
    public_request_retries_timeout=0,
    session_retry_total=3,
)

```

For public web endpoints that are sensitive to browser TLS fingerprints, install the optional curl transport:

```
pip install "instagrapi[curl]"

```

Then opt in explicitly:

```
cl = Client(public_transport="curl", public_transport_impersonate="chrome136")

```

The default remains `public_transport="requests"`. Private mobile API requests still use the regular mobile session. See [Public Transport](https://subzeroid.github.io/instagrapi/usage-guide/public-transport.html) for live comparison results and caveats.
### Private mobile headers
`base_headers` follows the current supported Android app profile for normal private API requests, including static transport/network hints such as `X-FB-HTTP-Engine`, `X-Tigon-Is-Retry`, and `X-Zero-*`.
Device-bound or attestation-style headers such as `x-meta-zca`, `x-meta-usdid`, and `x-ig-attest-params` are not generated by default. These values are tied to Android / Google Play / device signing context, so adding fake static values is more likely to hurt trust than help.
### TLS verification and debugging proxies
By default `instagrapi` verifies TLS certificates on all client sessions. Keep this enabled for production, residential proxies, and normal CONNECT-tunnel proxies.
If you use a trusted local debugging proxy that intercepts TLS, prefer installing its CA certificate and pointing the client at that bundle:

```
cl = Client(tls_verify="/path/to/proxy-ca.pem")

```

For short local captures you can disable verification explicitly:

```
cl = Client(tls_verify=False)

```

Do not disable TLS verification on untrusted networks or shared proxies because session cookies and passwords can be intercepted.

```
cl = Client()

# Los Angles user:
cl.set_proxy('http://los:angeles@proxy.address:8080')
cl.set_locale('en_US')
cl.set_timezone_offset(-7 * 60 * 60)  # Los Angeles UTC (GMT) -7 hours == -25200 seconds
cl.get_settings()
{
    ...
    'user_agent': 'Instagram 194.0.0.36.172 Android (26/8.0.0; 480dpi; 1080x1920; Xiaomi; MI 5s; capricorn; qcom; en_US; 301484483)',
    'country': 'US',
    'country_code': 1,
    'locale': 'en_US',
    'timezone_offset': -25200
}

# Moscow user:
cl.set_proxy('socks5://moscow:proxy@address:8080')
cl.set_locale('ru_RU')
cl.set_country_code(7)  # +7
cl.set_timezone_offset(3 * 3600)  # Moscow UTC+3
cl.get_settings()
{
    ...
    'user_agent': 'Instagram 194.0.0.36.172 Android (26/8.0.0; 480dpi; 1080x1920; Xiaomi; MI 5s; capricorn; qcom; ru_RU; 301484483)',
    'country': 'RU',
    'country_code': 7,
    'locale': 'ru_RU',
    'timezone_offset': 10800
}

```

## What’s Next?
  * [Getting Started](https://subzeroid.github.io/instagrapi/getting-started.html)
  * [Usage Guide](https://subzeroid.github.io/instagrapi/usage-guide/fundamentals.html)
  * [Best Practices](https://subzeroid.github.io/instagrapi/usage-guide/best-practices.html)
  * [Handle Exceptions](https://subzeroid.github.io/instagrapi/usage-guide/handle_exception.html)
  * [Challenge Resolver](https://subzeroid.github.io/instagrapi/usage-guide/challenge_resolver.html)
  * [Exceptions](https://subzeroid.github.io/instagrapi/exceptions.html)




---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/media.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Media
Viewing, downloading, uploading and editing publications
In terms of Instagram, this is called Media, usually users call it publications or posts
### Basic terms:
  * `media_id` - String ID `"{media_id}_{user_id}"`, e.g. `"2277033926878261772_1903424587"`
  * `media_pk` - Integer ID (real media id), e.g. `2277033926878261772`
  * `code` - Short code (slug for media), e.g. `BjNLpA1AhXM` from `"https://www.instagram.com/p/BjNLpA1AhXM/"`
  * `url` - URL to media publication, e.g. `"https://www.instagram.com/p/BjNLpA1AhXM/"`


### Media types:
  * `Photo` - When media_type=1
  * `Video` - When media_type=2 and product_type=feed
  * `IGTV` - When media_type=2 and product_type=igtv
  * `Reel` - When media_type=2 and product_type=clips
  * `Album` - When media_type=8


## Viewing and editing publication  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| media_id(media_pk: str)  | str  | Return full `media_id` by `media_pk` (e.g. `2277033926878261772 -> 2277033926878261772_1903424587`)  |  
| media_pk(media_id: str)  | str  | Return `media_pk` by full `media_id`  |  
| media_code_from_pk(media_pk: str)  | str  | Return shortcode for a media PK  |  
| media_pk_from_code(code: str)  | str  | Return media PK from shortcode  |  
| media_pk_from_url(url: str)  | str  | Return media PK from media URL; also handles `share/p/...` redirect URLs  |  
| user_medias(user_id: str, amount: int = 0)  | List[Media]  | Get user feed media  |  
| iter_user_medias(user_id: str, amount: int = 0, page_size: int = 0)  | Iterator[Media]  | Stream user feed media page by page without building a full list  |  
| user_medias_paginated(user_id: str, amount: int = 0, end_cursor: str = “”)  | Tuple[List[Media], str]  | Get one page of user media and next cursor  |  
| user_medias_chunk(user_id: str, end_cursor: str = “”)  | Tuple[List[Media], str]  | Compatibility alias for one page of user media  |  
| user_clips(user_id: str, amount: int = 0)  | List[Media]  | Get clips/reels by user  |  
| usertag_medias(user_id: str, amount: int = 0)  | List[Media]  | Get media where a user is tagged  |  
| usertag_medias_paginated(user_id: str, amount: int = 0, end_cursor: str = “”)  | Tuple[List[Media], str]  | Get one page of media where a user is tagged and next cursor  |  
| media_info(media_pk: str, use_cache: bool = True)  | Media  | Return media info  |  
| media_delete(media_id: str)  | bool  | Delete media  |  
| media_edit(media_id: str, caption: str, title: str = “”, usertags: List[Usertag] = [], location: Location = None)  | dict  | Edit caption, optional IGTV title, usertags, or location  |  
| media_user(media_pk: str)  | UserShort  | Get author of media  |  
| media_oembed(url: str)  | dict  | Return short oEmbed-style media info by URL  |  
| media_like(media_id: str)  | bool  | Like media  |  
| media_unlike(media_id: str)  | bool  | Unlike media  |  
| media_share_to_story(media_id: str, background: Path = None, caption: str = “”)  | Story  | Share an existing post to your story as a feed media sticker  |  
| media_note_create(media_id: str, text: str = “”, audience: int = 7, note_style: int = 13, extra_data: Optional[Dict] = None)  | dict  | Create a note attached to a media item  |  
| media_note_delete(note_id: str, extra_data: Optional[Dict] = None)  | bool  | Delete a note attached to a media item  |  
| media_seen(media_ids: List[str], skipped_media_ids: List[str] = [])  | bool  | Mark media as seen  |  
| media_likers(media_id: str)  | List[UserShort]  | Return users who liked this post  |  
| media_likers_gql(media_pk: str, amount: int = 0)  | List[dict]  | Return users who liked this post through the web GraphQL doc_id endpoint  |  
| archive_medias(amount: int = 0)  | List[Media]  | Get archived media from your account  |  
| media_archive(media_id: str)  | bool  | Archive media  |  
| media_unarchive(media_id: str)  | bool  | Unarchive media  |  
| media_pin(media_pk: str)  | bool  | Pin media to profile  |  
| media_unpin(media_pk: str)  | bool  | Unpin media from profile  |  
| media_template_v1(media_id: str)  | dict  | Fetch a clip template payload for a Reel/clip media  |  
| clip_mashup_info(media_pk: str)  | dict  | Fetch Reel remix/reuse availability metadata  |  
| clip_seen(media_ids: List[str], blend_media_ids: List[str] = None)  | bool  | Mark Reels/Clips as seen through the Clips seen-state endpoint  |  
| clip_pin(media_pk: str)  | bool  | Pin Reel to the Reels tab/profile Reels grid  |  
| clip_unpin(media_pk: str)  | bool  | Unpin Reel from the Reels tab/profile Reels grid  |  
| clip_change_cover(media_pk: str, cover_path: Path)  | bool  | Change the cover image for a published Reel  |  
| media_create_livestream(title: str = “Instagram Live”)  | dict  | Create a new livestream and return stream metadata  |  
| media_start_livestream(broadcast_id: str)  | dict  | Start an existing livestream  |  
| media_end_livestream(broadcast_id: str)  | dict  | End an existing livestream  |  
| media_get_livestream_info(broadcast_id: str)  | dict  | Get livestream info  |  
| media_get_livestream_comments(broadcast_id: str)  | dict  | Get livestream comments  |  
| media_get_livestream_viewers(broadcast_id: str)  | dict  | Get livestream viewers  |  
Media notes are separate from Direct inbox Notes. Use `media_note_create()` and `media_note_delete()` for the note surface attached to a post or Reel; use the [Notes guide](https://subzeroid.github.io/instagrapi/usage-guide/notes.html) for Direct inbox Notes.
Use `clip_seen()` for Reels/Clips. `media_seen()` keeps the older story/reel-tray seen payload. Instagram still decides whether a seen-state event is counted in view analytics.
Low level methods:  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| media_info_gql(media_pk: str)  | Media  | Get media from PK via public GraphQL API. Falls back from legacy `query_hash` to the newer `doc_id` media query when available.  |  
| media_info_v1(media_pk: str)  | Media  | Get media from PK via private mobile API  |  
| media_info_v2(media_id: str)  | Media  | Alternative source for media info via `discover/media_metadata/` (`media_or_ad` payload). Useful as fallback when `media_info_v1` fails on certain ad-tagged or sponsored media. Strips `_userid` suffix automatically.  |  
| user_medias_gql(user_id: str, amount: int = 0, sleep: int = 0)  | List[Media]  | Get user media via public GraphQL API  |  
| user_medias_paginated_gql(user_id: str, amount: int = 0, sleep: int = 2, end_cursor=None)  | Tuple[List[Media], str]  | Get one public GraphQL page of user media  |  
| user_medias_chunk_gql(user_id: str, sleep: int = 2, end_cursor=None, amount: int = 0)  | Tuple[List[Media], str]  | Compatibility alias for one public GraphQL page of user media  |  
| user_medias_v1(user_id: str, amount: int = 0)  | List[Media]  | Get user media via private mobile API  |  
| user_medias_paginated_v1(user_id: str, amount: int = 0, end_cursor=””)  | Tuple[List[Media], str]  | Get one private API page of user media  |  
| user_medias_chunk_v1(user_id: str, end_cursor: str = “”)  | Tuple[List[Media], str]  | Compatibility alias for one private API page of user media  |  
| user_clips_v1(user_id: str, amount: int = 0)  | List[Media]  | Get user clips via private mobile API  |  
| user_clips_paginated_v1(user_id: str, amount: int = 0, end_cursor=””)  | Tuple[List[Media], str]  | Get one private API page of clips  |  
| user_clips_chunk_v1(user_id: str, end_cursor: str = “”)  | Tuple[List[Media], str]  | Compatibility alias for one private API page of clips  |  
| user_videos_v1(user_id: str, amount: int = 0)  | List[Media]  | Get user videos via private mobile API  |  
| user_videos_paginated_v1(user_id: int, amount: int = 0, end_cursor=””)  | Tuple[List[Media], str]  | Get one private API page of videos  |  
| user_videos_chunk_v1(user_id: str, end_cursor: str = “”)  | Tuple[List[Media], str]  | Compatibility alias for one private API page of videos  |  
| usertag_medias_gql(user_id: str, amount: int = 0, sleep: int = 2)  | List[Media]  | Get media where a user is tagged via public GraphQL API  |  
| usertag_medias_paginated_gql(user_id: str, amount: int = 0, sleep: int = 2, end_cursor=None)  | Tuple[List[Media], str]  | Get one public GraphQL page of media where a user is tagged  |  
| usertag_medias_v1(user_id: str, amount: int = 0)  | List[Media]  | Get media where a user is tagged via private mobile API  |  
| usertag_medias_paginated_v1(user_id: str, amount: int = 0, end_cursor=””)  | Tuple[List[Media], str]  | Get one private API page of media where a user is tagged  |  
| usertag_medias_v1_chunk(user_id: str, max_id: str = “”)  | Tuple[List[Media], str]  | Compatibility alias for one private API page of tagged media  |  
| archive_medias_v1(amount: int = 0)  | List[Media]  | Get archived media via private mobile API  |  
| archive_medias_paginated_v1(amount: int = 0, end_cursor=””)  | Tuple[List[Media], str]  | Get one private API page of archived media  |  
### Example:

```
>>> from instagrapi import Client
>>> cl = Client()
>>> cl.login(USERNAME, PASSWORD)

>>> cl.media_pk_from_code("B-fKL9qpeab")
2278584739065882267

>>> cl.media_pk_from_code("B8jnuB2HAbyc0q001y3F9CHRSoqEljK_dgkJjo0")
2243811726252050162

>>> cl.media_pk_from_url("https://www.instagram.com/p/BjNLpA1AhXM/")
1787135824035452364

>>> cl.media_pk_from_url("https://www.instagram.com/share/p/BA123456789/")
1787135824035452364

>>> cl.media_info(1787135824035452364).dict()
{'pk': 1787135824035452364,
 'id': '1787135824035452364_1903424587',
 'code': 'BjNLpA1AhXM',
 'taken_at': datetime.datetime(2018, 5, 25, 15, 46, 53, tzinfo=datetime.timezone.utc),
 'media_type': 8,
 'product_type': '',
 'thumbnail_url': None,
 'location': {'pk': 260916528,
  'name': 'Foros, Crimea',
  'address': '',
  'lng': 33.7878,
  'lat': 44.3914,
  'external_id': 181364832764479,
  'external_id_source': 'facebook_places'},
 'user': {'pk': 1903424587,
  'username': 'example',
  'full_name': 'Example Example',
  'profile_pic_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t51.2885-19/s150x150/123884060_...&oe=5FD7600E')},
 'comment_count': 0,
 'like_count': 48,
 'caption_text': '@mind__flowers в Форосе под дождём, 24 мая 2018 #downhill #skateboarding #downhillskateboarding #crimea #foros',
 'usertags': [],
 'video_url': None,
 'view_count': 0,
 'video_duration': 0.0,
 'title': '',
 'resources': [{'pk': 1787135361353462176,
   'video_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t50.2886-16/33464086_3755...0e2362', scheme='https', ...),
   'thumbnail_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t51.2885-15/e35/3220311...AE7332', scheme='https', ...),
   'media_type': 2},
  {'pk': 1787135762219834098,
   'video_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t50.2886-16/32895...61320_n.mp4', scheme='https', ...),
   'thumbnail_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t51.2885-15/e35/3373413....8480_n.jpg', scheme='https', ...),
   'media_type': 2},
  {'pk': 1787133803186894424,
   'video_url': None,
   'thumbnail_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t51.2885-15/e35/324307712_n.jpg...', scheme='https', ...),
   'media_type': 1}]}

>>> cl.media_oembed("https://www.instagram.com/p/B3mr1-OlWMG/").dict()
{'version': '1.0',
 'title': 'В гостях у ДК @delai_krasivo_kaifui',
 'author_name': 'example',
 'author_url': 'https://www.instagram.com/example',
 'author_id': 1903424587,
 'media_id': '2154602296692269830_1903424587',
 'provider_name': 'Instagram',
 'provider_url': 'https://www.instagram.com',
 'type': 'rich',
 'width': 658,
 'height': None,
 'html': '<blockquote>...',
 'thumbnail_url': 'https://instagram.frix7-1.fna.fbcdn.net/v...0655800983_n.jpg',
 'thumbnail_width': 640,
 'thumbnail_height': 480,
 'can_view': True}


>>> cl.media_archive('2155832952940083788_1903424587')
True

>>> [media.pk for media in cl.archive_medias(amount=5)]
['2155832952940083788']

>>> cl.media_unarchive('2155832952940083788_1903424587')
True

>>> cl.user_medias_gql(1903424587, amount=1)[0].dict()
{'pk': 2592252466151482347,
 'id': '2592252466151482347_1903424587',
 'code': 'CP5h-I1FuPr',
 'taken_at': datetime.datetime(2021, 6, 9, 12, 9, 56, tzinfo=datetime.timezone.utc),
 'media_type': 8,
 'product_type': '',
 'thumbnail_url': None,
 'location': None,
 'user': {'pk': 1903424587,
  'username': 'example',
  'full_name': '',
  'profile_pic_url': None,
  'profile_pic_url_hd': None,
  'stories': []},
 'comment_count': 5,
 'like_count': 63,
 'has_liked': None,
 'caption_text': 'Любимые подвески ♥️ @daewon1song @tensortrucks',
 'usertags': [{'user': {'pk': 53860445,
    'username': 'tensortrucks',
    'full_name': '',
    'profile_pic_url': None,
    'profile_pic_url_hd': None,
    'stories': []},
   'x': 0.3146666667,
   'y': 0.368159204}],
 'video_url': None,
 'view_count': 0,
 'video_duration': 0.0,
 'title': '',
 'resources': [{'pk': 2592252463089480898,
   'video_url': None,
   'thumbnail_url': HttpUrl('https://instagram.fhel5-1.fna.fbcdn.net/v/t51.2885-15/e35/s1080x1080/198404255_317668533141074_749682826672118306_n.jpg?_nc_ht=instagram.fhel5-1.fna.fbcdn.net&_nc_cat=102&_nc_ohc=f8FR-bZNbp8AX-A6YQ4&edm=APU89FABAAAA&ccb=7-4&oh=864bb145a4fa7e523f5cc22f9ac5d015&oe=61145E4F&_nc_sid=86f79a', scheme='https', host='instagram.fhel5-1.fna.fbcdn.net', tld='net', host_type='domain', path='/v/t51.2885-15/e35/s1080x1080/198404255_317668533141074_749682826672118306_n.jpg', query='_nc_ht=instagram.fhel5-1.fna.fbcdn.net&_nc_cat=102&_nc_ohc=f8FR-bZNbp8AX-A6YQ4&edm=APU89FABAAAA&ccb=7-4&oh=864bb145a4fa7e523f5cc22f9ac5d015&oe=61145E4F&_nc_sid=86f79a'),
   'media_type': 1},
  {'pk': 2592252463081081550,
   'video_url': None,
   'thumbnail_url': HttpUrl('https://instagram.fhel5-1.fna.fbcdn.net/v/t51.2885-15/e35/s1080x1080/198228498_303261361473979_3031095263106513772_n.jpg?_nc_ht=instagram.fhel5-1.fna.fbcdn.net&_nc_cat=107&_nc_ohc=C9SeKrAO6poAX-nXhCG&edm=APU89FABAAAA&ccb=7-4&oh=6aab825e12fef746449be22c322762a1&oe=61132FB0&_nc_sid=86f79a', scheme='https', host='instagram.fhel5-1.fna.fbcdn.net', tld='net', host_type='domain', path='/v/t51.2885-15/e35/s1080x1080/198228498_303261361473979_3031095263106513772_n.jpg', query='_nc_ht=instagram.fhel5-1.fna.fbcdn.net&_nc_cat=107&_nc_ohc=C9SeKrAO6poAX-nXhCG&edm=APU89FABAAAA&ccb=7-4&oh=6aab825e12fef746449be22c322762a1&oe=61132FB0&_nc_sid=86f79a'),
   'media_type': 1},
  {'pk': 2592252463056089912,
   'video_url': None,
   'thumbnail_url': HttpUrl('https://instagram.fhel5-1.fna.fbcdn.net/v/t51.2885-15/e35/s1080x1080/199142152_323583732599636_4553823395468898634_n.jpg?_nc_ht=instagram.fhel5-1.fna.fbcdn.net&_nc_cat=108&_nc_ohc=_feIkorChpsAX_wzTff&edm=APU89FABAAAA&ccb=7-4&oh=a22a2f5b30772fbbb02db92b9394e981&oe=61147D59&_nc_sid=86f79a', scheme='https', host='instagram.fhel5-1.fna.fbcdn.net', tld='net', host_type='domain', path='/v/t51.2885-15/e35/s1080x1080/199142152_323583732599636_4553823395468898634_n.jpg', query='_nc_ht=instagram.fhel5-1.fna.fbcdn.net&_nc_cat=108&_nc_ohc=_feIkorChpsAX_wzTff&edm=APU89FABAAAA&ccb=7-4&oh=a22a2f5b30772fbbb02db92b9394e981&oe=61147D59&_nc_sid=86f79a'),
   'media_type': 1}]}

# Use paginated interface to resume fetch from stored cursor

>>> end_cursor = None
... for page in range(3):
...     medias, end_cursor = client.user_medias_paginated(1903424587, 5, end_cursor=end_cursor)
...     print([ m.taken_at.date().isoformat() for m in medias ])
...

['2021-06-09', '2019-10-16', '2019-10-14', '2019-06-13', '2019-06-06']
['2019-06-05', '2019-03-23', '2019-03-23', '2018-11-15', '2018-10-16']
['2018-10-16', '2018-10-11', '2018-10-09', '2018-10-09', '2018-08-02']

# Stream user media without storing every fetched page

>>> for media in client.iter_user_medias(1903424587, amount=100, page_size=25):
...     print(media.pk, media.code)
...

# Resume tagged-media fetches from a stored cursor

>>> tagged, end_cursor = client.usertag_medias_paginated(1903424587, 12, end_cursor="")
>>> next_tagged, end_cursor = client.usertag_medias_paginated(1903424587, 12, end_cursor=end_cursor)

>>> media_id = cl.media_id(1787135824035452364)
>>> cl.media_like(media_id)
True
>>> cl.media_unlike(media_id)
True

>>> media_pk = cl.media_pk_from_url("https://www.instagram.com/p/CGgDsi7JQdS/")
>>> story = cl.media_share_to_story(media_pk)
>>> story.pk
'3155832952940083788'


```

Notes:
  * `media_info()` uses private/mobile lookup first when the client has authorization data or a saved `sessionid`, then falls back to public/web lookup. Without authorization, it keeps public/web-first behavior. Explicit `media_info_gql()` still calls the public/web path directly.
  * `user_medias()` and `user_medias_paginated()` use private/mobile lookup first when the client has authorization data or a saved `sessionid`, then fall back to public/web lookup. Without authorization, they keep public/web-first behavior. Explicit `_gql` methods still call the public/web path directly.
  * Use `iter_user_medias()` for large profile media scans when you want each `Media` as soon as its page is fetched. Set `page_size` to control request size; leave it as `0` to keep the endpoint default.
  * `usertag_medias()` and `usertag_medias_paginated()` use private/mobile lookup first when the client has authorization data or a saved `sessionid`, then fall back to public/web lookup. Without authorization, they keep public/web-first behavior. Explicit `_gql` methods still call the public/web path directly.
  * For Reels where Instagram hides like/view counts, the public GraphQL path can expose play/view counts but not hidden like totals; `like_count` can be `-1`.
  * Extended media metadata from Instagram payloads is available on `Media` when returned by the source API, including caption edit state, dimensions, audio presence, hidden count state, viewer save/reshare state, paid partnership/affiliate flags, DASH video info, clips music attribution, and inline comment previews.
  * `media_pk_from_url()` now also resolves `share/p/...` URLs before extracting the canonical shortcode.
  * Accepted Instagram Collabs/coauthor users from private media payloads are available as `media.coauthor_producers`. This is separate from upload-time `coauthor_user_ids`, which only sends collaborator invitations.
  * `media_edit()` uses `caption` and optional `location`/`usertags`; for IGTV posts it can also derive or send a separate `title`.


Extended `Media` metadata fields:  
| Field  | Type  | Notes  |  
| --- | --- | --- |  
| `comments_preview`  |  `MediaCommentsPreview` or `None`  | Inline public/web comment preview when Instagram includes `edge_media_to_parent_comment` or preview comment edges. Use full comments helpers for complete pagination.  |  
| `hoisted_comments`  | `List[MediaInlineComment]`  | Comments Instagram hoists separately from the regular preview list. Usually empty.  |  
| `comments_preview.count`  | `int`  | Total count reported for the inline preview edge.  |  
| `comments_preview.has_next_page`  | `bool`  | Whether the inline preview edge has more comments after `end_cursor`.  |  
| `comments_preview.end_cursor`  |  `str` or `None`  | Cursor reported by the inline preview edge.  |  
| `comments_preview.comments`  | `List[MediaInlineComment]`  | Inline parent comments already present in the media payload.  |  
| `MediaInlineComment.pk`  | `str`  | Comment id.  |  
| `MediaInlineComment.text`  | `str`  | Comment text.  |  
| `MediaInlineComment.user`  | `UserShort`  | Comment author.  |  
| `MediaInlineComment.created_at_utc`  | `datetime`  | Comment creation time.  |  
| `MediaInlineComment.has_liked`  |  `bool` or `None`  | Current viewer like state when Instagram sends it.  |  
| `MediaInlineComment.like_count`  |  `int` or `None`  | Inline like count from the comment edge.  |  
| `MediaInlineComment.replied_to_comment_id`  |  `str` or `None`  | Parent comment id for inline replies.  |  
| `MediaInlineComment.did_report_as_spam`  |  `bool` or `None`  | Viewer report state when Instagram sends it.  |  
| `MediaInlineComment.is_restricted_pending`  |  `bool` or `None`  | Restricted/pending state when Instagram sends it.  |  
| `MediaInlineComment.replies_count`  | `int`  | Number of threaded replies reported inline.  |  
| `MediaInlineComment.replies`  | `List[MediaInlineComment]`  | Inline threaded replies already present in the media payload.  |  
## Download media  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| photo_download(media_pk: int, folder: Path, overwrite: bool = True)  | Path  | Download photo (path to photo with best resolution)  |  
| photo_download_by_url(url: str, filename: str, folder: Path, overwrite: bool = True)  | Path  | Download photo by URL (path to photo with best resolution)  |  
| video_download(media_pk: int, folder: Path, overwrite: bool = True)  | Path  | Download video (path to video with best resoluton)  |  
| video_download_by_url(url: str, filename: str, folder: Path, overwrite: bool = True)  | Path  | Download Video by URL (path to video with best resoluton)  |  
| album_download(media_pk: int, folder: Path, overwrite: bool = True)  | Path  | Download Album (multiple paths to photo/video with best resolutons)  |  
| album_download_by_urls(urls: List[str], folder: Path, overwrite: bool = True)  | Path  | Download Album by URLs (multiple paths to photo/video)  |  
| igtv_download(media_pk: int, folder: Path)  | Path  | Download IGTV (path to video with best resoluton)  |  
| igtv_download_by_url(url: str, filename: str, folder: Path)  | Path  | Download IGTV by URL (path to video with best resoluton)  |  
| clip_download(media_pk: int, folder: Path)  | Path  | Download Reels Clip (path to video with best resoluton)  |  
| clip_download_by_url(url: str, filename: str, folder: Path)  | Path  | Download Reels Clip by URL (path to video with best resoluton)  |  
`photo_download()` resolves photo metadata through the public/web media-info path first so it can use the largest display resource Instagram exposes for the post, then falls back to private/mobile metadata when the public web endpoint is gated. It does not rewrite CDN URLs manually.
### Example:

```

>>> from instagrapi import Client
>>> cl = Client()
>>> cl.login(USERNAME, PASSWORD)

>>> cl.media_pk_from_url("https://www.instagram.com/p/BqNQJleFoSJ/")
1913256444155036809

>>> video_url = cl.media_info(1913256444155036809).video_url
>>> cl.video_download_by_url(video_url, folder='/tmp')
PosixPath('/tmp/45588546_367538213983456_6830188946193737023_n.mp4')


```


```

>>> # Skip re-downloading if the target file already exists
>>> cl.video_download_by_url(video_url, folder='/tmp', overwrite=False)
PosixPath('/tmp/45588546_367538213983456_6830188946193737023_n.mp4')


```

If Instagram returns a `Content-Length` header and the downloaded file is shorter, download helpers remove the partial file and raise `ClientIncompleteReadError`.

```

>>> cl.media_pk_from_url("http://www.instagram.com/p/BjNLpA1AhXM/")
1787135824035452364

>>> cl.album_download(1787135824035452364)
[PosixPath('/app/example_1787135361353462176.mp4'),
 PosixPath('/app/example_1787135762219834098.mp4'),
 PosixPath('/app/example_1787133803186894424.jpg')]


```

## Upload media
Upload medias to your feed. Common arguments:
  * `path` - Path to source file
  * `caption` - Text for you post
  * `usertags` - List[Usertag] of mention users (see `Usertag` in [types.py](https://github.com/subzeroid/instagrapi/blob/master/instagrapi/types.py))
  * `location` - Location (e.g. `Location(name='Test', lat=42.0, lng=42.0)`)
  * `schedule_at` - Unix timestamp in seconds or `datetime` for scheduled publishing on eligible professional accounts

  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| photo_upload(path: Path, caption: str, upload_id: str, usertags: List[Usertag], location: Location, extra_data: Dict = {}, schedule_at: int | datetime = None, coauthor_user_ids: List[int | str] = None)  | Media  | Upload photo (Support JPG files)  |  
| video_upload(path: Path, caption: str, thumbnail: Path, usertags: List[Usertag], location: Location, extra_data: Dict = {}, schedule_at: int | datetime = None, coauthor_user_ids: List[int | str] = None)  | Media  | Upload video (Support MP4 files)  |  
| album_upload(paths: List[Path], caption: str, usertags: List[Usertag], location: Location, extra_data: Dict = {}, schedule_at: int | datetime = None, coauthor_user_ids: List[int | str] = None)  | Media  | Upload Album (Support JPG/MP4 files)  |  
| igtv_upload(path: Path, title: str, caption: str, thumbnail: Path, usertags: List[Usertag], location: Location, extra_data: Dict = {})  | Media  | Upload IGTV (Support MP4 files)  |  
| clip_upload(path: Path, caption: str, thumbnail: Path, usertags: List[Usertag], location: Location, extra_data: Dict = {}, trial: bool = False, trial_graduation_strategy: str = “manual”, share_to_facebook: bool = False, topics: List[int | str] = None, show_preview_in_feed: bool = True)  | Media  | Upload Reels Clip (Support MP4 files). Set `trial=True` to publish a Trial Reel on eligible accounts. Set `share_to_facebook=True` to cross-post to a linked Facebook destination. Pass Reel topic `fit_id` values with `topics=[...]`. Set `show_preview_in_feed=False` to hide the feed/profile grid preview  |  
| clip_change_cover(media_pk: str, cover_path: Path)  | bool  | Change the cover image for a published Reel  |  
| clip_trial_eligible()  | bool  | Check whether Reel creation preflight reports Trial Reels enabled before uploading video bytes  |  
| clip_info_for_creation()  | dict  | Get Reel creation preflight configuration from the mobile API  |  
| clip_interest_topics()  | List[dict]  | Get Reel topic catalog items with `name` and `fit_id` values for `clip_upload(..., topics=...)`  |  
| clip_share_to_fb_config()  | dict  | Get Reel Facebook sharing configuration from the mobile API  |  
| clip_share_to_fb_unified_config()  | dict  | Get the Android cross-posting unified config used by the Reel composer  |  
| clip_share_to_fb_unified_destination(config: Dict = None)  | dict  | Resolve confirmed Reel Facebook destination fields from the unified cross-posting config  |  
| clip_share_to_fb_destination(config: Dict = None, destination_id: str = None, destination_type: Literal[“USER”, “PAGE”] = None)  | dict  | Resolve confirmed Reel Facebook destination fields without treating Account Center linking ids as publish destinations  |  
| clip_share_to_fb_extra_data(config: Dict = None, destination_id: str = None, destination_type: Literal[“USER”, “PAGE”] = None)  | dict  | Build modern Reel Facebook cross-post configure fields for manual `extra_data`  |  
| clip_music_extra_data(track: Track or dict, product: MUSIC_PRODUCT = “story_camera_clips_v2”, extra_data: Dict = {})  | dict  | Build Reels music configure fields for manual `clip_upload(..., extra_data=...)`  |  
| clip_upload_with_music(path: Path, caption: str, track: Track or dict, thumbnail: Path = None, product: MUSIC_PRODUCT = “story_camera_clips_v2”, extra_data: Dict = {})  | Media  | Upload a Reel with music metadata without local audio muxing  |  
| clip_upload_as_reel_with_music(path: Path, caption: str, track: Track, extra_data: Dict = {})  | Media  | Upload a Reel after locally muxing the track into the video with MoviePy  |  
| photo_upload_with_music(path: Path, caption: str, track: Track or dict, extra_data: Dict = {}, schedule_at: int | datetime = None)  | Media  | Upload feed photo with music metadata  |  
| album_upload_with_music(paths: List[Path], caption: str, track: Track or dict, extra_data: Dict = {}, schedule_at: int | datetime = None)  | Media  | Upload feed album/carousel with music metadata  |  
For video uploads in Android environments, pass `thumbnail=...` to avoid automatic thumbnail generation, or install the optional video dependencies, MoviePy `2.2.1`, and executable ffmpeg. See [Pydroid and ffmpeg](https://subzeroid.github.io/instagrapi/usage-guide/pydroid.html) and [Termux](https://subzeroid.github.io/instagrapi/usage-guide/termux.html).
Scheduled publishing is available only where the Instagram app enables scheduled content, typically professional creator/business accounts. `schedule_at` works for feed photo, feed video, and album/carousel uploads. Reels, IGTV, Story, Direct, and cutout sticker upload helpers do not use this scheduled publishing flow.
In `extra_data`, you can pass additional media settings, for example:  
| Method  | Type  | Description  |  
| --- | --- | --- |  
| custom_accessibility_caption  | String  |  [Set alternative text](https://github.com/subzeroid/instagrapi/issues/351) `{"custom_accessibility_caption": "ALT TEXT HERE"}`  |  
| like_and_view_counts_disabled  | Int  |  [Disable like and view counts](https://github.com/subzeroid/instagrapi/issues/382) `{"like_and_view_counts_disabled": 1}`  |  
| disable_comments  | Int  | Disable comments `{"disable_comments": 1}`  |  
| invite_coauthor_user_ids  | List  | Low-level coauthor invite field. Prefer `coauthor_user_ids=[...]` on `photo_upload`, `video_upload`, or `album_upload`  |  
Trial Reels are available only for accounts where Instagram has enabled the feature. Use `clip_trial_eligible()` as a lightweight preflight if you process multiple accounts and want to avoid uploading video bytes for accounts where the Reel composer does not report Trial Reels enabled. Instagram can still reject Trial Reel publishing later during configure, so keep upload-side error handling for backend eligibility decisions. When `trial=True`, `clip_upload` sends `trial_params={"graduation_strategy": "manual"}` by default and disables feed preview for the upload.
For regular Reels, pass `show_preview_in_feed=False` to hide the Reel preview from the feed/profile grid. instagrapi sends this as Instagram’s low-level `clips_share_preview_to_feed` value `"0"`; the default `True` sends `"1"`. The legacy `feed_show` argument is still accepted as a raw override for callers that already build wire-format payloads.
Reel topics use Instagram’s interest topic `fit_id` values. Call `clip_interest_topics()` to get the current catalog, then pass selected ids with `clip_upload(..., topics=[topic["fit_id"]])`; instagrapi sends them as the Android `interest_topics` configure field.
Facebook Reel sharing requires a Facebook account/page linked in the Instagram app. Modern Android app builds no longer use only `{"share_to_facebook": 1}` for Reels; they also send destination and cross-posting fields such as `share_to_fb_destination_id`, `share_to_fb_destination_type`, `no_token_crosspost`, and `attempt_id`.
`clip_share_to_fb_config()` calls the lightweight Reel sharing preflight endpoint. On recent app versions this response contains availability flags, not the full Account Center destination state, and some linked accounts can still return `share_to_fb_unavailable=True` even when the Instagram app can cross-post manually. When `clip_upload(..., share_to_facebook=True)` has no manual destination override, instagrapi now falls back to Android’s `CrosspostingUnifiedConfigsQuery` via `clip_share_to_fb_unified_config()` and uses `clip_share_to_fb_unified_destination()` only if that response contains confirmed Reel-to-Facebook destination fields. Use `clip_share_to_fb_destination()` when a config or captured app response already contains confirmed destination fields; it normalizes `destination_id`, `destination_type`, optional audience, and validation bypass values. For accounts where the app can cross-post manually but automatic discovery still has no destination, pass `fb_destination_id` and `fb_destination_type="USER"` or `"PAGE"` to `clip_upload(...)`, or build `extra_data` manually with `clip_share_to_fb_extra_data(...)`. The destination type is typed as `Literal["USER", "PAGE"]`, and those uppercase values are what the Reel configure payload sends to Instagram. If neither the preflight/unified config data nor the caller provides a destination, instagrapi raises `ClientError` before uploading video bytes. The Reel cross-post `attempt_id` is generated automatically; only pass it to `clip_share_to_fb_extra_data(...)` when replaying or testing a specific low-level payload. `bloks_fxcal_link_reels_share()` exposes the raw Account Center Bloks link action seen on the Reel composer surface, but it starts an app linking flow and does not replace the interactive Facebook linking step in Instagram. Treat Account Center Bloks `fbid`, auth, and linking values as linking context, not as `fb_destination_id`; only use them as a Reel publish destination after verifying that the final Reel configure request sends the same value as `share_to_fb_destination_id`. See [#2556](https://github.com/subzeroid/instagrapi/issues/2556) for tracking automatic destination discovery.
### Example:

```
>>> import time
>>> from pathlib import Path
>>> from instagrapi import Client

>>> cl = Client()
>>> cl.login(USERNAME, PASSWORD)

>>> scheduled_photo = cl.photo_upload(
...     "/app/image.jpg",
...     "Scheduled photo",
...     schedule_at=int(time.time()) + 3600,
... )

>>> if cl.clip_trial_eligible():
...     trial_reel = cl.clip_upload(
...         "/app/reel.mp4",
...         "Trying a new Reel format",
...         trial=True,
...     )

>>> topics = cl.clip_interest_topics()
>>> technology_topic = next(topic for topic in topics if topic["name"] == "Technology")
>>> reel = cl.clip_upload(
...     "/app/reel.mp4",
...     "Reel with a topic",
...     topics=[technology_topic["fit_id"]],
... )

>>> reel = cl.clip_upload(
...     "/app/reel.mp4",
...     "Cross-posting this Reel to Facebook",
...     share_to_facebook=True,
... )

>>> reel = cl.clip_upload(
...     "/app/reel.mp4",
...     "Cross-posting with explicit Facebook destination",
...     share_to_facebook=True,
...     fb_destination_id="FACEBOOK_DESTINATION_ID",
...     fb_destination_type="USER",
... )

>>> fb_extra = cl.clip_share_to_fb_extra_data(
...     destination_id="FACEBOOK_DESTINATION_ID",
...     destination_type="USER",
... )
>>> reel = cl.clip_upload(
...     "/app/reel.mp4",
...     "Cross-posting with explicit Facebook destination",
...     extra_data=fb_extra,
... )

>>> reel = cl.clip_upload(
...     "/app/reel.mp4",
...     "Reel with an updated cover",
...     thumbnail=Path("/app/cover-a.jpg"),
... )
>>> cl.clip_change_cover(reel.pk, Path("/app/cover-b.jpg"))

>>> media = cl.photo_upload(
    "/app/image.jpg",
    "Test caption for photo with #hashtags and mention users such @example",
    extra_data={
        "custom_accessibility_caption": "alt text example",
        "like_and_view_counts_disabled": 1,
        "disable_comments": 1,
    }
)

>>> media.dict()
{'pk': 2573347427873726764,
 'id': '2573347427873726764_1903424587',
 'code': 'CO2Xdn6FCEs',
 'taken_at': datetime.datetime(2021, 5, 14, 10, 9, tzinfo=datetime.timezone.utc),
 'media_type': 1,
 'product_type': 'feed',
 'thumbnail_url': HttpUrl('https://instagram.fhel5-1.fna.fbcdn.net/v/t51.2885-15/e35/185486538_463522984736407_6315244509641560230_n.jpg?se=8&tp=1&_nc_ht=instagram.fhel5-1.fna.fbcdn.net&_nc_cat=107&_nc_ohc=6tBMsh9HlmMAX9zI_jc&edm=ACqnv0EBAAAA&ccb=7-4&oh=2b46f1e9fbd2416eb7d08b398e0f639e&oe=60C30437&_nc_sid=9ec724&ig_cache_key=MjU3MzM0NzQyNzg3MzcyNjc2NA%3D%3D.2-ccb7-4', scheme='https', host='instagram.fhel5-1.fna.fbcdn.net', tld='net', host_type='domain', path='/v/t51.2885-15/e35/185486538_463522984736407_6315244509641560230_n.jpg', query='se=8&tp=1&_nc_ht=instagram.fhel5-1.fna.fbcdn.net&_nc_cat=107&_nc_ohc=6tBMsh9HlmMAX9zI_jc&edm=ACqnv0EBAAAA&ccb=7-4&oh=2b46f1e9fbd2416eb7d08b398e0f639e&oe=60C30437&_nc_sid=9ec724&ig_cache_key=MjU3MzM0NzQyNzg3MzcyNjc2NA%3D%3D.2-ccb7-4'),
 'location': None,
 'user': {'pk': 1903424587,
  'username': 'example',
  'full_name': 'Example Example',
  'profile_pic_url': HttpUrl('https://instagram.fhel5-1.fna.fbcdn.net/v/t51.2885-19/s150x150/156689363_269505058076642_6448820957073669709_n.jpg?tp=1&_nc_ht=instagram.fhel5-1.fna.fbcdn.net&_nc_ohc=EtzrL0pAdg8AX-Xq8yS&edm=ACqnv0EBAAAA&ccb=7-4&oh=e2fd6a9d362f8587ea8123f23b248f1b&oe=60C2CB91&_nc_sid=9ec724', scheme='https', host='instagram.fhel5-1.fna.fbcdn.net', tld='net', host_type='domain', path='/v/t51.2885-19/s150x150/156689363_269505058076642_6448820957073669709_n.jpg', query='tp=1&_nc_ht=instagram.fhel5-1.fna.fbcdn.net&_nc_ohc=EtzrL0pAdg8AX-Xq8yS&edm=ACqnv0EBAAAA&ccb=7-4&oh=e2fd6a9d362f8587ea8123f23b248f1b&oe=60C2CB91&_nc_sid=9ec724'),
  'stories': []},
 'comment_count': 0,
 'like_count': 0,
 'has_liked': None,
 'caption_text': 'Test caption for photo with #hashtags and mention users such @example',
 'usertags': [],
 'video_url': None,
 'view_count': 0,
 'video_duration': 0.0,
 'title': '',
 'resources': []}

```

Upload a photo or carousel with feed music:

```
>>> music = cl.music_in_feed_audio_browser()
>>> track = music["items"][0]["playlist"]["preview_items"][0]["track"]

>>> photo = cl.photo_upload_with_music(
    "/app/image.jpg",
    "Photo with music",
    track,
    alacorn_session_id=music["alacorn_session_id"],
)

>>> album = cl.album_upload_with_music(
    ["/app/image.jpg", "/app/image2.jpg"],
    "Carousel with music",
    track,
    alacorn_session_id=music["alacorn_session_id"],
)

```

Now let’s mention users (Usertag) and location:

```
>>> from instagrapi import Client
>>> from instagrapi.types import Usertag, Location

>>> cl = Client()
>>> cl.login(USERNAME, PASSWORD)

>>> example = cl.user_info_by_username('example')
>>> media = cl.photo_upload(
    "/app/image.jpg",
    "Test caption for photo with #hashtags and mention users such @example",
    usertags=[Usertag(user=example, x=0.5, y=0.5)],
    location=Location(name='Russia, Saint-Petersburg', lat=59.96, lng=30.29)
)

>>> other = cl.user_info_by_username('other')
>>> album = cl.album_upload(
    ["/app/image.jpg", "/app/image2.jpg"],
    "Album with per-slide tags",
    usertags=[
        [Usertag(user=example, x=0.5, y=0.5)],
        [Usertag(user=other, x=0.25, y=0.75)],
    ],
)

>>> media.dict()
{'pk': 2573355619819242434,
 'id': '2573355619819242434_1903424587',
 'code': 'CO2ZU1QFMPC',
 'taken_at': datetime.datetime(2021, 5, 14, 10, 25, 16, tzinfo=datetime.timezone.utc),
 'media_type': 1,
 'product_type': 'feed',
 'thumbnail_url': HttpUrl('https://instagram.fhel5-1.fna.fbcdn.net/v/t51.2885-15/e35/185426950_474602463640866_4228057388625412955_n.jpg?se=8&tp=1&_nc_ht=instagram.fhel5-1.fna.fbcdn.net&_nc_cat=106&_nc_ohc=7NrVvAEG7f4AX_XPaOK&edm=ACqnv0EBAAAA&ccb=7-4&oh=bd2c90c2dcb693184e07c2777e09bb0b&oe=60C4E326&_nc_sid=9ec724&ig_cache_key=MjU3MzM1NTYxOTgxOTI0MjQzNA%3D%3D.2-ccb7-4', scheme='https', host='instagram.fhel5-1.fna.fbcdn.net', tld='net', host_type='domain', path='/v/t51.2885-15/e35/185426950_474602463640866_4228057388625412955_n.jpg', query='se=8&tp=1&_nc_ht=instagram.fhel5-1.fna.fbcdn.net&_nc_cat=106&_nc_ohc=7NrVvAEG7f4AX_XPaOK&edm=ACqnv0EBAAAA&ccb=7-4&oh=bd2c90c2dcb693184e07c2777e09bb0b&oe=60C4E326&_nc_sid=9ec724&ig_cache_key=MjU3MzM1NTYxOTgxOTI0MjQzNA%3D%3D.2-ccb7-4'),
 'location': {'pk': 107617247320879,
  'name': 'Russia, Saint-Petersburg',
  'address': 'Russia, Saint-Petersburg',
  'lng': 30.30605,
  'lat': 59.93318,
  'external_id': 107617247320879,
  'external_id_source': 'facebook_places'},
 'user': {'pk': 1903424587,
  'username': 'example',
  'full_name': 'Example Example',
  'profile_pic_url': HttpUrl('https://instagram.fhel5-1.fna.fbcdn.net/v/t51.2885-19/s150x150/156689363_269505058076642_6448820957073669709_n.jpg?tp=1&_nc_ht=instagram.fhel5-1.fna.fbcdn.net&_nc_ohc=EtzrL0pAdg8AX-Xq8yS&edm=ACqnv0EBAAAA&ccb=7-4&oh=e2fd6a9d362f8587ea8123f23b248f1b&oe=60C2CB91&_nc_sid=9ec724', scheme='https', host='instagram.fhel5-1.fna.fbcdn.net', tld='net', host_type='domain', path='/v/t51.2885-19/s150x150/156689363_269505058076642_6448820957073669709_n.jpg', query='tp=1&_nc_ht=instagram.fhel5-1.fna.fbcdn.net&_nc_ohc=EtzrL0pAdg8AX-Xq8yS&edm=ACqnv0EBAAAA&ccb=7-4&oh=e2fd6a9d362f8587ea8123f23b248f1b&oe=60C2CB91&_nc_sid=9ec724'),
  'stories': []},
 'comment_count': 0,
 'like_count': 0,
 'has_liked': None,
 'caption_text': 'Test caption for photo with #hashtags and mention users such @example',
 'usertags': [{'user': {'pk': 1903424587,
    'username': 'example',
    'full_name': 'Example Example',
    'profile_pic_url': HttpUrl('https://instagram.fhel5-1.fna.fbcdn.net/v/t51.2885-19/s150x150/156689363_269505058076642_6448820957073669709_n.jpg?tp=1&_nc_ht=instagram.fhel5-1.fna.fbcdn.net&_nc_ohc=EtzrL0pAdg8AX-Xq8yS&edm=ACqnv0EBAAAA&ccb=7-4&oh=e2fd6a9d362f8587ea8123f23b248f1b&oe=60C2CB91&_nc_sid=9ec724', scheme='https', host='instagram.fhel5-1.fna.fbcdn.net', tld='net', host_type='domain', path='/v/t51.2885-19/s150x150/156689363_269505058076642_6448820957073669709_n.jpg', query='tp=1&_nc_ht=instagram.fhel5-1.fna.fbcdn.net&_nc_ohc=EtzrL0pAdg8AX-Xq8yS&edm=ACqnv0EBAAAA&ccb=7-4&oh=e2fd6a9d362f8587ea8123f23b248f1b&oe=60C2CB91&_nc_sid=9ec724'),
    'stories': []},
   'x': 0.5,
   'y': 0.5}],
 'video_url': None,
 'view_count': 0,
 'video_duration': 0.0,
 'title': '',
 'resources': []}

```

For `album_upload`, nested `usertags` are matched by index with `paths`: `usertags[0]` applies to `paths[0]`, `usertags[1]` applies to `paths[1]`, and so on. A flat `List[Usertag]` is still accepted for backward compatibility and tags only the first carousel item.
When reading an album, the same index rule applies to resources: tags for the first carousel item are in `media.resources[0].usertags`, tags for the second item are in `media.resources[1].usertags`, etc.
Reels:
Timeline helpers:

```
>>> first_page = cl.get_timeline_feed("cold_start_fetch")
>>> second_page = cl.get_timeline_feed(max_id=first_page["next_max_id"])
>>> cl.reels(amount=10)
>>> cl.explore_reels(amount=10)
>>> cl.friends_reels(amount=10)

```

`get_timeline_feed()` remembers media ids from the previous response and sends `seen_posts` plus minimal `feed_view_info` when `max_id` is used. For stateless pagination, pass `seen_posts=...` and `feed_view_info=...` explicitly.

```
>>> clips = cl.user_clips_v1(25025320, amount=2)
>>> clips[0].dict()

{'pk': '3052048407587698594',
 'id': '3052048407587698594_25025320',
 'code': 'CpbDdszj7ei',
 'taken_at': datetime.datetime(2023, 3, 5, 21, 50, 4, tzinfo=datetime.timezone.utc),
 'media_type': 2,
 'product_type': 'clips',
 'thumbnail_url': HttpUrl('https://scontent-den4-1.cdninstagram.com/v/t51.2885-15/333966975_152901010970043_8971338145148712917_n.jpg?stp=dst-jpg_e15_p150x150&_nc_ht=scontent-den4-1.cdninstagram.com&_nc_cat=1&_nc_ohc=rRuJ7u4YrqEAX-UEMFq&edm=ACHbZRIBAAAA&ccb=7-5&ig_cache_key=MzA1MjA0ODQwNzU4NzY5ODU5NA%3D%3D.2-ccb7-5&oh=00_AfC_tNEWVjJLM5RQYUiQJFHQZSmvnDtAcpzs42DRSYt1pQ&oe=6409C451&_nc_sid=4a9e64', scheme='https', host='scontent-den4-1.cdninstagram.com', tld='com', host_type='domain', port='443', path='/v/t51.2885-15/333966975_152901010970043_8971338145148712917_n.jpg', query='stp=dst-jpg_e15_p150x150&_nc_ht=scontent-den4-1.cdninstagram.com&_nc_cat=1&_nc_ohc=rRuJ7u4YrqEAX-UEMFq&edm=ACHbZRIBAAAA&ccb=7-5&ig_cache_key=MzA1MjA0ODQwNzU4NzY5ODU5NA%3D%3D.2-ccb7-5&oh=00_AfC_tNEWVjJLM5RQYUiQJFHQZSmvnDtAcpzs42DRSYt1pQ&oe=6409C451&_nc_sid=4a9e64'),
 'location': {'pk': 213011753,
  'name': 'Sydney, Australia',
  'phone': '',
  'website': '',
  'category': '',
  'hours': {},
  'address': '',
  'city': '',
  'zip': None,
  'lng': 151.20797,
  'lat': -33.86751,
  'external_id': 110884905606108,
  'external_id_source': 'facebook_places'},
....
}

```

## Cutout Stickers
Create cutout stickers from photos for use in Direct Messages.  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| photo_upload_to_cutout_sticker(path: Path, bypass_ai: bool = True)  | Media  | Upload photo and create a Cutout Sticker  |  
| media_configure_to_cutout_sticker(upload_id: str, source_type: str, manual_box: List[float], use_ai_detection: bool, extra_data: Dict)  | Media  | Configure an uploaded photo as a Cutout Sticker (low-level)  |  
### Parameters
  * `bypass_ai` - If `True` (default), selects the full image using manual bounding box `[0, 0, 1, 1]`. Best for pre-processed images like transparent PNGs. If `False`, uses Instagram’s server-side AI (SAM) to detect and extract the subject.


### Example:

```
from instagrapi import Client

cl = Client()
cl.login(USERNAME, PASSWORD)

# Upload a pre-cut PNG sticker (bypass AI detection)
media = cl.photo_upload_to_cutout_sticker("sticker.png", bypass_ai=True)
print(media.dict())

# Upload a photo and let Instagram AI detect the subject
media = cl.photo_upload_to_cutout_sticker("photo.jpg", bypass_ai=False)
print(media.dict())

```



---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/account.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Account
Viewing and managing your profile  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| account_info()  | Account  | Get private info for the current account (email, phone number, birthday, biography, etc.)  |  
| account_edit(**data)  | Account  | Update profile fields such as `username`, `full_name`, `biography`, `external_url`, `phone_number`, and `email`  |  
| account_set_biography(biography: str)  | bool  | Update biography text, including entity-aware markup handling  |  
| account_change_picture(path: Path)  | UserShort  | Change profile picture  |  
| account_set_private()  | bool  | Switch account to private mode  |  
| account_set_public()  | bool  | Switch account to public mode  |  
| account_convert_to_business(category_id: str | int = “2347428775505624”, should_show_category: bool = True, should_show_public_contacts: bool = False)  | Account  | Convert the current account to a business professional account  |  
| account_convert_to_creator(category_id: str | int = “2347428775505624”, should_show_category: bool = True, should_show_public_contacts: bool = False)  | Account  | Convert the current account to a creator professional account  |  
| account_convert_to_professional(to_account_type: Literal[2, 3] = 3, category_id: str | int = “2347428775505624”, should_show_category: bool = True, should_show_public_contacts: bool = False)  | Account  | Generic professional account conversion helper; `2` is business and `3` is creator  |  
| account_security_info()  | dict  | Return account security settings, backup codes, trusted devices, and 2FA state  |  
| set_external_url(external_url: str)  | dict  | Replace bio links with a single external URL  |  
| remove_bio_links(link_ids: List[int])  | dict  | Remove one or more bio links by link ID  |  
| send_password_reset(identifier: str, recaptcha_challenge_field: str = “”)  | dict  | Send an Instagram password reset link or code to the account email or phone  |  
| reset_password(username: str)  | dict  | Backward-compatible alias for `send_password_reset()`  |  
| change_password(old_password: str, new_password: str)  | bool  | Change account password  |  
| send_confirm_email(email: str)  | dict  | Send a confirmation code to a new email address  |  
| confirm_email(email: str, code: str)  | dict  | Confirm a new email address with the received code  |  
| send_confirm_phone_number(phone_number: str)  | dict  | Send a confirmation code to a new phone number  |  
| confirm_phone_number(phone_number: str, code: str, has_sms_consent: bool = False)  | dict  | Confirm a new phone number with the received SMS code  |  
Example:

```
>>> from instagrapi import Client
>>> cl = Client()
>>> cl.login(USERNAME, PASSWORD)
>>> cl.account_info().dict()
{'pk': 1903424587,
 'username': 'example',
 'full_name': 'Example Example',
 'is_private': False,
 'profile_pic_url': HttpUrl('https://instagram.frix7-1.fna.fbcdn.net/v/t51.2885-19/s150x150/200092102_504535360754500_904902738723095864_n.jpg?tp=1&_nc_ht=instagram.frix7-1.fna.fbcdn.net&_nc_ohc=T2ZT6yA6XzoAX9MvAQA&edm=AJlpnE4BAAAA&ccb=7-4&oh=3865b51bb33b365c9de8bcf9775e519c&oe=60E982F2&_nc_sid=312772'),
 'is_verified': False,
 'biography': 'Engineer: Python, JavaScript, Erlang, Go, Swift\n@dhbastards \n@bestskatetrick \n@asphalt_kings_lb \n@best_drift_daily \n@wrclive \n@surferyone \n@bmxtravel',
 'external_url': 'https://example.org/',
 'is_business': False,
 'birthday': '1984-01-01',
 'phone_number': '+79991234567',
 'gender': 1,
 'email': '...@gmail.com'}

>>> cl.account_edit(external_url='https://github.com/subzeroid/instagrapi')
Account(pk=1903424587, username='example', ..., external_url='https://github.com/subzeroid/instagrapi')

>>> cl.account_set_biography("Python, APIs, and automation")
True

>>> cl.account_convert_to_creator(category_id="2347428775505624")
Account(pk=1903424587, username='example', ..., account_type=3)

>>> media_pk = cl.media_pk_from_url('https://www.instagram.com/p/BWnh360Fitr/')
1560364774164147051

>>> profile_pic_path = cl.photo_download(media_pk, folder='/tmp')
PosixPath('/tmp/example_1560364774164147051.jpg')

>>> cl.account_change_picture(profile_pic_path)
UserShort(pk=1903424587, username='example', ...)

>>> cl.send_confirm_email("addr@example.com")
{
    'is_email_legit': False,
    'title': 'Email Already in Use',
    'body': 'The email address you entered is already used on your account. Enter a different one to update your contact info.',
    'error_type': 'email_unchanged',
    'status': 'ok'
}

>>> cl.confirm_email("addr@example.com", "123456")
{'status': 'ok'}

>>> cl.send_confirm_phone_number("+5599999999")
{
    'action': 'sms_sent',
    'phone_verification_settings': {'max_sms_count': 2,
    'resend_sms_delay_sec': 60,
    'robocall_count_down_time_sec': 30,
    'robocall_after_max_sms': True},
    'status': 'ok'
}

>>> cl.confirm_phone_number("+5599999999", "123456")
{'status': 'ok'}

```

Notes:
  * `account_edit(**data)` only applies supported fields and preserves missing required profile fields from `account_info()`.
  * Use `account_set_biography()` when you want Instagram to re-process biography entities/markup explicitly.
  * Professional conversion uses Instagram’s mobile conversion flow and may still be blocked by account-specific eligibility, category, contact, or Account Center requirements.
  * `account_convert_to_business()` sends `to_account_type=2`; `account_convert_to_creator()` sends `to_account_type=3`. The generic helper exposes this as `ProfessionalAccountType = Literal[2, 3]`.
  * `send_password_reset()` starts Instagram’s recovery flow by requesting a reset link or code. It does not set a new password by itself; continue with the link/code flow that Instagram sends to the account email or phone.
  * `account_security_info()` and `insights_*` style methods require an authenticated session and may depend on the account type or enabled security features.


Low level methods:  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| news_inbox_v1(mark_as_seen: bool = False)  | dict  | Get raw “Active recently” / inbox activity payload  |  
Example:

```
>>> cl.news_inbox_v1()
{'story_mentions': {'mentions_count_string': '0 stories mention you.',
  'reels': [],
  'product_stories_count': '0 stories mention your product.',
  'product_stories_reels': []},
 'counts': {'likes': 0,
  'activity_feed_dot_badge': 0,
  'relationships': 0,
  'new_posts': 0,
  'comments': 0,
  'comment_likes': 0,
  'shopping_notification': 0,
  'fundraiser': 0,
  'usertags': 0,
  'campaign_notification': 0,
  'photos_of_you': 0,
  'story_mentions': 0,
  'requests': 0},
 'last_checked': 1625468461.1633658,
 'friend_request_stories': [],
 'new_stories': [{'story_type': 159,
   'type': 13,
   'args': {'rich_text': 'An unrecognized XiaoMi MI 5s just logged in near Moscow, Russia, RU',
    'destination': 'login_activity',
    'icon_url': 'https://i.instagram.com/static/images/activity/info-1.5.png/3385260677b8.png',
    'should_icon_apply_filter': True,
    'icon_should_apply_filter': True,
    'extra': {'lat': 55.7522, 'long': 37.6156},
    'actions': ['hide'],
    'timestamp': 1625475888.805998,
    'tuuid': '0ceff44c-dd70-11eb-8080-808080808080',
    'clicked': False},
   'counts': {},
   'pk': 'xjQlWRMfNO+f739i2qZ1zf8HJTo='}],
 'old_stories': [{'type': 3,
   'story_type': 101,
   'args': {'links': [{'start': 24,
      'end': 33,
  ...
}

```



---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/user.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# User
View a list of a user’s medias, following and followers
  * `user_id` - Integer ID of user, example `1903424587`

  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| user_followers(user_id: str, amount: int = 0, order: Optional[FOLLOWERS_ORDER] = None)  | Dict[int, UserShort]  | Get dict of followers users (amount=0 - fetch all followers). Use `order="date_followed_latest"` or `order="date_followed_earliest"` for mobile follower sorting  |  
| user_following(user_id: str, amount: int = 0)  | Dict[int, UserShort]  | Get dict of following users (amount=0 - fetch all)  |  
| iter_user_followers_v1(user_id: str, amount: int = 0, page_size: int = 200, order: Optional[FOLLOWERS_ORDER] = None)  | Iterator[UserShort]  | Stream followers from the private/mobile API without building a full dict  |  
| iter_user_following_v1(user_id: str, amount: int = 0, page_size: int = 200)  | Iterator[UserShort]  | Stream following users from the private/mobile API without building a full dict  |  
| search_followers(user_id: str, query: str)  | List[UserShort]  | Search by followers  |  
| search_following(user_id: str, query: str)  | List[UserShort]  | Search by following  |  
| user_info(user_id: str)  | User  | Get user info  |  
| user_info_by_username(username: str)  | User  | Get user info by username  |  
| user_about_v1(user_id: str)  | About  | Get “About this account” info  |  
| user_guides_v1(user_id: int)  | List[Guide]  | Get user’s guides  |  
| user_follow(user_id: str)  | bool  | Follow user, or request to follow a private user  |  
| user_unfollow(user_id: str)  | bool  | Unfollow user  |  
| user_block(user_id: str, surface: UserBlockSurface = “profile”)  | bool  | Block a user from a profile or Direct thread surface  |  
| user_unblock(user_id: str, surface: UserBlockSurface = “profile”)  | bool  | Unblock a user from a profile or Direct thread surface  |  
| user_follow_requests(amount: int = 0)  | List[UserShort]  | Get pending incoming follow requests  |  
| user_follow_request_approve(user_id: str)  | bool  | Approve a pending incoming follow request  |  
| user_follow_request_decline(user_id: str)  | bool  | Decline a pending incoming follow request  |  
| user_follow_requests_approve(user_ids: List[str])  | Dict[str, bool]  | Approve pending incoming follow requests  |  
| user_follow_requests_decline(user_ids: List[str])  | Dict[str, bool]  | Decline pending incoming follow requests  |  
| user_id_from_username(username: str)  | int  | Get user_id by username  |  
| username_from_user_id(user_id: str)  | str  | Get username by user_id  |  
| user_remove_follower(user_id: str)  | bool  | Remove your follower  |  
| user_report(user_id: str, reason: USER_REPORT_REASON = “spam”)  | bool  | Report a user account. Currently supports the live-verified spam report flow  |  
| mute_posts_from_follow(user_id: str)  | bool  | Mute posts from following user  |  
| unmute_posts_from_follow(user_id: str)  | bool  | Unmute posts from following user  |  
| mute_stories_from_follow(user_id: str)  | bool  | Mute stories from following user  |  
| enable_posts_notifications(user_id: str)  | bool  | Enable post notifications of user  |  
| disable_posts_notifications(user_id: str)  | bool  | Disable post notifications of user  |  
| enable_videos_notifications(user_id: str)  | bool  | Enable videos notifications of user  |  
| disable_videos_notifications(user_id: str)  | bool  | Disable videos notifications of user  |  
| enable_reels_notifications(user_id: str)  | bool  | Enable reels notifications of user  |  
| disable_reels_notifications(user_id: str)  | bool  | Disable reels notifications of user  |  
| enable_stories_notifications(user_id: str)  | bool  | Enable stories notifications of user  |  
| disable_stories_notifications(user_id: str)  | bool  | Disable stories notifications of user  |  
| close_friend_add(user_id: str)  | bool  | Add to Close Friends List  |  
| close_friend_remove(user_id: str)  | bool  | Remove from Close Friends List  |  
| user_suggested_profiles(user_id: str, expand_suggestion: bool = False)  | dict  | Suggested profiles (“Suggested for you”) for a profile. Wraps `chaining` and, with `expand_suggestion=True`, returns the raw `fetch_suggestion_details` payload (`items` in current app responses)  |  
| address_book_link(contacts: List[AddressBookContact | dict], include: Sequence[str] | str = (“extra_display_name”, “thumbnails”))  | dict  | Upload/link address book contacts and return Instagram’s raw contact-based suggestions response  |  
| address_book_unlink()  | dict  | Disconnect the uploaded address book from the current account  |  
| chaining(user_id: str)  | dict  | Suggested users for a profile (`discover/chaining/`) — same surface as the app’s “Suggested for you” carousel  |  
| fetch_suggestion_details(user_id: str, chained_ids: str)  | dict  | Expanded social-context fields for chained suggestion ids (`discover/fetch_suggestion_details/`)  |  
| discover_recommended_accounts_for_category_v1(user_id: str)  | dict  | Business-category-similar accounts: extracts `category_id` from the target’s stream payload, then calls `discover/recommended_accounts_for_category/`  |  
| user_related_profiles_gql(user_id: str)  | List[UserShort]  | Related profiles via public GraphQL `edge_chaining` (legacy `query_hash`, gated by IG — prefer `chaining` for reliability)  |  
### Option types
Follower sort orders are exposed as `FOLLOWERS_ORDER = Literal["date_followed_latest", "date_followed_earliest"]`. Pass `None` to keep Instagram’s default follower order.
User block surfaces are exposed as `UserBlockSurface = Literal["profile", "direct_thread_info"]`.
User report reasons are exposed as `USER_REPORT_REASON = Literal["spam"]`.  
| Type  | Values  | Used by  |  
| --- | --- | --- |  
| `FOLLOWERS_ORDER`  |  `"date_followed_latest"`, `"date_followed_earliest"`  |  `user_followers(order=...)`, `user_followers_v1(order=...)`, `iter_user_followers_v1(order=...)`  |  
| `UserBlockSurface`  |  `"profile"`, `"direct_thread_info"`  |  `user_block(surface=...)`, `user_unblock(surface=...)`  |  
| `USER_REPORT_REASON`  | `"spam"`  | `user_report(reason=...)`  |  
Lookup helpers:  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| user_short_gql(user_id: str, use_cache: bool = True)  | UserShort  | Short user info with current GraphQL/web-profile fallback chain  |  
| username_from_user_id_gql(user_id: str)  | str  | Resolve username from user id using the same fallback chain  |  
Streamed profile fetch (raw payloads, app-side surface):  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| user_stream_by_id_v1(user_id: str)  | dict  | Streamed profile envelope by pk (`users/{user_id}/info_stream/`)  |  
| user_stream_by_username_v1(username: str)  | dict  | Streamed profile envelope by username (`users/{username}/usernameinfo_stream/`)  |  
| user_stream_by_id_flat(user_id: str)  | dict  | Same as `_v1` but `stream_rows[*].user` partials merged into a single dict  |  
| user_stream_by_username_flat(username: str)  | dict  | Same as `_v1` but `stream_rows[*].user` partials merged into a single dict  |  
| user_web_profile_info_v1(username: str)  | dict  |  `users/web_profile_info/?username=...` via the private host (logged-in session, bypasses public-side rate limiting)  |  
| feed_user_stream_item(item_id: str, is_pull_to_refresh: bool = False)  | dict  | Raw streamed feed payload for a user/profile grid item  |  
Low level methods:  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| user_followers_gql_chunk(user_id: str, max_amount: int = 0, end_cursor: str = None)  | Tuple[List[UserShort], str]  | Get user’s followers information by Public Graphql API and end_cursor  |  
| user_followers_gql(user_id: str, amount: int = 0)  | List[UserShort]  | Get user’s followers information by Public Graphql API  |  
| user_followers_v1_chunk(user_id: str, max_amount: int = 0, max_id: str = “”, order: Optional[FOLLOWERS_ORDER] = None)  | Tuple[List[UserShort], str]  | Get user’s followers information by Private Mobile API and max_id (cursor). Supports `date_followed_latest` and `date_followed_earliest`  |  
| user_followers_v1(user_id: str, amount: int = 0, order: Optional[FOLLOWERS_ORDER] = None)  | List[UserShort]  | Get user’s followers information by Private Mobile API. Supports `date_followed_latest` and `date_followed_earliest`  |  
| iter_user_followers_v1(user_id: str, amount: int = 0, page_size: int = 200, order: Optional[FOLLOWERS_ORDER] = None)  | Iterator[UserShort]  | Stream followers page by page through `user_followers_v1_chunk()`  |  
| user_followers_private_gql_chunk(user_id: str, max_amount: int = 0, max_id: str = None, rank_token: str = None, order: Optional[FOLLOWERS_ORDER] = None)  | Tuple[List[UserShort], str]  | Get user’s followers through the private mobile GraphQL `FollowersList` surface and max_id cursor  |  
| user_followers_private_gql(user_id: str, amount: int = 0, rank_token: str = None, order: Optional[FOLLOWERS_ORDER] = None)  | List[UserShort]  | Get user’s followers through the private mobile GraphQL `FollowersList` surface  |  
| user_following_v1(user_id: str, amount: int = 0)  | List[UserShort]  | Get user’s following users information by Private Mobile API  |  
| iter_user_following_v1(user_id: str, amount: int = 0, page_size: int = 200)  | Iterator[UserShort]  | Stream following users page by page through `user_following_v1_chunk()`  |  
| user_follow_requests_chunk(max_amount: int = 0, max_id: str = “”)  | Tuple[List[UserShort], str]  | Get pending incoming follow requests by Private Mobile API and max_id  |  
| user_following_gql(user_id: str, amount: int = 0)  | List[UserShort]  | Get user’s following information by Public Graphql API  |  
| search_followers_v1(user_id: str, query: str)  | List[UserShort]  | Search by followers by Private Mobile API  |  
| search_following_v1(user_id: str, query: str)  | List[UserShort]  | Search by following by Private Mobile API  |  
| user_info_v2_gql(user_id: str)  | User  | Profile lookup through current doc_id GraphQL  |  
| user_info_by_username_v2_gql(username: str)  | User  | Resolve username through doc_id search, then fetch profile  |  
| private_graphql_followers_list(user_id: str, rank_token: str, …, order: Optional[FOLLOWERS_ORDER] = None)  | dict  | Raw private mobile GraphQL followers list. Supports `date_followed_latest` and `date_followed_earliest`  |  
| private_graphql_following_list(user_id: str, rank_token: str, …, order: Optional[FOLLOWERS_ORDER] = None)  | dict  | Raw private mobile GraphQL following list. Supports mobile `order` when accepted by Instagram  |  
| private_graphql_clips_profile(target_user_id: str, …)  | dict  | Raw private mobile GraphQL profile Reels stream  |  
| private_graphql_inbox_tray_for_user(user_id: str, …)  | dict  | Raw private mobile GraphQL inbox tray query  |  
The batch follow request helpers call the single-user approve/decline endpoints for each `user_id`; they do not implement an auto-approval policy.
`user_follow()` returns `True` only when it sends a new follow action and Instagram reports either an immediate follow or a new outgoing follow request for a private account. It returns `False` when the current account already follows the target or already has a pending outgoing follow request. Use `user_friendship_v1()` when you need to distinguish `following` from `outgoing_request`.
`UserShort` objects returned from private GraphQL follow-list payloads preserve selected v2-only fields when Instagram sends them: `friendship_status`, `profile_pic_id`, `fbid_v2`, `interop_messaging_user_fbid`, `strong_id__`, and raw `account_badges`. The legacy `latest_reel_media` property is also populated from Instagram’s current `1llatest_reel_media` key.
`user_report(user_id, reason="spam")` follows Instagram’s current mobile FRX report flow for account spam reports and submits the report. `reason` uses `USER_REPORT_REASON` and currently supports `"spam"`. This is a real account action; use it only for accounts you actually intend to report. Unsupported reasons raise `ValueError` until their FRX tag paths are captured and tested.
Example:

```
>>> cl.user_followers(cl.user_id).keys()
dict_keys([5563084402, 43848984510, 1498977320, ...])

>>> cl.user_following(cl.user_id)
{
  8530498223: UserShort(
    pk=8530498223,
    username="something",
    full_name="Example description",
    profile_pic_url=HttpUrl(
      'https://instagram.frix7-1.fna.fbcdn.net/v/t5...9217617140_n.jpg',
      scheme='https',
      host='instagram.frix7-1.fna.fbcdn.net',
      ...
    ),
  ),
  49114585: UserShort(
    pk=49114585,
    username='gx1000',
    full_name='GX1000',
    profile_pic_url=HttpUrl(
      'https://scontent-hel3-1.cdninstagram.com/v/t51.2885-19/10388...jpg',
      scheme='https',
      host='scontent-hel3-1.cdninstagram.com',
      ...
    )
  ),
  ...
}

>>> cl.user_info_by_username('example').dict()
{'pk': 1903424587,
 'username': 'example',
 'full_name': 'Example Example',
 'is_private': False,
 'profile_pic_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t51.2885-19/s150x150/123884060_803537687159702_2508263208740189974_n.jpg?...', scheme='https', host='scontent-hel3-1.cdninstagram.com', tld='com', host_type='domain', ...'),
 'is_verified': False,
 'media_count': 102,
 'follower_count': 576,
 'following_count': 538,
 'biography': 'Engineer: Python, JavaScript, Erlang',
 'external_url': HttpUrl('https://example.org/', scheme='https', host='example.org', tld='com', host_type='domain', path='/'),
 'is_business': False}


```

Sorted followers:

```
latest_followers = cl.user_followers(cl.user_id, amount=50, order="date_followed_latest")
earliest_followers = cl.user_followers_v1(cl.user_id, amount=50, order="date_followed_earliest")

```

Streaming followers/following:

```
for follower in cl.iter_user_followers_v1(cl.user_id, amount=1000, page_size=100, order="date_followed_latest"):
    print(follower.pk, follower.username)

for user in cl.iter_user_following_v1(cl.user_id, amount=1000, page_size=100):
    print(user.pk, user.username)

```

Raw private GraphQL helpers expose the same mobile `order` variable for callers that need the `FollowersList`/`FollowingList` payload directly:

```
payload = cl.private_graphql_followers_list(cl.user_id, cl.rank_token, order="date_followed_latest")

```

Use `user_followers_private_gql()` when you want the current mobile GraphQL followers list parsed into `UserShort` objects:

```
followers = cl.user_followers_private_gql(cl.user_id, amount=50, order="date_followed_latest")

```

Example: We go around the list of our followers and unfollow from them:

```
from instagrapi import Client
cl = Client()
cl.login(USERNAME, PASSWORD)

followers = cl.user_followers(cl.user_id)
for user_id in followers.keys():
    cl.user_unfollow(user_id)

```

Example: Suggested profiles (“Suggested for you”) for a target user:

```
from instagrapi import Client
from instagrapi.exceptions import InvalidTargetUser

cl = Client()
cl.login(USERNAME, PASSWORD)

user_id = cl.user_id_from_username("example")
try:
    suggested = cl.user_suggested_profiles(user_id)
    # Expanded social-context fields (current app responses expose them under "items"):
    detailed = cl.user_suggested_profiles(user_id, expand_suggestion=True)
except InvalidTargetUser:
    # Instagram refuses chaining for locked-down / private targets
    suggested = {"users": []}

```

Tip:
  * `user_info()`, `user_info_by_username()`, `user_id_from_username()`, and `username_from_user_id()` use private/mobile lookup first when the client has authorization data or a saved `sessionid`, then fall back to public/web lookup. Without authorization, these high-level helpers keep the public/web-first behavior. Explicit `_gql` methods still call the public/web path directly.
  * `user_followers()` and `user_following()` use private/mobile lookup first when the client has authorization data or a saved `sessionid`, then fall back to public/web lookup. Without authorization, these high-level helpers keep the public/web-first behavior. Explicit `_gql` methods still call the public/web path directly.
  * Use `iter_user_followers_v1()` and `iter_user_following_v1()` when you need to process large follow lists incrementally instead of keeping the full result in memory.




---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/location.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Location (place)
Viewing location info and medias by location  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| location_search(lat: float, lng: float)  | List[Location]  | Search Location by GEO coordinates  |  
| location_search_name(name: str)  | List[Location]  | Search Location by name  |  
| location_search_pk(location_pk: int)  | Location  | Resolve a Location by exact pk using search results  |  
| location_complete(location: Location)  | Location  | Complete blank fields  |  
| location_build(location: Location)  | String  | Serialized JSON  |  
| location_info(location_pk: int)  | Location  | Return Location info (pk, name, address, lng, lat, external_id, external_id_source)  |  
| location_medias_top(location_pk: int, amount: int = 9)  | List[Media]  | Return Top posts by Location  |  
| location_medias_recent(location_pk: int, amount: int = 24)  | List[Media]  | Return Most recent posts by Location  |  
| fbsearch_places(query: str, lat: float = 40.74, lng: float = -73.94)  | List[Location]  | >Search places via Facebook Search (40.74/-73.94 - New York, default GEO)  |  
Example:

```
>>> from instagrapi import Client

>>> cl = Client()
>>> cl.login(USERNAME, PASSWORD)

>>> location = cl.location_search(59.96, 30.29)[0]
>>> location.dict()
{'pk': None,
 'name': 'Russia, Saint-Petersburg',
 'address': 'Russia, Saint-Petersburg',
 'lng': 30.30605,
 'lat': 59.93318,
 'external_id': 107617247320879,
 'external_id_source': 'facebook_places'}

>>> location = cl.location_complete(location)
>>> location.dict()
{'pk': 107617247320879,
 'name': 'Russia, Saint-Petersburg',
 'address': 'Russia, Saint-Petersburg',
 'lng': 30.30605,
 'lat': 59.93318,
 'external_id': 107617247320879,
 'external_id_source': 'facebook_places'}

>>> cl.location_build(location)
'{"name":"Russia, Saint-Petersburg","address":"Russia, Saint-Petersburg","lat":59.93318,"lng":30.30605,"external_source":"facebook_places","facebook_places_id":107617247320879}'

>>> places = cl.location_search_name("Times Square")
>>> places[0].dict()
{'pk': 6889842, 'name': 'Times Square', ...}

>>> cl.location_search_pk(places[0].pk).dict()
{'pk': 6889842, 'name': 'Times Square', ...}

>>> location = cl.location_info(107617247320879)
>>> location.dict()
{'pk': 107617247320879,
 'name': 'Russia, Saint-Petersburg',
 'address': '',
 'lng': 30.30605,
 'lat': 59.93318,
 'external_id': None,
 'external_id_source': None}

>>> medias = cl.location_medias_top(107617247320879, amount=2)
>>> medias[0].dict()
{'pk': 2574095228556148891,
 'id': '2574095228556148891_8227888596',
 'code': 'CO5BfjkHgCb',
 'taken_at': datetime.datetime(2021, 5, 15, 11, 6, 25, tzinfo=datetime.timezone.utc),
 'media_type': 2,
 'product_type': 'feed',
 'thumbnail_url': HttpUrl('https://instagram.fhel3-1.fna.fbcdn.net/v/t51.2885-15/e35/185874360_510656656615872_846247842213042525_n.jpg?tp=1&_nc_ht=instagram.fhel3-1.fna.fbcdn.net&_nc_cat=1&_nc_ohc=vUIk3PZPPrMAX_GGZ7n&edm=AP_V10EBAAAA&ccb=7-4&oh=e418e018b9fc07b7d6b78f0790ddb481&oe=60A24C1F&_nc_sid=4f375e', scheme='https', host='instagram.fhel3-1.fna.fbcdn.net', tld='net', host_type='domain', path='/v/t51.2885-15/e35/185874360_510656656615872_846247842213042525_n.jpg', query='tp=1&_nc_ht=instagram.fhel3-1.fna.fbcdn.net&_nc_cat=1&_nc_ohc=vUIk3PZPPrMAX_GGZ7n&edm=AP_V10EBAAAA&ccb=7-4&oh=e418e018b9fc07b7d6b78f0790ddb481&oe=60A24C1F&_nc_sid=4f375e'),
 'location': {'pk': 107617247320879,
  'name': 'Russia, Saint-Petersburg',
  'address': '',
  'lng': 30.30605,
  'lat': 59.93318,
  'external_id': 107617247320879,
  'external_id_source': 'facebook_places'},
 'user': {'pk': 8227888596,
  'username': 'mzefirov',
  'full_name': 'МИХАИЛ ЗЕФИРОВ🌶️🔥ПРО ОТНОШЕНИЯ',
  'profile_pic_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t51.2885-19/s150x150/54513886_664942437287042_6311410572676038656_n.jpg?tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_ohc=mOWHIYJXbMsAX8wXvzf&edm=AP_V10EBAAAA&ccb=7-4&oh=90fa78d26bbb2c577dbc27d012c7cf09&oe=60C6A82B&_nc_sid=4f375e', scheme='https', host='scontent-hel3-1.cdninstagram.com', tld='com', host_type='domain', path='/v/t51.2885-19/s150x150/54513886_664942437287042_6311410572676038656_n.jpg', query='tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_ohc=mOWHIYJXbMsAX8wXvzf&edm=AP_V10EBAAAA&ccb=7-4&oh=90fa78d26bbb2c577dbc27d012c7cf09&oe=60C6A82B&_nc_sid=4f375e'),
  'stories': []},
 'comment_count': 94,
 'like_count': 3995,
 'has_liked': None,
 'caption_text': 'Антонина Роббинс, или немного о мотивации.\n\nСтавь ❤️и делись в сторис... это мотивирует.',
 'usertags': [],
 'video_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t50.2886-16/185466467_1373704339669543_4721533329541547409_n.mp4?_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_cat=107&_nc_ohc=IdbMAqYCjngAX987nBb&edm=AP_V10EBAAAA&ccb=7-4&oe=60A1DADD&oh=7c69dc13e5344f7095a94eb717b1ee9e&_nc_sid=4f375e', scheme='https', host='scontent-hel3-1.cdninstagram.com', tld='com', host_type='domain', path='/v/t50.2886-16/185466467_1373704339669543_4721533329541547409_n.mp4', query='_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_cat=107&_nc_ohc=IdbMAqYCjngAX987nBb&edm=AP_V10EBAAAA&ccb=7-4&oe=60A1DADD&oh=7c69dc13e5344f7095a94eb717b1ee9e&_nc_sid=4f375e'),
 'view_count': 36295,
 'video_duration': 55.433,
 'title': '',
 'resources': []}

>>> medias = cl.location_medias_recent(107617247320879, amount=2)
>>> medias[0].dict()
{'pk': 2574187014843321420,
 'id': '2574187014843321420_5600296444',
 'code': 'CO5WXONKMxM',
 'taken_at': datetime.datetime(2021, 5, 15, 13, 57, 6, tzinfo=datetime.timezone.utc),
 'media_type': 1,
 'product_type': '',
 'thumbnail_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t51.2885-15/e35/p1080x1080/186279877_479327446453989_5642409805215171470_n.jpg?tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_cat=109&_nc_ohc=Nx9KwOGWXLYAX_bh1Dx&edm=AP_V10EBAAAA&ccb=7-4&oh=999395b5e4a3c688bcb388616f405161&oe=60C4C08C&_nc_sid=4f375e', scheme='https', host='scontent-hel3-1.cdninstagram.com', tld='com', host_type='domain', path='/v/t51.2885-15/e35/p1080x1080/186279877_479327446453989_5642409805215171470_n.jpg', query='tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_cat=109&_nc_ohc=Nx9KwOGWXLYAX_bh1Dx&edm=AP_V10EBAAAA&ccb=7-4&oh=999395b5e4a3c688bcb388616f405161&oe=60C4C08C&_nc_sid=4f375e'),
 'location': {'pk': 107617247320879,
  'name': 'Russia, Saint-Petersburg',
  'address': '',
  'lng': 30.30605,
  'lat': 59.93318,
  'external_id': 107617247320879,
  'external_id_source': 'facebook_places'},
 'user': {'pk': 5600296444,
  'username': 'sultanieriabinina',
  'full_name': 'Султание Беляловна',
  'profile_pic_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t51.2885-19/s150x150/92693550_492095081670507_2163230119093600256_n.jpg?tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_ohc=_8hEZtz-JSIAX_NCxXx&edm=AP_V10EBAAAA&ccb=7-4&oh=17d2d1a8ae00765b8471cde868937c13&oe=60C69D73&_nc_sid=4f375e', scheme='https', host='scontent-hel3-1.cdninstagram.com', tld='com', host_type='domain', path='/v/t51.2885-19/s150x150/92693550_492095081670507_2163230119093600256_n.jpg', query='tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_ohc=_8hEZtz-JSIAX_NCxXx&edm=AP_V10EBAAAA&ccb=7-4&oh=17d2d1a8ae00765b8471cde868937c13&oe=60C69D73&_nc_sid=4f375e'),
  'stories': []},
 'comment_count': 0,
 'like_count': 0,
 'has_liked': None,
 'caption_text': '',
 'usertags': [{'user': {'pk': 3955327494,
    'username': '_parikmakher_irishka3127',
    'full_name': 'ИрИнА',
    'profile_pic_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t51.2885-19/s150x150/176040256_461659781826794_5379061705031591554_n.jpg?tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_ohc=uVHqkpa8v0UAX-cmGUE&edm=AP_V10EBAAAA&ccb=7-4&oh=22db3640b911117484d78422eec4f778&oe=60C523D5&_nc_sid=4f375e', scheme='https', host='scontent-hel3-1.cdninstagram.com', tld='com', host_type='domain', path='/v/t51.2885-19/s150x150/176040256_461659781826794_5379061705031591554_n.jpg', query='tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_ohc=uVHqkpa8v0UAX-cmGUE&edm=AP_V10EBAAAA&ccb=7-4&oh=22db3640b911117484d78422eec4f778&oe=60C523D5&_nc_sid=4f375e'),
    'stories': []},
   'x': 0.352,
   'y': 0.292}],
 'video_url': None,
 'view_count': 0,
 'video_duration': 0.0,
 'title': '',
 'resources': []}


```

Facebook Search:

```
>>> place = cl.fbsearch_places('Perch')[2]
>>> place.dict()
{
 'pk': 3824034,
 'name': 'Perch',
 'phone': '',
 'website': '',
 'category': '',
 'hours': {},
 'address': None,
 'city': None,
 'zip': None,
 'lng': -118.25135,
 'lat': 34.04882,
 'external_id': 207298912632228,
 'external_id_source': 'facebook_places'
}

>>> cl.location_info(place.pk).dict()
{
 'pk': 3824034,
 'name': 'Perch',
 'phone': '(213) 802-1770',
 'website': 'http://www.perchla.com',
 'category': '',
 'hours': {},
 'address': '448 S Hill St',
 'city': 'Los Angeles, California',
 'zip': '90013',
 'lng': -118.25135,
 'lat': 34.04882,
 'external_id': None,
 'external_id_source': None
}

```


```
>>> place = cl.fbsearch_places("Villa Sirot", 46.7032028502, 4.3093986902)[0]
>>> place.dict()
{'pk': 1001956449,
 'name': 'Villa Sirot',
 'phone': '',
 'website': '',
 'category': '',
 'hours': {},
 'address': None,
 'city': None,
 'zip': None,
 'lng': 4.3093986902426,
 'lat': 46.703202850229,
 'external_id': 165573396905197,
 'external_id_source': 'facebook_places'}

>>> cl.location_info(place.pk).dict()
{'pk': 1001956449,
 'name': 'Villa Sirot',
 'phone': '',
 'website': None,
 'category': 'Local Business',
 'hours': {'status': '',
  'current_status': '',
  'hours_today': '',
  'schedule': []},
 'address': None,
 'city': None,
 'zip': None,
 'lng': None,
 'lat': None,
 'external_id': 165573396905197,
 'external_id_source': None}


```

Low level methods:  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| location_info_v1(location_pk: int)  | Location  | Get a location using location pk (Private Mobile API)  |  
| location_medias_v1_chunk(location_pk: int, max_amount: int = 63, tab_key: Literal[“ranked”, “recent”] = “ranked”, max_id: str = None)  | Tuple[List[Media], str] Get chunk of medias for a location and max_id (cursor) by Private Mobile API  |   |  
| location_medias_v1(location_pk: int, amount: int = 63, tab_key: Literal[“ranked”, “recent”] = “ranked”)  | List[Media]  | Get medias for a location (Private Mobile API), paginating with the server cursor until `amount` is reached or the cursor is exhausted  |  
| location_medias_top_v1(location_pk: int, amount: int = 21)  | List[Media]  | Get top medias for a location (Private Mobile API)  |  
| location_medias_recent_v1(location_pk: int, amount: int = 63)  | List[Media]  | Get recent medias for a location (Private Mobile API), paginating past the first chunk when the endpoint returns `next_max_id`  |


---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/hashtag.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Hashtag
Viewing hashtag info and medias by hashtag
Pass hashtag names without the leading `#`, for example `pizza`. If a leading `#` is provided, instagrapi strips it and emits a warning; an empty hashtag name raises `ValueError`.  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| hashtag_info(name: str)  | Hashtag  | Return hashtag info (`id`, `name`, `media_count`, `profile_pic_url`)  |  
| hashtag_medias_top(name: str, amount: int = 9)  | List[Media]  | Return top posts for a hashtag  |  
| hashtag_medias_recent(name: str, amount: int = 27)  | List[Media]  | Return recent posts for a hashtag  |  
| hashtag_medias_paginated(name: str, amount: int = 27, tab_key: str = “recent”, end_cursor: str = None)  | Tuple[List[Media], str]  | Return one hashtag media page plus the next cursor; authenticated sessions use private/mobile pagination first  |  
| iter_hashtag_medias(name: str, amount: int = 0, page_size: int = 27, tab_key: str = “recent”)  | Iterator[Media]  | Stream hashtag media page by page without building a full list  |  
| hashtag_medias_reels_v1(name: str, amount: int = 27)  | List[Media]  | Return reels/clips for a hashtag via private API  |  
| hashtag_follow(hashtag: str, unfollow: bool = False)  | bool  | Follow a hashtag  |  
| hashtag_following(amount: int = 0)  | List[Hashtag]  | Return hashtags followed by the authenticated account  |  
| hashtag_unfollow(hashtag: str)  | bool  | Unfollow a hashtag  |  
Example:

```
>>> from instagrapi import Client

>>> cl = Client()
>>> cl.login(USERNAME, PASSWORD)

>>> hashtag = cl.hashtag_info('downhill')
>>> hashtag.dict()
{'id': 17841563089103670,
 'name': 'downhill',
 'media_count': 5178255,
 'profile_pic_url': HttpUrl('https://instagram.fhel3-1.fna.fbcdn.net/v/t51.2885-15/e35/s150x150/184304495_294863488920457_8839934375675895594_n.jpg?tp=1&_nc_ht=instagram.fhel3-1.fna.fbcdn.net&_nc_cat=101&_nc_ohc=L3i9yzFUBR8AX_MAXgr&edm=ABZsPhsBAAAA&ccb=7-4&oh=21a944a197506a42658e8273d92740b7&oe=60C37E35&_nc_sid=4efc9f', scheme='https', host='instagram.fhel3-1.fna.fbcdn.net', tld='net', host_type='domain', path='/v/t51.2885-15/e35/s150x150/184304495_294863488920457_8839934375675895594_n.jpg', query='tp=1&_nc_ht=instagram.fhel3-1.fna.fbcdn.net&_nc_cat=101&_nc_ohc=L3i9yzFUBR8AX_MAXgr&edm=ABZsPhsBAAAA&ccb=7-4&oh=21a944a197506a42658e8273d92740b7&oe=60C37E35&_nc_sid=4efc9f')}

>>> medias = cl.hashtag_medias_top('downhill', amount=2)
>>> medias[0].dict()
{'pk': 2574092718364154697,
 'id': '2574092718364154697_376712420',
 'code': 'CO5A7BxA9tJ',
 'taken_at': datetime.datetime(2021, 5, 15, 10, 49, 45, tzinfo=datetime.timezone.utc),
 'media_type': 1,
 'product_type': '',
 'thumbnail_url': HttpUrl('https://instagram.fhel3-1.fna.fbcdn.net/v/t51.2885-15/e35/s1080x1080/186430270_473573763896149_2030909827389015824_n.jpg?tp=1&_nc_ht=instagram.fhel3-1.fna.fbcdn.net&_nc_cat=101&_nc_ohc=4jFHY_INCnMAX-7fObK&edm=AP_V10EBAAAA&ccb=7-4&oh=9fb0c4cdb01a7aa376a96c0df366d844&oe=60C4C01A&_nc_sid=4f375e', scheme='https', host='instagram.fhel3-1.fna.fbcdn.net', tld='net', host_type='domain', path='/v/t51.2885-15/e35/s1080x1080/186430270_473573763896149_2030909827389015824_n.jpg', query='tp=1&_nc_ht=instagram.fhel3-1.fna.fbcdn.net&_nc_cat=101&_nc_ohc=4jFHY_INCnMAX-7fObK&edm=AP_V10EBAAAA&ccb=7-4&oh=9fb0c4cdb01a7aa376a96c0df366d844&oe=60C4C01A&_nc_sid=4f375e'),
 'location': {'pk': 517543,
  'name': 'Sestola',
  'address': '',
  'lng': 10.77328,
  'lat': 44.2266,
  'external_id': 103150459725396,
  'external_id_source': 'facebook_places'},
 'user': {'pk': 376712420,
  'username': 'vascobica',
  'full_name': '⚡Vasco Bica®⚡',
  'profile_pic_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t51.2885-19/s150x150/96211403_922669918147090_5138958292701151232_n.jpg?tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_ohc=tYlGX8kDuSgAX9WtBRF&edm=AP_V10EBAAAA&ccb=7-4&oh=ac96c75846d17519e53923a0ddb3aad0&oe=60C51486&_nc_sid=4f375e', scheme='https', host='scontent-hel3-1.cdninstagram.com', tld='com', host_type='domain', path='/v/t51.2885-19/s150x150/96211403_922669918147090_5138958292701151232_n.jpg', query='tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_ohc=tYlGX8kDuSgAX9WtBRF&edm=AP_V10EBAAAA&ccb=7-4&oh=ac96c75846d17519e53923a0ddb3aad0&oe=60C51486&_nc_sid=4f375e'),
  'stories': []},
 'comment_count': 8,
 'like_count': 327,
 'has_liked': None,
 'caption_text': 'Ready to fight ⚔️\n#js7 \n.\n.\n#swissmountainsports #racing #coppaitaliadh \n#mirandabikeparts\xa0#burning\xa0#jumping \xa0#whipit\xa0#scrubit\xa0#enduro\xa0#mtblife\xa0 #downhill\xa0#mountainbiking\xa0#sliding\xa0#dirt\xa0#dh\xa0 #mtb\xa0#bike\xa0#bikelife\xa0#friends\xa0#mtbswitzerland\xa0#downhillmtb\xa0#valais\xa0 #swissmountains\xa0\xa0#italy #italydownhill',
 'usertags': [{'user': {'pk': 3636959873,
    'username': 'christopherstrm',
    'full_name': 'Christopher Ström',
    'profile_pic_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t51.2885-19/s150x150/173775865_527371595096868_8991176723035066304_n.jpg?tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_ohc=tbsAzTDoLtEAX_HaT9Z&edm=AP_V10EBAAAA&ccb=7-4&oh=94a18b3b4d0d39d9dbda849b4c23a5a9&oe=60C5192F&_nc_sid=4f375e', scheme='https', host='scontent-hel3-1.cdninstagram.com', tld='com', host_type='domain', path='/v/t51.2885-19/s150x150/173775865_527371595096868_8991176723035066304_n.jpg', query='tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_ohc=tbsAzTDoLtEAX_HaT9Z&edm=AP_V10EBAAAA&ccb=7-4&oh=94a18b3b4d0d39d9dbda849b4c23a5a9&oe=60C5192F&_nc_sid=4f375e'),
    'stories': []},
   'x': 0.211352657,
   'y': 0.8478260870000001}],
 'video_url': None,
 'view_count': 0,
 'video_duration': 0.0,
 'title': '',
 'resources': []}

>>> medias = cl.hashtag_medias_recent('downhill', amount=2)
>>> medias[0].dict()
{'pk': 2574205305714324167,
 'id': '2574205305714324167_2984719638',
 'code': 'CO5ahY6BzLH',
 'taken_at': datetime.datetime(2021, 5, 15, 14, 33, 27, tzinfo=datetime.timezone.utc),
 'media_type': 8,
 'product_type': '',
 'thumbnail_url': None,
 'location': {'pk': 703017966745848,
  'name': 'Le Canyon Du Diable',
  'address': '',
  'lng': 3.4480762482,
  'lat': 43.6966105493,
  'external_id': 703017966745848,
  'external_id_source': 'facebook_places'},
 'user': {'pk': 2984719638,
  'username': 'lilian.champion',
  'full_name': 'Lilian 🇨🇵',
  'profile_pic_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t51.2885-19/s150x150/169115203_291696755653751_6779914563403118432_n.jpg?tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_ohc=VEqYwd5W1FYAX_7ID-6&edm=AP_V10EBAAAA&ccb=7-4&oh=7fe193da2e706c0cafd9e1d432734891&oe=60C59786&_nc_sid=4f375e', scheme='https', host='scontent-hel3-1.cdninstagram.com', tld='com', host_type='domain', path='/v/t51.2885-19/s150x150/169115203_291696755653751_6779914563403118432_n.jpg', query='tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_ohc=VEqYwd5W1FYAX_7ID-6&edm=AP_V10EBAAAA&ccb=7-4&oh=7fe193da2e706c0cafd9e1d432734891&oe=60C59786&_nc_sid=4f375e'),
  'stories': []},
 'comment_count': 0,
 'like_count': 0,
 'has_liked': None,
 'caption_text': "Quand on te prend en photo sans que tu aies demandé et que la personne t'envoie tout par mail après...😂😁🤙🏻 Merci l'inconnu du coup \n\n#downhill #mountainlovers #ytowners #vanlife #vanlifefrance",
 'usertags': [],
 'video_url': None,
 'view_count': 0,
 'video_duration': 0.0,
 'title': '',
 'resources': [{'pk': 2574205301050111226,
   'video_url': None,
   'thumbnail_url': HttpUrl('https://instagram.fhel3-1.fna.fbcdn.net/v/t51.2885-15/e35/184312115_2977220092557985_8274386175388868273_n.jpg?tp=1&_nc_ht=instagram.fhel3-1.fna.fbcdn.net&_nc_cat=101&_nc_ohc=YoLLGA0cAhsAX8MxnSo&edm=AP_V10EBAAAA&ccb=7-4&oh=b0f2740aaff1d80c5f5219ffa267a186&oe=60C4273E&_nc_sid=4f375e', scheme='https', host='instagram.fhel3-1.fna.fbcdn.net', tld='net', host_type='domain', path='/v/t51.2885-15/e35/184312115_2977220092557985_8274386175388868273_n.jpg', query='tp=1&_nc_ht=instagram.fhel3-1.fna.fbcdn.net&_nc_cat=101&_nc_ohc=YoLLGA0cAhsAX8MxnSo&edm=AP_V10EBAAAA&ccb=7-4&oh=b0f2740aaff1d80c5f5219ffa267a186&oe=60C4273E&_nc_sid=4f375e'),
   'media_type': 1},
  {'pk': 2574205301083731874,
   'video_url': None,
   'thumbnail_url': HttpUrl('https://instagram.fhel6-1.fna.fbcdn.net/v/t51.2885-15/e35/186524178_143770224434390_4909324648747352588_n.jpg?tp=1&_nc_ht=instagram.fhel6-1.fna.fbcdn.net&_nc_cat=102&_nc_ohc=w6z9v4MwYg8AX9FdWk0&edm=AP_V10EBAAAA&ccb=7-4&oh=99295fa82472bf4a425fc49bd03c1310&oe=60C40AFC&_nc_sid=4f375e', scheme='https', host='instagram.fhel6-1.fna.fbcdn.net', tld='net', host_type='domain', path='/v/t51.2885-15/e35/186524178_143770224434390_4909324648747352588_n.jpg', query='tp=1&_nc_ht=instagram.fhel6-1.fna.fbcdn.net&_nc_cat=102&_nc_ohc=w6z9v4MwYg8AX9FdWk0&edm=AP_V10EBAAAA&ccb=7-4&oh=99295fa82472bf4a425fc49bd03c1310&oe=60C40AFC&_nc_sid=4f375e'),
   'media_type': 1},
  {'pk': 2574205301066842492,
   'video_url': None,
   'thumbnail_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t51.2885-15/e35/186787154_332065288355469_7843843424299639709_n.jpg?tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_cat=109&_nc_ohc=-qZy9_HakCQAX-Cqk9v&edm=AP_V10EBAAAA&ccb=7-4&oh=031077ab2f56db0bab7ffbc920f80a41&oe=60C4F57B&_nc_sid=4f375e', scheme='https', host='scontent-hel3-1.cdninstagram.com', tld='com', host_type='domain', path='/v/t51.2885-15/e35/186787154_332065288355469_7843843424299639709_n.jpg', query='tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_cat=109&_nc_ohc=-qZy9_HakCQAX-Cqk9v&edm=AP_V10EBAAAA&ccb=7-4&oh=031077ab2f56db0bab7ffbc920f80a41&oe=60C4F57B&_nc_sid=4f375e'),
   'media_type': 1},
  {'pk': 2574205301075310332,
   'video_url': None,
   'thumbnail_url': HttpUrl('https://instagram.fhel3-1.fna.fbcdn.net/v/t51.2885-15/e35/185727252_524026898594344_9165723485744355754_n.jpg?tp=1&_nc_ht=instagram.fhel3-1.fna.fbcdn.net&_nc_cat=104&_nc_ohc=45NguRpEtZQAX83VSGE&edm=AP_V10EBAAAA&ccb=7-4&oh=c8c087ecfba444d9d85f7bd059f42a2a&oe=60C5C3C2&_nc_sid=4f375e', scheme='https', host='instagram.fhel3-1.fna.fbcdn.net', tld='net', host_type='domain', path='/v/t51.2885-15/e35/185727252_524026898594344_9165723485744355754_n.jpg', query='tp=1&_nc_ht=instagram.fhel3-1.fna.fbcdn.net&_nc_cat=104&_nc_ohc=45NguRpEtZQAX83VSGE&edm=AP_V10EBAAAA&ccb=7-4&oh=c8c087ecfba444d9d85f7bd059f42a2a&oe=60C5C3C2&_nc_sid=4f375e'),
   'media_type': 1}]}

```

Stream hashtag media without storing every fetched page:

```
for media in cl.iter_hashtag_medias("downhill", amount=100, page_size=25, tab_key="recent"):
    print(media.pk, media.code)

```

Low level methods:  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| hashtag_info_gql(name: str, amount: int = 12, end_cursor: str = None)  | Hashtag  | Get information about a hashtag by Public Graphql API  |  
| hashtag_info_v1(name: str)  | Hashtag  | Get information about a hashtag by Private Mobile API  |  
| hashtag_medias_paginated_gql(name: str, amount: int = 27, end_cursor: str = None)  | Tuple[List[Media], str]  | Get one recent hashtag media page by Public GraphQL API  |  
| hashtag_medias_paginated_v1(name: str, amount: int = 27, tab_key: Literal[“top”, “recent”, “clips”] = “recent”, end_cursor: str = None)  | Tuple[List[Media], str]  | Get one hashtag media page by Private Mobile API  |  
| iter_hashtag_medias(name: str, amount: int = 0, page_size: int = 27, tab_key: str = “recent”)  | Iterator[Media]  | Stream hashtag medias page by page through `hashtag_medias_paginated()`  |  
| hashtag_medias_v1_chunk(name: str, max_amount: int = 27, tab_key: Literal[“top”, “recent”, “clips”] = “top”, max_id: str = None)  | Tuple[List[Media], str]  | Get chunk of medias for a hashtag and max_id (cursor) by Private Mobile API  |  
| hashtag_medias_v1(name: str, amount: int = 27, tab_key: Literal[“top”, “recent”, “clips”] = “top”)  | List[Media]  | Get medias for a hashtag by Private Mobile API  |  
| hashtag_medias_top_v1(name: str, amount: int = 9)  | List[Media]  | Get top medias for a hashtag by Private Mobile API  |  
| hashtag_medias_recent_v1(name: str, amount: int = 27)  | List[Media]  | Get recent medias for a hashtag by Private Mobile API  |  
| hashtag_medias_reels_v1(name: str, amount: int = 27)  | List[Media]  | Get recent clips (reels) for a hashtag by Private Mobile API  |  
Example for [Request for loading every next time new posts from hashtag](https://github.com/subzeroid/instagrapi/issues/79):

```
>>> medias, cursor = cl.hashtag_medias_paginated('test', amount=32, tab_key='recent')
>>> next_medias, cursor = cl.hashtag_medias_paginated('test', amount=32, tab_key='recent', end_cursor=cursor)

>>> medias, cursor = cl.hashtag_medias_v1_chunk('test', max_amount=32, tab_key='recent')
>>> len(medias)
32
>>> cursor
QVFDR0dzT3FJT0V4amFjMaQ3czlGVzRKV3FNWDJqaE1mWmltWU5VWGYtbnV6RVpoOUlsR3dCN05RRmpLc2R5SVlCQTNaekV5bUVOV0F4Vno1MDkxN1Nndg==

# NEXT cursor:

>>> medias, cursor = cl.hashtag_medias_v1_chunk('test', max_amount=32, tab_key='recent', max_id=cursor)
>>> len(medias)
32
>>> cursor
QVFEUXpfM0RtaDdmMExPQ0k0UWRlaHFJa2RVdVlaX01LTzhkNF9Dd1N2UlhtVy1vSTZvMERfYW5XN205OTBRNFBCSVJ2ZTVfTG5ZMXVmY0VJbUM5TU9URQ==

>>> cl.hashtag_follow("python")
True

>>> cl.hashtag_following(amount=1)
[Hashtag(id='17841562401125985', name='python', media_count=12000000, profile_pic_url=None)]

>>> cl.hashtag_unfollow("python")
True

```

Notes:
  * Instagram’s old public hashtag web page JSON (`?__a=1`) is no longer reliable and the `_a1` helpers were removed. Use the high-level hashtag methods or the authenticated private/mobile `_v1` helpers.
  * High-level `hashtag_info()`, `hashtag_medias_top()`, and `hashtag_medias_recent()` use the private/mobile helpers.
  * `hashtag_following()` returns the authenticated following-list hashtag preview. Instagram may limit how many followed hashtags are included.
  * For resumable pagination, prefer `hashtag_medias_paginated()` and persist the returned cursor. Use `hashtag_medias_v1_chunk()` only when you need the low-level private/mobile helper.
  * Use `iter_hashtag_medias()` when you want to process large hashtag result sets incrementally. It uses the same pagination path as `hashtag_medias_paginated()`.
  * `hashtag_medias_v1_chunk()` accepts `top`, `recent`, or `clips` as `tab_key`.




---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/collection.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Collections
Saved posts, collections, and liked media.  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| collections()  | List[Collection]  | Get all collections for the authenticated account  |  
| collection_pk_by_name(name: str)  | int  | Resolve collection ID by collection name  |  
| collection_medias_by_name(name: str)  | List[Media]  | Get medias in a collection by collection name  |  
| collection_medias(collection_pk: str, amount: int = 21, last_media_pk: int = 0)  | List[Media]  | Get medias in a collection; use `amount=0` to keep paginating  |  
| collection_medias_v1_chunk(collection_pk: str, max_id: str = “”)  | Tuple[List[Media], str]  | Low-level chunk fetch with raw `next_max_id` cursor  |  
| liked_medias(amount: int = 21, last_media_pk: int = 0)  | List[Media]  | Get media liked by the current account  |  
| media_save(media_id: str, collection_pk: int = None)  | bool  | Save media, optionally into a specific collection  |  
| media_unsave(media_id: str, collection_pk: int = None)  | bool  | Remove media from saved posts or from a specific collection  |  
Example:

```
from instagrapi import Client

cl = Client()
cl.login(USERNAME, PASSWORD)

collections = cl.collections()
print([(item.id, item.name) for item in collections])

liked = cl.liked_medias(amount=10)
saved = cl.collection_medias("liked", amount=10)

travel_pk = cl.collection_pk_by_name("Travel")
travel_medias = cl.collection_medias(travel_pk, amount=0)

media_id = cl.media_id(cl.media_pk_from_url("https://www.instagram.com/p/CP5h-I1FuPr/"))
cl.media_save(media_id, collection_pk=travel_pk)
cl.media_unsave(media_id, collection_pk=travel_pk)

```

Notes:
  * `collection_pk` can be a numeric collection ID, `"liked"`, or a saved-posts style collection path handled by `collection_medias_v1_chunk()`.
  * `liked_medias()` is a convenience wrapper over `collection_medias("liked", ...)`.
  * `last_media_pk` in `collection_medias()` is a resume point based on already seen media, not the raw server cursor.




---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/comment.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Comment
Post comment, viewing, like and unlike comments  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| media_comment(media_id: str, text: str, replied_to_comment_id: Optional[int] = None)  | Comment  | Add a new comment to media or reply to an existing comment  |  
| media_comments(media_id: str, amount: int = 20)  | List[Comment]  | Get comments for media; pass `amount=0` to keep paginating until exhaustion  |  
| media_comments_chunk(media_id: str, max_amount: int, min_id: str = None)  | Tuple[List[Comment], str]  | Get a paginated chunk of comments and the next `min_id` cursor  |  
| media_comments_v1(media_id: str, amount: int = 20)  | List[Comment]  | Get comments through the private mobile comments endpoint  |  
| media_comments_v1_chunk(media_id: str, min_id: str = “”, max_id: str = “”)  | Tuple[List[Comment], str, str]  | Get one private comments page and both cursors  |  
| media_stream_comments_v1_chunk(media_id: str, min_id: str = “”, max_id: str = “”)  | Tuple[List[Comment], str, str]  | Get one streamed comments page and both cursors  |  
| media_comments_gql(media_pk: str, amount: int = 50, max_requests: int = 0)  | List[dict]  | Get comments through the web GraphQL doc_id endpoint  |  
| media_comments_gql_chunk(media_pk: str, end_cursor: str = “”)  | Tuple[List[dict], str]  | Get one web GraphQL comments page  |  
| media_comments_public_gql(code: str, amount: int = 50, max_requests: int = 0)  | List[dict]  | Get public web GraphQL comments by media shortcode  |  
| media_comments_public_gql_chunk(code: str, end_cursor: str = “”)  | Tuple[List[dict], str]  | Get one public web GraphQL comments page by media shortcode  |  
| media_comments_threaded_gql(media_pk: str, comment_pk: str, amount: int = 0)  | List[dict]  | Get threaded replies through the web GraphQL doc_id endpoint  |  
| media_comments_threaded_gql_chunk(media_pk: str, comment_pk: str, end_cursor: str = “”)  | Tuple[List[dict], str]  | Get one threaded GraphQL comments page  |  
| media_comment_infos(media_ids: List[str])  | dict  | Bulk-fetch comment summaries for media ids  |  
| media_comment_replies(media_id: str, comment_id: str, amount: int = 0)  | List[Comment]  | Get replies for a parent media comment; pass `amount=0` to keep paginating until exhaustion  |  
| media_comment_replies_chunk(media_id: str, comment_id: str, max_amount: int, min_id: str = None)  | Tuple[List[Comment], str]  | Get a paginated chunk of replies and the next child cursor  |  
| media_check_offensive_comment(media_id: str, text: str)  | bool  | Ask Instagram whether a comment text is considered offensive  |  
| media_check_offensive_comment_v2(media_id: str, comment: str)  | dict  | Lighter variant of `media_check_offensive_comment` — same endpoint without `with_action_data` wrapping; returns the raw payload so callers can inspect category / confidence flags beyond `is_offensive`  |  
| comment_like(comment_pk: int, revert: bool = False)  | bool  | Like a comment  |  
| comment_unlike(comment_pk: int)  | bool  | Unlike a comment  |  
| comment_pin(media_id: str, comment_pk: int, revert: bool = False)  | bool  | Pin a comment on your media  |  
| comment_unpin(media_id: str, comment_pk: int)  | bool  | Unpin a previously pinned comment  |  
| comment_bulk_delete(media_id: str, comment_pks: List[int])  | bool  | Delete one or more comments from your media  |  
| comment_likers_gql(comment_pk: str, amount: int = 0)  | List[dict]  | Get comment likers through public GraphQL  |  
| comment_likers_gql_chunk(comment_pk: str, end_cursor: str = “”)  | Tuple[List[dict], str]  | Get one public GraphQL comment-likers page  |  
Example:

```
>>> from instagrapi import Client

>>> cl = Client()
>>> cl.login(USERNAME, PASSWORD)

>>> media_id = cl.media_id(cl.media_pk_from_url('https://www.instagram.com/p/ByU3LAslgWY/'))

>>> comment = cl.media_comment(media_id, "Test comment")
>>> comment.dict()
{'pk': 17926777897585108,
 'text': 'Test comment',
 'user': {'pk': 1903424587,
  'username': 'example',
  'full_name': 'Example Example',
  'profile_pic_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t51.2885-19/s150x150/156689363_269505058076642_6448820957073669709_n.jpg?tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_ohc=EtzrL0pAdg8AX9pE_wN&edm=ABQSlwABAAAA&ccb=7-4&oh=e04d45b7651140e7fef61b1f67f1f408&oe=60C65AD1&_nc_sid=b2b2bd', scheme='https', host='scontent-hel3-1.cdninstagram.com', tld='com', host_type='domain', path='/v/t51.2885-19/s150x150/156689363_269505058076642_6448820957073669709_n.jpg', query='tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_ohc=EtzrL0pAdg8AX9pE_wN&edm=ABQSlwABAAAA&ccb=7-4&oh=e04d45b7651140e7fef61b1f67f1f408&oe=60C65AD1&_nc_sid=b2b2bd'),
  'stories': []},
 'created_at_utc': datetime.datetime(2021, 5, 15, 14, 50, 3, tzinfo=datetime.timezone.utc),
 'content_type': 'comment',
 'status': 'Active',
 'has_liked': None,
 'like_count': None}

>>> comment = cl.media_comment(media_id, "Test comment 2", replied_to_comment_id=comment.pk)
>>> comment.dict()
{'pk': 17926777897585109,
 'text': 'Test comment 2',
 'user': {'pk': 1903424587,
  'username': 'example',
  'full_name': 'Example Example',
  'profile_pic_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t51.2885-19/s150x150/156689363_269505058076642_6448820957073669709_n.jpg?tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_ohc=EtzrL0pAdg8AX9pE_wN&edm=ABQSlwABAAAA&ccb=7-4&oh=e04d45b7651140e7fef61b1f67f1f408&oe=60C65AD1&_nc_sid=b2b2bd', scheme='https', host='scontent-hel3-1.cdninstagram.com', tld='com', host_type='domain', path='/v/t51.2885-19/s150x150/156689363_269505058076642_6448820957073669709_n.jpg', query='tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_ohc=EtzrL0pAdg8AX9pE_wN&edm=ABQSlwABAAAA&ccb=7-4&oh=e04d45b7651140e7fef61b1f67f1f408&oe=60C65AD1&_nc_sid=b2b2bd'),
  'stories': []},
 'created_at_utc': datetime.datetime(2021, 5, 15, 14, 50, 3, tzinfo=datetime.timezone.utc),
 'content_type': 'comment',
 'status': 'Active',
 'has_liked': None,
 'like_count': None}

>>> comments = cl.media_comments(media_id)
>>> comments[0].dict()
 {'pk': 17926777897585108,
 'text': 'Test comment',
 'user': {'pk': 1903424587,
  'username': 'example',
  'full_name': 'Example Example',
  'profile_pic_url': HttpUrl('https://scontent-hel3-1.cdninstagram.com/v/t51.2885-19/s150x150/156689363_269505058076642_6448820957073669709_n.jpg?tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_ohc=EtzrL0pAdg8AX9pE_wN&edm=AId3EpQBAAAA&ccb=7-4&oh=e3fbafcdb63cec3535004e85eb3397ae&oe=60C65AD1&_nc_sid=705020', scheme='https', host='scontent-hel3-1.cdninstagram.com', tld='com', host_type='domain', path='/v/t51.2885-19/s150x150/156689363_269505058076642_6448820957073669709_n.jpg', query='tp=1&_nc_ht=scontent-hel3-1.cdninstagram.com&_nc_ohc=EtzrL0pAdg8AX9pE_wN&edm=AId3EpQBAAAA&ccb=7-4&oh=e3fbafcdb63cec3535004e85eb3397ae&oe=60C65AD1&_nc_sid=705020'),
  'stories': []},
 'created_at_utc': datetime.datetime(2021, 5, 15, 14, 50, 3, tzinfo=datetime.timezone.utc),
 'content_type': 'comment',
 'status': 'Active',
 'has_liked': False,
 'like_count': 0}

>>> (comments_part1, next_min_id) = cl.media_comments_chunk(media_id, 100)
>>> next_min_id
QVFBQmZCa1dxaFB5eFpBY2luVFMwLWdmN2ZCcUV6OF9hQWlIQk12ZWZqUlctZ2pOa1J5YjJ6bFY5Q1doSGNuUmpxSS1DdXRvZ0NLemJrR1hXd2p0dS1JMg==
>>> (comments_part2, next_min_id) = cl.media_comments_chunk(media_id, 100, next_min_id)
>>> next_min_id
QVFEbHpIWmpFc3BNUkgzUFVuOGZOQlhDQ1hHeWlVWHlJSnBhb2FHbFB3YlJtNThnOUlrd01JUWdKRmRwZTRpWWU0bnZmX3VMNHlwcDBkWTJpZjQ2NE9SeQ==

>>> public_comments = cl.media_comments_public_gql("CjPUjEvDKT4", amount=40)
>>> public_comments[0]["text"]
'Example public comment'

>>> parent_comment = cl.media_comments(media_id)[0]
>>> replies = cl.media_comment_replies(media_id, parent_comment.pk)
>>> replies[0].dict()
{'pk': 17926777897585110,
 'text': 'Reply text',
 'user': {'pk': 1903424587,
  'username': 'example',
  'full_name': 'Example Example',
  'profile_pic_url': None},
 'created_at_utc': datetime.datetime(2021, 5, 15, 14, 51, 3, tzinfo=datetime.timezone.utc),
 'content_type': 'comment',
 'status': 'Active',
 'replied_to_comment_id': '17926777897585108',
 'has_liked': False,
 'like_count': 0}

>>> preflight = cl.media_check_offensive_comment_v2(media_id, "Some draft text")
>>> preflight["is_offensive"]
False

>>> if not preflight["is_offensive"]:
...     cl.media_comment(media_id, "Some draft text")

>>> cl.comment_like(17926777897585108)
True

>>> cl.comment_unlike(17926777897585108)
True

>>> cl.comment_bulk_delete(media_id, [17926777897585108])
True

```

Notes:
  * `media_comments()` fetches both regular and headload comment pages until `amount` is reached.
  * `media_comments_chunk()` is the better choice when you want to store and resume the server cursor manually.
  * `media_comments_public_gql()` accepts a media shortcode and automatically builds the current public GraphQL `doc_id` request and post referer. Public web endpoints are still Instagram-gated and may return 401/403/429 depending on IP, TLS fingerprint, cookies, or session state.
  * `media_comment_replies()` fetches `inline_child_comments` for a parent comment and paginates with the returned child cursor.
  * `media_check_offensive_comment_v2()` can be used as an explicit lightweight preflight before `media_comment()`. `media_comment()` does not run extra preflight requests automatically, so callers can choose the request volume and handle the raw response.
  * `comment_pin()` / `comment_unpin()` only work on media owned by the authenticated account.
  * Reply creation is supported through `replied_to_comment_id`; reply retrieval is supported through `media_comment_replies()`.
  * Comment creation is a write action and can still trigger Instagram spam or trust checks. Reuse saved sessions, keep volume low on new accounts, and stop when Instagram returns feedback/challenge responses.




---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/highlight.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Highlight  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| highlight_pk_from_url(url: str)  | str  | Get highlight PK from URL  |  
| highlight_info(highlight_pk: str)  | Highlight  | Get highlight by PK or ID  |  
| user_highlights(user_id: str, amount: int = 0)  | List[Highlight]  | Get a user’s highlights  |  
| highlight_create(title: str, story_ids: List[str], cover_story_id: str = “”, crop_rect: List[float] = [0.0, 0.21830457, 1.0, 0.78094524])  | Highlight  | Create highlight  |  
| highlight_edit(highlight_pk: str, title: str = “”, cover: Dict = {}, added_media_ids: List[str] = [], removed_media_ids: List[str] = [])  | Highlight  | Low-level highlight edit helper  |  
| highlight_change_title(highlight_pk: str, title: str)  | Highlight  | Change title for highlight  |  
| highlight_change_cover(highlight_pk: str, cover_path: Path)  | Highlight  | Change cover for highlight  |  
| highlight_add_stories(highlight_pk: str, added_media_ids: List[str])  | Highlight  | Add stories to highlight  |  
| highlight_remove_stories(highlight_pk: str, removed_media_ids: List[str])  | Highlight  | Remove stories from highlight  |  
| highlight_delete(highlight_pk: str)  | bool  | Delete highlight  |  
Example:

```
>>> cl.highlight_info(17895485201104054).dict()
{
    'pk': 17895485201104054,
    'id': 'highlight:17895485201104054',
    'latest_reel_media': 1622366765,
    'cover_media': {
        'cropped_image_version': {'width': 150, 'height': 150, 'url': 'https://instagram.frix7-1.fna.fbcdn.net/v/t51.2885-...'},
        'crop_rect': [0, 0.21855760773966576, 1, 0.7814423922603342],
        'media_id': '2584323966581791455_8641392340'
    },
    'user': {
        'pk': 8641392340,
        'username': 'bestskatetrick',
        'full_name': 'The Best Skate Tricks',
        'profile_pic_url': HttpUrl('https://instagram.frix7-1.fna.fbcdn.net/v/t51.2885-19/s150x150/6526...'),
        'profile_pic_url_hd': None,
        'is_private': False,
        'stories': []
    },
    'title': 'Picnic 2021',
    'created_at': datetime.datetime(2021, 5, 29, 19, 39, 15, tzinfo=datetime.timezone.utc),
    'is_pinned_highlight': False,
    'media_count': 19,
    'media_ids': [2584323966581791455, 2584328925731679183, 2584328595757338887, ...],  # story ids
    'items': [Story, Story, Story, ...]
}

>>> cl.user_highlights(29817608135)
[Highlight(pk='17907771728171896', id='highlight:17907771728171896', latest_reel_media=1638039687, ...), ...]

```

Change highlight:

```
>>> cl.highlight_create("Test", ["2722223419628084989_29817608135"])
Highlight(pk='17920472818962144', id='highlight:17920472818962144', latest_reel_media=1638734336, ...)

>>> cl.highlight_change_title(17907771728171896, "Example title")
Highlight(pk='17907771728171896', id='highlight:17907771728171896', latest_reel_media=1638039687, ...)

>>> cl.highlight_change_cover(17907771728171896, "/tmp/test.jpg")  # recommend 720x720
Highlight(pk='17907771728171896', id='highlight:17907771728171896', ...)

>>> cl.highlight_add_stories(17907771728171896, [2722223419628084989])
Highlight(pk='17907771728171896', id='highlight:17907771728171896', latest_reel_media=1638734336, ...)

>>> cl.highlight_remove_stories(17907771728171896, [2722223419628084989])
Highlight(pk='17907771728171896', id='highlight:17907771728171896', latest_reel_media=1638039687, ...)

>>> cl.highlight_delete(17920472818962144)
True

```

Notes:
  * `story_ids`, `added_media_ids`, and `removed_media_ids` should use story/media IDs, not bare PKs.
  * `highlight_change_cover()` uploads the cover image first and then applies it through `highlight_edit()`.
  * `highlight_edit()` is useful when you want to combine multiple changes in one request instead of calling title/cover/story helpers separately.




---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/notes.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Notes  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| get_notes()  | List[Note]  | Retrieve direct Notes  |  
| get_note_by_user(notes: List[Note], username: str)  | Optional[Note]  | Find a Note by username  |  
| get_note_text_by_user(notes: List[Note], username: str)  | Optional[str]  | Get note text by username  |  
| create_note(text: str, audience: NoteAudience = NoteAudience.MUTUAL_FOLLOWERS)  | Note  | Post a new Note  |  
| notes_music_browser()  | Dict  | Retrieve music candidates for Notes  |  
| create_music_note(track: Track | Dict, text: str = “”, audience: NoteAudience = NoteAudience.MUTUAL_FOLLOWERS, start_time: Optional[int] = None, duration: int = 30000, browse_session_id: Optional[str] = None, alacorn_session_id: Optional[str] = None)  | Note  | Post a new Note with music  |  
| delete_note(note_id: int)  | bool  | Delete a posted Note  |  
| last_seen_update_note()  | bool  | Update the last seen time  |  
Example:

```
>>> from instagrapi.mixins.note import NoteAudience
>>> note = cl.create_note("Hello from Instagrapi!", audience=NoteAudience.MUTUAL_FOLLOWERS)
>>> print(note.dict())
{'id': '17849203563031468',
'text': 'Hello from Instagrapi!',
'user_id': 12312312312,
'user': {
  'pk': '12312312312',
  'username': 'something',
  'full_name': 'merimi on top',
  'profile_pic_url': HttpUrl('https://scontent-dus1-1.cdninstagram.com/v/t51.2885-19/364347953_6289474204435297_7603222331512295081_n.jpg?stp=dst-jpg_s150x150&_nc_ht=scontent-dus1-1.cdninstagram.com&_nc_cat=101&_nc_ohc=DVaE0MQwn0YAX8-S8dm&edm=AE-H4JwBAAAA&ccb=7-5&oh=00_AfAnH4mHGMl7B5tqzU7b9PMz9qSC4QE_-EX067lwPHnN1w&oe=64DDA1CB&_nc_sid=cff473', ),
  'profile_pic_url_hd': None,
  'is_private': False,
  'stories': []},
'audience': 0,
'created_at': datetime.datetime(2023, 8, 13, 14, 33, 43, tzinfo=datetime.timezone.utc),
'expires_at': datetime.datetime(2023, 8, 14, 14, 33, 43, tzinfo=datetime.timezone.utc),
'is_emoji_only': False,
'has_translation': False,
'note_style': 0}
>>> notes = cl.get_notes()
>>> print(notes)
[Note(id='17849203563031468', text='Hello from Instagrapi, everyone can see it!', ..., has_translation=False, note_style=0), Note(id='17902958207826742', text='Am so happy 💃💃💃💃🙈🤭', ..., has_translation=False, note_style=0)]

>>> cl.get_note_by_user(notes, "something")
Note(id='17849203563031468', text='Hello from Instagrapi, everyone can see it!', ...)

>>> cl.get_note_text_by_user(notes, "something")
'Hello from Instagrapi, everyone can see it!'

>>> cl.last_seen_update_note()

>>> cl.delete_note(note.id)

```

Music Notes use the same audience values as text Notes. A typical flow is to fetch candidates from `notes_music_browser()`, choose a track from the response, and pass it to `create_music_note()`:

```
music = cl.notes_music_browser()
track = music["items"][0]["playlist"]["preview_items"][0]["track"]

note = cl.create_music_note(
    track=track,
    text="",
    audience=NoteAudience.CLOSE_FRIENDS,
    alacorn_session_id=music.get("alacorn_session_id"),
)
cl.delete_note(note.id)

```

## Get Notes | Post Notes | Delete Notes
  * _Get Notes from Direct_
  * _Publish a new note with the ability to select an audience_
  * _Publish a new note with music_
  * _Delete posted Notes_
  * _Update last seen of Notes_


The note should not exceed 60 characters. The rate in between Notes requests should be fairly high _(_ i.e : 1 request/ 2 min)* to avoid triggering Instagram API
Common arguments:
  * `note_id` - ID of the Note object
  * `text` - Content of the Note
  * `audience` - Who can see the note. Use `NoteAudience.MUTUAL_FOLLOWERS` for followers you follow back or `NoteAudience.CLOSE_FRIENDS` for Close Friends only. Instagram still receives the numeric wire value internally.
  * `username` - Username used to search in an existing `notes` list
  * `track` - Track object or raw track dict from `notes_music_browser()`


Typical flow:

```
notes = cl.get_notes()
note = cl.get_note_by_user(notes, "instagram")
if note:
    print(note.text)

```



---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/realtime.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Realtime MQTT
!!! warning Realtime MQTT support is experimental. Instagram can change this private transport without notice.
The realtime client opens Instagram’s MQTToT connection for live events after login. It is useful when you need callbacks for realtime payloads instead of polling HTTP endpoints. It can also publish lightweight Direct actions over MQTT. Use the regular Direct methods for media sends and complete thread management.
FBNS push notifications use a separate `mqtt-mini.facebook.com` device-auth connection. Use FBNS when you need Instagram push payloads, for example Direct message notification callbacks.  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| `realtime_connect(transport=None)`  | `RealtimeClient`  | Create and connect the stateful realtime client  |  
| `realtime_disconnect()`  | `None`  | Disconnect the active realtime client  |  
| `realtime_on(event, handler)`  | `None`  | Register an event handler on the active realtime client  |  
| `realtime_ping()`  | `bool`  | Send a keepalive ping and wait for `PINGRESP`  |  
| `realtime_read_once()`  | `Any`  | Read one packet from the active realtime client  |  
| `fbns_connect(transport=None, auth=None, register=True)`  | `FbnsClient`  | Create, connect, and register the stateful FBNS client  |  
| `fbns_disconnect()`  | `None`  | Disconnect the active FBNS client  |  
| `fbns_on(event, handler)`  | `None`  | Register an event handler on the active FBNS client  |  
| `fbns_ping()`  | `bool`  | Send an FBNS keepalive ping and wait for `PINGRESP`  |  
| `fbns_read_once()`  | `Any`  | Read one packet from the active FBNS client  |  
`RealtimeClient` also exposes lower-level helpers:  
| Method  | Description  |  
| --- | --- |  
| `on(event, handler)`  | Register a handler for `receive`, `message`, or `realtime_sub`  |  
| `graph_ql_subscribe(subscriptions)`  | Publish raw GraphQL realtime subscriptions  |  
| `skywalker_subscribe(subscriptions)`  | Publish raw Skywalker subscriptions  |  
| `iris_subscribe(seq_id, snapshot_at_ms)`  | Publish Direct inbox sync state for message-sync events  |  
| `direct_subscribe(amount=1)`  | Fetch Direct inbox sync state and subscribe to message-sync events  |  
| `direct_send_text(thread_id, text, client_context=None)`  | Publish a Direct text message over MQTT  |  
| `direct_send_reaction(thread_id, item_id, emoji="", ...)`  | Publish a Direct reaction over MQTT  |  
| `direct_mark_seen(thread_id, item_id)`  | Publish Direct seen state over MQTT  |  
| `direct_indicate_activity(thread_id, is_active=True, client_context=None)`  | Publish Direct typing/activity state over MQTT  |  
| `send_foreground_state(...)`  | Publish foreground state and optional topic changes  |  
| `publish_json(topic, data)`  | Publish a JSON payload to a raw MQTToT topic  |  
| `ping()`  | Send a keepalive ping and wait for `PINGRESP`  |  
| `read_once()`  | Read and dispatch one packet  |  
Basic receive loop:

```
from instagrapi import Client

cl = Client()
cl.login(USERNAME, PASSWORD)


def handle_receive(event):
    print(event["topic"], event["payload"])


cl.realtime_on("receive", handle_receive)
rt = cl.realtime_connect()

while True:
    cl.realtime_read_once()

```

Receive Direct message sync payloads:

```
import json

from instagrapi import Client

cl = Client()
cl.login(USERNAME, PASSWORD)


def handle_direct_message(payload):
    print(json.dumps(payload, indent=2, ensure_ascii=False))


cl.realtime_on("message", handle_direct_message)

rt = cl.realtime_connect()
rt.direct_subscribe()

try:
    # Optional keepalive check for smoke tests or long-running workers.
    rt.ping()

    while True:
        cl.realtime_read_once()
except KeyboardInterrupt:
    pass
finally:
    cl.realtime_disconnect()

```

Send lightweight Direct actions over MQTT:

```
rt.direct_send_text(thread_id, "Hello from MQTT")
rt.direct_send_reaction(thread_id, item_id, emoji="❤️")
rt.direct_indicate_activity(thread_id, is_active=True)
rt.direct_mark_seen(thread_id, item_id)

```

For photos, videos, voice, thread creation, request approval, and other full Direct operations, use the normal `direct_*` HTTP methods. The MQTT payload shape is private and can change server-side, so inspect received dictionaries before depending on nested keys.
Receive FBNS push notifications:

```
import json

from instagrapi import Client

cl = Client()
cl.login(USERNAME, PASSWORD)


def handle_push(payload):
    print(json.dumps(payload, indent=2, ensure_ascii=False))


cl.fbns_on("push", handle_push)
fbns = cl.fbns_connect()

try:
    fbns.ping()
    while True:
        cl.fbns_read_once()
except KeyboardInterrupt:
    pass
finally:
    cl.fbns_disconnect()

```

`fbns_connect()` registers the FBNS token with Instagram’s private push register endpoint. The device-auth state returned by the broker is stored in `settings["fbns_auth"]`, so `dump_settings()` can persist it with the normal session data.
Subscribe to raw realtime topics:

```
rt.graph_ql_subscribe(["<graphql-subscription>"])
rt.skywalker_subscribe(["<skywalker-subscription>"])

```

Raw GraphQL and Skywalker subscription strings are advanced and unstable. Message sync is subscribed by the default connection topics, so the Direct message example above does not need an extra raw subscription.
Events:
  * `receive` is emitted for every decoded publish packet as `{"topic": topic, "payload": payload}`.
  * `message` is emitted for message-sync payloads.
  * `direct` is emitted for parsed Direct realtime payloads from message-sync or realtime-sub streams.
  * `typing`, `seen`, and `presence` are emitted for Direct realtime payloads that can be classified.
  * `send_response` is emitted for MQTT Direct command responses.
  * `iris_sub_response` is emitted for Iris subscription responses.
  * `realtime_sub` is emitted for realtime subscription payloads.
  * `push` is emitted for parsed FBNS `fbpushnotif` payloads.
  * FBNS also emits the notification `collapse_key` as an event name when present, for example `direct_v2_message`.
  * FBNS emits `reg_response`, `registered`, `logging`, and `pp` for registration and lower-level broker payloads.




---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/pydroid.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Pydroid and ffmpeg
Android/Pydroid can run many `instagrapi` flows, but video helpers need special care because Android apps often cannot execute arbitrary binaries from shared storage.
## What needs ffmpeg
`instagrapi` does not need ffmpeg for login, reads, photo uploads, downloads, or normal API requests.
For standard MP4 files, `instagrapi` can read video width, height, and duration with its built-in MP4 parser. If you also pass a thumbnail file, these upload helpers do not need MoviePy/ffmpeg just to analyze the upload:

```
from pathlib import Path

cl.video_upload(Path("video.mp4"), "caption", thumbnail=Path("thumb.jpg"))
cl.clip_upload(Path("reel.mp4"), "caption", thumbnail=Path("thumb.jpg"))
cl.igtv_upload(Path("video.mp4"), "title", "caption", thumbnail=Path("thumb.jpg"))
cl.video_upload_to_story(Path("story.mp4"), thumbnail=Path("thumb.jpg"))

```

MoviePy/ffmpeg is still required when `instagrapi` has to render or extract media. Install the optional video extra for these flows:

```
pip install "instagrapi[video]"
pip install --no-deps "moviepy==2.2.1"

```

The extra is intentionally not part of the default install, because it pulls in NumPy and ffmpeg-related packages that can be hard to build on Android. MoviePy `2.2.1` currently declares `Pillow<12`, but instagrapi keeps `Pillow>=12.2.0` for security fixes; the `--no-deps` install keeps the safe Pillow version. MoviePy `1.x` is no longer supported by instagrapi’s video helpers.
  * automatic thumbnail generation when `thumbnail` is not provided
  * `StoryBuilder`
  * `prepare_video()`
  * `clip_upload_as_reel_with_music()` and other audio/video composition helpers
  * video album uploads, because album video items currently generate thumbnails internally
  * non-standard MP4 files that the built-in parser cannot read


Use `clip_upload_with_music(..., thumbnail=...)` when you only need Reels music metadata and do not need local audio muxing.
## Error
If ffmpeg is missing or cannot be executed, video thumbnail generation can fail with:

```
RuntimeError: No ffmpeg exe could be found. Install ffmpeg on your system, or set the IMAGEIO_FFMPEG_EXE environment variable.

```

Current `instagrapi` upload helpers raise a clearer error for this thumbnail path:

```
Could not generate video thumbnail. Pass thumbnail=... or install MoviePy 2.2.1. Install video dependencies with pip install "instagrapi[video]" and then install MoviePy with pip install --no-deps "moviepy==2.2.1". Make sure ffmpeg is executable or set IMAGEIO_FFMPEG_EXE.

```

## Fix
The most reliable Pydroid setup is to pre-process the video outside Pydroid and pass both files:
  * `video.mp4` - MP4 file accepted by Instagram, usually H.264 video with AAC audio
  * `thumb.jpg` - JPEG thumbnail for the upload


Then call the upload method with `thumbnail=Path("thumb.jpg")`.
If you need automatic thumbnail generation or StoryBuilder inside Pydroid, install the optional video dependencies and MoviePy, install an ffmpeg binary that the Pydroid app can execute, and set `IMAGEIO_FFMPEG_EXE` before running the upload:

```
import os

os.environ["IMAGEIO_FFMPEG_EXE"] = "/absolute/path/to/ffmpeg"

```

Verify the same Python process can execute it:

```
import os
import subprocess

subprocess.run([os.environ["IMAGEIO_FFMPEG_EXE"], "-version"], check=True)

```

If this raises `PermissionError`, the file exists but Android is not allowing Pydroid to execute it. A binary placed under shared storage such as `/storage/emulated/0/...` can hit that limitation. Move ffmpeg to a location executable by the app or use a Pydroid package/plugin that provides an executable binary.
## Minimal upload example

```
from pathlib import Path

from instagrapi import Client

cl = Client()
cl.login(USERNAME, PASSWORD)

media = cl.clip_upload(
    Path("reel.mp4"),
    "Uploaded from Pydroid",
    thumbnail=Path("reel-thumb.jpg"),
)
print(media.pk)

```

If you omit `thumbnail=...`, Pydroid must have a working ffmpeg executable so `instagrapi` can capture a frame from the video.


---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/termux.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Termux
Termux can run many `instagrapi` flows, but Android does not use the same binary wheel ecosystem as desktop Linux. Keep the default install small and add media tooling only when the script really needs it.
## Install

```
pkg update
pkg install python python-pillow
python -m pip install -U pip setuptools wheel
python -m pip install --extra-index-url https://termux-user-repository.github.io/pypi/ instagrapi

```

`python-pillow` is recommended because photo uploads use Pillow through `instagrapi.image_util`. Installing it with `pkg` avoids a slow or fragile Pillow source build in pip.
The Termux User Repository PyPI index provides Android wheels for native packages that PyPI may only publish as desktop Linux wheels. On Android, `instagrapi` uses `pydantic==2.12.5`, which depends on `pydantic-core==2.41.5`; that version has Android wheels for Python 3.13 in the Termux index. Newer `pydantic-core` releases may otherwise try to build with Rust and fail on-device.
## Video Uploads
For standard MP4 uploads, pass your own thumbnail and `instagrapi` can read width, height, and duration with its built-in MP4 parser:

```
from pathlib import Path

media = cl.clip_upload(
    Path("reel.mp4"),
    "Uploaded from Termux",
    thumbnail=Path("reel-thumb.jpg"),
)

```

This path does not need MoviePy, NumPy, or ffmpeg.
## Optional Video Helpers
Install the optional video extra only if you need automatic thumbnail generation, `StoryBuilder`, `prepare_video()`, or audio/video composition helpers:

```
pkg install ffmpeg
python -m pip install "instagrapi[video]"
python -m pip install --no-deps "moviepy==2.2.1"

```

MoviePy `2.2.1` currently declares `Pillow<12`, but instagrapi keeps `Pillow>=12.2.0` for security fixes; the `--no-deps` install keeps the safe Pillow version. MoviePy `1.x` is no longer supported by instagrapi’s optional video helpers.
If MoviePy cannot find ffmpeg, point ImageIO at the Termux binary before running the script:

```
export IMAGEIO_FFMPEG_EXE="$(command -v ffmpeg)"

```

If `pip install "instagrapi[video]"` tries to build NumPy and fails, avoid the optional video helpers on-device: prepare the MP4 and thumbnail elsewhere, then use upload methods with `thumbnail=...`.


---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/story.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Story  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| user_stories(user_id: str, amount: int = None)  | List[Story]  | Get list of stories by user_id; public/web first, private fallback when authenticated  |  
| story_info(story_pk: int, use_cache: bool = True)  | Story  | Return story info  |  
| story_delete(story_pk: int)  | bool  | Delete story  |  
| story_seen(story_pks: List[int], skipped_story_pks: List[int])  | bool  | Mark a story as seen  |  
| story_pk_from_url(url: str)  | int  | Get Story (media) PK from URL  |  
| story_download(story_pk: int, filename: str = “”, folder: Path = “”)  | Path  | Download story media by media_type  |  
| story_download_by_url(url: str, filename: str = “”, folder: Path = “”)  | Path  | Download story media using URL to file (mp4 or jpg)  |  
| story_viewers(story_pk: int, amount: int = 20)  | List[UserShort]  | List of story viewers (via Private API)  |  
| story_likers(story_pk: int, amount: int = 0)  | List[UserShort]  | List of story likers (via Private API)  |  
| archive_story_days(amount: int = 0, include_memories: bool = True)  | List[StoryArchiveDay]  | Get your story archive day shells  |  
| archive_stories(amount: int = 0)  | List[Story]  | Get your archived stories  |  
| story_like(story_id: str, revert: bool = False, mark_seen: bool = True)  | bool  | Like a story  |  
| story_unlike(story_id: str)  | bool  | Unlike a story  |  
| story_poll_vote(story_id: str, poll_id: str, vote: int)  | bool  | Vote in a story poll by option index  |  
Example:

```
>>> cl.story_download(cl.story_pk_from_url('https://www.instagram.com/stories/example/2581281926631793076/'))
PosixPath('/app/189361307_229642088942817_9180243596650100310_n.mp4')

>>> s = cl.story_info(2581281926631793076)

>>> cl.story_download_by_url(s.video_url)  # url to mp4 file
PosixPath('/app/189361307_229642088942817_9180243596650100310_n.mp4')

>>> cl.story_download_by_url(s.thumbnail_url)  # URL to jpg file
PosixPath('/app/191260083_2908005872746895_8988438451809588865_n.jpg')

>>> days = cl.archive_story_days(amount=1)
>>> days[0].id
'archiveDay:1710000000000'

>>> archived = cl.archive_stories(amount=5)
>>> [story.pk for story in archived]
['3155832952940083788']

>>> story = cl.user_stories(USER_ID, amount=1)[0]
>>> cl.story_poll_vote(story.id, story.polls[0].id, 0)  # vote for the first option
True

```

## Story Archive
`archive_story_days()` returns `StoryArchiveDay` objects for the logged-in account’s story archive. Use `archive_stories()` when you need the story media items from those archive days.
Low level methods:  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| archive_story_days_v1(amount: int = 0, include_memories: bool = True)  | List[StoryArchiveDay]  | Get story archive days via private mobile API  |  
| archive_story_days_paginated_v1(amount: int = 0, end_cursor: str = “”, include_memories: bool = True, reel_id: str = “”)  | Tuple[List[StoryArchiveDay], str]  | Get one private API page of story archive days  |  
| archive_stories_v1(amount: int = 0)  | List[Story]  | Get archived stories via private mobile API  |  
## Upload Stories
Upload medias to your stories.
The story file should be at 9:16 resolution (e.g. 720x1280). If you have a different resolution, then you need to prepare a file or use the StoryBuilder, which is written about below.
Common arguments:
  * `path` - Path to media file
  * `caption` - Optional caption text
  * `thumbnail` - Thumbnail instead capture from source file
  * `mentions` - Tag profiles in story
  * `locations` - Add locations to story
  * `links` - Story link stickers (Instagram currently uses the first link only)
  * `hashtags` - Add hashtags to story
  * `stickers` - Add stickers to story
  * `medias` - Reshared feed media stickers
  * `polls` - Add polls to story
  * `resize_mode` - Story media sizing mode. Exposed as `StoryResizeMode = Literal["fill", "fit"]`; `"fill"` keeps the current crop/fill behavior, `"fit"` renders the full source media on a Story canvas without cropping

  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| photo_upload_to_story(path: Path, caption: str = “”, upload_id: str = “”, mentions: List[StoryMention] = [], locations: List[StoryLocation] = [], links: List[StoryLink] = [], hashtags: List[StoryHashtag] = [], stickers: List[StorySticker] = [], medias: List[StoryMedia] = [], polls: List[StoryPoll] = [], extra_data: Dict[str, str] = {}, resize_mode: StoryResizeMode = “fill”)  | Story  | Upload photo to story  |  
| video_upload_to_story(path: Path, caption: str = “”, thumbnail: Path = None, mentions: List[StoryMention] = [], locations: List[StoryLocation] = [], links: List[StoryLink] = [], hashtags: List[StoryHashtag] = [], stickers: List[StorySticker] = [], medias: List[StoryMedia] = [], polls: List[StoryPoll] = [], extra_data: Dict[str, str] = {}, resize_mode: StoryResizeMode = “fill”)  | Story  | Upload video to story  |  
| media_share_to_story(media_id: str, background: Path = None, caption: str = “”)  | Story  | Share an existing post to your story with a generated or provided background  |  
| photo_upload_to_story_with_music(path: Path, caption: str, track: Track or dict, thumbnail: Path = None, duration: float = 15.0, extra_data: Dict = {})  | Story  | Upload photo to story as a short video with the selected music track muxed into it  |  
| video_upload_to_story_with_music(path: Path, caption: str, track: Track or dict, thumbnail: Path = None, extra_data: Dict = {})  | Story  | Upload video to story with the selected music track muxed into it  |  
| story_music_extra_data(track: Track or dict, extra_data: Dict = {})  | dict  | Build Story music configure fields for manual story upload `extra_data`  |  
In `extra_data`, you can pass additional story settings, for example:  
| Method  | Type  | Description  |  
| --- | --- | --- |  
| audience  | String  |  [Publish story for close friends](https://github.com/subzeroid/instagrapi/issues/1210) `{"audience": "besties"}`  |  
Notes:
  * `links`, `hashtags`, `locations`, `stickers`, `medias`, and `polls` are all part of the story sticker payload.
  * `media_share_to_story()` is a convenience wrapper for the feed media sticker flow. It uploads a generated black 9:16 background unless you pass your own `background`.
  * Link stickers are supported through `StoryLink`; this is no longer the old Instagram “swipe up” flow.
  * For story uploads, use a 9:16 asset, pass `resize_mode="fit"` to keep the full source media visible on a Story canvas, or build one manually with `StoryBuilder`.
  * Android users should pass `thumbnail=...` for video stories or install the optional video dependencies, MoviePy `2.2.1`, and executable ffmpeg. See [Pydroid and ffmpeg](https://subzeroid.github.io/instagrapi/usage-guide/pydroid.html) and [Termux](https://subzeroid.github.io/instagrapi/usage-guide/termux.html).
  * Story music helpers require the optional video dependencies, MoviePy `2.2.1`, and executable ffmpeg because they render a local MP4 before upload.
  * Story music helpers add Story music metadata and bake the selected track into the uploaded media. They do not expose Instagram’s native interactive lyrics/music sticker UI.
  * Anonymous public story fetch is not guaranteed. If the public/web story path fails, reliable story retrieval usually requires an authenticated session.


Examples:

```
from instagrapi import Client
from instagrapi.types import StoryMention, StoryMedia, StoryLink, StoryHashtag, StoryPoll

cl = Client()
cl.login(USERNAME, PASSWORD)

media_pk = cl.media_pk_from_url('https://www.instagram.com/p/CGgDsi7JQdS/')
media_path = cl.video_download(media_pk)
example = cl.user_info_by_username('example')
hashtag = cl.hashtag_info('dhbastards')

cl.video_upload_to_story(
    media_path,
    "Credits @example",
    mentions=[StoryMention(user=example, x=0.49892962, y=0.703125, width=0.8333333333333334, height=0.125)],
    links=[StoryLink(webUri='https://github.com/subzeroid/instagrapi')],
    hashtags=[StoryHashtag(hashtag=hashtag, x=0.23, y=0.32, width=0.5, height=0.22)],
    medias=[StoryMedia(media_pk=media_pk, x=0.5, y=0.5, width=0.6, height=0.8)],
    polls=[StoryPoll(x = 0.5, y = 0.5, width = 0.7, height = 0.5, question = "Question", options = ["Option 1", "Option 2", "Option 3"])],
)

cl.media_share_to_story(media_pk, caption="Shared to story")

```

Fit a landscape photo or video into a Story without cropping:

```
cl.photo_upload_to_story(Path("/app/landscape.jpg"), resize_mode="fit")
cl.video_upload_to_story(Path("/app/landscape.mp4"), resize_mode="fit")

```

## Upload Story with Music
Story music upload works by rendering an MP4 locally and then publishing it with the normal story upload flow.

```
pip install "instagrapi[video]"
pip install --no-deps "moviepy==2.2.1"

```


```
from pathlib import Path

track = cl.search_music("song name")[0]

cl.video_upload_to_story_with_music(
    Path("/app/story.mp4"),
    "Credits @example",
    track,
    thumbnail=Path("/app/story-thumb.jpg"),
)

cl.photo_upload_to_story_with_music(
    Path("/app/story.jpg"),
    "Credits @example",
    track,
    duration=7,
)

```

## Build Story to Upload
If you want to format your story correctly (correct resolution, user mentions, etc) use StoryBuilder. StoryBuilder renders media with MoviePy and ffmpeg, so install the optional video dependencies first:

```
pip install "instagrapi[video]"
pip install --no-deps "moviepy==2.2.1"

```

MoviePy `2.2.1` currently declares `Pillow<12`, but instagrapi keeps `Pillow>=12.2.0` for security fixes; the `--no-deps` install keeps the safe Pillow version. Older MoviePy `1.x` imports such as `moviepy.editor` and clip methods such as `set_duration`, `set_position`, `resize`, and `subclip` are not supported by instagrapi’s video helpers.  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| StoryBuilder.build_clip(clip: moviepy.Clip, max_duration: int = 0)  | StoryBuild  | Build CompositeVideoClip with background and mentioned users. Return MP4 file and mentions with coordinates  |  
| StoryBuilder.video(max_duration: int = 0)  | StoryBuild  | Call build_clip(VideoClip, max_duration)  |  
| StoryBuilder.video_fit(max_duration: int = 0)  | StoryBuild  | Build a 720x1280 Story video canvas that fits the full source video without cropping  |  
| StoryBuilder.photo(max_duration: int = 0)  | StoryBuild  | Call build_clip(ImageClip, max_duration)  |  
Example:

```
from instagrapi.types import StoryMention, StoryMedia, StoryLink
from instagrapi.story import StoryBuilder

media_pk = cl.media_pk_from_url('https://www.instagram.com/p/CGgDsi7JQdS/')
media_path = cl.video_download(media_pk)
example = cl.user_info_by_username('example')

buildout = StoryBuilder(
    media_path,
    'Credits @example',
    [StoryMention(user=example)],
    Path('/path/to/background_720x1280.jpg')
).video(15)  # seconds

cl.video_upload_to_story(
    buildout.path,
    "Credits @example",
    mentions=buildout.mentions,
    links=[StoryLink(webUri='https://github.com/subzeroid/instagrapi')],
    medias=[StoryMedia(media_pk=media_pk)]
)

```

Result:
![](https://raw.githubusercontent.com/example/instagrapi/master/examples/dhb.gif)
Photo upload:

```
cl.photo_upload_to_story('/app/image.jpg')

```

Upload photo as video:

```
buildout = StoryBuilder('/app/image.jpg').photo()
cl.video_upload_to_story(buildout.path)

```

Like & unlike story:

```
pk = cl.story_pk_from_url("https://instagram.com/stories/purely.anand/2884886531427631361/")
info = cl.story_info(pk).dict()

cl.story_like(info['id']) # To like story
cl.story_unlike(info['id']) # To unlike story

# another way to unlike story
cl.story_like(info['id'], revert=True)

```

More stories here <https://www.instagram.com/wrclive/>


---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/direct.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Direct  
| Method  | Return  | Description  |  
| --- | --- | --- |  
|  `direct_threads(amount: int = 20, selected_filter: Optional[Literal["flagged", "unread"]] = None, box: Optional[Literal["primary", "general"]] = None, thread_message_limit: Optional[int] = None)`   
Note: omit `selected_filter` / `box` or pass `None` for the default inbox  | List[DirectThread]  | Get all threads from inbox  |  
| direct_pending_inbox(amount: int = 20)  | List[DirectThread]  | Get all threads from pending inbox  |  
| direct_requests(amount: int = 20)  | List[DirectThread]  | Get message request threads (pending inbox / invitations)  |  
| direct_pending_requests_preview(pending_inbox_filters: Optional[List[str]] = None)  | Dict  | Get lightweight pending request counters  |  
| direct_request_approve(thread_id: int)  | bool  | Approve a message request thread  |  
| direct_has_interop_upgraded()  | bool  | Check Direct interop upgrade state  |  
| direct_search_gen_ai_bots(amount: int = 20)  | List[UserShort]  | Search generated AI bot suggestions  |  
| direct_channels(user_id: Optional[int] = None, thread_subtypes: Optional[List[int]] = None)  | List[Dict]  | Get Direct channels for a user  |  
| direct_set_e2ee_eligibility(e2ee_eligibility: int = 4)  | bool  | Set Direct E2EE eligibility state  |  
| direct_thread(thread_id: int, amount: int = 20)  | DirectThread  | Get Thread with Messages  |  
| direct_messages(thread_id: int, amount: int = 20)  | List[DirectMessage]  | Get only Messages in Thread  |  
| direct_message(thread_id: int, message_id: int, amount: int = 20)  | DirectMessage  | Get one Message from Thread by id  |  
| direct_answer(thread_id: int, text: str)  | DirectMessage  | Add Message to exist Thread  |  
| direct_send(text: str, user_ids: List[int] = [], thread_ids: List[int] = [], reply_to_message: Optional[DirectMessage] = None)  | DirectMessage  | Send Message to Users or Threads, optionally as a reply  |  
| direct_send_reaction(thread_id: int, message_id: int, emoji: str = “❤”, client_context: Optional[str] = None)  | bool  | Send an emoji reaction to a message  |  
| direct_delete_reaction(thread_id: int, message_id: int, emoji: str = “❤”, client_context: Optional[str] = None)  | bool  | Delete your emoji reaction from a message  |  
| direct_message_like(thread_id: int, message_id: int, client_context: Optional[str] = None)  | bool  | Like a message with a heart reaction  |  
| direct_message_unlike(thread_id: int, message_id: int, client_context: Optional[str] = None)  | bool  | Remove your heart reaction from a message  |  
| direct_search(query: str)  | List[DirectShortThread]  | Search threads (for example by username)  |  
| direct_thread_by_participants(user_ids: List[int])  | DirectThread  | Get thread by user_id  |  
| direct_thread_create(user_ids: List[int], title: str = “”)  | str  | Create a group thread and return its thread id  |  
| direct_thread_add_users(thread_id: int, user_ids: List[int])  | bool  | Add users to a group thread  |  
| direct_thread_hide(thread_id: int)  | bool  | Delete (called “hide”)  |  
| direct_thread_update_title(thread_id: int, title: str)  | bool  | Update a group thread title  |  
| direct_media_share(media_id: str, user_ids: List[int] = [], thread_ids: List[int] = [], send_attribute: SEND_ATTRIBUTE_MEDIA = “feed_timeline”, media_type: DirectMediaType = “photo”)  | DirectMessage  | Share a media to users or existing threads  |  
| direct_story_share(story_id: str, user_ids: List[int], thread_ids: List[int])  | DirectMessage  | Share a story to list of users  |  
| direct_profile_share(user_id: str, user_ids: List[int], thread_ids: List[int])  | DirectMessage  | Share a user profile to list of users  |  
| direct_thread_mark_unread(thread_id: int)  | bool  | Mark a thread as unread  |  
| direct_message_delete(thread_id: int, message_id: int)  | bool  | Delete a message from thread  |  
| direct_message_unsend(thread_id: int, message_id: int)  | bool  | Unsend a message from thread  |  
| direct_thread_mute(thread_id: int, revert: bool = False)  | bool  | Mute the thread  |  
| direct_thread_unmute(thread_id: int)  | bool  | Unmute the thread  |  
| direct_thread_mute_video_call(thread_id: int, revert: bool = False)  | bool  | Mute video call for the thread  |  
| direct_thread_unmute_video_call(thread_id: int)  | bool  | Unmute video call for the thread  |  
| direct_send_photo(path: Path, user_ids: List[int], thread_ids: List[int])  | DirectMessage  | Send a direct photo to list of users or threads  |  
| direct_send_video(path: Path, user_ids: List[int], thread_ids: List[int])  | DirectMessage  | Send a direct video (.mp4 / H.264 + AAC) to list of users or threads  |  
| direct_send_voice(path: Path, user_ids: List[int], thread_ids: List[int], waveform: Optional[List[float]])  | DirectMessage  | Send a direct voice (audio) message; path must be m4a/AAC  |  
| video_upload_to_direct(path: Path, caption: str, thumbnail: Path, mentions: List[StoryMention], thread_ids: List[int] = [], extra_data: Dict[str, str] = {})  | DirectMessage  | Upload video to direct thread as a story and configure it  |  
### Option types
Direct media type is exposed as `DirectMediaType = Literal["photo", "video"]`.  
| Type  | Values  | Used by  |  
| --- | --- | --- |  
| `DirectMediaType`  |  `"photo"`, `"video"`  |  `direct_send_file(content_type=...)`, `direct_media_share(media_type=...)`  |  
Notes:
  * For `direct_send()`, `direct_media_share()`, `direct_send_photo()`, `direct_send_video()`, and `direct_send_voice()`, pass exactly one of `user_ids` or `thread_ids`.
  * Direct recipient arguments accept either one id (`user_ids=123`) or a list of ids (`user_ids=[123]`).
  * Direct message requests / invitations are exposed as `direct_requests()`; `direct_pending_inbox()` remains as the older name.
  * `direct_pending_requests_preview()` is the lightweight Android-app preview for request counters; use `direct_requests()` when you need the actual threads.
  * `direct_channels()` and `direct_search_gen_ai_bots()` expose raw app surfaces whose response shape may vary by rollout.
  * `direct_thread()` paginates internally until it collects `amount` messages or reaches the end of the thread.
  * `direct_message()` scans the latest `amount` messages in a thread and raises `DirectMessageNotFound` if the id is not present in that window.
  * Shared XMA items such as `xma_clip`, `xma_media_share`, `xma_story_share`, and `xma_profile` keep their original payload in `message.raw_xma`. When Instagram includes `target_url`, the normalized link is also available through `message.xma_share`.
  * Disappearing direct photos and videos with `item_type == "raven_media"` are exposed through `message.visual_media`.
  * Media-changing direct endpoints are more sensitive to session quality than read-only inbox calls. Stable sessions loaded via `dump_settings()/load_settings()` are more reliable than browser-only `sessionid` reuse.


Handling disabled message requests:

```
from instagrapi.exceptions import DirectMessageRequestsDisabled

try:
    cl.direct_send("Hello", user_ids=[user_id])
except DirectMessageRequestsDisabled:
    print("The recipient does not accept new Direct message requests.")

```

Example of basic actions:

```
>>> from instagrapi import Client
>>> cl = Client()
>>> cl.login(USERNAME, PASSWORD)

>>> thread = cl.direct_threads(1)[0]
>>> thread.pk
18123276039123479

>>> thread.users
[UserShort(pk=123123123, username='something', full_name='Dima Something', profile_pic_url=HttpUrl('https://instagram.frix7-1.fna.fbcdn.net/v/t51.2885-19/s150x150/11374323_1630877790512376_1081658215_a.jpg?_nc_ht=instagram.frix7-1.fna.fbcdn.net&_nc_ohc=k22oMvVv8xEAX-UEVRB&edm=AI8ESKwBAAAA&ccb=7-4&oh=be799948b28f19d85158153d886d16d3&oe=6135D80F&_nc_sid=195af5', scheme='https', host='instagram.frix7-1.fna.fbcdn.net', tld='net', host_type='domain', path='/v/t51.2885-19/s150x150/11374323_1630877790512376_1081658215_a.jpg', query='_nc_ht=instagram.frix7-1.fna.fbcdn.net&_nc_ohc=k22oMvVv8xEAX-UEVRB&edm=AI8ESKwBAAAA&ccb=7-4&oh=be799948b28f19d85158153d886d16d3&oe=6135D80F&_nc_sid=195af5'), profile_pic_url_hd=None, is_private=False, stories=[])]

>>> thread.messages[0]
DirectMessage(id=300761992574947211231231241955932160, user_id=123123123, thread_id=None, timestamp=datetime.datetime(2021, 8, 31, 18, 20, 28, 754135, tzinfo=datetime.timezone.utc), item_type='text', is_shh_mode=False, reactions=None, text='Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua', animated_media=None, media=None, media_share=None, reel_share=None, story_share=None, felix_share=None, clip=None, placeholder=None)

>>> cl.direct_pending_inbox(1)[0]
DirectThread(
    pk=17881231232408606,
    id=3402823668123123123949128156938656669726,
    messages=[
        DirectMessage(
            id=30073094913010429825449992959033344,
            user_id=123123123123,
            ...
        )
    ],
    ...
)

>>> request = cl.direct_requests(1)[0]
>>> cl.direct_request_approve(request.id)
True

>>> cl.direct_thread(thread.id, 1)
DirectThread(
    pk=18103276039108479,
    id=340282366841710300949128373114263369599,
    messages=[
        DirectMessage(
            id=30076199257494728485375741955932160,
            user_id=7789547,
            ...
        )
    ],
    ...
)

>>> message = cl.direct_messages(thread.id, 1)[0]
DirectMessage(id=300712312341231237412312312360, user_id=12312312, thread_id=None, timestamp=datetime.datetime(2021, 8, 31, 18, 20, 28, 754135, tzinfo=datetime.timezone.utc), item_type='text', is_shh_mode=False, reactions=None, text='Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua', animated_media=None, media=None, media_share=None, reel_share=None, story_share=None, felix_share=None, clip=None, placeholder=None)

>>> cl.direct_message(thread.id, message.id)
DirectMessage(id=300712312341231237412312312360, user_id=12312312, thread_id=None, timestamp=datetime.datetime(2021, 8, 31, 18, 20, 28, 754135, tzinfo=datetime.timezone.utc), item_type='text', is_shh_mode=False, reactions=None, text='Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua', animated_media=None, media=None, media_share=None, reel_share=None, story_share=None, felix_share=None, clip=None, placeholder=None)

>>> cl.direct_answer(thread.id, 'Hello!')
DirectMessage(id=30076213210116812312341061613568, user_id=None, thread_id=34028236684171031231231231233331238762, timestamp=datetime.datetime(2021, 8, 31, 18, 33, 5, 127298, tzinfo=datetime.timezone.utc), item_type=None, is_shh_mode=None, reactions=None, text=None, animated_media=None, media=None, media_share=None, reel_share=None, story_share=None, felix_share=None, clip=None, placeholder=None)

>>> cl.direct_send('How are you?', user_ids=[cl.user_id])  # send youself
DirectMessage(id=30076213210116812312341061613568, user_id=None, thread_id=34028236684171031231231231233331238762, timestamp=datetime.datetime(2021, 8, 31, 18, 33, 5, 127298, tzinfo=datetime.timezone.utc), item_type=None, is_shh_mode=None, reactions=None, text=None, animated_media=None, media=None, media_share=None, reel_share=None, story_share=None, felix_share=None, clip=None, placeholder=None)

>>> cl.direct_send('How are you?', thread_ids=[thread.id])
DirectMessage(id=30076213210116812312341061613568, user_id=None, thread_id=34028236684171031231231231233331238762, timestamp=datetime.datetime(2021, 8, 31, 18, 33, 5, 127298, tzinfo=datetime.timezone.utc), item_type=None, is_shh_mode=None, reactions=None, text=None, animated_media=None, media=None, media_share=None, reel_share=None, story_share=None, felix_share=None, clip=None, placeholder=None)

>>> cl.direct_send('Reply text', thread_ids=[thread.id], reply_to_message=message)
DirectMessage(id=30076213210116812312341061613568, user_id=None, thread_id=34028236684171031231231231233331238762, timestamp=datetime.datetime(2021, 8, 31, 18, 33, 5, 127298, tzinfo=datetime.timezone.utc), item_type=None, is_shh_mode=None, reactions=None, text=None, animated_media=None, media=None, media_share=None, reel_share=None, story_share=None, felix_share=None, clip=None, placeholder=None)

>>> cl.direct_send_reaction(thread.id, message.id, emoji="😂", client_context=message.client_context)
True

>>> cl.direct_message_like(thread.id, message.id, client_context=message.client_context)
True

>>> cl.direct_message_unlike(thread.id, message.id, client_context=message.client_context)
True

>>> cl.direct_thread_by_participants([cl.user_id])
DirectThread(pk=178612312342, id=340282366812312312312341298762, messages=[DirectMessage(id=30076214123123123123123864, user_id=1903424587, thread_id=None, timestamp=datetime.datetime(2021, 8, 31, 18, 33, 49, 107154, ...)

>>> thread_id = cl.direct_thread_create([user_id_1, user_id_2], title="New group")
>>> cl.direct_thread(thread_id, amount=1)
DirectThread(pk=178612312342, id=340282366812312312312341298762, messages=[...], ...)

>>> cl.direct_thread_add_users(thread_id, [user_id_3])
True

>>> cl.direct_thread_update_title(thread.id, "New group title")
True

>>> cl.direct_media_share(media.pk, user_ids=[cl.user_id])
DirectMessage(id=3007629312312312312312300374016, user_id=None, thread_id=340282366812313212334410641298762, timestamp=datetime.datetime(2021, 8, 31, 19, 45, 20, 708276, tzinfo=datetime.timezone.utc), item_type=None, is_shh_mode=None, reactions=None, text=None, animated_media=None, media=None, media_share=None, reel_share=None, story_share=None, felix_share=None, clip=None, placeholder=None)

>>> cl.direct_media_share(media.pk, thread_ids=[thread.id])
DirectMessage(id=3007629312312312312312300374016, user_id=None, thread_id=340282366812313212334410641298762, timestamp=datetime.datetime(2021, 8, 31, 19, 45, 20, 708276, tzinfo=datetime.timezone.utc), item_type=None, is_shh_mode=None, reactions=None, text=None, animated_media=None, media=None, media_share=None, reel_share=None, story_share=None, felix_share=None, clip=None, placeholder=None)

>>> cl.direct_story_share(media.pk, user_ids=[cl.user_id])
DirectMessage(id=30076291231321231369939116032, user_id=None, thread_id=340282312312312334410641298762, timestamp=datetime.datetime(2021, 8, 31, 19, 48, 12, 217677, tzinfo=datetime.timezone.utc), item_type=None, is_shh_mode=None, reactions=None, text=None, animated_media=None, media=None, media_share=None, reel_share=None, story_share=None, felix_share=None, clip=None, placeholder=None)

>>> cl.direct_story_share(media.pk, thread_ids=[thread.id])
DirectMessage(id=30076291231231230352896, user_id=None, thread_id=3402812312312310641298762, timestamp=datetime.datetime(2021, 8, 31, 19, 48, 38, 482706, tzinfo=datetime.timezone.utc), item_type=None, is_shh_mode=None, reactions=None, text=None, animated_media=None, media=None, media_share=None, reel_share=None, story_share=None, felix_share=None, clip=None, placeholder=None)

>>> cl.direct_message_delete(thread.id, message.pk)
True

>>> cl.direct_message_unsend(thread.id, message.id)
True

>>> photo_path = cl.photo_download(cl.media_pk_from_url('https://www.instagram.com/p/BgqFyjqloOr/'))
>>> cl.direct_send_photo(photo_path, user_ids=[cl.user_id])  # or
>>> cl.direct_send_photo(photo_path, thread_ids=[thread.id])
DirectMessage(id=300775273512312312312321568, user_id=None, thread_id=34028236123123123123128762, timestamp=datetime.datetime(2021, 9, 1, 14, 20, 24, 949673, tzinfo=datetime.timezone.utc), item_type=None, is_shh_mode=None, reactions=None, text=None, animated_media=None, media=None, media_share=None, reel_share=None, story_share=None, felix_share=None, clip=None, placeholder=None)

>>> video_path = cl.video_download(cl.media_pk_from_url('https://www.instagram.com/p/B3rFQPblq40/'))
>>> cl.direct_send_video(video_path, user_ids=[cl.user_id])  # or
>>> cl.direct_send_video(video_path, thread_ids=[thread.id])

>>> # Voice/audio DM. Audio MUST be AAC in an MP4 container (.m4a).
>>> # Convert via ffmpeg first if needed:
>>> #   ffmpeg -i input.wav -c:a aac -b:a 64k -ac 1 -ar 44100 voice.m4a
>>> cl.direct_send_voice("voice.m4a", thread_ids=[thread.id])
Analyzing video file "/.../example_2155839952940084788.mp4"
DirectMessage(id=300775489123123123123664, user_id=None, thread_id=34012312312312312398762, timestamp=datetime.datetime(2021, 9, 1, 14, 39, 56, 959454, tzinfo=datetime.timezone.utc), item_type=None, is_shh_mode=None, reactions=None, text=None, animated_media=None, media=None, media_share=None, reel_share=None, story_share=None, felix_share=None, clip=None, placeholder=None)

>>> cl.video_upload_to_direct(video_path, thread_ids=[thread.id])
Analyzing video file "/.../example_2155839952940084788.mp4"
Generating thumbnail "/.../example_2155839952940084788.mp4.jpg"...
DirectMessage(id=3007123123123123664, user_id=None, thread_id=3401212312312312398762, timestamp=datetime.datetime(2021, 9, 1, 14, 39, 56, 959454, tzinfo=datetime.timezone.utc), item_type=None, is_shh_mode=None, reactions=None, text=None, animated_media=None, media=None, media_share=None, reel_share=None, story_share=None, felix_share=None, clip=None, placeholder=None)

>>> cl.direct_thread_mark_unread(340282366841710301949128122292511813703)
True

>>> cl.direct_thread_mute(340282366841710301949128122292511813703)
True

>>> cl.direct_thread_mute_video_call(340282366841710301949128122292511813703)
True

>>> cl.direct_thread_unmute_video_call(340282366841710301949128122292511813703)
True

>>> cl.direct_thread_unmute(340282366841710301949128122292511813703)
True

```



---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/insight.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Insights
Get business/professional account statistics. Common arguments:
  * `post_type` - Media type: “ALL”, “CAROUSEL_V2”, “IMAGE”, “SHOPPING”, “VIDEO”.
  * `time_frame` - Time frame for media publishing date: “ONE_WEEK”, “ONE_MONTH”, “THREE_MONTHS”, “SIX_MONTHS”, “ONE_YEAR”, “TWO_YEARS”.
  * `data_ordering` - Data ordering in instagram response: “REACH_COUNT”, “LIKE_COUNT”, “FOLLOW”, “SHARE_COUNT”, “BIO_LINK_CLICK”, “COMMENT_COUNT”, “IMPRESSION_COUNT”, “PROFILE_VIEW”, “VIDEO_VIEW_COUNT”, “SAVE_COUNT”.


These arguments are exposed as `POST_TYPE`, `TIME_FRAME`, and `DATA_ORDERING` Literal aliases.  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| insights_media_feed_all(post_type: POST_TYPE = “ALL”, time_frame: TIME_FRAME = “TWO_YEARS”, data_ordering: DATA_ORDERING = “REACH_COUNT”, count: int = 0, sleep: int = 2)  | List[Dict]  | Return feed media edges with insight stats and pagination  |  
| insights_account()  | Dict  | Get account-level insights (activity, audience, content tabs)  |  
| insights_media(media_pk: int)  | Dict  | Get insights for a single media object  |  
Example:

```
from instagrapi import Client

cl = Client()
cl.login(USERNAME, PASSWORD)

cl.insights_media_feed_all("VIDEO", "ONE_WEEK", "LIKE_COUNT", 42)
cl.insights_account()

media_pk = cl.media_pk_from_url('https://www.instagram.com/p/CP5h-I1FuPr/')
cl.insights_media(media_pk)

```

Notes:
  * These methods require an authenticated business/professional account. Personal accounts can raise `UserError`.
  * `insights_media_feed_all()` paginates internally and sleeps between pages; reduce `count` if you only need a small sample.
  * `insights_media()` raises `MediaError` when Instagram does not return insight data for the requested media.
  * If Instagram returns media metadata without `inline_insights_node`, `insights_media()` raises `MediaError` instead of returning partial counts with null insight metrics.




---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/track.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Track
Viewing and downloading tracks  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| track_info_by_canonical_id(music_canonical_id: str)  | Track  | Get track by `music_canonical_id`  |  
| track_info_by_id(track_id: str, max_id: str = “”)  | dict  | Get raw track payload by internal Instagram track ID  |  
| track_stream_info_by_id(track_id: str, max_id: str = “”)  | dict  | Streamed clips-pivot page (`clips/stream_clips_pivot_page/`) — clips using this audio + audio-asset metadata, the surface IG’s app uses to render the “Audio” page  |  
| track_download_by_url(url: str, filename: str = “”, folder: Path = “”)  | Path  | Download track by URL  |  
| search_music(query: str)  | List[Track]  | Search music and return track objects  |  
| music_in_feed_audio_browser(browse_session_id: str = None)  | dict  | Browse music candidates for feed photo and carousel uploads  |  
| music_trending(product: MUSIC_PRODUCT = “feed_post”)  | dict  | Browse trending music candidates  |  
| music_top_trends(product: MUSIC_PRODUCT = “music_in_feed”, page_size: int = 15)  | dict  | Browse top trending music candidates  |  
| music_search_v2(query: str, product: MUSIC_PRODUCT = “music_in_feed”, from_typeahead: bool = False, search_session_id: str = None, browse_session_id: str = None)  | dict  | Search music through the current app endpoint  |  
| music_keyword_search(query: str, product: MUSIC_PRODUCT = “music_in_feed”, num_keywords: int = 3, search_session_id: str = “”, browse_session_id: str = None)  | dict  | Search music keyword suggestions  |  
| music_clips_audio_browser(product: MUSIC_PRODUCT = “story_camera_clips_v2”, browse_session_id: str = None)  | dict  | Browse music candidates for the Reels/Clips camera  |  
| music_verify_original_audio_title(original_audio_name: str)  | bool  | Validate an original audio title for Reels publishing  |  
| music_bookmark(original_audio_id: str, surface_requested_from: str = “audio_aggregation_page”)  | bool  | Bookmark an original audio track  |  
| music_bookmarked(max_id: str = “”)  | dict  | Retrieve bookmarked music tracks  |  
### Example:

```
>>> from instagrapi import Client
>>> cl = Client()
>>> cl.login(USERNAME, PASSWORD)

>>> [media.clips_metadata['music_canonical_id'] for media in cl.reels(amount=10)]

['18159860503036324',
 '18245182426110798',
 '18156435169051995',
 '18274086877034385',
 '18243482860109137',
 '18244791958105000',
 '18310451203035205',
 '18293984647065921',
 '18154598032011335',
 '18301950994013617']

>>> cl.track_info_by_canonical_id(18159860503036324).dict()
{
'id': '2398788493765573',
'title': 'A Little Bit Goes a Long Way',
'subtitle': '',
'display_artist': 'Yheti',
'audio_cluster_id': 1054108181594434,
'artist_id': None,
'cover_artwork_uri': None,
'cover_artwork_thumbnail_uri': None,
'progressive_download_url': None,
'fast_start_progressive_download_url': None,
'reactive_audio_download_url': None,
'highlight_start_times_in_ms': [38500],
'is_explicit': False,
'dash_manifest': '<?xml version="1.0" encoding="UTF-8"?>\n<!--Generated with https://github.com/google/shaka-packager version v1.6.0-release-->\n<MPD xmlns="urn:mpeg:dash:schema:mpd:2011" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:cenc="urn:mpeg:cenc:2013" xsi:schemaLocation="urn:mpeg:dash:schema:mpd:2011 DASH-MPD.xsd" profiles="urn:mpeg:dash:profile:isoff-on-demand:2011" minBufferTime="PT2S" type="static" mediaPresentationDuration="PT182.137S">\n  <Period id="0">\n    <AdaptationSet id="0" contentType="audio" subsegmentAlignment="true">\n      <Representation id="0" bandwidth="130017" codecs="mp4a.40.2" mimeType="audio/mp4" audioSamplingRate="48000">\n        <AudioChannelConfiguration schemeIdUri="urn:mpeg:dash:23003:3:audio_channel_configuration:2011" value="2"/>\n        <BaseURL>https://scontent-cph2-1.xx.fbcdn.net/v/t39.12897-6/84846439_2484536748531420_3971102873273499648_n.m4a?_nc_cat=101&amp;ccb=1-7&amp;_nc_sid=02c1ff&amp;_nc_ohc=N6k7lDt_6TAAX_yKEoV&amp;_nc_ad=z-m&amp;_nc_cid=0&amp;_nc_ht=scontent-cph2-1.xx&amp;oh=00_AT9Cly5G-kzGxRceunBi8NUl5eFLEqwlMEJbWnxykUTO0Q&amp;oe=62DF3A6E</BaseURL>\n        <SegmentBase indexRange="741-1864" timescale="48000">\n          <Initialization range="0-740"/>\n        </SegmentBase>\n      </Representation>\n    </AdaptationSet>\n  </Period>\n</MPD>\n',
'uri': HttpUrl('https://scontent-cph2-1.xx.fbcdn.net/v/t39.12897-6/84846439_2484536748531420_3971102873273499648_n.m4a?_nc_cat=101&ccb=1-7&_nc_sid=02c1ff&_nc_ohc=N6k7lDt_6TAAX_yKEoV&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent-cph2-1.xx&oh=00_AT9Cly5G-kzGxRceunBi8NUl5eFLEqwlMEJbWnxykUTO0Q&oe=62DF3A6E', scheme='https', host='scontent-cph2-1.xx.fbcdn.net', tld='net', host_type='domain', port='443', path='/v/t39.12897-6/84846439_2484536748531420_3971102873273499648_n.m4a', query='_nc_cat=101&ccb=1-7&_nc_sid=02c1ff&_nc_ohc=N6k7lDt_6TAAX_yKEoV&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent-cph2-1.xx&oh=00_AT9Cly5G-kzGxRceunBi8NUl5eFLEqwlMEJbWnxykUTO0Q&oe=62DF3A6E'),
'has_lyrics': False,
'audio_asset_id': 2398788493765573,
'duration_in_ms': 182094,
'dark_message': None,
'allows_saving': True,
'territory_validity_periods': {}
}

>>> track_uri = cl.track_info_by_canonical_id(18159860503036324).uri
HttpUrl('https://scontent-cph2-1.xx.fbcdn.net/v/t39.12897-6/84846439_2484536748531420_3971102873273499648_n.m4a?_nc_cat=101&ccb=1-7&_nc_sid=02c1ff&_nc_ohc=N6k7lDt_6TAAX_yKEoV&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent-cph2-1.xx&oh=00_AT9Cly5G-kzGxRceunBi8NUl5eFLEqwlMEJbWnxykUTO0Q&oe=62DF3A6E', scheme='https', host='scontent-cph2-1.xx.fbcdn.net', tld='net', host_type='domain', port='443', path='/v/t39.12897-6/84846439_2484536748531420_3971102873273499648_n.m4a', query='_nc_cat=101&ccb=1-7&_nc_sid=02c1ff&_nc_ohc=N6k7lDt_6TAAX_yKEoV&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent-cph2-1.xx&oh=00_AT9Cly5G-kzGxRceunBi8NUl5eFLEqwlMEJbWnxykUTO0Q&oe=62DF3A6E')

>>> cl.track_download_by_url(track_uri, folder="/tmp")
PosixPath('/tmp/84846439_2484536748531420_3971102873273499648_n.m4a')

>>> cl.search_music("love")[0].dict()
{
'id': '354372829354341',
'title': 'Love Your Voice',
'subtitle': '',
'display_artist': 'JONY',
'audio_cluster_id': 410742646320351,
'artist_id': None,
'cover_artwork_uri': HttpUrl('https://cdn.fbsbx.com/v/t65.14500-21/191897578_1074647849725858_3973554110966662866_n.jpg?stp=cp0_dst-jpg_e15_p526x296_q65&_nc_cat=1&ccb=1-7&_nc_sid=cbead8&_nc_ohc=ugygksMclf4AX_u7L7g&_nc_ht=cdn.fbsbx.com&oh=00_AT89FBXl6h7Q6zytlI5cA4UIG_zQkK_DsOqyUqyXk1zyIg&oe=62DAEA82', scheme='https', host='cdn.fbsbx.com', tld='com', host_type='domain', port='443', path='/v/t65.14500-21/191897578_1074647849725858_3973554110966662866_n.jpg', query='stp=cp0_dst-jpg_e15_p526x296_q65&_nc_cat=1&ccb=1-7&_nc_sid=cbead8&_nc_ohc=ugygksMclf4AX_u7L7g&_nc_ht=cdn.fbsbx.com&oh=00_AT89FBXl6h7Q6zytlI5cA4UIG_zQkK_DsOqyUqyXk1zyIg&oe=62DAEA82'),
'cover_artwork_thumbnail_uri': HttpUrl('https://cdn.fbsbx.com/v/t65.14500-21/191897578_1074647849725858_3973554110966662866_n.jpg?stp=cp0_dst-jpg_e15_q65_s168x128&_nc_cat=1&ccb=1-7&_nc_sid=cbead8&_nc_ohc=ugygksMclf4AX_u7L7g&_nc_ht=cdn.fbsbx.com&oh=00_AT81eLXWBA5EaM20EhaMldwlyzKG1X1zA_nYNkYWf6c5cg&oe=62DAEA82', scheme='https', host='cdn.fbsbx.com', tld='com', host_type='domain', port='443', path='/v/t65.14500-21/191897578_1074647849725858_3973554110966662866_n.jpg', query='stp=cp0_dst-jpg_e15_q65_s168x128&_nc_cat=1&ccb=1-7&_nc_sid=cbead8&_nc_ohc=ugygksMclf4AX_u7L7g&_nc_ht=cdn.fbsbx.com&oh=00_AT81eLXWBA5EaM20EhaMldwlyzKG1X1zA_nYNkYWf6c5cg&oe=62DAEA82'),
'progressive_download_url': HttpUrl('https://scontent-cph2-1.xx.fbcdn.net/v/t39.12897-6/199073207_321615622853093_2366400633227710754_n.m4a?_nc_cat=1&ccb=1-7&_nc_sid=02c1ff&_nc_ohc=UxUNJHpsoy4AX-eA1Bm&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent-cph2-1.xx&oh=00_AT_IpjsOwgCikt0wNx1nS7FzEJE-1pKkzNZSXIpKCzkZhg&oe=62DE2CA8', scheme='https', host='scontent-cph2-1.xx.fbcdn.net', tld='net', host_type='domain', port='443', path='/v/t39.12897-6/199073207_321615622853093_2366400633227710754_n.m4a', query='_nc_cat=1&ccb=1-7&_nc_sid=02c1ff&_nc_ohc=UxUNJHpsoy4AX-eA1Bm&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent-cph2-1.xx&oh=00_AT_IpjsOwgCikt0wNx1nS7FzEJE-1pKkzNZSXIpKCzkZhg&oe=62DE2CA8'),
'fast_start_progressive_download_url': HttpUrl('https://scontent-cph2-1.xx.fbcdn.net/v/t39.12897-6/199073207_321615622853093_2366400633227710754_n.m4a?_nc_cat=1&ccb=1-7&_nc_sid=02c1ff&_nc_ohc=UxUNJHpsoy4AX-eA1Bm&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent-cph2-1.xx&oh=00_AT_IpjsOwgCikt0wNx1nS7FzEJE-1pKkzNZSXIpKCzkZhg&oe=62DE2CA8', scheme='https', host='scontent-cph2-1.xx.fbcdn.net', tld='net', host_type='domain', port='443', path='/v/t39.12897-6/199073207_321615622853093_2366400633227710754_n.m4a', query='_nc_cat=1&ccb=1-7&_nc_sid=02c1ff&_nc_ohc=UxUNJHpsoy4AX-eA1Bm&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent-cph2-1.xx&oh=00_AT_IpjsOwgCikt0wNx1nS7FzEJE-1pKkzNZSXIpKCzkZhg&oe=62DE2CA8'),
'reactive_audio_download_url': None,
'highlight_start_times_in_ms': [20000, 35500, 86500],
'is_explicit': False,
'dash_manifest': '<?xml version="1.0" encoding="UTF-8"?>\n<!--Generated with https://github.com/google/shaka-packager version v1.6.0-release-->\n<MPD xmlns="urn:mpeg:dash:schema:mpd:2011" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:cenc="urn:mpeg:cenc:2013" xsi:schemaLocation="urn:mpeg:dash:schema:mpd:2011 DASH-MPD.xsd" profiles="urn:mpeg:dash:profile:isoff-on-demand:2011" minBufferTime="PT2S" type="static" mediaPresentationDuration="PT150.372S">\n  <Period id="0">\n    <AdaptationSet id="0" contentType="audio" subsegmentAlignment="true">\n      <Representation id="0" bandwidth="130029" codecs="mp4a.40.2" mimeType="audio/mp4" audioSamplingRate="48000">\n        <AudioChannelConfiguration schemeIdUri="urn:mpeg:dash:23003:3:audio_channel_configuration:2011" value="2"/>\n        <BaseURL>https://scontent-cph2-1.xx.fbcdn.net/v/t39.12897-6/198992520_981513595929106_5731656525090532090_n.m4a?_nc_cat=1&amp;ccb=1-7&amp;_nc_sid=02c1ff&amp;_nc_ohc=ZZ6zJXs2dkAAX-B0LDK&amp;_nc_ad=z-m&amp;_nc_cid=0&amp;_nc_ht=scontent-cph2-1.xx&amp;oh=00_AT8j4tjiUNSVWv9qbkg9Ro9MzAGeW9_wXU4e0ncV0MhdZQ&amp;oe=62DECA6E</BaseURL>\n        <SegmentBase indexRange="741-1672" timescale="48000">\n          <Initialization range="0-740"/>\n        </SegmentBase>\n      </Representation>\n    </AdaptationSet>\n  </Period>\n</MPD>\n',
'uri': HttpUrl('https://scontent-cph2-1.xx.fbcdn.net/v/t39.12897-6/198992520_981513595929106_5731656525090532090_n.m4a?_nc_cat=1&ccb=1-7&_nc_sid=02c1ff&_nc_ohc=ZZ6zJXs2dkAAX-B0LDK&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent-cph2-1.xx&oh=00_AT8j4tjiUNSVWv9qbkg9Ro9MzAGeW9_wXU4e0ncV0MhdZQ&oe=62DECA6E', scheme='https', host='scontent-cph2-1.xx.fbcdn.net', tld='net', host_type='domain', port='443', path='/v/t39.12897-6/198992520_981513595929106_5731656525090532090_n.m4a', query='_nc_cat=1&ccb=1-7&_nc_sid=02c1ff&_nc_ohc=ZZ6zJXs2dkAAX-B0LDK&_nc_ad=z-m&_nc_cid=0&_nc_ht=scontent-cph2-1.xx&oh=00_AT8j4tjiUNSVWv9qbkg9Ro9MzAGeW9_wXU4e0ncV0MhdZQ&oe=62DECA6E'),
'has_lyrics': True,
'audio_asset_id': 354372829354341,
'duration_in_ms': 150329,
'dark_message': None,
'allows_saving': True,
'territory_validity_periods': {}
}


```

Notes:
  * `track_info_by_canonical_id()` is the high-level typed path and usually the one you want for reels/clips music metadata.
  * `track_info_by_id()` returns the lower-level raw response shape, which is useful for debugging or when you already have an Instagram track ID.
  * The `music_*` helpers expose raw app music surfaces so callers can inspect rollout-specific fields and reuse IDs in upload flows.




---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/best-practices.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Best Practices
This is a best practices guide around using the Instagram API so that you don’t get rate limited or banned.
## Use a Stable Proxy Identity
If you’re getting errors like this:
  * “The username you entered doesn’t appear to belong to an account. Please check your username and try again.”
  * `BadPassword` even though the same password works in another context


Or you notice that Instagram is sending suspicious login emails, review the network identity for that account. Instagram may be rate limiting the IP, distrusting the login location, or challenging the account because the device/session and IP history do not look consistent.
For production automation, the safest baseline is one account per stable proxy/IP. Reusing the same country, city, ASN/mobile carrier, device settings, and saved session is less suspicious than using a different IP address every time you make a request.
Avoid treating any proxy type as a universal fix. Residential, mobile, ISP, and datacenter proxies can all fail if they are abused, shared too widely, or rotated aggressively. The exact provider matters less than consistency, reputation, and whether your request pattern fits the account history.
Here is the shape of using a proxy with `instagrapi`:

```
from instagrapi import Client

cl = Client()
before_ip = cl._send_public_request("https://api.ipify.org/")
cl.set_proxy("http://username:password@proxy.example.com:8080")
after_ip = cl._send_public_request("https://api.ipify.org/")

print(f"Before: {before_ip}")
print(f"After: {after_ip}")

```

Notes:
  * Keep one stable proxy/IP per account whenever possible.
  * Avoid rapidly rotating countries, cities, or carrier/mobile fingerprints for the same account.
  * Prefer proxy hostnames that resolve through the proxy when using SOCKS, for example `socks5h://...`.
  * Match `set_country(...)`, `set_locale(...)`, device settings, and saved sessions to the account’s normal environment.
  * Do not rotate proxy identity in the middle of a challenge, password reset, or relogin loop.
  * Treat a shared IP pool as higher risk; reduce account count and request volume if you cannot dedicate an IP per account.


If `BadPassword` happens with a known-good password, use the [`BadPassword` troubleshooting guide](https://instagrapi.com/guides/errors/bad-password/) to separate real credential problems from Instagram trust/risk rejections.
## Warm Accounts Gradually
New, restored, or previously challenged accounts should not immediately run high-volume actions.
Practical warmup rules:
  * Start with read-heavy authenticated actions before write-heavy actions.
  * Avoid repeated fresh password logins. Save settings and reuse the same device/session identity.
  * Keep early write actions low and human-like: fewer follows, likes, comments, DMs, uploads, and profile edits.
  * Increase volume slowly over days, not minutes.
  * Stop and inspect the account manually after repeated challenges, forced password changes, or feedback blocks.
  * Do not run the same workload across many accounts from the same fresh proxy pool at once.


## Add Delays
It’s recommended you try to mimic the behavior of a real user. This means you should add delays between requests. The delays should be random and not too long.
The following is a good example of how to add delays between requests.

```
from instagrapi import Client

cl = Client()

# adds a random delay between 1 and 3 seconds after each request
cl.delay_range = [1, 3]

```

Delays are only one layer. For larger jobs, also limit concurrency per account, per proxy, and per action type. A single account doing many parallel actions is more suspicious than the same work spread out with clear cooldowns.
## Handle Rate Limits and Anti-Abuse Responses Explicitly
Instagram uses several different responses for throttling, suspicious behavior, or temporary restrictions. Treat them differently instead of retrying every error the same way.
###  `ClientThrottledError` / HTTP 429
This usually means the current IP or request pattern is too aggressive for that path right now. Public web endpoints can hit this independently from private mobile endpoints; a `429` on a public GraphQL/web path does not necessarily mean the logged-in mobile session is broken.
Recommended response:
  * stop the current burst of requests
  * back off before retrying
  * reduce concurrency for that account
  * prefer authenticated/private helpers when a public web helper repeatedly fails
  * try the optional `public_transport="curl"` path only for public web endpoints, and treat it as a transport option, not a rate-limit bypass
  * if the same account keeps hitting `429`, pause it or move it to a cleaner proxy/IP


### `PleaseWaitFewMinutes`
This is usually more serious than a single `429`. Instagram is telling you to slow down for that account, device, or IP combination.
Recommended response:
  * stop write actions for that account for a while
  * do not spam retries in a tight loop
  * keep the same device settings and only retry later
  * if it keeps happening, review proxy quality and account warmup


### `FeedbackRequired`
This often means an action was blocked or the account is temporarily restricted.
Recommended response:
  * inspect `client.last_json.get("feedback_message")`
  * stop repeating the same action immediately
  * freeze the account or action type for a cooldown window
  * if you automate multiple action types, disable the offending one first


### `LoginRequired`
This usually means the current private session is no longer valid.
Recommended response:
  * relogin with the same saved device/session state
  * validate the session with a lightweight authenticated call
  * if relogin keeps failing, stop and inspect the account manually instead of forcing repeated fresh logins


### `ChallengeRequired`
This means Instagram wants an additional verification step. Some flows can be automated, but newer challenge paths may still require manual review.
Recommended response:
  * call `challenge_resolve(...)` only if you have working handlers for codes/password changes
  * if you hit `/auth_platform/`, UFAC web flows, or Bloks redirect checkpoints, expect manual handling in the official Instagram app or web flow
  * do not rotate identity aggressively in the middle of a challenge


### Practical Rules
  * Separate read-heavy jobs from write-heavy jobs whenever possible.
  * Use one stable proxy/IP per account instead of hopping between locations.
  * Persist sessions and device identifiers; avoid password login from scratch on every run.
  * Freeze accounts that hit repeated anti-abuse responses instead of hammering them harder.
  * Track errors per account, per proxy, and per action type so you can see which variable is actually causing trouble.
  * Retry transport errors differently from account restrictions. A timeout may be retried; a challenge or feedback block needs cooldown and investigation.


## Automation Warnings and Suspicious Login Screens
Instagram can show in-app warning screens or suspicious-login prompts even when the account is not fully challenged. These are usually trust signals tied to the account, device/session, proxy/IP history, and action pattern. They are not reliable to “bypass” generically from the library.
Recommended response:
  * stop the affected workflow and inspect the account in the official app
  * keep the same saved settings, device identifiers, locale, country, and proxy while investigating
  * avoid repeated fresh password logins, aggressive proxy rotation, or replaying the same failed action
  * capture sanitized diagnostics: method name, endpoint if visible, exception class, `client.last_json`, status code, and whether the same account works in the official app
  * open an issue only when the same payload is reproducible; without `last_json`, the project cannot safely add a named exception


## Read-Only Monitoring Workloads
For small jobs that only check whether selected users posted new media or stories, keep the workflow boring:
  * reuse one saved session with `dump_settings()` / `load_settings()`
  * poll a small target set with a moderate interval, for example several minutes rather than seconds
  * store the last seen media/story ids locally and compare new responses against that state
  * keep this account separate from write-heavy actions such as follows, likes, comments, uploads, and Direct messages
  * expect public/web paths to be opportunistic; reliable private-account story access requires that the logged-in account has permission to view the target


See [`examples/monitor_user_content.py`](https://github.com/subzeroid/instagrapi/blob/master/examples/monitor_user_content.py) for a minimal state-file based polling example.
## Common Anti-Patterns
These patterns often create support issues that are not library bugs:
  * logging in with username/password on every script run
  * switching proxies after every request
  * sharing one noisy IP across many unrelated accounts
  * retrying `429`, `PleaseWaitFewMinutes`, `FeedbackRequired`, or challenges in a tight loop
  * mixing browser `sessionid` reuse with frequent private API password logins
  * treating a browser/web `sessionid` as equivalent to a stable private mobile session after Instagram returns `login_required`
  * changing password, email, phone, profile, and posting behavior from a fresh proxy at the same time
  * running write-heavy automation immediately after account creation or recovery
  * ignoring `client.last_json` and treating every exception as a generic transient failure


## Separate Library Bugs from Operational Blocks
A library bug usually reproduces consistently for the same endpoint and payload, especially across accounts with healthy sessions. Useful reports include the method called, sanitized request/response data, stack trace, dependency versions, and whether the same account works in the official app.
An operational block is usually account, proxy, session, or action-pattern specific. Signs include `BadPassword` with a known-good password, `429`, `PleaseWaitFewMinutes`, `FeedbackRequired`, suspicious login emails, challenges, forced password changes, or behavior that disappears after cooldown, cleaner proxy identity, or manual app verification.
When reporting an issue, include enough context to distinguish these cases. Remove cookies, session IDs, tokens, passwords, phone numbers, emails, and private user data before sharing logs.
## Use Sessions
If you call `.login()` from scratch on every run, Instagram sees repeated fresh logins. That is much more suspicious than reusing a stable device session.
The normal pattern is:
  1. Login once
  2. Save settings with `.dump_settings()`
  3. Load them later with `.load_settings()` or `.set_settings()`
  4. Reuse the same device/session identifiers across runs


The first time you run your script

```
from instagrapi import Client

cl = Client()
cl.login(USERNAME, PASSWORD)
cl.dump_settings("session.json")

```

And on the next run:

```
from instagrapi import Client

cl = Client()
cl.load_settings("session.json")
cl.login(USERNAME, PASSWORD)
cl.get_timeline_feed()  # optional session validity check

```

You’ll notice we do a call to `cl.get_timeline_feed()` to check if the session is valid. If it’s not valid, you’ll get an exception.
If you want more explicit control over the loaded settings object:

```
from instagrapi import Client

cl = Client()
session = cl.load_settings("session.json")
cl.set_settings(session)
cl.login(USERNAME, PASSWORD)

```

Putting this all together, you can write a reusable login helper like this:

```
from instagrapi import Client
from instagrapi.exceptions import LoginRequired
import logging

logger = logging.getLogger()

def login_user():
    """
    Attempts to login to Instagram using either the provided session information
    or the provided username and password.
    """

    cl = Client()
    session = cl.load_settings("session.json")

    login_via_session = False
    login_via_pw = False

    if session:
        try:
            cl.set_settings(session)
            cl.login(USERNAME, PASSWORD)

            # check if session is valid
            try:
                cl.get_timeline_feed()
            except LoginRequired:
                logger.info("Session is invalid, need to login via username and password")

                old_session = cl.get_settings()

                # use the same device uuids across logins
                cl.set_settings({})
                cl.set_uuids(old_session["uuids"])

                cl.login(USERNAME, PASSWORD)
            login_via_session = True
        except Exception as e:
            logger.info("Couldn't login user using session information: %s" % e)

    if not login_via_session:
        try:
            logger.info("Attempting to login via username and password. username: %s" % USERNAME)
            if cl.login(USERNAME, PASSWORD):
                login_via_pw = True
        except Exception as e:
            logger.info("Couldn't login user using username and password: %s" % e)

    if not login_via_pw and not login_via_session:
        raise Exception("Couldn't login user with either password or session")

    return cl

```

## Prefer Read/Write Separation
If your workload is mostly data retrieval, keep that path separate from account-changing actions.
In practice:
  * Reading data is usually easier to scale and safer to isolate.
  * Writing actions such as posting, following, editing profile data, or sending DMs need much stricter operational hygiene.
  * When possible, use official Instagram APIs for account-changing actions and keep private API automation focused on the gaps.




---


# Source: https://subzeroid.github.io/instagrapi/development-guide.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Development Guide
Welcome! Thank you for wanting to make the project better. This section provides an overview on how repository structure and how to work with the code base.
Before you dive into this, it is best to read:
  * The [Contributing guide](https://github.com/subzeroid/instagrapi/blob/master/CONTRIBUTING.md)


## Local Environment
Use a virtual environment and install the project from `pyproject.toml` with test extras:

```
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -e ".[test]"
pre-commit install

```

This installs the library, runtime dependencies, test tools, lint tools, and documentation tooling in one environment.
If you use [uv](https://docs.astral.sh/uv/), keep the same `pyproject.toml` source of truth:

```
uv venv
source .venv/bin/activate
uv pip install -e ".[test]"
pre-commit install

```

If you prefer to keep `pre-commit` outside the project environment, install it with [pipx](https://pipx.pypa.io/):

```
pipx install pre-commit
pre-commit install

```

## Debugging
Python’s built-in [pdb](https://docs.python.org/3/library/pdb.html) debugger is enough for most local debugging. You can create a breakpoint anywhere in the code:

```
def my_function():
    breakpoint()
    ...

```

When the code reaches the breakpoint, it will drop into an interactive debugger.
See the documentation on [pdb](https://docs.python.org/3/library/pdb.html) for more information.
## Testing
You’ll be unable to merge code unless linting and tests pass. The main local checks are:

```
pytest -sv tests/regression
ruff check .
ruff format --check .
bandit -c pyproject.toml -r instagrapi
mkdocs build --strict

```

To apply automatic lint and formatting fixes locally:

```
ruff check . --fix
ruff format .

```

Before committing, run the pre-commit hooks against changed files or the whole tree:

```
pre-commit run --all-files

```

Generally we should endeavor to write tests for every feature. Every new feature branch should increase the test coverage rather than decreasing it.
We use [pytest](https://docs.pytest.org/en/latest/) as our testing framework. Regression tests live in `tests/regression/`; live-account tests live in `tests/live/`.
#### Stages
To customize / override a specific testing stage, please read the documentation specific to that tool:
  1. [PyTest](https://docs.pytest.org/en/latest/)
  2. [Ruff](https://docs.astral.sh/ruff/)
  3. [Bandit](https://bandit.readthedocs.io/en/stable/)


### `pyproject.toml`
Setuptools is used to package the library through `pyproject.toml`.
`pyproject.toml` is the source of truth for package metadata, runtime dependencies, and test/development extras.
### Dependencies
  * `[project].dependencies` lists runtime dependencies imported by the library.
  * `[project.optional-dependencies].test` lists tools needed for tests, linting, docs, and local development.
  * Runtime dependency lower bounds should stay at the currently tested/security-patched version, with an upper bound before the next major release.
  * Android-specific pins are allowed when the mobile Python ecosystem needs an exact wheel-compatible version, for example the Termux pydantic-core wheel constraint.


Publishing is handled by the tag-based `publish.yml` workflow. Pushes and pull requests run the package workflow first; maintainers cut a version tag only after the checks are green.
## Continuous Integration Pipeline
The `Package` workflow runs Bandit, Ruff, compatibility regression tests on Python 3.10 through 3.14, and a strict docs build. Pull requests and pushes to `master` both build the docs; pushes to `master` also publish the `dev` docs with `mike`.
Live-account tests are kept in a separate manually triggered `Live Account Tests` workflow. It accepts a focused target such as `media`, `upload`, `direct`, `timeline`, `story-location`, `location`, `usertag`, `user`, or `all`, and uses the pooled `TEST_ACCOUNTS_URL` secret.
The `Publish to PyPI` workflow runs only for version tags such as `2.6.7`. It verifies the tag matches `pyproject.toml`, builds the wheel and sdist, publishes through PyPI trusted publishing, and creates the GitHub release.


---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/handle_exception.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
You can handle any exceptions using a generic handler:

```
import json
import logging

from instagrapi import Client
from instagrapi.exceptions import (
    BadPassword, ReloginAttemptExceeded, ChallengeRequired,
    SelectContactPointRecoveryForm, RecaptchaChallengeForm,
    FeedbackRequired, PleaseWaitFewMinutes, LoginRequired,
    ClientThrottledError, DirectMessageRequestsDisabled,
)
from instagrapi.utils import json_value

logger = logging.getLogger(__name__)

def handle_exception(client: Client, e: Exception):
    if isinstance(e, BadPassword):
        client.logger.exception(e)
        if client.relogin_attempt > 0:
            raise ReloginAttemptExceeded(e)
        raise e
    elif isinstance(e, LoginRequired):
        client.logger.exception(e)
        client.relogin()
        return True
    elif isinstance(e, ChallengeRequired):
        api_path = json_value(client.last_json, "challenge", "api_path")
        if api_path == "/challenge/":
            logger.warning("Generic challenge flow requires manual handling or a custom resolver")
        else:
            try:
                client.challenge_resolve(client.last_json)
            except ChallengeRequired as e:
                raise e
            except (ChallengeRequired, SelectContactPointRecoveryForm, RecaptchaChallengeForm) as e:
                raise e
        return True
    elif isinstance(e, FeedbackRequired):
        message = client.last_json.get("feedback_message", "")
        if "This action was blocked. Please try again later" in message:
            logger.warning("Action blocked by Instagram: %s", message)
        elif "We restrict certain activity to protect our community" in message:
            logger.warning("Temporary activity restriction: %s", message)
        elif "Your account has been temporarily blocked" in message:
            logger.warning("Temporary account block: %s", message)
    elif isinstance(e, ClientThrottledError):
        logger.warning("HTTP 429 from Instagram, back off and review proxy/account pressure")
    elif isinstance(e, PleaseWaitFewMinutes):
        logger.warning("Please wait before retrying: %s", e)
    elif isinstance(e, DirectMessageRequestsDisabled):
        logger.warning("Recipient does not accept new Direct message requests: %s", e)
    raise e

cl = Client()
cl.handle_exception = handle_exception
cl.login(USERNAME, PASSWORD)

```

In this way, you can centrally handle errors and not repeat handlers throughout your code. In a real application, you would usually extend this with your own proxy rotation, account freeze/backoff storage, or metrics hooks.
For `BadPassword` with a password that works elsewhere, see the [`BadPassword` troubleshooting guide](https://instagrapi.com/guides/errors/bad-password/). Instagram can return `bad_password` for risky proxy/IP/device/session states, so avoid retry loops and first compare against the official app on the same network identity.
For a practical playbook around `429`, `feedback_required`, `PleaseWaitFewMinutes`, and session/challenge handling, see [Best Practices](https://subzeroid.github.io/instagrapi/usage-guide/best-practices.html).
Full example [here](https://github.com/subzeroid/instagrapi/blob/master/examples/handle_exception.py)


---


# Source: https://subzeroid.github.io/instagrapi/exceptions.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
## Common Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| ClientError  | Exception  | Base Exception for Instagram calls  |  
| GenericRequestError  | ClientError  | Base Exception for Request (Solution: try changing your proxy)  |  
| ClientGraphqlError  | ClientError  | Exception for GraphQL calls  |  
| ClientJSONDecodeError  | ClientError  | JSON Exception  |  
| ClientConnectionError  | ClientError  | Connection error (Solution: try changing your proxy)  |  
| ClientBadRequestError  | ClientError  | HTTP 400 Exception  |  
| ClientUnauthorizedError  | ClientError  | HTTP 401 Exception  |  
| ClientForbiddenError  | ClientError  | HTTP 403 Exception  |  
| ClientNotFoundError  | ClientError  | HTTP 404 Exception  |  
| ClientThrottledError  | ClientError  | HTTP 429 Exception (Solution: try changing your proxy)  |  
| ClientRequestTimeout  | ClientError  | Request Timeout Exception  |  
| ClientIncompleteReadError  | ClientError  | Raises when response interrupted  |  
| ClientLoginRequired  | ClientError  | Raises when Instagram required Login (Solution: try changing your proxy)  |  
| ReloginAttemptExceeded  | ClientError  | Raises when all attempts exceeded  |  
| ClientErrorWithTitle  | ClientError  | Occurs when Instagram returns an unknown error with the title  |  
| ClientUnknownError  | ClientError  | Occurs when Instagram returns an unknown error  |  
| WrongCursorError  | ClientError  | Occurs when the cursor for pagination is passed in the wrong format  |  
| ClientStatusFail  | ClientError  | Occurs when Instagram returns message with status=fail with details  |  
| RelatedProfileRequired  | ClientError  | Raised by `user_related_profiles_gql` on empty results when caller has set `client.num_retry < 4` (opt-in retry signal)  |  
## Proxy Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| ProxyError  | ClientError  | Base exception for proxy  |  
| ConnectProxyError  | ProxyError  | Occurs when it is not possible to connect to your proxy  |  
| AuthRequiredProxyError  | ProxyError  | Occurs when incorrect credentials are passed to authorize your proxy  |  
| ProxyAddressIsBlocked  | PrivateError  | Happens when your proxy is blocked by Instagram, change your proxy!  |  
| SentryBlock  | PrivateError  | Raises when get message=sentry_block (most likely you were banned from instagram by ip address. Solution: try changing your proxy)  |  
| RateLimitError  | PrivateError  | Raises when get message=rate_limit_error (Solution: try changing your proxy)  |  
| PleaseWaitFewMinutes  | PrivateError  | Raises when get message=”Please wait a few minutes before you try again” (Solution: try changing your proxy)  |  
## GraphQL/Public Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| AccountSuspended  | ClientError  | Your account is suspended  |  
| TermsUnblock  | ClientError  | Your account may be blocked, you need to agree to the terms  |  
| TermsAccept  | ClientError  | Your account may be blocked, you need to agree to the terms  |  
| AboutUsError  | ClientError  | Your account may be blocked  |  
## Private Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| PrivateError  | ClientError  | Base Exception for Private calls (received from Instagram)  |  
| FeedbackRequired  | PrivateError  | Raises when get message=feedback_required  |  
| PreLoginRequired  | ClientError  | Raises when authorization is required before calling a method  |  
| LoginRequired  | PrivateError  | Raises when get message=login_required (from Instagram)  |  
| BadPassword  | PrivateError  | Raises when get message=bad_password. See [`BadPassword` troubleshooting](https://instagrapi.com/guides/errors/bad-password/) for proxy/IP/device/session trust cases where the password is correct but Instagram rejects the login context.  |  
| TwoFactorRequired  | PrivateError  | Raises when get message=two_factor_required  |  
| UnknownError  | PrivateError  | Raises when get unknown message (new message from instagram)  |  
| AccountEditError  | PrivateError  | Raises when `accounts/edit_profile/` returns an account edit failure  |  
| AccountContactPointRequired  | AccountEditError  | Raises when profile editing requires an email or confirmed phone number  |  
| BadCredentials  | PrivateError  | The login and password pair for your account have not been passed  |  
| IsRegulatedC18Error  | ClientBadRequestError  | The user is limited to 18+  |  
## Challenge Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| ChallengeError  | PrivateError  | Base Challenge Exception (received from Instagram)  |  
| ChallengeRedirection  | ChallengeError  | Raises when get type=CHALLENGE_REDIRECTION  |  
| ChallengeRequired  | ChallengeError  | Raises when Instagram requires additional verification; raw `message=challenge_required` responses get a payload-specific recovery message  |  
| ChallengeSelfieCaptcha  | ChallengeError  | Raises when get step=selfie_captcha  |  
| ChallengeUnknownStep  | ChallengeError  | Occurs when challenge is unknown  |  
| SelectContactPointRecoveryForm  | ChallengeError  | Raises when get challengeType=SelectContactPointRecoveryForm  |  
| RecaptchaChallengeForm  | ChallengeError  | Raises when get challengeType=RecaptchaChallengeForm  |  
| SubmitPhoneNumberForm  | ChallengeError  | Raises when get challengeType=SubmitPhoneNumberForm  |  
| LegacyForceSetNewPasswordForm  | ChallengeError  | Raises when get challengeType=LegacyForceSetNewPasswordForm  |  
| ConsentRequired  | PrivateError  | Raises when get message=consent_required  |  
| GeoBlockRequired  | PrivateError  | Raises when get message=geoblock_required  |  
| CheckpointRequired  | PrivateError  | Raises when get message=checkpoint_required  |  
## Media Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| MediaError  | PrivateError  | Base Media Exception (received from Instagram)  |  
| MediaNotFound  | MediaError  | Raises when user unavailable  |  
| InvalidTargetUser  | PrivateError  | Occurs when the selected user cannot be mentioned (does not exist, has been deleted or is closed by privacy settings)  |  
| InvalidMediaId  | PrivateError  | Occurs when the selected media does not exists  |  
| MediaUnavailable  | PrivateError  | Occurs when the selected media is no longer available  |  
## User Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| UserError  | PrivateError  | Base User Exception (received from Instagram)  |  
| UserNotFound  | UserError  | Raises when user unavailable  |  
| PrivateAccount  | PrivateError  | The target user is closed by privacy settings  |  
## Account Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| ResetPasswordError  | ClientError  | Raises when password is not reset  |  
| UnsupportedError  | ClientError  | Raises when option is supported  |  
| UnsupportedSettingValue  | UnsupportedError  | Raises when account setting value is not supported  |  
## Collection Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| CollectionError  | PrivateError  | Base Collection Exception (received from Instagram)  |  
| CollectionNotFound  | CollectionError  | Raises when collection unavailable  |  
## Direct Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| DirectError  | PrivateError  | Base Direct Exception  |  
| DirectThreadNotFound  | DirectError  | Raises when thread not found  |  
| DirectMessageNotFound  | DirectError  | Raises when message in thread not found  |  
| DirectMessageRequestsDisabled  | DirectError  | Raises when recipient privacy settings reject a new Direct message request  |  
## Photo Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| PhotoNotDownload  | PrivateError  | Raises when source photo not found  |  
| PhotoNotUpload  | PrivateError  | Raises when photo not upload  |  
| PhotoConfigureError  | PhotoNotUpload  | Raises when photo not configured  |  
| PhotoConfigureStoryError  | PhotoConfigureError  | Raises when photo story not configured  |  
## Video Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| VideoNotDownload  | PrivateError  | Raises when source video not found  |  
| VideoNotUpload  | PrivateError  | Raises when video not upload  |  
| VideoConfigureError  | VideoNotUpload  | Raises when video not configured  |  
| VideoConfigureStoryError  | VideoConfigureError  | Raises when video story not configured  |  
| VideoTooLongException  | PrivateError  | Raises when video too long  |  
## IGTV Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| IGTVNotUpload  | PrivateError  | Raises when IGTV not upload  |  
| IGTVConfigureError  | IGTVNotUpload  | Raises when IGTV not configured  |  
## Reels/Clip Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| ClipNotUpload  | PrivateError  | Raises when Reels Clip not upload  |  
| ClipConfigureError  | ClipNotUpload  | Raises when Reels Clip not configured  |  
## Album Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| AlbumNotDownload  | PrivateError  | Raises when album not found  |  
| AlbumUnknownFormat  | PrivateError  | Raises when format of media not MP4 or JPG  |  
| AlbumConfigureError  | PrivateError  | Raises when album not configured  |  
## Story Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| StoryNotFound  | NotFoundError  | Raises when story not found  |  
## Highlight Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| HighlightNotFound  | NotFoundError  | Raises when highlight not found  |  
## Hashtag Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| HashtagError  | PrivateError  | Base exception for hashtag  |  
| HashtagNotFound  | NotFoundError  | Raises when hashtag not found  |  
| HashtagPageWarning  | ClientForbiddenError  | Occurs when Instagram returns warning_message with category_name=HASHTAG_PAGE_WARNING_MESSAGE  |  
## Location Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| LocationError  | PrivateError  | Base exception for location  |  
| LocationNotFound  | NotFoundError  | Raises when location not found  |  
## Comment Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| CommentNotFound  | PrivateError  | Raises when comment not found  |  
| CommentsDisabled  | PrivateError  | The ability to comment has been disabled by the author of the post  |  
## Share Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| ShareDecodeError  | PrivateError  | Occurs when the data format for Share-obj is incorrect  |  
## Note Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| NoteNotFound  | NotFoundError  | Raises when note not found  |  
## Track Exceptions  
| Exception  | Base  | Description  |  
| --- | --- | --- |  
| TrackNotFound  | NotFoundError  | Raises when track not found  |


---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/examples.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Examples
Runnable examples live in the repository:
  * [examples/README.md](https://github.com/subzeroid/instagrapi/blob/master/examples/README.md)
  * [examples directory](https://github.com/subzeroid/instagrapi/tree/master/examples)


The examples read credentials and runtime options from environment variables instead of hard-coding secrets:

```
export IG_USERNAME="your_username"
export IG_PASSWORD="your_password"
export IG_SESSION_FILE="./ig_settings.json"

```

Common scripts:  
| Script  | Purpose  |  
| --- | --- |  
| [`public_lookup.py`](https://github.com/subzeroid/instagrapi/blob/master/examples/public_lookup.py)  | Public profile lookup with optional `public_transport="curl"`.  |  
| [`download_user_media.py`](https://github.com/subzeroid/instagrapi/blob/master/examples/download_user_media.py)  | Login, list recent media for a username, and download photos/videos/albums.  |  
| [`monitor_user_content.py`](https://github.com/subzeroid/instagrapi/blob/master/examples/monitor_user_content.py)  | Poll a small set of users for new posts and stories using a saved session.  |  
| [`upload_media.py`](https://github.com/subzeroid/instagrapi/blob/master/examples/upload_media.py)  | Upload a feed photo, feed video, Reel, or Trial Reel.  |  
| [`upload_story.py`](https://github.com/subzeroid/instagrapi/blob/master/examples/upload_story.py)  | Upload a photo or video story, optionally with a link sticker.  |  
| [`direct_message.py`](https://github.com/subzeroid/instagrapi/blob/master/examples/direct_message.py)  | Send a Direct text message to user IDs or thread IDs.  |  
| [`handle_exception.py`](https://github.com/subzeroid/instagrapi/blob/master/examples/handle_exception.py)  | Centralized exception handling for challenges, relogin, and rate limits.  |  
Examples:

```
python examples/public_lookup.py instagram
IG_PUBLIC_TRANSPORT=curl python examples/public_lookup.py instagram
python examples/download_user_media.py instagram --amount 5 --folder ./downloads
python examples/monitor_user_content.py instagram --stories --interval 900
python examples/upload_media.py reel ./reel.mp4 --thumbnail ./thumb.jpg --caption "Reel"
python examples/upload_story.py photo ./story.jpg --caption "Story"
python examples/direct_message.py --user-ids 123456789 --text "Hello"

```

Video uploads in Android environments should pass `--thumbnail` or install the optional video dependencies, MoviePy `2.2.1`, and executable `ffmpeg`. See [Pydroid and ffmpeg](https://subzeroid.github.io/instagrapi/usage-guide/pydroid.html) and [Termux](https://subzeroid.github.io/instagrapi/usage-guide/termux.html).


---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/challenge_resolver.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
## Challenge Resolver
Instagrapi lets you attach handlers for common login challenge flows such as code verification and password reset.
## New password challenge
You can automatically change your password to solve the challenge from Instagram.
Declare `change_password_handler` which will return a new password.

```
def change_password_handler(username):
    # Simple way to generate a random string
    chars = list("abcdefghijklmnopqrstuvwxyz1234567890!&£@#")
    password = "".join(random.sample(chars, 8))
    return password

cl = Client()
cl.change_password_handler = change_password_handler
cl.login(IG_USERNAME, IG_PASSWORD)

```

## Code verification challenge
You can automatically process the codes sent to you to solve the challenge from Instagram.
You need to declare `challenge_code_handler` which will return the code received from Instagram via Email or SMS:

```
from instagrapi.mixins.challenge import ChallengeChoice


def challenge_code_handler(username, choice):
    if choice == ChallengeChoice.SMS:
        return get_code_from_sms(username)
    elif choice == ChallengeChoice.EMAIL:
        return get_code_from_email(username)
    return False

cl = Client()
cl.phone_number = "+15551234567"  # required for submit_phone challenges
cl.challenge_code_handler = challenge_code_handler
cl.login(IG_USERNAME, IG_PASSWORD)

```

Notes:
  * `challenge_code_handler(username, choice)` should return the received code as a string. Returning a falsey value means no code is available yet.
  * Login `submit_phone` challenges use `client.phone_number`, then call `challenge_code_handler(username, ChallengeChoice.SMS)` for the received code.
  * Signup SMS challenges use the `phone_number` passed to `signup(...)` and call `challenge_code_handler(username, ChallengeChoice.SMS)` for the received code.
  * Phone-only signup is supported with `signup(username, password, email="", phone_number="+15551234567")`. If both `email` and `phone_number` are provided, instagrapi keeps the email signup flow and uses the phone number only for signup challenges.
  * `signup(...)` emits a `RuntimeWarning` because it uses Instagram’s legacy account-create flow and should be treated as experimental. On modern Instagram app versions this flow is often rejected with `SignupSpamError` / `feedback_required` because the official app uses additional signup checks that instagrapi does not currently generate. Treat this as a platform rejection, not as a malformed SMS/email code.
  * Current `master` raises a clearer `ChallengeRequired` for `/auth_platform/?apc=...` flows. That path is not yet supported automatically and still requires manual verification.
  * Bloks redirect checkpoints such as `bloks_action="com.bloks.www.ig.challenge.redirect.async"` or placeholder `step_name="STEP_NAME"` require manual confirmation in the official Instagram app or web flow on a trusted device; instagrapi raises `ChallengeRequired` with the sanitized challenge context instead of treating this as a legacy step.
  * For long-running automation, persist client settings around challenge handling so you can retry without rebuilding the entire device/session state.


## Selfie and manual review challenges
`ChallengeSelfieCaptcha` and selfie/manual-review style flows are account review decisions by Instagram. `instagrapi` does not provide a generic bypass for these challenges. When they appear repeatedly during signup or login, stop the automated flow, keep the same account/device/proxy context, and resolve the account manually in the official app if possible.
For bug reports, include sanitized `client.last_json`, the exception class, and the flow that triggered it. Do not share cookies, session IDs, phone numbers, email addresses, passwords, or verification codes.
For example, you can get the code through the IMAP of Gmail:

```
def get_code_from_email(username):
    mail = imaplib.IMAP4_SSL("imap.gmail.com")
    mail.login(CHALLENGE_EMAIL, CHALLENGE_PASSWORD)
    mail.select("inbox")
    result, data = mail.search(None, "(UNSEEN)")
    assert result == "OK", "Error1 during get_code_from_email: %s" % result
    ids = data.pop().split()
    for num in reversed(ids):
        mail.store(num, "+FLAGS", "\\Seen")  # mark as read
        result, data = mail.fetch(num, "(RFC822)")
        assert result == "OK", "Error2 during get_code_from_email: %s" % result
        msg = email.message_from_string(data[0][1].decode())
        payloads = msg.get_payload()
        if not isinstance(payloads, list):
            payloads = [msg]
        code = None
        for payload in payloads:
            body = payload.get_payload(decode=True).decode()
            if "<div" not in body:
                continue
            match = re.search(">([^>]*?({u})[^<]*?)<".format(u=username), body)
            if not match:
                continue
            print("Match from email:", match.group(1))
            match = re.search(r">(\d{6})<", body)
            if not match:
                print('Skip this email, "code" not found')
                continue
            code = match.group(1)
            if code:
                return code
    return False

```

All challenges solved in the module [challenge.py](https://github.com/subzeroid/instagrapi/blob/master/instagrapi/mixins/challenge.py)
Automatic submission code from SMS/Email in examples [here](https://github.com/subzeroid/instagrapi/blob/master/examples/challenge_resolvers.py)


---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/types.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Types
`instagrapi.types` contains the public Pydantic models returned by high-level client methods and accepted by upload/story helpers.
Import models directly when you need structured input objects:

```
from instagrapi.types import Location, Media, StoryMention, UserShort, Usertag

```

## How To Read Fields
Required fields have no default value. `Optional[...]` fields may be absent from Instagram responses or returned as `null`. Fields with raw `dict` or `list` types intentionally preserve Instagram data whose shape is not stable enough for a dedicated public model yet.
## Common Models  
| Model  | Common source  | Notes  |  
| --- | --- | --- |  
| `Account`  | `account_info()`  | Private account profile for the authenticated user, including email/phone fields when Instagram returns them.  |  
| `User`  |  `user_info(...)`, `user_info_by_username(...)`  | Full public profile fields such as counts, biography, public contacts, business category, location, and messaging ids.  |  
| `UserShort`  | user lists, tags, comments, direct threads  | Compact user profile used inside many other models. Preserves newer v2 fields such as `fbid_v2`, `profile_pic_id`, `account_badges`, and `friendship_status`.  |  
| `Media`  |  `media_info(...)`, feeds, timelines, hashtag media  | Main post/Reel/album object. Includes caption/count flags, resources, usertags, coauthors, DASH info, music attribution, and inline comment previews when returned.  |  
| `Resource`  | `Media.resources`  | Album child media with thumbnail/video URLs and nested usertags.  |  
| `Comment`  | comment helpers  | Public comment model with author, text, like state/count, and reply target.  |  
| `DirectThread`  | direct thread helpers  | Direct conversation shell with participants, messages, mute/pin/group state, and activity metadata.  |  
| `DirectMessage`  | direct message helpers  | Individual direct item with text, media shares, visual media, links, reactions, replies, and seen state.  |  
| `Story`  | story/reel helpers  | Story media object with stickers, mentions, hashtags, links, locations, sponsor tags, and video metadata.  |  
| `Location`  | location helpers and upload metadata  | Place metadata used by media and story publishing flows.  |  
| `Hashtag`  | hashtag helpers  | Hashtag identity, media count, and profile picture.  |  
| `Track`  | music/Reels helpers  | Music track metadata and audio URLs when available.  |  
| `Note`  | notes helpers  | Direct Notes payload with author, audience, timestamps, and style flags.  |  
## Account And User Models
::: instagrapi.types.Account
::: instagrapi.types.User
::: instagrapi.types.UserShort
::: instagrapi.types.RelationshipShort
::: instagrapi.types.Relationship
::: instagrapi.types.Viewer
::: instagrapi.types.Usertag
::: instagrapi.types.About
::: instagrapi.types.BioLink
::: instagrapi.types.Broadcast
::: instagrapi.types.AddressBookPhone
::: instagrapi.types.AddressBookEmail
::: instagrapi.types.AddressBookContact
## Media Models
::: instagrapi.types.Media
::: instagrapi.types.Resource
::: instagrapi.types.MediaOembed
::: instagrapi.types.MediaXma
::: instagrapi.types.MediaDimensions
::: instagrapi.types.MediaDashInfo
::: instagrapi.types.MediaInlineComment
::: instagrapi.types.MediaCommentsPreview
::: instagrapi.types.SharedMediaImageCandidate
::: instagrapi.types.SharedMediaImageVersions
::: instagrapi.types.AdditionalCandidates
::: instagrapi.types.ScrubberSpritesheetInfo
::: instagrapi.types.ScrubberSpritesheetInfoCandidates
::: instagrapi.types.Collection
::: instagrapi.types.Comment
::: instagrapi.types.Location
::: instagrapi.types.Hashtag
::: instagrapi.types.Guide
::: instagrapi.types.Highlight
::: instagrapi.types.Share
## Reels And Music Models
::: instagrapi.types.ClipsMetadata
::: instagrapi.types.ClipsAchievementsInfo
::: instagrapi.types.AudioReattributionInfo
::: instagrapi.types.ClipsAdditionalAudioInfo
::: instagrapi.types.ClipsAudioRankingInfo
::: instagrapi.types.ClipsBrandedContentTagInfo
::: instagrapi.types.ClipsContentAppreciationInfo
::: instagrapi.types.ClipsMashupInfo
::: instagrapi.types.ClipsConsumptionInfo
::: instagrapi.types.ClipsFbDownstreamUseXpostMetadata
::: instagrapi.types.ClipsIgArtist
::: instagrapi.types.ClipsOriginalSoundInfo
::: instagrapi.types.ClipsReusableTextColor
::: instagrapi.types.ClipsReusableTextInfo
::: instagrapi.types.ClipsMusicAttributionInfo
::: instagrapi.types.Track
## Story Models
::: instagrapi.types.Story
::: instagrapi.types.StoryMention
::: instagrapi.types.StoryMedia
::: instagrapi.types.StoryHashtag
::: instagrapi.types.StoryLocation
::: instagrapi.types.StoryStickerLink
::: instagrapi.types.StorySticker
::: instagrapi.types.StoryPoll
::: instagrapi.types.StoryBuild
::: instagrapi.types.StoryLink
::: instagrapi.types.StoryArchiveDay
## Direct Models
::: instagrapi.types.DirectThread
::: instagrapi.types.DirectShortThread
::: instagrapi.types.DirectMessage
::: instagrapi.types.DirectResponse
::: instagrapi.types.DirectMedia
::: instagrapi.types.ReplyMessage
::: instagrapi.types.MessageReaction
::: instagrapi.types.MessageReactions
::: instagrapi.types.MessageLink
::: instagrapi.types.LinkContext
::: instagrapi.types.LastSeenInfo
::: instagrapi.types.DisappearingMessagesSeenState
::: instagrapi.types.FallbackUrl
::: instagrapi.types.DirectMessageImageCandidate
::: instagrapi.types.DirectMessageImageVersions
::: instagrapi.types.VideoVersion
::: instagrapi.types.FriendshipStatus
::: instagrapi.types.VisualMedia
::: instagrapi.types.VisualMediaContent
::: instagrapi.types.VisualMediaUser
::: instagrapi.types.ExpiringMediaActionSummary
## Notes
::: instagrapi.types.Note


---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/totp.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# TOTP
TOTP setup and code generation  
| Method  | Return  | Description  |  
| --- | --- | --- |  
| totp_generate_seed()  | str  | Generate 2FA TOTP seed  |  
| totp_enable(verification_code: str)  | List[str]  | Enable TOTP 2FA and return backup codes  |  
| totp_disable()  | bool  | Disable TOTP 2FA  |  
| totp_generate_code(seed: str)  | str  | Generate a current 2FA TOTP code from a seed  |  
Example:

```
>>> from instagrapi import Client
>>> cl = Client()
>>> cl.login(USERNAME, PASSWORD)

>>> seed = cl.totp_generate_seed()
"67EIYPWCIJDTTVX632NEODKEU2PY5BIW"

>>> code = cl.totp_generate_code(seed)
"123456"

>>> cl.totp_enable(code)
["1234 5678", "1234 5678", "1234 5678", "1234 5678", "1234 5678"]

>>> cl.totp_disable()
True

```

Notes:
  * `totp_generate_seed()` gives you the secret key you would normally scan into an authenticator app.
  * `totp_generate_code()` is a local helper and can be used anywhere you already have the TOTP seed.
  * Save the backup codes returned by `totp_enable()` immediately. Instagram does not guarantee that you can fetch the same codes again later.


## Bloks two-factor flow
Some accounts are moved by Instagram to a newer CAA/Bloks two-factor flow. In that case the legacy `accounts/two_factor_login/` endpoint can reject a valid code with `Invalid Parameters`.
`Client.login(..., verification_code="123456")` still uses the legacy mobile endpoint first. If Instagram returns a `two_step_verification_context`, instagrapi automatically retries through the Bloks two-factor flow. If the legacy login response does not expose that context, instagrapi can make a current CAA/Bloks login request to recover the context and continue the same Bloks verification path. When Instagram still does not return enough state, the exception explains that the account needs manual app verification or a fresh current-app login response.
8-digit backup codes can be passed through the same `verification_code` parameter:

```
cl.login(USERNAME, PASSWORD, verification_code="12345678")

```

When the code is 8 digits and Instagram exposes `two_step_verification_context`, instagrapi selects the Bloks `backup_codes` challenge instead of sending the code to the legacy TOTP/SMS endpoint.
The low-level helpers remain available when you need to inspect or drive the flow manually:

```
from instagrapi import Client

cl = Client()

# The context comes from Instagram's login challenge response.
context = "<two_step_verification_context>"

cl.bloks_two_step_verification_entrypoint(context)
cl.bloks_two_step_verification_method_picker(context)
cl.bloks_two_step_verification_select_method(context, selected_method="totp")

code = cl.totp_generate_code("<totp seed>")
result = cl.bloks_two_step_verification_verify_code(context, code, challenge="totp")
login_payload = cl.bloks_extract_login_response(result)
cl.bloks_apply_login_response(login_payload)

```

For SMS, select and verify the `sms` challenge instead:

```
cl.bloks_two_step_verification_select_method(context, selected_method="sms")
result = cl.bloks_two_step_verification_verify_code(context, "123456", challenge="sms")

```

For backup codes, select `backup_codes`, open the backup-code entry screen, then verify the 8-digit code:

```
cl.bloks_two_step_verification_select_method(context, selected_method="backup_codes")
cl.bloks_two_step_verification_enter_backup_code(context)
result = cl.bloks_two_step_verification_verify_code(context, "12345678", challenge="backup_codes")

```

`bloks_caa_login_send_request(...)` is also available as a low-level helper for inspecting the CAA/Bloks login response manually. `bloks_extract_two_step_verification_context(...)` extracts the context from that response when Instagram returns the current Bloks redirect action.
`bloks_extract_login_response(...)` returns decoded `login_response`, response `headers`, cookie values, raw cookie header text, and the raw embedded object when Instagram returns a successful Bloks login payload. It returns `{}` when the response is an intermediate UI state or an error. `bloks_apply_login_response(...)` can then copy the returned authorization data and cookies into the current client session.
Automatic fallback can only run after Instagram exposes `two_step_verification_context` to the client or to the CAA/Bloks login response. A `BadPassword` response with a known-good password can still be account-risk handling before Instagram exposes that context, so treat it as a signal to inspect proxy/IP, device consistency, and the raw login response.


---


# Source: https://subzeroid.github.io/instagrapi/usage-guide/public-transport.html

# [instagrapi ](https://subzeroid.github.io/instagrapi/)
## 🔥 The fastest and powerful Python library for Instagram Private API 2026 with HikerAPI SaaS
[](https://github.com/subzeroid/instagrapi)
# Public Transport
`instagrapi` uses two network surfaces:
  * private mobile API requests, used for authenticated mobile flows;
  * public web requests, used by helpers such as public profile and public media lookups.


The default public web transport is `requests`. It has the smallest dependency footprint and keeps the existing transport-level retry behavior.
The public transport option is exposed as `PublicTransport = Literal["requests", "curl"]`.
For public web endpoints that are sensitive to browser TLS fingerprints, you can install the optional curl transport:

```
pip install "instagrapi[curl]"

```

Then opt in explicitly:

```
from instagrapi import Client

cl = Client(public_transport="curl", public_transport_impersonate="chrome136")

```

Private mobile API requests still use the regular mobile session. The curl transport only changes the public web session.
## Live Comparison
This is a point-in-time live comparison from May 15, 2026. Instagram public web behavior changes frequently, so treat these numbers as a practical signal, not a guarantee.
Method:
  * branch: curl public transport PR branch;
  * environment: fresh remote Linux clone with `instagrapi[curl]` installed;
  * Python: 3.12;
  * rounds: 4;
  * public request retry loop: disabled with `public_request_retries_count = 1`;
  * curl impersonation: `chrome136`;
  * identical inputs for both transports.

  
| Public web helper  | `requests`  | `curl`  |  
| --- | --- | --- |  
| `user_info_by_username_gql("instagram")`  | 0/4 ok, p50 12.05s  | 3/4 ok, p50 1.42s  |  
| `user_info_by_username_gql("1fexd")`  | 0/4 ok, p50 12.05s  | 2/4 ok, p50 0.20s  |  
| `media_pk_from_url("https://www.instagram.com/p/C_BM2yAN4Rm/")`  | 4/4 ok, p50 0.00s  | 4/4 ok, p50 0.00s  |  
| `media_info_gql("3441088131388376166")`  | 0/4 ok, p50 2.49s  | 0/4 ok, p50 2.45s  |  
| Total  | 4/16 ok, p50 7.28s  | 9/16 ok, p50 0.23s  |  
Observed failures:
  * `requests` repeatedly hit `429` on `users/web_profile_info`;
  * `curl` avoided those `429` responses in early rounds, then hit `401` on the same public endpoint;
  * both transports hit `404` on the tested public media info path.


## Recommendation
Use the default `requests` transport unless you specifically need public web endpoints that are being rate limited or blocked by TLS fingerprint checks.
Use `public_transport="curl"` when:
  * public profile web lookups return repeated `429` responses with the default transport;
  * you can install the optional native dependencies pulled by `instagrapi[curl]`;
  * you understand that public web access is still opportunistic and can return `401`, `403`, `404`, or `429`.


Prefer authenticated private API helpers for production workflows when an equivalent private/mobile path exists.


---
