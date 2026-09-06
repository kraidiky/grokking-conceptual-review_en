# The Clock and the Pizza algorithms

[Neural collapse](neural-collapse.md) ← previous card, next → [intrinsic-task-symmetry](intrinsic-task-symmetry.md)

[Concept card index](index.md), category: [2. Mechanisms and representations](index.md#cat-2)\
→ Next category: [Modular arithmetic](modular-arithmetic.md)\
← Previous category: [Grokking](grokking.md)

## Definition

**The Clock and Pizza algorithms** are two qualitatively different internal circuits (subnetworks implementing a sub-algorithm of the task) that a network converges to when learning [modular addition](modular-arithmetic.md) `c = (a + b) mod n` (the remainder of the sum on division by the modulus; the inputs decompose naturally onto a circle of `n` points). The distinction was introduced by Zhong et al. (2306.17844, "The Clock and the Pizza") \[[1.2](#ref-1-2)\] and is stated as follows: **Clock** is a structured solution on continuous [Fourier features](fourier-features-circuits.md) (the inputs are encoded as roots of unity on a circle, and the network adds their **angles**), whereas **Pizza** is a fragmented, "piecewise-memorising" solution that computes the **mean of the vectors** of the input embeddings on the same circle \[[1.1](#ref-1-1)\]. Both circuits carry modular addition through to perfect generalisation, but realise it differently in geometric terms.

![The two internal mechanisms of modular addition — the "Clock" and the "Pizza" — that trained networks converge to (fig. 1 of Zhong et al.)](assets/clock-vs-pizza.png)

## Elaboration

The Clock/Pizza distinction grew out of the [mechanistic interpretability](mechanistic-interpretability.md) of [grokking](grokking.md) on modular arithmetic: after a long [memorisation phase](memorization-phase.md) the network passes to a generalising solution, and that solution turns out not to be unique. In the available corpus the strictest definition of both circuits is given by McCracken et al.: **Clock** and **Pizza** differ in the mechanism by which inputs are aggregated inside the transformer block — in Clock the attention (the mechanism weighting the inputs) is learned and adds the **angles** of the input vectors, while in Pizza the attention is rigidly uniform (attention rate `α = 0`) and the block reduces to averaging the vectors \[[2.1](#ref-2-1)\]. Zhong et al. showed that the two circuits can even coexist within a single network \[[2.1](#ref-2-1)\], which makes the distinction a consequence of the architecture's redundant degrees of freedom rather than a property of the task.

Two competing readings have formed around this distinction. The first (Yildirim) treats Clock/Pizza as a real, substantive opposition and ties **Pizza** to memorisation: the redundant degrees of freedom of a standard transformer (the freedom to encode information in the norm of a vector and in learned [attention routing](attention-routing-heads.md)) open up "piecewise-memorising" solution pathways, and it is these that drag generalisation out, whereas **Clock** is a pure structured solution on Fourier features \[[1.1](#ref-1-1)\]. On this account, removing the superfluous degrees of freedom (rigid normalisation of the residual stream, or uniform attention) removes the grokking [phase transition](phase-transition.md) — the network takes the "clock" route straight away \[[1.1](#ref-1-1)\]. The second reading (McCracken et al.) **contests the fundamentality** of the distinction: Clock and Pizza are not different algorithms but particular implementations of a single abstract one (the approximate Chinese Remainder Theorem — splitting `mod n` into independent computations over coprime divisors); after a renormalisation of frequencies ("remapping" — bringing neurons to a common frequency by a change of variable) their behaviour turns out to be qualitatively equivalent \[[2.1](#ref-2-1)\]. Clock/Pizza is thus at once the standard illustration that the learned solution is not unique, and the subject of a dispute over whether there are two algorithms here or one.

## Alternative definitions and nuances

### A. Clock: adding angles on continuous Fourier features

A definition through the mechanism: the network encodes the inputs `a` and `b` as points on the unit circle (Fourier features — the sine and cosine of `2πa/n`) and, after the attention block, computes the **angle of the sum** `a + b`, that is, it continuously "rotates" the representation. The key distinguishing mark is learned, data-dependent attention (`α = 1`) and reliance on continuous Fourier structure; it is this that Yildirim calls the "structured, continuous Fourier solution" and ties to fast, undelayed generalisation \[[1.1](#ref-1-1)\].

### B. Pizza: averaging vectors and piecewise memory

A definition through the alternative mechanism: instead of adding angles, a block with **uniform** attention (`α = 0`) computes the **mean** of the input vectors on the circle; geometrically the solution region is cut into "slices" (hence the name), and the solution itself rests on piecewise memorisation. The distinguishing source of the difference is not the task but the redundant degrees of freedom of the architecture (the norm of a vector and learned routing), which permit such a fragmented route; on Yildirim's account it is exactly the presence of Pizza routes ("memorization-heavy solution pathways") that defers generalisation \[[1.1](#ref-1-1)\].

### Contested. A single abstract algorithm: the distinction is not fundamental

The contesting reading (McCracken et al.): the Clock/Pizza opposition is an artefact of the level of description, not two different computations. The controlled parameter here is the frequency of a neuron: after it is normalised (remapping, the authors' Def. 4.2), the neurons of MLPs, of Pizza transformers and of Clock transformers behave alike, and both schemes are read as an approximate implementation of the Chinese Remainder Theorem. The testable consequence that sets this position apart: Clock and Pizza must show qualitative equivalence after remapping and must be able to coexist within a single network — which is what the authors demonstrate \[[2.1](#ref-2-1)\].

## References

###### ref-1-1
**\[1.1\]** 2603.05228 — Yildirim, "The Geometric Inductive Bias of Grokking:
Bypassing Phase Transitions via Architectural Topology". [`"(the “Pizza” algorithm) rather than the structured, continuous Fourier solution (the “Clock”"`](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p2-2).\
Also: [`"Zhong et al. (2023) identified two qualitatively distinct solutions: a structured “Clock” algorithm using continuous Fourier features and a fragmented “Pizza” algorithm relying on piecewise memorization"`](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p3-3);
[`"memorization-heavy solution pathways that delay the emergence of invariant representations"`](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p2-2) —
.


###### ref-1-2
**\[1.2\]** 2306.17844 — Zhong et al. 2023, "The Clock and the Pizza: Two Stories in Mechanistic Explanation of Neural Networks". The primary source of the distinction: it introduces both names and both schemes. Nuance: both schemes are circular and Fourier-based, and differ in the nonlinearity they require rather than in "structure versus memorisation". [`"the *Pizza* algorithm operates *inside* the circle formed by embeddings (just as pepperoni are spread all over a pizza), instead of operating on the circumference of the circle"`](../papers/2306.17844.the-clock-and-the-pizza-two-stories-in-mechanistic-explanation-of-neural-networks/original/2306.17844.the-clock-and-the-pizza-two-stories-in-mechanistic-explanation-of-neural-networks.md#p4-2).\
Also: [`"*Clock* requires multiplication of inputs in Step 2, while *Pizza* requires only absolute value computation, which is easily implemented by the ReLU layers"`](../papers/2306.17844.the-clock-and-the-pizza-two-stories-in-mechanistic-explanation-of-neural-networks/original/2306.17844.the-clock-and-the-pizza-two-stories-in-mechanistic-explanation-of-neural-networks.md#p4-3); [`"both clock and pizza give perfect accuracy, but arrive at answers via different interal computations"`](../papers/2306.17844.the-clock-and-the-pizza-two-stories-in-mechanistic-explanation-of-neural-networks/original/2306.17844.the-clock-and-the-pizza-two-stories-in-mechanistic-explanation-of-neural-networks.md#p9-4).
## References of works that joined the discussion

### Contested

###### ref-2-1
**\[2.1\]** 2505.18266 — McCracken et al. 2025, "Uncovering a Universal Abstract Algorithm for Modular Addition in Neural Networks". Contests the soundness of the distinction: the clock and the pizza are implementations of a single abstract algorithm (the approximate CRT), not two different ones. [`"unified under a common abstract algorithm. While prior work interpreted variations in neuron-level representations as evidence for distinct algorithms"`](../papers/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks/original/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks.md#p1-2).\
Also: [`"pizza and clock show qualitative equivalence after remapping"`](../papers/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks/original/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks.md#fig-1); [`"They introduced the *Pizza* circuit, which contrasted with [4]’s clock."`](../papers/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks/original/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks.md#p2-4); [`"both clock and pizza circuits could coexist within the same network simultaneously"`](../papers/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks/original/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks.md#p2-4).

## Passing mentions

Works that only mention the distinction — a literature review, a related-work paragraph, a passing citation — without examining it.

**\[4.1\]** 2510.04930 — Saheb Pasand et al., "Egalitarian Gradient Descent: A
Simple Approach to Accelerated Grokking". [`"Notably, Zhong et al. (2023) identify complementary algorithmic mechanisms (“clock” and “pizza”) and circular embeddings that emerge at the grokking transition"`](../papers/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking/original/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking.md#p3-2).

**\[4.2\]** 2602.16746 — Xu, "Low-Dimensional and Transversely Curved
Optimization Dynamics in Grokking". [`"Zhong et al. (2024) described clock and pizza representations in modular addition"`](../papers/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking/original/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking.md#p20-4).

**\[4.3\]** 2603.15492 — Acharya et al., "Grokking as a Variance-Limited Phase
Transition". [`"These studies map the topology of the solution (e.g., the “Clock Circuit”) but lack a kinetic mechanism to explain the timescale of the transition"`](../papers/2603.15492.grokking-as-a-variance-limited-phase-transition-spectral-gating-and-the-epsilon-stability-threshold/original/2603.15492.grokking-as-a-variance-limited-phase-transition-spectral-gating-and-the-epsilon-stability-threshold.md#p1-7).

**\[4.4\]** 2604.06256 — Xu, "Spectral Edge Dynamics Reveal Functional Modes of Learning". Nuance: a mention without examination; the year is shifted. [`"Zhong et al. 2024 described clock and pizza representations in this setting."`](../papers/2604.06256.spectral-edge-dynamics-reveal-functional-modes-of-learning/original/2604.06256.spectral-edge-dynamics-reveal-functional-modes-of-learning.md#p14-7).

**\[4.5\]** 2602.06702 — Singh, Misra, Orvieto, "Explaining Grokking in Transformers…". Zhong et al. are brought in as an argument that the solution is not unique: (54) [`"find that this solution is not unique, and show that transformers can learn the “pizza” algorithm"`](../papers/2602.06702.explaining-grokking-in-transformers-through-the-lens-of-inductive-bias/2602.06702.explaining-grokking-in-transformers-through-the-lens-of-inductive-bias.card.md#p12-3). In the neighbouring sentence of the same paragraph, Zhong et al.'s result on phase transitions is attributed to another work — examined in the "Common misreadings and overstatements" section of that card, anchor `mc-2306-17844`.

**\[4.6\]** 2606.12966 — Sivasankar, "Circuit Synchronization Precedes Generalization: A Causal Precursor to Grokking". [`"small hyperparameter changes induce qualitatively different procedures (a “clock” and a “pizza” algorithm), both Fourier-based"`](../papers/2606.12966.circuit-synchronization-precedes-generalization-a-causal-precursor-to-grokking/2606.12966.circuit-synchronization-precedes-generalization-a-causal-precursor-to-grokking.card.md#p16-3).
