# Global Grokking Concept Index

Built by inverting the per-paper extractions into a "concept -> papers" index over 66 arXiv papers on grokking (originally from the txt extractions of the repository the wiki was split out of; they are not stored here). Every link is quote-anchored: an exact English fragment of the original, tied to the stored text of the paper in `papers/<folder>/original/` by a paragraph anchor, and for headings and formulas by a link to the file. Synonymous labels (e.g. frequency-principle / spectral-bias; lazy-to-rich / kernel-to-feature-learning; anti-grokking / generalization-collapse; weight-norm-minimization / zero-loss-manifold) are reduced to a single canonical concept, with the merged aliases given in brackets.

The link format: `arxivid: ["verbatim English quote"](../papers/<folder>/original/<file>.md#anchor)` — the quotes are given verbatim, in English, in the serialisation of the stored original; do not alter them. Verbatimness is checked by quote_check.py.

###### cat-1

## 1. Phenomena

### [Grokking / delayed generalization](grokking.md) — 162 papers

The phenomenon of delayed generalisation: a network first fits the training sample almost perfectly at a low test accuracy, and after orders of magnitude more training the test accuracy rises abruptly. The term and the phenomenon were introduced by Power et al. (2022).

### [Memorization phase / plateau](memorization-phase.md) — 81 papers

The initial stage of training under grokking: an almost perfect accuracy on the training sample at a low test one — a protracted plateau preceding the abrupt transition to generalisation.

### [Phase transition](phase-transition.md) — 66 papers

A reading of delayed generalisation as an abrupt change of regime on the pattern of phase transitions in physics: a long low plateau of test accuracy and a sudden jump.

### [Slingshot effect / mechanism](slingshot.md) — 30 papers

An optimisation anomaly of adaptive optimizers at late stages of training: cycles of a rapid growth of the last layer's weight norm, a spike of the training loss and a shelf of the norm. It often accompanies grokking without explicit regularisation.

### [Emergence / emergent abilities](emergence.md) — 29 papers

The abrupt appearance of qualitatively new capabilities on crossing a critical threshold of scale — the number of parameters, of data or of compute. In the grokking literature it is the same abruptness, but governed by training time.


### [Double descent](double-descent.md) — 27 papers

The non-monotonicity of the test error: a fall, a rise to a peak near the interpolation point and a second fall in the overfitted region. It shares with grokking the question of why overfitting turns out to be an intermediate stage rather than the end.


### [Softmax Collapse](softmax-collapse.md) — 11 papers

A numerical instability: without regularisation, training pushes the model to the edge of numerical stability, floating-point errors in the softmax halt the training and prevent grokking. Introduced by Prieto et al. (2025).

### [Ungrokking](ungrokking.md) — 11 papers

The transition inverse to grokking: a network that has already reached a perfect test accuracy regresses to a low one under further training — from generalisation back to memorisation. Predicted by the theory of circuit efficiency (Varma et al., 2023).


### [Anti-grokking / generalization collapse](anti-grokking.md) — 9 papers
Merged aliases: anti-grokking / generalization-collapse.

A third phase after grokking: under a very long continuation of training the test accuracy collapses back to a low value while the training accuracy stays saturated. Introduced by Prakash & Martin (2025).

### [Catastrophic forgetting](catastrophic-forgetting.md) — 9 papers

An abrupt loss of what was learned earlier when training continues on new data or a changed distribution; in the context of grokking, an explanation of the loss of a generalising solution already attained.

### [Semi-grokking](semi-grokking.md) — 6 papers

Delayed generalisation only to a partial test accuracy: the network groks but comes out at an incomplete quality. Discovered by Varma et al. (2023) as a consequence of the same theory of circuit efficiency.

### [Behavioral vs true grokking](behavioral-vs-true-grokking.md) — 4 papers

What is to count as grokking: a jump in accuracy, or a jump together with the assembly of a generalising mechanism. The distinction is measurable — the rearrangement of the circuit continues for thousands of steps after the curve has already recorded the transition.

### [Comprehension / grokking / memorization / confusion](comprehension-confusion-phases.md) — 3 papers

A partition of the plane of settings into four regions by the relation between the times at which the two curves reach a threshold. Not to be confused with the three-part partition of training time: there the phases follow one another over the course of a run, here they are regions in the space of settings.

### [Naive Loss Minimization](nlm.md) — 2 papers

The component of the gradient that lowers the cross-entropy by simply scaling the logits upwards without changing the predictions; past the point of overfitting the gradient goes almost entirely into it, postponing generalisation.

###### cat-2

## 2. Mechanisms and representations

### [Structured representation learning](structured-representation-learning.md) — 53 papers

An explanation of grokking: generalisation arises from the gradual formation of structured internal representations encoding the make-up of the task, rather than from the memorisation of examples as such.

### [Fourier features / circuits](fourier-features-circuits.md) — 50 papers

Periodic representations of the inputs on a few key frequencies, and subnetworks that add numbers through trigonometric identities — the language for describing solutions of modular arithmetic, coming from the analysis of Nanda et al.


### [Feature emergence / feature learning](feature-emergence-feature-learning.md) — 38 papers

The appearance during training of features that encode the make-up of the task; generalisation coincides with the emergence of structure in the embeddings, which builds up throughout the plateau.

### [Lazy-to-rich / kernel-to-feature-learning transition](lazy-to-rich-kernel-to-feature-learning.md) — 33 papers
Merged aliases: lazy-to-rich / kernel-to-feature-learning / lazy-learning-stage / lazy-rich-regime-transition.

A reading of grokking as a change of regimes: first "lazy" training near the initialization (kernel regression with the NTK, memorisation), then a passage into the "rich" regime of feature learning, which yields generalisation.

### [Loss landscape / basins](loss-landscape-basins.md) — 32 papers

The geometry of the loss function over weight space: delayed generalisation is described as a movement of the optimisation trajectory between basins — out of a memorising minimum into a generalising one.


### [Circuit efficiency](circuit-efficiency.md) — 29 papers

The property of a circuit of producing the required logits at a smaller parameter norm; when several circuits solve the training sample equally well, weight decay selects the more efficient one. The basis of Varma et al.'s explanations of grokking, ungrokking and semi-grokking.


### [Sparse subnetwork / lottery ticket](sparse-subnetwork-lottery-ticket.md) — 26 papers

Links grokking to the isolation, inside a dense network, of a small sparse subnetwork that implements the generalising algorithm and displaces the dense memorising one.

### [Manifold / representation compression](manifold-representation-compression.md) — 25 papers

A reading in which generalisation sets in once the representations or the weight trajectory contract from an inflated memorising configuration into a compact low-dimensional manifold.

### [Neural tangent kernel, NTK](neural-tangent-kernel-ntk.md) — 22 papers
Merged aliases: neural-tangent-kernel / NTK-task-kernel-alignment.

The kernel to which the training of a network reduces in the lazy (linearised) regime; in the theory of grokking it sets the initial memorising phase, out of which the network moves as it passes to feature learning.

### [Attention routing / heads](attention-routing-heads.md) — 18 papers

The redistribution of information between the positions of a sequence by attention heads through learned "query-key" interactions; in analyses of grokking, the place where the learned algorithm is read off.

### [Group representations / cosets](group-representations-cosets.md) — 14 papers

The language of the representation theory of groups for describing the solution a network has found: after grokking the network implements a structure dictated by the representations of the group rather than an arbitrary fit.

### [Neural collapse](neural-collapse.md) — 13 papers

A structural phenomenon of the final phase of training: the class representations in the penultimate layer contract to the class means, arranged in a simplex equiangular tight frame (ETF); in the corpus, a lens on the late stages of grokking.

### [Clock vs Pizza](clock-vs-pizza.md) — 9 papers

Two qualitatively different internal circuits to which a network converges on modular addition — the "Clock" and the "Pizza"; the distinction was introduced by Zhong et al. as evidence of the non-uniqueness of the learned algorithm.

### [Intrinsic task symmetry](intrinsic-task-symmetry.md) — 9 papers

The invariance of the generating rule under a transformation of the input — commutativity, associativity, transitivity — declared the cause of generalisation rather than its companion. The other side of it: the same symmetry forbids generalisation in the kernel regime.

### [Frequency principle / spectral bias](frequency-principle-spectral-bias.md) — 7 papers
Merged aliases: frequency-principle / spectral-bias / F-Principle / frequency-perspective.

The implicit inductive bias of neural networks to fit the target function "from low frequencies to high ones": the slowly varying components are learned first, the high-frequency details substantially later.

### [Orthogonal gradient / perp-Grad](orthogonal-gradient-perp-grad.md) — 7 papers
Merged aliases: gradient-orthogonality / orthogonal-gradient-flow / perp-Grad.

The component of the gradient orthogonal to the direction of the weights or to the zero-loss manifold — the part of the updates that actually changes the predictions; the device of the same name (perp-Grad) keeps only that part.

### [Universality hypothesis](universality-hypothesis.md) — 6 papers

