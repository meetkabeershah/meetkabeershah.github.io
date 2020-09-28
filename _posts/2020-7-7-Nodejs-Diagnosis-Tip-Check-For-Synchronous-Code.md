---
layout: post
title: Node js performance diagnosis tip - Check for synchronous code in Nodejs process
---

Check for synchronous code in Nodejs process:
The command line utility `--trace-sync-io` tells us about synchronous tasks.

Example use:

`node --trace-sync-io index.js`

The Node js runtime provides the --trace-sync-io command-line utility:

https://nodejs.org/api/cli.html#cli_trace_sync_io

This utility can find the synchronous blocking code sections in a Node js project. Synchronous code can be replaced with an asynchronous code to amplify the performance of the project. 