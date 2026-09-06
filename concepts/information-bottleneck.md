# Information bottleneck

[quadratic-networks](quadratic-networks.md) ← previous card, next → [Singular learning theory (SLT)](singular-learning-theory.md)

[Concept card index](index.md), category: [7. Theory and formal results](index.md#cat-7)\
→ Next category: [Grokking](grokking.md)\
← Previous category: [Progress measures](progress-measures.md)

## Definition

**The information bottleneck** is a frame in which learning is described as compression of the input while the information about the target is preserved, and which predicts two spells: fitting, and then compression. For [grokking](grokking.md) it is attractive because it offers a ready explanation of the delay — generalisation arrives in the second spell — and that is exactly how the corpus cites it: the theory of the information bottleneck *"suggests a compression phase followed by a fitting phase"*, with the qualification that this very picture is sensitive to technical details \[[1.1](#ref-1-1)\].

## Elaboration

**Why the frame did not become the default explanation.** The qualification it enters the corpus with matters more than the frame itself: the dispute over whether a compression spell exists at all has been running since 2018 and turns on how one estimates mutual information in a deterministic network. In the grokking corpus it is therefore used as a metaphor for the order of events, not as a measured quantity.

**What took its place.** Practically the same work is done by measures of [representation compression](manifold-representation-compression.md) and of [complexity](model-complexity-error-tradeoff.md): the linear mapping number, the effective rank, the spectral entropy. They are computable without estimating mutual information and are therefore testable — that is their advantage over the bottleneck \[[3.1](#ref-3-1)\].

**How the corpus keeps it.** Not on its own but in a bundle: grokking, [double descent](double-descent.md) and the bottleneck are treated as three frames with a common underlying structure \[[3.2](#ref-3-2)\], and that is what makes it useful — it supplies a vocabulary shared by three lines, while grokking serves as the clean setting where compression, generalisation and memorisation can be traced exactly \[[1.2](#ref-1-2)\].

**Where the frame does work.** It remains useful as a language for putting the question: what exactly the network throws away at the transition and what it keeps. In that form it meets [grokking as compression](manifold-representation-compression.md) and the line where delayed generalisation is read as a descent towards a solution of lower complexity \[[3.1](#ref-3-1)\].

## Alternative definitions and nuances

### A. Two spells: fitting and compression

The original form \[[1.1](#ref-1-1)\]. The distinguishing feature is that the order of events is predicted, not their timing; hence the weakness too: observing a delay is consistent with the frame but does not confirm it, because other pictures predict the same order.

### B. Compression measured without mutual information

The substitute form: instead of estimating $I(X;T)$ one takes a computable measure of representation complexity \[[3.1](#ref-3-1)\]. The source of the difference is testability: the quantity is computed exactly, and the claim "the network has compressed" stops depending on how information is estimated.

## References

###### ref-1-1
**\[1.1\]** 2310.05918 — Liu et al., "Grokking as Compression: A Nonlinear Complexity Perspective". [`"The theory of information bottleneck Tishby et al. [2000] suggests a compression phase followed by a fitting phase, although the compression story is sensitive to technical details"`](../papers/2310.05918.grokking-as-compression-a-nonlinear-complexity-perspective/original/2310.05918.grokking-as-compression-a-nonlinear-complexity-perspective.md#p5-1).

###### ref-1-2
**\[1.2\]** 2509.20829 — Sakamoto et al., "Explaining Grokking and Information Bottleneck through Neural Collapse Emergence". [`"Two prominent examples are grokking, where test performance improves abruptly long after the training loss has plateaued, and the information bottleneck principle"`](../papers/2509.20829.explaining-grokking-and-information-bottleneck-through-neural-collapse-emergence/2509.20829.explaining-grokking-and-information-bottleneck-through-neural-collapse-emergence.card.md#p1-2).

## References of works that joined the discussion

### In support

###### ref-3-2
**\[3.2\]** 2504.12700 — de Mello Koch & Ghosh, "A Two-Phase Perspective on Deep Learning Dynamics". Nuance: the frame enters the corpus not on its own but as one of three that are supposed to share a common structure — together with grokking and double descent. [`"We propose that these frameworks are not merely analogous but reflect a common underlying structure"`](../papers/2504.12700.a-two-phase-perspective-on-deep-learning-dynamics/original/2504.12700.a-two-phase-perspective-on-deep-learning-dynamics.md#p3-2).

###### ref-3-1
**\[3.1\]** 2310.05918 — Liu et al., "Grokking as Compression: A Nonlinear Complexity Perspective". Nuance: the place of the untestable information measure is taken by a computable measure of representation complexity. [`"We define *linear mapping number* (LMN) to measure network complexity"`](../papers/2310.05918.grokking-as-compression-a-nonlinear-complexity-perspective/original/2310.05918.grokking-as-compression-a-nonlinear-complexity-perspective.md#p1-2).
