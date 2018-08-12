---
layout: post
title: 10. Programming - Testing is Crucial
categories: saltire
comments: true
---

Earlier in these blogs, I was talking about the Python scripts I needed to write so that data from Envision Solar’s systems could be posted to a database. I had left the scripts relatively untouched since I wrote them in the first or second week of the internship. Data I am using for my Android and iOS apps is pulled in from the charger companies using these scripts. This data, for the most part, is a dictionary, or is converted to a dictionary by some code I wrote. Dictionaries are useful because they provide key-value pairs, much like a database does - i.e. Age: 25, Sex: Male, Location: San Diego (MSN reference there for anyone over the age of 20). 

The *key* of a dictionary will usually be a string, a piece of text, but the *value* can be any data type, so we must be careful when dealing with them. I thought I was careful - type-checking, key-checking, and even using recursion for nested dictionaries - but the script crashed when Bryan tried to run it on real systems this week. I expected some crashes. I left extensive testing until the end purposely. But I was not expecting a crash like this one.

Most of my programming solutions at university or in coding challenges have been easily debuggable, especially for algorithms. Data goes in, expected results are calculated, and these results compared against actual results. Generally the *form* of the data are known, so it is easily fixed when something goes wrong. By form, I mean that if an algorithm has an input of an array of integers, for example, then we can perform our operations on this data in a very safe manner. It will not crash because *we know* each element in the array is an integer, and so we are only executing method calls or data manipulation to suit this data type. So, let’s figure out why my script crashed and fix it.

Code:

```python
portList = _finditem(dict,"Port") # recursive function to get array of port status dictionaries
    for i,port in enumerate(portList):
        for k,v in port.iteritems():
            if str(k)=="Status":
               # we’ve found what we were looking for
```

Error: 

```python
*’str’ object has no attribute ‘iteritems’*
```

In this code, I check to see if a key called “Port” exists. I use a recursive function to do so because the data is nested. If it does exist, I *know* that the value of this key is an array of dictionaries. Each element in the array is some status information about a charger port on Envision’s systems. I then loop over all ports in the array, get key-value pairs from the dictionary of that port, then check if a key of “Status” exists to finally get the paired value.

**So why the crash?** 

The crash log is showing that a port I looped over does not have the capability to call the method *iteritems*, implying it is not a dictionary. Weird. It has to be. I *know* it is. Time to debug.

If there is more than one port, then we have an N-element array of dictionaries for the status of the ports. That’s good. That’s what I planned for. The logic, then, is that if there is one port only, their will *still be* an N-element array, just that now N=1. So why, oh why, did the programmer who wrote the code for this charger’s API decide *“if there are many ports we return an array; if there is one port we return a dictionary”*?!

It is actually **more difficult** to write code to change your data format in one specific case than it is to just leave it alone, and it clearly just confuses developers on the end of their API. Maybe someone out there can comment as to why this programmer’s code would ever be a good idea in the real world. I have never seen anything like it before. 

Luckily, it was a quick fix in the end, but one I feel should have been unnecessary. I will be sure to not trust instinct when utilising other people’s code and test it properly beforehand. Sometimes there is a difference between *knowing* you are right and ensuring you are.

[Previous Post](saltirenine.html) | [Next Post](saltireeleven.html)
