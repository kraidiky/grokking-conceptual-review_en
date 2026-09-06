# Heavy-tailed self-regularization (HTSR)

[seed-variance-reproducibility](seed-variance-reproducibility.md) ← previous card, next → [Linear and sparse probing](linear-sparse-probing.md)

[Concept card index](index.md), category: [6. Analytical tools and metrics](index.md#cat-6)\
→ Next category: [Effective theory and statistical mechanics](effective-theory-statistical-mechanics.md)\
← Previous category: [Grokfast / gradient low-pass filtering](gradient-low-pass-filtering.md)

## Definition

**Heavy-tailed self-regularization (HTSR)** is a theory (Martin & Mahoney, 2021) that studies the empirical spectral density (ESD — the distribution of eigenvalues of the correlation matrix of a layer's weights) of individual weight matrices and characterises it by a single quantity, the heavy-tailed power-law (PL) exponent α. Into the grokking corpus HTSR is brought as an analytic lens by Prakash & Martin: they apply it to delayed generalisation, showing that the HTSR exponent α tracks the passage into the [grokking](grokking.md) phase and predicts the subsequent fall of generalisation \[[1.1](#ref-1-1)\]\[[1.2](#ref-1-2)\].

![The evolution of the heavy-tailed exponent alpha per layer over the course of optimisation (fig. 4 of Prakash & Martin)](assets/htsr-alpha-evolution.png)

## Elaboration

The mechanics are as follows. For each weight matrix `W` a correlation (Gram) matrix is built, and its eigenvalues give the ESD; if the entries of `W` were independent and identically distributed, the ESD would converge to the **Marchenko–Pastur (MP)** distribution — the random-matrix "null model" against which actually trained weights are compared. In trained layers the right edge of the ESD, instead of an MP bulk edge, spreads into a power-law tail `ρ ∼ λ^−α`, and the exponent α quantifies the strength of the correlations \[[1.1](#ref-1-1)\]. α thereby works as an **[order parameter](order-parameter.md)**: on HTSR, different ranges of α correspond to different phases of training — α ≳ 5–6 (the layer is nearly random, little structure), 2 ≲ α ≲ 5–6 (a moderately heavy tail, the layer is well conditioned and generalises better), α = 2 (the ideal — a fully optimised layer) and α < 2 (a very heavy tail, VHT — a sign of overfitting) \[[1.1](#ref-1-1)\]. The lower boundary α = 2 is a hard cut-off; the upper one (5–6) is softer and depends on the aspect ratio of the matrix.

Hence the practical conclusion: α ≈ 2 is a universal convergence target for a layer, and the trajectory α(t) is a sensitive indicator of the network's state. A sharp fall of α towards 2 coincides with the onset of grokking, while a further drop below 2 foreshadows and then characterises the late collapse — [anti-grokking](anti-grokking.md) \[[1.2](#ref-1-2)\]. A later work links HTSR to its continuation, the theory **SETOL** (Semi-Empirical Theory of Learning), and adds a second spectral metric — [correlation traps](correlation-traps.md) (anomalously large eigenvalues of a shuffled weight matrix) — with the traps, rather than α, declared the principal signal of the collapse; in the MA model their appearance is accompanied by a rise of α above 2 — [catastrophic forgetting](catastrophic-forgetting.md) \[[1.2](#ref-1-2)\]. Both statuses of α (by phases) and the nature of the collapse make HTSR akin to a wider circle of phenomena — [phase transitions](phase-transition.md) in the dynamics of training.

## Alternative definitions and nuances

### A. α as an order parameter / a measure of layer quality (HTSR)

A reading of α not merely as a number but as an order parameter: a single quantity extracted from a layer's ESD, monotonically relating the strength of the weight correlations to the phase of training and the degree of convergence of that particular layer \[[1.1](#ref-1-1)\]. The source of the difference: the exponent is tied to an individual layer (layer quality) and sets ranges (α > 5–6 "random", 2–5 "fat-tailed", < 2 "very heavy"), rather than to the network as a whole; α = 2 acts as a hard universal cut-off between good generalisation and overfitting.

### B. α = 2 as the phase boundary of thermodynamic equilibrium (SETOL)

A reading of α = 2 not empirically but as a phase boundary: on SETOL, the theory complementing HTSR, a layer reaches thermodynamic equilibrium at optimal generalisation, and the condition α = 2 corresponds to the boundary between ideal generalisation and overfitting, while a layer with α < 2 and/or with correlation traps is in a state of overfitting \[[1.2](#ref-1-2)\]. The source of the difference: α = 2 acquires a theoretical grounding (an analogy with Wilson's exact renormalisation group) rather than being postulated from observations.

### In support

- **Spectral entropy as a complementary order parameter** \[[3.1](#ref-3-1)\]: the work takes the HTSR exponent α as a landmark but proposes a quantity of its own — the normalised spectral entropy of the representations — and conjectures outright that its critical threshold corresponds to that same HTSR passage of the weight spectrum from an MP bulk to "bulk + power-law tail". The source of the difference: the phenomenon is described by an additional, independently measured order parameter that agrees with the heavy-tailed picture rather than being set against it.

## References

###### ref-1-1
**\[1.1\]** 2506.04434 — Prakash & Martin 2025, "Grokking and Generalization Collapse: Insights from HTSR theory". [`"HTSR theory examines the empirical spectral density (ESD) of individual layer weight matrices $(\mathbf{W})$, quantified by the heavy-tailed power law (PL) exponent $\alpha$"`](../papers/2506.04434.grokking-and-generalization-collapse-insights-from-htsr-theory/original/2506.04434.grokking-and-generalization-collapse-insights-from-htsr-theory.md#p1-4).\
Also: [`"with the exponent $\alpha$ quantifying the strength of the correlations"`](../papers/2506.04434.grokking-and-generalization-collapse-insights-from-htsr-theory/original/2506.04434.grokking-and-generalization-collapse-insights-from-htsr-theory.md#p3-10); [`"$\alpha=2$ **Ideal value:** Corresponds to fully optimized layers in models. Associated with layers in models that generalize best."`](../papers/2506.04434.grokking-and-generalization-collapse-insights-from-htsr-theory/original/2506.04434.grokking-and-generalization-collapse-insights-from-htsr-theory.md#p4-1).

###### ref-1-2
**\[1.2\]** 2602.02859 — Prakash & Martin, "Late-Stage Generalization Collapse in Grokking: Detecting anti-grokking with WeightWatcher". [`"we examine two layer quality metrics: (i) the HTSR PL exponent α, and (ii) the SETOL Correlation Traps"`](../papers/2602.02859.late-stage-generalization-collapse-in-grokking-detecting-anti-grokking-with-weightwatcher/original/2602.02859.late-stage-generalization-collapse-in-grokking-detecting-anti-grokking-with-weightwatcher.md#p3-8).\
Also (α < 2 — a very heavy tail, overfitting): [`"$\alpha<2$: **Very-Heavy-Tailed (VHT)** Extremely heavy tails indicate overfitting to the training data"`](../papers/2602.02859.late-stage-generalization-collapse-in-grokking-detecting-anti-grokking-with-weightwatcher/original/2602.02859.late-stage-generalization-collapse-in-grokking-detecting-anti-grokking-with-weightwatcher.md#p3-11).\
Also (α = 2 as a phase boundary, SETOL): [`"A layer with $\alpha<2$, and/or one or more Correlation Traps (below), corresponds to states of overfitting, as observed here"`](../papers/2602.02859.late-stage-generalization-collapse-in-grokking-detecting-anti-grokking-with-weightwatcher/original/2602.02859.late-stage-generalization-collapse-in-grokking-detecting-anti-grokking-with-weightwatcher.md#p3-13).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2604.13123 — Truong et al., "Spectral Entropy Collapse as a Phase Transition in Delayed Generalisation: An Interventional and Predictive Framework for Grokking". Nuance: takes the HTSR exponent α as a landmark and proposes an additional order parameter aligned with it — spectral entropy. [`"Prakash and Martin (2025) use Heavy-Tailed Self-Regularisation with the spectral exponent $\alpha$ and identify an *anti-grokking* regime"`](../papers/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation.card.md#p3-5)\
Also (the conjecture about correspondence with the bulk→tail passage): [`"the threshold $\tilde{H}^{*}\approx 0.609$ corresponds to the point at which the weight-matrix spectrum transitions from Marchenko–Pastur-dominated (bulk regime) to bulk + power-law-tail (learned-feature regime)"`](../papers/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation.card.md#p18-4).


###### ref-3-2
**\[3.2\]** 2605.12394 — Prakash & Martin 2026, "Detecting overfitting in Neural Networks during long-horizon grokking using Random Matrix Theory". An inversion of the instrument within the line: instead of the heavy-tailed structure of the correlated matrix $\mathbf{W}$, what is analysed is the spectrum of the element-wise shuffled $\mathbf{W}^{\mathrm{rand}}$ — an outlier that survives the shuffling speaks of the atypicality of the distribution of entries itself; the exponent $\alpha$ is not used, and it is stated outright that the mechanism does not require a tail with an exponent below two. [`"Prior spectral diagnostics use heavy-tailed structure of the correlated (unrandomized) layer weight matrices $\mathbf{W}$, and related metrics to characterize trained networks. We analyze the spectral properties of the randomized $\mathbf{W}$"`](../papers/2605.12394.detecting-overfitting-in-neural-networks-during-long-horizon-grokking-using-random-matrix-theory/original/2605.12394.detecting-overfitting-in-neural-networks-during-long-horizon-grokking-using-random-matrix-theory.md#p2-7).\
Also (an exponent below 2 is not needed): [`"The mechanism does not require exponent $<2$, and the observed traps are often driven by several large or moderately large entries rather than one extraordinary coordinate"`](../papers/2605.12394.detecting-overfitting-in-neural-networks-during-long-horizon-grokking-using-random-matrix-theory/original/2605.12394.detecting-overfitting-in-neural-networks-during-long-horizon-grokking-using-random-matrix-theory.md#p20-3).

### Contested

###### ref-2-1
**\[2.1\]** 2605.20441 — Verma 2026, "Weight Decay Regimes in Grokking Transformers: Cheap Online Diagnostics". Applies WeightWatcher to the canonical trajectory of a grokking transformer and obtains a disagreement in time with the very thing the measure was brought here for: the heavy tail forms at the onset of grokking, not at the late collapse, so the "third phase" sign is no good as a direct determinant of the collapse's onset. Nuance: the anti-grokking regime is not contested — what is contested is the use of $\alpha$ as its detector; the trace is taken as a median over layers on a single seed, with no per-layer breakdown and no across-seed coverage. [`"$\alpha$ falls from $2.07$ at initialization to $1.39$ by epoch 500 (Phase 1 grokking onset) and remains $\lesssim 1.5$ through Phase 5."`](../papers/2605.20441.weight-decay-regimes-in-grokking-transformers-cheap-online-diagnostics/original/2605.20441.weight-decay-regimes-in-grokking-transformers-cheap-online-diagnostics.md#p8-2).\
Also (the caution of the conclusion): [`"We report this as a partial parallel rather than a reproduction."`](../papers/2605.20441.weight-decay-regimes-in-grokking-transformers-cheap-online-diagnostics/original/2605.20441.weight-decay-regimes-in-grokking-transformers-cheap-online-diagnostics.md#p8-2).
## Passing mentions

Works that only mention the phenomenon — a literature review, a related-work paragraph, a passing citation — without examining it.

**\[4.1\]** 2605.06152 — Liu, Cao, Li, Zhou 2026, "Grokking or Glitching? How Low-Precision Drives Slingshot Loss Spikes". Prakash and Martin (2025) are named among the demonstrations of grokking without explicit regularisation. [`"growing empirical evidence shows that grokking can also occur without explicit regularization, although many of these demonstrations are conducted under mean-squared error (MSE) loss Gromov (2023); Kumar et al. (2024); Golechha (2024); Prakash and Martin (2025)"`](../papers/2605.06152.grokking-or-glitching-how-low-precision-drives-slingshot-loss-spikes/original/2605.06152.grokking-or-glitching-how-low-precision-drives-slingshot-loss-spikes.md#p3-1).

**\[4.2\]** 2408.11804 — Yunis et al., "Approaching Deep Learning through the Spectral Dynamics of Weights". Nuance: Martin & Mahoney are cited as empirical support for the line on low-rank properties of weights, but the connection to HTSR is exhausted by the citation — the work computes neither an empirical spectral density, nor a power-law exponent, nor a Marchenko–Pastur edge; the spectrum of the weights is collapsed into the entropy of the singular-value distribution. [`"Numerous studies investigate low-rank biases in various matrices, including the Jacobian (Pennington et al. 2018), weight matrices (Le & Jegelka 2021; Martin & Mahoney 2020; Martin & Mahoney 2021; Frei et al. 2022; Ongie & Willett 2022), Gram matrix (Huh et al. 2022), and features (Yu & Wu 2023; Feng et al. 2022)."`](../papers/2408.11804.approaching-deep-learning-through-the-spectral-dynamics-of-weights/original/2408.11804.approaching-deep-learning-through-the-spectral-dynamics-of-weights.md#p4-2).

**\[4.3\]** 2602.06702 — Singh, Misra, Orvieto, "Explaining Grokking in Transformers…". [`"higher values of weight decay show more heavy-tailed eigenspectra in $Z$"`](../papers/2602.06702.explaining-grokking-in-transformers-through-the-lens-of-inductive-bias/2602.06702.explaining-grokking-in-transformers-through-the-lens-of-inductive-bias.card.md#p7-10). — where $Z$ is the correlation matrix of the pre-logits, not a weight matrix; therein lies the difference from the HTSR line, which the work does not cite.

**\[4.4\]** 2605.08237 — Wang, Ying, Kanamori 2026, "Distributional Spectral Diagnostics for Localizing Grokking Transitions". Nuance: the line closest in intent — "cheap spectral diagnostics without access to the test set" — is mentioned in a single phrase and never set against the residual. [`"Weight-matrix spectra have been studied via random-matrix theory and heavy-tailed self-regularization [30, 25]."`](../papers/2605.08237.distributional-spectral-diagnostics-for-localizing-grokking-transitions/2605.08237.distributional-spectral-diagnostics-for-localizing-grokking-transitions.card.md#p31-2).
