# Architectural inductive bias

[Overparameterisation and depth](overparameterization-depth.md) ← previous card, next → —

[Concept card index](index.md), category: [4. Training and optimisation factors](index.md#cat-4)\
→ Next category: [Grokfast / gradient low-pass filtering](gradient-low-pass-filtering.md)\
← Previous category: [Modular arithmetic](modular-arithmetic.md)

## Definition

**Architectural inductive bias** is a preference over solutions built into the arrangement of the network itself, prior to any training: by the topology of the residual stream, by the presence of normalisation, by the way tokens are mixed. In the [grokking](grokking.md) corpus the notion is put forward as a controllable factor rather than as background: *"inductive biases expressed through architecture modulate grokking"*, and this is checked with an architectural probe — the placement of layer normalisation, which yields sharply different grokking speeds while converging to identically arranged solutions \[[1.3](#ref-1-3)\].

The line's main result is conditional: bypassing the delay by architecture is possible, *"but strictly depends on alignment between architectural priors and task symmetry"* \[[1.1](#ref-1-1)\].

## Elaboration

**How the experiment is set up.** Not by a post-hoc analysis of a trained network, but by changing the topology *before* training, with two independent interventions: bounding the magnitude of the residual stream ($L_2$ normalisation, a [spherical constraint](spherical-weight-norm-constraint.md)) and replacing learned attention with uniform summation. Each of them on its own removes the [memorisation phase](memorization-phase.md) on modular addition and multiplication: training and test accuracy rise together from initialisation onward \[[1.1](#ref-1-1)\].

**The negative control is the most valuable thing here.** The same spherical constraint *"fails entirely"* on the [non-commutative composition of permutations](group-composition-non-commutative-s5.md) $S_5$: the models generalise on no seed at all, although they do reach perfect training accuracy \[[1.2](#ref-1-2)\]. The explanation leans on someone else's analysis: the generalising solutions on $S_5$ rest on discrete [cosets](group-representations-cosets.md) rather than on the continuous [Fourier features](fourier-features-circuits.md) that the spherical geometry agrees with. Hence the conclusion: the matter is not the capacity constraint as such, but its alignment with the [intrinsic symmetry of the task](intrinsic-task-symmetry.md).

**Why this makes the notion an instrument rather than a caveat.** The connection runs both ways: *"testing architectural constraints and observing which accelerate or impede generalization can reveal properties of the task's intrinsic structure"* \[[3.1](#ref-3-1)\]. A constraint's failure becomes a measurement: it says that the generalising representation does not lie on a continuous circular manifold. The order "interpret the circuits, then arrange the architecture" turns [mechanistic interpretability](mechanistic-interpretability.md) into a design technique.

**Where the bias remains an unexplained residue.** In works that explain grokking by a single quantity, architecture surfaces as what keeps the explanation from closing: the collapse of spectral entropy is observed without grokking too, so it is *"necessary but not sufficient"*, and *"architectural inductive bias plays a role"* \[[3.2](#ref-3-2)\]. Such a usage is an honest admission of a limit, but also a reminder that "architectural bias" in this role is not measured, only named.

**What the notion does not explain.** It speaks of timing and of whether generalisation will come at all, but it is under no obligation to change the learned algorithm itself. This distinction is essential and separates the line from the [universality hypothesis](universality-hypothesis.md): architecture moves the path, not necessarily the destination.

## Alternative definitions and nuances

### A. Bias as topology

The strong form: the degrees of freedom of the architecture prolong memorisation, and constraining them removes the delay \[[1.1](#ref-1-1)\], \[[1.2](#ref-1-2)\]. The distinguishing feature is that the intervention is placed before training and therefore gives causal rather than accompanying evidence; the control quantity here is discrete (the topology is there or it is not), unlike continuous factors such as [weight decay](weight-decay.md).

### B. Bias as the placement of normalisation

The mild form: the same layers in a different order — and the time to generalisation changes by orders of magnitude, although the solution obtained is the same \[[1.3](#ref-1-3)\]. The source of the difference is what is measured: speed, not attainability. Hence its role in the explanation: architecture sets how far one must walk, not where one arrives.

### C. Bias as an unexplained residue

The auxiliary form: the notion is named where a single measure fails to match experiment \[[3.2](#ref-3-2)\]. The distinguishing feature is that here it is not measured and works as a name for a discrepancy; the value of such an entry lies in honestly marking out the range of the explanation, not in explaining anything.

### D. An objection: architecture does not change the algorithm learned

Against the strong form speaks an observation from another level of description: *"multilayer perceptrons and transformers universally implement the abstract algorithm"* — the [approximate Chinese Remainder Theorem](approximate-chinese-remainder-theorem.md) \[[2.1](#ref-2-1)\]. If that is right, architectural bias governs timing and attainability but not the content of the solution, and then the strong form A has to be restated as a claim about the path rather than about the algorithm.

## References

###### ref-1-1
**\[1.1\]** 2603.05228 — Yildirim, "The Geometric Inductive Bias of Grokking: Bypassing Phase Transitions via Architectural Topology". [`"bypassing the generalization delay is possible—but strictly depends on alignment between architectural priors and task symmetry"`](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p1-2).

###### ref-1-2
**\[1.2\]** 2603.05228 — Yildirim, "The Geometric Inductive Bias of Grokking: Bypassing Phase Transitions via Architectural Topology". [`"the same spherical constraint fails entirely: models cannot generalize on any seed within the training window, despite reaching perfect training accuracy"`](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p2-5).

###### ref-1-3
**\[1.3\]** 2602.06702 — Singh et al., "Explaining Grokking in Transformers through the Lens of Inductive Bias". [`"*Inductive biases expressed through architecture modulate grokking.*"`](../papers/2602.06702.explaining-grokking-in-transformers-through-the-lens-of-inductive-bias/2602.06702.explaining-grokking-in-transformers-through-the-lens-of-inductive-bias.card.md#p2-1).

## References of works that joined the discussion

### Contested

###### ref-2-1
**\[2.1\]** 2505.18266 — McCracken et al., "Uncovering a Universal Abstract Algorithm for Modular Addition in Neural Networks". Contests: if different architectures implement one and the same abstract algorithm, then architectural bias governs the timing rather than the content of the solution. [`"multilayer perceptrons and transformers universally implement the abstract algorithm"`](../papers/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks/original/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks.md#p1-2).

### In support

###### ref-3-1
**\[3.1\]** 2603.05228 — Yildirim, "The Geometric Inductive Bias of Grokking: Bypassing Phase Transitions via Architectural Topology". Nuance: the connection is reversed — from which constraint helps and which hinders, the structure of the task itself can be read off. [`"testing architectural constraints and observing which accelerate or impede generalization can reveal properties of the task’s intrinsic structure"`](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p16-2).

###### ref-3-2
**\[3.2\]** 2604.13123 — Truong et al., "Spectral Entropy Collapse as a Phase Transition in Delayed Generalisation". Nuance: the notion is named as a residue not covered by a single measure — entropy collapse happens without grokking too. [`"Entropy collapse is therefore **necessary but not sufficient** for generalisation in our setting; architectural inductive bias plays a role."`](../papers/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation.card.md#p5-1).
