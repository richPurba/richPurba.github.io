---
layout: post
title:  "Where the money goes"
date:   2020-07-04 00:00:00+02:00
categories: investment
---

# Do you care about your money?
Such a strange dream i had as a kid. I was amazed by high net-worth individuals around the world. Little did i knew about how the media defined 'net-worth'. The more i realize now that these individuals know how to make a good invesment thus net-worth is a slightly misunderstood term. They simply earn their net-worth not from accumulating balance on their bank account!

In the famous Marshmallow Experiment at Stanford, researcher discovered many children who can resist the temptation of eating  marshmallow so they could wait a little bit longer are the kids who, later in their 30s, have been very successfull in life (financially maybe? Or achievements?). 
If you could wait longer, you could benefit better. I remember an article on Harvard Business Review challenged this experiment (can't recall on which edition it was). The authors claim that these individuals have to have purpose first in order to wait longer (in the Marshmallow experiment, of course, the purpose is to get Marshmallow).
Makes sense. 

# Some studies
I hate to say that sometimes i follow the stories of many CEOs and successful entreprenurs just so that i can carefully take some steps in my career. I read the stories from Stephane Kasriel, Dan Bricklin, Peter Thiel, Jim Whitehurst, Ben Horowitz, Andy Grove, Jeff Bezos, and others (nothing important in the order). 
These people are so inspiring but i fear that their achievements blind me to imitate their paths. Thus 'inspiring' is always a dangerous thought. And yet, Peter Thiel speaks out loud about this: the next Mark Zuckerberg, won't be a social network inventor, the next Bill Gates won't create Operating System. If you don't understand this, then you clearly never read history. 
Of course, like Marc Andressen, Peter's voice is like a jiminy cricket's on my shoulder when i have any desire to be a great entrepreneur. 
> What valuable company is nobody building?

# Ideas worth investing
I want to build a company. It's been my childhood dream. But the time is not now. I have tried with many past ventures, but failed. 
 - A platform of freelancer
 - A bank
 - Operating System with blockchain
 - Browser with blockchain

# Dfinity platform
If you didn't know [dfinity](https://dfinity.org/), it's probably the most outstanding practical blockchain out there. We've seen many blockchain projects (like Ethereum), but most of them (if not all of them) are out of touch with reality. 

The Threshold Relay is probably the best idea in Dfinity. It highlights how deep the understanding of cryptography of the team to solve the Byzantine Problem in Computer Science (after Leslie Lamport). The calculation of the final consensus of a state is much faster than Etherum, consider that the Proof of Work (Proof of Stake for Ethereum) calculation is much different than calculating all the hash from all participants at a given time, implicating the need of theoretical ecoonomics to prevent obvious threat model such as 51% attack or nothing at stake. 

In his a very thorough [explanation](https://assets.ctfassets.net/ywqk17d3hsnp/3alhREtaSkgaw2c0KAoYWE/57fada4d99a208a8dc31e37efabb6257/intro-dfinity-crypto.pdf), Dominic explains actually how this solution solves the Byzantine problem. The mainstream blockchain problem will solve this with traditional proof of work. But Dfinity comes with a very interesting solution from Boneh-Lynn-Shacham signatures. With this idea, we can conceive a thershold groups where one of the clients belongs to a certain group and with this threshold, we can create a subset of 'consensus mechanism'.

Well, Dominic will disagree if i have to use the term Consensus Mechanism. In fact, he never really likes to liken this dfinity platform as a blockchain, especially due to BLS signature scheme. In the slide above, he describes how this Threshold relay creates such consistency just by signing a Verifiable Random Function. This means that as you scale up many users to get some form of consensus, you actually don't need to accumulate all the works from the nodes and create a proof of work to get the eventual consistency, but rather with the uniquness, unmanipulable, and unpredictable of the random number sequence we can create a consistent view of the world's states.
This creates a much faster finality of the system.