---
layout: post
title: Website network load optimization tip
---

Sometimes we implement multiple external links which points to the same resource. For example in one of our websites we have 

- [https://platform.instagram.com/en_US/embeds.js](https://platform.instagram.com/en_US/embeds.js)

- [https://www.instagram.com/embed.js](https://www.instagram.com/embed.js)

Both of these result to 

[https://www.instagram.com/static/bundles/es6/EmbedSDK.js/363a6c0267bf.js](https://www.instagram.com/static/bundles/es6/EmbedSDK.js/363a6c0267bf.js)

Thus the website made 3 network requests for the same resource 😅😅

The solution?

I observed that implementing the final result i.e.  

[https://www.instagram.com/static/bundles/es6/EmbedSDK.js/363a6c0267bf.js](https://www.instagram.com/static/bundles/es6/EmbedSDK.js/363a6c0267bf.js)

reduced the number of network calls from 3 to 1 ✌

Why wait? Try to implement this in your respective projects too!!