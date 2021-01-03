---
layout: post
title:  "Streams of Logic in Java"
date:   2020-09-19 00:00:00+02:00
categories: java
---
> DISCLAIMER: The views and opinions expressed here are those of the author and do not necessarily reflect the official policy or position of Accenture. Any content provided by our bloggers or authors are of their opinion and are not intended to malign any religion, ethnic group, club, organization, company, individual or anyone or anything.


When Sanjay Ghemawat and Jeffrey Dean published their phenomenal paper [Map Reduce](https://research.google/pubs/pub62/), the whole world was taken by storm by the design of these two simple and powerful functions: **Map** and **Reduce**, hence the name. Ghemawat's work on on [Google File System](https://research.google/pubs/pub51/) was the harbinger of this MapReduce idea. It's very much a very influential Distributed System Design to the whole world of Computer Engineering. It's not a surprise if you see in great detail that Apache Kafka is built with a very similar design to Google File System. Dr. Ghemawat is very influential in the industry, especially in Distributed System. It's not a coincidence i think that he was supervised by a Dutch Professor at MIT, Frans Kaashoek, who has been very influential in the same domain of Distributed System (look at his very [easy-to-read book](https://ocw.mit.edu/resources/res-6-004-principles-of-computer-system-design-an-introduction-spring-2009/online-textbook/faults_open_5_0.pdf) )<br/>

Even Java Streams API couldn't resist to get this idea implemented in JDK 8 (of course Joshua Bloch, one of the architects of Java, is employed by Google). If you see carefully how they build the reduce function (or *fold* as they phrase it), then you would see the similarity. Take a look at how Map Reduce works: you take any input, say list of strings, put it into several workers (the **Map** phase). Prior to that the Master has to *fork* the workers, administer the job, and do the **Reduce** phase where we different (reduce) workers take all the intermediate results and combined those with the same key and append the result of the same key (with the same order when it was mapped). Very neat and simple. 
Let's see how a functional programming with Stream in Java works in an example.

```
var list = List.of("c","a","d","t");                \\ line 1
Stream<String> someStream = list.stream();          \\ line 2
Predicate<String> isItD = string -> !string.contains("d");
String word = someStream                            \\ line 4
                    .filter(isItD)                  \\ line 5
                    .reduce( (a,b)-> a.concat(b));  \\ line 6
System.out.println(String.format("the word you received is : %s",word));// prints "cat"
```
It's very neat right? This is why i think Java can still be a winner compare to Scala, especially with the feature of Lambda and Stream. But the logic runs deeper than you think. It has the magic that Dr. Ghemawat introduced in 2004. The Stream API allows you to do this MapReduce processes in a manner of a fault-tolerant way. This doesn't look like that in the cover of how you write the code. At line 2, you just have to get the stream with `stream()` method. It then returns the `Stream<T>` interface of that particular type. Alluding to the MapReduce, Java refers the **Map** step at line 2. Well, you actually just map it to a Stream in this case (say a particular Object in the heap). But the good example of MapReduce is when you actually call:

```
Stream<String> someStream = list.parallelStream();
```
This will produce many `Stream`s that can be described as *workers* (in MapReduce term). And yes, you are now mapping it into a worker. The stream is processed in parallel. One has to notice that the javadoc of this function doesn't really say that it *will be* parallel. To quote: 
> Returns a *possibly parallel* {@code Stream} with this collection as its source.


Possible. This makes it really hard to understand how exactly parallelism is conducted in Streams. Maybe if you really need something parallel, one has to choose Multithreading option in Java. Furthermore, it could be true that Stream of Java is not actually a MapReduce implementation. But despite that fact, it is true that the `reduce()` method line 6 from the above code shows that it actually process the element of the stream (and if `parallelStream` is making a parallel workers, then it is actually a MapReduce imeplementation!)<br/>
### Forward.
Reduce is the operation where you aggregate the right workers with the same keys to produce the result. In Java streams, this process is counted towards the Terminal phase. Java Streams describes this process in a pipeline fashion: input, processes, output. The processes are series of **Intermediate** jobs and *a***Terminal** process (once a Stream is terminated by a Terminal process, that's the end of it. YOLO!). The terminal processes are more important: it's rather useless to invoke intermediate if there is no Terminal. How this is implemented is still a mystery to my eyes.  <br/> In line 5, this is where the intermediate job in the pipeline takes place. It filters the stream to possible operations. The Lambda here is very fancy to make things more functional programming than imperative. If you see there, it's very easy to read and some people call it a *stateless* way of programming: you actually use symbolic manipulation to get the job done rather than manipulating many `var` or variables in order to get what you need. <br/>

## Data is the new Oil ?
It turns this way of programming is really handy and neat to be used. You can query many of these complicated relational databases and their tables and get the result really quickly just by using Java streams. You create a POJO of a Person object and get to the Person table (use JDBC, get the right database pool, etc), and you just have to query all the data in your Business Logic Tier with Streams and your code will be easy to read. If you could harness a really good design on your data pipeline, it will produce many insights and profitability in the business (something that i have to elaborate more in different post). One particular example that is really important at the moment is the implementation of Apache Kafka. <br/>
Kafka is an even-based, fault-tolerant streaming platform, where anyone can stream their data into the platform and retrieve the data from other ends. The platform stores the event in the append-fashion log files, which is written into many partitions. The platform is using MQTT protocol (the pub-sub communication) to stream from one producer to log (or *Commit Log*) in a topic and replicate the topic into various partitions of Commit Log. The consumer then can consume that event from the Commit Log.