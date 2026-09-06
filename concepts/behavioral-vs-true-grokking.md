# Behavioural versus true grokking

[Semi-grokking](semi-grokking.md) ← previous card, next → [comprehension-confusion-phases](comprehension-confusion-phases.md)

[Concept card index](index.md), category: [1. Phenomena](index.md#cat-1)\
→ Next category: [Structured representation learning](structured-representation-learning.md)\
← Previous category: [Effective theory and statistical mechanics](effective-theory-statistical-mechanics.md)

## Definition

The distinction between **behavioural** and **true** grokking is the question of what exactly counts as [grokking](grokking.md): the jump in test accuracy on its own, or the jump together with the formation of a generalising mechanism inside the network. The question is raised by works that mechanistically re-examine grokked models and find that *"grokked and non-grokked models follow identical reasoning paths"*, grokking itself merely embedding what had been memorised \[[1.1](#ref-1-1)\]. Hence the working name for the case where the behaviour is there but the mechanism is not — "fake grokking": *"behavioral grokking without circuit formation"* \[[1.2](#ref-1-2)\].

## Elaboration

The distinction rests on grokking having two independently measurable sides. The outward one is the accuracy curves, the threshold, the [time to grokking](grokking-time.md). The inward one is the presence of a [circuit](fourier-features-circuits.md) that produces that accuracy, and its sufficiency in isolation from the rest of the network. As long as the two sides coincide there is nothing to distinguish; the works of this line show that they come apart, and in both directions.

**The mechanism is there but the jump has not come yet.** The generalising scheme forms before the visible transition — this was established by the line of [progress measures](progress-measures.md) and underlies the whole idea of hidden progress beneath the plateau.

**The jump has come but the rearrangement is not finished.** The converse case has been measured directly: half of the post-grokking rearrangement of the scheme falls, in the median, 350 steps *after* the test-accuracy transition, and ninety per cent of it at 1250–1850 steps, and so it goes across all 32 seeds per task \[[2.1](#ref-2-1)\]. That is, the moment counted as grokking from the curve does not coincide with the moment at which the mechanism is ready.

**Why this is not a dispute about words.** What counts as proved depends on the answer: if grokking is defined behaviourally, then the claim "the model has acquired the ability to reason" does not follow from the jump \[[1.1](#ref-1-1)\]. The [circuit efficiency](circuit-efficiency.md) frame gives this a natural explanation: the task admits both a generalising and a memorising solution, and the transition is a change of winner rather than an ability appearing out of nowhere \[[3.1](#ref-3-1)\]. In the extreme regimes the distinction becomes observable: in [semi-grokking](semi-grokking.md) the network is stuck between the solutions, which shows that "has grokked" is not a binary property \[[3.2](#ref-3-2)\].

**What is missing.** Checking the "fake" case is limited computationally: the authors state plainly that they could not survey it exhaustively, because the phenomenon requires extremely long training \[[1.2](#ref-1-2)\].

## Alternative definitions and nuances

### A. The behavioural definition

Grokking = the jump of delayed accuracy after a plateau; nothing is claimed about the internal arrangement. The virtue is that the definition is operational and carries over to any task; the price is that it also covers cases where no generalising mechanism is present and the rise in accuracy is explained by an integration of what was memorised \[[1.1](#ref-1-1)\].

### B. The mechanistic definition

Grokking = the formation of a circuit that solves the task in isolation. The distinguishing feature is that it is checked by ablation and by filtering the representation, not by a curve; the consequence is that the moment of grokking shifts relative to the behavioural one, and the shift has been measured: the rearrangement continues for thousands of steps after the jump \[[2.1](#ref-2-1)\].

### C. The definition through competition of solutions

An intermediate position: grokking is the moment at which the generalising solution becomes more efficient than the memorising one \[[3.1](#ref-3-1)\]. The control quantity here is the sample size (the critical data size), not time; hence the prediction of reversible phenomena such as ungrokking, and of regimes where the network stays between the solutions \[[3.2](#ref-3-2)\].

### D. The two-pattern frame and its limits

A related reading: two patterns, a fast one that generalises poorly and a slow one that generalises well \[[3.3](#ref-3-3)\]. The caveat sounded within the corpus itself: without a definition of "pattern" the frame describes but does not predict, and it therefore has to be anchored either by a measure of efficiency or by a mechanistic check.

## References

###### ref-1-1
**\[1.1\]** 2601.09049 — He et al., "Is Grokking Worthwhile? Functional Analysis and Transferability of Generalization Circuits in Transformers". [`"We show that grokked and non-grokked models follow identical reasoning paths"`](../papers/2601.09049.is-grokking-worthwhile-functional-analysis-and-transferability-of-generalization-circuits-in-transformers/original/2601.09049.is-grokking-worthwhile-functional-analysis-and-transferability-of-generalization-circuits-in-transformers.md#p4-6).

###### ref-1-2
**\[1.2\]** 2601.09049 — He et al., "Is Grokking Worthwhile? Functional Analysis and Transferability of Generalization Circuits in Transformers". [`"our investigation into “fake grokking” (behavioral grokking without circuit formation) is not exhaustive"`](../papers/2601.09049.is-grokking-worthwhile-functional-analysis-and-transferability-of-generalization-circuits-in-transformers/original/2601.09049.is-grokking-worthwhile-functional-analysis-and-transferability-of-generalization-circuits-in-transformers.md#p5-2).

## References of works that joined the discussion

### Contested

###### ref-2-1
**\[2.1\]** 2607.06628 — Truong Xuan Khanh, "Cross-Trajectory Chimera Interventions Reveal Dissociable Roles of Weight Magnitude and Direction in Grokking". Contests the behavioural definition from within: the rearrangement of the scheme goes on for thousands of steps after the curve has already counted grokking. [`"$50\%$ of the post-grokking reorganization is reached at a median of $350$ steps after the test-accuracy transition"`](../papers/2607.06628.cross-trajectory-chimera-interventions-reveal-dissociable-roles-of-weight-magnitude-and-direction-in-grokking/2607.06628.cross-trajectory-chimera-interventions-reveal-dissociable-roles-of-weight-magnitude-and-direction-in-grokking.card.md#p7-3).

### In support

###### ref-3-1
**\[3.1\]** 2309.02390 — Varma et al., "Explaining grokking through circuit efficiency". Nuance: the transition is explained by a change of winner between two solutions rather than by the appearance of a new ability. [`"We propose that grokking occurs when the task admits a generalising solution and a memorising solution"`](../papers/2309.02390.explaining-grokking-through-circuit-efficiency/2309.02390.explaining-grokking-through-circuit-efficiency.card.md#p1-3).

###### ref-3-2
**\[3.2\]** 2309.02390 — Varma et al., "Explaining grokking through circuit efficiency". Nuance: near the boundary, regimes are predicted in which "has grokked" stops being a binary property. [`"which we call the critical dataset size $D_{\textrm{crit}}$"`](../papers/2309.02390.explaining-grokking-through-circuit-efficiency/2309.02390.explaining-grokking-through-circuit-efficiency.card.md#p2-1).

###### ref-3-3
**\[3.3\]** 2311.18817 — Lyu et al., "Dichotomy of Early and Late Phase Implicit Biases Can Provably Induce Grokking". Nuance: the two-pattern frame describes the distinction but itself needs a definition of "pattern", failing which it does not predict. [`"Davies et al. 2022 hypothesized that both grokking and double descent are the result of the existence of two patterns: one pattern is faster to learn but generalizes poorly, and the other pattern is slower to learn but generalizes well."`](../papers/2311.18817.dichotomy-of-early-and-late-phase-implicit-biases-can-provably-induce-grokking/original/2311.18817.dichotomy-of-early-and-late-phase-implicit-biases-can-provably-induce-grokking.md#p16-1).
