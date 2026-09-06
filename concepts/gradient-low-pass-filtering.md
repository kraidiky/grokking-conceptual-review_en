# Grokfast / gradient low-pass filtering

— ← previous card, next → [StableMax / perp-Grad (numerical-stability fix)](numerical-stability-fix.md)

[Concept card index](index.md), category: [5. Interventions and methods](index.md#cat-5)\
→ Next category: [Progress measures](progress-measures.md)\
← Previous category: [Weight decay (L2 regularisation)](weight-decay.md)

## Definition

**Grokfast** (gradient low-pass filtering) is a technique for accelerating [grokking](grokking.md) — the delayed generalisation in which a network first memorises the training sample almost perfectly and generalises orders of magnitude of iterations later. The idea of the technique: treat the sequence of each parameter's gradients over training iterations as a time signal, isolate spectrally (through a frequency decomposition) the slowly varying, "generalising" component in it, and amplify that component by adding to the current gradient a copy of itself passed through a low-pass filter (LPF — a filter that passes slow oscillations and suppresses fast ones) \[[1.1](#ref-1-1)\]. The notion was introduced by Lee et al. (Grokfast), who showed that such amplification speeds generalisation up with just "a few lines of code" \[[1.1](#ref-1-1)\].

![The Grokfast scheme: the sequence of a parameter's gradients as a stochastic signal; amplifying its low-frequency component accelerates grokking (fig. 1 of Lee et al.)](assets/grokfast-scheme.png)

## Elaboration

Grokfast's original hypothesis reads gradient descent as signal processing: a parameter's trajectory under gradient descent can be decomposed into a fast-varying component that produces overfitting and a slow-varying one that produces generalisation — and it is the second, low-frequency one, that accounts for the delayed character of the transition \[[1.1](#ref-1-1)\]. Hence the recipe: amplify the low-frequency part of the gradient so that generalisation (see the [memorisation phase](memorization-phase.md), which the technique aims to shorten) comes sooner. Technically this is implemented as an additive filter: to the current parameter update is added a version of the gradient averaged over recent steps. The paper offers two variants of the filter — a moving average (MA) over a fixed window and an exponential moving average (EMA) — controlled by two hyperparameters: the amplification factor and the window size (for EMA, the decay factor). The technique is compatible with ordinary [weight decay](weight-decay.md) (L2 regularisation) and, by the authors' observation, has a synergistic effect with it. In the concept index the same technique also appears under the name "low-pass gradient filter" — it is one and the same family of methods.

Subsequent works accepted the empirical result (manipulating the gradient's spectrum accelerates grokking) but contested the standing of fixed low-pass filtering as the right mechanism. NeuralGrok replaces "strict" low-pass filtering with a learned gradient transformation, pointing to Grokfast's sensitivity to hyperparameters \[[2.1](#ref-2-1)\]. Egalitarian Gradient Descent (EGD) goes further and calls Grokfast "a heuristic frequency filter without guarantees", proposing instead a principled equalisation of [learning rates](learning-rate.md) along the singular directions of the gradient \[[2.2](#ref-2-2)\]. What has formed around the notion, then, is not a line of support but a line of competing replacements: grokking here is still described as an abrupt [phase transition](phase-transition.md), but the dispute is about which operation on the gradient accelerates it.

## Alternative definitions and nuances

### A. An additive low-pass filter on the gradient (the operational reading)

A definition through the operation itself: Grokfast is the addition to the gradient of a copy of itself passed through a low-pass filter — *"amplifying the low-frequencies of the gradients $g(t)$ can be achieved by adding a low-pass filtered signal $g(t)$ to itself"* \[[1.1](#ref-1-1)\]. The distinguishing machinery here is the construction of the filter: it has exactly two scalar hyperparameters (the amplification factor and the window size), and the concrete implementation is a moving average over a queue of fixed capacity, whose mean is the low-frequency component added — *"low-pass filtered gradients which is added to the current parameter update at each optimizer step"* \[[1.1](#ref-1-1)\]. On this reading, the notion is defined by WHAT the [optimiser](optimizer-adam-adamw-sgd.md) does to the gradient signal, not by why it works.

### B. Splitting the trajectory into an overfitting and a generalising component (the spectral reading)

A definition through a causal hypothesis: the parameter trajectory decomposes into two frequency components — a fast (overfitting) one and a slow (generalising) one — and delayed generalisation is a consequence of exactly the slow, low-frequency component of the updates \[[1.1](#ref-1-1)\]. The difference from reading A is that the source of the difference lies not in the construction of the filter but in the spectral model of the gradient signal: the technique is defined by WHICH of the two spectral components it amplifies, and why amplifying the low-frequency part accelerates the transition. Reading A is the way it is implemented; reading B is the justification for the choice of component.

### Contested

Two works contest the standing of fixed low-pass filtering as the right or sufficient mechanism of acceleration, while keeping the broader thesis about manipulating the gradient. NeuralGrok abandons "strict" low-pass filtering in favour of a learned bilevel transformation of the gradient and points out that the windowed variant of Grokfast is sensitive to hyperparameter tuning and depends on the task \[[2.1](#ref-2-1)\]. EGD characterises Grokfast as "a heuristic frequency filter without such guarantees" and proposes instead an equalisation of convergence speeds along the principal (singular) directions of the gradient, which, unlike Grokfast's buffering window, does not require storing a large buffer of past updates \[[2.2](#ref-2-2)\]. Both objections are aimed not at the fact (spectral manipulation accelerates grokking) but at the particular form — a fixed low-pass filter.

## References

###### ref-1-1
**\[1.1\]** 2405.20233 — Lee et al., "Grokfast: Accelerated Grokking by Amplifying Slow Gradients". [`"Amplifying the low-frequencies of the gradients g(t) can be achieved by adding a low-pass filtered signal g(t) to itself."`](../papers/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients.card.md#p3-1).\
Also (the hypothesis): [`"the delayed generalization of grokking is a consequence of the slow-varying component of the parameter updates"`](../papers/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients.card.md#p2-5);\
Also (the implementation): [`"low-pass filtered gradients which is added to the current parameter update at each optimizer step"`](../papers/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients.card.md#p3-10);\
Also (the acceleration): [`"lines of code that amplifies the slow-varying components of gradients"`](../papers/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients.card.md#p1-2).

## References of works that joined the discussion

### Contested

###### ref-2-1
**\[2.1\]** 2504.17243 — Zhou et al., "NeuralGrok: Accelerate Grokking by Neural Gradient Transformation". Contests: instead of strict low-pass filtering, a learned gradient transformation. [`"Instead of strict low-pass filtering, we propose NEURALGROK"`](../papers/2504.17243.neuralgrok-accelerate-grokking-by-neural-gradient-transformation/original/2504.17243.neuralgrok-accelerate-grokking-by-neural-gradient-transformation.md#p1-4).\
Also (what Grokfast does): [`"Lee et al. (2024) demonstrated that by amplifying the low-frequency component of the gradient by a low-pass filter (LPF), the generalization can be greatly accelerated"`](../papers/2504.17243.neuralgrok-accelerate-grokking-by-neural-gradient-transformation/original/2504.17243.neuralgrok-accelerate-grokking-by-neural-gradient-transformation.md#p1-3);\
Also (the complaint): [`"GROKFAST-MA is quite sensitive to hyperparameter settings, which can be task-dependent."`](../papers/2504.17243.neuralgrok-accelerate-grokking-by-neural-gradient-transformation/original/2504.17243.neuralgrok-accelerate-grokking-by-neural-gradient-transformation.md#p4-2)

###### ref-2-2
**\[2.2\]** 2510.04930 — Saheb Pasand et al., "Egalitarian Gradient Descent: A Simple Approach to Accelerated Grokking". Contests: Grokfast is a heuristic filter without guarantees; the principled alternative is equalising the speeds along the singular directions. [`"Grokfast is a heuristic frequency filter without such guarantees"`](../papers/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking/original/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking.md#p8-9).\
Also (what Grokfast does): [`"Grokfast amplifies slow (low-frequency) gradient components via simple optimizer-side filters, consistently accelerating grokking across tasks and architectures"`](../papers/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking/original/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking.md#p4-2);\
Also (the difference): [`"unlike Grokfast, EGD equalizes the optimization speed across principal directions"`](../papers/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking/original/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking.md#p8-8).


###### ref-2-3
**\[2.3\]** 2506.12284 — Walker et al., "GrokAlign: Geometric Characterisation and Acceleration of Grokking". Puts Grokfast into a direct comparison over ten seeds on the MNIST setup of Liu et al. and obtains a negative result: under cross-entropy Grokfast is slightly slower than the baseline run (↑1.01× in steps, ↑1.03× in time), and under mean-squared error it gives ↓1.08× against GrokAlign's ↓1.69×. Nuance: Grokfast's settings are not named at all — neither α, nor λ, nor the choice between EMA and MA — so from what is published one cannot tell a defeat of the technique from a defeat of its tuning; the baseline row of the table is empty, and there are no absolute times. [`"Grokfast provides a relatively lower improvement in the mean-squared error case and is ineffective in the cross-entropy case"`](../papers/2506.12284.grokalign-geometric-characterisation-and-acceleration-of-grokking/original/2506.12284.grokalign-geometric-characterisation-and-acceleration-of-grokking.md#p9-3).\
Also (how the technique is described): [`"Grokfast [32] works to improve the rate of grokking by manipulating the gradients during training to amplify certain signals."`](../papers/2506.12284.grokalign-geometric-characterisation-and-acceleration-of-grokking/original/2506.12284.grokalign-geometric-characterisation-and-acceleration-of-grokking.md#p9-2)

###### ref-2-4
**\[2.4\]** 2604.20923 — Golwala, "ILDR: Geometric Early Detection of Grokking". Contests the fitness of the slow gradient as a signal, but tests it in a passive mode: [`"the amplification step is removed so that training remains unchanged across all conditions"`](../papers/2604.20923.ildr-geometric-early-detection-of-grokking/original/2604.20923.ildr-geometric-early-detection-of-grokking.md#p2-5). [`"On seeds $0, 1,$ and $42$ it leads by $\sim 2000$ steps and on seeds $2, 3, 777,$ and $9999$ it lags by $4000\text{--}6500$ steps."`](../papers/2604.20923.ildr-geometric-early-detection-of-grokking/original/2604.20923.ildr-geometric-early-detection-of-grokking.md#p7-5).\
Also (the dependence on depth): the lag shrinks with depth — 13600, 4900 and 1000 steps at 1, 2 and 4 layers ([p. 9, para. 4](../papers/2604.20923.ildr-geometric-early-detection-of-grokking/original/2604.20923.ildr-geometric-early-detection-of-grokking.md#p9-4)), whence the author concludes that the signal catches a property of the model rather than of the task.\
Also (a misattribution): the work attributes Grokfast to "Liu, Y., et al." in the text, in the caption of the measure and in the bibliography; examined in the "Common misreadings and overstatements" section of that card, anchor `mc-2405-20233`.
### Stepping outside

###### ref-4-1
**\[4.1\]** 2509.10562 — Lopatin, Kozyrev & Pechen 2025, "Predator–Prey Model: Driven Hunt for Accelerated Grokking". A third member of the line of grokking accelerators: as in Grokfast and NeuralGrok, the correction is inserted between computing the gradient and taking the step, but the source is different — an external drift from a second copy of the parameter vector, computed with no gradient at all, so that an iteration is no more expensive than the baseline. Neither Grokfast nor NeuralGrok is cited; the untested alternative shared with Grokfast — an ablation against a simple amplification of momentum — is missing here as well. [`"one epoch of training in the graphs in Fig. 2 contains the same number of gradient calls as one epoch in the graphs in Fig. 1"`](../papers/2509.10562.predator-prey-model-driven-hunt-for-accelerated-grokking/2509.10562.predator-prey-model-driven-hunt-for-accelerated-grokking.card.md#p7-1)..

## Passing mentions

Works that only mention the phenomenon — a literature review, a related-work paragraph, a passing citation — without examining it.

**\[4.1\]** 2504.13292 — Xu et al., "Let Me Grok For You: Accelerating Grokking". [`"Lee et al. (2024) proposed a gradient amplification algorithm GrokFast to accelerate grokking."`](../papers/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model/original/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model.md#p10-2).

**\[4.2\]** 2506.05718 — Notsawo et al., "Grokking Beyond the Euclidean Norm of Model Parameters". [`"Lee et al. (2024) accelerate grokking by amplifying slow gradient components, reducing training time across tasks."`](../papers/2506.05718.grokking-beyond-the-euclidean-norm-of-model-parameters/original/2506.05718.grokking-beyond-the-euclidean-norm-of-model-parameters.md#p17-4).

**\[4.3\]** 2603.01968 — Hwang et al., "Intrinsic Task Symmetry Drives Generalization in Algorithmic Tasks". [`"optimization techniques like GrokFast that amplify slow-varying gradients (Lee et al., 2024)"`](../papers/2603.01968.intrinsic-task-symmetry-drives-generalization-in-algorithmic-tasks/original/2603.01968.intrinsic-task-symmetry-drives-generalization-in-algorithmic-tasks.md#p2-6).

**\[4.4\]** 2603.05228 — Yildirim, "The Geometric Inductive Bias of Grokking". [`"via gradient low-pass filtering—is complementary but operates within the memorize-then-generalize paradigm"`](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p4-1).

**\[4.5\]** 2603.24746 — Bi et al., "Grokking as a Falsifiable Finite-Size Transition". [`"Lee et al. [28] accelerate the phenomenon by amplifying slow gradients"`](../papers/2603.24746.grokking-as-a-falsifiable-finite-size-transition/2603.24746.grokking-as-a-falsifiable-finite-size-transition.card.md#p12-2).

**\[4.6\]** 2604.13123 — Truong Xuan Khanh et al., "Spectral Entropy Collapse as a Phase Transition in Delayed Generalisation". [`"Lee et al. (2024) showed that amplifying slow gradient components accelerates grokking"`](../papers/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation.card.md#p2-5)

**\[4.7\]** 2606.12966 — Sivasankar, "Circuit Synchronization Precedes Generalization: A Causal Precursor to Grokking". [`"Lee et al. 2024 amplify slow-varying gradient components; our intervention is complementary"`](../papers/2606.12966.circuit-synchronization-precedes-generalization-a-causal-precursor-to-grokking/2606.12966.circuit-synchronization-precedes-generalization-a-causal-precursor-to-grokking.card.md#p16-4).
