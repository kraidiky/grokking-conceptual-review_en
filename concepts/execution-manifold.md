# Execution manifold

[activation-sparsity](activation-sparsity.md) ← previous card, next → [polysemanticity-superposition](polysemanticity-superposition.md)

[Concept card index](index.md), category: [2. Mechanisms and representations](index.md#cat-2)\
→ Next category: [Modular arithmetic](modular-arithmetic.md)\
← Previous category: [Grokking](grokking.md)

## Definition

**The execution manifold** is a low-dimensional surface in weight space on which the training trajectory is held: a network with hundreds of thousands of parameters in effect moves along a handful of directions. The observation is stated as a general property: *"optimization trajectories remain confined to an empirically invariant low-dimensional execution manifold"* \[[1.1](#ref-1-1)\], and in this picture [grokking](grokking.md) is *"a prolonged confinement to a low-dimensional subspace of weight space"* out of which the trajectory eventually escapes \[[1.2](#ref-1-2)\].

## Elaboration

**How it is measured.** The simplest way is by the principal components of the trajectory: if the first component takes most of the variance, the motion is essentially one-dimensional. The measurement gives 68–83% for the first component across every grokking condition checked \[[3.1](#ref-3-1)\], so the claim of low dimensionality is not qualitative but numerical.

**What this changes in the account of the delay.** If the motion is confined, then a long plateau is not the absence of motion but motion in a constrained direction; leaving that regime is what generalisation is. The picture meets [landscape basins](loss-landscape-basins.md), but speaks about something else: not about which pit the network sits in, but about how many directions it can move along inside it.

**Relation to the other lines.** The low dimensionality of the trajectory explains why one-dimensional measures such as the weight norm describe the dynamics so well: if the motion is nearly one-dimensional, any monotone coordinate along it will do as an [order parameter](order-parameter.md). That is also what makes the notion vulnerable: a measure agreeing with the course of training stops being evidence for the mechanism behind the measure.

**A caveat.** The invariance of the manifold is called empirical: it is observed, not derived, and it has been checked on small transformers and modular arithmetic \[[1.1](#ref-1-1)\]. Whether it carries over to large models remains open — as it does for the neighbouring geometric pictures.

## Alternative definitions and nuances

### A. The manifold as observed low dimensionality

The operational form: the share of the trajectory's variance taken by the first components \[[3.1](#ref-3-1)\]. The distinguishing feature is that the quantity is measured directly and is comparable across runs; the limitation is that PCA is linear, and it will describe a curved manifold as lower-dimensional than it is.

### B. The manifold as a region of confinement

The dynamic form: the trajectory is confined, and generalisation comes when it escapes \[[1.2](#ref-1-2)\]. The source of the difference is that what is being explained is not a structure but an event of escape; hence the prediction that interventions widening the available directions should shorten the delay.

### C. Invariance as a property of the task

The third reading is the strongest: the manifold is the same across different runs and tasks, that is, it is fixed by the task rather than by the accident of initialisation \[[1.1](#ref-1-1)\]. The distinguishing feature is that this is checked by matching manifolds across seeds; and it is exactly here that the picture comes closest to the question of the [universality of solutions](polysemanticity-superposition.md), where agreement across seeds is in fact not always found.

## References

###### ref-1-1
**\[1.1\]** 2602.18523 — Xu, "The Geometry of Multi-Task Grokking: Transverse Instability, Superposition, and Weight Decay Phase Structure". [`"optimization trajectories remain confined to an empirically invariant low-dimensional execution manifold"`](../papers/2602.18523.the-geometry-of-multi-task-grokking-transverse-instability-superposition-and-weight-decay-phase-structure/original/2602.18523.the-geometry-of-multi-task-grokking-transverse-instability-superposition-and-weight-decay-phase-structure.md#p1-3).

###### ref-1-2
**\[1.2\]** 2602.16746 — Xu, "Low-Dimensional and Transversely Curved Optimization Dynamics in Grokking". [`"We propose that grokking corresponds to prolonged confinement on a low-dimensional subspace in weight space"`](../papers/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking/original/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking.md#p1-2).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2602.16746 — Xu, "Low-Dimensional and Transversely Curved Optimization Dynamics in Grokking". Nuance: the low dimensionality is not qualitative but measured — the first principal component takes 68–83% of the trajectory's variance. [`"the first principal component captures 68–83% of trajectory variance across all grokking conditions"`](../papers/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking/original/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking.md#p6-7).

###### ref-3-2
**\[3.2\]** 2606.17120 — Ersoy & Wiesner, "Noise-Driven Escape from Metastable Phases explains Grokking in Deep Neural Networks". Nuance: the escape from confinement is described as hysteresis at a first-order phase transition in the strength of L2 smoothing. [`"grokking is consistent with hysteresis in first-order L2 phase transitions"`](../papers/2606.17120.noise-driven-escape-from-metastable-phases-explains-grokking/original/2606.17120.noise-driven-escape-from-metastable-phases-explains-grokking.md#p1-2).
