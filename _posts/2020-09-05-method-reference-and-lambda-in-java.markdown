---
layout: post
title:  "Method Reference and Lambda in Java"
date:   2020-09-05 00:00:00+02:00
categories: java
---
> DISCLAIMER: The views and opinions expressed here are those of the author and do not necessarily reflect the official policy or position of Devoteam. Any content provided by our bloggers or authors are of their opinion and are not intended to malign any religion, ethnic group, club, organization, company, individual or anyone or anything.



# The Mystery of Method Reference in Java
If you google Method reference in Java, all of these example will eventually lead you to [Oracle's official tutorial](https://docs.oracle.com/javase/tutorial/java/javaOO/methodreferences.html). The example from Oracle is a little bit unclear and less extensive. But let me give you the basic idea of method reference before diving deep into the problem.
If you have basic Lambda expression of `a`, where `a` is of type `String`, then 

>  `(a) -> a.equals(b)`

is a valid lambda expression. The method signature is `public boolean equals(Object o)`. Thus `b` can be another object to compare with (practically you would want to use `String`).
Thus, with better readability, you could write the best out of functional programming in Java:

> `a::equals` 

If you want to deep dive on this, you could go first to the concept of Lambda by Alfonso Church. It's rather abstract and confusing. But i will write here the general idea to help you with. This is quite important since the strictly typed Java language will know at compile time if you provide the wrong type in your lambda expression, as i stumbled upon this many times. I simply don't understand it. <br/>
Alright. <br/>
Church ambition was to create an abstraction of mathematical expression such that with that abstraction you can do some arithmetic out of it.

> f(x) = x + 1

simple enough. Every variable of `x` will be transferred to `f(x)` and thus will produce, say for `x=1` , 2. <br/>
Can you abstract away this operation such that you can make an operation **about** `f(x)` ? What if i could say 

> `ℷx.M[x]`

This means that you have a description about `x` ( that is `ℷx`) that has a well-formed construction of a particular operation (`f(x) = x + 1`).  Remember that `x` here is not the variable like you usually put in your Algebra. But it is another abstract layer of that function. Church proudly presented this as a *type free* operation. This is the kind of operation that, within its notational system, sustains no contradiction in any symbolic manipulation you want to make.

Now think about that in Java. JDK provides you the many functional interface like `Predicate`, `Consumer`, `Supplier`, or something of your own. And you can make many operations with the concept of Lamda, where type operation is provided and thus can be manipulated within its own notational system. In the previous Java example, it should be easy to grasp: i want to make an operation *about* a String where method (in this case instance method) `equals` has to be used. I don't care about the actual value of `a`, whether it is `"James"` or `"Nothing"`.

# Now The Perplexity
JDK or Oracle will give you the list of kind of method reference that you can apply for this:
1. Reference to a *static method*. Easy enough, just use `String::join`. `join` method signature is `public static String join(CharSequence delimiter, CharSequence... elements)`
2. Reference to an *instance method* of a *particular object*. Just like i mentioned about: `a::equals`. `a` is that particular object
3. Reference to an *instance method* of an *arbitrary object*. This is quite hard. Arbitrary means that you do want to use some operation without knowing the order which one is manipulated under. A better way of rephrasing this is by saying which instance method that we are going to use using number of parameter. Say following:
> `String[] strings = {"a","b","c"};  Arrays.sort(strings, String::compareToIgnoreCase);`
<br/> `compareToIgnoreCase` receives a `String` as a parameter and in this case you want to use any arbitrary object to as a parameter and to compare it with different oject. Say another example is `BiConsumer<String,String> bicns = String::compareToIgnoreCase;`
4. Reference to a constructor. In Java, somehow you can treat the keyword `new` if it's a method. `SomeClass::new` is somehow awkward but possible. This reminds me that when you have a nested classes, you would instantiate that inner class like `new OuterClass.new InnerClass();`

### So back to the point 3... 
The actual comparison in method `sort` of `Arrays` utility class is being done or calculated by the some logic. The `sort` receives parameters `T[]`, which is generic `T`  (if you don't understand this, i will try to cover later. You can try to read [Benjamin Pierce's Type and Programming Language](https://www.cis.upenn.edu/~bcpierce/tapl/) as a starter) and `Comparator<? super T>`, which is a functional interface with lowerbound wildcard of generic `T` (which means you can provide any other object from `T` up to `Object` ). The lambda expression in Java captures all of the manipulation of the types very well: it knows that the method reference of `compareToIgnoreCase` has to be implemented such that you have two parameters to do the operation. As such it could fit `BiConsumer` interface.
> `BiConsumer<String,String> bc = String::compareToIgnoreCase;`

in a way that the operation or in the form of Lambda of Church `M[x]` will take the two types, say `a` and `b`, and do something like `a.compareToIgnoreCase(b)`, or in the java lambda: `(a,b) -> a.compareToIgnoreCase(b)`. Remember that `BiConsumer` has generic `T` and `U` as inputs, which in case of `bc` above, `String` for both arbitrary operations between `String` in `compareToIgnoreCase`. And the specification of both type have to be both `String` and `String` (or `CharSequence`, but since `String` `implements` `CharSequence`, they arey interchangeable), which is true in `compareToIgnoreCase` case (no pun intended). 

## Practical things to remember
If you find this so abstract to understand, i will give you some key takeaways. 
You want to have an abstraction of operation/application from Types. First, you want to know whether to use *Static methods* or *instance methods* (constructor in this case is also instance method). 
### Which one is to use? 
First check the parameter(s) of that method and the return type. And see if you *need* operation on that parameter's Type. If you need operation on *any* Type, doesn't matter which object, then you should use the `Type::methodName` pattern. For example, while `thisIsAString::isEmpty` doesn't work on an instance of `thisIsAString`, code `String::isEmpty` works on arbitrary object, especially if you want to declare it to a reference `Consumer<String>`. The former is trying to make a lambda operation based on specific instance or reference of a Type that is really not type free, but bound to a variable. Whereas `String::isEmpty` is not bound to any type or instance. <br/>
If you take `thisIsAString` and do this `Predicate<String> prdct = thisIsAString::startsWith` do you think this compiles? <br/>
This compiles because `startsWith` expects an *operation* of the parameter object `String`. There is an expectation to implement this method such that when `prdct` is used, it expects that implementation to be *concrete*:
> `String a = "a"; prdct.test(a); // depends how you declare thisIsAString` <br/>

which reads *my operation is to be that `startsWith` an object `thisIsAString` and impose that rule on object `a`* 
But what about `Consumer<String> cnsm = String::equals` ? This doesn't compile? It turns out, again, the abstraction of the operation doesn't work. Here is the lambda operation: `(a,b) -> a.equals(b)` What's wrong? Because there are two Types needed to accomplish this lambda operation and `Consumer` has a parameterized Type `<U>`. Thus it is correct if we use `BiConsumer` which is parameterized with `T` and `U`.

### Church's Formal Definition
Church's idea is pretty good and fundamenal to today's programming practices. The abstraction is quite hard but i can write in much simpler words:

> (*Specification*)[**Identifcation**] *application*

In the example above, `ℷx.M[x]` gives you an idea about how this works. But there is a better abstraction: `(ℷx)[f(x)]g` such that it equals to `g(x)` and equals to `x+1`. The `(ℷx)` is the *Specification*, the `f(x)` is **Identification** and g is the *application*. We have mentioned this word *application* many times, which we phrased it as operation. 