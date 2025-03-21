---
id: auth-google-oauth
title: 'Part Five: Google Oauth'
description: 'Supabase Deep Dive Part 5: Google OAuth Provider'
---

### About

How to add Google OAuth Logins to your Supabase Application.

### Watch

<iframe className="w-full video-with-border" width="640" height="385" src="https://www.youtube-nocookie.com/embed/_XM9ziOzWk4" frameBorder="1" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowFullScreen></iframe>

### Logging in with external OAuth providers

Connecting social logins such as Google, GitHub, or Facebook couldn't be easier. In this guide we'll walk you through the process of connecting Google, but the process is basically the same for all of the providers which includes: azure, bitbucket, github, gitlab, facebook, and google.

First you'll need to create a google project inside their [cloud console](https://console.cloud.google.com/home/dashboard), in other providers they may refer to this as an "app" and is usually available on the company's developer portal.

![Create a new Google Project inside cloud console](/img/auth-5-1.png)

Once you have a project, type "OAuth" into the search bar and open up "OAuth Consent Screen"

![Open the OAuth consent screen](/img/auth-5-2.png)

Select 'External' and proceed to fill out the rest of the form fields

![Select External on the OAuth form](/img/auth-5-3.png)

Next open up Credentials page on the left

![Open up Credentials page](/img/auth-5-4.png)

And click to create a new set of credentials, select OAuth client ID as the option

![Create new oauth client id credentials](/img/auth-5-5.png)

Now choose Web Application (assuming you're creating a web app) and in the Authorized redirect URI section you need to add: `https://<your-ref>.supabase.co/auth/v1/callback`. You can find your Supabase URL in Settings > API inside the Supabase dashboard.

![Add your redirect URI](/img/auth-5-6.png)

Now you can grab the client ID and secret from the popup, and insert them into the google section inside the Supabase dashboard in Auth > Settings:

![take client id and secret](/img/auth-5-7.png)

![insert client id and secret into supabase dashboard in auth > auth](/img/auth-5-8.png)

Hit save. Now you should be able to navigate in the browser to:

```
https://<your-ref>.supabase.co/auth/v1/authorize?provider=google
```

And log in to your service using any google or gmail account.

You can additionally add a query parameter `redirect_to=` to the end of the URL for example:

```
https://<your-ref>.supabase.co/auth/v1/authorize?provider=google&redirect_to=http://localhost:3000/welcome
```

But make sure any URL you enter here is on the same host as the site url that you have entered on the Auth > Settings page on the Supabase dashboard. (There is additional functionality coming soon, where you'll be able to add additional URLs to the allow list).

If you want to redirect the user to a specific page in your website or app after a successful authentication.

You also have the option of requesting additional scopes from the oauth provider. Let's say for example you want the ability to send emails on behalf of the user's gmail account. You can do this by adding the query parameter `scopes`, like:

```
https://<your-ref>.supabase.co/auth/v1/authorize?provider=google&https://www.googleapis.com/auth/gmail.send
```

Note however that your app will usually have to be verified by Google before you can request advanced scopes such as this.

The only thing left to implement is the UI, but if you prefer to use something pre-built, we have a handy [Auth Widget](https://github.com/supabase/ui/#using-supabase-ui-auth), where you can enable/disable whichever auth providers you want to support.

For any support please get in touch at beta at supabase.io or for feature requests open an issue in the [backend](https://github.com/supabase/gotrue) or [frontend](https://github.com/supabase/gotrue-js) repos.

### Resources

- JWT debugger: https://jwt.io/​

### Next steps

- Watch [Part One: JWTs](/docs/learn/auth-deep-dive/auth-deep-dive-jwts)
- Watch [Part Two: Row Level Security](/docs/learn/auth-deep-dive/auth-row-level-security)
- Watch [Part Three: Policies](/docs/learn/auth-deep-dive/auth-policies)
- Watch [Part Four: GoTrue](/docs/learn/auth-deep-dive/auth-gotrue)
<!-- - Watch [Part Five: Google Oauth](/docs/learn/auth-deep-dive/auth-google-oauth) -->
- Sign up for Supabase: [app.supabase.io](https://app.supabase.io)
