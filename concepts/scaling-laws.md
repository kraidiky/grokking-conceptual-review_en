# Scaling laws

[Criticality and the critical point](criticality-critical-point.md) ← previous card, next → [quadratic-networks](quadratic-networks.md)

[Concept card index](index.md), category: [7. Theory and formal results](index.md#cat-7)\
→ Next category: [Grokking](grokking.md)\
← Previous category: [Progress measures](progress-measures.md)

## Definition

**Scaling laws** are power-law dependences of a model's performance on model size, data volume and compute budget, established for large language models and carried over into the conversation about [grokking](grokking.md) as a frame that delayed generalisation must either fit into or contradict. They appear in the corpus in two ways: as one of the "striking discoveries" about generalisation alongside [double descent](double-descent.md), grokking and [emergence](emergence.md) \[[1.1](#ref-1-1)\], and as an object of derivation — a law describing the boundary between memorisation and generalisation is proved from the learning dynamics \[[1.2](#ref-1-2)\].

## Elaboration

The difference between the two usages matters more than it seems. A classical scaling law is an empirical fit: the loss falls as a power of the number of parameters and of the amount of data, monotonically and smoothly \[[3.2](#ref-3-2)\]. The law the grokking corpus speaks of is a claim about a **threshold**: at what amount of data the learned features stop being generalisable and remain memorising ones \[[1.2](#ref-1-2)\].

**Where the frame breaks.** A smooth power law sits badly with a sharp transition: abilities that look as though they appear in a jump call the very monotonicity into question \[[3.3](#ref-3-3)\], while in the simplified setting of modular arithmetic the familiar "larger models are better at the same data" simply fails to hold — some smaller models overtake slightly larger ones \[[3.1](#ref-3-1)\]. That is the point the notion is kept in the corpus for: grokking serves as a counterexample to the naive reading of the laws.

**The dispute about sharpness.** A line of its own contests the sharpness itself: step-like curves may be produced by a discrete evaluation metric rather than by an internal rearrangement of the network \[[2.1](#ref-2-1)\]. For scaling laws this is critical — if the step is an artefact of the metric, then no smooth law is violated and there is nothing to argue about; if the step is real, then the law does not describe everything.

**What deriving the law from the dynamics gives.** When a law is obtained not by fitting but from the equations of learning, it acquires testable consequences: it predicts how large a sample is needed for the generalising features to remain stable, and how this depends on [weight decay](weight-decay.md), the [learning rate](learning-rate.md) and the structure of the task \[[1.2](#ref-1-2)\], \[[3.4](#ref-3-4)\]. Such a law speaks of a boundary that shows on the [phase diagram](phase-diagram.md) as a line — and it is therefore checked at points, not along the tail of a curve.

## Alternative definitions and nuances

### A. The empirical power law

The original form: the loss as a power function of scale, fitted over many runs \[[3.2](#ref-3-2)\], \[[3.3](#ref-3-3)\]. The control quantities are the number of parameters, the amount of data, the compute budget; the prediction is monotone and knows nothing of internal rearrangements. It is against this form that the works on grokking press their claim: it does not forbid delayed generalisation, but it does not describe it either.

### B. The law of the memorisation/generalisation boundary

Here the quantity is not the loss but the position of the threshold: how much data is needed for the learned local maxima to remain generalisable \[[1.2](#ref-1-2)\]. The distinguishing feature is that the law is derived from the dynamics and checked by the predicted boundary matching the measured one, not by the quality of a tail fit \[[3.4](#ref-3-4)\]. That puts it closer to the critical sample size of the [data line](data-fraction-critical-dataset-size.md) than to the Kaplan laws.

### C. The dispute over what actually scales

The third position: the observed step is a property of the metric, not of the model \[[2.1](#ref-2-1)\]. The source of the difference here is methodological: a continuous measure (the loss, the probability of the correct answer) may rise smoothly where a discrete one (accuracy) gives a jump. For the card this means that any claim "the scaling law is violated under grokking" requires saying by which measure it was obtained.

## References

###### ref-1-1
**\[1.1\]** 2401.10463 — Zhu et al., "Critical Data Size of Language Models from a Grokking Perspective". [`"researchers have made a series of striking discoveries across generalization abilities, including neural scaling laws [4], double descent [11], grokking [15] and emergent abilities [23]"`](../papers/2401.10463.critical-data-size-of-language-models-from-a-grokking-perspective/2401.10463.critical-data-size-of-language-models-from-a-grokking-perspective.card.md#p1-3).

###### ref-1-2
**\[1.2\]** 2509.21519 — Tian, "Provable Scaling Laws of Feature Emergence from Learning Dynamics of Grokking". [`"*Scaling Laws of Feature Emergence, Generalization and Memorization* can be derived by inspecting how the landscape changes with the data distribution."`](../papers/2509.21519.provable-scaling-laws-of-feature-emergence-from-learning-dynamics-of-grokking/original/2509.21519.provable-scaling-laws-of-feature-emergence-from-learning-dynamics-of-grokking.md#p2-5).

## References of works that joined the discussion

### Contested

###### ref-2-1
**\[2.1\]** 2511.12768 — Hong et al., "Evidence of Phase Transitions in Small Transformer-Based Language Models". Contests: step-like curves may be produced by a discrete evaluation metric rather than by an internal rearrangement of the network — in which case no smooth law is violated. [`"They argued mathematically and empirically that many step-like curves reported in Wei et al. arise from discrete, non-linear evaluation metrics rather than abrupt internal reorganizations."`](../papers/2511.12768.evidence-of-phase-transitions-in-small-transformer-based-language-models/original/2511.12768.evidence-of-phase-transitions-in-small-transformer-based-language-models.md#p4-2).

### In support

###### ref-3-1
**\[3.1\]** 2401.10463 — Zhu et al., "Critical Data Size of Language Models from a Grokking Perspective". Nuance: in the simplified setting the familiar "larger models are better at the same data" fails to hold. [`"As shown in Figure 4A, some smaller models achieve better performance than slightly la"`](../papers/2401.10463.critical-data-size-of-language-models-from-a-grokking-perspective/2401.10463.critical-data-size-of-language-models-from-a-grokking-perspective.card.md#p8-1).

###### ref-3-2
**\[3.2\]** 2412.09810 — DeMoss et al., "The Complexity Dynamics of Grokking". Nuance: the monotone "bigger is better" is named as the contemporary view, and it is that view grokking presents its bill to. [`"the contemporary view in deep learning is that “larger models are better” [12], with empirically observed scaling laws across a range of modalities and architectures"`](../papers/2412.09810.the-complexity-dynamics-of-grokking/original/2412.09810.the-complexity-dynamics-of-grokking.md#p5-1).

###### ref-3-3
**\[3.3\]** 2503.23298 — Wang et al., "Learning Towards Emergence: Paving the Way to Induce Emergence by Inhibiting Monosemantic Neurons on Pre-trained Models". Nuance: the law is usually a mild power law, and it is against that background that sharp abilities look like an exception. [`"Studies on Scaling Laws (Henighan et al., 2020; Kaplan et al., 2020) have analyzed the relationship between scale and performance, which typically follows a"`](../papers/2503.23298.learning-towards-emergence-inhibiting-monosemantic-neurons-on-pre-trained-models/2503.23298.learning-towards-emergence-inhibiting-monosemantic-neurons-on-pre-trained-models.card.md#p1-3).

###### ref-3-4
**\[3.4\]** 2509.21519 — Tian, "Provable Scaling Laws of Feature Emergence from Learning Dynamics of Grokking". Nuance: the proved law is checked by the predicted boundary matching the measured one, not by the quality of a fit. [`"the proved scaling laws about the generalization/memorization boundary (Thm. 4) fits well with the experiments"`](../papers/2509.21519.provable-scaling-laws-of-feature-emergence-from-learning-dynamics-of-grokking/original/2509.21519.provable-scaling-laws-of-feature-emergence-from-learning-dynamics-of-grokking.md#fig-1).
