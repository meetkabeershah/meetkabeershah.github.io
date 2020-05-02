---
title: AWS Elastic load balance and CORS issues
layout: post
---

![AWS Elastic load balance and CORS issues](https://www.geekboy.ninja/blog/wp-content/uploads/2016/12/cors.png)

[credit](https://www.geekboy.ninja/blog/tag/cross-origin-resource-sharing/)

>In one of my projects, I’m getting issues while connecting to AWS load balancers - I have written this post to secure my studies in this regard.

We have an [Angular 4](https://angular.io/) front end hosted on [AWS S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingBucket.html), with an [AWS elastic load balancer](https://aws.amazon.com/elasticloadbalancing/) behind which we have multiple [EC2 servers](https://aws.amazon.com/ec2/) each running a [pm2](http://pm2.keymetrics.io/) service behind an [nginx](https://www.nginx.com/) proxy.

The REST requests from the front end reaches the server without [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) issues:

- without the AWS elastic load balancer and directly to the EC2 server

The REST requests breaks with the CORS errors from the front end and not reaches the server:

- with the AWS elastic load balancer and not directly to the EC2 server

Although we’re not yet successful but [these are the stuff (as per @agentspacecake)](https://forums.aws.amazon.com/thread.jspa?messageID=619662) which we have tried so far:

- Allowed CORS in the [S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/dev/cors.html), example [config](https://gist.github.com/tommoor/4429838) — done
- Allowed CORS in the back end using [CORS node module](https://www.npmjs.com/package/cors) — done
- Allowed CORS in the [nginx proxy using the CORS headers](https://enable-cors.org/server_nginx.html) — done
- Allow CORS on the load balancer’s front — **not done**

Based on my studies so far:

- Per @Max@AWS, we [need to whitelist the “Origin” header](https://forums.aws.amazon.com/thread.jspa?threadID=190886)
- Per @Brian@AWS, we’d [want to whitelist the “Origin” and any other headers you’d like to forward](https://forums.aws.amazon.com/thread.jspa?threadID=156446)
- This was a bug in the [past especially for chrome](https://bugs.chromium.org/p/chromium/issues/detail?id=101805)
- As per @Arun@AWS, [the requests needs to contain the headers which are expected to return](https://forums.aws.amazon.com/thread.jspa?threadID=103604)
- Not sure if the [browser caching could surface the CORS issue](https://forums.aws.amazon.com/thread.jspa?threadID=112772)
- Per @hescar, we can also try [adding a ‘Origin’ header](https://forums.aws.amazon.com/thread.jspa?threadID=103604)
- Looks like, we shall [not use * wildcard](https://stackoverflow.com/questions/16908983/does-amazon-s3-need-time-to-update-cors-settings-how-long/18029490#18029490)
- The AWS staff says that [ELB doesn’t support CORS yet](https://forums.aws.amazon.com/thread.jspa?threadID=147318#527641)
- The feature request to [ELB CORS support still looks open](https://forums.aws.amazon.com/thread.jspa?messageID=508201&#508201)
- The docs says that the [JSON Content-Type is not allowed in simple/actual requests](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/cors-support.html)

>Requests only use the GET or POST HTTP methods. If the POST method is used, then Content-Type can only be one of the following: application/x-www-form-urlencoded, multipart/form-data, or text/plain.

Hope this helps to some extent.
