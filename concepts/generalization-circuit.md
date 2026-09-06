# Generalisation circuit

[approximate-chinese-remainder-theorem](approximate-chinese-remainder-theorem.md) ← previous card, next → [model-complexity-error-tradeoff](model-complexity-error-tradeoff.md)

[Concept card index](index.md), category: [2. Mechanisms and representations](index.md#cat-2)\
→ Next category: [Modular arithmetic](modular-arithmetic.md)\
← Previous category: [Grokking](grokking.md)

## Definition

**The generalisation circuit** is the part of the network that carries out the generalising solution of the task, as against the **memorising circuit**, which achieves the same zero training error by another route. The framing belongs to the mechanistic line: *"the network implements two classes of circuits"* — the "memorising" ones first, the "generalising" ones later — both being admissible solutions on the training distribution \[[1.1](#ref-1-1)\]. [Grokking](grokking.md) is then not the appearance of an ability but a change in which circuit determines the answer.

## Elaboration

**How they are told apart.** The distinction is useless until the circuits can be measured separately. Hence a pair of [progress measures](progress-measures.md): one tracks the performance of the generalising circuit alone, the other what is left without it \[[1.1](#ref-1-1)\]. That pair is what makes the claim "the circuit had formed before the jump" testable rather than rhetorical.

**Where the boundary between them runs.** The [circuit efficiency](circuit-efficiency.md) frame supplies a quantitative criterion: the critical data size is the sample size at which *"memorizing and generalizing circuits produce identical logits"* \[[2.1](#ref-2-1)\]. Below it memorisation wins, above it generalisation does; the transition stops being a riddle about time and becomes the crossing of two curves.

**How obligatory the circuit is.** The line is not beyond dispute. It has been shown that tuning a single output-scale (laziness) parameter is enough to make grokking on the same one-layer transformer vanish continuously \[[3.1](#ref-3-1)\] — that is, the presence of two circuits does not by itself entail a delay; the delay depends on the training regime. And works that mechanistically re-examine grokked models find cases where no generalising circuit forms at all and the rise in accuracy is explained by an embedding of what was memorised — see [behavioural versus true grokking](behavioral-vs-true-grokking.md).

**Relation to [Fourier circuits](fourier-features-circuits.md).** On modular addition the generalising circuit is known by name — a set of frequencies and the operations on them; there "the generalisation circuit" stops being an abstraction and acquires an address in the weights. In tasks where the algorithm is unknown, the notion remains definable only through measures: the circuit is whatever gives the right answer in isolation from the rest \[[3.2](#ref-3-2)\].

## Alternative definitions and nuances

### A. Two classes of circuits

The original form: a memorising and a generalising circuit coexist, both solve the training sample, and they differ in their behaviour on the held-out one \[[1.1](#ref-1-1)\]. The distinguishing feature is that it is made operational through a pair of measures: the restricted loss and the excluded one. A caveat: "circuit" here is not a delimited subnetwork with boundaries, but whatever the measure catches.

### B. The circuit as the more economical solution

A reading through efficiency: the generalising circuit wins not by being "more correct" but by being cheaper in norm per unit of performance; the point where the logits are equal fixes the critical data size \[[2.1](#ref-2-1)\]. The source of the difference is predictive power: the frame predicts reversible phenomena (ungrokking, semi-grokking) near the boundary, which a descriptive distinction does not.

### C. The circuit as an addressable subnetwork

The strongest form, available wherever the algorithm has been worked out: the circuit is the specific frequencies and heads that can be filtered out and checked in isolation. The distinguishing feature is a test of sufficiency (does the circuit work alone) and of necessity (does the network work without it), not merely an agreement of curves \[[3.2](#ref-3-2)\].

## References

###### ref-1-1
**\[1.1\]** 2302.03025 — Chughtai et al., "A Toy Model of Universality: Reverse Engineering how Networks Learn Group Operations". [`"We argue that the network implements two classes of cir"`](../papers/2302.03025.a-toy-model-of-universality-reverse-engineering-how-networks-learn-group-operations/2302.03025.a-toy-model-of-universality-reverse-engineering-how-networks-learn-group-operations.card.md#p6-11).

## References of works that joined the discussion

### Contested

###### ref-2-1
**\[2.1\]** 2401.10463 — Zhu et al., "Critical Data Size of Language Models from a Grokking Perspective". Refines: the boundary between the circuits acquires a number — the critical data size as the point of equal logits. [`"They define ‘critical data size’ as the number of data points at which memorizing and generalizing circuits produce identical logits."`](../papers/2401.10463.critical-data-size-of-language-models-from-a-grokking-perspective/2401.10463.critical-data-size-of-language-models-from-a-grokking-perspective.card.md#p12-2).

### In support

###### ref-3-1
**\[3.1\]** 2310.06110 — Kumar et al., "Grokking as the Transition from Lazy to Rich Training Dynamics". Nuance: the presence of two circuits does not entail a delay — tuning a single laziness parameter makes grokking vanish continuously. [`"merely tuning the network output scaling/laziness parameter $\alpha$ is alone sufficient to make grokking continuously vanish"`](../papers/2310.06110.grokking-as-the-transition-from-lazy-to-rich-training-dynamics/original/2310.06110.grokking-as-the-transition-from-lazy-to-rich-training-dynamics.md#p3-1).

###### ref-3-2
**\[3.2\]** 2312.06581 — Stander et al., "Grokking Group Multiplication with Cosets". Nuance: in works where the algorithm has not been worked out, the circuit is defined by the model's behaviour rather than by an address in the weights. [`"The models we study exhibit “grokking”, wherein the model first memorizes the training set and then much later generalizes to the held out data perfectly."`](../papers/2312.06581.grokking-group-multiplication-with-cosets/original/2312.06581.grokking-group-multiplication-with-cosets.md#p2-2).
