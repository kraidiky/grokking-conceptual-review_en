# Selective (layerwise) weight decay

[Edge of stability](edge-of-stability.md) ← previous card, next → [The direction of the weight-decay effect](weight-decay-direction.md)

[Concept card index](index.md), category: [4. Training and optimisation factors](index.md#cat-4)\
→ Next category: [Grokfast / gradient low-pass filtering](gradient-low-pass-filtering.md)\
← Previous category: [Modular arithmetic](modular-arithmetic.md)

## Definition

**Selective weight decay** is the application of [weight decay](weight-decay.md) not to all the network's parameters but to a chosen part of them: usually the embeddings, biases and normalisation scales are taken out from under the penalty, though the reverse is also met. The device is old, and in papers on [grokking](grokking.md) it most often passes as a line in the description of the setup rather than as an object of study: *"weight decay has only been applied to the decoder and not to the embedding layer"*, with the authors noting at once that this distinguishes their setup from the original one \[[1.1](#ref-1-1)\].

The distinction matters, because a scalar $\lambda$ in a report does not say what it is applied to — and both the time to generalisation and which solution gets chosen depend on that.

## Elaboration

**What exactly is taken out from under the penalty.** All the usual partitions occur in the corpus: weight matrices only — *"decoupled weight decay $\lambda$ applied to weight matrices only"* \[[1.2](#ref-1-2)\]; everything except biases and norms \[[3.2](#ref-3-2)\]; token and position embeddings excluded "following standard practice" \[[3.1](#ref-3-1)\]. The difference is not cosmetic: in one of the works the norm is defined over exactly the same set the penalty acts on — *"weight decay and the clamp act on $E,W_{1},W_{2}$; biases are unregularized and excluded from $\|W\|$"* \[[1.3](#ref-1-3)\] — so the quantity by which the delay is measured depends on the partition just as the delay itself does.

**The converse case.** The penalty is also imposed where it is usually removed. When layer normalisation is added, a large effective learning rate stops being enough and the norm of the attention-head inputs has to be reduced, *"which we achieve by applying weight decay to the scale parameters of the layernorm transforms"* \[[2.1](#ref-2-1)\]. This limits any conclusion of the form "weight decay is needed for grokking": what is needed is not the penalty itself but the lowering of a particular norm, and its addressee depends on the architecture.

**Parameter groups as a device.** The partition is sometimes an aim rather than a detail: the unembedding is kept *"as its own group so that the output head can be given a separate learning rate and weight decay, and so that it can be frozen independently"* \[[1.4](#ref-1-4)\]. In the same work the sweep includes a setting with zero decay on the readout head — and the collapse happens all the same, which clears the penalty of suspicion as its cause. A neighbouring work checks the groups by intervention: a one-shot scaling of any single group barely moves the time \[[3.4](#ref-3-4)\].

**Different $\lambda$ instead of "on/off".** The mild form of selectivity is not to exclude but to assign a coefficient of one's own: AdamW with a common $\lambda$ plus a separate $L_2$ on the embeddings \[[5.1](#ref-5-1)\]↗; a proposal to split the penalty between Lipschitz-active and remaining weights with two independent factors \[[3.5](#ref-3-5)\]; in theoretical settings this is allowed outright — *"we allow different layers to have different learning rate and weight decay schedules"* \[[3.6](#ref-3-6)\].

**What the corpus lacks.** A systematic comparison of partitions: no work runs the same experiment with several addressees of the penalty in order to measure how much the time to generalisation depends on it. The partition is almost always reported as a setting inherited from practice, and discrepancies between works in the value of $\lambda$ are therefore only conditionally comparable.

## Alternative definitions and nuances

### A. Exclusion as hygiene

The weak form: embeddings, biases and norms are taken out from under the penalty because that is the custom \[[3.1](#ref-3-1)\], \[[3.2](#ref-3-2)\]. The distinguishing feature is that the device is neither discussed nor tested; its price is that the number $\lambda$ in two works may mean different things, and comparing times between them is a tacit assumption.

### B. The addressee of the penalty as a control quantity

The strong form: the choice of which parameters to penalise itself decides whether the transition comes \[[2.1](#ref-2-1)\], \[[1.4](#ref-1-4)\]. The source of the difference is that here the partition is tested by intervention rather than inherited; hence the conclusion that what acts is not the penalty in general but the lowering of a particular norm.

### C. Layerwise decay as a non-Euclidean penalty

The mathematical form, where selectivity stops being an experimental setting. If a matrix is parameterised in factorised form, then a layerwise Frobenius penalty on the factors equals the nuclear norm of the product: eliminating the factorisation induces a variational penalty, and so *"explicit factorized weight decay corresponds to the nuclear norm"* \[[1.5](#ref-1-5)\]. For a network of $L$ layers the exponent depends on depth — *"in a deep linear network, layerwise weight decay corresponds to a Schatten-$p$ penalty on the end-to-end map, with $p=2/L$"* — and such a penalty compresses small singular values more strongly, shifting the representation towards a low effective rank \[[1.6](#ref-1-6)\].

The distinguishing feature is the subject of the claim: not "which matrices to penalise" but what implicit penalty on the learned map follows from the chosen partition. The consequences are testable: in the first work the nuclear norm selects between two geometries of the solution (a cyclic code against a simplex ETF) with an advantage of order $\Theta(K)$; in the second, the gap between the logarithmic clock of fitting and the polynomial clock of simplification is exactly the [delay](grokking-time.md).

### D. Decoupling versus a penalty in the loss

A neighbouring distinction easily confused with selectivity: whether decay is applied through the loss function or as a separate step after the optimiser. All three strategies of the work compared are applied *"decoupled (after the optimiser step, not through the loss)"* \[[3.2](#ref-3-2)\]. The distinguishing feature is that here what changes is not the addressee of the penalty but its interaction with an adaptive optimiser; for AdamW the two ways are not equivalent, and reports of $\lambda$ are therefore incomparable unless the way is stated.

## References

###### ref-1-1
**\[1.1\]** 2205.10343 — Liu et al., "Towards Understanding Grokking: An Effective Theory of Representation Learning". [`"weight decay has only been applied to the decoder and not to the embedding layer"`](../papers/2205.10343.towards-understanding-grokking-an-effective-theory-of-representation-learning/original/2205.10343.towards-understanding-grokking-an-effective-theory-of-representation-learning.md#p8-8).

###### ref-1-2
**\[1.2\]** 2606.13753 — Truong et al., "The Weight Norm Sets the Grokking Timescale: A Causal Delay Law". [`"decoupled weight decay $\lambda$ applied to weight matrices only"`](../papers/2606.13753.the-weight-norm-sets-the-grokking-timescale-a-causal-delay-law/2606.13753.the-weight-norm-sets-the-grokking-timescale-a-causal-delay-law.card.md#p4-6).

###### ref-1-3
**\[1.3\]** 2606.18465 — Truong, "What Does the Weight Norm Control in Grokking? Logit-Scale Mediation under Cross-Entropy". [`"Weight decay and the clamp act on $E,W_{1},W_{2}$; biases are unregularized and excluded from $\|W\|$."`](../papers/2606.18465.what-does-the-weight-norm-control-in-grokking-logit-scale-mediation-under-cross-entropy/2606.18465.what-does-the-weight-norm-control-in-grokking-logit-scale-mediation-under-cross-entropy.card.md#p10-4).

###### ref-1-4
**\[1.4\]** 2608.07436 — Janati et al., "Post-Grokking Collapse at the Representation–Readout Interface in Muon-Trained Transformers". [`"The unembedding is kept as its own group so that the output head can be given a separate learning rate and weight decay, and so that it can be frozen independently in the interventions reported below."`](../papers/2608.07436.post-grokking-collapse-at-the-representation-readout-interface-in-muon-trained-transformers/original/2608.07436.post-grokking-collapse-at-the-representation-readout-interface-in-muon-trained-transformers.md#p4-3).

###### ref-1-5
**\[1.5\]** 2606.08985 — Tan et al., "Beyond Neural Collapse: Task-Intrinsic Geometry Governs Neural Representations in Modular Arithmetic". [`"Therefore, explicit factorized weight decay corresponds to the nuclear norm"`](../papers/2606.08985.beyond-neural-collapse-task-intrinsic-geometry-governs-neural-representations-in-modular-arithmetic/2606.08985.beyond-neural-collapse-task-intrinsic-geometry-governs-neural-representations-in-modular-arithmetic.card.md#p11-7).

###### ref-1-6
**\[1.6\]** 2606.05863 — Tan et al., "Deciphering Two Training Clocks in Grokking via Deep Linear Network Theory with Conditional ReLU Reduction". [`"In a deep linear network, layerwise weight decay corresponds to a Schatten-$p$ penalty on the end-to-end map, with $p=2/L$."`](../papers/2606.05863.deciphering-two-training-clocks-in-grokking-via-deep-linear-network-theory-with-conditional-relu-reduction/2606.05863.deciphering-two-training-clocks-in-grokking-via-deep-linear-network-theory-with-conditional-relu-reduction.card.md#p2-7).

## References of works that joined the discussion

### Contested

###### ref-2-1
**\[2.1\]** 2507.20057 — Lyle et al., "What Can Grokking Teach Us About Learning Under Nonstationarity?". Contests the conclusion "weight decay is needed for grokking": what is needed is not the penalty in general but the lowering of a particular norm, and its addressee is set by the architecture. [`"it becomes necessary to also reduce the norm of the attention head inputs, which we achieve by applying weight decay to the scale parameters of the layernorm transforms in the network"`](../papers/2507.20057.what-can-grokking-teach-us-about-learning-under-nonstationarity/original/2507.20057.what-can-grokking-teach-us-about-learning-under-nonstationarity.md#fig-2).

### In support

###### ref-3-1
**\[3.1\]** 2605.04396 — Ali, "Critical Windows of Complexity Control: When Transformers Decide to Reason or Memorize". Nuance: the exclusion of embeddings is named as standard practice rather than as a finding; $\lambda$ itself is meanwhile taken out of the optimiser step so that it can be switched on and off on a schedule. [`"Token and position embeddings are excluded from weight decay, following standard practice."`](../papers/2605.04396.critical-windows-of-complexity-control-when-transformers-decide-to-reason-or-memorize/original/2605.04396.critical-windows-of-complexity-control-when-transformers-decide-to-reason-or-memorize.md#p4-3).

###### ref-3-2
**\[3.2\]** 2606.04405 — Li, "Low-Rank Decay for Grokking in Scale-Invariant Transformers: A Spectral-Geometric View". Nuance: the partition is reported together with the way it is applied — decoupled, after the optimiser step, not through the loss. [`"**L2 (Frobenius weight decay):** $W\leftarrow W\cdot(1-\eta\lambda)$, applied to all non-bias, non-norm parameters."`](../papers/2606.04405.low-rank-decay-for-grokking-in-scale-invariant-transformers-a-spectral-geometric-view/2606.04405.low-rank-decay-for-grokking-in-scale-invariant-transformers-a-spectral-geometric-view.card.md#p4-11).

###### ref-3-4
**\[3.4\]** 2606.13753 — Truong et al., "The Weight Norm Sets the Grokking Timescale: A Causal Delay Law". Nuance: the groups are checked by intervention — a one-shot scaling of any of them barely moves the time, so the matter is not the norm of an individual group. [`"A one-shot $0.8\times$ scaling of any single parameter group (embedding, hidden, or output) likewise leaves $T_{\mathrm{grok}}$ within"`](../papers/2606.13753.the-weight-norm-sets-the-grokking-timescale-a-causal-delay-law/2606.13753.the-weight-norm-sets-the-grokking-timescale-a-causal-delay-law.card.md#p7-2).

###### ref-3-5
**\[3.5\]** 2607.08350 — Pranjić et al., "Grokking and epoch-wise double descent in quantum neural networks". Nuance: selectivity is proposed along a non-architectural line — Lipschitz-active weights against the rest, with two independent factors. [`"one could penalize the Lipschitz-active and remaining weight-norms independently by decomposing the regularization term in Equation 4 using two distinct hyperparameters"`](../papers/2607.08350.grokking-and-epoch-wise-double-descent-in-quantum-neural-networks/2607.08350.grokking-and-epoch-wise-double-descent-in-quantum-neural-networks.card.md#p5-1).

###### ref-3-6
**\[3.6\]** 2207.08799 — Barak et al., "Hidden Progress in Deep Learning: SGD Learns Parities Near the Computational Limit". Nuance: in the theoretical setting different per-layer schedules are allowed outright — that is, selectivity is built into the formulation rather than chosen in an experiment. [`"We allow different layers to have different learning rate and weight decay schedules."`](../papers/2207.08799.hidden-progress-in-deep-learning-sgd-learns-parities-near-the-computational-limit/2207.08799.hidden-progress-in-deep-learning-sgd-learns-parities-near-the-computational-limit.card.md#p4-5).

### External works

###### ref-5-1
**\[5.1\]** 2502.01628 — **External work (excerpt): Liu, Tegmark et al., "Harmonic Loss Trains Interpretable AI Models".** Nuance: the selectivity here is mild — the optimiser's common weight decay is supplemented by a separate $L_2$ on the embeddings, so the embeddings have a factor of their own rather than an exemption. [`"a weight decay of $10^{-2}$, and an $L_{2}$ regularization on the embeddings with strength 0.01"`](../externals/2502.01628.harmonic-loss-trains-interpretable-ai-models/original/2502.01628.harmonic-loss-trains-interpretable-ai-models.md#p4-3).
