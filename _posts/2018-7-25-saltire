---
layout: post
title: 9. Woah, We're Halfway There!
categories: saltire
comments: true
---

It's the seventh week here at Envision Solar. By now I'd like to have finished the first prototype of the Android app and already moving on to the iOS app. Whilst android has almost been completed, with just a few things like visuals and animations to implement, iOS hasn't even begun. The database structure is changing all the time due to the functionality of the app changing. Adding in historical data is the real challenge. Selecting a date to view data and pulling all EV ARC documents from that date counts as one read per document, not per call. This isn't an issue if I'm pulling totals up to the current date because I can order the DB docs and pull the last X amount only. If a user wants a split time frame, i.e. "Get me all of December 2017", then my DB structure can't handle that. It would require reading all the documents from December until the current date, and then filtering for the ones we want. That's a lot of reads.

On another note, I spoke with a couple of the sales guys and got them to critique the app. Theyre happy with the look and feel overall and gave me some good advice about adding in error notifications. At least that way the user doesn't need to regularly open the app to see if there's anything wrong with their systems. Unfortunately we may be running out of time for additional features at the moment. Push notifications aren't a quick job. They need to be handled by Cloud functions on the database as well as by a fair amount of code client-side. We currently aren't using cloud functions, so it would require some documenatation consuming before even attempting it.

There was also the suggestion to implement weather information for each ARC so that an owner can see perhaps why their system isn't producing much solar. Good idea. I found an open source API to access weather info using geo-coordinates, complete with weather icons to match. There is a 60 max limit on how many API calls can be made per minute before having to start paying for the service, however, I don't see that being an issue right now. The company has fewer than 200 EV ARCs out there and, even with the expected growth, the way I've implemented the weather call is such that it requires a manual refresh client-side. Someone could always attempt to sit there and refresh their data as fast as possible, of course, but then it would just terminate the call whilst their EV ARC data would still refresh. Good stuff.

Still, even with Android being mostly completed, I feel like I need to work faster to get on top of this. It doesn't help that compiling each time on my device to test the app takes minutes at a time but that's no excuse - that's all a five-year-old laptop can do! 

At least the design for the app is out of the way. The aesthetics could be due a change, though; I'm no artist. However, the navigation and flow of the app seems to be fully settled upon. This means I can work pretty quickly on developing the navigation for iOS. I just need to learn the programming language first... 

Less than four weeks to learn Swift for iOS, develop the codebase, finalise the database structure, and to test both applications. Wish me luck!

[Previous Post](saltireeight.html) | [Next Post](saltireten.html)
