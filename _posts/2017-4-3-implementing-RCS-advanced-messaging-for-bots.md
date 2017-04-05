---
layout: post
title: Implementing RCS Advanced Messaging for Bots
---

![RCS Advanced Messaging](http://www.droid-life.com/wp-content/uploads/2014/11/google-messenger.jpg)

[Courtesy](http://www.droid-life.com/2015/03/13/google-messenger-updated-with-gif-support-and-a-widget/)

The actual [Advanced Messaging / RCS 2](http://www.gsma.com/network2020/rcs-2/) implementation is [Android Messages](https://play.google.com/store/apps/details?id=com.google.android.apps.messaging).

This platform needs to expose it's APIs so that our bots can access it. The core people working on RCS / Advanced Messaging are [Jibe](https://jibe.google.com/jibe-platform/). They seems to be in process of providing Advanced Messaging / RCS 2 APIs but technically there's nothing ready. 

Was having a look at the [Solaiemes RCS API](https://solaiemes-rcs-api.3scale.net/api). Solaiemes is the subsidiary of Mavenir/Xura. At this point, it's **API end points** are not working:

 - [http://api.2445580839652.proxy.3scale.net:80/rcsapi/session](http://api.2445580839652.proxy.3scale.net:80/rcsapi/session)
 - [https://tadhack.solaiemes-rcs-api.3scale.net/rcsapi](https://tadhack.solaiemes-rcs-api.3scale.net/rcsapi)
 - [https://tadhack.3scale.net/rcsapi](https://tadhack.3scale.net/rcsapi)
 - [http://tadhack.solaiemes.com/rcsapi](http://tadhack.solaiemes.com/rcsapi)

The following API seems to be the most close to what is actually needed:

 - [Mavenir](http://www.mavenir.com/our-solutions/rich-communication-rcs)
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
 - [Symsoft](mailto:sales@symsoft.com)
 - [MessageBird](mailto:support@messagebird.com)
 - [Summit Tech](mailto:info@summit-tech.com)
 - [RCS](https://www.richcommunicationsuite.com/contact.php)
 - [Spirent](mailto:support@spirent.com)
 - [Nablecomm](mailto:contact@nablecomm.com)
 - [RCS-RDS](mailto:sales@rcs-rds.ro)
 - [NewPace](http://www.newpace.ca/contact)
 - [Infinite Convergence](mailto:carrier-support@infinite.com)
 - [ZTE](mailto:8008309870@zte.com.cn)
 - [Utimaco](mailto:li-contact@utimaco.com)
 - [Media 5 Corp](mailto:dev_support@media5corp.com)
 - [Acision](mailto:contact@acision.com)
 - [Newnet Mobility](https://newnetmobility.com/contact/)
 
As of 3^rd April'2017, the following vendors do not support Advanced Messaging

 - [Gateway API](mailto:support@gatewayapi.com)
 - [GupShup](http://gupshup.io)
 - [InfoBip](https://www.infobip.com/)
 - [TeleMessage](https://www.telemessage.com/contact-us/)
  
Although, [GSMA](mailto:info@gsma.com) is not supposed to, and has not responded to our technical questions. GSMA has specified [RCS API](http://www.gsma.com/network2020/wp-content/uploads/2013/08/RCC_13_v2.0.pdf) requirements so far.
