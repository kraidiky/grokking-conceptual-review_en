# Overparameterisation and depth

[The direction of the weight-decay effect](weight-decay-direction.md) ← previous card, next → [architectural-inductive-bias](architectural-inductive-bias.md)

[Concept card index](index.md), category: [4. Training and optimisation factors](index.md#cat-4)\
→ Next category: [Grokfast / gradient low-pass filtering](gradient-low-pass-filtering.md)\
← Previous category: [Modular arithmetic](modular-arithmetic.md)

## Definition

**Overparameterisation** is an excess of parameters relative to the amount of training data, at which the network is able to fit the sample completely; **depth** is the number of layers this fitting passes through. Both quantities enter the conversation about [grokking](grokking.md) as controls: whether delayed generalisation happens, and when, depends on them. The general frame of the problem runs thus: there is no complete theory of generalisation in overparameterised models, and grokking, alongside [neural collapse](neural-collapse.md), is one of the observations that might bring it closer \[[1.1](#ref-1-1)\].

A systematic test of depth gives an unexpected answer: *"depth has a non-monotonic effect"* — depth-4 MLPs consistently fail to grok, whereas depth-8 residual networks recover generalisation \[[1.2](#ref-1-2)\].

## Elaboration

**The non-monotonicity and its cause.** The naive expectation "deeper is better" does not hold: between depth 2 and depth 8 lies a dip out of which the network is pulled not by extra layers but by stabilisation — residual connections and normalisation \[[3.1](#ref-3-1)\]. Hence the conclusion the notion is kept for: the observed effect of depth is confounded with the effect of optimisation stability, and works that change only the number of layers measure not depth but the training's ability not to fall apart \[[1.2](#ref-1-2)\].

**Overparameterisation as a condition, not a cause.** Grokking is usually observed in overparameterised networks, but there is no necessity in that: the results on [sparse parity](sparse-parity.md) were obtained in narrow-width regimes where no fixed kernel, including the [NTK](neural-tangent-kernel-ntk.md), can solve the task \[[3.2](#ref-3-2)\], \[[3.3](#ref-3-3)\]. That is, delayed generalisation does not require an excess of parameters — it requires the task to be computationally hard to solve quickly.

**Why the excess does not get in the way of generalisation at all.** The standard explanation is that the intrinsic dimension of the learned representation is far smaller than the ambient one: a network with a huge number of parameters lives on a low-dimensional manifold \[[3.4](#ref-3-4)\]. For grokking this matters because it turns the question "why does a redundant network generalise" into the question "when does it find the low-dimensional solution", and that is already a question about [representation compression](manifold-representation-compression.md) and about timing.

**How this is measured.** Depth and width enter the sweeps on a par with the modulus and the data fraction: an optimiser's advantage is checked for robustness across modulus, training fraction, width and depth \[[3.5](#ref-3-5)\], while the grid of depths itself is set together with the number of seeds, because at greater depth the spread grows \[[3.6](#ref-3-6)\].

## Alternative definitions and nuances

### A. Depth as a control parameter

The direct usage: change the number of layers all else being equal and watch the outcome \[[1.2](#ref-1-2)\], \[[3.6](#ref-3-6)\]. The distinguishing feature is non-monotonicity: the result is not captured by "deeper is better" or "worse", and any claim about depth requires saying whether the network is stabilised by residual connections and normalisation.

### B. Overparameterisation as a regime

What matters here is not the number of layers but the ratio of the number of parameters to the amount of data. The corpus's caveat: grokking reproduces outside this regime as well \[[3.2](#ref-3-2)\], so overparameterisation is the usual condition of the experiments rather than a necessary part of the phenomenon.

### C. Low dimensionality of what is learned as the reconciling account

The third position removes the contradiction "an excess of parameters versus the simplicity of the solution": the ambient space is large, but the learned representation lies on a low-dimensional submanifold \[[3.4](#ref-3-4)\]. The distinguishing feature is what is measured: not the number of parameters but the intrinsic dimension of the representation, and it is therefore checked by spectral measures rather than by counting weights.

## References

###### ref-1-1
**\[1.1\]** 2210.15435 — Žunkovič et al., "Grokking phase transitions in learning local rules with gradient descent". [`"we still do not have a complete theory of generalisation in over-parameterised models"`](../papers/2210.15435.grokking-phase-transitions-in-learning-local-rules-with-gradient-descent/2210.15435.grokking-phase-transitions-in-learning-local-rules-with-gradient-descent.card.md#p3-1).

###### ref-1-2
**\[1.2\]** 2603.25009 — Manir et al., "A Systematic Empirical Study of Grokking: Depth, Architecture, Activation, and Regularization". [`"**depth has a non-monotonic effect**, with depth-4 MLPs consistently failing to grok while depth-8 residual networks recover generalization"`](../papers/2603.25009.a-systematic-empirical-study-of-grokking-depth-architecture-activation-and-regularization/2603.25009.a-systematic-empirical-study-of-grokking-depth-architecture-activation-and-regularization.card.md#p1-3).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2603.25009 — Manir et al., "A Systematic Empirical Study of Grokking: Depth, Architecture, Activation, and Regularization". Nuance: the dip at intermediate depth is cured not by layers but by stabilisation — residual connections and normalisation. [`"**Depth requires stabilization.** Grokking exhibits a non-monotonic dependence on depth"`](../papers/2603.25009.a-systematic-empirical-study-of-grokking-depth-architecture-activation-and-regularization/2603.25009.a-systematic-empirical-study-of-grokking-depth-architecture-activation-and-regularization.card.md#p2-2).

###### ref-3-2
**\[3.2\]** 2207.08799 — Barak et al., "Hidden Progress in Deep Learning: SGD Learns Parities Near the Computational Limit". Nuance: delayed generalisation reproduces without an excess of parameters — in narrow-width regimes. [`"Our theoretical and empirical results hold in non-overparameterized regimes"`](../papers/2207.08799.hidden-progress-in-deep-learning-sgd-learns-parities-near-the-computational-limit/2207.08799.hidden-progress-in-deep-learning-sgd-learns-parities-near-the-computational-limit.card.md#p3-5).

###### ref-3-3
**\[3.3\]** 2207.08799 — Barak et al., "Hidden Progress in Deep Learning: SGD Learns Parities Near the Computational Limit". Nuance: in these regimes no fixed kernel solves the task, so the matter is not capacity but computational hardness. [`"no fixed kernel (including the neural tangent kernel (Jacot et al. 2018), whose dimensionality is the network’s parameter count) can solve the sparse parity problem"`](../papers/2207.08799.hidden-progress-in-deep-learning-sgd-learns-parities-near-the-computational-limit/2207.08799.hidden-progress-in-deep-learning-sgd-learns-parities-near-the-computational-limit.card.md#p8-4).

###### ref-3-4
**\[3.4\]** 2211.13239 — Brown et al., "Relating Regularization and Generalization through the Intrinsic Dimension of Activations". Nuance: an excess of parameters is compatible with a simple solution, because the learned representation lies on a low-dimensional submanifold. [`"the success of vastly over-parameterized neural networks (Zhang et al. 2016) seems counterintuitive"`](../papers/2211.13239.relating-regularization-and-generalization-through-the-intrinsic-dimension-of-activations/original/2211.13239.relating-regularization-and-generalization-through-the-intrinsic-dimension-of-activations.md#p2-1).

###### ref-3-5
**\[3.5\]** 2608.07436 — Janati et al., "Post-Grokking Collapse at the Representation–Readout Interface in Muon-Trained Transformers". Nuance: depth enters the sweep on a par with the modulus, the training fraction and the width — as an axis for checking the robustness of the result. [`"the advantage holds across modulus, training fraction, width, and depth"`](../papers/2608.07436.post-grokking-collapse-at-the-representation-readout-interface-in-muon-trained-transformers/original/2608.07436.post-grokking-collapse-at-the-representation-readout-interface-in-muon-trained-transformers.md#p4-3).

###### ref-3-6
**\[3.6\]** 2603.25009 — Manir et al., "A Systematic Empirical Study of Grokking: Depth, Architecture, Activation, and Regularization". Nuance: the grid of depths is set together with the number of seeds, because at greater depth training is less stable. [`"We evaluate three depths: $d\in\{2,4,8\}$."`](../papers/2603.25009.a-systematic-empirical-study-of-grokking-depth-architecture-activation-and-regularization/2603.25009.a-systematic-empirical-study-of-grokking-depth-architecture-activation-and-regularization.card.md#p4-9).
