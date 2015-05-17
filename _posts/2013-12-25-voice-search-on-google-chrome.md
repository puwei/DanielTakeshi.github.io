---
title: Voice Recognition on Google Chrome
author: Daniel Seita
layout: post
permalink: /2013/12/25/voice-search-on-google-chrome/
geo_public:
  - 0
categories:
  - Computer Science
tags:
  - Chrome
  - Google
  - voice recognition
---

<img src="{{site.url}}/assets/GoogleVoiceRecognition.png" alt="googlevoice">

About a month ago, Google Chrome released [voice search and voice action][2]. The main idea is that
we can literally just talk to the computer while browsing Google, and it will respond with (ideally)
what you wanted. This feature isn&#8217;t limited to just browsing Google, though. It&#8217;s also
possible to tell Google to start an email, or to find information about people in your contacts
list.

To use it, open Google, click on the microphone and wait until Google prompts you to say something. But if one has to click on a microphone, it wouldn&#8217;t make sense to use voice recognition because we can type almost as fast as we can talk. (It seems like this feature is built for mobile users, where typing is typically a lot slower.) So there is now a Google Voice Search Hotword extension, so one can avoid typing at all by saying &#8220;OK Google.&#8221; For details, refer to [their article][3] about the extension. As one can see, it&#8217;s still in beta (at the time of this blog post), so this is all recent technology. In fact, Google suggested that they released this feature so that people cooking for Thanksgiving didn&#8217;t have to wash their hands in order to use Google.

<span style="line-height:1.5;">The voice extension sounds nice at first, but there&#8217;s always the unfortunate caveat in voice recognition: it&#8217;s not good enough due to a variety of reasons, such as multiple words sounding the same, uncommon words, inconsistent or unclear speech, and so on. In fact, for users of Gmail, I sure hope that this voice recognition won&#8217;t immediately send emails created out of voice recognition without user confirmation, since there&#8217;s too much that could go wrong with that feature.</span>

But maybe I&#8217;m just naturally pessimistic about the success of voice recognition, especially after trying to search my own name on Google and getting &#8220;Daniel C Town.&#8221; I know that no voice recognition software has any chance of recognizing my last name. What I wonder is if this Google feature will be able to remember my browsing history *after* I say my name and, in the future, use that data to correctly identify it via voice recognition?

Still, voice recognition is certainly an important aspect of applied artificial intelligence and machine learning, so I look forward to seeing this subfield progress.

To recap:

  1. Can be useful under limited circumstances (dirty hands, quick browsing, etc.)
  2. Will probably be far more popular on mobile devices
  3. Hindered by the natural limitations of voice recognition
  4. Potentially a privacy concern
  5. Definitely opens up additional areas for future work/research

 [1]: http://seitad.files.wordpress.com/2013/12/googlevoicerecognition.png
 [2]: https://support.google.com/chrome/answer/1331723?hl=en
 [3]: https://support.google.com/websearch/answer/3542118
