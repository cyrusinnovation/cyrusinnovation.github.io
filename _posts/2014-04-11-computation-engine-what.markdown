---
layout: post
title:  "Computation Engine: What?"
date:   2014-04-11 15:38:55
categories: computation-engine 
post_author: Paul Blair
---

*"You can build a simple rules engine yourself. All you need is to create a bunch of objects with conditions and actions, store them in a collection, and run through them to evaluate the conditions and execute the actions." -- Martin Fowler, ["Rules Engine"][rules-engine]*

At first blush, the [Computation Engine][computation-engine] project is just what Martin Fowler describes: a way of specifying a sequence of "rules" to execute. Unlike rules engines, though, Computation Engine is not a truth-maintenance system and does not support sophisticated techniques like backward chaining. The rules engine that Martin Fowler describes contains rules that are a series of if-then statements, and that can be written in any order. Here the vision is a lot simpler: Put some input in at the front, run through a deterministic series of steps, and get some output at the end. The steps might be rules, but they can be any sort of computation.

The way I've described it, this seems no different from any other piece of functional code. What's so special about a "computation engine"?

First and most obvious is that the computations can be specified at runtime, without being
hard-coded into the structure of your application. For example, you can store your
computations as text strings in a database and read them in when your application starts.
You don't have to rebuild and redeploy your entire system (or some service) whenever your business rules change.

Don't imagine, though, that Computation Engine will let business people specify computations themselves, as some rules engines claim to allow. The expression language that Computation Engine understands is Scala, and using this library requires not only knowing how to write Scala code to express the computations, but also how to instantiate computations. A user will need to have a fair amount of tech-savvy to use this library. Computation Engine is not only not a Business-Writable DSL, it is not even a Business-Readable DSL.

Computation Engine has significant implications on how you write your code. The beginning of the chain of computation takes in a Scala map of Any -> Any, and the ultimate result is a similar map. Abandon all type safety ye who enter here!

The advantage of removing type constraints is that it allows computations to be specified on any arbitrary subset of the incoming data. The writer of the computation has to know that certain values in the data map are of certain types, that some are integers and others are strings, for example. But the incoming data map can combine values of many different types, and the results of computations can add values of new types to the map, without facing the wrath of the type checker. (This, I think, is what Rich Hickey means when he says "let data be data.")

Of course, once the chain of computations is over and you go back into Scala land, you'll have to have data of types that your application expects. But how you get there is something you can change on the fly without having to modify the rest of your application.

Since you can't rely on the compiler to check that the right data is being passed in, though, you have to test the hell out of the callers to make sure they will always obey the contract your computation implicitly specifies. Similarly, you need to test each computation in the chain to make sure its results will always follow the contracts of computations further along that require that data. One of the project's future directions is to come up with a framework for inferring these contracts and specify what tests need to be written. Ideally, ScalaCheck could be used to automate some of these tests.


[rules-engine]:    http://martinfowler.com/bliki/RulesEngine.html
[computation-engine]:    http://github.com/cyrusinnovation/computation-engine
