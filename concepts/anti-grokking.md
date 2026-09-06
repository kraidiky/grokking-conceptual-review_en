# Anti-grokking / generalisation collapse

[Ungrokking](ungrokking.md) ← previous card, next → [Catastrophic forgetting](catastrophic-forgetting.md)

[Concept card index](index.md), category: [1. Phenomena](index.md#cat-1)\
→ Next category: [Structured representation learning](structured-representation-learning.md)\
← Previous category: [Effective theory and statistical mechanics](effective-theory-statistical-mechanics.md)

## Definition

**Anti-grokking, or late-stage generalisation collapse**, is a third phase of grokking: after the network has already grokked, a very long continuation of training makes its test accuracy **collapse** back to a low level while the training accuracy stays saturated. Introduced by Prakash & Martin (2025) — on the original dataset without [weight decay](weight-decay.md) \[[1.1](#ref-1-1)\]\[[1.2](#ref-1-2)\].

![The phases of long training: memorisation and grokking are followed, as optimisation continues, by a late collapse of generalisation — anti-grokking (fig. 1 of Prakash & Martin)](assets/anti-grokking-phases.png)

## Elaboration

Prakash & Martin single out anti-grokking as a previously unreported **third phase** — after memorisation and [grokking](grokking.md): the training accuracy is saturated while the test accuracy collapses \[[1.1](#ref-1-1)\]. The collapse sets in on the **original** dataset, **without** weight decay, after of the order of 10⁷ steps \[[1.2](#ref-1-2)\]. The mechanism is **[correlation traps](correlation-traps.md)** (anomalously large entries of the weight matrices, detected by the spectral metrics of [HTSR](heavy-tailed-self-regularization-htsr.md) / WeightWatcher), which cause [catastrophic forgetting](catastrophic-forgetting.md) \[[1.1](#ref-1-1)\]; weight-decay regularisation suppresses their appearance.

The phenomenon has a forerunner from 2023 in a third regime: Varma et al. saw an unexplained late rise of the test loss in a selected semi-grokking run with weight decay and conjectured a multi-phase dynamics of mixtures of circuits \[[3.3](#ref-3-3)\] — the observation received neither a term nor a systematic treatment.

Hence the key difference from [ungrokking](ungrokking.md): ungrokking is a regression of generalisation when the dataset is reduced *in a weight-decay regime*, whereas anti-grokking arises on the *original* data *without* weight decay and is therefore **not predicted** by the [circuit efficiency](circuit-efficiency.md) theory on which ungrokking is built \[[1.2](#ref-1-2)\].

## Alternative definitions and nuances

### A. A third phase of grokking (WeightWatcher)

A definition as a phase of the dynamics: after grokking comes a late collapse of generalisation, detected by spectral metrics of the weights (correlation traps) \[[1.1](#ref-1-1)\]. The source of the difference: the phenomenon is tied to a phase of training and to spectral anomalies of the weight matrices.

### B. A collapse outside the assumptions of ungrokking (HTSR)

A definition by conditions: a late collapse on the original dataset without weight decay, which the ungrokking mechanism does not cover \[[1.2](#ref-1-2)\]. The source of the difference: independence from a small dataset and from weight decay is what is stressed.

### In support

- **A late regime caught by a spectral metric** \[[3.1](#ref-3-1)\]: anti-grokking as a late collapse of test accuracy (of the order of 10⁷ steps) is recognised by a spectral metric where competing metrics miss it — an independent confirmation that the regime is real. The source of the difference: the phenomenon is singled out by a diagnostic measure of its own.

## References

###### ref-1-1
**\[1.1\]** 2602.02859 — Prakash & Martin, "Late-Stage Generalization Collapse in Grokking: Detecting anti-grokking with WeightWatcher". [`"a previously unreported third phase of grokking in this training regime"`](../papers/2602.02859.late-stage-generalization-collapse-in-grokking-detecting-anti-grokking-with-weightwatcher/original/2602.02859.late-stage-generalization-collapse-in-grokking-detecting-anti-grokking-with-weightwatcher.md#p1-2).\
Also (the substance): [`"a late-stage collapse of generalization"`](../papers/2602.02859.late-stage-generalization-collapse-in-grokking-detecting-anti-grokking-with-weightwatcher/original/2602.02859.late-stage-generalization-collapse-in-grokking-detecting-anti-grokking-with-weightwatcher.md#p1-2).\
Also (the mechanism): [`"Correlation Traps can induce catastrophic forgetting and/or prototype memorization"`](../papers/2602.02859.late-stage-generalization-collapse-in-grokking-detecting-anti-grokking-with-weightwatcher/original/2602.02859.late-stage-generalization-collapse-in-grokking-detecting-anti-grokking-with-weightwatcher.md#p1-5).

###### ref-1-2
**\[1.2\]** 2506.04434 — Prakash & Martin 2025, "Grokking and Generalization Collapse: Insights from HTSR theory". [`"**late-stage generalization collapse** (’anti-grokking’) occurring on the *original* dataset after prolonged training (~$10^{7}$ steps) *without* WD (WD=0)"`](../papers/2506.04434.grokking-and-generalization-collapse-insights-from-htsr-theory/original/2506.04434.grokking-and-generalization-collapse-insights-from-htsr-theory.md#p3-1).\
Also: [`"This distinct phenomenon is not predicted by varma2023explaining as it falls outside of the crucial weight decay assumption on which it relies"`](../papers/2506.04434.grokking-and-generalization-collapse-insights-from-htsr-theory/original/2506.04434.grokking-and-generalization-collapse-insights-from-htsr-theory.md#p3-1).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2604.13123 — Truong et al., "Spectral Entropy Collapse as a Phase Transition in Delayed Generalisation: An Interventional and Predictive Framework for Grokking". Nuance: anti-grokking is confirmed as a late regime caught by a spectral metric. [`"identify an *anti-grokking* regime — a late-stage test-accuracy collapse after $\sim\!10^{7}$ steps — not captured by competing metrics"`](../papers/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation.card.md#p3-5).\
Also (a testable prediction): [`"any rebound of $\tilde{H}$ upward at $\sim\!10^{7}$ steps would be a natural candidate signature of the transition into the anti-grokking regime"`](../papers/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation.card.md#p18-7)


###### ref-3-2
**\[3.2\]** 2605.20441 — Verma 2026, "Weight Decay Regimes in Grokking Transformers: Cheap Online Diagnostics". The first independent observation of a late collapse under conditions opposite to the original ones: not on the original set without weight decay after $\sim\!10^{7}$ steps, but at $\lambda=1.0$ over 20 thousand epochs, and across the retention cohort the collapse thickens at **larger** weight decay. It brings the notion two corrections: the cycle is declared a seed-dependent fragility (retention $5/5$, $4/5$, $3/5$, $4/5$), and the spectral sign of the "third phase" does not agree in time — the heavy tail forms at the onset of grokking. Nuance: there is no mechanism — neither correlation traps nor catastrophic forgetting; the figure with the $\alpha$ trace is built on a single seed, and the across-seed computation is declared deferred outright. [`"confirms the five-stage pattern is a *seed-dependent fragility* rather than a universal cycle"`](../papers/2605.20441.weight-decay-regimes-in-grokking-transformers-cheap-online-diagnostics/original/2605.20441.weight-decay-regimes-in-grokking-transformers-cheap-online-diagnostics.md#p6-3).\
Also (the disagreement in time with Prakash & Martin): [`"Heavy-tail structure therefore *forms during grokking onset, not during late-stage collapse*"`](../papers/2605.20441.weight-decay-regimes-in-grokking-transformers-cheap-online-diagnostics/original/2605.20441.weight-decay-regimes-in-grokking-transformers-cheap-online-diagnostics.md#p8-2).
###### ref-3-3
**\[3.3\]** 2309.02390 — Varma et al. 2023, "Explaining Grokking Through Circuit Efficiency". The earliest observation of the class in the corpus — a forerunner in a different regime rather than a priority claim: in a specially selected single semi-grokking run (D=1532, with weight decay) a late rise of the test loss was seen and left unexplained more than two years before Prakash & Martin named and systematically described the third phase. [`"At epoch $3.2\times 10^{7}$ we see test loss *rise*, we do not know why"`](../papers/2309.02390.explaining-grokking-through-circuit-efficiency/2309.02390.explaining-grokking-through-circuit-efficiency.card.md#fig-6).\
Also (the multi-phase conjecture in the same place): [`"There seem to be multiple phases, perhaps corresponding to the network transitioning between mixtures of multiple circuits with increasing efficiencies, but further investigation is needed"`](../papers/2309.02390.explaining-grokking-through-circuit-efficiency/2309.02390.explaining-grokking-through-circuit-efficiency.card.md#fig-6).

###### ref-3-4
**\[3.4\]** 2605.12394 — Prakash & Martin 2026, "Detecting overfitting in Neural Networks during long-horizon grokking using Random Matrix Theory". The extended version of the instrumental line: the term anti-grokking is presented as their own introduction (direct predecessors with the same experiments are not cited), and its structural difference from pre-grokking — correlation traps in the shuffled weight spectra — is now shown on three settings, including GPT2 on knowledge composition; the appearance of the traps coincides with the minimum of the test loss. [`"Correlation Traps reveal a structural difference between two superficially similar regimes. In both pre-grokking and anti-grokking, training accuracy can be high while test accuracy is poor. But the weight spectra are different"`](../papers/2605.12394.detecting-overfitting-in-neural-networks-during-long-horizon-grokking-using-random-matrix-theory/original/2605.12394.detecting-overfitting-in-neural-networks-during-long-horizon-grokking-using-random-matrix-theory.md#p8-5)..


###### ref-3-5
**\[3.5\]** 2509.21016 — Sun et al. 2025, "RL Grokking Recipe: How Does RL Unlock and Transfer New Algorithms in LLMs?". An observation of quality loss under continued training after convergence, independent of the Prakash–Martin line — in an RL setting: on Manufactoria-REGEX, continuing GRPO training after the curve has levelled off collapses performance ("RL collapse"), whence the conclusion that stabilisation or early stopping is needed. Nuance: a single curve from a single run, with no analysis (neither weight norms nor spectral signs); no parallel with supervised anti-grokking is drawn in the paper. [`"Continued training eventually triggers an *RL collapse*, highlighting the need for stabilization or early stopping once solutions consolidate."`](../papers/2509.21016.rl-grokking-recipe-how-does-rl-unlock-and-transfer-new-algorithms-in-llms/2509.21016.rl-grokking-recipe-how-does-rl-unlock-and-transfer-new-algorithms-in-llms.card.md#p31-2).
###### ref-3-6
**\[3.6\]** 2607.08350 — Pranjić, Roth, Tutschku 2026, "Grokking and epoch-wise double descent in quantum neural networks". A late decline of generalisation in a quantum setting: without an anchor, a noticeable share of runs drift back after the transition to high test error while the training loss stays frozen, and a weak explicit $L_2$ penalty ($\lambda=10^{-4}$) at $n_{l}>4$ brings the final error almost to zero without changing the distribution of $\tau_{\mathrm{g}}/\tau_{\mathrm{f}}$ — the anchor holds the solution once found rather than speeding the search up. Nuance: the abstract's central explanation ("the decline correlates with unbounded growth of the weight norm") has no direct evidence — neither the norm nor the promised Lipschitz bound is measured anywhere, and the only indirect support is that a penalty on the norm removes the decline; entanglement, named as the motivation for the work, is never measured; no connection with ungrokking or circuit competition is drawn, and Omnigrok is not cited. [`"In contrast, the unregularized trajectories display significant variance, with a prominent cluster of runs drifting back to high test error regimes by the end of training."`](../papers/2607.08350.grokking-and-epoch-wise-double-descent-in-quantum-neural-networks/2607.08350.grokking-and-epoch-wise-double-descent-in-quantum-neural-networks.card.md#p16-6).

###### ref-3-7
**\[3.7\]** 2608.07436 — Janati, El Maghraoui, Kanavalau, Belfatmi 2026, "Post-Grokking Collapse at the Representation–Readout Interface in Muon-Trained Transformers". A demarcation of the late failure by what happens to the training accuracy: in anti-grokking it stays perfect while the test accuracy collapses, whereas here both fall within a single interval between measurements ($100\%\to 21.12\%$ and $100\%\to 19.04\%$) and the training loss rises from $1.53\times 10^{-7}$ to $57.5$ — a mechanism acting on generalisation alone would leave the training set solved. Nuance: what does agree is the more important thing — both lines claim that the late collapse escapes the existing progress measures, but they part company on the remedy: there, spectral statistics over the weights are proposed; here, it is shown that the spectrum of the representation is precisely blind to it; the nearest work by subject, 2602.02859, is not cited at all. [`"A mechanism acting on generalization alone would leave the training set solved. This one does not, which points to the interface between the representation and the readout rather than to either alone."`](../papers/2608.07436.post-grokking-collapse-at-the-representation-readout-interface-in-muon-trained-transformers/original/2608.07436.post-grokking-collapse-at-the-representation-readout-interface-in-muon-trained-transformers.md#p3-1).
