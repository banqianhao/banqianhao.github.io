---
layout: post
title: Design Patterns
category: "Design Patterns"
tags: ["Design Patterns"]
---

Table of Contents:

<ul style="list-style:none">
    <li>
        <a href="#ObserverPattern" style="color:#585eaa"><i class="fa fa-link"></i> Observer Pattern</a>
    </li>
    <li>
        <a href="#DecoratorPattern" style="color:#585eaa"><i class="fa fa-link"></i> Decorator Pattern</a>
    </li>
    <li>
        <a href="#CommandPattern" style="color:#585eaa"><i class="fa fa-link"></i> Command Pattern</a>
    </li>
    <li>
        <a href="#SingletonPattern" style="color:#585eaa"><i class="fa fa-link"></i> Singleton Pattern</a>
    </li>
    <li>
        <a href="#AdapterPattern" style="color:#585eaa"><i class="fa fa-link"></i> AdapterPattern Pattern</a>
    </li>
</ul>

#<a style="color:#000" name="ObserverPattern"><i class="fa fa-link"></i> Design Patterns--Observer Pattern</a>

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


#<a style="color:#000" name="DecoratorPattern"><i class="fa fa-link"></i> Decorator Pattern</a>

###Constructing a drink order with Decorators

We start with our DarkRoast object.

![drink](/DL/DesignPattern/drink.png)

The customer wants Mocha, so we create a Mocha object and wrap it around the DarkRoast.

![drink1](/DL/DesignPattern/drink (1).png)

The customer also wants Whip, so we create a Whip decorator and wrap Mocka with it.

![drink2](/DL/DesignPattern/drink (2).png)

Now it's tome to compute the cost for the customer.

1. First, we call `cost()` on the outmost decorator, Whip.
2. Whip calls cost() on Mocha.
3. Mocha calls cost() on DakRoast.
4. DarkRoast returns its cost, 99 cents.
5. Mocha adds its cost, 20 cents, to the result from DarkRoast, and returns the new total, \$1.19.
6. Whip adds its total, 10 cents, to the result from Mocha, and returns the final result--\$1.29.

###The Decorator Pattern defined

![decoretordefine](/DL/DesignPattern/decoratordefined.png)

###Example: The Beverage code
{% highlight java linenos %}
public abstract class Beverage {
    String description = "Unknown Beverage";
    public String getDescription() {
        return description;
    }
    public abstract double cost();
}

public abstract class CondimentDecorator extends Beverage {
    public abstract String getDescription();
}

public class Espresso extends Beverage {
    public Espresso() {
        description = "Espresso";
    }
    public double cost() {
        return 1.99;
    }
}

public class HouseBlend extends Beverage {
    public HouseBlend() {
        description = "House Blend Coffee";
    }
    public double cost() {
        return 0.89;
    }
}

public class Mocha extends CondimentDecorator {
    Beverage beverage;
    public Mocha(Beverage beverage) {
        this.beverage = beverage;
    }
    public String getDescription() {
        return beverage.getDescription() + ", Mocha";
    }
    public double cost() {
        return 0.20 + beverage.cost();
    }
}

public class OpenCoffee {
    public static void main(String args[]) {
        Beverage beverage = new Espresso();
        System.out.println(beverage.getDescription() + " $" + beverage.cost());

        Beverage beverage2 = new HouseBlend();
        beverage2 = new Mocha(beverage2);
        beverage2 = new Mocha(beverage2);
        beverage2 = new Whip(beverage2);
        System.out.println(beverage2.getDescription() + " $" + beverage2.cost());
    }
}
{% endhighlight %}


#<a style="color:#000" name="CommandPattern"><i class="fa fa-link"></i> Command Pattern</a>

In object-oriented programming, the command pattern is a behavioral design pattern in which an object is used to represent and encapsulate all the information needed to call a method at a later time. This information includes the method name, the object that owns the method and values for the method parameters.

![command](/DL/DesignPattern/command.png)

{% highlight java linenos %}
public interface Order {
    public abstract void execute();
}

// Receiver
class StockTrade {
    public void buy() {
        System.out.println("You want to buy stocks");
    }
    public void sell() {
        System.out.println("You want to sell stocks ");
    }
}

// Invoker
class Agent {
    private m_ordersQueue = new ArrayList();

    public Agent() {
    }

    void placeOrder(Order order) {
        ordersQueue.addLast(order);
        order.execute(ordersQueue.getFirstAndRemove());
    }
}

//ConcreteCommand
class BuyStockOrder implements Order {
    private StockTrade stock;
    public BuyStockOrder (StockTrade st) {
        stock = st;
    }
    public void execute() {
        stock.buy();
    }
}

//ConcreteCommand
class SellStockOrder implements Order { 
    private StockTrade stock;
    public SellStockOrder (StockTrade st) {
        stock = st;
    }
    public void execute() {
        stock.sell();
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        StockTrade stock = new StockTrade();
        BuyStockOrder bsc = new BuyStockOrder (stock);
        SellStockOrder ssc = new SellStockOrder (stock);
        Agent agent = new Agent();

        agent.placeOrder(bsc); // Buy Shares
        agent.placeOrder(ssc); // Sell Shares
    }
}
{% endhighlight %}

#<a style="color:#000" name="SingletonPattern"><i class="fa fa-link"></i> Singleton Pattern</a>

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



#<a style="color:#000" name="AdapterPattern"><i class="fa fa-link"></i> Adapter Pattern</a>

The Adapter Pattern converts the interface of a class into another interface the clients expect. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.

### Object Adapter

![objectadapter](/DL/DesignPattern/objectAdapter.png)

### Class Adapter

![ClassAdapter](/DL/DesignPattern/ClassAdapter.png)




