# Ungrokking

[Softmax Collapse](softmax-collapse.md) ← previous card, next → [Anti-grokking / generalisation collapse](anti-grokking.md)

[Concept card index](index.md), category: [1. Phenomena](index.md#cat-1)\
→ Next category: [Structured representation learning](structured-representation-learning.md)\
← Previous category: [Effective theory and statistical mechanics](effective-theory-statistical-mechanics.md)

## Definition

**Ungrokking** is the transition inverse to [grokking](grokking.md): a network that has already reached perfect test accuracy **regresses to low** test accuracy under further training — that is, it returns from generalisation to [memorisation](memorization-phase.md). Predicted and demonstrated by Varma et al. (2023) on the basis of the theory of [circuit efficiency](circuit-efficiency.md) \[[1.1](#ref-1-1)\].

![Ungrokking: a network trained to 100% test accuracy slides back when fine-tuned on a reduced sample (fig. 4 of Varma et al.)](assets/ungrokking-reduced-dataset.png)

## Elaboration

The mechanism is **circuit efficiency** (a circuit being a subnetwork that implements some function). A memorising circuit becomes the **less efficient** the larger the training set, whereas a generalising circuit does not; hence there is a **[critical data size](data-fraction-critical-dataset-size.md)** Dcrit at which the two are equally efficient \[[1.1](#ref-1-1)\]. If a grokked (already generalising) network is trained on further with a set **smaller** than Dcrit, memorisation is again the more efficient, and the network **slides back** to poor test accuracy \[[1.1](#ref-1-1)\]. The mechanism's necessary conditions are **[weight decay](weight-decay.md)** regularisation (an L2 penalty on the weight norms) and a reduced dataset. Right at the threshold (D ≈ Dcrit) the same theory yields a kindred behaviour — **[semi-grokking](semi-grokking.md)**: delayed generalisation not to perfect but merely to **partial** test accuracy.

Appendix A.2 compares the transition point from both sides: a semi-grokking run reaches a test accuracy of $\sim 0.7$ at a set size of $\sim 2000,$ whereas ungrokking runs hold the same accuracy down to $\sim 800$–1000 — less than half \[[1.1](#ref-1-1)\]. A direction-dependent transition point is the definition of hysteresis, the signature of a first-order [phase transition](phase-transition.md). A wiki editor's remark: the authors themselves do not use the word "hysteresis", and the corpus's first-order-transition theories (Rubin et al.; Ersoy & Wiesner, for whom hysteresis is the central mechanism) do not cite this earliest two-sided measurement.

The works that joined the discussion mark out the boundaries of the phenomenon. Huang et al. **reproduce** ungrokking within the circuits-competition frame: when the balance is shifted towards memorisation, the network chooses pure memorisation without generalisation \[[3.1](#ref-3-1)\]. Prakash et al., by contrast, **contest the completeness** of the mechanism: they observe a separate late [collapse of generalisation](anti-grokking.md) — **"anti-grokking"** — on the **original** dataset, **without** weight decay, after very long training (of the order of 10⁷ steps); ungrokking predicts nothing of the sort, since this lies outside its assumptions (a small dataset and weight decay) \[[2.1](#ref-2-1)\].

## Alternative definitions and nuances

### A. Regression to memorisation below Dcrit (Varma)

The canonical reading: ungrokking is the loss of generalisation when a grokked network is trained on further with a dataset smaller than the critical size Dcrit, where the crossover of efficiencies makes memorisation more profitable than generalisation \[[1.1](#ref-1-1)\]. The source of the difference: the control parameter is the **size of the training set**, and the premise is a weight-decay regime.

### B. A kindred behaviour: semi-grokking (at Dcrit)

From the same theory follows not a regression but **partial** generalisation: at D ≈ Dcrit the network groks with a delay but comes out only at **incomplete** test accuracy \[[1.1](#ref-1-1)\]. The source of the difference: this is not a relapse but a **plateau** exactly at the point of equal circuit efficiency.

### Contested

- **"Anti-grokking" outside the conditions of ungrokking** \[[2.1](#ref-2-1)\]: a late collapse of generalisation arises on the original dataset and without weight decay after very long training — that is, beyond the assumptions of circuit-efficiency theory, and it is not predicted by it. The source of the difference: a collapse of generalisation also occurs where the ungrokking mechanism (a small dataset + WD) does not apply.

### In support

- **Reproduction within circuits competition** \[[3.1](#ref-3-1)\]: shifting the efficiency balance towards memorisation makes the model choose pure memorisation without generalisation — a direct agreement with the ungrokking of Varma et al. The source of the difference: the same phenomenon obtained within an independent "circuits competition" frame.

## References

###### ref-1-1
**\[1.1\]** 2309.02390 — Varma et al., "Explaining grokking through circuit efficiency". [`"ungrokking, in which a network regresses from perfect to low test accuracy"`](../papers/2309.02390.explaining-grokking-through-circuit-efficiency/2309.02390.explaining-grokking-through-circuit-efficiency.card.md#p1-3).\
Also (the two-sided measurement, appendix A.2): [`"ungrokking runs that achieve a test accuracy of $\sim$0.7 with a dataset size of around 800–1000, less than half of what the semi-grokking run required"`](../papers/2309.02390.explaining-grokking-through-circuit-efficiency/2309.02390.explaining-grokking-through-circuit-efficiency.card.md#p17-3).\
Also (the mechanism): [`"memorising circuits become more inefficient with larger training datasets while generalising circuits do not, suggesting there is a critical dataset size"`](../papers/2309.02390.explaining-grokking-through-circuit-efficiency/2309.02390.explaining-grokking-through-circuit-efficiency.card.md#p1-3).\
Also (the condition): [`"a model that has successfully grokked returns to poor test accuracy when further trained on a dataset much smaller than"`](../papers/2309.02390.explaining-grokking-through-circuit-efficiency/2309.02390.explaining-grokking-through-circuit-efficiency.card.md#p2-1).

## References of works that joined the discussion

### Contested

###### ref-2-1
**\[2.1\]** 2506.04434 — Prakash & Martin 2025, "Grokking and Generalization Collapse: Insights from HTSR theory". Contests the completeness of the mechanism: the late collapse of generalisation ("anti-grokking") happens outside the conditions of ungrokking. [`"**late-stage generalization collapse** (’anti-grokking’) occurring on the *original* dataset after prolonged training (~$10^{7}$ steps) *without* WD (WD=0)"`](../papers/2506.04434.grokking-and-generalization-collapse-insights-from-htsr-theory/original/2506.04434.grokking-and-generalization-collapse-insights-from-htsr-theory.md#p3-1).\
Also: [`"This distinct phenomenon is not predicted by varma2023explaining as it falls outside of the crucial weight decay assumption on which it relies"`](../papers/2506.04434.grokking-and-generalization-collapse-insights-from-htsr-theory/original/2506.04434.grokking-and-generalization-collapse-insights-from-htsr-theory.md#p3-1).

### In support

###### ref-3-1
**\[3.1\]** 2402.15175 — Huang et al., "Unified View of Grokking, Double Descent and Emergent Abilities: A Perspective from Circuits Competition". Nuance: ungrokking is reproduced within the circuits-competition frame. [`"choose pure memorization without generalization, which is consistent with ungrokking stated by Varma et al. (2023)"`](../papers/2402.15175.unified-view-of-grokking-double-descent-and-emergent-abilities/original/2402.15175.unified-view-of-grokking-double-descent-and-emergent-abilities.md#p2-2).

###### ref-3-2
**\[3.2\]** 2311.18817 — Lyu et al., "Dichotomy of Early and Late Phase Implicit Biases Can Provably Induce Grokking". Nuance: introduces *misgrokking* — a regression of the test curve with the training sample unchanged, produced by a mismatch of the **late** bias with the data, whereas the ungrokking of Varma et al. is caused by shrinking the sample after grokking. Its value for the corpus is an argument against identifying grokking with the acquisition of simplicity: the direction of the transition is set by the agreement of the late bias with the data, not by the simplicity of the solution. [`"the neural net first fits the training set and achieves $100\%$ test accuracy, and then after training for sufficiently longer, the test accuracy drops to nearly $50\%$"`](../papers/2311.18817.dichotomy-of-early-and-late-phase-implicit-biases-can-provably-induce-grokking/original/2311.18817.dichotomy-of-early-and-late-phase-implicit-biases-can-provably-induce-grokking.md#p7-8).\
Also (the mechanism): [`"the early phase implicit bias can make the neural net generalize easily, but the late phase implicit bias can destroy this good generalization since the ground-truth weight vector may not have a large $L^{1}$-margin"`](../papers/2311.18817.dichotomy-of-early-and-late-phase-implicit-biases-can-provably-induce-grokking/original/2311.18817.dichotomy-of-early-and-late-phase-implicit-biases-can-provably-induce-grokking.md#p7-8).

###### ref-3-3
**\[3.3\]** 2506.05718 — Notsawo, Dumas & Rabusseau, "Grokking Beyond the Euclidean Norm of Model Parameters". Nuance: ungrokking becomes controllable without explicit regularisation as well — depth opens the way to it; together with the choice of the regularised property $P$ this widens the set of ungrokking levers beyond shrinking the sample. [`"over-parameterization by adding depth makes it possible to grok or ungrok without explicitly using regularization, which is impossible in shallow cases"`](../papers/2506.05718.grokking-beyond-the-euclidean-norm-of-model-parameters/original/2506.05718.grokking-beyond-the-euclidean-norm-of-model-parameters.md#p1-2).

###### ref-3-4
**\[3.4\]** 2606.26050 — Li, Sreedhar 2026, "Natural Ungrokking: Asymmetric Control of Which Rules Survive Pretraining". A new carrier of the reverse sign — "natural ungrokking": an 11.5M-parameter model, in the middle of ordinary pretraining on stationary web data, learns the pronoun-gender rule ($0.94$ on held-out probes by step 925) and loses it by steps 3,500–4,400 of the same run, while the evidence for it remains in the stream; unlike the ungrokking of Varma et al., where generalisation retreats when the dataset is shrunk BETWEEN runs, the trigger here is the frequency structure of the corpus itself, with no edit to the data; the agreement control stays solved — what is lost is the rule, not the construction. Nuance: the emergence of the rule in mid-run is nowhere shown to be grokking (there is no memorisation phase with failing generalisation) — the root was borrowed for the reverse sign, not for a reverse phenomenon; the claim "no trace in the loss curve" is repeated three times, yet the paper contains no loss curve at all. [`"The model acquired the rule and then stopped applying it (Figure 1a). We call this within-run reversal *natural ungrokking*."`](../papers/2606.26050.natural-ungrokking-asymmetric-control-of-which-rules-survive-pretraining/original/2606.26050.natural-ungrokking-asymmetric-control-of-which-rules-survive-pretraining.md#p1-6).

###### ref-3-6
**\[3.6\]** 2412.----- — Zheng, Daruwalla, Benjamin, Klindt 2024, "Delays in generalization match delayed changes in representational geometry" (UniReps 2024, PMLR 285; the work is not on arXiv). The representational-geometry measures reveal a late corruption of already learned features in networks that do not grok, while the change of the kernel does not show it. The authors relate the observation to the late memorisation of Stephenson et al. and to the misgrokking of Lyu et al. [`"features learned during early training can deteriorate in later epochs"`](../papers/2412.-----.delays-in-generalization-match-delayed-changes-in-representational-geometry/2412.-----.delays-in-generalization-match-delayed-changes-in-representational-geometry.card.md#p7-19).

###### ref-3-5
**\[3.5\]** 2310.13061 — Doshi, Das, He, Gromov 2024, "To grok or not to grok: Disentangling generalization and memorization on corrupted algorithmic datasets". The forgetting phase: under a very large weight decay the accuracy collapses after the network has already generalised, and the cause is a collapse of the weight norms. Nuance: forgetting is met exclusively in networks that have grokked, and it was obtained by the strength of the regularisation rather than by a schedule. [`"we find that the accuracies plummet after the network has generalized!"`](../papers/2310.13061.to-grok-or-not-to-grok-disentangling-generalization-and-memorization-on-corrupted-algorithmic-datasets/original/2310.13061.to-grok-or-not-to-grok-disentangling-generalization-and-memorization-on-corrupted-algorithmic-datasets.md#p5-3).

## Passing mentions

Works that only mention the phenomenon — a literature review, a related-work paragraph, a passing citation — without examining it.

**\[4.1\]** 2405.17479 — Zhou et al., "A rationale from frequency perspective for grokking in training neural network". [`"Varma et al. (2023) explained grokking through circuit efficiency and discovered two novel phenomena called ungrokking and semi-grokking"`](../papers/2405.17479.a-rationale-from-frequency-perspective-for-grokking-in-training-neural-network/2405.17479.a-rationale-from-frequency-perspective-for-grokking-in-training-neural-network.card.md#p2-2).

**\[4.2\]** 2601.19791 — Xu et al., "To Grok Grokking: Provable Grokking in Ridge Regression". [`"Varma et al. (2023) interpreted grokking from the perspective of circuit efficiency, and discovered two related phenomena named “ungrokking” and “semi-grokking”"`](../papers/2601.19791.to-grok-grokking-provable-grokking-in-ridge-regression/original/2601.19791.to-grok-grokking-provable-grokking-in-ridge-regression.md#p3-2).

**\[4.3\]** 2401.10463 — Zhu et al. 2024. Nuance: ungrokking is mentioned only as the content of Varma et al.; the paper runs no fine-tuning of grokked models on smaller sets. [`"And fine-tuning grokked models with smaller data sizes will lead to poor test performance (i.e., ungrokking)."`](../papers/2401.10463.critical-data-size-of-language-models-from-a-grokking-perspective/2401.10463.critical-data-size-of-language-models-from-a-grokking-perspective.card.md#p12-2).
