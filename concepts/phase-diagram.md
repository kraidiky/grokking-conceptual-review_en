# Phase diagram

[Linear and sparse probing](linear-sparse-probing.md) ← previous card, next → [Correlation traps](correlation-traps.md)

[Concept card index](index.md), category: [6. Analytical tools and metrics](index.md#cat-6)\
→ Next category: [Effective theory and statistical mechanics](effective-theory-statistical-mechanics.md)\
← Previous category: [Grokfast / gradient low-pass filtering](gradient-low-pass-filtering.md)

## Definition

**A phase diagram** is a map of training regimes in the coordinates of hyperparameters: a plane (or a slice of a many-dimensional volume) on which it is marked where the network memorises, where it groks and where it does not learn at all. It is brought into the corpus by the macroscopic analysis of Liu et al.: alongside the microscopic effective theory they build *"a macroscopic analysis of phase diagrams describing learning performance across hyperparameters"* \[[1.1](#ref-1-1)\]. The point of the device is that [grokking](grokking.md) stops being a property of one setting and becomes a region on a map, one that has boundaries.

The second common form is to colour the map not by regime but by a quantity: a contour plot of the [time to grokking](grokking-time.md) over two hyperparameters, with white marking the regions where there is no grokking at all \[[1.2](#ref-1-2)\].

## Elaboration

A diagram requires three things: axes (the control parameters), an indicator of the regime, and a resolution of the grid. In the corpus the axes are almost always taken from the training settings — [weight decay](weight-decay.md), training-set size, [learning rate](learning-rate.md), layer width — and the indicator is either a binary outcome ("grokked / did not grok") or a continuous quantity such as the time or the final accuracy.

**What the mapping gives.** It turns scattered observations into a claim about a boundary: grokking is observed only within a certain range of hyperparameters \[[3.3](#ref-3-3)\], and the question shifts from "does it happen" to "where does the edge run". The notion of the critical training-set size — the least amount of data at which generalisation is still reachable \[[3.1](#ref-3-1)\] — comes from here too: it is a coordinate of the boundary, not a separate phenomenon.

**How a diagram differs from a [phase transition](phase-transition.md).** A transition is an event in training time, a diagram is a map in the space of settings; on it, the transition shows as a line separating regions. The distinction matters because in the corpus one and the same word "phase" is carried by both things, and a work reporting a "phase structure" may mean either regimes of the trajectory or regions of settings \[[3.4](#ref-3-4)\].

**Where the boundaries are analytic.** In solvable models the diagram is not mapped by a grid of runs but obtained by solving an equation: a numerical solution of the implied equation yields the full phase diagram and confirms the assumptions of the theorem \[[3.2](#ref-3-2)\]. This changes the standing of the map: from a summary of experiments it becomes a prediction that can be checked at points.

**What the diagram does not say.** A region on the map is silent about the mechanism: two points inside one region may implement different algorithms. The work on the clock and the pizza maps exactly the boundary between algorithms — by attention rate and layer width — and finds it almost linear \[[3.5](#ref-3-5)\]; such a map does not coincide with a "grokked / did not grok" map and is built on different indicators. And every diagram is limited by the grid it was computed on: the authors leave transfer to large models and real-world tasks open \[[2.1](#ref-2-1)\].

## Alternative definitions and nuances

### A. A binary map of regimes

The simplest form: every grid point is labelled with the outcome of a run, and the regions are separated by a line. The control parameters are usually the sample size and the strength of regularisation \[[1.1](#ref-1-1)\]. The virtue is direct readability; the price is that the outcome depends on the definition of grokking (threshold, step budget) and on [seed variance](seed-variance-reproducibility.md): near the boundary, one and the same grid point may answer differently on different seeds.

### B. A map of a quantity

Instead of the regime, a number is plotted on the map — most often the time: a contour plot of the time to grokking over two hyperparameters, with explicitly marked regions where grokking does not occur \[[1.2](#ref-1-2)\]. The distinguishing feature: such a map shows not only where the boundary runs but also how fast the quantity grows on approach to it, and it is therefore fit for checking a predicted form of the dependence — an exponential in the weight norm, for instance.

### C. An analytic diagram

The boundary is obtained not by a grid of runs but by solving an equation for the order parameter \[[3.2](#ref-3-2)\]. The source of the difference is the standing of the result: an empirical map describes what has already been observed, an analytic one predicts the boundary at points where nobody has computed anything, and is therefore falsifiable. A caveat: analytic diagrams have been obtained in models far simpler than a transformer, and transfer to it is a question of its own.

### D. A map of algorithms rather than of regimes

A special case: the axes are the same, but the regions are labelled by *which* solution was learned rather than by whether generalisation took place. Such a diagram shows the transition between two mechanisms — from one algorithm of modular addition to another, say — and its boundary is almost linear in attention rate and layer width \[[3.5](#ref-3-5)\]. The indicator of regime here is not accuracy but behavioural measures that tell the algorithms apart, which makes the map incomparable with a "grokked / did not grok" one.

## References

###### ref-1-1
**\[1.1\]** 2205.10343 — Liu et al., "Towards Understanding Grokking: An Effective Theory of Representation Learning". [`"a *macroscopic* analysis of phase diagrams describing learning performance across hyperparameters"`](../papers/2205.10343.towards-understanding-grokking-an-effective-theory-of-representation-learning/original/2205.10343.towards-understanding-grokking-an-effective-theory-of-representation-learning.md#p1-2).

###### ref-1-2
**\[1.2\]** 2310.16441 — Levi et al., "Grokking in Linear Estimators – A Solvable Model that Groks without Understanding". [`"White regions indicate no grokking, as generalization accuracy does not converge to $95\%$."`](../papers/2310.16441.grokking-in-linear-estimators-a-solvable-model-that-groks-without-understanding/original/2310.16441.grokking-in-linear-estimators-a-solvable-model-that-groks-without-understanding.md#fig-4).

## References of works that joined the discussion

### Contested

###### ref-2-1
**\[2.1\]** 2602.18523 — Xu, "The Geometry of Multi-Task Grokking: Transverse Instability, Superposition, and Weight Decay Phase Structure". Limits: the diagram is built on 2–3 tasks at a single modulus and with small models, and the authors leave its transfer to large models open. [`"Whether the scaling of manifold rank with task count, the holographic incompressibility, and the WD phase diagram generalize to larger models and real-world tasks remains open."`](../papers/2602.18523.the-geometry-of-multi-task-grokking-transverse-instability-superposition-and-weight-decay-phase-structure/original/2602.18523.the-geometry-of-multi-task-grokking-transverse-instability-superposition-and-weight-decay-phase-structure.md#p30-7).

### In support

###### ref-3-1
**\[3.1\]** 2205.10343 — Liu et al., "Towards Understanding Grokking: An Effective Theory of Representation Learning". Nuance: the critical training-set size is a coordinate of the boundary on the diagram, not a separate phenomenon. [`"The critical training set size corresponds to the least amount of training"`](../papers/2205.10343.towards-understanding-grokking-an-effective-theory-of-representation-learning/original/2205.10343.towards-understanding-grokking-an-effective-theory-of-representation-learning.md#p1-6).

###### ref-3-2
**\[3.2\]** 2310.03789 — Rubin et al., "Grokking as a First Order Phase Transition in Two Layer Networks". Nuance: the diagram is obtained by solving an equation rather than by a grid of runs, and therefore predicts the boundary where no experiments were run. [`"Solving the implied equation for $a$ numerically yields the full phase diagram here"`](../papers/2310.03789.grokking-as-a-first-order-phase-transition-in-two-layer-networks/original/2310.03789.grokking-as-a-first-order-phase-transition-in-two-layer-networks.md#p8-6).

###### ref-3-3
**\[3.3\]** 2306.13253 — Notsawo et al., "Predicting Grokking Long Before it Happens". Nuance: the observation the diagram is needed for — grokking lives only within a range of settings. [`"Recent work has shown that grokking is observed only with a certain range of hyperparameters"`](../papers/2306.13253.predicting-grokking-long-before-it-happens/original/2306.13253.predicting-grokking-long-before-it-happens.md#p2-1).

###### ref-3-4
**\[3.4\]** 2602.18649 — Xu, "Global Low-Rank, Local Full-Rank: The Holographic Encoding of Learned Algorithms". Nuance: "phase structure" here refers to regimes of the trajectory, not to regions of settings — the same word in another sense. [`"A detailed analysis of the training dynamics, phase structure, and transverse instabilities of these models"`](../papers/2602.18649.global-low-rank-local-full-rank-the-holographic-encoding-of-learned-algorithms/original/2602.18649.global-low-rank-local-full-rank-the-holographic-encoding-of-learned-algorithms.md#p3-6).

###### ref-3-5
**\[3.5\]** 2306.17844 — Zhong et al., "The Clock and the Pizza: Two Stories in Mechanistic Explanation of Neural Networks". Nuance: the regions are labelled by the algorithm learned rather than by the fact of generalisation, and the boundary turns out to be almost linear. [`"We also observe an almost linear phase boundary with regards to both attention rate and layer width."`](../papers/2306.17844.the-clock-and-the-pizza-two-stories-in-mechanistic-explanation-of-neural-networks/original/2306.17844.the-clock-and-the-pizza-two-stories-in-mechanistic-explanation-of-neural-networks.md#p8-5).

## Passing mentions

Works that only mention the notion — a literature review, a related-work paragraph, a passing citation — without examining it.

**\[4.1\]** 2302.03025 — Chughtai et al., "A Toy Model of Universality: Reverse Engineering how Networks Learn Group Operations". [`"Liu et al. 2022b construct further small examples of grokking, which they use to compute phase diagrams"`](../papers/2302.03025.a-toy-model-of-universality-reverse-engineering-how-networks-learn-group-operations/2302.03025.a-toy-model-of-universality-reverse-engineering-how-networks-learn-group-operations.card.md#p3-1).
