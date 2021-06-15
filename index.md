# Aggregate Computing With Machine Learning, Challenges and Directions

This document contains works, problem identification, formalisation, and intuitions about Aggregate computing with Machine Learning.

# Context
Large scale collective systems are hard to design. Indeed they have characterised aspects usually present in complex systems like: 
- large number of heterogeneous entities
- decentralised control
- autonomous adaptation from environmental changes
- macro-behaviour emerge from local behaviour as a swarm or collective intelligence (self-organisation)

Over the years, researchers handle this complexity with different techniques, ranging from evolutionary computation, deep learning, and Aggregate Computing.
The latter is a declarative paradigm by which programmers tell directly what the global entity (the system as a whole) should do. It is possible thanks to the functional manipulation of a distributed data structure called Computational Field. The composition is another essential feature of Aggregate Computing. Indeed it is possible to describe complex behaviour as a composition of low-level building blocks.

This promising paradigm has different application (swarm robotics, smart cities, crowd engineering, etc.) and foundational results (eventual consistency and self-stabilisation).

As a practical meaning creates the right blocks isn't easy to write high-level applications. Moreover, sometimes we would like to tell only when the system behaves badly, and then it adjusts itself accordingly.

So, in our mind, this is the first point that led us to think about merging Aggregate Computing with Reinforcement Learning (and later with Machine Learning in general).

This section is not exhaustive, so please read these articles (a, b, c) to learn more about Aggregate Computing.

# Why

- learns the "unprogrammable": it seems a "genetic" algorithm manifesto, but it is easy applicable here. Indeed, some essential building blocks (e.g. a distributed leader election) are hard to encode in Aggregate Computing. Having an automatic method that learns how to express some pattern only giving a "nice-to-have" can simplify the design process of complex systems.
- improve adaptivity: Aggregate Computing is built to embrace adaptivity. Indeed different patterns (such as the channel formation, the gradient cast and so on) are intrinsically adaptive, thank the Aggregate Computing model itself. However, combine these techniques with machine learning can get led to an even better adaptivity.
- improve performance: 
- avoid tedious parameter tuning:
- discover the engineering challenges of a hybrid programming approach:
- scaling up (naturally) machine learning technique to large scale and unpredictable systems:

# Execution model

# Possible conflicts
- Aggregate computing born to handle self-organisation by a global specification of the system behaviour. So we have a declarative specification of the system, knowing why nodes behave in some way. With standard Machine Learning, we miss this link, so we carefully pay attention to this point.