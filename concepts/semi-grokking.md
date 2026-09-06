# Semi-grokking

[Catastrophic forgetting](catastrophic-forgetting.md) ← previous card, next → [behavioral-vs-true-grokking](behavioral-vs-true-grokking.md)

[Concept card index](index.md), category: [1. Phenomena](index.md#cat-1)\
→ Next category: [Structured representation learning](structured-representation-learning.md)\
← Previous category: [Effective theory and statistical mechanics](effective-theory-statistical-mechanics.md)

## Definition

**Semi-grokking** is delayed generalisation that reaches not perfect but merely **partial** ("middling") test accuracy: the network groks, yet settles at incomplete quality. Discovered by Varma et al. (2023) as a relative of [grokking](grokking.md) and [ungrokking](ungrokking.md), following from the same theory of [circuit efficiency](circuit-efficiency.md) \[[1.1](#ref-1-1)\].

![Semi-grokking near the critical data size: accuracy, loss and parameter norm of a single run — generalisation halts at a partial level (fig. 6 of Varma et al.)](assets/semi-grokking-run.png)

## Elaboration

Semi-grokking is tied to the **[critical data size](data-fraction-critical-dataset-size.md)** Dcrit — the size of the training set at which the memorising and the generalising circuit (the subnetworks that respectively store examples and carry out the general algorithm) are equally efficient. Where ungrokking takes a dataset *smaller* than Dcrit (memorisation wins, generalisation is lost), semi-grokking takes a size *right around* Dcrit: the [phase transition](phase-transition.md) to generalisation does happen, but it only brings the network out at an intermediate, "middling" test accuracy \[[1.1](#ref-1-1)\]. Semi-grokking is thus neither a relapse nor a full grok, but a stable **plateau of partial generalisation** at the point where the two circuits are equally efficient.

## Alternative definitions and nuances

### A. A plateau of partial generalisation at Dcrit (Varma)

The canonical reading: at D ≈ Dcrit the phase transition brings the network out only at incomplete test accuracy \[[1.1](#ref-1-1)\]. The source of the difference: the control parameter is the dataset size taken exactly at the threshold of equal circuit efficiency.

### In support

- **Moderate capabilities at the critical size** \[[3.1](#ref-3-1)\]: at the critical data size the model shows semi-grokking — moderate generalisation; an independent reproduction within the circuits-competition frame. The source of the difference: the same behaviour obtained inside a different theoretical frame.

## References

###### ref-1-1
**\[1.1\]** 2309.02390 — Varma et al., "Explaining grokking through circuit efficiency". [`"semi-grokking, in which a network shows delayed generalisation to partial rather than perfect test accuracy"`](../papers/2309.02390.explaining-grokking-through-circuit-efficiency/2309.02390.explaining-grokking-through-circuit-efficiency.card.md#p1-3).\
Also (the mechanism): [`"leading to a phase transition but only to middling test accuracy"`](../papers/2309.02390.explaining-grokking-through-circuit-efficiency/2309.02390.explaining-grokking-through-circuit-efficiency.card.md#p2-1).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2402.15175 — Huang et al., "Unified View of Grokking, Double Descent and Emergent Abilities: A Perspective from Circuits Competition". Nuance: semi-grokking is reproduced within the circuits-competition frame. [`"named semi-grokking, characterized by moderate generalization capabilities"`](../papers/2402.15175.unified-view-of-grokking-double-descent-and-emergent-abilities/original/2402.15175.unified-view-of-grokking-double-descent-and-emergent-abilities.md#p2-2).

## Passing mentions

Works that only mention the phenomenon — a literature review, a related-work paragraph, a passing citation — without examining it.

**\[4.1\]** 2511.04760 — Singh et al., "When Data Falls Short: Grokking Below the Critical Threshold". [`"Training below this threshold yields semi-grokking, and fine-tuning grokked models on such small data can cause “ungrokking.”"`](../papers/2511.04760.when-data-falls-short-grokking-below-the-critical-threshold/original/2511.04760.when-data-falls-short-grokking-below-the-critical-threshold.md#p2-4).

**\[4.2\]** 2509.21519 — Tian, "Provable Scaling Laws of Feature Emergence from Learning Dynamics of Grokking". [`"Boundary of generalization and memorization (semi-grokking (Varma et al., 2023))"`](../papers/2509.21519.provable-scaling-laws-of-feature-emergence-from-learning-dynamics-of-grokking/original/2509.21519.provable-scaling-laws-of-feature-emergence-from-learning-dynamics-of-grokking.md#p8-2).

**\[4.3\]** 2601.19791 — Xu et al., "To Grok Grokking: Provable Grokking in Ridge Regression". [`"Varma et al. (2023) interpreted grokking from the perspective of circuit efficiency, and discovered two related phenomena named “ungrokking” and “semi-grokking”"`](../papers/2601.19791.to-grok-grokking-provable-grokking-in-ridge-regression/original/2601.19791.to-grok-grokking-provable-grokking-in-ridge-regression.md#p3-2).

**\[4.4\]** 2401.10463 — Zhu et al. 2024. Nuance: semi-grokking is mentioned only as the content of Varma et al., from whose setup the authors distance themselves; the paper has no experiments of its own at the critical size with intermediate accuracy. [`"Training with these data points will result in suboptimal test loss (i.e., semi-grokking)."`](../papers/2401.10463.critical-data-size-of-language-models-from-a-grokking-perspective/2401.10463.critical-data-size-of-language-models-from-a-grokking-perspective.card.md#p12-2).
