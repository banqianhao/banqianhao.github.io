---
layout: post
title: the Decorator Pattern
category: "Design Patterns"
tags: ["Design Patterns"]
---

###Constructing d drink order with Decorators

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



