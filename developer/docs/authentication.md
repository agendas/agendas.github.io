---
layout: docs
---

# Authentication

The Agendas API uses the [OAuth2 protocol](https://oauth.net/2/).

## Grant Types

There are 2 kinds of grant types you'll be able to use with Agendas:
* **Authorization Code Grant.** This grant type sends an authorization code back to your server. Your server then uses that authorization code, along with a client secret, to request an access token and a refresh token. ~~Support for this grant type in the Agendas API is coming soon.~~ The Agendas API now supports Authorization Code Grant!
* **Implicit Grant.** In this grant type, our API sends an access token directly to a redirect URL that you specify. This method does not require a client secret but **does not support refresh tokens**.

### Which grant type should I use?

**Use Authorization Code Grant if:**
* You can keep the client secret secret
* You need to use refresh tokens

**Use Implicit Grant if:**
* You can't ensure the security of the client secret
* Your app doesn't have any servers

**TL;DR** Generally, use implicit grant for static web apps or mobile apps. For apps that run on a server, use authorization code grant.

## Configuring Authentication

To configure authentication settings, go to the [Agendas developer console](https://app.agendas.co/#/console), select your app on the dashboard, then scroll down to the section titled *Authentication*.

### Configuring Authorization Code Grant

Here's how to configure authorization code grant for your app:
1. Click on the *Auth Code Grant* tab.
2. Enable the switch if you haven't done so.
3. Click the *Show* button below the switch to retrieve your client secret.
4. That's it!

Should you ever need to regenerate your client secret, use the red regenerate button to the right of your client secret.

### Configuring Implicit Grant
1. Select the *Implicit* tab.
2. Click the *Enable* button (or the edit icon if you've already enabled it.)
3. Enter the redirect URL you'd like to use.
4. That's it!

## Retrieving an Access Token

### Authorization Code Grant
~~Coming soon!~~ Now here!

#### Step 1: Request a Grant Code

To obtain a grant code, open a browser window with the URL `https://api.agendas.co/api/v1/authorize`. Pass in your client ID, a redirect URL, and some scopes (separated by spaces) through query variables.

*Sample Request:*
```
https://api.agendas.co/api/v1/authorize?response_type=code&client_id=CLIENT_ID&redirect_uri=REDIRECT_URL&scope=SCOPE,SCOPE
```

| Param Name | Description |
| --- | --- |
| `response_type` | Pass in `code` to use authorization code grant. |
| `client_id` | Your app's client ID. You can find this in the console. |
| `redirect_uri` | The URL to send the token to. |
| `scope` | A space-separated list of [authentication scopes](#authentication-scopes). |

#### Step 2: Get the Grant Code

If authentication succeeds, the API will redirect the user to your redirect URL, like so:

*Example Response URL:* `https://redirect.url?code=GRANT_CODE`

The grant code will be in the `code` parameter of the URL. This grant code is only valid for 60 seconds, so use it quickly!

#### Step 3: Retrieve an Access Token

To retrieve an access token, send an HTTP `POST` request to the `token` endpoint with these values in the request body:

| Key | Type | Required? | Description |
| --- | --- | --- | --- |
| `grant_type` | string | Yes | Pass in `authorization_code` to use authorization code grant. |
| `code` | string | Yes | The grant code you received in step 2. |
| `client_id` | string | Yes | Your app's client ID. You can find this in the console. |
| `client_secret` | string | Yes | Your app's client **secret**. You can find this in the console. |

If authentication is successful, the endpoint will return these values:

| Key | Type | Description |
| --- | --- | --- |
| `ok` | boolean | Whether authentication succeeded. (should be `true`) |
| `token_type` | string | The type of access token the server has issued. This is always set to `bearer`. |
| `expires_in` | number | The number of seconds until the access token expires (usually 1 hour). |
| `access_token` | string | Your [access token.](#using-access-tokens) |
| `refresh_token` | string | A refresh token to use in step 4. This token never expires. |

If authentication fails, the endpoint will return an error:

| Status | Error Code | Description |
| --- | --- | --- |
| 400 | `invalid_request` | Your request is missing some parameters. |
| 400 | `invalid_grant` | The authorization code (or refresh token) is invalid. |
| 400 | `invalid_client` | The client secret and client ID are invalid. |
| 500 | `server_error` | An internal server error occurred. |

*Sample Request:*
```
POST https://api.agendas.co/api/v1/token
```
```javascript
{
  "grant_type": "authorization_code",
  "code": GRANT_CODE,
  "client_id": CLIENT_ID,
  "client_secret": CLIENT_SECRET
}
```

*Sample Response:*
```javascript
{
  "ok": true,
  "token_type": "bearer",
  "expires_in": 3600,
  "access_token": ACCESS_TOKEN,
  "refresh_token": REFRESH_TOKEN
}
```

*Sample Error:*
```javascript
{
  "ok": false,
  "error": "invalid_grant"
}
```

#### Step 4: Refresh an Access Token

After an hour, your access token will expire, and you will lose access to the user's agendas.

But don't worry! You can use refresh tokens to fix this problem.

To use a refresh token, use the same `token` endpoint you used in step 3. Pass in these values:

| Key | Type | Required? | Description |
| --- | --- | --- | --- |
| `grant_type` | string | Yes | Pass in `refresh_token` to use your refresh token. |
| `refresh_token` | string | Yes | The refresh token you received in step 3. |
| `client_id` | string | Yes | Your app's client ID. You can find this in the console. |
| `client_secret` | string | Yes | Your app's client **secret**. You can find this in the console. |

The server will issue a new access token and a new refresh token, as shown in step 3.

**NOTE:** Refresh tokens never expire on their own. However, calling the `token` endpoint will invalidate any existing refresh tokens.

### Implicit Grant
To obtain a token, open a browser window with the URL `https://api.agendas.co/api/v1/authorize`. Pass in your client ID, redirect URL, and scopes (separated by spaces) through query variables.

You can also pass in an optional `state` parameter.

*Sample Request:*
```
https://api.agendas.co/api/v1/authorize?response_type=token&client_id=CLIENT_ID&redirect_uri=REDIRECT_URL&scope=SCOPE,SCOPE
```

| Param Name | Description |
| --- | --- |
| `response_type` | Pass in `token` to use implicit grant. |
| `client_id` | Your app's client ID. You can find this in the console. |
| `redirect_uri` | The URL to send the token to. This **must** match the redirect URL you've set in the console. |
| `scope` | A space-separated list of [authentication scopes](#authentication-scopes). |

#### Response

If authentication succeeds, the API will redirect the user to your redirect URL. The access token will be in the `access_token` parameter of the URL. This access token is valid for 7 days.

*Example Response URL:* `https://redirect.url?access_token=ACCESS_TOKEN&token_type=bearer&expires_in=604800`

## Authentication Scopes

Here's a list of the authentication scopes you can use:

| Scope Name | Permission |
| --- | --- |
| `email` | Retrieve the user's email address |
| `username-read` | Read the user's username |
| `agenda-read` | Read the user's agendas, tags, and tasks |
| `agenda-write` | Write to the user's agendas, tags, and tasks |

## Using Access Tokens
When calling an API method, you can authenticate using these 2 methods:
* **Authorization Header.** This is the **recommended** method. To authenticate, encode the token within the `Authorization` HTTP header, like so:
  ```
  Authorization: Bearer {token}
  ```
  Ensure that the term `Bearer` is in the header.
* **Token Parameter.** This method should *only* be used for testing. To authenticate using this method, encode the token within the URL, like so: `https://api.agendas.co/api/v1/{endpoint}?token=TOKEN`

### Authentication Errors
Authentication errors will be sent in plain text.

| Status | Response Body | Meaning |
| --- | --- | --- |
| 401 | `Missing token` | You did not provide an access token. |
| 401 | `Invalid token type` | Your token's type is not supported by the Agendas API. Make sure it is a `Bearer` token. |
| 401 | `Token expired` | Your token has expired. You should ask the user to re-authenticate. |
| 401 | `Invalid token` | The token you provided is incorrect, has been revoked, or is otherwise invalid. You should ask the user to re-authenticate.
| 403 | | Your app does not have permission to access a resource. Try re-authenticating with the correct scopes.

## Next Steps

* Learn how to [work with a user's agendas](agendas).
* [Get information about a user](user).
