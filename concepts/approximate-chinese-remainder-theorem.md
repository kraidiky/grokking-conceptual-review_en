# Approximate Chinese Remainder Theorem (aCRT)

[The universality hypothesis](universality-hypothesis.md) ← previous card, next → [generalization-circuit](generalization-circuit.md)

[Concept card index](index.md), category: [2. Mechanisms and representations](index.md#cat-2)\
→ Next category: [Modular arithmetic](modular-arithmetic.md)\
← Previous category: [Grokking](grokking.md)

## Definition

**The approximate Chinese Remainder Theorem** is a proposed abstract description of what a network computes once it has grokked [modular arithmetic](modular-arithmetic.md): the task splits into several independent subsystems by residues, each is solved separately, and the answers are intersected. The claim is strong because it is not about one architecture: *"multilayer perceptrons and transformers universally implement the abstract algorithm we call the approximate Chinese Remainder Theorem"* \[[1.1](#ref-1-1)\]. The classical CRT rests on cosets; here they have to be weakened, because networks learn frequencies that do not divide the modulus: *"we now introduce approximate cosets (approximate equivalence classes) using the minimum path distance between vertices in $\Gamma$"*, where $\Gamma$ is the Cayley graph \[[1.2](#ref-1-2)\]. The outcome of this weakening is stated by the paper outright: approximate cosets are thereby more general than cosets.

## Elaboration

**What is measurable here.** A claim about neurons: *"simple neurons in layer 1 activate (ReLU $>0$) on an approximate coset containing the correct answer $c$… all neurons in later hidden layers activate on linear combinations of approximate cosets"* \[[1.3](#ref-1-3)\]. This is directly testable: take a trained network and, for each neuron, compute the set of inputs on which it stays silent. The abstract algorithm thereby acquires an observable consequence — exactly what the [universality hypothesis](universality-hypothesis.md) in its general form was lacking.

**A numerical prediction.** From the analogy with the CRT a count follows: *"the CRT uses $\mathcal{O}(\log(n))$ modular subsystems, and Corollary 4.8 gives that DNNs need $\mathcal{O}(\log(n))$ unique frequencies"* \[[1.4](#ref-1-4)\]. This is what sets the frame apart from a restatement: it predicts how many [frequencies](fourier-features-circuits.md) must be learned, and the prediction is checked against experiment at different moduli.

**Relation to its predecessors.** The frame is built as a generalisation of two accounts previously taken to be rivals. The first is the [Fourier multiplication algorithm](fourier-features-circuits.md), where *"the attention and MLP layers then combine these using trigonometric identities"* \[[3.1](#ref-3-1)\]; the second is the [coset circuits](group-representations-cosets.md) found on permutation groups \[[3.2](#ref-3-2)\]. Approximate cosets subsume ordinary ones, so both accounts turn out to be implementations of a single algorithm. [Pizza](clock-vs-pizza.md) falls in here as well: its difference from the Clock is declared low-level rather than algorithmic \[[3.3](#ref-3-3)\].

**What the frame does not cover — by the authors' own admission.** The test is set at the two extremes of group structure, cyclic groups and permutation groups: *"a core limitation of our work is that we do not explore the groups between these two extremes"* \[[1.5](#ref-1-5)\]. The intermediate cases are exactly where the generalisation may break, and the qualification is kept verbatim, because without it the claim looks broader than what was checked.

**How to read the claim.** "Approximate" here is not a softening but an essential part: the strict CRT requires the frequencies to divide the modulus, whereas networks learn frequencies that do not. The whole content of the frame lies in what replaces exact divisibility — distance on the Cayley graph; and its vulnerability rests on the same thing, since a sufficiently broad notion of closeness will fit too much.

## Alternative definitions and nuances

### A. aCRT as a description of the computation

The main form: the network decomposes the task into subsystems by residues and intersects their answers \[[1.1](#ref-1-1)\], \[[1.4](#ref-1-4)\]. The distinguishing feature is the level of description: it speaks of the computed function and its decomposition, not of which neurons carry it; hence its compatibility with accounts that disagree at the level of neurons.

### B. Approximate cosets as a notion in their own right

The instrumental form: what matters is not the CRT but the weakening of a coset to a set that is close on the Cayley graph \[[1.2](#ref-1-2)\], \[[1.3](#ref-1-3)\]. The source of the difference is that this notion survives the abandonment of the analogy with the theorem: even if the decomposition by residues turns out to be a stretch, the claim "a neuron activates on a connected piece of the Cayley graph" is testable on its own.

### C. aCRT as a unifying frame

The historical form: the value lies not in a new mechanism but in the reduction of previously incompatible accounts to one \[[3.1](#ref-3-1)\], \[[3.2](#ref-3-2)\], \[[3.3](#ref-3-3)\]. The distinguishing feature is that it is checked not by experiment but by enumeration: each known description is shown to come out as a special case. The weakness is in exactly the same place: the unification is achieved by widening the definition, and whether a distinction has been lost in the process remains open.

## References

###### ref-1-1
**\[1.1\]** 2505.18266 — McCracken et al., "Uncovering a Universal Abstract Algorithm for Modular Addition in Neural Networks". [`"multilayer perceptrons and transformers universally implement the abstract algorithm we call the approximate Chinese Remainder Theorem"`](../papers/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks/original/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks.md#p1-2).

###### ref-1-2
**\[1.2\]** 2505.18266 — McCracken et al., "Uncovering a Universal Abstract Algorithm for Modular Addition in Neural Networks". [`"We now introduce **approximate cosets** (approximate equivalence classes) using the minimum path distance between vertices in $\Gamma$."`](../papers/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks/original/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks.md#p4-5).

###### ref-1-3
**\[1.3\]** 2505.18266 — McCracken et al., "Uncovering a Universal Abstract Algorithm for Modular Addition in Neural Networks". [`"*Simple neurons in layer 1 activate (ReLU $>0$) on an approximate coset containing the correct answer $c$, by concentrating their preactivations on approximate cosets that contain $a$ and $b$; all neurons in later hidden layers activate on linear combinations of approximate cosets.*"`](../papers/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks/original/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks.md#p4-7).

###### ref-1-4
**\[1.4\]** 2505.18266 — McCracken et al., "Uncovering a Universal Abstract Algorithm for Modular Addition in Neural Networks". [`"The CRT uses $\mathcal{O}(\log(n))$ modular subsystems, and Corollary 4.8 gives that DNNs need $\mathcal{O}(\log(n))$ unique frequencies"`](../papers/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks/original/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks.md#p9-1).

###### ref-1-5
**\[1.5\]** 2505.18266 — McCracken et al., "Uncovering a Universal Abstract Algorithm for Modular Addition in Neural Networks". [`"A core limitation of our work is that we do not explore the groups between these two extremes."`](../papers/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks/original/2505.18266.uncovering-a-universal-abstract-algorithm-for-modular-addition-in-neural-networks.md#p9-4).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2301.05217 — Nanda et al., "Progress measures for grokking via mechanistic interpretability". Nuance: the predecessor account that aCRT declares its own special case — angle addition through trigonometric identities. [`"The attention and MLP layers then combine these using trigonometric identities to compute the sine and cosine of $w_{k}(a+b)$"`](../papers/2301.05217.progress-measures-for-grokking-via-mechanistic-interpretability/2301.05217.progress-measures-for-grokking-via-mechanistic-interpretability.card.md#p2-1).

###### ref-3-2
**\[3.2\]** 2312.06581 — Stander et al., "Grokking Group Multiplication with Cosets". Nuance: the second special case is the coset circuits found on permutation groups; approximate cosets subsume ordinary ones. [`"The models discover the true subgroup structure of the full group and converge on neural circuits that decompose the group arithmetic using the permutation group’s subgroups."`](../papers/2312.06581.grokking-group-multiplication-with-cosets/original/2312.06581.grokking-group-multiplication-with-cosets.md#p1-2).

###### ref-3-3
**\[3.3\]** 2306.17844 — Zhong et al., "The Clock and the Pizza: Two Stories in Mechanistic Explanation of Neural Networks". Nuance: the very pair of rival schemes whose difference aCRT declares low-level. [`"Some networks trained to perform modular addition implement a familiar *Clock* algorithm (previously described by Nanda et al. [1]); others implement a previously undescribed, less intuitive, but comprehensible procedure we term the *Pizza* algorithm"`](../papers/2306.17844.the-clock-and-the-pizza-two-stories-in-mechanistic-explanation-of-neural-networks/original/2306.17844.the-clock-and-the-pizza-two-stories-in-mechanistic-explanation-of-neural-networks.md#p1-2).
