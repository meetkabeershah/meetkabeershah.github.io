---
title: Study on technical feasibility of WhatsApp bot implementation
type: post
---

![WhatsApp](https://www.whatsapp.com/img/fb-post.jpg)

[courtesy](https://web.whatsapp.com/)

For some of technical experiments, I was trying to figure out how beneficial and feasible it is to implement bots for diffetent chat platforms in terms of market share and so possibilities of adaptation.

Popular chat platforms like [Messenger](https://developers.facebook.com/docs/messenger-platform/), [Slack](https://api.slack.com/bot-users), [Skype](https://dev.skype.com/bots) etc. have happily (in the sense officially) provided APIs for bots to interact with except, WhatsApp.

However, since many years, a lot of activities has happened around this - struggle towards automated interaction with WhatsApp platform:

 1. [Bots App](https://www.npmjs.com/package/botsapp)
 Bots App is interesting because it shows that something is really tried and tested.
 
 2. [Yowsup](https://github.com/tgalal/yowsup)
 A project still actively developed to interact with WhatsApp platform.
 
 3. [Yallagenie](http://www.yallagenie.com/) 
 Yallagenie claim that there is a demo bot which can be interacted with at [+971 56 112 6652](tel://+971561126652)

 4. [Hubtype](https://hubtype.com/articles/how-to-create-a-whatsapp-chatbot.html)
 Hubtype is working towards having a bot platform for **WhatsApp for business**.

 5. [Fred](https://medium.com/@AlfredBaudisch/how-a-whatsapp-bot-got-famous-and-evolved-as-the-brazilian-wechat-and-conversational-commerce-e2213262183d)
 Fred's task was to automate WhatsApp conversations, however since it was not officially supported by WhatsApp - it was shut down.

 7. [Oye Gennie](http://www.oyegennie.com/)
 A bot [blocked](https://www.quora.com/How-do-I-build-a-simple-Whatsapp-bot/answer/Ankur-Rastogi?srid=hM8Hz) by WhatsApp.
 
 8. [App/Website to WhatsApp](https://faq.whatsapp.com/en/android/28000012)
 We can use custom URL schemes and Android intent system to interact with WhatsApp but still NOT WhatsApp API.
 
 9. [Chat API daemon](https://github.com/Mawalu/chat-api-daemon)
 Probably created by inspecting the API calls in WhatsApp web version. NOT affiliated with WhatsApp.
 
 10. [WhatsBot](https://devpost.com/software/whatsbot#updates)
 Deactivated WhatsApp bot. Created during a [hackathon](https://techcrunch.com/2015/12/06/whatsbot-brings-a-virtual-assistant-to-whatsapp/).
 
 11. [No API claim](http://mashable.com/2015/03/25/whatsapp-developers-api/#CvXpmtrjROqA)
 WhatsApp co-founder clearly stated this in a conference that they did not had any plans for APIs for WhatsApp.
 
 12. [Bot Ware](https://www.botware.com.br/messenger-and-whatsapp-chatbot-development/)
 They probably are expecting WhatsApp to release their APIs for chat bot platforms.
 
 13. [Vixi](http://vixi.io/)
 They seems to be talking about how some platform which probably would work for WhatsApp. There is no clarity as such.
 
 14. [Unofficial API](https://market.mashape.com/datayuge/whatsapp)
 This API can shut off any time.
 
 And the number goes on...
 
 So far, [WhatsApp do not officially support APIs](https://faq.whatsapp.com/search?query=api&lang=en). There is no trace on the whole Internet which talks about **official** API support from WhatsApp.

This single reason is more than enough for Chat bot building companies to not support WhatsApp and not risk their investments and resources.
