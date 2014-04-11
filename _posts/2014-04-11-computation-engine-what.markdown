---
layout: post
title:  "Computation Engine: What?"
date:   2014-04-11 15:38:55
categories: computation-engine 
post_author: Paul Blair
---

*"You can build a simple rules engine yourself. All you need is to create a bunch of objects with conditions and actions, store them in a collection, and run through them to evaluate the conditions and execute the actions." -- Martin Fowler, "[Rules Engine][rules-engine]"*

The [Computation Engine][computation-engine] project is just what Martin Fowler describes:
a way of specifying a sequence of "rules" to execute. Unlike more heavyweight rules engines, Computation Engine is not a truth-maintenance system and does not support sophisticated techniques like backward chaining. The vision is a lot simpler: Put some input in at the front, run through a deterministic series of steps, and get some output at
the end. The steps might be rules, but really they are any sort of computation.

The way I've described it, this seems no different from any other piece of functional code. What's so special about a "computation engine"?

First and most obvious is that the computations can be specified at runtime, without being
hard-coded into the structure of your application. For example, you can store your
computations as text strings in a database and read them in when your application starts.
You don't have to rebuild and redeploy your entire system (or some service) whenever your business rules change.



[rules-engine]:    http://martinfowler.com/bliki/RulesEngine.html
[computation-engine]:    http://github.com/cyrusinnovation/computation-engine
