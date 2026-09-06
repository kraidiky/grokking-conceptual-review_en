# The complexity–error tradeoff

[generalization-circuit](generalization-circuit.md) ← previous card, next → [sparse-solutions-hidden-progress](sparse-solutions-hidden-progress.md)

[Concept card index](index.md), category: [2. Mechanisms and representations](index.md#cat-2)\
→ Next category: [Modular arithmetic](modular-arithmetic.md)\
← Previous category: [Grokking](grokking.md)

## Definition

**The complexity–error tradeoff** is a frame in which training is described as an exchange between how complex the learned function is and how small the error is: the network first attains a zero training error with a complex (memorising) solution, and then, under the pressure of regularisation, moves to a simpler solution with the same error — and it is this second step that is seen from the outside as [grokking](grokking.md). Hence a direct reading of the delay as **compression**: the complexity of the network is measured by the number of linear mappings, and that number describes the compression well up to the moment of generalisation \[[1.1](#ref-1-1)\].

The weak spot of the frame is named within the frame itself: *"there are multiple definitions for model complexity across different model categories"*, and they change even within one category \[[1.2](#ref-1-2)\] — that is, without a choice of a concrete measure the claim about a tradeoff is not testable.

## Elaboration

**Complexity as a parameter rather than as an outcome.** One branch of the corpus controls the complexity from the outside: the number of parameters is varied and one looks at what happens to the delay, calling this outright a regulation of the effective complexity of the model \[[3.1](#ref-3-1)\]. The tradeoff then turns into a map of regimes: beyond a certain threshold an increase of complexity stops giving a commensurate return \[[3.3](#ref-3-3)\], and that is a boundary on the [phase diagram](phase-diagram.md) rather than a property of a single network.

The measure around which this exchange is built goes in the corpus under the name **linear mapping number** (LMN).

**Complexity as a quantity measured over the course of training.** The other branch measures the complexity of the learned function itself: the number of linear regions (for ReLU networks) is generalised to the number of linear mappings and falls as generalisation proceeds \[[1.1](#ref-1-1)\]. This makes the tradeoff observable: it acquires a curve rather than only two end states.

**The link to double descent.** The frame is a relative of [double descent](double-descent.md), and in the corpus the two are compared directly: different parts of the network learn at different speeds, which produces two bias–variance tradeoff curves with different minima \[[3.2](#ref-3-2)\]. Hence an important consequence: the observed non-monotonicity of the test error may be not a property of complexity as such but a consequence of a mismatch of speeds inside the network.

**How the tradeoff differs from [circuit efficiency](circuit-efficiency.md).** There two concrete circuits are compared by norm per unit of quality, here two regimes are compared by an abstract measure of complexity. The practical difference: circuit efficiency predicts *which* solution will win, the tradeoff predicts *when* the transition will happen; and the first is tested by ablating a circuit, the second by measuring a complexity measure over time.

## Alternative definitions and nuances

### A. Complexity as the number of linear mappings

The measure is tied to the make-up of the network: for a ReLU network one counts the number of linear regions, and its generalisation (LMN) falls at the passage to a generalising solution \[[1.1](#ref-1-1)\]. The distinguishing feature is that the measure is computable at any step of training and therefore yields a compression curve; the price is that it is defined for piecewise-linear networks and does not carry over verbatim to other activations.

### B. Complexity as the number of parameters

Here the complexity is not measured but imposed: the size of the model is varied and one looks at the outcome \[[3.1](#ref-3-1)\], \[[3.3](#ref-3-3)\]. The source of difference is the direction of inference: not "what happened to the complexity during training" but "what training does at a given complexity". Caveat: the effective complexity of a trained network is not equal to its number of parameters, and works that conflate these two senses arrive at incommensurable statements.

### C. The tradeoff as a bias–variance exchange

The classical reading: the error decomposes into bias and variance, and the minimum lies at an intermediate complexity. In the corpus it is met alongside double descent and with the caveat that several tradeoff curves with different minima can add up to a non-monotone total error \[[3.2](#ref-3-2)\]. The distinguishing feature: the subject here is the test error rather than the learned function, so the statement requires no measure of the complexity of the network itself.

### D. A refusal of a single measure

A position worth holding explicitly: there is no universal measure of complexity, the definitions differ between categories of models and within a category \[[1.2](#ref-1-2)\]. The consequence for the card is that every statement of the form "the network has become simpler" must name its measure; without one it is irrefutable and therefore empty.

## References

###### ref-1-1
**\[1.1\]** 2310.05918 — Liu et al., "Grokking as Compression: A Nonlinear Complexity Perspective". [`"We define *linear mapping number* (LMN) to measure network complexity, which is a generalized version of linear region number for ReLU networks."`](../papers/2310.05918.grokking-as-compression-a-nonlinear-complexity-perspective/original/2310.05918.grokking-as-compression-a-nonlinear-complexity-perspective.md#p1-2).

###### ref-1-2
**\[1.2\]** 2310.17247 — Miller et al., "Grokking Beyond Neural Networks: An Empirical Exploration with Model Complexity". [`"Not only are there multiple definitions for model complexity across different model categories"`](../papers/2310.17247.grokking-beyond-neural-networks-an-empirical-exploration-with-model-complexity/2310.17247.grokking-beyond-neural-networks-an-empirical-exploration-with-model-complexity.card.md#p2-3).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2303.06173 — Davies et al., "Unifying Grokking and Double Descent". Nuance: the complexity here is imposed from the outside — by the number of parameters — and one looks at the outcome rather than measuring it in the trained network. [`"We explore the effects of regulating effective model complexity by varying parameter-count."`](../papers/2303.06173.unifying-grokking-and-double-descent/2303.06173.unifying-grokking-and-double-descent.card.md#p4-1).

###### ref-3-2
**\[3.2\]** 2303.06173 — Davies et al., "Unifying Grokking and Double Descent". Nuance: the non-monotonicity may come not from the complexity but from a mismatch of the learning speeds of different parts of the network. [`"Heckel & Yilmaz 2020 find different parts of networks learning at different speeds can cause two bias-variance trade-off curves with different minima"`](../papers/2303.06173.unifying-grokking-and-double-descent/2303.06173.unifying-grokking-and-double-descent.card.md#p4-4).

###### ref-3-3
**\[3.3\]** 2401.10463 — Zhu et al., "Critical Data Size of Language Models from a Grokking Perspective". Nuance: beyond the threshold an increase of complexity stops giving a commensurate return — the tradeoff is visible as a boundary on the map of settings. [`"This suggests a threshold beyond which increasing the model complexity does not yiel"`](../papers/2401.10463.critical-data-size-of-language-models-from-a-grokking-perspective/2401.10463.critical-data-size-of-language-models-from-a-grokking-perspective.card.md#p7-2).
