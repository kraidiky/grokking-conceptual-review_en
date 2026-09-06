# Quadratic networks

[Scaling laws](scaling-laws.md) ← previous card, next → [Information bottleneck](information-bottleneck.md)

[Concept card index](index.md), category: [7. Theory and formal results](index.md#cat-7)\
→ Next category: [Grokking](grokking.md)\
← Previous category: [Progress measures](progress-measures.md)

## Definition

**Quadratic networks** are two-layer networks with the activation $\sigma(x)=x^2$: *"we train a 2-layer quadratic network… with hidden width $K$, and no bias terms"* \[[1.2](#ref-1-2)\]. In the [grokking](grokking.md) corpus this is not an architecture for practice but a solvable toy: with a quadratic activation *"the full network function takes an even simpler form"* \[[1.1](#ref-1-1)\] — a cubic polynomial in the parameters — and the solution of [modular addition](modular-arithmetic.md) can therefore be written out in closed form rather than recovered by reverse engineering.

## Elaboration

**Why they were needed.** Every theoretical claim about grokking runs into nonlinearity: a ReLU network has no closed-form expressions, an infinitely wide one has no feature learning. A quadratic activation is the smallest departure from linearity at which feature learning is still present and the algebra is still possible. Hence its appearance in three different theoretical lines at once, with different tools and the same role of scaffolding.

**The first line: an analytic solution.** The weights that compute the sum modulo $p$ are written out in formulas — cosines with frequencies $2\pi k/p$ and sets of phases \[[1.1](#ref-1-1)\]. This is the only case in the corpus where the generalising solution is known exactly rather than analysed after the fact; [Fourier features](fourier-features-circuits.md) here are not a find but a consequence of the construction. The price is that the conclusions are tied to MSE, a two-layer MLP and this activation.

**The second line: sample-complexity bounds.** The claim that the task is hard in the [kernel regime](neural-tangent-kernel-ntk.md) is complemented by a positive half: *"two-layer quadratic networks that achieve zero training loss with bounded $\ell_{\infty}$ norm generalize well with substantially fewer training points"*, and such networks are findable by gradient descent with small $\ell_{\infty}$ regularisation \[[1.3](#ref-1-3)\]. Here quadraticity is a condition of the theorem, not a convenience of exposition: it is exactly what allows the set of zero-error solutions to be described.

**The third line: the geometry of the landscape.** [Singular learning theory](singular-learning-theory.md) is applied to grokking on quadratic networks as well — as *"a basin-selection perspective on grokking"*, where the local learning coefficient ranks competing near-zero-loss basins \[[1.4](#ref-1-4)\]. The reason for the choice is the same: for a quadratic network the solution set is a known algebraic variety, and the degeneracy is computed rather than guessed at.

**What this shared ground gives.** Three unconnected frames — an exact solution, a sample-complexity bound, Bayesian geometry — converge on one toy model, and their conclusions are therefore comparable with each other. This is a rare case in the corpus where a divergence of explanations cannot be written off to different settings. The other side is a shared blind spot: everything that depends on depth, softmax loss or attention is absent from these results by construction, and transfer to transformers remains an assumption to be checked separately \[[1.3](#ref-1-3)\].

**A caveat about what they are not.** A quadratic network is neither an approximation of a practical architecture nor a proposal to replace one. The claim "in a quadratic network grokking works thus" says nothing on its own about a ReLU network; transfer requires a separate argument, and in the corpus it is usually given empirically — by reproducing the same phenomenon on an ordinary architecture.

## Alternative definitions and nuances

### A. A solvable model

The form in which quadraticity is needed for the sake of a closed-form solution \[[1.1](#ref-1-1)\]. The distinguishing feature is the kind of knowledge obtained: not an estimate but an identity; hence its special role in disputes — the construction serves as a counterexample showing that a generalising solution exists and is reachable without [regularisation](regularization-necessity.md).

### B. A class for which bounds are provable

The form where quadraticity is a premise of a sample-complexity theorem \[[1.3](#ref-1-3)\]. The source of the difference is that the claim is not about a particular network but about the whole class of zero-error, bounded-norm solutions; the consequence is that the result survives a change of seed and of initialisation, which empirical observations do not guarantee.

### C. The algebraic variety of solutions

The form where the network is taken for the sake of the structure of its solution set \[[1.4](#ref-1-4)\]. The distinguishing feature is that what is studied is not the trajectory but the geometry: the degeneracy of a solution is expressed through the dimension of the intersecting variety, and this is the only one of the three forms where basins, rather than solutions, are compared.

### D. Relation to the other solvable settings

A quadratic network is one of several simplified carriers of grokking, alongside [models outside neural networks](grokking-in-non-neural-models.md); the difference is that here the features are still learned rather than given. That is exactly why the construction \[[1.1](#ref-1-1)\] also serves as a support for later works, in which it turns out to be a special case of a more general scheme \[[3.1](#ref-3-1)\], and why the experimental setting is deliberately cleared of a constant bias, *"forcing the model to learn the task's structure"* \[[3.2](#ref-3-2)\].

## References

###### ref-1-1
**\[1.1\]** 2301.02679 — Gromov, "Grokking modular arithmetic". [`"In passing, we note that, in the case of quadratic activation the full network function takes an even simpler form"`](../papers/2301.02679.grokking-modular-arithmetic/2301.02679.grokking-modular-arithmetic.card.md#p4-3).

###### ref-1-2
**\[1.2\]** 2603.01192 — Cullen et al., "A Basin-Selection Perspective on Grokking via Singular Learning Theory". [`"We train a 2-layer quadratic network $f_{\theta}$ with parameters $\theta=(W,V)$, hidden width $K$, and no bias terms"`](../papers/2603.01192.a-basin-selection-perspective-on-grokking-via-singular-learning-theory/2603.01192.a-basin-selection-perspective-on-grokking-via-singular-learning-theory.card.md#p4-1).

###### ref-1-3
**\[1.3\]** 2407.12332 — Mohamadi et al., "Why Do You Grok? A Theoretical Analysis of Grokking Modular Addition". [`"two-layer quadratic networks that achieve zero training loss with bounded $\ell_{\infty}$ norm generalize well with substantially fewer training points"`](../papers/2407.12332.why-do-you-grok-a-theoretical-analysis-of-grokking-modular-addition/original/2407.12332.why-do-you-grok-a-theoretical-analysis-of-grokking-modular-addition.md#p1-2).

###### ref-1-4
**\[1.4\]** 2603.01192 — Cullen et al., "A Basin-Selection Perspective on Grokking via Singular Learning Theory". [`"we develop a basin-selection perspective on grokking in quadratic networks: LLC ranks competing near-zero-loss basins by statistical preference"`](../papers/2603.01192.a-basin-selection-perspective-on-grokking-via-singular-learning-theory/2603.01192.a-basin-selection-perspective-on-grokking-via-singular-learning-theory.card.md#p1-2).

## References of works that joined the discussion

### In support

###### ref-3-1
**\[3.1\]** 2311.07568 — Morwani et al., "Feature emergence via margin maximization: case studies in algebraic tasks". Nuance: the analytic construction turns out to be a scheme of which the later proofs become a special case. [`"Gromov 2023 provides an analytic construction of various two-layer quadratic networks that can solve the modular addition task."`](../papers/2311.07568.feature-emergence-via-margin-maximization-case-studies-in-algebraic-tasks/2311.07568.feature-emergence-via-margin-maximization-case-studies-in-algebraic-tasks.card.md#p4-1).

###### ref-3-2
**\[3.2\]** 2603.01192 — Cullen et al., "A Basin-Selection Perspective on Grokking via Singular Learning Theory". Nuance: the setting is deliberately cleared of the trivial route to low loss, so that generalisation can only go through learning features. [`"This projection eliminates trivial constant-bias fitting, forcing the model to learn the task’s structure"`](../papers/2603.01192.a-basin-selection-perspective-on-grokking-via-singular-learning-theory/2603.01192.a-basin-selection-perspective-on-grokking-via-singular-learning-theory.card.md#p4-3).
