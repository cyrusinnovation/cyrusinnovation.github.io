---
layout: post
title:  "Computation Engine: What?"
date:   2014-04-11 15:38:55
categories: computation-engine 
post_author: Paul Blair
---

I'm happy to announce version 1.0 of the [Computation Engine][computation-engine] project is available on GitHub and on Maven Central. The project is similar to a rules engine, in that it allows for specifying a sequence of "rules" to be evaluated and applied at runtime. Unlike rules engines, though, Computation Engine is not a truth-maintenance system; the steps do not need to be if-then rules, but may be any sort of (ideally stateless) computation. The vision is pretty simple: Put in a generic map of input at the front, run through a deterministic series of steps, and get another map containing output at the end.

Computation Engine is written in Scala and also uses Scala as its expression language. It works best with other Scala code. Its sweet spot is applications in which business rules are complex and subject to frequent, unpredictable, and significant changes. 

For more details, see the [GitHub project page][computation-engine] and the [source code repository][computation-engine-code]. The project's Maven coordinates have the group ID `com.cyrusinnovation.computation-engine` and the artifact ID `computation-engine-core`.

[computation-engine]:    http://cyrusinnovation.github.io/computation-engine/
[computation-engine-code]: http://github.com/cyrusinnovation/computation-engine