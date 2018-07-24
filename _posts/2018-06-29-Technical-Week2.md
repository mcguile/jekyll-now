---
layout: default
title: 7. Technical - Getting the Data We Need
categories: saltire
comments: true
---

Hi, all. These blogs are going to become less organised and more rambling as the weeks here go by. I blame the heat. The rigid structure of writing one blog per week seems forced. Sometimes I do nothing; sometimes I do lots of things. From here on out consider these posts without a timeframe. Just know that they are still at least sequential.

At the end of last week I had managed to settle upon the database structure for this project and I refactored Bryan's EV ARC script. The script still posts to his SQL database, though, not my brand new, shiny Firestore. Before I attempt to post any data to Firestore, I first need to know what data to post. A lengthy chat with Bryan gave me the details I needed. Aside from Bryan's inverter data, I also need to get data from the chargers themselves. Unfortunately for me, it's not just one company that they buy from, it's two, and any ARC when built could use one or the other, or a combination of the two. So, I need to access two APIs (an interface between me and the charger company's data) to get the information I need.

The data I can get back is endless. Both companies not only have the means to tell you the current state of the charger, like the amperage, voltage, savings, time left to charge, etc., but they can also give historical data, like session start and end times, durations, and energy consumed. The document which demonstrates how to request the data for one company, ChargePoint, is over 120 pages long. 

After devouring those thrilling reads, I set about JuiceBox's API first. Using Python's *requests* library it was simple enough. The *requests* package handles all the hard stuff for me - I only need to give it a URL and some extra authentication info and I get a response in a JSON format. For example, {"Charging": {"Amperage": 12, "Voltage": 57,...}} - and this is fairly straightforward to parse into a dictionary format I can upload. 

Next is ChargePoint. They return their data in a format called SOAP. I’d never even heard of that one before. It looks horrendous and is equally horrendous to parse into usable data. If anyone has ever done any programming before you should understand that this is not easy to work with. It took me quite some time to figure out ways to get the data I want. I managed to find a Python package called *XMLtoDict* that does as it says on the tin. As SOAP is actually a form of XML, I can convert the response to a Python dictionary, exactly the format I want, then just loop through the dictionary keys looking for specific keywords and adding their values to my upload data. 

Simple enough, right? Well, no, because I’d forgotten that there is no package installer on the router like *apt-get* or *yum*, and their definitely isn’t any Python package installer like *pip*. If a package needs to be installed on the router, just like this *XMLtoDict* does, every single package which the the first package depends upon also needs to be installed. We *can* install packages, as long as they are compiled from source without dependencies. So, the big question: *are there dependencies for XMLtoDict*? I left this one for Bryan as I prayed. He’s been good at taking my problems and coming back with solutions. And this time was no different. He could install it with one or two small dependencies installed beforehand. Good stuff.

I figured I’d test it myself on the router before moving on. Little did I know that even though Bryan had successfully installed *XMLtoDict*, he never actually tested anything else. Which is fair because that’s all I asked him to do and I’ve been writing the entire codebase. It turned out we (read: I) completely forgot about the *requests* package. The package that is absolutely required so I can call upon the APIs and actually get any data. Without calling the APIs, we have no data, we have no database, and we certainly we have no apps. Off Bryan went again with my problems; only this time he didn’t return so quickly. When he did, he said couldn’t install it without a million other dependencies. He tried but every sequential installation just took him further down the rabbit hole. 

So here I am, baffled. How am I meant to solve this one?

