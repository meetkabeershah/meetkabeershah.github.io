---
layout: post
title: RCS 2 / Advanced Messaging - implementation research
---

![RCS Advanced Messaging](http://www.droid-life.com/wp-content/uploads/2014/11/google-messenger.jpg)

[Courtesy](http://www.droid-life.com/2015/03/13/google-messenger-updated-with-gif-support-and-a-widget/)

Recently, I was doing some studies on implementation of [Advanced Messaging / RCS 2](http://www.gsma.com/network2020/rcs-2/) as a channel for chat bots.

The client implementation seems to be [Android Messages](https://play.google.com/store/apps/details?id=com.google.android.apps.messaging).

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
 - [Wit Software](https://www.wit-software.com/contacts/)
 - [TelesTax](https://telestax.com/contact/)
 - [Tropo](https://www.tropo.com/help/contact-us/)
 - [Tatango](https://www.tatango.com/platform/rcs-messaging/)
 - [Interop](http://interoptechnologies.com/rcs/)
 
As of april'2017, the following vendors do not support Advanced Messaging

 - [FortyTwo](mailto:sales@fortytwo.com)
 - [Dexter](mailto:info@rundexter.com)
 - [Gateway API](mailto:support@gatewayapi.com)
 - [GupShup](http://gupshup.io)
 - [InfoBip](https://www.infobip.com/)
 - [TeleMessage](https://www.telemessage.com/contact-us/)
  
Although, [GSMA](mailto:info@gsma.com) is not supposed to, and has not responded to our technical questions. GSMA has specified [RCS API](http://www.gsma.com/network2020/wp-content/uploads/2013/08/RCC_13_v2.0.pdf) requirements so far.

# Btw, what is RCS?

**Features of Advanced Messaging**

 - Ubiquity
 - Simplicity
 - Everyone is invited
 - All the features
 - Enhanced messaging experience

**WHAT IS ‘MESSAGING AS A PLATFORM (MAAP)?**

To most users messaging is just an ‘app’ – a program on their phones they use to keep in touch. Advanced Messaging will change that though – messaging is now becoming a ‘platform’ on which applications will be built to deliver whole new levels of interaction and experience. It is where SMS is headed. End-users simply want all the services they need as quickly and conveniently as possible, and MaaP lets operators deliver that. If you want to book a taxi, a flight or look up train times for example, you will not need to download a specific new app – just hit your messenger. MaaP removes that barrier of another app to download and connects suppliers directly to consumers. Messaging as a Platform will give operators all new possibilities for developing and implementing innovative services, and most importantly, for generating new revenues.

**The potential for Messaging as a Platform**

One of the more striking developments of messaging in recent times has been the evolution of messaging apps and clients into the ‘new home page’. End-users pick up their mobile devices in the morning and the first place many head to is their chat or messaging app. It has now become both their inbox and their home page. This is an evolution that operators can use to develop Messaging as a Platform propositions.

**For users**

This enables all sorts of companies to interact with customers in unprecedented ways – travellers, for example, could receive their actual electronic boarding pass securely from airlines rather than receiving an SMS with a link. When on holiday users can order a taxi or Uber, check the weather at their destination and the exchange rate, find a recommended restaurant and book a table and pay for it and learn some handy phrases in another language – all just by sending messages.

**For marketers**

Further to this progression in customer service and fulfilment, marketers too benefit from Advanced Messaging. They can use read receipts to tell if end-users have read promotional messages and where and when they read them. They can embed call-to-action codes in them, giving access to previously unavailable data to analyse. It all adds up to richer, more engaging advertising content. 

**For bots**

Furthermore, Advanced Messaging also enables Bot-to-Person interactions, where end-user engagements are simply richer and more detailed. The Messaging as a Platform approach and its exponentially increased degree of interaction makes huge new monetization opportunities available to MNOs.

**For  workplace**

Operators can extend their blue sky thinking with Messaging as a Platform; why not a smart, Wi-Fi-enabled video doorbell which uses messaging to record a video message from a visitor when you are not home and ‘chat’ it direct to your mobile device? Built-in AI-based intelligent assistants are great in their place but some people do not like talking out loud to their phone in public places – chatbots can enable that same function via a messaging platform.

**Advanced Messaging deployment models: getting it right**

Another key benefit of Advanced Messaging is that deployment models can be mixtures of various approaches; operators do not need to commit entirely to a single method and limit their options.
 
 1. **OWN IMS**
 PROS
- Retain control of core service
- Flexibility and ability to integrate with other services
 CONS
- Complex project, requires expertise
- Costly in the short term, CAPEX

 2. **HOSTED SERVICE**
 PROS
- Pay-as-you-grow model
- Fast deployment and time to market
- Benefit from third-party data centre infrastructure and expertise
- Scope for complementing other services e.g. VoLTE
 CONS
- Limited service flexibility
- No in-premises deployment option

[Source](http://www.gsma.com/network2020/wp-content/uploads/2016/11/Network-2020-006-Advanced-Communications-eBook-edition-1-2.pdf)
