---
title: Facebook API - The URL couldn't be validated. Callback verification failed with the following errors
layout: post
---

![Webhooks](https://images.kualo.com/mailmachine/wufoowebhook.png)

[courtesy](https://my.kualo.com/uk/knowledgebasekualo.php?kbcat=0&article=120)

Was trying to [setup FB messenger webhook](https://developers.facebook.com/docs/messenger-platform/getting-started/app-setup/#webhook_setup) with a strong verify token. Somewhat like this: `o\/ERviEE\/vt0|<E|\|`

![o\/ERviEE\/vt0|<E|\| verify token set](https://i.stack.imgur.com/RBumW.png)

The same is been verified in the code:

    req.query['hub.verify_token'] === 'o\/ERviEE\/vt0|<E|\|'

However, the value received from FB is: `o\\/ERviEE\\/vt0|<E|\\|`

![o\\/ERviEE\\/vt0|<E|\\|  verify token get](https://i.stack.imgur.com/MKtwP.png)

**This is strange**. There seems to be no document reference as such which talks about how Facebook escapes special characters for verify tokens or alike. Not sure if this happens for other entities as well.

Conclusion: need to be a little bit cautious when using special characters for verify tokens.

Because, Facebook escapes special characters for webhooks' verify tokens.
