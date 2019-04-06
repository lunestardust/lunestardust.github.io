---
layout: post
title: CHROME_DEV_NOTE 01 Sending DOM content to serial port
date: 2019-04-06 18:37:24.000000000 +08:00
---


The post explains the method of sending DOM content to serial port by cross-extension messaging

### Difference between Chrome Apps and Extensions

In the first place, please read the two posts [What Are Chrome Apps?](https://developer.chrome.com/apps/about_apps) and [What are extensions?](https://developer.chrome.com/extensions).

Recently, I was asked to build a project,
in which a part of web page content should be sent to serial port.
I decided to accomplish the task by Chrome Extensions.
Well, 
I found that it is impossible to access serial port in an extension.
Then, 
I tried to use Chrome App.
Unfortunately,
an App cannot get DOM content.

The case indicated that
an extension is CLOSE to webpage
while an App is CLOSE TO system.

### Message passing between extensions and apps

My final solution was
combining an extension with an App.
This is implemented by [cross-extension messaging](https://developer.chrome.com/extensions/messaging#external).
The [externally_connectable](https://developer.chrome.com/apps/manifest/externally_connectable) was declared in the App.

### No future
Google has announced that
> Chrome will be removing support for Chrome Apps on Windows, Mac, and Linux. 

So...That's it. Enjoy!
