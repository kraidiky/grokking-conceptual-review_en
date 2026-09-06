# The universality hypothesis

[Orthogonal gradient (⊥Grad)](orthogonal-gradient-perp-grad.md) ← previous card, next → [approximate-chinese-remainder-theorem](approximate-chinese-remainder-theorem.md)

[Concept card index](index.md), category: [2. Mechanisms and representations](index.md#cat-2)\
→ Next category: [Modular arithmetic](modular-arithmetic.md)\
← Previous category: [Grokking](grokking.md)

## Definition

**The universality hypothesis** is the supposition that networks trained on similar tasks arrive at a similar arrangement: *"the universality hypothesis (Olah et al. 2020; Li et al. 2016) asserts that models learn similar features and circuits across different models when trained on similar tasks"* \[[1.1](#ref-1-1)\]. For the [grokking](grokking.md) corpus it is not a side question but a condition for the whole enterprise to make sense: if the solutions are arbitrary, then an analysis of one grokked network says nothing about the next, and [mechanistic interpretability](mechanistic-interpretability.md) loses its subject matter.

In the corpus the word also carries a second, unrelated sense — the **universality class** of statistical physics: a set of critical exponents shared by different systems with the same transition. In that sense [double descent](double-descent.md) falls *"in a different universality class from the grokking transition studied here"* \[[1.4](#ref-1-4)\].

## Elaboration

**How the hypothesis is tested.** Not by argument but on a test bed: one takes a family of related tasks where the correct solution is known mathematically, and looks at whether the networks converge to a single algorithm. [Composition of elements of finite groups](group-composition-non-commutative-s5.md) was chosen for exactly this reason — it *"defines a large family of related tasks, forming an algorithmic test bed for investigating universality"* \[[1.2](#ref-1-2)\]. [Modular arithmetic](modular-arithmetic.md) turns out to be a special case rather than a story of its own.

**How the hypothesis was refuted in its strong form.** By two blows from different directions. The first: on a fixed training set *"small changes to model hyperparameters and initializations can induce discovery of qualitatively different algorithms"*, and within a single network the algorithms coexist in parallel \[[2.1](#ref-2-1)\] — hence [the Clock and the Pizza](clock-vs-pizza.md). The second: the claimed unification of mechanisms through representation theory did not hold, because networks on $S_5$ and $S_6$ *"discover the true subgroup structure of the full group and converge on neural circuits that decompose the group arithmetic using the permutation group's subgroups"* — [coset circuits](group-representations-cosets.md) rather than a composition of representations \[[2.2](#ref-2-2)\].

**How the hypothesis was restated so as to survive the refutation.** The key is the level of description. The claim is moved from neurons to an abstract algorithm: *"seemingly disparate neural network solutions observed in the simple task of modular addition are unified under a common abstract algorithm"* \[[1.3](#ref-1-3)\], declared to be the [approximate Chinese Remainder Theorem](approximate-chinese-remainder-theorem.md). In that setting the coset circuits on permutations are not a refutation but a special case: *"as our approximate cosets generalize cosets"*, what was found on permutations *"aligns with our results"* \[[3.1](#ref-3-1)\]. The price of the restatement is a loss of testability: the more abstractly the algorithm is described, the harder it is to name an observation that would refute it.

**What practice is left with.** A distinction of levels: universality at the level of neurons is refuted, at the level of [Fourier features](fourier-features-circuits.md) it holds with qualifications, at the level of an abstract algorithm it is claimed and under discussion. In examining a new grokked network it is worth naming at once the level at which agreement is expected — otherwise a dispute about "the same algorithm" cannot be settled. The requirement on [seed variance](seed-variance-reproducibility.md) belongs here too: agreement of solutions between runs is exactly a measurement of universality in its narrowest form.

## Alternative definitions and nuances

### A. Universality of features and circuits

The original form, from mechanistic interpretability \[[1.1](#ref-1-1)\]. The distinguishing feature is that it is checked by matching parts: are the same neurons and subcircuits found in two networks. In the grokking corpus this form has been refuted by direct experiment \[[2.1](#ref-2-1)\], and it is that refutation that made the question a live one.

### B. Universality of the abstract algorithm

The weakened form: what must agree is not the parts but the computed function and its decomposition \[[1.3](#ref-1-3)\]. The source of the difference is the level of description; the consequence is that the work shifts to proving that all the schemes observed are implementations of a single abstract algorithm \[[3.1](#ref-3-1)\], while the dispute moves to whether the description has become so general that it covers what one wanted to tell apart; the history of that shift is set out by the paper itself \[[3.2](#ref-3-2)\].

### C. Universality class

A homonym from statistical physics: two systems belong to one class if the critical exponents of their transitions agree \[[1.4](#ref-1-4)\]. The distinguishing feature is that what is compared is not the arrangement of the network but the form of the divergence near the transition; and the demands on the claim are different — finite-size checks are needed, not an analysis of weights. A claim of a class for grokking is stated outright in the corpus to be unestablished: *"what is not established is the final transition order or a stable universality class"* \[[1.5](#ref-1-5)\]. The two senses must not be mixed: an agreement of exponents says nothing about a sameness of algorithms, and a sameness of algorithms says nothing about exponents.

## References

###### ref-1-1
**\[1.1\]** 2302.03025 — Chughtai et al., "A Toy Model of Universality: Reverse Engineering how Networks Learn Group Operations". [`"The *universality hypothesis* (Olah et al. 2020; Li et al. 2016) asserts that models learn similar features and circuits across different models when trained on similar tasks."`](../papers/2302.03025.a-toy-model-of-universality-reverse-engineering-how-networks-learn-group-operations/2302.03025.a-toy-model-of-universality-reverse-engineering-how-networks-learn-group-operations.card.md#p1-3).

###### ref-1-2
**\[1.2\]** 2302.03025 — Chughtai et al., "A Toy Model of Universality: Reverse Engineering how Networks Learn Group Operations". [`"as this defines a large family of related tasks, forming an algorithmic test bed for investigating universality"`](../papers/2302.03025.a-toy-model-of-universality-reverse-engineering-how-networks-learn-group-operations/2302.03025.a-toy-model-of-universality-reverse-engineering-how-networks-learn-group-operations.card.md#p1-4).

###### ref-1-3
**\[1.3\]** 2505.18266 — McCracken et al., "Uncovering a Universal Abstract Algorithm for Modular Addition in Neural Networks". [`"seemingly disparate neural network solutions observed in the simple task of modular addition are unified under a common abstract algorithm"`](../papers/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks/original/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks.md#p1-2).

###### ref-1-4
**\[1.4\]** 2606.13753 — Truong et al., "The Weight Norm Sets the Grokking Timescale: A Causal Delay Law". [`"placing it in a different universality class from the grokking transition studied here"`](../papers/2606.13753.the-weight-norm-sets-the-grokking-timescale-a-causal-delay-law/2606.13753.the-weight-norm-sets-the-grokking-timescale-a-causal-delay-law.card.md#p4-3).

###### ref-1-5
**\[1.5\]** 2603.24746 — Bi et al., "Grokking as a Falsifiable Finite-Size Transition". [`"What is not established is the final transition order or a stable universality class."`](../papers/2603.24746.grokking-as-a-falsifiable-finite-size-transition/2603.24746.grokking-as-a-falsifiable-finite-size-transition.card.md#p6-5).

## References of works that joined the discussion

### Contested

###### ref-2-1
**\[2.1\]** 2306.17844 — Zhong et al., "The Clock and the Pizza: Two Stories in Mechanistic Explanation of Neural Networks". Contests: universality at the level of the algorithm is refuted on a fixed training set — the difference is made by the settings alone. [`"Small changes to model hyperparameters and initializations can induce discovery of qualitatively different algorithms from a fixed training set"`](../papers/2306.17844.the-clock-and-the-pizza-two-stories-in-mechanistic-explanation-of-neural-networks/original/2306.17844.the-clock-and-the-pizza-two-stories-in-mechanistic-explanation-of-neural-networks.md#p1-2).

###### ref-2-2
**\[2.2\]** 2312.06581 — Stander et al., "Grokking Group Multiplication with Cosets". Contests: on permutations the networks learn not a composition of representations but a decomposition by subgroups, which removes the claim of a unification of mechanisms. [`"The models discover the true subgroup structure of the full group and converge on neural circuits that decompose the group arithmetic using the permutation group’s subgroups."`](../papers/2312.06581.grokking-group-multiplication-with-cosets/original/2312.06581.grokking-group-multiplication-with-cosets.md#p1-2).

### In support

###### ref-3-1
**\[3.1\]** 2505.18266 — McCracken et al., "Uncovering a Universal Abstract Algorithm for Modular Addition in Neural Networks". Nuance: the refutation is turned into a special case — approximate cosets subsume ordinary ones, and different groups fall under a single description. [`"As our approximate cosets generalize cosets, work finding coset circuits in networks trained on permuting lists (permutation groups) [9] aligns with our results."`](../papers/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks/original/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks.md#p2-1).

###### ref-3-2
**\[3.2\]** 2505.18266 — McCracken et al., "Uncovering a Universal Abstract Algorithm for Modular Addition in Neural Networks". Nuance: the history of the dispute is set out by the work itself — and from it the requirement to state the hypothesis at the level of an abstract algorithm is derived. [`"later work by Stander et al. [9] reverse-engineered models trained on $S_{n}$ under identical conditions and found that networks instead learn *coset*-based circuits, refuting the GCR universality claim"`](../papers/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks/original/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks.md#p2-4).
