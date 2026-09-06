# Linear and sparse probing

[Heavy-tailed self-regularization (HTSR)](heavy-tailed-self-regularization-htsr.md) ← previous card, next → [phase-diagram](phase-diagram.md)

[Concept card index](index.md), category: [6. Analytical tools and metrics](index.md#cat-6)\
→ Next category: [Effective theory and statistical mechanics](effective-theory-statistical-mechanics.md)\
← Previous category: [Grokfast / gradient low-pass filtering](gradient-low-pass-filtering.md)

## Definition

**Linear probing** is a method for analysing a network's internal representations: a light linear classifier (a "probe") is attached to the frozen hidden activations of a trained model, and from its accuracy one judges whether the property of interest is linearly decodable from those activations; high probe accuracy is read as a sign of the quality and structure of the internal representation \[[1.1](#ref-1-1)\]. **Sparse probing** is a variant of the same device that selects not the whole representation but a sparse subset of individual neurons for detecting a specific feature \[[2.1](#ref-2-1)\]. Into the context of [grokking](grokking.md), as an instrument for frame-by-frame observation of representations, it is brought by Fan et al. \[[1.1](#ref-1-1)\] and Kvinge et al. \[[5.1](#ref-5-1)\]↗.

## Elaboration

The canonical procedure: a randomly initialised linear "head" is attached to each internal layer of the network, trained on the training set for a fixed number of steps and then evaluated on the test set; the accuracy of such a probe measures whether the learned features are good enough to be **linearly separable** (that is, whether the classes can be separated by a hyperplane) in the high-dimensional space \[[1.1](#ref-1-1)\]. Probe accuracy thereby works as an [order parameter](order-parameter.md) (a scalar quantity tracking the transition) for the quality of the representation across layers and across training steps. The targeted variant probes not "quality in general" but the decodability of a specific concept: Kvinge et al. train a linear probe to predict, from the hidden activations, whether a pair of elements belongs to a subgroup, and calibrate it with a random labelling in order to tell genuine algebraic structure from an artefact \[[5.1](#ref-5-1)\]↗. Sparse probing (introduced by Gurnee et al., 2023; in this corpus applied by Wang et al.) selects a sparse set of neurons and, by F1 score or interpretability, identifies **monosemantic neurons** — those activating on exactly one feature \[[2.1](#ref-2-1)\]. The method has a contested side: probing is computationally expensive, and on small models (70M parameters) the probe classifier may fail to catch the target neurons \[[2.1](#ref-2-1)\], while probe accuracy varies noticeably between runs — sometimes the model solves the task correctly but the probe guesses at chance level \[[5.1](#ref-5-1)\]↗. On the other hand, frame-by-frame linear probing records that the decodability of the target information from the hidden states grows over the course of grokking and reaches perfection only after the transition \[[3.1](#ref-3-1)\], while the accuracy of a subgroup probe tracks the global accuracy \[[5.1](#ref-5-1)\]↗ — which makes the probe a [progress measure](progress-measures.md) for the representation. A related but different device in kind is the interventional (causal) probe: Truong et al. (2604.13123) intervene in the representation itself (a representation-mixing probe) rather than training a classifier on top of it; that is not linear or sparse probing but a causal test. The method is in demand in work on [emergence](emergence.md), where the probe is used to judge that internal features appear earlier than the external metric shows.

## Alternative definitions and nuances

### A. A probe of representation quality across layers (Fan et al.)

Here probing is defined operationally: a linear head on each internal layer, trained for a fixed number of steps, with its test accuracy a scalar estimate of how linearly separable the internal features are \[[1.1](#ref-1-1)\]. The distinguishing machinery is the layer-wise profile of probe accuracy as an indicator of at what depth and at what moment of training a "good" representation forms; the probe here is agnostic to the content of the task and measures quality, not a specific concept.

### B. A targeted probe for a specific concept, with calibration (Kvinge et al.)

A definition through the decodability of a property fixed in advance: the activations are labelled binarily (does the pair of elements belong to the subgroup H) and a linear probe is trained to predict that label \[[5.1](#ref-5-1)\]↗. The key difference is the presence of a **calibration baseline**: in parallel, the probe is trained on a random subset of elements that does not form a subgroup, and the conclusion that the structure really is encoded is drawn only if the probe on the true subgroup beats the probe on the random labelling \[[5.1](#ref-5-1)\]↗. The source of the difference from reading A: the probe tests for the presence of a specific algebraic structure, not for general quality.

### C. Sparse probing of neurons (Gurnee et al. via Wang et al.)

A definition through the selection of neurons rather than through the whole representation: the probe picks a sparse subset of neurons most informative about a given feature and, by their statistics (F1, auto-interpretability), detects monosemantic neurons \[[2.1](#ref-2-1)\]. The difference from A and B is the unit of analysis: not a hyperplane in the full activation space but a small set of individual neuron coordinates; this makes the probe an instrument for mechanistically attributing a feature to specific neurons.

### Contested

Wang et al. (2503.23298) join sparse probing as a reference standard but contest its practical fitness as a working detector: probing experiments are costly in time and call for cheaper alternatives, and on a small model the probe classifier turns out to be ineffective — hence a proxy metric is proposed (the Monosemanticity Score) \[[2.1](#ref-2-1)\].

### In support

Wang et al. (2405.15071) join the reading of the probe as a progress measure for the representation: linear probing of the hidden state shows that the target information becomes perfectly decodable after grokking, and that decodability improves monotonically throughout the transition \[[3.1](#ref-3-1)\].

## References

###### ref-1-1
**\[1.1\]** 2405.19454 — Fan, Pascanu, Jaggi 2024, "Deep Grokking: Would Deep Neural Networks Generalize Better?". [`"For linear probing, we attach a randomly initialized linear classifier head to each internal layer $l$ of the neural network. We train the linear head only for a fixed number of steps on the training set, then evaluate it on the test set."`](../papers/2405.19454.deep-grokking-would-deep-neural-networks-generalize-better/2405.19454.deep-grokking-would-deep-neural-networks-generalize-better.card.md#p2-2).\
Also: [`"The linear probing accuracy measures whether the learnt internal features are good enough to be linearly separable in the high-dimensional space."`](../papers/2405.19454.deep-grokking-would-deep-neural-networks-generalize-better/2405.19454.deep-grokking-would-deep-neural-networks-generalize-better.card.md#p2-2)

## References of works that joined the discussion

### Contested

###### ref-2-1
**\[2.1\]** 2503.23298 — Wang et al., "Learning Towards Emergence: Inducing Emergence by Inhibiting Monosemantic Neurons". Contests: probing is costly and unreliable on small models, and a cheaper proxy is needed. [`"However, probing experiments are time-consuming, making it crucial to develop alternative methods to boost the study of monosemanticity."`](../papers/2503.23298.learning-towards-emergence-inhibiting-monosemantic-neurons-on-pre-trained-models/2503.23298.learning-towards-emergence-inhibiting-monosemantic-neurons-on-pre-trained-models.card.md#p3-5).\
Also: [`"probing classifier may not be effective in detecting monosemantic neurons in the 70M model."`](../papers/2503.23298.learning-towards-emergence-inhibiting-monosemantic-neurons-on-pre-trained-models/2503.23298.learning-towards-emergence-inhibiting-monosemantic-neurons-on-pre-trained-models.card.md#p13-6)\
Also (the device itself as a reference standard): [`"We use sparse probing (Gurnee et al., 2023) on Pythia models (Biderman et al., 2023) to detect monosemantic neurons."`](../papers/2503.23298.learning-towards-emergence-inhibiting-monosemantic-neurons-on-pre-trained-models/2503.23298.learning-towards-emergence-inhibiting-monosemantic-neurons-on-pre-trained-models.card.md#fig-1)

### In support

###### ref-3-1
**\[3.1\]** 2405.15071 — Wang et al., "Grokked Transformers are Implicit Reasoners". Nuance: the probe as a progress measure — decodability grows over the course of grokking. [`"We also run linear probing on S[5, r1] throughout training to predict the second token of the bridge entity b"`](../papers/2405.15071.grokked-transformers-are-implicit-reasoners/2405.15071.grokked-transformers-are-implicit-reasoners.card.md#p18-1).\
Also: [`"the second token of $b$ can be perfectly decoded from $S[5,r_{1}]$ after grokking, and the decodability improves throughout grokking"`](../papers/2405.15071.grokked-transformers-are-implicit-reasoners/2405.15071.grokked-transformers-are-implicit-reasoners.card.md#p18-1)

###### ref-3-2
**\[3.2\]** 2604.06256 — Xu, "Spectral Edge Dynamics Reveal Functional Modes of Learning". Nuance: what is declared to be the support is not the value of $R^{2}$ (for $x^{2}+y^{2}$ it is $0.15$–$0.16$) but the qualitative selectivity of the cross terms; there are no causal interventions. [`"We test this by probing the perturbation with three feature sets via ridge regression"`](../papers/2604.06256.spectral-edge-dynamics-reveal-functional-modes-of-learning/original/2604.06256.spectral-edge-dynamics-reveal-functional-modes-of-learning.md#p11-6).

###### ref-3-3
**\[3.3\]** 2604.13082 — Gomezjurado Gonzalez, "The Long Delay to Arithmetic Generalization…". [`"Each probe is an L2-regularized logistic regression fit on standardized mean-pooled encoder states."`](../papers/2604.13082.the-long-delay-to-arithmetic-generalization-when-learned-representations-outrun-behavior/original/2604.13082.the-long-delay-to-arithmetic-generalization-when-learned-representations-outrun-behavior.md#p14-3).\
Also (an extreme case of probe and behaviour parting company): in a 12-layer decoder-only baseline, [`"Exact-match at the final checkpoint is $0.000$ in every base"`](../papers/2604.13082.the-long-delay-to-arithmetic-generalization-when-learned-representations-outrun-behavior/original/2604.13082.the-long-delay-to-arithmetic-generalization-when-learned-representations-outrun-behavior.md#p25-2) — with probes at $\geq 0.999$ in the early layers.
###### ref-3-4
**\[3.4\]** 2604.07380 — Xu 2026, "The Lifecycle of the Spectral Edge: From Gradient Learning to Weight-Decay Compression". A telling gap between probes: the linear probe for depth falls to 0.86 (on individual seeds to 0.67) and the quadratic one to 0.59, while an MLP probe holds 0.990 — the information is not lost but nonlinearly re-encoded by weight-decay compression; in a memorising model the linear probe score is higher, which is read as a sign of explicit storage rather than of better computation. [`"A shallow MLP probe (one hidden layer, 64 units) recovers $R^{2}=0.990\pm 0.003$ on the same representations"`](../papers/2604.07380.the-lifecycle-of-the-spectral-edge-from-gradient-learning-to-weight-decay-compression/original/2604.07380.the-lifecycle-of-the-spectral-edge-from-gradient-learning-to-weight-decay-compression.md#p5-5).\
Also (the inversion): [`"the memorized model has *higher* linear probe $R^{2}$ for depth (0.95 vs. 0.71)"`](../papers/2604.07380.the-lifecycle-of-the-spectral-edge-from-gradient-learning-to-weight-decay-compression/original/2604.07380.the-lifecycle-of-the-spectral-edge-from-gradient-learning-to-weight-decay-compression.md#p10-1).

###### ref-3-5
**\[3.5\]** 2606.00230 — Muckatira, Shivagunde, Deshpande, Rumshisky 2026, "A Pre-Training Analogue of Grokking in Language Models: Tracing Delayed Grammatical Generalization". A grammatical concept vector as the difference of the hidden states of the acceptable and the unacceptable sentence of a BLiMP minimal pair: the mean vector, computed on a proxy training split, separates grammaticality on the proxy validation split by an inner product (AUROC), and the effective rank of the centred matrix of concept vectors is higher after the transition than before it in all five sets — against the line that "representations compress after generalisation". Nuance: the AUROC rises clearly for only three phenomena out of five (for irregular participles the separability is high from the start; for the second agreement case it is at chance); the dispute about compression is conducted on incomparable measures — the rank is computed over pair differences, whereas the works cited measured the hidden states themselves; and the comparison of the points $t_{\text{before}}=100$ and $t_{\text{after}}$ (500–1400 steps) is confounded with the general course of early training. [`"we find that for these concept vectors, effective rank generally increases after delayed generalization, suggesting that the grammatical concept does not collapse into a few dominant directions."`](../papers/2606.00230.a-pre-training-analogue-of-grokking-in-language-models-tracing-delayed-grammatical-generalization/original/2606.00230.a-pre-training-analogue-of-grokking-in-language-models-tracing-delayed-grammatical-generalization.md#p7-2).

## Passing mentions

Works that only mention the phenomenon — a literature review, a related-work paragraph, a passing citation — without examining it.

**\[4.1\]** 2604.13123 — Truong et al., "Spectral Entropy Collapse as a Phase Transition in Delayed Generalisation". [`"We provide interventional evidence via a representation-mixing probe, with an extended norm-matched control ($n=30$) disentangling the roles of parameter norm and representation entropy"`](../papers/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation.card.md#p2-3) (Different in kind — an interventional, causal probe on the activations, not a trained linear or sparse classifier on top of them.)


### External works

###### ref-5-1
**\[5.1\]** 2601.21150 — External work (demoted from the corpus): Kvinge et al., "Can Neural Networks Learn Small Algebraic Worlds?". [`"We can test whether $f$ captures a distinct representation of $H$ by probing for subgroup membership on the hidden activations of $f$"`](../externals/2601.21150.can-neural-networks-learn-small-algebraic-worlds/2601.21150.can-neural-networks-learn-small-algebraic-worlds.card.md#p7-2).\
Also: [`"we find substantial evidence that performant models sometimes capture subgroup structure within their internal representations which we can access via the linear probing"`](../externals/2601.21150.can-neural-networks-learn-small-algebraic-worlds/2601.21150.can-neural-networks-learn-small-algebraic-worlds.card.md#p7-6)
