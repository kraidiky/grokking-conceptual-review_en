# Grokking outside neural networks (non-neural and solvable models)

[Reasoning and knowledge graphs](reasoning-knowledge-graphs.md) ← previous card, next → [Distribution shift](distribution-shift.md)

[Concept card index](index.md), category: [3. Tasks and datasets](index.md#cat-3)\
→ Next category: [Weight decay (L2 regularisation)](weight-decay.md)\
← Previous category: [Structured representation learning](structured-representation-learning.md)

## Definition

**Grokking outside neural networks** is the observation of delayed generalisation in models that are either not deep networks at all (ridge and logistic regression, kernel methods) or are linear and therefore solvable analytically. The point of the line is that [grokking](grokking.md) stops being a property of the transformer: it *"can surprisingly occur in linear networks performing linear tasks"* \[[1.1](#ref-1-1)\], while for ridge regression a full end-to-end guarantee is proved — early overfitting, poor generalisation for a long time, generalisation at the end \[[1.2](#ref-1-2)\].

## Elaboration

The value of solvable settings is that in them the definitions stop being operational. In binary logistic classification *"'memorizing' and 'generalizing' solutions can be strictly defined"* \[[1.3](#ref-1-3)\], and hence the transition between them is not an observation on a curve but an event about which a theorem can be proved. There too the chief indeterminacy of the transformer papers disappears: the [time to grokking](grokking-time.md) is derived in closed form rather than measured against a threshold.

**What this gives the corpus.** First, a separation of the necessary from the incidental: if grokking reproduces without attention, without embeddings and without nonlinearity, then none of them is its cause. Second, testability of mechanisms: a linear setting makes it possible to set the account through the passage from the lazy to the rich regime directly against the account through norm compression \[[3.1](#ref-3-1)\].

**Physical models.** A branch of its own is not "simpler than a neural network" but "closer to statistical physics": a dense network classifying configurations of the two-dimensional Ising model groks in the presence of [weight decay](weight-decay.md), and the source of the delay is traced to a rearrangement of the architecture in which successive layers retain ever fewer active neurons \[[3.2](#ref-3-2)\]. Here the task supplies a controllable data generator with a known correlation structure \[[3.3](#ref-3-3)\], which the algorithmic datasets do not have.

**A caveat about transfer.** No solvable model reproduces a transformer: a linear teacher–student setup has neither [Fourier circuits](fourier-features-circuits.md) nor competition of subnetworks, and an agreement of the outward curve does not mean an agreement of the mechanism. The line admits this itself: the dynamics of a shallow transformer on algorithmic data is called "drastically different", and that is exactly why it had to be explained separately \[[3.4](#ref-3-4)\].

## Alternative definitions and nuances

### A. A linear model with strict definitions

A setting in which "memorisation" and "generalisation" are definitions rather than thresholds: binary logistic classification, where both solutions are written out explicitly \[[1.3](#ref-1-3)\]. The distinguishing feature is that in such a model the question "does it grok" has a yes/no answer by construction, and the dispute shifts to whether this is the same grokking as the transformer's.

### B. A proved guarantee instead of an observation

Ridge regression with gradient descent and weight decay: all three spells are proved at once — early overfitting, long poor generalisation, eventual generalisation \[[1.2](#ref-1-2)\], \[[3.5](#ref-3-5)\]. The source of the difference from the empirical works is the standing of the claim: here it is a theorem with conditions, and it is therefore checked not by reproduction but by checking the conditions.

### C. Analytically solvable dynamics

A linear teacher–student model with Gaussian inputs: the full training dynamics is written out, and grokking turns out to be a property of the solution of the equations rather than a find on a plot \[[1.1](#ref-1-1)\]. What separates it from the previous form is the object of derivation: not the fact that there are three spells, but the form of the dependence of the timing on the parameters.

### D. A physical model as a source of data

The Ising model gives not a simplification of the network but a simplification of the **data**: a known distribution with tunable correlation \[[3.3](#ref-3-3)\]. The mechanism of the delay is then sought in the network itself — in the gradual thinning of active neurons across the layers \[[3.2](#ref-3-2)\] — so the setting tests not "is nonlinearity needed" but "what does regularisation do to the architecture".

## References

###### ref-1-1
**\[1.1\]** 2310.16441 — Levi et al., "Grokking in Linear Estimators – A Solvable Model that Groks without Understanding". [`"We show both analytically and numerically that grokking can surprisingly occur in linear networks performing linear tasks in a simple teacher-student setup with Gaussian inputs."`](../papers/2310.16441.grokking-in-linear-estimators-a-solvable-model-that-groks-without-understanding/original/2310.16441.grokking-in-linear-estimators-a-solvable-model-that-groks-without-understanding.md#p1-2).

###### ref-1-2
**\[1.2\]** 2601.19791 — Xu et al., "To Grok Grokking: Provable Grokking in Ridge Regression". [`"We prove end-to-end grokking results for learning over-parameterized linear regression models using gradient descent with weight decay."`](../papers/2601.19791.to-grok-grokking-provable-grokking-in-ridge-regression/original/2601.19791.to-grok-grokking-provable-grokking-in-ridge-regression.md#p1-2).

###### ref-1-3
**\[1.3\]** 2410.04489 — Beck et al., "Grokking at the Edge of Linear Separability". [`"in a simple binary logistic classification task, for which "memorizing" and "generalizing" solutions can be strictly defined"`](../papers/2410.04489.grokking-at-the-edge-of-linear-separability/2410.04489.grokking-at-the-edge-of-linear-separability.card.md#p1-2).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2601.19791 — Xu et al., "To Grok Grokking: Provable Grokking in Ridge Regression". Nuance: a solvable setting makes it possible to set the account through the passage from the lazy to the rich regime directly against other mechanisms. [`"Several existing theoretical papers attribute the occurrence of grokking to a transition in the optimization dynamics from the lazy to the rich regime"`](../papers/2601.19791.to-grok-grokking-provable-grokking-in-ridge-regression/original/2601.19791.to-grok-grokking-provable-grokking-in-ridge-regression.md#p1-4).

###### ref-3-2
**\[3.2\]** 2510.25966 — Hutchison & Yevick, "Grokking in the Ising Model". Nuance: the source of the delay is traced to a rearrangement of the architecture — a decreasing number of active neurons across the layers — rather than to properties of the data. [`"The origin of grokking in this system results from the evolution of the network to an architecture in which successive layers contain a monotonically smaller number of active neurons."`](../papers/2510.25966.grokking-in-the-ising-model/original/2510.25966.grokking-in-the-ising-model.md#p1-7).

###### ref-3-3
**\[3.3\]** 2510.25966 — Hutchison & Yevick, "Grokking in the Ising Model". Nuance: the physical model is valuable as a controllable data generator with a known correlation structure. [`"The Ising model, viewed as a generator of images with maximum randomness subject to a given correlation among spins, provides an optimal framework in which to examine neural network evolution during training."`](../papers/2510.25966.grokking-in-the-ising-model/original/2510.25966.grokking-in-the-ising-model.md#p1-8).

###### ref-3-4
**\[3.4\]** 2310.16441 — Levi et al., "Grokking in Linear Estimators – A Solvable Model that Groks without Understanding". Nuance: the line itself admits that the dynamics of a transformer on algorithmic data is "drastically different" — an agreement of curves does not mean an agreement of mechanism. [`"found that a shallow transformer trained on algorithmic datasets features drastically different dynamics"`](../papers/2310.16441.grokking-in-linear-estimators-a-solvable-model-that-groks-without-understanding/original/2310.16441.grokking-in-linear-estimators-a-solvable-model-that-groks-without-understanding.md#p1-4).

###### ref-3-5
**\[3.5\]** 2601.19791 — Xu et al., "To Grok Grokking: Provable Grokking in Ridge Regression". Nuance: the aim is named outright — to prove an end-to-end guarantee, not to reproduce a curve. [`"our goal is to prove an end-to-end grokking guarantee"`](../papers/2601.19791.to-grok-grokking-provable-grokking-in-ridge-regression/original/2601.19791.to-grok-grokking-provable-grokking-in-ridge-regression.md#p2-1).
