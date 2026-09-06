# Singular learning theory (SLT)

[Information bottleneck](information-bottleneck.md) ← previous card, next → —

[Concept card index](index.md), category: [7. Theory and formal results](index.md#cat-7)\
→ Next category: [Grokking](grokking.md)\
← Previous category: [Progress measures](progress-measures.md)

## Definition

**Singular learning theory** is a frame that starts from the fact that neural networks belong to the *singular* statistical models: the map from parameters to functions is not one-to-one, and the set of minima consists not of isolated points but of manifolds with singularities. The motivation is direct: classical statistics is not enough, PAC bounds are vacuous and do not account for the generalising power of networks \[[1.1](#ref-1-1)\]. The frame's central quantity is the **local learning coefficient** (LLC), which enters the asymptotics of the free energy on a par with the empirical likelihood \[[1.2](#ref-1-2)\].

## Elaboration

**What the frame gives [grokking](grokking.md).** It explains why a delay is possible at all without the loss changing: if the solutions lie on a manifold, moving along it does not change the error but does change the complexity of the solution, and hence generalisation. Hence too the tie to [plateaus](memorization-phase.md): long plateaus of the training error arise near singular regions of parameter space produced by permutation symmetries and redundancies \[[3.1](#ref-3-1)\] — and that observation is older than the term "grokking" itself.

**How it is tested.** Not by derivation but by measurement: the LLC is estimated along training and one watches whether it marks the transitions. A summary of such a test is honest in its assessment: the evidence for an Arrhenius-like relation between the change in free energy and the rate of the transition came out *mixed* \[[1.3](#ref-1-3)\]. That is, in the corpus the frame is a working instrument with partial confirmation, not an established theory of grokking.

**Relation to the neighbouring lines.** SLT meets [effective theory and statistical mechanics](effective-theory-statistical-mechanics.md) through the free energy, and [basin selection](loss-landscape-basins.md) through the claim that the transition is a change of region with a different coefficient. It differs from the entropic line in that there the volume is counted by sampling, whereas here it enters the asymptotics as an exponent.

**The weak spot.** Estimating the LLC requires sampling and is sensitive to its settings, while carrying a theorem proved for Bayesian asymptotics with a growing sample over to training on a fixed sample calls for qualifications — which the corpus does state explicitly.

## Alternative definitions and nuances

### A. Singularity as a property of the model

The original form: a network is a singular statistical model, and classical asymptotics therefore do not apply \[[1.1](#ref-1-1)\]. The distinguishing feature is that this is a claim about the geometry of the solution set, not about the dynamics; it does not yet follow from it that a transition between regions will occur.

### B. The LLC as a measurable quantity

The applied form: the coefficient is estimated numerically and tracked along training \[[1.2](#ref-1-2)\], \[[1.3](#ref-1-3)\]. The source of the difference: here the frame becomes a [progress measure](progress-measures.md) and falls under the same requirements — stability across seeds, leading the transition, reproducibility of the estimate.

### C. Plateaus as traces of singular regions

The historical form, predating the corpus: long plateaus are explained by proximity to singular regions of parameter space \[[3.1](#ref-3-1)\]. The distinguishing feature is what is being explained: not delayed generalisation but a stall of the training error; the tie to grokking is here a conjecture that requires showing the stall and the delay to have the same cause.

## References

###### ref-1-1
**\[1.1\]** 2512.00686 — Lakkapragada, "Using physics-inspired Singular Learning Theory to understand grokking & other phase transitions in modern neural networks". [`"neural networks are *s"`](../papers/2512.00686.using-physics-inspired-singular-learning-theory-to-understand-grokking-and-other-phase-transitions-in-modern-neural-networks/original/2512.00686.using-physics-inspired-singular-learning-theory-to-understand-grokking-and-other-phase-transitions-in-modern-neural-networks.md#p1-3).

###### ref-1-2
**\[1.2\]** 2512.00686 — Lakkapragada, "Using physics-inspired Singular Learning Theory to understand grokking & other phase transitions in modern neural networks". [`"$\lambda_{\alpha}$ is the local learning coefficient (LLC[^3]) (Lau et al., 2023)"`](../papers/2512.00686.using-physics-inspired-singular-learning-theory-to-understand-grokking-and-other-phase-transitions-in-modern-neural-networks/original/2512.00686.using-physics-inspired-singular-learning-theory-to-understand-grokking-and-other-phase-transitions-in-modern-neural-networks.md#p2-1).

###### ref-1-3
**\[1.3\]** 2512.00686 — Lakkapragada, "Using physics-inspired Singular Learning Theory to understand grokking & other phase transitions in modern neural networks". [`"we obtain mixed evidence for an Arrhenius-style reaction-rate relationship"`](../papers/2512.00686.using-physics-inspired-singular-learning-theory-to-understand-grokking-and-other-phase-transitions-in-modern-neural-networks/original/2512.00686.using-physics-inspired-singular-learning-theory-to-understand-grokking-and-other-phase-transitions-in-modern-neural-networks.md#p7-4).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2510.04930 — Saheb Pasand et al., "Egalitarian Gradient Descent: A Simple Approach to Accelerated Grokking". Nuance: the observation is older than the term — plateaus were tied to singular parameter regions long before the work on grokking. [`"Plateaus arise near *singular* parameter regions—caused by permutation symmetries and redundancies"`](../papers/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking/original/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking.md#p3-1).

###### ref-3-2
**\[3.2\]** 2603.01192 — Cullen et al., "A Basin-Selection Perspective on Grokking via Singular Learning Theory". Nuance: the LLC is applied to grokking directly — as a measure of the local degeneracy of the loss surface that tells the competing basins apart. [`"The key measure is the local learning coefficient (LLC)"`](../papers/2603.01192.a-basin-selection-perspective-on-grokking-via-singular-learning-theory/2603.01192.a-basin-selection-perspective-on-grokking-via-singular-learning-theory.card.md#p1-2).
