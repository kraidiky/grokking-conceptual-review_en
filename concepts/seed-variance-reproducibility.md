# Seed variance and reproducibility

[Order parameter](order-parameter.md) ← previous card, next → [Heavy-tailed self-regularization (HTSR)](heavy-tailed-self-regularization-htsr.md)

[Concept card index](index.md), category: [6. Analytical tools and metrics](index.md#cat-6)\
→ Next category: [Effective theory and statistical mechanics](effective-theory-statistical-mechanics.md)\
← Previous category: [Grokfast / gradient low-pass filtering](gradient-low-pass-filtering.md)

## Definition

**Seed variance** is the divergence of outcomes between runs that differ only in the random seed (initialisation, data order, split of the sample), and **reproducibility** is the question of what in a report survives a change of that seed. For [grokking](grokking.md) the question is not a housekeeping one: the quantity most works are built around — the [time to grokking](grokking-time.md) — varies at one and the same setting from "grokked early" to "did not grok within the budget", and a single run does not show this: *"single runs lie in this regime, systematically"* \[[1.1](#ref-1-1)\].

A vivid measure of the stakes: at one depth, four out of five seeds grok, one is an order of magnitude late, and one does not grok at all \[[1.2](#ref-1-2)\]. The spread touches not only the timings but also what the network learns: trained on one and the same group, the learned representations do not agree across seeds \[[1.3](#ref-1-3)\].

## Elaboration

The seed in these works changes several things at once — the initial weights, the order in which data is presented, and often the split into training and test as well — so "five seeds" means five draws of the whole task, not five initialisations on fixed data. Hence three different usages of the spread in the corpus.

**As a reported quantity.** The minimal discipline is to report the number of seeds and the spread next to the mean: "to ensure reproducibility", three seeds \[[3.5](#ref-3-5)\], ten seeds per depth \[[3.2](#ref-3-2)\], forty seeds per setting \[[3.1](#ref-3-1)\], the spread over eight runs right in the comparison table \[[3.8](#ref-3-8)\]. Completeness of the report on settings belongs here too, without which someone else's run is unreproducible in principle \[[3.7](#ref-3-7)\]. A separate subtlety is how to compute a mean when some seeds did not grok: runs that never reached the threshold are marked DNF and excluded from the mean delay, which biases it downwards, and the number of such seeds is therefore reported alongside \[[1.2](#ref-1-2)\].

**As a threshold of significance.** The spread turns into a criterion when it is used to decide whether an effect exists. Nudges along the commutator do not accelerate grokking: all 27 runs generalise within times indistinguishable *"within seed-to-seed variability"* \[[3.4](#ref-3-4)\] — a negative result that could not be stated without the spread. The same logic works in the other direction for early signals: a signal is no good if its lead is unstable, with the *"standard deviation exceeding mean lead time"* \[[3.3](#ref-3-3)\].

**As a matter of experimental design.** The strongest form is to make the comparison paired: two arms grow from one and the same state and coincide bit for bit up to the intervention, so that every subsequent difference is attributed to the intervention rather than to the seed \[[2.1](#ref-2-1)\]. The weakest is to report a gain from a single seed: a variant that wins on first touching the threshold groks, at a lower learning rate, in only one seed out of four \[[2.2](#ref-2-2)\].

The spread reaches into the definition of the moment itself: the criterion for detecting grokking demands not only a mean above the threshold but also a small standard deviation within the measurement window \[[3.6](#ref-3-6)\] — that is, stability is built into the definition rather than checked afterwards. A separate question is the numerical environment: part of the spread comes not from the seed but from non-determinism of the computation, and works that achieve bit-for-bit reproducibility separate the one from the other \[[1.1](#ref-1-1)\].

## Alternative definitions and nuances

### A. Spread of timings versus spread of solutions

The first usage is the spread of a measured quantity (the step of grokking, the final accuracy): the seeds give a distribution, and the question is its width and its tails \[[1.2](#ref-1-2)\]. The second is the spread of what is learned: two seeds with the same accuracy implement different representations of one and the same group \[[1.3](#ref-1-3)\]. The distinguishing feature: in the first case averaging makes sense, in the second it destroys the subject — the mean of two incompatible solutions is not a solution, and one has to compare distributions of structures rather than numbers.

### B. Paired comparison versus comparison of means

Here the source of the difference is the design of the experiment, not the statistics. A paired scheme branches two trajectories from one state and therefore excludes the seed as a source of difference by construction \[[2.1](#ref-2-1)\]; a comparison of means requires enough seeds and leaves open whether the difference is explained by a lucky draw. The practical consequence: a claim of acceleration backed by one seed and a claim backed by paired arms are statements of different strength, although both report "it got faster" \[[2.2](#ref-2-2)\].

### C. Spread as noise and spread as subject matter

In most works the spread is an interference to be averaged away. But where the seed changes the split of the sample, it draws the task itself, and the distribution of outcomes becomes the subject: the fraction of seeds that grokked carries more information than the mean time over those that did \[[1.1](#ref-1-1)\]. The control quantity here is the coverage of the training sample and the regularisation, not the optimiser; hence the conclusion that the transition is conditional rather than universal.

### D. Non-determinism of the computation

A separate source of divergence easily confused with the seed: replaying a stored trajectory on an accelerator is not bit-for-bit, and two runs of the same setting diverge without any change of seed. Works that need their arms paired move to the CPU for this, or branch inside a single process \[[2.1](#ref-2-1)\], and works on numerical stability separate the contribution of the environment from that of the initialisation outright \[[1.1](#ref-1-1)\].

## References

###### ref-1-1
**\[1.1\]** 2607.05104 — Ootani, "Grokking Is Conditional and Fragile: A Fully-Tractable, Multi-Seed Study at 12K Parameters". [`"Single runs lie in this regime, systematically."`](../papers/2607.05104.grokking-is-conditional-and-fragile-a-fully-tractable-multi-seed-study-at-12k-parameters/original/2607.05104.grokking-is-conditional-and-fragile-a-fully-tractable-multi-seed-study-at-12k-parameters.md#p11-2).

###### ref-1-2
**\[1.2\]** 2603.25009 — Manir et al., "A Systematic Empirical Study of Grokking: Depth, Architecture, Activation, and Regularization". [`"4 of 5 grokked; one seed exhibited a very late grokking at step 212,000 and one DNF"`](../papers/2603.25009.a-systematic-empirical-study-of-grokking-depth-architecture-activation-and-regularization/2603.25009.a-systematic-empirical-study-of-grokking-depth-architecture-activation-and-regularization.card.md#p6-2).

###### ref-1-3
**\[1.3\]** 2302.03025 — Chughtai et al., "A Toy Model of Universality: Reverse Engineering how Networks Learn Group Operations". [`"Under strong universality, we would expect the representations learned to be consistent across random seeds when trained on the same group. In general, we do not find this to be true"`](../papers/2302.03025.a-toy-model-of-universality-reverse-engineering-how-networks-learn-group-operations/2302.03025.a-toy-model-of-universality-reverse-engineering-how-networks-learn-group-operations.card.md#p7-6).

## References of works that joined the discussion

### Contested

###### ref-2-1
**\[2.1\]** 2608.07436 — Janati et al., "Post-Grokking Collapse at the Representation–Readout Interface in Muon-Trained Transformers". Contests the comparison of means: two arms grow from one state and coincide bit for bit up to the intervention, so the seed is excluded as a source of difference by construction. [`"The two arms are identical before the freeze to a maximum absolute difference of zero across every logged evaluation."`](../papers/2608.07436.post-grokking-collapse-at-the-representation-readout-interface-in-muon-trained-transformers/original/2608.07436.post-grokking-collapse-at-the-representation-readout-interface-in-muon-trained-transformers.md#fig-3).

###### ref-2-2
**\[2.2\]** 2607.20512 — Wang, "The Active Ingredient in Muon's Grokking". Contests a gain reported as a single number: at a lower learning rate the variant groks in only one seed out of four. [`"Spec groks in only 1/4 seeds at $3\!\times\!10^{-4}$"`](../papers/2607.20512.the-active-ingredient-in-muons-grokking/original/2607.20512.the-active-ingredient-in-muons-grokking.md#p6-1).

### In support

###### ref-3-1
**\[3.1\]** 2308.09543 — Hu et al., "Delays, Detours, and Forks in the Road: Latent State Models of Training Dynamics". Nuance: forty seeds are taken not for reporting but to measure the sensitivity of training to randomness itself. [`"we add layer normalization back in and train over 40 random seeds"`](../papers/2308.09543.delays-detours-and-forks-in-the-road-latent-state-models-of-training-dynamics/original/2308.09543.delays-detours-and-forks-in-the-road-latent-state-models-of-training-dynamics.md#p9-1).

###### ref-3-2
**\[3.2\]** 2305.18741 — Murty et al., "Grokking of Hierarchical Structure in Vanilla Transformers". Nuance: ten seeds per depth is the minimal discipline when architectures are compared. [`"we train models with 10 random seeds for 300k (400k for Dyck) steps"`](../papers/2305.18741.grokking-of-hierarchical-structure-in-vanilla-transformers/original/2305.18741.grokking-of-hierarchical-structure-in-vanilla-transformers.md#p2-6).

###### ref-3-3
**\[3.3\]** 2604.20923 — Golwala, "ILDR: Geometric Early Detection of Grokking". Nuance: the spread is turned into a criterion of a signal's fitness — a lead is useless if its deviation exceeds it. [`"proves unstable across seeds with standard deviation exceeding mean lead time"`](../papers/2604.20923.ildr-geometric-early-detection-of-grokking/original/2604.20923.ildr-geometric-early-detection-of-grokking.md#p1-2).

###### ref-3-4
**\[3.4\]** 2602.16746 — Xu, "Low-Dimensional and Transversely Curved Optimization Dynamics in Grokking". Nuance: seed variance serves as a threshold of significance, and the negative result is stated exactly through it. [`"within seed-to-seed variability). This negative result demonstrates that defect accumulation alone is insufficient to induce grokking"`](../papers/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking/original/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking.md#p12-7).

###### ref-3-5
**\[3.5\]** 2310.19470 — Minegishi et al., "Bridging Lottery Ticket and Grokking: Understanding Grokking from Inner Structure of Networks". Nuance: three seeds are named outright as a measure of reproducibility rather than as an averaging. [`"To ensure reproducibility, we conduct experiments with three different seeds"`](../papers/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks/original/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks.md#p20-1).

###### ref-3-6
**\[3.6\]** 2603.24746 — Bi et al., "Grokking as a Falsifiable Finite-Size Transition". Nuance: stability is built into the definition of the moment of grokking itself — the window requires a small deviation, not merely a high mean. [`"require the held-out standard deviation in that window to stay below $0.02$"`](../papers/2603.24746.grokking-as-a-falsifiable-finite-size-transition/2603.24746.grokking-as-a-falsifiable-finite-size-transition.card.md#p8-47).

###### ref-3-7
**\[3.7\]** 2510.04930 — Saheb Pasand et al., "Egalitarian Gradient Descent: A Simple Approach to Accelerated Grokking". Nuance: reproducibility is understood as completeness of the report on low-level settings, not only as a number of seeds. [`"For reproducibility, information about low-level details like learning rate, amount of weight decay"`](../papers/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking/original/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking.md#p9-6).

###### ref-3-8
**\[3.8\]** 2410.03569 — Saxena et al., "Making Hard Problems Easier with Custom Data Distributions and Loss Regularization: A Case Study in Modular Arithmetic". Nuance: the spread is reported next to the mean right in the comparison table — otherwise "better" is indistinguishable from "lucky". [`"We report the *average* $\tau=0.5\%$ accuracy (see §3) and the variance across 8 trials."`](../papers/2410.03569.making-hard-problems-easier-with-custom-data-distributions-and-loss-regularization/original/2410.03569.making-hard-problems-easier-with-custom-data-distributions-and-loss-regularization.md#tab-4).