Networks trained on similar tasks arrive at a similar make-up — an assumption without which the analysis of one grokked network says nothing about the next. At the level of neurons it has been refuted; at the level of an abstract algorithm it has been claimed anew. The homonym from physics — a universality class — has nothing to do with it.

### [Approximate Chinese Remainder Theorem, aCRT](approximate-chinese-remainder-theorem.md) — 4 papers

An abstract description of what a network computes once it has grokked modular arithmetic: a decomposition into subsystems by residues with an intersection of the answers. It rests on a weakened notion of a coset — proximity in the Cayley graph instead of an exact division of the modulus.

### [Generalization circuit](generalization-circuit.md) — 4 papers

The part of the network implementing the generalising solution, against the memorising circuit. The distinction is operational through a pair of progress measures, and the boundary between the circuits acquires a number — the critical dataset size.

### [Model complexity / error tradeoff](model-complexity-error-tradeoff.md) — 4 papers

A trade-off between the complexity of the learned function and the error: the network attains a zero error with a complex solution and then moves to a simple one with the same error. The weak spot of the frame is named within it — there is no single measure of complexity.

### [Sparse solutions / hidden progress](sparse-solutions-hidden-progress.md) — 4 papers

A monotone advance inside the network beneath an outward plateau, and the sparsity of the solution it leads to. Hence the idea of hidden progress measures: a quantity that grows during the plateau and predicts the jump.

### [Activation and structural sparsity](activation-sparsity.md) — 3 papers

Three different observations under one name: sparsity in the Fourier domain, in the structure of the subnetwork and in the response. The test of the hypothesis is set up honestly — models with the same sparsity are built separately.

### [Execution manifold](execution-manifold.md) — 3 papers

A low-dimensional surface in weight space on which the training trajectory is held: the first principal component takes 68–83% of the variance. The delay is being held on it, the generalisation is leaving it.

### [Polysemanticity / superposition](polysemanticity-superposition.md) — 3 papers

A neuron that responds to several unrelated features, and the explanation of this through a superposition of more features than there are directions. It bears on every instrument for analysing grokked networks that assumes one notion per direction.

###### cat-3

## 3. Tasks and datasets

### [Modular arithmetic](modular-arithmetic.md) — 78 papers

The class of tasks of the form (a ∘ b) mod p on which grokking was first observed and which became its canonical testbed; division requires a prime modulus — it is defined as the inverse of multiplication and is unique only for prime p.


### [Canonical grokking testbed / Power et al. setup](canonical-grokking-testbed.md) — 51 papers

The experimental setting of Power et al. (2022) — tables of binary operations, a small transformer, the data fraction as the control parameter — inherited by most works of the corpus as the standard ground.

### [Vision / real-world data: MNIST, CIFAR, ...](vision-real-world-data-mnist-cifar.md) — 34 papers

A collective notion for observations of grokking beyond synthetic algorithmic tasks — on image classification (MNIST, CIFAR, ImageNet), on text and on molecules.

### [Sparse parity](sparse-parity.md) — 23 papers

A synthetic binary classification task: the label is the parity (XOR) of k hidden bits from a fixed secret subset of an n-bit string, with k much smaller than n; one of the canonical testbeds of grokking.

### [Label noise / random labels; in Power et al. — outliers](label-noise-random-labels.md) — 21 papers

A deliberate replacement of the true training labels by random ones — for some of the examples or for all of them; brought into the corpus by Power et al. as "outliers", whose number measures the influence of noise on the onset of generalisation.

### [Group composition, non-commutative, S5](group-composition-non-commutative-s5.md) — 16 papers

Tasks of predicting the result of a group operation from a pair of elements; the key watershed is commutativity: non-commutative groups such as S5 behave differently from modular arithmetic.

### [Reasoning / knowledge graphs](reasoning-knowledge-graphs.md) — 5 papers

The link established by Wang et al. (2024) between grokking and a transformer's capacity for implicit reasoning over parametric knowledge represented as a knowledge graph: inferring new facts without explicit intermediate steps.

### [Grokking in non-neural and solvable models](grokking-in-non-neural-models.md) — 4 papers

Delayed generalisation in models that are not deep networks, or that are linear and therefore solvable analytically: ridge and logistic regression, a linear teacher-student, the Ising model. Their value is rigorous definitions of the memorising and the generalising solution.

### [Distribution shift](distribution-shift.md) — 2 papers

A divergence between the training and the validation distribution: both an explanation of the delay (the sparsity of the data produces the shift) and the condition under which a grokked model is tested for robustness.

### [Systematic / hierarchical generalization](systematic-generalization.md) — 2 papers

Generalisation to structurally novel inputs, where the training sample is explained equally well by two rules and the test sample tells them apart. Hence structural grokking and its non-monotone dependence on depth.

###### cat-4

## 4. Training and optimisation factors

### [Weight decay](weight-decay.md) — 100 papers

A penalty proportional to the square of the L2 norm of the weights (equivalent to a component-wise decay of the weights at every step); the corpus's main regulariser — both the speed and the very onset of grokking are tied to it in most settings.


### [Data fraction / critical dataset size](data-fraction-critical-dataset-size.md) — 64 papers

A threshold in the volume of the training sample separating two regimes: above it the network eventually generalises, below it it stays at memorisation; conveniently expressed as a fraction of all the admissible examples of the task.

### [Optimizer: Adam / AdamW / SGD](optimizer-adam-adamw-sgd.md) — 54 papers

The algorithm that updates the weights from the gradients; in the corpus the choice of optimizer is a substantive factor: Power et al. already showed that the details of the optimisation affect the very onset of delayed generalisation.

### [Weight-norm minimization / zero-loss manifold](weight-norm-minimization.md) — 45 papers
Merged aliases: weight-norm minimization / norm minimization on the zero-loss manifold.

A reading of grokking as a movement along the zero-loss manifold towards a solution of smaller weight norm: once the memorisation is complete, training slowly slides towards a generalising configuration of minimal norm.

### [Initialization scale](initialization-scale.md) — 41 papers

The initial weight norm of a network, set by a factor applied to the standard scheme; Omnigrok established that a large initialization scale induces grokking and a small one removes it.

### [Regularization necessity](regularization-necessity.md) — 34 papers

An open dispute of the corpus: whether regularisation is a necessary condition of grokking; directly opposite experimental answers have been collected, each honestly obtained in its own setting.

### [Learning rate](learning-rate.md) — 30 papers

The scale of the weight update step; one of the control parameters — alongside weight decay, the batch size and the data fraction — on which it depends whether delayed generalisation sets in, and how fast.

### [Regularization variants](regularization-variants.md) — 26 papers

A family of regularisation devices other than the canonical weight decay which also induce or accelerate the delayed transition to generalisation.

### [Goldilocks zone](goldilocks-zone.md) — 22 papers

A narrow, "just right" region of parameters inside which — and only inside which — substantive representation learning happens; introduced by Liu et al. (2022) with reference to grokking.

### [Gradient noise / full-batch training](gradient-noise.md) — 19 papers

The question of whether grokking needs stochastic optimisation noise (mini-batch SGD noise, injected Gaussian noise, the "temperature" lr/B); the line of the corpus where the noise hypothesis of Power et al. and the full-batch experiments are set against one another.

### [Edge of stability](edge-of-stability.md) — 11 papers

A regime of gradient descent in which the sharpness of the landscape (the largest eigenvalue of the Hessian) grows, through progressive sharpening, up to the stability threshold 2/η and is held around it.

### [Selective / layerwise weight decay](selective-weight-decay.md) — 11 papers

A weight decay applied not to all the parameters: the embeddings, the biases and the normalisation gains are usually taken out from under the penalty, though the converse also occurs — a decay on the layernorm scales. The layer-wise form ceases to be a detail of the experiment: a penalty on the factorisation factors equals the nuclear norm of the product, and the depth sets the exponent of the Schatten norm.

### [Weight decay direction / 1/gamma law](weight-decay-direction.md) — 9 papers

The question of in which direction, and by what law, the strength of the weight decay shifts the grokking — one of the few points of the corpus where the empirical evidence formally contradicts itself.

### [Overparameterization / depth](overparameterization-depth.md) — 5 papers

An excess of parameters relative to the data, and the number of layers, as control quantities. Depth acts non-monotonically: the dip at intermediate depth is cured not by layers but by stabilisation; over-parameterisation is a usual condition of the experiments rather than a necessary part of the phenomenon.

### [Architectural inductive bias](architectural-inductive-bias.md) — 4 papers

A preference among solutions built into the network before training: by the topology of the residual stream, by the normalisation, by the way the tokens are mixed. The delay can be bypassed by architecture, but only when its preferences agree with the symmetry of the task — the negative control on a non-commutative group shows exactly that.

###### cat-5

## 5. Interventions and methods

### [Gradient low-pass filtering](gradient-low-pass-filtering.md) — 13 papers

A device for accelerating grokking: the sequence of gradients of each parameter is treated as a time signal, and its slow (low-frequency) component, associated with generalisation, is amplified.

### [Numerical-stability fix](numerical-stability-fix.md) — 13 papers

