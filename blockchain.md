---
layout: page
title: Blockchain
permalink: /blockchain/
---

# State Machine Replication
What a name! I never studied computer science, but after i jumped myself in as a Java programmer, i have seen a consistent problem in all of my past projects: how do we keep all different applcations consistently sharing the same information when the state changes from one to the other state. This might be trivial question, but the impact is quite serious in real world project.
The seminal paper of [Leslie Lamport](https://web.archive.org/web/20170123205550/http://research.microsoft.com/en-us/um/people/lamport/pubs/byz.pdf) formalizes this consistency problem as Byzantine Fault Tolerant

# A course on Distributed System
This [course](http://www.distributedsystemscourse.com/) is very awesome by the way.


# Dfinity
Many blockchain projects have been hindered with the promise of the new architecture, especially because the consistency of all states bring up more perils than promises. The one example that comes to my mind is the file storing problem. You would want to store files in your OS filesystem, but to do so in blockchain presents a challenging problem in the state of the universe of blockchain. <br/>
Some people come with an idea of Interplanetary File System (IPFS). It is a nice workaround and it gives you a separate universe where in that universe you just have to make another state machine for files only and your blockchain reads it from that universe. You would have a filesystem not embedded in your blockchain. <br/>
Maybe to explain a bit more on this problem, state consistency has been a problem in computer science. Eric Brewer has pointed out, in his CAP theorem, that in order to achieve three general problems of Consistency, Availability, and Partitioning, you have to sacrifice one of them to gain at most the two. You can't get availability by partitioning and expecting the state of the machine is consistent.<br/>



# A potential Project
1. An open Investment, where users are allowed to get some network to discuss and value an investment. 
The discussion will open some participations and involvement and will get paid with some percentage from the original owner of the idea. 
We charge the user from using the platform. This is business model is typically small in margin.
2. An insurance company where the users are invited to use the platform by some incentives at the beginning and work together towards increasing the size of the company
3. eCommerce web portal, where we provide a web portal for any company or individual. This eCommerce will be the safest, most secure portal in the history of secure internet without any additional layer of protection. There should be a road map where this eCommerce will take on the payment platform as well. 