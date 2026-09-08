# Intrinsic task symmetry

[The Clock and the Pizza algorithms](clock-vs-pizza.md) ← previous card, next → [Frequency principle and spectral bias](frequency-principle-spectral-bias.md)

[Concept card index](index.md), category: [2. Mechanisms and representations](index.md#cat-2)\
→ Next category: [Modular arithmetic](modular-arithmetic.md)\
← Previous category: [Grokking](grokking.md)

## Definition

**Intrinsic task symmetry** is the invariance of the rule generating the data under a transformation of the input: a permutation of the operands (commutativity), a regrouping (associativity), transitivity in comparison tasks, the triangle equality in graph tasks. The notion is introduced as an account of [grokking](grokking.md) in the order of causes: *"intrinsic task symmetry is the key driver of generalization"*, determining the particular kind of geometry learned in algorithmic tasks \[[1.1](#ref-1-1)\]. From this follows a division of training into three spells — *"(i) memorization, (ii) symmetry acquisition, and (iii) geometric organization"* — with generalisation arising in the second \[[1.2](#ref-1-2)\].

## Elaboration

**Where the observation came from.** It is older than the account: the original paper on grokking noted that *"such operations tend to require less data for generalization than closely related non-symmetrical counterparts"*, and immediately qualified that the effect may depend in part on the architecture — a transformer can easily learn a symmetric function by neglecting the positional embedding \[[1.3](#ref-1-3)\]. Four years later a claim about a cause grew out of that aside about the [data fraction](data-fraction-critical-dataset-size.md).

**What turns symmetry into a measurable quantity.** Symmetry violation is computed as the divergence of the predictions on symmetry-related pairs of inputs, and it is found to have a threshold: *"once a run's symmetry violation drops below a characteristic level, it reliably reaches perfect test accuracy, while runs that remain above this level do not"* \[[1.4](#ref-1-4)\]. The notion thereby enters the circle of [progress measures](progress-measures.md) and falls under their requirements: to lead the transition and to hold across seeds. The authors' qualification is kept verbatim — the transition is *"not perfectly sharp"*.

**Why this is a claim about a cause rather than about accompaniment.** The distinction is drawn by intervention: a penalty for symmetry violation is added to the loss, and the time to generalisation shortens — *"directly minimizing symmetry violations systematically shifts the grokking transition"* \[[1.5](#ref-1-5)\]. The same move has been checked independently by augmenting the data with commutative pairs \[[3.1](#ref-3-1)\], which places the line within [accelerated grokking](accelerated-grokking.md). The intervention works without [weight decay](weight-decay.md) as well, which tells against an account that assigns all the work to norm smoothing.

**Where symmetry hinders rather than helps.** The notion has a reverse side that matters more in this card than the claim itself: the same symmetries make the task *"fundamentally hard for permutation-equivariant kernel methods"* \[[2.2](#ref-2-2)\]. A network in the [kernel regime](neural-tangent-kernel-ntk.md) inherits the symmetry of the task and therefore cannot generalise, although it does reach zero training error; leaving that regime is the condition for generalisation. Symmetry, then, is not a force pulling towards the solution but a constraint that in one regime cannot be broken and in another must be assimilated.

**Not to be confused with the symmetry of the network.** The notion concerns the symmetry of the *rule*, not the permutation symmetries of the parameters that generate degenerate manifolds in the landscape (that is the neighbouring line — [singular learning theory](singular-learning-theory.md)). The shared word hides opposite roles: the symmetry of the task is what the model has to assimilate, the symmetry of the parameters is what makes the solution non-unique.

## Alternative definitions and nuances

### A. Symmetry as the cause of generalisation

The strong form: assimilating the invariance is a necessary condition of algorithmic generalisation, and it is also what appoints the geometry of the representations \[[1.1](#ref-1-1)\], \[[1.2](#ref-1-2)\]. The distinguishing feature is a testable consequence: if symmetry is the cause, then encouraging it must shift the time to generalisation, and that is measured \[[1.5](#ref-1-5)\]. The form's vulnerability is that all the tests are set on tasks where the symmetry is known in advance and can be written as a formula.

### B. Symmetry as a property that makes the task easier

The weak form, descending from the original observation: symmetric operations require less data \[[1.3](#ref-1-3)\]. The source of the difference is the subject of the claim: not a mechanism but a [threshold in the data fraction](data-fraction-critical-dataset-size.md). The form is more modest and therefore more robust: it survives the objection about architectural dependence, which the authors themselves raised.

### C. Symmetry as an obstacle in the kernel regime

The reverse form: the invariance of the task forbids generalisation to a whole class of methods \[[2.2](#ref-2-2)\]. The distinguishing feature is a proof rather than a measurement: a lower bound on the population loss for permutation-equivariant predictors. It is in this form that the notion meets the [lazy→rich transition](lazy-to-rich-kernel-to-feature-learning.md): generalisation requires leaving the regime that inherits the symmetry of the task.

### D. Symmetry beyond commutativity

An extension: the symmetry of a task is not exhausted by permuting the operands. [Composition in the non-commutative group](group-composition-non-commutative-s5.md) $S_5$ groks as well, although <i>"$S_{5}$ is not abelian, so the composition is non-commutative"</i> \[[2.3](#ref-2-3)\], while a sweep over tensor algebras by three independent properties — associativity, commutativity, unitality — shows that what should be compared is the property rather than one special case of it \[[3.3](#ref-3-3)\]. The same gap is visible from the side of the architecture: an intervention that removes the delay on a commutative operation fails entirely on the non-commutative $S_5$, because *"commutative operations require only a bag-of-tokens representation"* \[[3.2](#ref-3-2)\] and non-commutative ones do not. The distinguishing feature is that here symmetry stops being a single quantity and becomes a lattice of properties, and the question "which symmetry drives generalisation" has to be asked afresh for each of them.

## References

###### ref-1-1
**\[1.1\]** 2603.01968 — Hwang & Park, "Intrinsic Task Symmetry Drives Generalization in Algorithmic Tasks". [`"intrinsic task symmetry is the key driver of generalization"`](../papers/2603.01968.intrinsic-task-symmetry-drives-generalization-in-algorithmic-tasks/original/2603.01968.intrinsic-task-symmetry-drives-generalization-in-algorithmic-tasks.md#p1-5).

###### ref-1-2
**\[1.2\]** 2603.01968 — Hwang & Park, "Intrinsic Task Symmetry Drives Generalization in Algorithmic Tasks". [`"(i) memorization, (ii) symmetry acquisition, and (iii) geometric organization"`](../papers/2603.01968.intrinsic-task-symmetry-drives-generalization-in-algorithmic-tasks/original/2603.01968.intrinsic-task-symmetry-drives-generalization-in-algorithmic-tasks.md#p1-2).

###### ref-1-3
**\[1.3\]** 2201.02177 — Power et al., "Grokking: Generalization Beyond Overfitting on Small Algorithmic Datasets". [`"Such operations tend to require less data for generalization than closely related non-symmetrical counterparts"`](../papers/2201.02177.grokking-generalization-beyond-overfitting-on-small-algorithmic-datasets/2201.02177.grokking-generalization-beyond-overfitting-on-small-algorithmic-datasets.card.md#p3-4).

###### ref-1-4
**\[1.4\]** 2603.01968 — Hwang & Park, "Intrinsic Task Symmetry Drives Generalization in Algorithmic Tasks". [`"once a run’s symmetry violation drops below a characteristic level, it reliably reaches perfect test accuracy, while runs that remain above this level do not"`](../papers/2603.01968.intrinsic-task-symmetry-drives-generalization-in-algorithmic-tasks/original/2603.01968.intrinsic-task-symmetry-drives-generalization-in-algorithmic-tasks.md#p5-8).

###### ref-1-5
**\[1.5\]** 2603.01968 — Hwang & Park, "Intrinsic Task Symmetry Drives Generalization in Algorithmic Tasks". [`"directly minimizing symmetry violations systematically shifts the grokking transition"`](../papers/2603.01968.intrinsic-task-symmetry-drives-generalization-in-algorithmic-tasks/original/2603.01968.intrinsic-task-symmetry-drives-generalization-in-algorithmic-tasks.md#p8-5).

## References of works that joined the discussion

### Contested

###### ref-2-1
**\[2.1\]** 2311.06597 — Tan et al., "Understanding Grokking Through A Robustness Viewpoint". Contests: if generalisation went through assimilating the symmetry, commutativity ought to be learned before the transition — and it is not. [`"standard training on Modulo Addition Dataset fails to learn commutative law before grokking, which contradicts intuition"`](../papers/2311.06597.understanding-grokking-through-a-robustness-viewpoint/2311.06597.understanding-grokking-through-a-robustness-viewpoint.card.md#p2-4).

###### ref-2-2
**\[2.2\]** 2407.12332 — Mohamadi et al., "Why Do You Grok? A Theoretical Analysis of Grokking Modular Addition". Nuance: in the kernel regime the same symmetry works the other way round — it forbids generalisation, and the proof runs by a lower bound rather than by measurement. [`"this task is *fundamentally hard* for permutation-equivariant kernel methods, due to inherent symmetries"`](../papers/2407.12332.why-do-you-grok-a-theoretical-analysis-of-grokking-modular-addition/original/2407.12332.why-do-you-grok-a-theoretical-analysis-of-grokking-modular-addition.md#p3-4).

###### ref-2-3
**\[2.3\]** 2302.03025 — Chughtai et al., "A Toy Model of Universality: Reverse Engineering how Networks Learn Group Operations". Limits: grokking sets in where there is no symmetry of operand order at all. [`"$S_{5}$ is not abelian, so the composition is non-commutative"`](../papers/2302.03025.a-toy-model-of-universality-reverse-engineering-how-networks-learn-group-operations/2302.03025.a-toy-model-of-universality-reverse-engineering-how-networks-learn-group-operations.card.md#p4-5).

### In support

###### ref-3-1
**\[3.1\]** 2405.16658 — Park et al., "Acceleration of Grokking in Learning Arithmetic Operations via Kolmogorov-Arnold Representation". Nuance: an independent test of causality — not by a penalty for violation but by augmenting the training data with commutative pairs. [`"It is empirically verified that the commutative augmentation technique introduced accelerates grokking."`](../papers/2405.16658.acceleration-of-grokking-in-learning-arithmetic-operations-via-kolmogorov-arnold-representation/2405.16658.acceleration-of-grokking-in-learning-arithmetic-operations-via-kolmogorov-arnold-representation.card.md#p3-2).

###### ref-3-2
**\[3.2\]** 2603.05228 — Yildirim, "The Geometric Inductive Bias of Grokking: Bypassing Phase Transitions via Architectural Topology". Nuance: the symmetry of the task is paired with the architecture — a commutative operation needs only a "bag of tokens", and an intervention that rescues it fails on a non-commutative one. [`"commutative operations require only a bag-of-tokens representation"`](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p1-2).

###### ref-3-3
**\[3.3\]** 2602.19533 — Notsawo et al., "Grokking Finite-Dimensional Algebra". Nuance: symmetry is decomposed into independent properties and swept — associativity, commutativity and unitality give eight classes of algebras. [`"Let $a$=$associative$, $c$=$commutative$, $u$=$unital$."`](../papers/2602.19533.grokking-finite-dimensional-algebra/original/2602.19533.grokking-finite-dimensional-algebra.md#p8-1).

## Passing mentions

Works that only mention the notion — a literature review, a related-work paragraph, a passing citation — without examining it.

**\[4.1\]** 2506.05718 — Notsawo et al., "Grokking Beyond the Euclidean Norm of Model Parameters". [`"Park et al. (2024) accelerate grokking by using data augmentation for commutative operations"`](../papers/2506.05718.grokking-beyond-the-euclidean-norm-of-model-parameters/original/2506.05718.grokking-beyond-the-euclidean-norm-of-model-parameters.md#p17-4).
