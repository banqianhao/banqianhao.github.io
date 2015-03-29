---
layout: post
title: Design Patterns--Observer Pattern
category: "Design Patterns"
tags: ["Design Patterns"]
---


###You know the newspaper or magazine subscriptions work:

 1. A newspaper publisher goes into business and begins publishing newspapers.
 2. You subscribe to a particular publisher, and every time there's a new edition it gets delivered to you. As long as you remain a subscriber, you get new newspapers.
 3. You unsubscribe when you don't want papers anymore, and they stop being delivered.
 4. While the publisher remains in business, people, hotels, airlines and other businesses constantly subscribe and unsubscribe to the newspaper.

### Publisher + Subscribers = Observer Pattern


![closerlook](/DL/observerPattern/closerlook.png)

###The Observer Pattern defined: the class diagram


![opd](/DL/observerPattern/opd.png)


`notifyObserver()` may call `update()` of every Observer that had been registered.
