---
layout: post
title: Design Patterns--Singleton Pattern
category: "Design Pattern"
tags: ["Design Pattern"]
---

There are many objects we only need one of: thread pools, caches, dialog, boxes, object that handle preferences and registry settings, objects used for logging, and objects that act as device drivers to devices like printers and graphics cards. In fact, for many of these types of objects, if we were to instantiate more than one we'd run into all sort of problems like incorrect program behavior, overuse of resources, or inconsistent results.

### how

{% highlight java linenos %}
public class Singleton {
    private static Singleton uniqueInstance;
    // other useful instance varuables here

    private Singleton() {}

    public static synchronized Singleton getInstance() {
        if (uniqueInstance == null) {
            uniqueInstance = new Singleton();
        }
        return uniqueInstance;
    }

    // other useful methods here
}
{% endhighlight %}

Or move to an eagerly created instance rather than a lazily create one.

{% highlight java linenos %}
public class Singleton {
    private static Singleton uniqueInstance = new getInstance();

    private Singleton() {}

    public static Singleton getInstance() {
        return uniqueInstance;
    }
}
{% endhighlight %}

Use "double-checked locking" to reduce the use of synchronization in getInstance().

{% highlight java linenos %}
public class Singleton {
    private volatile static Singleton uniqueInstance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (uniqueInstance == null) {
            synchronized (Singleton.class) {
                if (uniqueInstance == null) {
                    uniqueInstance = new getInstance();
                }
            }
        }
        return uniqueInstance;
    }
}
{% endhighlight %}




