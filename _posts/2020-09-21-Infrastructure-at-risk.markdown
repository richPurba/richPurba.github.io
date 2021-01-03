---
layout: post
title:  "Infrastructure at Risk"
date:   2020-09-21 00:00:00+02:00
categories: investment, DevOps, Blockchain
---
> DISCLAIMER: The views and opinions expressed here are those of the author and do not necessarily reflect the official policy or position of Accenture. Any content provided by our bloggers or authors are of their opinion and are not intended to malign any religion, ethnic group, club, organization, company, individual or anyone or anything.


# Deploy and Conquer?
An authoritarian is a leader that dictates his or her own opinion about that which is necessary to do, especially in excluding the majority to make any decision to overrule or object any decision from that authority. Well Apple describes this very much. Despite the fact that many Hollywood producers created many Steve Jobs movies showing how popular they are in the narrative of the modern world, this company is a breed of supremacists of technology. It recently removed [Epic's Game](www.epicgames.com) from its app store. Can Epic's Game say no to that? Of course they don't have such power to do that. <br/>
It's not as easy as deploy your killer-app to the app store and get what you planned. They have one rule: follow our rules otherwise decimated. It's the Big Brother in Orwellian sense, they watch you if you don't follow their rules. 

## TikTok is against National Security.
Now another recent example that is so relevant and pressing is President Trump's concern about ByteDance's product TikTok. The app is potentially a surveillance from The People Republic. You have to know that a company with more than 50 employees in China has to have some member of the party in the company. Effectively, this is making big corporates as watchers for the entire world. China has been successfully deployed AI-backed image recoginition in every single camera of big cities and airports. It's very scary and real: the Big Brothers are *literally* watching us. With this, Trump pushed ByteDance to make a separate entity in US, and Oracle is one of the biggest parent company to cater TikTok's in their portfolio. Do you see the problem?

## Infrastructure
In a Von-Neumann way of architecting a computer, a Disk is essential to store any data. Whatever app you develop, database is used to *persist* your data: user name, password, bank account, etc. You have to do this in order to record the state of your application. Unfortunately, this is the major reason why you should be worry about some companies who can use your (private) data and abuse it. This happens many times at Facebook; the biggest reason why GDPR was executed in EU. <br/>
Of course the state of the art of cryptography has helped us to secure your data. The popular *HTTPS* protocol is a new breed of HTTP protocol with security layer in it (*TLS* or *SSL*), which is a crypto mechanism where some party is deemed to be trustworthy and reliable to sign a CA certificate. Maybe this is too technical but Certificate is a reproducible public-key cryptography that uses [SHA](https://en.wikipedia.org/wiki/Secure_Hash_Algorithms) hash function, for example, and encoded in [RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem)#Operation), which is usually known by X.509 standard in making your TLS calls valid. If that's not enough, the CA has to be signed with a trustworthy party that puts into your CA to make a signed chain of CA. The concept is very similar to Multifactor authentication: if you want to login to your Yahoo Mail, a separate notification will be sent to your yahoo App, assuming that your mobile is more trustworthy since you carry it all of your time (not to mention your toilet time).

### A good Math
One particularly interesting about Mathematics is that it gives us a framework of using logic and symbols to *reproduce* natural phenomena. This is very important since if you use algebra<br/>

> f(x) = x + 1


then you can get the `f(x)` values are `(1,2,3,4,5,6)` given that `x` is `(0,1,2,3,4,5)`. This seems trivial but this displays the very *reproducibility* of math. Of course, when using cryptography out in the public, we can't use this kind of easy-to-reverse math. One particular Math that is very interesting for Open Internet is that of Eliptic Curve, which uses eliptic curves over finite fields that makes the reversing of the math to find the correct private key `(x)` given public key `f(x)` really *intractable*: you can't get the private just by brute force attack from a series of alphanumerical set. Bitcoin and Ethereum is using this at the heart of all Proof-of-something consensus mechanism.


## Blockchain
The decentralized position of a network and resources, where no monolithic party has to agree about your app or you don't have to worry about where your data is store, is the future. We are on the verge of blockchain revolution where you can use some new TikTok app in China where the US will also see how the data is used in China transparently, *if they want to do so and vice versa*. This is the future. The new archicture provides us a wide range of possibility and also some entirely new business model: you need strong economic model baked in the technology. 