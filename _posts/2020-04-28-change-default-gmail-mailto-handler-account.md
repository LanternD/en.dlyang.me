---
layout: post
title: Change Default Gmail mailto Handler Account
description: A method to select the account for processing the mailto links if there are multiple accounts in the browser.
permalink: /change-default-gmail-mailto-handler-account/
categories: [blog]
tags: [Gmail, account, mailto]
date: 2020-04-28 11:28:37
---

# Note

I came accross this problem when I visited [Shimmy1996's blog](https://www.shimmy1996.com), which uses email as comment system.

I found that Gmail uses the first account as the default to handle the `mailto` links. You have to change the link manually (from `/u/0` to `/u/1` things like that) to switch to another account.

Shimmy pointed out a way to deal with it, changing the default account to handle the link.

# Tutorials

[Getting Gmail to handle all mailto: links with registerProtocolHandler](https://developers.google.com/web/updates/2012/02/Getting-Gmail-to-handle-all-mailto-links-with-registerProtocolHandler)

This link shows how to add Gmail as the mailto handler in the browser. What we need to change is revising the link in the configuration.

In the Gmail tab/window, open JavaScript console, enter the following:

```javascript
navigator.registerProtocolHandler(
    "mailto",
    "https://mail.google.com/mail/u/1?extsrc=mailto&url=%s",
    "Gmail"
);
```

Change the `/u/1` to whatever account you want. Press <kbd>Enter</kbd> and done.

Now you should be able to use the new account to reply emails.

---

BTW, I found an interesting [text art](https://twitter.com/reddit/status/1254877928677969920?s=20), share it here:

```html
|￣￣￣￣￣￣￣￣￣|
|  Pls continue |
|    social     |
| distancing if |
|  ur able to   |
|＿＿＿＿＿＿＿＿＿|
(\__/)  || 
(・ ㅅ ・) || 
/ 　 づ
```

(I modified some characters to achieve satisfying visual effect.)
