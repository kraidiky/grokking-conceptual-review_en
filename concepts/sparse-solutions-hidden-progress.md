# Sparse solutions and hidden progress

[model-complexity-error-tradeoff](model-complexity-error-tradeoff.md) ← previous card, next → [activation-sparsity](activation-sparsity.md)

[Concept card index](index.md), category: [2. Mechanisms and representations](index.md#cat-2)\
→ Next category: [Modular arithmetic](modular-arithmetic.md)\
← Previous category: [Grokking](grokking.md)

## Definition

**Hidden progress** is advance inside the network that goes on gradually and monotonically while the outward measures (loss, accuracy) stand on a plateau: from outside one sees a long plateau and a sharp jump, while inside the required feature is smoothly strengthening \[[1.1](#ref-1-1)\]. The notion was introduced on parity learning, where it is shown that *"black-box losses and accuracies exhibit a long plateau and sharp phase transition, hiding gradual progress in the SGD iterates"* \[[1.1](#ref-1-1)\], and it was carried over from there to [grokking](grokking.md).

The other half of the notion is the **sparsity of the solution**: what this progress leads to. The generalising solution turns out to be concentrated on a few directions (frequencies, neurons, a subnetwork), whereas the memorising one is smeared out, and it is precisely the passage to the sparse solution that looks from outside like a jump.

## Elaboration

Tying the two halves together is what makes the notion workable: if the solution is sparse, then it has a measurable coordinate (what share of the power sits on the required directions), and this coordinate grows long before the jump in accuracy — that is, it serves as a **hidden progress measure**. Nanda et al. put the task exactly this way: to find measures that *"precede"* the sharp transition and make it predictable \[[1.2](#ref-1-2)\], and they obtain them not by search but from a mechanistic account of the learned algorithm \[[3.2](#ref-3-2)\].

**How hidden progress differs from [progress measures](progress-measures.md).** A progress measure is an instrument; hidden progress is the claim that there is something to measure: monotone motion runs beneath the plateau rather than treading in place. The difference is testable: the work on parities shows a Fourier gap growing during the plateau \[[3.1](#ref-3-1)\], whereas an analysis of embeddings at the early steps of grokking finds no structure either in PCA or in t-SNE \[[3.3](#ref-3-3)\] — that is, hidden progress is not visible to every measure and not in every setting.

**Where sparsity becomes the cause.** If the generalising solution is a sparse subnetwork competing with a dense memorising one, then the transition is a change of winner rather than the appearance of a new ability; hidden progress is then the accumulation of weight on the sparse branch. This line meets [sparse subnetworks](sparse-subnetwork-lottery-ticket.md) and [circuit efficiency](circuit-efficiency.md), where the generalising scheme beats the memorising one in norm per unit of performance.

**A caveat about the setting.** The original result was obtained in online training with fresh batches, which removes overfitting but couples training time and the number of independent examples — the authors state this plainly \[[2.1](#ref-2-1)\]. Carrying it over to grokking, where the sample is fixed and overfitting is essential, is therefore not automatic.

## Alternative definitions and nuances

### A. Hidden progress as a measurable quantity beneath the plateau

The strong form: there exists a quantity that grows monotonically during the plateau and predicts the jump \[[1.1](#ref-1-1)\], \[[3.1](#ref-3-1)\]. The distinguishing feature is predictive power: the quantity must lead the transition, not coincide with it. Hence the requirement on any such measure — a stable lead across seeds, failing which it is useless as a precursor.

### B. Hidden progress as a consequence of a mechanism

Weaker in form, stronger in grounding: the measure is not sought by search but derived from the algorithm once it has been worked out — knowing that the network computes sums through a discrete transform, one can watch the share of power in the required frequencies \[[1.2](#ref-1-2)\], \[[3.2](#ref-3-2)\]. The source of the difference: such a measure is tied to a specific task and does not carry over to a setting where the algorithm is unknown.

### C. Sparsity as a property of the solution rather than of the path

The third reading looks not at the path but at the outcome: the generalising solution occupies few directions, the memorising one many. "Hidden progress" is then the gradual flow of power between two solutions. A caveat: the sparsity of the outcome does not by itself prove that the transition was gradual on the inside — it is equally consistent with an abrupt rearrangement, and therefore calls for a separate measurement along training \[[3.3](#ref-3-3)\].

## References

###### ref-1-1
**\[1.1\]** 2207.08799 — Barak et al., "Hidden Progress in Deep Learning: SGD Learns Parities Near the Computational Limit". [`"Black-box losses and accuracies exhibit a long plateau and sharp phase transition (top), hiding gradual progress in the SGD iterates (bottom)."`](../papers/2207.08799.hidden-progress-in-deep-learning-sgd-learns-parities-near-the-computational-limit/2207.08799.hidden-progress-in-deep-learning-sgd-learns-parities-near-the-computational-limit.card.md#fig-3).

###### ref-1-2
**\[1.2\]** 2301.05217 — Nanda et al., "Progress measures for grokking via mechanistic interpretability". [`"We could better understand and predict these phase transitions by finding *hidden progress measures* (Barak et al., 2022): metrics that precede and ar"`](../papers/2301.05217.progress-measures-for-grokking-via-mechanistic-interpretability/2301.05217.progress-measures-for-grokking-via-mechanistic-interpretability.card.md#p1-4).

## References of works that joined the discussion

### Contested

###### ref-2-1
**\[2.1\]** 2207.08799 — Barak et al., "Hidden Progress in Deep Learning: SGD Learns Parities Near the Computational Limit". Limits: the original result was obtained in online training, which removes overfitting and therefore does not match the grokking setting on a fixed sample. [`"While this mitigates the confounding factor of overfitting, it couples the resources of training time and independent samples in a suboptimal way"`](../papers/2207.08799.hidden-progress-in-deep-learning-sgd-learns-parities-near-the-computational-limit/2207.08799.hidden-progress-in-deep-learning-sgd-learns-parities-near-the-computational-limit.card.md#p10-3).

### In support

###### ref-3-1
**\[3.1\]** 2210.01117 — Liu et al., "Omnigrok: Grokking Beyond Algorithmic Data". Nuance: hidden progress is named here as one of the partial answers to the question of the cause of grokking, alongside the slow formation of representations. [`"Barak et al. [2022] uses Fourier gap to describe hidden progress"`](../papers/2210.01117.omnigrok-grokking-beyond-algorithmic-data/original/2210.01117.omnigrok-grokking-beyond-algorithmic-data.md#p1-8)

###### ref-3-2
**\[3.2\]** 2301.05217 — Nanda et al., "Progress measures for grokking via mechanistic interpretability". Nuance: the measure is not sought by search but derived from a mechanistic account of the learned algorithm. [`"we introduce a different approach to uncovering hidden progress measures: via *mechanistic explanations*"`](../papers/2301.05217.progress-measures-for-grokking-via-mechanistic-interpretability/2301.05217.progress-measures-for-grokking-via-mechanistic-interpretability.card.md#p1-5).

###### ref-3-3
**\[3.3\]** 2205.10343 — Liu et al., "Towards Understanding Grokking: An Effective Theory of Representation Learning". Nuance: hidden progress is not visible to every measure — at the early steps neither PCA nor t-SNE finds structure in the embeddings. [`"We study the embeddings at different training times and find that neither PCA (shown in Figure 1) nor t-SNE (not shown here) reveal any structure."`](../papers/2205.10343.towards-understanding-grokking-an-effective-theory-of-representation-learning/original/2205.10343.towards-understanding-grokking-an-effective-theory-of-representation-learning.md#p8-8).
