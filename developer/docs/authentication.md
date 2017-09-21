---
layout: docs
---

# Authentication

The Agendas API uses the [OAuth2 protocol](https://oauth.net/2/).

## Grant Types

There are 2 kinds of grant types you'll be able to use with Agendas:
* **Authorization Code Grant *(coming soon)*.** This grant type sends an authorization code back to your server. Your server then uses that authorization code, along with a client secret, to request an access token and a refresh token. Support for this grant type in the Agendas API is coming soon.
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
