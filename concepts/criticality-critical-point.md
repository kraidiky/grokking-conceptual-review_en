# Criticality and the critical point

[Kolmogorov complexity](kolmogorov-complexity.md) ← previous card, next → [Scaling laws](scaling-laws.md)

[Concept card index](index.md), category: [7. Theory and formal results](index.md#cat-7)\
→ Next category: [Grokking](grokking.md)\
← Previous category: [Progress measures](progress-measures.md)

## Definition

**A critical point** in this line is a value of the control parameter near which the training dynamics slow down so much that generalisation arrives with a delay: *"grokking happens near a critical point, similar to “critical slowing down” in the physics literature"* \[[1.1](#ref-1-1)\]. In the solvable setting of binary logistic classification this is proved: the delay arises and grows as the fraction of one class approaches $1/2$, and $\lambda=1/2$ turns out to be exactly the critical point \[[1.2](#ref-1-2)\].

## Elaboration

The notion comes from statistical physics, where near a critical point the relaxation time diverges and the system becomes sensitive to small perturbations. Carrying it over into learning makes [grokking](grokking.md) not an anomaly but expected behaviour: if the trajectory passes near a critical point, a long plateau is the norm, not a riddle.

**How this differs from a [phase transition](phase-transition.md).** A transition is an event (a boundary being crossed); criticality is a property of the neighbourhood: slowing down, diverging scales, heightened sensitivity. A work may observe a transition and claim no criticality; here it is exactly the latter that is claimed, and it is therefore tested by the form of the dependence of time on the distance to the point, not by the mere fact of a jump.

**How general a law this is.** The claim is stated cautiously: the authors write plainly that they cannot show it rigorously, and conjecture that the tie to critical points holds in other settings as well, referring to solvable models where it is shown directly \[[3.1](#ref-3-1)\]. That is, criticality in the corpus is a working hypothesis with one proved case, not an established mechanism of grokking.

**Where criticality is computed.** In solvable models the exponents are not postulated but derived: the transition turns out to be a second-order phase transition with a test-error critical exponent equal to one, while the regularisation parameters change only the prefactor \[[3.3](#ref-3-3)\]. A related picture without the word "criticality" is a metastable regime out of which the trajectory exits, and it is this exit that is seen as generalisation \[[3.4](#ref-3-4)\].

**Neighbouring usages.** The word "critical" in the corpus is also carried by other quantities — above all by the critical sample size, a threshold on data \[[3.2](#ref-3-2)\]. That is not a critical point in the physical sense: there is no claim there of slowing down or divergence, only a boundary between regimes. They are worth telling apart, because their predictions differ: criticality predicts **how** the delay grows as the point is approached, a threshold **where** the boundary runs.

## Alternative definitions and nuances

### A. A critical point of the control parameter

The strict form: the parameter value at which the dynamics slow down and the delay grows \[[1.2](#ref-1-2)\]. The distinguishing feature is provability in a solvable model and a testable form of the dependence; the limitation is that the setting is minimal (binary logistic classification with Gaussian classes), and carrying it over to a transformer remains a conjecture \[[3.1](#ref-3-1)\].

### B. Critical slowing down as an account of the delay

The reading in which a long plateau is not "the network is doing nothing" but "the network is moving through a region where everything is slow". The distinguishing feature against the [hidden progress](sparse-solutions-hidden-progress.md) frame: there, monotone advance towards the solution runs beneath the plateau, whereas here the slowing is a property of the landscape near the point, and what is predicted is not the growth of a measure but a time scale.

### C. "Critical" as a threshold rather than a point

A usage worth keeping separate: the critical sample size \[[3.2](#ref-3-2)\] and thresholds like it mark a boundary between regimes but entail neither slowing down nor divergence. Conflating the two senses gives the false impression that every threshold in the corpus is physically critical.

## References

###### ref-1-1
**\[1.1\]** 2410.04489 — Beck et al., "Grokking at the Edge of Linear Separability". [`"*grokking happens near a critical point*, similar to “critical slowing down” in the physics literature"`](../papers/2410.04489.grokking-at-the-edge-of-linear-separability/2410.04489.grokking-at-the-edge-of-linear-separability.card.md#p2-1).

###### ref-1-2
**\[1.2\]** 2410.04489 — Beck et al., "Grokking at the Edge of Linear Separability". [`"We show that this happens because $\lambda=1/2$ is a *critical point*."`](../papers/2410.04489.grokking-at-the-edge-of-linear-separability/2410.04489.grokking-at-the-edge-of-linear-separability.card.md#p1-9).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2410.04489 — Beck et al., "Grokking at the Edge of Linear Separability". Nuance: the carry-over to other settings is stated as a conjecture, not as a result. [`"While we cannot show it rigorously, we conjecture that grokking is intimately related to such critical points also in different settings."`](../papers/2410.04489.grokking-at-the-edge-of-linear-separability/2410.04489.grokking-at-the-edge-of-linear-separability.card.md#p9-3).

###### ref-3-2
**\[3.2\]** 2401.10463 — Zhu et al., "Critical Data Size of Language Models from a Grokking Perspective". Nuance: the "critical data size" is a threshold between regimes, not a critical point in the physical sense. [`"We explore the critical data size in language models, a threshold that marks a fundamental shift from quick memorization to slow generalization."`](../papers/2401.10463.critical-data-size-of-language-models-from-a-grokking-perspective/2401.10463.critical-data-size-of-language-models-from-a-grokking-perspective.card.md#p1-2).

###### ref-3-3
**\[3.3\]** 2210.15435 — Žunkovič et al., "Grokking phase transitions in learning local rules with gradient descent". Nuance: in a solvable model criticality is not postulated but computed — a second-order transition with a test-error exponent equal to one. [`"Grokking in the considered 1D exponential model is a second-order phase transition with the test-error critical exponent equal to one."`](../papers/2210.15435.grokking-phase-transitions-in-learning-local-rules-with-gradient-descent/2210.15435.grokking-phase-transitions-in-learning-local-rules-with-gradient-descent.card.md#p7-10).

###### ref-3-4
**\[3.4\]** 2602.16746 — Xu, "Low-Dimensional and Transversely Curved Optimization Dynamics in Grokking". Nuance: a related picture without the word "criticality" — the delay as confinement in a metastable regime out of which the trajectory exits. [`"generalization emerges as the trajectory exits this metastable regime"`](../papers/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking/original/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking.md#p3-2).

###### ref-3-5
**\[3.5\]** 2603.24746 — Bi et al., "Grokking as a Falsifiable Finite-Size Transition". Nuance: finite-size scaling is the device by which criticality is told apart from a sharp but ordinary feature of a finite system. [`"finite-size scaling (FSS) provides precisely the sequential diagnostic protocol"`](../papers/2603.24746.grokking-as-a-falsifiable-finite-size-transition/2603.24746.grokking-as-a-falsifiable-finite-size-transition.card.md#p1-4).
