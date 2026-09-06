# Time to grokking

[Causal ablation and intervention](causal-ablation-intervention.md) ← previous card, next → [Order parameter](order-parameter.md)

[Concept card index](index.md), category: [6. Analytical tools and metrics](index.md#cat-6)\
→ Next category: [Effective theory and statistical mechanics](effective-theory-statistical-mechanics.md)\
← Previous category: [Grokfast / gradient low-pass filtering](gradient-low-pass-filtering.md)

## Definition

**The time to grokking** is the interval between the moment the network has fitted the training sample and the moment it starts to generalise: the very delay by which [grokking](grokking.md) differs from ordinary training. The quantity is operational, and in the corpus it is defined through two thresholds: *"we define $T_{\text{train}}$ as the first step at which training accuracy $\geq 99\%$, and $T_{\text{grok}}$ as the first step at which validation (test) accuracy $\geq 99\%$"*, the grokking delay being $\Delta T=T_{\text{grok}}-T_{\text{train}}$ \[[1.1](#ref-1-1)\]. The phenomenon itself is named in Power et al., where the speed of learning is declared one of the objects of study on small algorithmic datasets \[[1.3](#ref-1-3)\]; the name "time to grokking" settled later, once it began to be proved as a theorem \[[1.4](#ref-1-4)\].

Defining it by a "first step" is not enough: at large learning rates the accuracy oscillates around the threshold, so the second definition accepted in the corpus demands persistence — *"we define the grokking step $t_{\text{grok}}$ as the first training step at which test accuracy exceeds a threshold for $n_{\text{sustained}}=3$ consecutive evaluations"* \[[1.2](#ref-1-2)\]. The difference between "first crossing" and "stable grok" is not cosmetic: it can invert the comparison of two methods \[[2.1](#ref-2-1)\].

## Elaboration

The time to grokking is the only quantity by which the corpus compares interventions: every work promising to "accelerate grokking" promises to shorten exactly this. Hence the three questions the card is built around: how to measure it, what sets it, and in what units it can honestly be reported.

**How to measure it.** The threshold (99%, 98%, 95%), the persistence criterion and the step budget are three knobs, and each changes the number. A setting that did not reach the threshold within the budget is marked "did not grok" and drops out of the averages, which by itself biases the estimate towards speed \[[1.1](#ref-1-1)\]. Works that measure with two measures at once show that the ordering of methods diverges between them \[[2.1](#ref-2-1)\].

**What sets it.** The most developed line of the corpus ties the time to the weight norm: the network first [memorises](memorization-phase.md), raising the norm, and then relaxes under [weight decay](weight-decay.md), and *"the weight norm causally controls the timescale of grokking"* \[[3.1](#ref-3-1)\]. Hence the quantitative form — the delay is the time of exponential contraction of the norm from the memorising solution to the structured one \[[3.2](#ref-3-2)\] — and a direct dose-response test: with the norm clamped, the time grows exponentially in the value held \[[3.3](#ref-3-3)\]. Besides the norm, the time is changed by the training-data fraction, the [learning rate](learning-rate.md), the geometry of the sample itself (a skew of the support vectors carries the hyperplane further from the origin and thereby lengthens the delay \[[3.6](#ref-3-6)\]) and the choice of optimiser.

**In what units.** An optimiser step is not a unit of time. An orthogonalising update costs more than an ordinary one, so an advantage in steps and an advantage in seconds spent are different numbers, and a work reporting only the first overstates the gain \[[2.2](#ref-2-2)\]. For the same reason, counting in FLOPs is coming into use \[[2.1](#ref-2-1)\].

A branch of its own is **predicting the time in advance**: if the network has not grokked yet but a signal has already moved, then the difference between the grokking step and the step at which the signal fires ("lead time") itself becomes a measurable quantity, and the spread of that difference across seeds a measure of the signal's fitness \[[3.8](#ref-3-8)\]. Here the time to grokking meets the [progress measures](progress-measures.md): a signal is worth exactly as much as its lead over $t_{\text{grok}}$ is stable.

In analytically solvable settings the time stops being an empirical quantity and is derived in closed form — from the gradient-flow dynamics of a linear teacher–student model \[[3.4](#ref-3-4)\], or as the distribution of the time to grokking at a [phase transition](phase-transition.md) with critical exponents \[[3.5](#ref-3-5)\]. This makes the notion testable: the predicted dependence can be checked against the one measured on a transformer.

## Alternative definitions and nuances

### A. The difference of two thresholds

The most common form: two steps taken at one and the same accuracy threshold — on training and on test — and their difference $\Delta T=T_{\text{grok}}-T_{\text{train}}$ \[[1.1](#ref-1-1)\]. The control quantity here is the threshold itself: 99% and 95% give different numbers, and at a threshold close to one the tail of slow fine-tuning counts in. The virtue of the form is that it separates the delay from the speed of memorisation: a setting that takes longer to fit the training sample does not thereby look "slower to grok".

### B. Stable grok versus first crossing

The second definition requires the threshold to hold for $n$ consecutive evaluations \[[1.2](#ref-1-2)\]. The source of the difference is the oscillation of accuracy at large learning rates: the trajectory touches the threshold and falls away, and "first crossing" counts a grok where the network has not yet solved the task stably. Works reporting both measures find settings that win on first crossing and lose on stable grok \[[2.1](#ref-2-1)\]; a strict criterion ("no evaluation below the threshold thereafter") also disqualifies runs that touched the threshold and then collapsed \[[2.2](#ref-2-2)\].

### C. The time as an exponent of norm contraction

Here the time is not measured but derived: the order parameter is the weight norm, the control parameter is the [weight decay](weight-decay.md) coefficient, and the delay comes out as the time in which exponential contraction carries the norm from the memorising solution to the structured one \[[3.2](#ref-3-2)\]. The difference from the empirical definitions is that what is predicted is not a single number but the form of the dependence: with the norm clamped, the time grows exponentially in the value held, and this form is separable from a power law and from a saddle-node one \[[3.3](#ref-3-3)\]. The line's caveat: causality is shown by intervening on the norm, not by observing its coincidence with the moment of the grok \[[3.1](#ref-3-1)\].

### D. Closed form in solvable models

In a linear teacher–student model the gradient-flow dynamics is solved analytically, and both losses are expressed through one and the same norm of a matrix difference, so that the delay comes out as a function of the initial conditions rather than as a measurement \[[3.4](#ref-3-4)\]. In solvable models of rule learning the time to grokking turns out to be a random variable with a derivable distribution and critical exponents — this is not a mean time but its law \[[3.5](#ref-3-5)\]. The distinguishing feature: here the time is predicted before the experiment, whereas in the transformer works it is measured afterwards.

### E. The time as a target of intervention

The applied reading: the time to grokking is what gets shortened. Interventions report exactly this — swapping parameters within a layer carries the time from $t\approx 3000$ down to $t\approx 650$ epochs \[[3.7](#ref-3-7)\], and a whole line of works sets shortening the delay as a task in its own right \[[3.9](#ref-3-9)\]. The source of the difference from the other readings is that here the quantity does not describe the phenomenon but serves as an objective; hence the requirement to report it together with the units and with the spread across seeds — otherwise a gain is indistinguishable from a lucky seed \[[2.2](#ref-2-2)\].

## References

###### ref-1-1
**\[1.1\]** 2603.25009 — Manir et al., "A Systematic Empirical Study of Grokking: Depth, Architecture, Activation, and Regularization". [`"We define $T_{\text{train}}$ as the first step at which training accuracy $\geq 99\%$, and $T_{\text{grok}}$ as the first step at which validation (test) accuracy $\geq 99\%$."`](../papers/2603.25009.a-systematic-empirical-study-of-grokking-depth-architecture-activation-and-regularization/2603.25009.a-systematic-empirical-study-of-grokking-depth-architecture-activation-and-regularization.card.md#p3-9).

###### ref-1-2
**\[1.2\]** 2602.16967 — Xu, "Early-Warning Signals of Grokking via Loss-Landscape Geometry". [`"We define the grokking step $t_{\text{grok}}$ as the first training step at which test accuracy exceeds a threshold for $n_{\text{sustained}}=3$ consecutive evaluations"`](../papers/2602.16967.early-warning-signals-of-grokking-via-loss-landscape-geometry/original/2602.16967.early-warning-signals-of-grokking-via-loss-landscape-geometry.md#p7-3).

###### ref-1-3
**\[1.3\]** 2201.02177 — Power et al., "Grokking: Generalization Beyond Overfitting on Small Algorithmic Datasets". [`"generalization, and speed of learning can be studied in great detail"`](../papers/2201.02177.grokking-generalization-beyond-overfitting-on-small-algorithmic-datasets/2201.02177.grokking-generalization-beyond-overfitting-on-small-algorithmic-datasets.card.md#p1-4).

###### ref-1-4
**\[1.4\]** 2601.19791 — Xu et al., "To Grok Grokking: Provable Grokking in Ridge Regression". [`"We prove end-to-end grokking results for learning over-parameterized linear regression models using gradient descent with weight decay."`](../papers/2601.19791.to-grok-grokking-provable-grokking-in-ridge-regression/original/2601.19791.to-grok-grokking-provable-grokking-in-ridge-regression.md#p1-2).

## References of works that joined the discussion

### Contested

###### ref-2-1
**\[2.1\]** 2607.20512 — Wang, "The Active Ingredient in Muon's Grokking". Contests: one measure of time is not enough — the work reports two and adds a count in FLOPs, and the ordering of the variants diverges between the measures. [`"We report first-crossing and stable-grok steps-to-grok at the pre-registered $0.95$ threshold."`](../papers/2607.20512.the-active-ingredient-in-muons-grokking/original/2607.20512.the-active-ingredient-in-muons-grokking.md#p2-4).

###### ref-2-2
**\[2.2\]** 2608.07436 — Janati et al., "Post-Grokking Collapse at the Representation–Readout Interface in Muon-Trained Transformers". Contests: a gain measured in steps does not carry over to time spent. [`"A Muon step costs $1.75$ to $1.80$ times an AdamW step, so the depth-$2$ advantage is $2.22$ in steps and $1.28$ in elapsed time."`](../papers/2608.07436.post-grokking-collapse-at-the-representation-readout-interface-in-muon-trained-transformers/original/2608.07436.post-grokking-collapse-at-the-representation-readout-interface-in-muon-trained-transformers.md#p4-3).

### In support

###### ref-3-1
**\[3.1\]** 2606.13753 — Truong et al., "The Weight Norm Sets the Grokking Timescale: A Causal Delay Law". Nuance: causality is shown by intervening on the norm, not by its value coinciding with the moment of the grok. [`"We show that the weight norm causally controls the *timescale* of grokking"`](../papers/2606.13753.the-weight-norm-sets-the-grokking-timescale-a-causal-delay-law/2606.13753.the-weight-norm-sets-the-grokking-timescale-a-causal-delay-law.card.md#p1-2).

###### ref-3-2
**\[3.2\]** 2603.13331 — Truong et al., "The Norm-Separation Delay Law of Grokking: A First-Principles Theory of Delayed Generalization". Nuance: the delay is derived as a time of norm contraction, not measured. [`"weight decay drives an exponential contraction of parameter norms from the former toward the latter"`](../papers/2603.13331.the-norm-separation-delay-law-of-grokking-a-first-principles-theory-of-delayed-generalization/2603.13331.the-norm-separation-delay-law-of-grokking-a-first-principles-theory-of-delayed-generalization.card.md#p2-3).

###### ref-3-3
**\[3.3\]** 2606.18465 — Truong, "What Does the Weight Norm Control in Grokking? Logit-Scale Mediation under Cross-Entropy". Nuance: the form of the dependence is separated from a power law and from a saddle-node one, that is, it is testable rather than fitted. [`"Across all five moduli the relationship is exponential, $T_{\mathrm{grok}}\propto\exp(\alpha\|W\|)$, with a per-modulus slope $\alpha$."`](../papers/2606.18465.what-does-the-weight-norm-control-in-grokking-logit-scale-mediation-under-cross-entropy/2606.18465.what-does-the-weight-norm-control-in-grokking-logit-scale-mediation-under-cross-entropy.card.md#p3-5).

###### ref-3-4
**\[3.4\]** 2310.16441 — Levi et al., "Grokking in Linear Estimators – A Solvable Model that Groks without Understanding". Nuance: the time comes out as a function of the initial conditions rather than as a measurement. [`"We solve analytically the gradient-flow training dynamics in a linear teacher-student"`](../papers/2310.16441.grokking-in-linear-estimators-a-solvable-model-that-groks-without-understanding/original/2310.16441.grokking-in-linear-estimators-a-solvable-model-that-groks-without-understanding.md#p2-1).

###### ref-3-5
**\[3.5\]** 2210.15435 — Žunkovič et al., "Grokking phase transitions in learning local rules with gradient descent". Nuance: what is predicted is not a mean time but a distribution of times together with critical exponents. [`"find exact analytic expressions for the critical exponents, grokking probability, and grokking time distribution"`](../papers/2210.15435.grokking-phase-transitions-in-learning-local-rules-with-gradient-descent/2210.15435.grokking-phase-transitions-in-learning-local-rules-with-gradient-descent.card.md#p1-2).

###### ref-3-6
**\[3.6\]** 2602.08302 — Das et al., "Grokking in Linear Models for Logistic Regression". Nuance: the time is derived from the geometry of the sample — a skew of the support vectors — rather than from optimisation settings. [`"This increases grokking time as theoretically predicted."`](../papers/2602.08302.grokking-in-linear-models-for-logistic-regression/original/2602.08302.grokking-in-linear-models-for-logistic-regression.md#p6-9).

###### ref-3-7
**\[3.7\]** 2608.01833 — Chan et al., "Tunneling the Loss Landscape: Bypassing Memorization with Monte Carlo Parameter Swapping". Nuance: the time is reported as the outcome of an intervention, while the baseline curve is tuned for the shortest grokking. [`"the swap intervention substantially reduces the grokking time, with models generalizing at approximately $t\approx 650$ epochs compared to $t\approx 3000$ epochs for the AdamW model"`](../papers/2608.01833.tunneling-the-loss-landscape-bypassing-memorization-with-monte-carlo-parameter-swapping/original/2608.01833.tunneling-the-loss-landscape-bypassing-memorization-with-monte-carlo-parameter-swapping.md#p4-9).

###### ref-3-8
**\[3.8\]** 2604.20923 — Golwala, "ILDR: Geometric Early Detection of Grokking". Nuance: the fitness of a signal is measured by the spread of its lead across seeds, not by the fact of a lead. [`"proves unstable across seeds with standard deviation exceeding mean lead time"`](../papers/2604.20923.ildr-geometric-early-detection-of-grokking/original/2604.20923.ildr-geometric-early-detection-of-grokking.md#p1-2).

###### ref-3-9
**\[3.9\]** 2603.05228 — Yildirim, "The Geometric Inductive Bias of Grokking: Bypassing Phase Transitions via Architectural Topology". Nuance: shortening the delay is set as a task in its own right rather than as a by-product. [`"Prior work on grokking—delayed generalization after memorization—has sought to shorten this delay through data augmentation or optimizer design"`](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p1-2).

## Passing mentions

Works that only mention the notion — a literature review, a related-work paragraph, a passing citation — without examining it.

**\[4.1\]** 2210.01117 — Liu et al., "Omnigrok: Grokking Beyond Algorithmic Data". [`"Grokking, the unusual phenomenon for algorithmic datasets where generalization happens long after overfitting the training data, has remained elusive."`](../papers/2210.01117.omnigrok-grokking-beyond-algorithmic-data/original/2210.01117.omnigrok-grokking-beyond-algorithmic-data.md#p1-3).

**\[4.2\]** 2509.10562 — Lopatin et al., "Predator–Prey Model: Driven Hunt for Accelerated Grokking". [`"This number of iterations is strongly influenced by the initial initialization, in particular by the initial weight norm of the model"`](../papers/2509.10562.predator-prey-model-driven-hunt-for-accelerated-grokking/2509.10562.predator-prey-model-driven-hunt-for-accelerated-grokking.card.md#p4-1).

**\[4.3\]** 2602.18523 — Xu, "The Geometry of Multi-Task Grokking: Transverse Instability, Superposition, and Weight Decay Phase Structure". [`"Grokking—the abrupt transition from memorization to generalization long after near-zero training loss—has been extensively studied in single-task settings."`](../papers/2602.18523.the-geometry-of-multi-task-grokking-transverse-instability-superposition-and-weight-decay-phase-structure/original/2602.18523.the-geometry-of-multi-task-grokking-transverse-instability-superposition-and-weight-decay-phase-structure.md#p1-2).
