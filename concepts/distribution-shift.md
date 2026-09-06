# Distribution shift

[Grokking outside neural networks (non-neural and solvable models)](grokking-in-non-neural-models.md) ← previous card, next → [systematic-generalization](systematic-generalization.md)

[Concept card index](index.md), category: [3. Tasks and datasets](index.md#cat-3)\
→ Next category: [Weight decay (L2 regularisation)](weight-decay.md)\
← Previous category: [Structured representation learning](structured-representation-learning.md)

## Definition

**Distribution shift** is a divergence between what the network saw during training and what it is tested on. In the corpus it appears in two roles at once: as an *explanation* of [grokking](grokking.md) and as the *condition* under which grokking is tested for robustness. The first role is stated outright: *"data sparsity induces grokking by causing a distribution shift during training"* \[[1.1](#ref-1-1)\] — that is, delayed generalisation is a consequence of the training sample representing the task incompletely.

The second role is practical: a grokked model is tested not on its own deal but on another one, and the question is whether what has been learned carries over \[[1.2](#ref-1-2)\].

## Elaboration

**How the shift is made controllable.** The value of this line is that the shift stops being a property of the data "as it happened to come out" and becomes a knob: synthetic datasets are built in which the divergence between training and testing is set exactly, and grokking is reproduced even with abundant data \[[1.1](#ref-1-1)\]. The same device is carried over to real-world data: MNIST digits are clustered in the learned feature space and the clusters are dealt out between training and testing so that the shift is known \[[3.1](#ref-3-1)\].

**The link to the [training data fraction](data-fraction-critical-dataset-size.md).** If the shift is the cause, then the critical dataset size ceases to be a separate phenomenon: below the threshold the sample systematically fails to cover the task, and that is precisely the shift. The works on scarce data join these two questions directly — the regime below the threshold, where grokking is unobservable, and the transfer to another distribution \[[1.2](#ref-1-2)\].

**Transfer of grokked knowledge.** Hence an applied question: can a grokked model be used to train another one on a different distribution \[[3.2](#ref-3-2)\]. Here the shift is no longer an obstacle but a condition of the task: the teacher is trained on one modulus, the student is trained on another.

**What the shift does not explain.** In settings where both samples are drawn from a single operation table by a random split, the distributions coincide by construction, and yet the delay is there. The shift is therefore an explanation for some of the cases rather than a general mechanism; the strong form of the claim ("grokking is a consequence of the shift") requires showing a shift where none was deliberately introduced.

## Alternative definitions and nuances

### A. The shift as the cause of the delay

The strong form: an incomplete coverage of the task by the training sample produces a divergence which the network does not overcome at once \[[1.1](#ref-1-1)\]. The distinguishing feature is testability by intervention: the shift is set explicitly and one looks at whether grokking appears with abundant data. Caveat: reproducing grokking under an imposed shift does not prove that the same mechanism was at work in the original settings.

### B. The shift as a condition of the test

Weaker in its claims, closer to practice: we trained on one distribution, we test on another and measure what survived \[[1.2](#ref-1-2)\], \[[3.2](#ref-3-2)\]. The controlling quantity here is the distance between the distributions (a different modulus, a different cluster), and what is measured is not the time but the preservation of what was learned.

### C. A shift induced on real-world data

A separate device: the divergence is constructed on a natural dataset by clustering the examples in the learned feature space and dealing the clusters out between training and testing \[[3.1](#ref-3-1)\]. The distinguishing feature is that the shift is known by construction while remaining "natural" in content, which closes off the usual objection to synthetic settings.

## References

###### ref-1-1
**\[1.1\]** 2502.01774 — Carvalho et al., "Grokking Explained: A Statistical Phenomenon". [`"We posit that data sparsity induces grokking by causing a distribution shift during training."`](../papers/2502.01774.grokking-explained-a-statistical-phenomenon/original/2502.01774.grokking-explained-a-statistical-phenomenon.md#p1-4).

###### ref-1-2
**\[1.2\]** 2511.04760 — Singh et al., "When Data Falls Short: Grokking Below the Critical Threshold". [`"We focus on data-scarce regimes where the number of training samples falls below the critical threshold, making grokking unobservable, and on practical scenarios involving distribution s"`](../papers/2511.04760.when-data-falls-short-grokking-below-the-critical-threshold/original/2511.04760.when-data-falls-short-grokking-below-the-critical-threshold.md#p1-3).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2502.01774 — Carvalho et al., "Grokking Explained: A Statistical Phenomenon". Nuance: the shift is induced on real-world data as well — by clustering digits in the learned feature space — so that it is known by construction. [`"we conduct experiments on the MNIST dataset to explore grokking under a real-world scenario of induced distribution shifts"`](../papers/2502.01774.grokking-explained-a-statistical-phenomenon/original/2502.01774.grokking-explained-a-statistical-phenomenon.md#p1-6).

###### ref-3-2
**\[3.2\]** 2511.04760 — Singh et al., "When Data Falls Short: Grokking Below the Critical Threshold". Nuance: the shift turns into a condition of the task — a grokked teacher trains a student on a different distribution. [`"**Can a grokked model be leveraged to *train* another model on a different distribution?**"`](../papers/2511.04760.when-data-falls-short-grokking-below-the-critical-threshold/original/2511.04760.when-data-falls-short-grokking-below-the-critical-threshold.md#p1-5).
