# Phases: comprehension, grokking, memorization, confusion

[behavioral-vs-true-grokking](behavioral-vs-true-grokking.md) ← previous card, next → [Naive Loss Minimization](nlm.md)

[Concept card index](index.md), category: [1. Phenomena](index.md#cat-1)\
→ Next category: [Structured representation learning](structured-representation-learning.md)\
← Previous category: [Effective theory and statistical mechanics](effective-theory-statistical-mechanics.md)

## Definition

The quartet of phases — **comprehension**, **grokking**, **memorization** and **confusion** — is a partition of the plane of settings into four regions according to how the times to reach a high accuracy on training and on testing relate to one another. The partition was introduced together with the [phase diagram](phase-diagram.md): for each pair of values of the [learning rate](learning-rate.md) and the [weight decay](weight-decay.md) one counts the number of steps to 90% accuracy, and *"the 2D plane is split into four phases"* \[[1.1](#ref-1-1)\].

The distinction inside the pair "comprehension — grokking" is the very content of the notion: both regions generalise, but in the first generalisation comes at once and in the second it comes with a delay. "Memorization" gives no generalisation at all, "confusion" gives not even a fit.

## Elaboration

The point of the quartet is that it turns the question "why does the network grok" into the question "where does it stand on the map". [Grokking](grokking.md) turns out to be not a property of the model but a region of settings bordering on three others; a transition between the regions is the same thing as a crossing of a boundary on the diagram, not an event inside a single run.

In the corpus the same partition is also met under the name **four learning phases**.

**The relation to the phases of a trajectory.** The same work is done by the more widespread three-part partition of *time*: poor quality on both curves, then a perfect fit at a low validation accuracy, then a rise of the validation accuracy to the level of the training one \[[3.1](#ref-3-1)\]. The names are alike, the subject is different: there the phases follow one another over the course of a single training run, here they are regions in the space of settings. A conflation of these two senses is a common source of confusion in reading: "the memorisation phase" can mean both a segment of a trajectory and a cell of a map.

**What the quartet specifically gives.** It makes it observable that grokking has two different neighbours: on one side a regime where generalisation comes at once (and so the question "why the delay" turns into "what is getting in the way"), on the other a regime where there is none at all. Hence the natural continuation of the line: to measure not only the fact of generalisation but the position of the point relative to the boundary, and to describe the boundary by the critical dataset size \[[3.2](#ref-3-2)\].

**A caveat.** The partition is built on a threshold (90% accuracy) and on a step budget: shifting the threshold moves the boundaries, and a finite budget turns "a very late generalisation" into "memorisation". This is the same dependence on the definition as with the [grokking time](grokking-time.md), and it is inherited by every map of this kind.

## Alternative definitions and nuances

### A. Four regions of settings

The original form: the axes are the learning rate and the weight decay, the feature is the relation between the times at which the two curves reach the threshold \[[1.1](#ref-1-1)\]. The distinguishing feature: what is called a phase is a region rather than a segment of time, and so statements are put as "at such settings the network is in phase X" rather than "the network has passed into phase X".

### B. Three phases of a trajectory

The more widespread usage: the phases are consecutive segments of a single training run \[[3.1](#ref-3-1)\]. The source of difference is what counts as the variable: here it is time, there it is the settings. The practical consequence: two statements about "phases" from different works may fail to contradict each other even when they look incompatible.

### C. Regimes by the amount of data

A third partition runs not along the optimisation but along the data: a shortage, a sufficiency and an excess of data, with a threshold (the critical size) marking the shift from quick memorisation to slow generalisation \[[3.2](#ref-3-2)\]. The distinguishing feature is the control parameter; hence the different predictive power as well: a map by data says how many examples are needed, a map by optimisation says which settings are admissible.

## References

###### ref-1-1
**\[1.1\]** 2205.10343 — Liu et al., "Towards Understanding Grokking: An Effective Theory of Representation Learning". [`"The 2D plane is split into four phases: *comprehension*, *grokking*, *memorization* and *confusion*"`](../papers/2205.10343.towards-understanding-grokking-an-effective-theory-of-representation-learning/original/2205.10343.towards-understanding-grokking-an-effective-theory-of-representation-learning.md#p7-2).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2306.13253 — Notsawo et al., "Predicting Grokking Long Before it Happens". Nuance: the same partitioning work, but the variable is the training time rather than the settings. [`"The phenomenon of grokking is characterized by three phases in order"`](../papers/2306.13253.predicting-grokking-long-before-it-happens/original/2306.13253.predicting-grokking-long-before-it-happens.md#p2-9).

###### ref-3-2
**\[3.2\]** 2401.10463 — Zhu et al., "Critical Data Size of Language Models from a Grokking Perspective". Nuance: the third partition runs along the amount of data, and its threshold is the critical dataset size. [`"We explore the critical data size in language models, a threshold that marks a fundamental shift from quick memorization to slow generalization."`](../papers/2401.10463.critical-data-size-of-language-models-from-a-grokking-perspective/2401.10463.critical-data-size-of-language-models-from-a-grokking-perspective.card.md#p1-2).
