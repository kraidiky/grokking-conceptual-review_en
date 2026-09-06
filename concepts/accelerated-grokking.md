# Accelerated grokking

[Spherical weight-norm constraint](spherical-weight-norm-constraint.md) ← previous card, next → —

[Concept card index](index.md), category: [5. Interventions and methods](index.md#cat-5)\
→ Next category: [Progress measures](progress-measures.md)\
← Previous category: [Weight decay (L2 regularisation)](weight-decay.md)

## Definition

**Accelerating grokking** is a family of interventions whose aim is to shorten the delay between fitting the training sample and generalising, without changing the task itself. The motive is stated outright: the delay *"compromises predictability and efficiency"* \[[1.2](#ref-1-2)\], and therefore *"our goal is to accelerate generalization of a model under grokking phenomenon"* \[[1.1](#ref-1-1)\]. The measure of success is the [time to grokking](grokking-time.md), and the dispute is about what exactly the shortening is achieved by.

## Elaboration

The corpus's techniques fall into four families by where they intervene.

**Into the gradient.** If the delay is attributed to a slowly changing component of the updates, then it can be amplified by a filter: grokking is tied to the low-frequency part of the dual representation of the updates \[[3.1](#ref-3-1)\], and hence [gradient filtering](gradient-low-pass-filtering.md). Related techniques transform the gradient differently — by orthogonalisation or by a learned transformation.

**Into the representation at the input.** Another line explains the delay by an uninformative embedding and proposes to bring in a ready-made one: an informative embedding secures continuous progress instead of a plateau \[[3.2](#ref-3-2)\]. Here the acceleration is achieved not by changing the dynamics but by changing the starting point.

**Into the parameters along the way.** The third family pushes the network out of a stalled state: swapping values within a layer cuts the time by roughly a factor of five \[[3.3](#ref-3-3)\]; large Gaussian noise and restarts belong here as well.

**Into regularisation and the norm.** The fourth is control of the weight norm and [weight decay](weight-decay.md): keeping the norm inside the "Goldilocks zone" speeds generalisation up, at the price of introducing an extra constraint \[[3.4](#ref-3-4)\].

**A general caveat.** Almost all acceleration claims are measured in optimiser steps rather than in time spent, and are compared against a baseline curve tuned for the shortest grokking; converted into seconds, part of the gain disappears — this is examined in the card on the [time to grokking](grokking-time.md). The second common weakness is [seed variance](seed-variance-reproducibility.md): an acceleration shown on a single seed is indistinguishable from luck.

## Alternative definitions and nuances

### A. Acceleration as a change of the dynamics

The intervention works on the updates: it amplifies the slow component, orthogonalises, transforms \[[3.1](#ref-3-1)\]. The distinguishing feature is that the task is solved by the same network from the same starting point, and only the path changes; it is verified by comparing trajectories all else being equal.

### B. Acceleration as a change of the starting point

The intervention works before training: an embedding obtained by a cheap model is transferred in \[[3.2](#ref-3-2)\]. The source of the difference is that one cannot say here "the same task is solved faster", because part of the work has been moved outside the measured run; an honest comparison has to count the cost of obtaining the embedding.

### C. Acceleration as a push out of a stall

The intervention works along the way and destroys the current state: parameter swapping, large noise \[[3.3](#ref-3-3)\]. The distinguishing feature is a counter-intuitive condition: destroying part of what has been learned speeds generalisation up, which is what makes this branch evidence for the picture of a kinetic stall, and not merely a technique.

### D. Acceleration as a constraint

The intervention narrows the search region: the norm is fixed on a sphere of a suitable radius \[[3.4](#ref-3-4)\]. The caveat sounded within the corpus itself: the technique introduces an extra hyperparameter, and the gain has to be counted with its tuning included.

## References

###### ref-1-1
**\[1.1\]** 2405.20233 — Lee et al., "Grokfast: Accelerated Grokking by Amplifying Slow Gradients". [`"our goal is to accelerate generalization of a model under grokking phen"`](../papers/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients.card.md#p1-2).

###### ref-1-2
**\[1.2\]** 2504.13292 — Xu et al., "Let Me Grok for You: Accelerating Grokking via Embedding Transfer from a Weaker Model". [`"this delayed generalization phenomenon compromises predictability and efficiency"`](../papers/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model/original/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model.md#p1-2).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2405.20233 — Lee et al., "Grokfast: Accelerated Grokking by Amplifying Slow Gradients". Nuance: the acceleration is derived from the hypothesis that the delay is carried by the slowly changing part of the updates. [`"the grokking phenomenon is directly related to the low-frequency part of the dual representatio"`](../papers/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients.card.md#p2-5).

###### ref-3-2
**\[3.2\]** 2504.13292 — Xu et al., "Let Me Grok for You: Accelerating Grokking via Embedding Transfer from a Weaker Model". Nuance: the acceleration is achieved not by changing the dynamics but by replacing the starting point — by transferring in an informative embedding. [`"an informative embedding enables continuous progress during training"`](../papers/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model/original/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model.md#p1-7).

###### ref-3-3
**\[3.3\]** 2608.01833 — Chan et al., "Tunneling the Loss Landscape: Bypassing Memorization with Monte Carlo Parameter Swapping". Nuance: destroying part of what has been learned speeds generalisation up — an argument for the picture of a kinetic stall. [`"the swap intervention substantially reduces the grokking time"`](../papers/2608.01833.tunneling-the-loss-landscape-bypassing-memorization-with-monte-carlo-parameter-swapping/original/2608.01833.tunneling-the-loss-landscape-bypassing-memorization-with-monte-carlo-parameter-swapping.md#p4-9).

###### ref-3-4
**\[3.4\]** 2504.13292 — Xu et al., "Let Me Grok for You: Accelerating Grokking via Embedding Transfer from a Weaker Model". Nuance: keeping the norm on a sphere speeds generalisation up, but introduces an extra hyperparameter. [`"found that restricting the weight norm to a sphere of the appropriate radius during training can accelerate generalization"`](../papers/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model/original/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model.md#p3-1).

###### ref-3-5
**\[3.5\]** 2504.17243 — Zhou et al., "NeuralGrok: Accelerate Grokking by Neural Gradient Transformation". Nuance: the gradient transformation is not set by hand but learned by an auxiliary module jointly with the model. [`"learns an optimal gradient transformation to accelerate"`](../papers/2504.17243.neuralgrok-accelerate-grokking-by-neural-gradient-transformation/original/2504.17243.neuralgrok-accelerate-grokking-by-neural-gradient-transformation.md#p1-2).

```
concept:
  category: 5
  papers_linked: 5               # distinct papers across the reference sections
  counted_at: 2026-08-28
```

###### ref-3-6
**\[3.6\]** 2507.----- — Mason-Williams & Mason-Williams 2025, "Decomposed Learning: An Avenue for Mitigating Grokking" (the MOSS workshop at ICML 2025; the work is not on arXiv). A technique of a different kind from the other accelerators of this card: not a gradient filter and not an embedding transfer, but a reparameterisation of the weight matrix by a truncated singular value decomposition. Nuance: there is a single setting — modular arithmetic on a small perceptron — and no comparison with the other accelerators. [`"Decomposed Learning reduces and/or mitigates the grokking phenomena against the non-SVD representation provided by the baselines"`](../papers/2507.-----.decomposed-learning-an-avenue-for-mitigating-grokking/2507.-----.decomposed-learning-an-avenue-for-mitigating-grokking.card.md#p4-2).