The interventions of Prieto et al. (2025) that remove the softmax collapse or the gradient component producing it: StableMax and perp-Grad switch grokking on without regularisation.

### [Freezing subnetwork](freezing-subnetwork.md) — 11 papers

The weights of the network are fixed and only the structure is optimised — which connections to keep active; generalisation is attained by finding a good subnetwork inside the network already at hand (edge-popup).

### [Spherical weight-norm constraint](spherical-weight-norm-constraint.md) — 11 papers

An intervention holding the L2 norm of the weights or the activations fixed: the parameters are forced onto a sphere, the scale degree of freedom is removed, and the information is encoded by direction alone.

### [Accelerated grokking](accelerated-grokking.md) — 5 papers

A family of interventions that shorten the delay: into the gradient, into the initial embedding, into the parameters along the way, into the norm. Their common weakness is that the gain is measured in steps rather than in seconds, and often on a single seed.

###### cat-6

## 6. Analytical tools and metrics

### [Progress measures](progress-measures.md) — 67 papers

Continuous metrics of the internal state of a network which precede an abrupt jump in capability and are causally linked to it — a way of seeing the gradual hidden process behind the outward suddenness of grokking (Nanda et al., 2023).

### [Mechanistic interpretability](mechanistic-interpretability.md) — 48 papers

Reverse engineering of learned behaviour: recovering from the weights and the activations a human-readable algorithm that the network actually executes; the corpus's reference method after Nanda et al.'s analysis of modular addition.

### [Spectral analysis, SVD, ESD, FVE](spectral-analysis-svd-esd-fve.md) — 39 papers

A family of diagnostics based on the spectra of a network's internal matrices (SVD, ESD, FVE): delayed generalisation is tracked through the rearrangement of the singular and eigenvalues of the weights, the gradients and the representations.

### [Causal ablation / intervention](causal-ablation-intervention.md) — 24 papers

A methodology for establishing the causal rather than the correlational role of components: a frequency, a circuit or a feature is deliberately removed or substituted and the effect on the network's behaviour is measured.

### [Grokking time](grokking-time.md) — 18 papers

The delay between the fitting of the training sample and the onset of generalisation — the quantity by which the corpus compares interventions. It is defined operationally through thresholds, and which method turns out to be faster depends on the choice of definition (first crossing against stable grok) and of units (steps, seconds, FLOPs).

### [Order parameter](order-parameter.md) — 13 papers

A macroscopic quantity that changes abruptly when a control parameter crosses a critical threshold — the canonical marker of a phase transition, carried into the theories of grokking from statistical physics.

### [Seed variance / reproducibility](seed-variance-reproducibility.md) — 13 papers

A divergence of outcomes between runs that differ only in the random seed, and the question of what among the reported results survives a change of it. The spread enters the report, serves as a significance threshold for negative results and determines the design of the experiment: paired branches from one state against a comparison of means.

### [Heavy-tailed self-regularization, HTSR](heavy-tailed-self-regularization-htsr.md) — 9 papers

The theory of Martin & Mahoney: the spectral density of the weight matrices is characterised by a heavy-tailed power-law exponent α; it is brought into the corpus as an analytical lens by Prakash & Martin.

### [Linear / sparse probing](linear-sparse-probing.md) — 8 papers

A light linear classifier-probe is attached to frozen activations; from its accuracy one judges whether the property of interest is linearly decodable, that is, how structured the representation is.

### [Phase diagram](phase-diagram.md) — 8 papers

A map of the training regimes in the coordinates of the hyperparameters: where the network memorises, where it groks, where it does not train at all. It comes in binary form, coloured by a quantity (the time), and analytical — obtained by solving an equation rather than by a grid of runs.

### [Correlation traps](correlation-traps.md) — 4 papers

Anomalously large eigenvalues in the spectrum of an element-wise shuffled weight matrix, lying far beyond the upper edge of the "bulk" part of the Marchenko-Pastur distribution.

### [Negative results](negative-results.md) — 4 papers

Measurements showing that the expected effect is absent. They demand the same as positive ones: a declared expectation, a measure and a significance threshold — for which the spread across seeds serves.

###### cat-7

## 7. Theory and formal results

### [Effective theory / statistical mechanics](effective-theory-statistical-mechanics.md) — 27 papers

Physically motivated descriptions of grokking through a few macroscopic quantities — an order parameter, a control parameter, phases — on the pattern of the physics of phase transitions.

### [Margin maximization / implicit bias](margin-maximization-implicit-bias.md) — 25 papers

The implicit preference of gradient descent on separable data: among the interpolating solutions the one with the maximal margin is chosen; in the corpus this is used to explain the second, slow period of training under grokking.

### [Generalization bounds](generalization-bounds.md) — 18 papers

Formally provable estimates of generalising ability: on the generalisation error, on the sample complexity or — applied to grokking — on the length of the delay before generalisation.

### [Norm-Separation Delay Law](norm-separation-delay-law.md) — 10 papers

The quantitative law of Truong et al.: the grokking delay is inversely proportional to the effective rate of contraction of the norm and proportional to the logarithm of the ratio of the norms of the memorising and the generalising solution.

### [Kolmogorov complexity](kolmogorov-complexity.md) — 7 papers

The length of the shortest program generating an object; a measure of complexity under which the generalising solution is simpler than the memorising one, and delayed generalisation is read as a descent of the model towards a lower complexity.

### [Criticality / critical point](criticality-critical-point.md) — 5 papers

A value of the control parameter near which the dynamics slows so much that generalisation comes with a delay. Proved in one solvable setting, and the transfer to the rest is claimed as a guess; the "critical dataset size" is a threshold of a different kind.

### [Scaling laws](scaling-laws.md) — 5 papers

Power-law dependences of quality on scale, carried into the discussion of grokking as a frame that delayed generalisation either contradicts or fits into. Standing apart is the law of the memorisation-generalisation boundary, derived from the dynamics, and the dispute over whether the step is produced by the measure.

### [Quadratic networks](quadratic-networks.md) — 4 papers

Two-layer networks with an $x^2$ activation — the smallest departure from linearity at which feature learning still exists while the derivations are still possible. Three unconnected frames have converged on them: an exact solution, a bound on the sample complexity and the Bayesian geometry of the landscape.

### [Information bottleneck](information-bottleneck.md) — 3 papers

A frame of compressing the input while preserving the information about the target, predicting a fit and then a compression. In the corpus it survives as a vocabulary shared with double descent and grokking, while its place as a measurable quantity has been taken by computable complexity measures.

### [Singular learning theory, SLT](singular-learning-theory.md) — 3 papers

A frame proceeding from the fact that networks are singular statistical models and that the set of minima is a manifold with singularities. The central quantity is the local learning coefficient; the confirmation in the corpus is mixed.

###### cat-8

## 8. Concept stubs (no card yet)

The entries of this category are stubs: a name, an English term and the quotes already written out; the concept has no card. The counter "— N papers" here does not mean the same as it does for the cards of categories 1–7: for a card it is `papers_linked`, the number of papers in its reference blocks, whereas a stub has nothing to link to, so the counter is recomputed from the texts — how many papers of the corpus contain the English term in the body of `original/` (with the bibliography cut off, as in `count_incorpus.py`). The number of quotes under an entry is usually smaller than the counter: the quotes are written out as the papers are imported. The recount is `.claude/skills/check-corpus-integrity/scripts/count_stub_mentions.py` (`--write` rewrites the counters, `--check` only verifies); it also holds the rule for building the query. The entries are ordered by the English term.

### Absolute Gradient Entropy, AGE — 1 paper

