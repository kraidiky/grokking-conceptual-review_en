# Negative results

[Correlation traps](correlation-traps.md) ← previous card, next → —

[Concept card index](index.md), category: [6. Analytical tools and metrics](index.md#cat-6)\
→ Next category: [Effective theory and statistical mechanics](effective-theory-statistical-mechanics.md)\
← Previous category: [Grokfast / gradient low-pass filtering](gradient-low-pass-filtering.md)

## Definition

**A negative result** is a measurement showing that the expected effect is absent: the intervention does not accelerate, the feature does not predict, the mechanism does not reproduce. In the [grokking](grokking.md) corpus they occur less often than positive ones, but it is they that constrain the explanations, and some works present them as a contribution in their own right: *"We emphasize the failure modes as a contribution in their own right"* \[[1.2](#ref-1-2)\]. The plain formulation is also met on its own: *"We also report a clear negative result"* \[[1.1](#ref-1-1)\].

## Elaboration

**What separates a negative result from the absence of a result.** It requires the same as a positive one: an expectation declared in advance, a measure, and a threshold of significance. In the corpus the threshold is [seed variance](seed-variance-reproducibility.md) — nudges along the commutator do not accelerate generalisation, because all 27 runs fall *"within seed-to-seed variability"* \[[3.1](#ref-3-1)\]. Without that comparison, "did not accelerate" is indistinguishable from "the noise ate the effect".

**What they close off.** Negative results are the only way to separate the accompanying from the acting. A mechanism that accompanies grokking but does not change it under intervention loses the standing of a cause; that is exactly how the claims about defect accumulation, about the sufficiency of a single measure, and about the transferability of features between setups get removed. Their other side is the sharpening of boundaries: a negative result in one setup does not carry over to another, and the card therefore requires the setup to be named together with the outcome.

**Why there are few of them.** The reason is named in the corpus itself: checking negative cases is expensive — the phenomenon requires extremely long training, and an exhaustive survey does not come out \[[3.2](#ref-3-2)\]. Hence the skew: failed interventions more often stay in appendices or go unpublished altogether.

**How to read them.** A negative result from a single seed is not negative: it is indistinguishable from an unlucky draw. Reliable examples in the corpus are therefore always accompanied by the number of runs and the spread, and the weak ones by the authors' qualification that the check was incomplete \[[3.2](#ref-3-2)\].

## Alternative definitions and nuances

### A. A negative result as a contribution

The work declares its failure modes to be part of its contribution and examines them on a par with its successes \[[1.2](#ref-1-2)\]. The distinguishing feature is that the failure is described as fully as the success: the conditions under which it occurs are named, and so is the measure by which it was recorded.

### B. A negative result as a constraint on an explanation

Here the subject is not a technique but a mechanism: the supposed cause is shown to be insufficient \[[3.1](#ref-3-1)\]. The source of the difference is that the conclusion is addressed to theory rather than to practice; and the demand on it is stricter, because "insufficient" can only be checked by intervention, not by observation.

### C. A negative result inside a positive work

The commonest form in the corpus: the main outcome is positive, and alongside it comes the report that the expected explanation was not confirmed \[[1.1](#ref-1-1)\]. The distinguishing feature is that such results are almost never cited and are the first to be lost, although it is exactly they that carry the limits of transferability.

## References

###### ref-1-1
**\[1.1\]** 2607.05104 — Ootani, "Grokking Is Conditional and Fragile: A Fully-Tractable, Multi-Seed Study at 12K Parameters". [`"We also report a clear negative result."`](../papers/2607.05104.grokking-is-conditional-and-fragile-a-fully-tractable-multi-seed-study-at-12k-parameters/original/2607.05104.grokking-is-conditional-and-fragile-a-fully-tractable-multi-seed-study-at-12k-parameters.md#p10-1).

###### ref-1-2
**\[1.2\]** 2607.20552 — Pandey, "Thermodynamic Weight Decay: Exploring Grokking Acceleration via Attention Specific Heat". [`"We emphasize the failure modes as a contribution in their own right."`](../papers/2607.20552.thermodynamic-weight-decay-exploring-grokking-acceleration-via-attention-specific-heat/original/2607.20552.thermodynamic-weight-decay-exploring-grokking-acceleration-via-attention-specific-heat.md#p8-2).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2602.16746 — Xu, "Low-Dimensional and Transversely Curved Optimization Dynamics in Grokking". Nuance: the negative result is stated through a threshold of significance — the seed-to-seed spread — rather than through the absence of a visible effect. [`"within seed-to-seed variability). This negative result demonstrates that defect accumulation alone is insufficient to induce grokking"`](../papers/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking/original/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking.md#p12-7).

###### ref-3-2
**\[3.2\]** 2601.09049 — He et al., "Is Grokking Worthwhile? Functional Analysis and Transferability of Generalization Circuits in Transformers". Nuance: the reason there are few negative checks is named outright — they are expensive, and the survey comes out incomplete. [`"our investigation into “fake grokking” (behavioral grokking without circuit formation) is not exhaustive"`](../papers/2601.09049.is-grokking-worthwhile-functional-analysis-and-transferability-of-generalization-circuits-in-transformers/original/2601.09049.is-grokking-worthwhile-functional-analysis-and-transferability-of-generalization-circuits-in-transformers.md#p5-2).
