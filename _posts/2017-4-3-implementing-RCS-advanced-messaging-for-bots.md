---
layout: post
title: Implementing RCS Advanced Messaging for Bots
---

![RCS Advanced Messaging](https://www.att.com/shopcms/media/att/2015/shop/landing/advanced-messaging/247371-lp-advanced-messaging-mrq.jpg)

[Courtesy](https://www.att.com/shop/wireless/features/advanced-messaging.html)

The actual [Advanced Messaging / RCS 2](http://www.gsma.com/network2020/rcs-2/) implementation is [Android Messages](https://play.google.com/store/apps/details?id=com.google.android.apps.messaging).

This platform needs to expose it's APIs so that our bots can access it. The people working on RCS / Advanced Messaging are [Jibe](https://jibe.google.com/jibe-platform/). They seems to be in process of providing Advanced Messaging / RCS 2 APIs but technically there's nothing ready. 

Was having a look at the [Solaiemes RCS API](https://solaiemes-rcs-api.3scale.net/api). At this point, I feel that it's **API end points** are not working:

 - http://api.2445580839652.proxy.3scale.net:80/rcsapi/session
 - https://tadhack.solaiemes-rcs-api.3scale.net/rcsapi
 - https://tadhack.3scale.net/rcsapi
 - http://tadhack.solaiemes.com/rcsapi

The following API seems to be the most close to what is actually needed:

 - [42 AMP API](https://www.fortytwo.com/solutions/amp/)
 - [Jibe](https://jibe.google.com/jibe-platform/)
 
The following vendors are yet to confirm whether they support Advanced Messaging / RCS 2:

 - [Twilio](https://www.twilio.com/console/support/tickets/927458)
 - [Airbop](http://support.airbop.com/discussions/questions/662-how-rcsadvanced-messaging-can-be-used-with-botframework)
 - [Mavenir](mailto:contactus@mavenir.com)
 - [Solaiemes](mailto:info@solaiemes.com)
 - [Muut](mailto:info@muut.com)
 - [FortyTwo](mailto:sales@fortytwo.com)
 - [Dexter](mailto:info@rundexter.com)
 
As of 3 <sup>rd</sup> April'2017, the following chat bot providers do not support Advanced Messaging

 - [GupShup](http://gupshup.io)
 - [InfoBip](https://www.infobip.com/)
 
Although, [GSMA](mailto:info@gsma.com) is not supposed to, and has not responded to our technical questions.