- 2504.17243: [`"a novel Absolute Gradient Entropy (AGE) metric"`](../papers/2504.17243.neuralgrok-accelerate-grokking-by-neural-gradient-transformation/original/2504.17243.neuralgrok-accelerate-grokking-by-neural-gradient-transformation.md#p1-2) — [in the card](../papers/2504.17243.neuralgrok-accelerate-grokking-by-neural-gradient-transformation/original/2504.17243.neuralgrok-accelerate-grokking-by-neural-gradient-transformation.md#p1-2)

### Activation nonlinearity control — 0 papers

- 2411.05353: [`"can be controlled by modifying the profile of the activation function"`](../papers/2411.05353.controlling-grokking-with-nonlinearity-and-data-symmetry/original/2411.05353.controlling-grokking-with-nonlinearity-and-data-symmetry.md#p1-5) — [in the card](../papers/2411.05353.controlling-grokking-with-nonlinearity-and-data-symmetry/original/2411.05353.controlling-grokking-with-nonlinearity-and-data-symmetry.md#p1-5)

### Adaptive kernel feature learning — 0 papers

- 2310.03789: [`"the adaptive kernel approach, to two teacher-student models"`](../papers/2310.03789.grokking-as-a-first-order-phase-transition-in-two-layer-networks/original/2310.03789.grokking-as-a-first-order-phase-transition-in-two-layer-networks.md#p1-2) — [in the card](../papers/2310.03789.grokking-as-a-first-order-phase-transition-in-two-layer-networks/original/2310.03789.grokking-as-a-first-order-phase-transition-in-two-layer-networks.md#p1-2)

### Arrhenius scaling — 1 paper

- 2606.17120: [`"with escape times following Arrhenius scaling"`](../papers/2606.17120.noise-driven-escape-from-metastable-phases-explains-grokking/original/2606.17120.noise-driven-escape-from-metastable-phases-explains-grokking.md#p1-2) — [in the card](../papers/2606.17120.noise-driven-escape-from-metastable-phases-explains-grokking/original/2606.17120.noise-driven-escape-from-metastable-phases-explains-grokking.md#p1-2)

### Causal role analysis — 0 papers

- 2509.17738: [`"the causal role of either"`](../papers/2509.17738.flatness-is-necessary-neural-collapse-is-not-rethinking-generalization-via-grokking/original/2509.17738.flatness-is-necessary-neural-collapse-is-not-rethinking-generalization-via-grokking.md#p1-2) — [in the card](../papers/2509.17738.flatness-is-necessary-neural-collapse-is-not-rethinking-generalization-via-grokking/original/2509.17738.flatness-is-necessary-neural-collapse-is-not-rethinking-generalization-via-grokking.md#p1-2)

### Dense vs sparse circuit competition — 0 papers

- 2303.11873: [`"two largely distinct subnetworks: a dense one that dominates before the transition"`](../papers/2303.11873.a-tale-of-two-circuits-grokking-as-competition-of-sparse-and-dense-subnetworks/original/2303.11873.a-tale-of-two-circuits-grokking-as-competition-of-sparse-and-dense-subnetworks.md#p1-2) — [in the card](../papers/2303.11873.a-tale-of-two-circuits-grokking-as-competition-of-sparse-and-dense-subnetworks/original/2303.11873.a-tale-of-two-circuits-grokking-as-competition-of-sparse-and-dense-subnetworks.md#p1-2)

### Circuit complexity metric — 0 papers

- 2506.04434: [`"Approximate Local Circuit Complexity"`](../papers/2506.04434.grokking-and-generalization-collapse-insights-from-htsr-theory/original/2506.04434.grokking-and-generalization-collapse-insights-from-htsr-theory.md#p2-1) — [in the card](../papers/2506.04434.grokking-and-generalization-collapse-insights-from-htsr-theory/original/2506.04434.grokking-and-generalization-collapse-insights-from-htsr-theory.md#p2-1)

### Cleanup removes memorization — 0 papers

- 2301.05217: [`"removes the memorization components"`](../papers/2301.05217.progress-measures-for-grokking-via-mechanistic-interpretability/2301.05217.progress-measures-for-grokking-via-mechanistic-interpretability.card.md#p2-3) — [in the card](../papers/2301.05217.progress-measures-for-grokking-via-mechanistic-interpretability/2301.05217.progress-measures-for-grokking-via-mechanistic-interpretability.card.md#p2-3)

### Co-grokking — 1 paper

- 2402.16726: [`"some multi-task mixtures may lead to co-grokking"`](../papers/2402.16726.towards-empirical-interpretation-of-internal-circuits-and-properties-in-grokked-transformers-on-modular-polynomials/original/2402.16726.towards-empirical-interpretation-of-internal-circuits-and-properties-in-grokked-transformers-on-modular-polynomials.md#p1-1) — [in the card](../papers/2402.16726.towards-empirical-interpretation-of-internal-circuits-and-properties-in-grokked-transformers-on-modular-polynomials/original/2402.16726.towards-empirical-interpretation-of-internal-circuits-and-properties-in-grokked-transformers-on-modular-polynomials.md#p1-1)

### Commutator defect curvature — 0 papers

- 2602.16746: [`"commutator defects—the non-commutativity of"`](../papers/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking/original/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking.md#p1-2) — [in the card](../papers/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking/original/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking.md#p1-2)

### Cross-layer memory sharing — 0 papers

- 2405.15071: [`"encouraging cross-layer knowledge sharing"`](../papers/2405.15071.grokked-transformers-are-implicit-reasoners/2405.15071.grokked-transformers-are-implicit-reasoners.card.md#p1-2) — [in the card](../papers/2405.15071.grokked-transformers-are-implicit-reasoners/2405.15071.grokked-transformers-are-implicit-reasoners.card.md#p1-2)

### Cross-task transferability — 0 papers

- 2402.16726: [`"grokked models obtain common features transferable among similar operations"`](../papers/2402.16726.towards-empirical-interpretation-of-internal-circuits-and-properties-in-grokked-transformers-on-modular-polynomials/original/2402.16726.towards-empirical-interpretation-of-internal-circuits-and-properties-in-grokked-transformers-on-modular-polynomials.md#p1-1) — [in the card](../papers/2402.16726.towards-empirical-interpretation-of-internal-circuits-and-properties-in-grokked-transformers-on-modular-polynomials/original/2402.16726.towards-empirical-interpretation-of-internal-circuits-and-properties-in-grokked-transformers-on-modular-polynomials.md#p1-1)

### Curriculum easy-hard data — 0 papers

- 2410.03569: [`"exposes models to easy and harder versions of modular arithmetic"`](../papers/2410.03569.making-hard-problems-easier-with-custom-data-distributions-and-loss-regularization/original/2410.03569.making-hard-problems-easier-with-custom-data-distributions-and-loss-regularization.md#p2-2) — [in the card](../papers/2410.03569.making-hard-problems-easier-with-custom-data-distributions-and-loss-regularization/original/2410.03569.making-hard-problems-easier-with-custom-data-distributions-and-loss-regularization.md#p2-2)

### Curvature analysis — 1 paper

- 2512.03437: [`"Analyses of features and curvature further suggest that post‑grokking models learn"`](../papers/2512.03437.grokked-models-are-better-unlearners/2512.03437.grokked-models-are-better-unlearners.card.md#p1-2) — [in the card](../papers/2512.03437.grokked-models-are-better-unlearners/2512.03437.grokked-models-are-better-unlearners.card.md#p1-2)

### Data symmetry breaking — 0 papers

- 2604.00316: [`"Breaking Data Symmetry is Needed For Generalization in Feature Learning Kernels"`](../papers/2604.00316.breaking-data-symmetry-is-needed-for-generalization-in-feature-learning-kernels/original/2604.00316.breaking-data-symmetry-is-needed-for-generalization-in-feature-learning-kernels.md#p1-1) — [in the card](../papers/2604.00316.breaking-data-symmetry-is-needed-for-generalization-in-feature-learning-kernels/original/2604.00316.breaking-data-symmetry-is-needed-for-generalization-in-feature-learning-kernels.md#p1-1)

### Dropout eliminates grokking — 0 papers

- 2510.25966: [`"dropout can eliminate grokking"`](../papers/2510.25966.grokking-in-the-ising-model/original/2510.25966.grokking-in-the-ising-model.md#p2-2) — [in the card](../papers/2510.25966.grokking-in-the-ising-model/original/2510.25966.grokking-in-the-ising-model.md#p2-2)

### Dropout Robustness Curve, DRC — 1 paper

- 2507.11645: [`"a Dropout Robustness Curve (DRC)"`](../papers/2507.11645.tracing-the-path-to-grokking-embeddings-dropout-and-network-activation/original/2507.11645.tracing-the-path-to-grokking-embeddings-dropout-and-network-activation.md#p1-5) — [in the card](../papers/2507.11645.tracing-the-path-to-grokking-embeddings-dropout-and-network-activation/original/2507.11645.tracing-the-path-to-grokking-embeddings-dropout-and-network-activation.md#p1-5)

### Early grokking prediction — 0 papers

- 2306.13253: [`"predict grokking without training for a large number"`](../papers/2306.13253.predicting-grokking-long-before-it-happens/original/2306.13253.predicting-grokking-long-before-it-happens.md#p1-2) — [in the card](../papers/2306.13253.predicting-grokking-long-before-it-happens/original/2306.13253.predicting-grokking-long-before-it-happens.md#p1-2)

### Early-warning power law — 0 papers

- 2602.16746: [`"the lead time obeys a power law ∆t ∝ t α"`](../papers/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking/original/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking.md#p1-2) — [in the card](../papers/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking/original/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking.md#p1-2)

### Edge of linear separability — 1 paper

- 2410.04489: [`"the training dataset is nearly linearly separable"`](../papers/2410.04489.grokking-at-the-edge-of-linear-separability/2410.04489.grokking-at-the-edge-of-linear-separability.card.md#p1-2) — [in the card](../papers/2410.04489.grokking-at-the-edge-of-linear-separability/2410.04489.grokking-at-the-edge-of-linear-separability.card.md#p1-2)

### Embedding cosine similarity — 0 papers

- 2507.11645: [`"similarity between embeddings in a high-dimensional spaces"`](../papers/2507.11645.tracing-the-path-to-grokking-embeddings-dropout-and-network-activation/original/2507.11645.tracing-the-path-to-grokking-embeddings-dropout-and-network-activation.md#p2-3) — [in the card](../papers/2507.11645.tracing-the-path-to-grokking-embeddings-dropout-and-network-activation/original/2507.11645.tracing-the-path-to-grokking-embeddings-dropout-and-network-activation.md#p2-3)

### Embedding-space uniformity — 0 papers

- 2504.03162: [`"the uniformity of the embedding space and the"`](../papers/2504.03162.beyond-progress-measures-theoretical-insights-into-the-mechanism-of-grokking/2504.03162.beyond-progress-measures-theoretical-insights-into-the-mechanism-of-grokking.card.md#p1-2) — [in the card](../papers/2504.03162.beyond-progress-measures-theoretical-insights-into-the-mechanism-of-grokking/2504.03162.beyond-progress-measures-theoretical-insights-into-the-mechanism-of-grokking.card.md#p1-2)

### Embedding transfer acceleration — 0 papers

- 2504.13292: [`"a simple and principled method for accelerating grokking"`](../papers/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model/original/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model.md#p1-2) — [in the card](../papers/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model/original/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model.md#p1-2)

### Energy-function gradient ascent — 0 papers

- 2509.21519: [`"gradient ascent of an energy function E"`](../papers/2509.21519.provable-scaling-laws-of-feature-emergence-from-learning-dynamics-of-grokking/original/2509.21519.provable-scaling-laws-of-feature-emergence-from-learning-dynamics-of-grokking.md#p1-2) — [in the card](../papers/2509.21519.provable-scaling-laws-of-feature-emergence-from-learning-dynamics-of-grokking/original/2509.21519.provable-scaling-laws-of-feature-emergence-from-learning-dynamics-of-grokking.md#p1-2)

### Fourier initialization — 1 paper
- 2603.05228: [`"deterministically initialized with cosine and sine values at five key frequencies"`](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p6-8) — [in the card](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p6-8)

### Feature-learning kernel, RFM — 0 papers

- 2604.00316: [`"via the Recursive Feature Machine (RFM)"`](../papers/2604.00316.breaking-data-symmetry-is-needed-for-generalization-in-feature-learning-kernels/original/2604.00316.breaking-data-symmetry-is-needed-for-generalization-in-feature-learning-kernels.md#p1-4) — [in the card](../papers/2604.00316.breaking-data-symmetry-is-needed-for-generalization-in-feature-learning-kernels/original/2604.00316.breaking-data-symmetry-is-needed-for-generalization-in-feature-learning-kernels.md#p1-4)

### Feature rank collapse — 0 papers

- 2405.19454: [`"the decreasing of feature ranks and the"`](../papers/2405.19454.deep-grokking-would-deep-neural-networks-generalize-better/2405.19454.deep-grokking-would-deep-neural-networks-generalize-better.card.md#p1-3) — [in the card](../papers/2405.19454.deep-grokking-would-deep-neural-networks-generalize-better/2405.19454.deep-grokking-would-deep-neural-networks-generalize-better.card.md#p1-3)

### Flat minima generalization — 0 papers

- 2603.01192: [`"“flatter” regions of the loss landscape generalise better"`](../papers/2603.01192.a-basin-selection-perspective-on-grokking-via-singular-learning-theory/2603.01192.a-basin-selection-perspective-on-grokking-via-singular-learning-theory.card.md#p1-4) — [in the card](../papers/2603.01192.a-basin-selection-perspective-on-grokking-via-singular-learning-theory/2603.01192.a-basin-selection-perspective-on-grokking-via-singular-learning-theory.card.md#p1-4)

### Flatness regularization — 1 paper

- 2509.17738: [`"models regularized away from flat"`](../papers/2509.17738.flatness-is-necessary-neural-collapse-is-not-rethinking-generalization-via-grokking/original/2509.17738.flatness-is-necessary-neural-collapse-is-not-rethinking-generalization-via-grokking.md#p1-2) — [in the card](../papers/2509.17738.flatness-is-necessary-neural-collapse-is-not-rethinking-generalization-via-grokking/original/2509.17738.flatness-is-necessary-neural-collapse-is-not-rethinking-generalization-via-grokking.md#p1-2)

### Floating-point precision — 1 paper

- 2605.06152: [`"of floating-point arithmetic precision limits"`](../papers/2605.06152.grokking-or-glitching-how-low-precision-drives-slingshot-loss-spikes/original/2605.06152.grokking-or-glitching-how-low-precision-drives-slingshot-loss-spikes.md#p1-2) — [in the card](../papers/2605.06152.grokking-or-glitching-how-low-precision-drives-slingshot-loss-spikes/original/2605.06152.grokking-or-glitching-how-low-precision-drives-slingshot-loss-spikes.md#p1-2)

### Fourier head — 1 paper

- 2603.05228: [`"Fourier-constrained output heads"`](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p3-4) — [in the card](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p3-4)

### Fourier initialization — 1 paper

- 2603.05228: [`"deterministically initialized with cosine and sine values at five key frequencies"`](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p6-8) — [in the card](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p6-8)

### Fourier / frequency entropy — 1 paper

- 2310.19470: [`"we introduce Fourier Entropy (FE) as follows"`](../papers/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks/original/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks.md#p10-5) — [in the card](../papers/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks/original/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks.md#p10-5)

### Frequency misalignment — 0 papers

- 2405.17479: [`"a misalignment between the preferred frequency in the"`](../papers/2405.17479.a-rationale-from-frequency-perspective-for-grokking-in-training-neural-network/2405.17479.a-rationale-from-frequency-perspective-for-grokking-in-training-neural-network.card.md#p1-5) — [in the card](../papers/2405.17479.a-rationale-from-frequency-perspective-for-grokking-in-training-neural-network/2405.17479.a-rationale-from-frequency-perspective-for-grokking-in-training-neural-network.card.md#p1-5)

### Gaussian Feature Learning, GFL — 1 paper

- 2310.03789: [`"that of Gaussian Feature Learning (GFL)"`](../papers/2310.03789.grokking-as-a-first-order-phase-transition-in-two-layer-networks/original/2310.03789.grokking-as-a-first-order-phase-transition-in-two-layer-networks.md#p1-4) — [in the card](../papers/2310.03789.grokking-as-a-first-order-phase-transition-in-two-layer-networks/original/2310.03789.grokking-as-a-first-order-phase-transition-in-two-layer-networks.md#p1-4)

### Geometric signatures — 1 paper

- 2509.17738: [`"geometric signatures of generalization"`](../papers/2509.17738.flatness-is-necessary-neural-collapse-is-not-rethinking-generalization-via-grokking/original/2509.17738.flatness-is-necessary-neural-collapse-is-not-rethinking-generalization-via-grokking.md#p1-3) — [in the card](../papers/2509.17738.flatness-is-necessary-neural-collapse-is-not-rethinking-generalization-via-grokking/original/2509.17738.flatness-is-necessary-neural-collapse-is-not-rethinking-generalization-via-grokking.md#p1-3)

### Gradient alignment forget-retain — 0 papers

- 2512.03437: [`"reduced gradient alignment between forget and retain subsets"`](../papers/2512.03437.grokked-models-are-better-unlearners/2512.03437.grokked-models-are-better-unlearners.card.md#p1-2) — [in the card](../papers/2512.03437.grokked-models-are-better-unlearners/2512.03437.grokked-models-are-better-unlearners.card.md#p1-2)

### Gradient spectral decomposition — 0 papers

- 2405.20233: [`"we can spectrally decompose the parameter trajectories under"`](../papers/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients.card.md#p1-2) — [in the card](../papers/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients.card.md#p1-2)

### Graph properties of subnetwork — 0 papers

- 2310.19470: [`"beneficial graph properties such as increased average"`](../papers/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks/original/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks.md#p1-2) — [in the card](../papers/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks/original/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks.md#p1-2)

### Grokked lottery tickets — 0 papers

- 2310.19470: [`"lottery tickets obtained during the generalizing phase (termed grokked tickets)"`](../papers/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks/original/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks.md#p1-2) — [in the card](../papers/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks/original/2310.19470.bridging-lottery-ticket-and-grokking-understanding-grokking-from-inner-structure-of-networks.md#p1-2)

### Grokking as compression — 1 paper

- 2310.05918: [`"many of them share a similar high-level idea which is"`](../papers/2310.05918.grokking-as-compression-a-nonlinear-complexity-perspective/original/2310.05918.grokking-as-compression-a-nonlinear-complexity-perspective.md#p1-3) — [in the card](../papers/2310.05918.grokking-as-compression-a-nonlinear-complexity-perspective/original/2310.05918.grokking-as-compression-a-nonlinear-complexity-perspective.md#p1-3)

### Grokking transferability — 0 papers

- 2601.09049: [`"the downstream transferability of “grokked” Transformers remains largely underexplored"`](../papers/2601.09049.is-grokking-worthwhile-functional-analysis-and-transferability-of-generalization-circuits-in-transformers/original/2601.09049.is-grokking-worthwhile-functional-analysis-and-transferability-of-generalization-circuits-in-transformers.md#p4-1) — [in the card](../papers/2601.09049.is-grokking-worthwhile-functional-analysis-and-transferability-of-generalization-circuits-in-transformers/original/2601.09049.is-grokking-worthwhile-functional-analysis-and-transferability-of-generalization-circuits-in-transformers.md#p4-1)

### Grokking weakens with complexity — 0 papers

- 2402.09469: [`"as $k$ increases, the grokking phenomenon becomes weak"`](../papers/2402.09469.fourier-circuits-in-neural-networks-and-transformers-a-case-study-of-modular-arithmetic-with-multiple-inputs/original/2402.09469.fourier-circuits-in-neural-networks-and-transformers-a-case-study-of-modular-arithmetic-with-multiple-inputs.md#fig-4) — [in the card](../papers/2402.09469.fourier-circuits-in-neural-networks-and-transformers-a-case-study-of-modular-arithmetic-with-multiple-inputs/original/2402.09469.fourier-circuits-in-neural-networks-and-transformers-a-case-study-of-modular-arithmetic-with-multiple-inputs.md#fig-4)

### Heuristic core — 1 paper

- 2403.03942: [`"evidence of a *heuristic core*: a set of attention heads that appear in all generalizing subnetworks but, on their own, do not generalize"`](../papers/2403.03942.the-heuristic-core-understanding-subnetwork-generalization-in-pretrained-language-models/2403.03942.the-heuristic-core-understanding-subnetwork-generalization-in-pretrained-language-models.card.md#fig-1) — [in the card](../papers/2403.03942.the-heuristic-core-understanding-subnetwork-generalization-in-pretrained-language-models/2403.03942.the-heuristic-core-understanding-subnetwork-generalization-in-pretrained-language-models.card.md#fig-1)

### Hyperparameter tuning — 8 papers

- 2601.19791: [`"through proper hyperparameter tuning"`](../papers/2601.19791.to-grok-grokking-provable-grokking-in-ridge-regression/original/2601.19791.to-grok-grokking-provable-grokking-in-ridge-regression.md#p1-2) — [in the card](../papers/2601.19791.to-grok-grokking-provable-grokking-in-ridge-regression/original/2601.19791.to-grok-grokking-provable-grokking-in-ridge-regression.md#p1-2)

### Implicit bias of adaptive optimizers — 0 papers

- 2206.04817: [`"characterizing an implicit bias of such optimizers"`](../papers/2206.04817.the-slingshot-mechanism-an-empirical-study-of-adaptive-optimizers-and-grokking/2206.04817.the-slingshot-mechanism-an-empirical-study-of-adaptive-optimizers-and-grokking.card.md#p2-8) — [in the card](../papers/2206.04817.the-slingshot-mechanism-an-empirical-study-of-adaptive-optimizers-and-grokking/2206.04817.the-slingshot-mechanism-an-empirical-study-of-adaptive-optimizers-and-grokking.card.md#p2-8)

### Inactive neurons metric — 0 papers

- 2507.11645: [`"percentage of inactive neurons decreases during generalization"`](../papers/2507.11645.tracing-the-path-to-grokking-embeddings-dropout-and-network-activation/original/2507.11645.tracing-the-path-to-grokking-embeddings-dropout-and-network-activation.md#p1-5) — [in the card](../papers/2507.11645.tracing-the-path-to-grokking-embeddings-dropout-and-network-activation/original/2507.11645.tracing-the-path-to-grokking-embeddings-dropout-and-network-activation.md#p1-5)

### Insufficient sampling / aliasing — 1 paper

- 2405.17479: [`"caused by insufficient sampling"`](../papers/2405.17479.a-rationale-from-frequency-perspective-for-grokking-in-training-neural-network/2405.17479.a-rationale-from-frequency-perspective-for-grokking-in-training-neural-network.card.md#p1-6) — [in the card](../papers/2405.17479.a-rationale-from-frequency-perspective-for-grokking-in-training-neural-network/2405.17479.a-rationale-from-frequency-perspective-for-grokking-in-training-neural-network.card.md#p1-6)

### Interpolation threshold criticality — 0 papers

- 2410.04489: [`"the interpolation threshold, reminiscent of critical"`](../papers/2410.04489.grokking-at-the-edge-of-linear-separability/2410.04489.grokking-at-the-edge-of-linear-separability.card.md#p1-2) — [in the card](../papers/2410.04489.grokking-at-the-edge-of-linear-separability/2410.04489.grokking-at-the-edge-of-linear-separability.card.md#p1-2)

### Knowledge distillation — 2 papers

- 2511.04760: [`"Knowledge Distillation (KD) from a model that has already"`](../papers/2511.04760.when-data-falls-short-grokking-below-the-critical-threshold/original/2511.04760.when-data-falls-short-grokking-below-the-critical-threshold.md#p1-3) — [in the card](../papers/2511.04760.when-data-falls-short-grokking-below-the-critical-threshold/original/2511.04760.when-data-falls-short-grokking-below-the-critical-threshold.md#p1-3)

### L-infinity regularization — 0 papers

- 2407.12332: [`"can be found by gradient descent with small ℓ∞ regularization"`](../papers/2407.12332.why-do-you-grok-a-theoretical-analysis-of-grokking-modular-addition/original/2407.12332.why-do-you-grok-a-theoretical-analysis-of-grokking-modular-addition.md#p1-2) — [in the card](../papers/2407.12332.why-do-you-grok-a-theoretical-analysis-of-grokking-modular-addition/original/2407.12332.why-do-you-grok-a-theoretical-analysis-of-grokking-modular-addition.md#p1-2)

### Last-layer weight-norm cycling — 0 papers

- 2206.04817: [`"cyclic behavior of the norm of the"`](../papers/2206.04817.the-slingshot-mechanism-an-empirical-study-of-adaptive-optimizers-and-grokking/2206.04817.the-slingshot-mechanism-an-empirical-study-of-adaptive-optimizers-and-grokking.card.md#p1-2) — [in the card](../papers/2206.04817.the-slingshot-mechanism-an-empirical-study-of-adaptive-optimizers-and-grokking/2206.04817.the-slingshot-mechanism-an-empirical-study-of-adaptive-optimizers-and-grokking.card.md#p1-2)

### Less-salient frequency first — 0 papers

- 2405.17479: [`"initially learn the less salient"`](../papers/2405.17479.a-rationale-from-frequency-perspective-for-grokking-in-training-neural-network/2405.17479.a-rationale-from-frequency-perspective-for-grokking-in-training-neural-network.card.md#p1-2) — [in the card](../papers/2405.17479.a-rationale-from-frequency-perspective-for-grokking-in-training-neural-network/2405.17479.a-rationale-from-frequency-perspective-for-grokking-in-training-neural-network.card.md#p1-2)

### LLC trajectory probe — 0 papers

- 2603.01192: [`"LLC trajectories estimated from training data track the onset of generalisation"`](../papers/2603.01192.a-basin-selection-perspective-on-grokking-via-singular-learning-theory/2603.01192.a-basin-selection-perspective-on-grokking-via-singular-learning-theory.card.md#p1-2) — [in the card](../papers/2603.01192.a-basin-selection-perspective-on-grokking-via-singular-learning-theory/2603.01192.a-basin-selection-perspective-on-grokking-via-singular-learning-theory.card.md#p1-2)

### Local complexity analysis — 1 paper

- 2512.03437: [`"quantifies the density of linear regions in a neural network’s input space partition"`](../papers/2512.03437.grokked-models-are-better-unlearners/2512.03437.grokked-models-are-better-unlearners.card.md#p9-8) — [in the card](../papers/2512.03437.grokked-models-are-better-unlearners/2512.03437.grokked-models-are-better-unlearners.card.md#p9-8)

### Local asynchronous grokking — 0 papers

- 2506.21551: [`"enter their grokking stages asynchronously"`](../papers/2506.21551.grokking-in-llm-pretraining-monitor-memorization-to-generalization-without-test/2506.21551.grokking-in-llm-pretraining-monitor-memorization-to-generalization-without-test.card.md#p1-2) — [in the card](../papers/2506.21551.grokking-in-llm-pretraining-monitor-memorization-to-generalization-without-test/2506.21551.grokking-in-llm-pretraining-monitor-memorization-to-generalization-without-test.card.md#p1-2)

### Logit scaling growth — 0 papers

- 2501.04697: [`"a direction of uncontrolled logit growth"`](../papers/2501.04697.grokking-at-the-edge-of-numerical-stability/2501.04697.grokking-at-the-edge-of-numerical-stability.card.md#p2-4) — [in the card](../papers/2501.04697.grokking-at-the-edge-of-numerical-stability/2501.04697.grokking-at-the-edge-of-numerical-stability.card.md#p2-4)

### Low-pass gradient filter — 0 papers

- 2405.20233: [`"low-pass filtered gradients which is added to the current"`](../papers/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients.card.md#p3-10) — [in the card](../papers/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients/2405.20233.grokfast-accelerated-grokking-by-amplifying-slow-gradients.card.md#p3-10)

### Low-rank matrix factorization — 1 paper

- 2506.05718: [`"sparse recovery and low rank matrix factorization"`](../papers/2506.05718.grokking-beyond-the-euclidean-norm-of-model-parameters/original/2506.05718.grokking-beyond-the-euclidean-norm-of-model-parameters.md#p4-3) — [in the card](../papers/2506.05718.grokking-beyond-the-euclidean-norm-of-model-parameters/original/2506.05718.grokking-beyond-the-euclidean-norm-of-model-parameters.md#p4-3)

### Machine unlearning — 1 paper

- 2512.03437: [`"*machine unlearning*, i.e., removing the influence of specified data without full retraining"`](../papers/2512.03437.grokked-models-are-better-unlearners/2512.03437.grokked-models-are-better-unlearners.card.md#p1-2) — [in the card](../papers/2512.03437.grokked-models-are-better-unlearners/2512.03437.grokked-models-are-better-unlearners.card.md#p1-2)

### Matrix Renyi entropy metric — 0 papers

- 2311.06597: [`"The $\alpha$-order (Rényi) entropy for matrix $\mathbf{R}$ is defined as follows"`](../papers/2311.06597.understanding-grokking-through-a-robustness-viewpoint/2311.06597.understanding-grokking-through-a-robustness-viewpoint.card.md#p3-4) — [in the card](../papers/2311.06597.understanding-grokking-through-a-robustness-viewpoint/2311.06597.understanding-grokking-through-a-robustness-viewpoint.card.md#p3-4)

### Model complexity reduction — 0 papers

- 2504.17243: [`"the intrinsic complexity of the model leveraging the absolute weight"`](../papers/2504.17243.neuralgrok-accelerate-grokking-by-neural-gradient-transformation/original/2504.17243.neuralgrok-accelerate-grokking-by-neural-gradient-transformation.md#p2-1) — [in the card](../papers/2504.17243.neuralgrok-accelerate-grokking-by-neural-gradient-transformation/original/2504.17243.neuralgrok-accelerate-grokking-by-neural-gradient-transformation.md#p2-1)

### Modular representations — 1 paper

- 2512.03437: [`"post‑grokking models learn *more modular representations*"`](../papers/2512.03437.grokked-models-are-better-unlearners/2512.03437.grokked-models-are-better-unlearners.card.md#p1-2) — [in the card](../papers/2512.03437.grokked-models-are-better-unlearners/2512.03437.grokked-models-are-better-unlearners.card.md#p1-2)

### MoE expert pathways — 0 papers

- 2506.21551: [`"expert choices across layers in MoE"`](../papers/2506.21551.grokking-in-llm-pretraining-monitor-memorization-to-generalization-without-test/2506.21551.grokking-in-llm-pretraining-monitor-memorization-to-generalization-without-test.card.md#p1-2) — [in the card](../papers/2506.21551.grokking-in-llm-pretraining-monitor-memorization-to-generalization-without-test/2506.21551.grokking-in-llm-pretraining-monitor-memorization-to-generalization-without-test.card.md#p1-2)

### Multi-stage generalization — 1 paper

- 2405.19454: [`"We observe a multi-stage progress in generalization"`](../papers/2405.19454.deep-grokking-would-deep-neural-networks-generalize-better/2405.19454.deep-grokking-would-deep-neural-networks-generalize-better.card.md#p1-9) — [in the card](../papers/2405.19454.deep-grokking-would-deep-neural-networks-generalize-better/2405.19454.deep-grokking-would-deep-neural-networks-generalize-better.card.md#p1-9)

### Multi-task emergence — 0 papers

- 2402.15175: [`"By extending our framework to multi-task learning"`](../papers/2402.15175.unified-view-of-grokking-double-descent-and-emergent-abilities/original/2402.15175.unified-view-of-grokking-double-descent-and-emergent-abilities.md#p3-2) — [in the card](../papers/2402.15175.unified-view-of-grokking-double-descent-and-emergent-abilities/original/2402.15175.unified-view-of-grokking-double-descent-and-emergent-abilities.md#p3-2)

### Mutual information progress measure — 0 papers

- 2408.08944: [`"higher-order mutual information to analyze the"`](../papers/2408.08944.information-theoretic-progress-measures-reveal-grokking-is-an-emergent-phase-transition/original/2408.08944.information-theoretic-progress-measures-reveal-grokking-is-an-emergent-phase-transition.md#p1-2) — [in the card](../papers/2408.08944.information-theoretic-progress-measures-reveal-grokking-is-an-emergent-phase-transition/original/2408.08944.information-theoretic-progress-measures-reveal-grokking-is-an-emergent-phase-transition.md#p1-2)

### Natural gradient descent — 1 paper

- 2510.04930: [`"formal links to natural gradient descent"`](../papers/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking/original/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking.md#p1-6) — [in the card](../papers/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking/original/2510.04930.egalitarian-gradient-descent-a-simple-approach-to-accelerated-grokking.md#p1-6)

### Normalized Transformer hypersphere — 0 papers

- 2603.05228: [`"a normalized Transformer that constrains all vectors to the unit hypersphere"`](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p4-2) — [in the card](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p4-2)

### Numerical Feature Inflation, NFI — 1 paper

- 2605.06152: [`"this mechanism Numerical Feature Inflation (N FI)"`](../papers/2605.06152.grokking-or-glitching-how-low-precision-drives-slingshot-loss-spikes/original/2605.06152.grokking-or-glitching-how-low-precision-drives-slingshot-loss-spikes.md#p1-2) — [in the card](../papers/2605.06152.grokking-or-glitching-how-low-precision-drives-slingshot-loss-spikes/original/2605.06152.grokking-or-glitching-how-low-precision-drives-slingshot-loss-spikes.md#p1-2)

### OOD generalization gap — 0 papers

- 2403.03942: [`"generalize very differently to adversarial out-of-domain (OOD) evaluation sets"`](../papers/2403.03942.the-heuristic-core-understanding-subnetwork-generalization-in-pretrained-language-models/2403.03942.the-heuristic-core-understanding-subnetwork-generalization-in-pretrained-language-models.card.md#p1-5) — [in the card](../papers/2403.03942.the-heuristic-core-understanding-subnetwork-generalization-in-pretrained-language-models/2403.03942.the-heuristic-core-understanding-subnetwork-generalization-in-pretrained-language-models.card.md#p1-5)

### Pathway similarity metric — 0 papers

- 2506.21551: [`"one computes the pathway similarity"`](../papers/2506.21551.grokking-in-llm-pretraining-monitor-memorization-to-generalization-without-test/2506.21551.grokking-in-llm-pretraining-monitor-memorization-to-generalization-without-test.card.md#p1-2) — [in the card](../papers/2506.21551.grokking-in-llm-pretraining-monitor-memorization-to-generalization-without-test/2506.21551.grokking-in-llm-pretraining-monitor-memorization-to-generalization-without-test.card.md#p1-2)

### PCA symmetry factorization — 0 papers

- 2411.05353: [`"can yield a factorization of the modulus"`](../papers/2411.05353.controlling-grokking-with-nonlinearity-and-data-symmetry/original/2411.05353.controlling-grokking-with-nonlinearity-and-data-symmetry.md#p2-4) — [in the card](../papers/2411.05353.controlling-grokking-with-nonlinearity-and-data-symmetry/original/2411.05353.controlling-grokking-with-nonlinearity-and-data-symmetry.md#p2-4)

### PCA trajectory analysis — 0 papers

- 2602.16746: [`"Using PCA on attention weight trajectories and commutator defect analysis"`](../papers/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking/original/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking.md#p1-2) — [in the card](../papers/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking/original/2602.16746.low-dimensional-and-transversely-curved-optimization-dynamics-in-grokking.md#p1-2)

### Permutation equivariance — 1 paper

- 2407.12332: [`"no permutation-equivariant model can achieve small population error"`](../papers/2407.12332.why-do-you-grok-a-theoretical-analysis-of-grokking-modular-addition/original/2407.12332.why-do-you-grok-a-theoretical-analysis-of-grokking-modular-addition.md#p1-2) — [in the card](../papers/2407.12332.why-do-you-grok-a-theoretical-analysis-of-grokking-modular-addition/original/2407.12332.why-do-you-grok-a-theoretical-analysis-of-grokking-modular-addition.md#p1-2)

### Preconditioned gradient descent — 1 paper

- 2601.03162: [`"the impact of preconditioned gradient descent"`](../papers/2601.03162.on-the-convergence-behavior-of-preconditioned-gradient-descent-toward-the-rich-learning-regime/2601.03162.on-the-convergence-behavior-of-preconditioned-gradient-descent-toward-the-rich-learning-regime.card.md#p1-2) — [in the card](../papers/2601.03162.on-the-convergence-behavior-of-preconditioned-gradient-descent-toward-the-rich-learning-regime/2601.03162.on-the-convergence-behavior-of-preconditioned-gradient-descent-toward-the-rich-learning-regime.card.md#p1-2)

### Problem-specific loss regularization — 1 paper

- 2410.03569: [`"Design a custom loss function with a penalty term specific to modular"`](../papers/2410.03569.making-hard-problems-easier-with-custom-data-distributions-and-loss-regularization/original/2410.03569.making-hard-problems-easier-with-custom-data-distributions-and-loss-regularization.md#p2-3) — [in the card](../papers/2410.03569.making-hard-problems-easier-with-custom-data-distributions-and-loss-regularization/original/2410.03569.making-hard-problems-easier-with-custom-data-distributions-and-loss-regularization.md#p2-3)

### Relative flatness — 1 paper

- 2509.17738: [`"the Hessian trace normalized by the weight"`](../papers/2509.17738.flatness-is-necessary-neural-collapse-is-not-rethinking-generalization-via-grokking/original/2509.17738.flatness-is-necessary-neural-collapse-is-not-rethinking-generalization-via-grokking.md#p2-2) — [in the card](../papers/2509.17738.flatness-is-necessary-neural-collapse-is-not-rethinking-generalization-via-grokking/original/2509.17738.flatness-is-necessary-neural-collapse-is-not-rethinking-generalization-via-grokking.md#p2-2)

### Residual magnitude — 1 paper

- 2603.05228: [`"unbounded residual magnitude and data-dependent attention routing"`](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p1-2) — [in the card](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p1-2)

### Robustness sufficient condition — 0 papers

- 2311.06597: [`"the decrease of weight norm usually happens before the grokking on the test dataset, making it seemingly a sufficient condition for grokking but not a necessary condition"`](../papers/2311.06597.understanding-grokking-through-a-robustness-viewpoint/2311.06597.understanding-grokking-through-a-robustness-viewpoint.card.md#p1-4) — [in the card](../papers/2311.06597.understanding-grokking-through-a-robustness-viewpoint/2311.06597.understanding-grokking-through-a-robustness-viewpoint.card.md#p1-4)

### Simplified decision boundaries — 1 paper

- 2510.25966: [`"simplified decision boundaries in the input space"`](../papers/2510.25966.grokking-in-the-ising-model/original/2510.25966.grokking-in-the-ising-model.md#p2-3) — [in the card](../papers/2510.25966.grokking-in-the-ising-model/original/2510.25966.grokking-in-the-ising-model.md#p2-3)

### Sparse data augmentation — 0 papers

- 2410.03569: [`"Sparse data elements are critical for learning"`](../papers/2410.03569.making-hard-problems-easier-with-custom-data-distributions-and-loss-regularization/original/2410.03569.making-hard-problems-easier-with-custom-data-distributions-and-loss-regularization.md#p7-1) — [in the card](../papers/2410.03569.making-hard-problems-easier-with-custom-data-distributions-and-loss-regularization/original/2410.03569.making-hard-problems-easier-with-custom-data-distributions-and-loss-regularization.md#p7-1)

### Spectral entropy collapse — 1 paper

- 2604.13123: [`"norm expansion followed by entropy collapse"`](../papers/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation.card.md#p1-2) — [in the card](../papers/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation/2604.13123.spectral-entropy-collapse-as-a-phase-transition-in-delayed-generalisation.card.md#p1-2)

### Spectral gating — 2 papers

- 2603.15492: [`"revealing a “Spectral Gating” mechanism that regulates the transition"`](../papers/2603.15492.grokking-as-a-variance-limited-phase-transition-spectral-gating-and-the-epsilon-stability-threshold/original/2603.15492.grokking-as-a-variance-limited-phase-transition-spectral-gating-and-the-epsilon-stability-threshold.md#p1-2) — [in the card](../papers/2603.15492.grokking-as-a-variance-limited-phase-transition-spectral-gating-and-the-epsilon-stability-threshold/original/2603.15492.grokking-as-a-variance-limited-phase-transition-spectral-gating-and-the-epsilon-stability-threshold.md#p1-2)

### Spectral signature predictor — 0 papers

- 2306.13253: [`"We propose spectral signature to quantify the oscilla-"`](../papers/2306.13253.predicting-grokking-long-before-it-happens/original/2306.13253.predicting-grokking-long-before-it-happens.md#p2-2) — [in the card](../papers/2306.13253.predicting-grokking-long-before-it-happens/original/2306.13253.predicting-grokking-long-before-it-happens.md#p2-2)

### Spurious dimensions induce grokking — 0 papers

- 2310.17247: [`"via the addition of dimensions containing spurious information"`](../papers/2310.17247.grokking-beyond-neural-networks-an-empirical-exploration-with-model-complexity/2310.17247.grokking-beyond-neural-networks-an-empirical-exploration-with-model-complexity.card.md#p1-1) — [in the card](../papers/2310.17247.grokking-beyond-neural-networks-an-empirical-exploration-with-model-complexity/2310.17247.grokking-beyond-neural-networks-an-empirical-exploration-with-model-complexity.card.md#p1-1)

### Temperature-bounded output — 0 papers

- 2603.05228: [`"logit magnitudes are strictly bounded by the temperature parameter"`](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p6-7) — [in the card](../papers/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology/original/2603.05228.the-geometric-inductive-bias-of-grokking-bypassing-phase-transitions-via-architectural-topology.md#p6-7)

### Three-stage training dynamic — 1 paper

- 2603.01968: [`"we identify a consistent three-stage training dynamic:"`](../papers/2603.01968.intrinsic-task-symmetry-drives-generalization-in-algorithmic-tasks/original/2603.01968.intrinsic-task-symmetry-drives-generalization-in-algorithmic-tasks.md#p1-6) — [in the card](../papers/2603.01968.intrinsic-task-symmetry-drives-generalization-in-algorithmic-tasks/original/2603.01968.intrinsic-task-symmetry-drives-generalization-in-algorithmic-tasks.md#p1-6)

### Time-scale separation — 1 paper

- 2509.20829: [`"distinct time scales between fitting the training set"`](../papers/2509.20829.explaining-grokking-and-information-bottleneck-through-neural-collapse-emergence/2509.20829.explaining-grokking-and-information-bottleneck-through-neural-collapse-emergence.card.md#p1-2) — [in the card](../papers/2509.20829.explaining-grokking-and-information-bottleneck-through-neural-collapse-emergence/2509.20829.explaining-grokking-and-information-bottleneck-through-neural-collapse-emergence.card.md#p1-2)

### Token uniformity — 1 paper

- 2504.03162: [`"this optimization merely leads to token uniformity"`](../papers/2504.03162.beyond-progress-measures-theoretical-insights-into-the-mechanism-of-grokking/2504.03162.beyond-progress-measures-theoretical-insights-into-the-mechanism-of-grokking.card.md#p1-2) — [in the card](../papers/2504.03162.beyond-progress-measures-theoretical-insights-into-the-mechanism-of-grokking/2504.03162.beyond-progress-measures-theoretical-insights-into-the-mechanism-of-grokking.card.md#p1-2)

### Tunnel effect — 1 paper

- 2405.19454: [`"Emergence of *Tunnel* on various depth of models"`](../papers/2405.19454.deep-grokking-would-deep-neural-networks-generalize-better/2405.19454.deep-grokking-would-deep-neural-networks-generalize-better.card.md#fig-3) — [in the card](../papers/2405.19454.deep-grokking-would-deep-neural-networks-generalize-better/2405.19454.deep-grokking-would-deep-neural-networks-generalize-better.card.md#fig-3)

### Weight entropy metric — 0 papers

- 2411.05353: [`"a metric for the generalization ability of"`](../papers/2411.05353.controlling-grokking-with-nonlinearity-and-data-symmetry/original/2411.05353.controlling-grokking-with-nonlinearity-and-data-symmetry.md#p1-5) — [in the card](../papers/2411.05353.controlling-grokking-with-nonlinearity-and-data-symmetry/original/2411.05353.controlling-grokking-with-nonlinearity-and-data-symmetry.md#p1-5)

### Within-class variance contraction — 0 papers

- 2509.20829: [`"population within-class variance is a key factor underlying both grokking"`](../papers/2509.20829.explaining-grokking-and-information-bottleneck-through-neural-collapse-emergence/2509.20829.explaining-grokking-and-information-bottleneck-through-neural-collapse-emergence.card.md#p1-2) — [in the card](../papers/2509.20829.explaining-grokking-and-information-bottleneck-through-neural-collapse-emergence/2509.20829.explaining-grokking-and-information-bottleneck-through-neural-collapse-emergence.card.md#p1-2)

### XOR classification task — 2 papers

- 2504.13292: [`"on a synthetic XOR task where delayed generalization"`](../papers/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model/original/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model.md#p1-3) — [in the card](../papers/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model/original/2504.13292.let-me-grok-for-you-accelerating-grokking-via-embedding-transfer-from-a-weaker-model.md#p1-3)

### Zero-sum gradient constraint — 0 papers

- 2605.06152: [`"This breaks the zero-sum constraint of gradients across classes"`](../papers/2605.06152.grokking-or-glitching-how-low-precision-drives-slingshot-loss-spikes/original/2605.06152.grokking-or-glitching-how-low-precision-drives-slingshot-loss-spikes.md#p1-2) — [in the card](../papers/2605.06152.grokking-or-glitching-how-low-precision-drives-slingshot-loss-spikes/original/2605.06152.grokking-or-glitching-how-low-precision-drives-slingshot-loss-spikes.md#p1-2)
