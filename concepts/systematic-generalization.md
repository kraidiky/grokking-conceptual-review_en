# Systematic generalization (hierarchical generalization)

[Distribution shift](distribution-shift.md) ← previous card, next → —

[Concept card index](index.md), category: [3. Tasks and datasets](index.md#cat-3)\
→ Next category: [Weight decay (L2 regularisation)](weight-decay.md)\
← Previous category: [Structured representation learning](structured-representation-learning.md)

## Definition

**Systematic generalization** is the ability to apply a learned rule to inputs built differently from everything seen: not to new examples of the same kind, but to new combinations. In the corpus it arrives through language: the datasets are constructed so that *"both a non-hierarchical as well as a hierarchical rule can perfectly fit the training set, but only the hierarchical rule generalizes to structurally novel inputs"* \[[1.1](#ref-1-1)\]. This makes the task an almost ideal test for [grokking](grokking.md): the fit is possible in two ways, and the only question is which of them the network will choose and when.

Hence the name for the phenomenon in this area — **structural grokking**: generalisation to structurally novel inputs keeps improving after the in-domain quality has already saturated \[[1.2](#ref-1-2)\].

## Elaboration

**Why this is not just one more task.** In [modular arithmetic](modular-arithmetic.md) the generalising solution is unique and known; here there are two of them, and they differ not in efficiency but in the kind of rule — linear or hierarchical. This makes it possible to ask not "when will the network generalise" but "which rule will it prefer", and makes the preference measurable on structurally novel inputs rather than on a held-out part of the same table.

**Non-monotonicity in depth.** Structural grokking depends on [depth](overparameterization-depth.md) through an inverted U-shaped curve: hierarchical generalisation first improves and then declines as the model gets deeper \[[1.2](#ref-1-2)\]. This echoes the non-monotonicity found in modular arithmetic, but it is obtained on a different family of tasks and so serves as independent evidence.

**The role of the training objective.** A separate finding of this line: the inclination towards hierarchical generalisation is induced by the language-modelling objective itself rather than by the architecture — when the objective is changed the behaviour changes, and the result carries over even to recurrent networks \[[3.1](#ref-3-1)\]. For the corpus this matters because it moves the question from the make-up of the network to the make-up of the training signal.

**A methodological trap.** Early works declared that ordinary transformers fail such tests; the explanation turned out to be procedural — early stopping on in-domain quality, which cuts training off exactly before the structural generalisation arrives \[[3.2](#ref-3-2)\]. This is the same class of error as too short a step budget in [measuring the grokking time](grokking-time.md): the negative result turns out to be a property of the protocol.

## Alternative definitions and nuances

### A. Generalisation to structurally novel inputs

A definition through the data: the training sample admits two rules, the test sample tells them apart \[[1.1](#ref-1-1)\]. The distinguishing feature is that the criterion of success is not "a high accuracy" but "the right rule was chosen", and so the test requires a specially built dataset rather than a random split.

### B. Structural grokking

A definition through the dynamics: what is of interest is not the fact but the timing — generalisation keeps improving after the in-domain quality has saturated \[[1.2](#ref-1-2)\]. The source of difference: what is measured here is the gap between two curves in time rather than the final value, and so the result is sensitive to the length of training and to the stopping rule \[[3.2](#ref-3-2)\].

### C. A bias induced by the training objective

The third position explains the preference for a rule neither by the architecture nor by the data, but by the training objective \[[3.1](#ref-3-1)\]. The controlling quantity is the kind of objective (language modelling against seq2seq); the practical consequence is that the dispute "is recurrence needed for hierarchy" turns out to be ill-posed until the objective is fixed.

## References

###### ref-1-1
**\[1.1\]** 2305.18741 — Murty et al., "Grokking of Hierarchical Structure in Vanilla Transformers". [`"These datasets are constructed so that both a non-hierarchical as well as a hierarchical rule can perfectly fit the training set, but only the hierarchical rule generalizes to structurally novel inputs."`](../papers/2305.18741.grokking-of-hierarchical-structure-in-vanilla-transformers/original/2305.18741.grokking-of-hierarchical-structure-in-vanilla-transformers.md#fig-1).

###### ref-1-2
**\[1.2\]** 2305.18741 — Murty et al., "Grokking of Hierarchical Structure in Vanilla Transformers". [`"we show that structural grokking exhibits inverted U-shaped scaling behavior as a function of model depth: hierarchical generalization improves, then declines, as we train deeper models"`](../papers/2305.18741.grokking-of-hierarchical-structure-in-vanilla-transformers/original/2305.18741.grokking-of-hierarchical-structure-in-vanilla-transformers.md#p1-4).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2404.16367 — Ahuja et al., "Learning Syntax Without Planting Trees: Understanding Hierarchical Generalization in Transformers". Nuance: the preference for the hierarchical rule is induced by the training objective rather than by the architecture, and carries over to recurrent networks. [`"Our results above suggest that the language modeling objective imposes bias towards hierarchical generalization in transformers."`](../papers/2404.16367.learning-syntax-without-planting-trees-understanding-hierarchical-generalization-in-transformers/original/2404.16367.learning-syntax-without-planting-trees-understanding-hierarchical-generalization-in-transformers.md#p6-7).

###### ref-3-2
**\[3.2\]** 2305.18741 — Murty et al., "Grokking of Hierarchical Structure in Vanilla Transformers". Nuance: the earlier negative results were explained by the protocol — early stopping on in-domain quality. [`"We attribute these failures to early stopping based on in-domain validation performance"`](../papers/2305.18741.grokking-of-hierarchical-structure-in-vanilla-transformers/original/2305.18741.grokking-of-hierarchical-structure-in-vanilla-transformers.md#p1-5).
