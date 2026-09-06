# Polysemanticity and superposition

[execution-manifold](execution-manifold.md) ← previous card, next → —

[Concept card index](index.md), category: [2. Mechanisms and representations](index.md#cat-2)\
→ Next category: [Modular arithmetic](modular-arithmetic.md)\
← Previous category: [Grokking](grokking.md)

## Definition

**Polysemanticity** is the property of a neuron responding to several unrelated features at once; **superposition** is the explanation for it: the network places more features than it has directions, laying them over one another in a single subspace. The opposite pole is a **monosemantic** neuron, excited by exactly one feature \[[1.2](#ref-1-2)\]. This matters for the corpus because every instrument used to take grokked networks apart — [probing](linear-sparse-probing.md), ablations, the reading of [Fourier circuits](fourier-features-circuits.md) — silently assumes that the direction found answers to a single notion.

Admitting superposition changes the setting: some model components *"represent features in superposition"*, and a reading neuron by neuron in the standard basis therefore gives only an approximation \[[1.1](#ref-1-1)\].

## Elaboration

**Why this bears on grokking.** Mechanistic analyses are built like this: find the directions, show that they carry the algorithm, verify by ablation. If the directions are polysemantic, every step weakens — an ablation touches not one function but several, and the conclusion "this part computes addition" stops being exact. In the corpus this shows up as a gap between "the circuit has been found" and "the circuit is sufficient": the strong works test sufficiency by filtering the representation, not merely by the presence of a direction.

**The tie to scale.** The observation a whole line is built around: monosemantic neurons *"gradually diminish as the model scale increases"* \[[1.2](#ref-1-2)\]. Hence an unexpected move — not to fight polysemanticity but to use it as a lever: inhibiting monosemanticity is offered as a technique that hastens the appearance of abilities \[[3.1](#ref-3-1)\]. What matters for the card is that here polysemanticity turns from an obstacle to interpretability into a controllable quantity.

**What modular arithmetic gives.** In tasks where the algorithm is known, polysemanticity is directly testable: one can ask whether the same direction carries features of several operations. Work on transfer between operations shows that grokked models acquire common features transferable between similar tasks \[[3.2](#ref-3-2)\] — that is, directions are shared between operations, which is polysemanticity in its mild form.

**A caveat.** In the corpus superposition is almost always invoked as an explanation rather than measured: there are no works that would count the number of features per direction in a grokked network. Claims of the form "the features lie in superposition" should therefore be read as a frame inherited from the interpretability of large models, not as a result obtained on grokking.

## Alternative definitions and nuances

### A. Polysemanticity as a property of a neuron

The observational form: a neuron responds to several unrelated features \[[1.2](#ref-1-2)\]. The distinguishing feature is that the definition is operational (statistics of responses) and needs no hypothesis about why it came out that way. The price is that it is tied to the basis of neurons and therefore does not carry over to representations the network holds in arbitrary directions.

### B. Superposition as an explanation

The theoretical form: there are more features than directions, and they overlap \[[1.1](#ref-1-1)\]. The source of the difference is a prediction: superposition promises that the features are recoverable by a sparse decomposition, whereas plain polysemanticity says nothing about that. In the grokking corpus this prediction has not been tested.

### C. Monosemanticity as a lever rather than a goal

The applied reading: if monosemanticity declines with scale, then inhibiting it can be used as a training technique \[[3.1](#ref-3-1)\]. The distinguishing feature is the direction of the conclusion: not "let us make the network clearer" but "let us make it faster", with interpretability incidental. A caveat: the link between inhibition and acceleration was shown in its own setup and has not been checked on the algorithmic tasks of the corpus.

## References

###### ref-1-1
**\[1.1\]** 2405.12755 — Golechha, "Progress Measures for Grokking on Real-world Tasks". [`"While some model components represent features in superpo"`](../papers/2405.12755.progress-measures-for-grokking-on-real-world-tasks/original/2405.12755.progress-measures-for-grokking-on-real-world-tasks.md#p4-2).

###### ref-1-2
**\[1.2\]** 2503.23298 — Wang et al., "Learning Towards Emergence: Paving the Way to Induce Emergence by Inhibiting Monosemantic Neurons on Pre-trained Models". [`"The literature has observed that monosemantic neurons in neural networks gradually diminish as the model scale increases."`](../papers/2503.23298.learning-towards-emergence-inhibiting-monosemantic-neurons-on-pre-trained-models/2503.23298.learning-towards-emergence-inhibiting-monosemantic-neurons-on-pre-trained-models.card.md#p1-2).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2503.23298 — Wang et al., "Learning Towards Emergence: Paving the Way to Induce Emergence by Inhibiting Monosemantic Neurons on Pre-trained Models". Nuance: monosemanticity is defined operationally — by the statistics of responses to a single feature, through sparse probing. [`"The left figure shows the output statistics of a monosemantic neuron, which is activated only by the feature “Python”."`](../papers/2503.23298.learning-towards-emergence-inhibiting-monosemantic-neurons-on-pre-trained-models/2503.23298.learning-towards-emergence-inhibiting-monosemantic-neurons-on-pre-trained-models.card.md#fig-1).

###### ref-3-2
**\[3.2\]** 2402.16726 — Furuta et al., "Towards Empirical Interpretation of Internal Circuits and Properties in Grokked Transformers on Modular Polynomials". Nuance: the transfer of features between similar operations is a mild form of polysemanticity, testable where the algorithm is known. [`"*grokked models obtain common features transferable among similar op"`](../papers/2402.16726.towards-empirical-interpretation-of-internal-circuits-and-properties-in-grokked-transformers-on-modular-polynomials/original/2402.16726.towards-empirical-interpretation-of-internal-circuits-and-properties-in-grokked-transformers-on-modular-polynomials.md#p1-3).
