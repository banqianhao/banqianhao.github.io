---
layout: post
title: Design Patterns--Command Pattern
category: "Design Patterns"
tags: ["Design Patterns"]
---

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

