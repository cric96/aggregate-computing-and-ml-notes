# Aggregate Computing With Machine Learning, Challenges and Directions

This document contains works, problem identifications, formalisations, and intuitions about Aggregate computing with Machine Learning.

# Context
Large scale collective systems are hard to design. Indeed they have characterised aspects usually present in complex systems like: 
- large number of heterogeneous entities
- decentralised control
- autonomous adaptation from environmental changes
- macro-behaviour emerge from local behaviour as a swarm or collective intelligence (self-organisation)

Over the years, researchers handle this complexity with different techniques, ranging from evolutionary computation, deep learning, and Aggregate Computing.
The latter is a declarative paradigm by which programmers tell directly what the global entity (the system as a whole) should do. It is possible thanks to the functional manipulation of a distributed data structure called Computational Field. The composition is another essential feature of Aggregate Computing. Indeed it is possible to describe complex behaviour as a composition of low-level building blocks.

This promising paradigm has different application (swarm robotics, smart cities, crowd engineering, etc.) and foundational results ([eventual consistency](https://doi.org/10.1109/SASO.2016.12) and [self-stabilisation](https://doi.org/10.1145/3177774)).

As a practical meaning creates the right blocks isn't easy to write high-level applications. Moreover, sometimes we would like to tell only when the system behaves badly, and then it adjusts itself accordingly.

So, in our mind, this is the first point that led us to think about merging Aggregate Computing with [Reinforcement Learning](https://doi.org/10.1109/TNN.1998.712192) (and later with Machine Learning in general).

This section is not exhaustive, so please read these articles ([a](https://doi.org/10.1109/MC.2015.261), [b](https://doi.org/10.1007/978-3-030-61470-6\_21), [c](https://doi.org/10.1007/978-3-030-22397-7\_12)) to learn more about Aggregate Computing.

# Why

- learns the "unprogrammable": it seems a "genetic" algorithm manifesto, but it is easy applicable here. Indeed, some essential building blocks (e.g. a distributed leader election) are hard to encode in Aggregate Computing. Having an automatic method that learns how to express some pattern only giving a "nice-to-have" can simplify the design process of complex systems.
- improve adaptivity: Aggregate Computing is built to embrace adaptivity. Indeed different patterns (such as the channel formation, the gradient cast and so on) are intrinsically adaptive, thank the Aggregate Computing model itself. However, combine these techniques with machine learning can get led to an even better adaptivity.
- improve performance: after defining behaviours of a building block, we tend to improve the performance according to some metric (e.g. time to converge, time to adapt regarding environmental changes, etc.). This improvement process could be guided by learning, finding the best solution according to the metric chosen. 
- avoid tedious parameter tuning: Some aggregate computing applications tend to depend upon hyperparameters (e.g. in this work, the system behaviour is influenced by a feedback loop). Learning can avoid tuning these values.
- discover the engineering challenges of a hybrid programming technique: a long-term goal of our approach is to find a way to seamless merge declarative approach to automatic method. 
- scaling up (naturally) machine learning techniques to large scale and unpredictable systems: Aggregate programming is born to handle large scale systems straightforwardly. Applying Machine Learning here must present the same properties

# Execution model
The global-level specification of an *aggregate program* (i.e. a program that use Aggregate Programming) has to break up and then executes in each device.
Locally, a single program evaluation is called *round*. It is executed asynchronously and proactively. At the end of each round, nodes produce a data structure called *export* and share it to its neighbourhood. It contains all the information necessary to make neighbourhood progress in the collective computation (sensor sensing, local program output, etc.).
To summarise, the steps that each node *have to* compute to participate in the collective behaviour are:
1. produce a context: it contains the sensors perception and the exports gather from the neighbourhood;
2. evaluate the aggregate program according to the current context and producing an *export*
3. make actuation according to the export computed
4. share the export to the neighbourhood

The model does not impose:
- how nodes find their neighbourhood: we suppose this relation exists. It could be based on spatial constraints (e.g. all nodes far from ten meters), network constraints (e.g. all nodes connected with me via Bluetooth) or arbitrarily logical constraints.
- node evaluation frequency (even if some works considering time exists)
- how the communication between node happens: we suppose that, when a node wakes up and compute the next export, the neighbour's exports are collected in some way (direct communication, via MOM, via a cloud service, ...)

# FScaFi main operators
[FScaFi](https://doi.org/10.1007/978-3-030-61470-6\_21) is a variant of field calculus in which the neighbour field is not directly encoded. Indeed, the interaction with the neighbourhood happens only with foldhood operations. It is worth noting that in this model is possible to use *built-in* functions. It makes it possible to reuse libraries, sensor queries, relational sensors (i.e. sensors that depends on neighbour values), and so on. 

The essential constructs of the calculus are:

> **Time evolution**: rep(e1){e2} is a construct for dynamically changing
fields through the ``repeated" application of the functional expression e2. At the first computation round (or, more precisely, when no previous state is available—e.g., initially or at re-entrance after state was cleared out due to branching), e2 is applied to e1, then
at each other step it is applied to the value obtained at the previous step.

> **Neighbourhood interaction**: foldhood(e1)(e2){e3} and nbr{e} model device-to-device interaction. The foldhood construct evaluates expression e3 against every aligned neighbour (including the device itself), then aggregates the values collected through e2 together with the initial value e1. The nbr construct tags expressions e signalling that (when evaluated against a
neighbour) the value of e has to be gathered from neighbours (and not directly evaluated). Such behaviour is implemented via a conceptual broadcast of the values evaluated for e.

# A Machine Learning model, a draft
Inspired from Graph Neural Network works, I tried to model a neural network(s) that can be used together with Aggregate Computing.
In this preliminary work, the collective system is a static graph:

<div align="center">
<img src="https://latex.codecogs.com/svg.latex?{\color{Teal}&space;G(N,&space;E)}" title="{\color{Teal} G(N, E)}" />
</div>

In which <img src="https://latex.codecogs.com/svg.latex?{\color{Teal}&space;N}" title="{\color{Teal} N}"/> is the set of all system nodes and <img src="https://latex.codecogs.com/svg.latex?{\color{Teal}&space;N}" title="{\color{Teal} E}"/> is the set containing the neighbour's relation between nodes.
# Possible conflicts
- Aggregate computing born to handle self-organisation by a global specification of the system behaviour. So we have a declarative specification of the system, knowing why nodes behave in some way. With standard Machine Learning, we miss this link, so we carefully pay attention to this point.

