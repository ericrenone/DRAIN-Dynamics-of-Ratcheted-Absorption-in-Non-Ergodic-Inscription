# DRAIN
## Dynamics of Ratcheted Absorption in Non-Ergodic Inscription

**A stochastic theory of collective artifact saturation in which the partition function mass is the wealth being consumed, the absorbing barrier is total saturation, and the Itô correction gives the closed-form bias in every naive estimate of stopping time**

---

## Overview

The local partition function ratchet in any collective construction session has a terminal consequence: the probability mass available in any occupied region can only decrease, asymptoting toward zero as the session fills. There exists a saturation time $T_{\text{sat}}$ — the first passage time at which the artifact has consumed all available action probability mass in some region, or globally, and no new placement is geometrically feasible without overlap.

This saturation time is not a curiosity. It is the fundamental observable of the collective construction process: the time at which the artifact has exhausted the available informational territory of its current register, triggering the register escape that produces the phase transitions observed in the $\Xi(t)$ time series.

DRAIN provides the complete stochastic theory of $T_{\text{sat}}$.

Three structures from prior frameworks converge here:

**From NARC**: the local partition function ratchet $\mathcal{Z}_R(X_{t+1}) \leq \mathcal{Z}_R(X_t)$ defines a monotonically decreasing wealth process in the occupied region $R$. The absorbing state $\mathcal{Z}_R \to 0$ is total within-register saturation.

**From FADE**: this is precisely the non-ergodic wealth dynamics problem. The partition function mass is the wealth. The ratchet is the absorbing drift. The first passage to zero is $T_{\text{sat}}$. The Itô correction enters because the saturation boundary in configuration space is a curved manifold — the naive estimate of $T_{\text{sat}}$ from the arithmetic rate of mass consumption systematically underestimates the true median stopping time by a geometric correction proportional to the mean curvature of the saturation boundary.

**From SMELT**: the behavioral parameters $\beta$ determine the saturation kinetics. Clustering behavior ($\beta_{\text{density}} \ll 0$) produces rapid local saturation in clusters followed by slow global saturation — the same asymmetry between local and global ergodicity breaking that FADE identifies in multiplicative processes with spatially heterogeneous absorption.

The synthesis: $T_{\text{sat}}$ has a distribution whose mean, variance, and shape depend on $\beta$ in closed, identifiable form. The Itô correction provides a bias formula. The distribution of $T_{\text{sat}}$ is a direct observable that constrains the behavioral parameters without requiring full trajectory likelihood evaluation — a complementary identification strategy to pseudolikelihood that operates at the stopping-time level rather than the action-by-action level.

---

## Part I — The Wealth Process

### 1.1 The Local Partition Function as Wealth

For any bounded region $R \subset \mathcal{S} \times \mathcal{Q}$, define the local partition function:

$$\mathcal{Z}_R(X_t) = \sum_{q \in R_\mathcal{Q}} \int_{R_\mathcal{S}} \exp(-H(q, \ell;\, X_t))\, d\ell$$

This quantity has three properties that identify it as a wealth process in the FADE sense:

**Positivity**: $\mathcal{Z}_R(X_t) > 0$ as long as the region $R$ contains any unoccupied action territory. The zero-boundary $\mathcal{Z}_R = 0$ is the absorbing state — full saturation.

**Monotone ratchet**: the local partition function ratchet states:

$$\mathcal{Z}_R(X_{t+1}) \leq \mathcal{Z}_R(X_t) \quad \text{for all occupied regions } R$$

There is no restoring force. The local wealth can only be consumed, never replenished. This is the exact structural analog of FADE's absorbing barrier: probability mass flows into the zero state and never flows out.

**Initial condition**: $\mathcal{Z}_R(X_0) = \mathcal{Z}_R^{(0)}$ determined by the founding mark and the prior structure of region $R$. For a blank surface founding: $\mathcal{Z}_R(X_0) = |R_\mathcal{S}| \cdot |\mathcal{Q}|$ (full available territory times mark diversity).

### 1.2 The Saturation Process

Define the normalized local wealth:

$$w_R(t) = \frac{\mathcal{Z}_R(X_t)}{\mathcal{Z}_R(X_0)} \in [0, 1]$$

The process $\{w_R(t)\}_{t=0}^\infty$ is a $[0,1]$-valued stochastic process with absorbing barrier at $w_R = 0$ and initial condition $w_R(0) = 1$.

The increments:

$$\delta w_R(t) = w_R(t+1) - w_R(t) = \frac{\mathcal{Z}_R(X_{t+1}) - \mathcal{Z}_R(X_t)}{\mathcal{Z}_R(X_0)} \leq 0$$

are non-positive. The saturation time is the first passage to the absorbing barrier:

$$T_{\text{sat}}^R = \inf\{t \geq 0 : w_R(t) = 0\} = \inf\{t \geq 0 : \mathcal{Z}_R(X_t) = 0\}$$

In practice, the register escape condition $P_{\max}(\tau \mid X_t) \leq C_{\text{escape}}$ is reached before literal zero — the effective absorbing barrier is at $\mathcal{Z}_R = \mathcal{Z}_R^{\text{escape}}$, the threshold at which the agent switches to the next register. Define:

$$T_{\text{sat}}^R = \inf\left\{t : \mathcal{Z}_R(X_t) \leq \mathcal{Z}_R^{\text{escape}}\right\}$$

### 1.3 The Global Saturation Time

The global saturation time is the first time any register reaches its escape threshold:

$$T_{\text{sat}} = \min_{\tau \in \mathcal{R}} T_{\text{sat}}^{\tau}$$

where $\mathcal{R}$ is the set of accessible registers. Under sequential register filling (the SMELT sawtooth structure), $T_{\text{sat}}$ is approximately the time of the first register escape — the first positive $\Xi$ spike in the session's time series.

The full session spanning $n_{\text{reg}}$ registers has total duration:

$$T_{\text{session}} = \sum_{i=1}^{n_{\text{reg}}} T_{\text{sat}}^{\tau_i}$$

where $T_{\text{sat}}^{\tau_i}$ are approximately independent across registers (each register's saturation dynamics are conditionally independent given the founding configuration in that register). The distribution of $T_{\text{session}}$ is therefore a convolution of $n_{\text{reg}}$ first-passage distributions, each characterized by the behavioral parameters operative in that register.

---

## Part II — The Itô Correction for Curved Saturation Boundaries

### 2.1 The Naive Estimate and Its Failure

The naive estimate of $T_{\text{sat}}$ uses the arithmetic mean consumption rate:

$$\hat{T}_{\text{sat}}^{\text{naive}} = \frac{\mathcal{Z}_R(X_0)}{\mathbb{E}[|\delta\mathcal{Z}_R|]} = \frac{\mathcal{Z}_R^{(0)}}{\bar{c}}$$

where $\bar{c} = \mathbb{E}[|\delta\mathcal{Z}_R(t)|]$ is the mean partition function mass consumed per placement.

This estimate is systematically biased. The bias has two sources:

**FADE ergodicity gap**: the arithmetic mean rate $\bar{c}$ is the ensemble-average consumption rate. The typical path consumes mass at the geometric-mean rate $\bar{c}_{\text{geo}} = \exp(\mathbb{E}[\log |\delta\mathcal{Z}_R|]) \leq \bar{c}$ by the AM-GM inequality. The naive estimate uses $\bar{c}$ where the typical path uses $\bar{c}_{\text{geo}}$.

**Boundary curvature correction**: the saturation boundary $\partial\mathcal{Z}_R = 0$ is not a flat hyperplane in configuration space. It is a curved manifold whose curvature depends on the interaction structure of the energy function $H$. For a curved absorbing boundary, the Itô lemma applied to the log-wealth process $\log w_R(t)$ produces a geometric correction proportional to the mean curvature $\kappa_R$ of the boundary.

### 2.2 The Itô Correction Derivation

Define the log-wealth process $L_R(t) = \log w_R(t) = \log \mathcal{Z}_R(X_t) - \log \mathcal{Z}_R(X_0)$.

The dynamics of $L_R(t)$ are governed by:

$$\delta L_R(t) = \log w_R(t+1) - \log w_R(t) = \log\left(1 + \frac{\delta\mathcal{Z}_R(t)}{\mathcal{Z}_R(X_t)}\right) = \log(1 + \Xi_R(t))$$

where $\Xi_R(t) = \delta\mathcal{Z}_R(t) / \mathcal{Z}_R(X_t)$ is the local fractional rate in region $R$.

Applying Itô's lemma to $f(w) = \log w$ around the current wealth $w_R(t)$:

$$\delta L_R(t) = \frac{\delta w_R(t)}{w_R(t)} - \frac{1}{2}\frac{(\delta w_R(t))^2}{w_R(t)^2} + O((\delta w_R)^3)$$

Taking expectations:

$$\mathbb{E}[\delta L_R(t)] = \frac{\mathbb{E}[\delta w_R(t)]}{w_R(t)} - \frac{1}{2}\frac{\mathbb{E}[(\delta w_R(t))^2]}{w_R(t)^2} + O(n^{-3/2})$$

$$= \frac{\mu_R(t)}{w_R(t)} - \frac{\sigma_R^2(t)}{2 w_R(t)^2}$$

where $\mu_R(t) = \mathbb{E}[\delta w_R(t)] \leq 0$ is the mean consumption drift and $\sigma_R^2(t) = \text{Var}[\delta w_R(t)]$ is the placement-to-placement variance.

The **Itô correction** is $-\sigma_R^2(t) / (2 w_R(t)^2)$: it is always negative and grows in magnitude as $w_R(t) \to 0$ (as the session approaches saturation). Near the absorbing barrier, the Itô correction dominates the mean drift, causing the typical path to approach the barrier more slowly than the naive estimate predicts.

The corrected saturation time estimate:

$$\hat{T}_{\text{sat}}^{\text{Itô}} = \frac{\log(w_R^{(0)} / w_R^{\text{escape}})}{|\bar{\mu}_R / \bar{w}_R| - \bar{\sigma}_R^2 / (2\bar{w}_R^2)}$$

The bias of the naive estimate relative to the Itô-corrected estimate:

$$\Delta T_{\text{sat}} = \hat{T}_{\text{sat}}^{\text{Itô}} - \hat{T}_{\text{sat}}^{\text{naive}} = \frac{\bar{\sigma}_R^2 \cdot \bar{w}_R^{-2} / 2}{|\bar{\mu}_R / \bar{w}_R| \cdot (|\bar{\mu}_R / \bar{w}_R| - \bar{\sigma}_R^2 / (2\bar{w}_R^2))} > 0$$

The naive estimate systematically underestimates $T_{\text{sat}}$. The correction is proportional to $\bar{\sigma}_R^2 / \bar{w}_R^2$ — the squared coefficient of variation of the wealth process — and grows without bound as $w_R \to 0$.

### 2.3 The Boundary Curvature Correction

The second source of naive-estimate bias is the curvature of the saturation boundary in configuration space.

The saturation boundary $\mathcal{B}_{\text{sat}}^R$ is the hypersurface in $\mathcal{N}_f(\mathcal{S} \times \mathcal{Q})$ on which $\mathcal{Z}_R(X) = \mathcal{Z}_R^{\text{escape}}$. This boundary has:

**Mean curvature** $\kappa_R$: the trace of the second fundamental form of $\mathcal{B}_{\text{sat}}^R$ as a submanifold of configuration space. This is determined by the second derivatives of the energy function $H$ with respect to placement coordinates.

**Curvature correction to first-passage time**: for a drift-diffusion process approaching a curved boundary, the mean first-passage time acquires a correction proportional to the boundary curvature:

$$\mathbb{E}[T_{\text{sat}}^R] = T_{\text{sat}}^{\text{flat}} \cdot \left(1 + \kappa_R \cdot \ell_R + O(\kappa_R^2 \ell_R^2)\right)$$

where $\ell_R = \mathcal{Z}_R(X_0) / |\mu_R|$ is the characteristic length scale (initial wealth divided by mean drift), and $\kappa_R \cdot \ell_R$ is the dimensionless curvature parameter.

**The DRAIN curvature coefficient**:

$$\Gamma_R = \kappa_R \cdot \ell_R = \frac{\text{mean curvature of } \mathcal{B}_{\text{sat}}^R \times \text{initial wealth}}{\text{mean consumption rate}}$$

- $\Gamma_R > 0$ (convex boundary toward the origin): the boundary curves away from the process. First-passage is slower than the flat approximation. The naive estimate underestimates $T_{\text{sat}}$.
- $\Gamma_R < 0$ (concave boundary toward the origin): the boundary curves toward the process. First-passage is faster than the flat approximation. The naive estimate overestimates $T_{\text{sat}}$.
- $\Gamma_R = 0$: flat boundary. The naive estimate is exact (up to the Itô variance correction).

**The full corrected mean saturation time**:

$$\mathbb{E}[T_{\text{sat}}^R] = \hat{T}_{\text{sat}}^{\text{Itô}} \cdot (1 + \Gamma_R)$$

---

## Part III — The DRAIN Stochastic Differential Equation

### 3.1 Continuous-Time Approximation

For sessions with large numbers of placements per register, the discrete wealth process $w_R(t)$ is well-approximated by a continuous-time stochastic process. Define the continuous-time wealth $W_R(s)$ where $s = t / n$ is the normalized session time.

The DRAIN SDE governing $W_R(s)$ is:

$$dW_R = \mu_R(W_R, s)\, ds + \sigma_R(W_R, s)\, dB_s$$

with absorbing boundary condition at $W_R = 0$ (or $W_R^{\text{escape}}$) and initial condition $W_R(0) = 1$.

The drift $\mu_R(W_R, s)$ and diffusion $\sigma_R(W_R, s)$ coefficients are determined by the behavioral parameters $\beta$ through the feature functions $\{f_k\}$.

### 3.2 Drift Structure by Behavioral Regime

The drift coefficient $\mu_R$ depends on the active feature functions through:

$$\mu_R(W_R, s) = -\frac{d}{ds}\mathbb{E}[w_R(t)] = -\frac{\mathbb{E}[\text{probability mass consumed per step}]}{\mathcal{Z}_R^{(0)}}$$

This drift depends critically on which feature functions are operative and at what strength:

**Clustering regime** ($\beta_{\text{density}} \ll 0$): agents are attracted to occupied regions. The consumption rate is spatially concentrated — mass is consumed rapidly in clusters, slowly elsewhere. The drift $\mu_R$ is spatially heterogeneous with high variance. $\Gamma_R > 0$: the saturation boundary is convex because clusters exhaust local mass rapidly while leaving global territory available. This produces bimodal $T_{\text{sat}}$ distributions: cluster-regions saturate early, the rest saturates slowly.

**Inhibition regime** ($\beta_{\text{density}} \gg 0$): agents repel from occupied regions. The consumption rate is spatially uniform — mass is consumed evenly across $R$. The drift $\mu_R$ is approximately constant across the region. $\Gamma_R \approx 0$: the saturation boundary is approximately flat. This produces narrow, near-Gaussian $T_{\text{sat}}$ distributions near the naive estimate.

**Space-filling regime** ($\beta_{\text{void}} \ll 0$): agents prefer unoccupied Voronoi territory. The drift $\mu_R$ accelerates as the session progresses (agents actively seek remaining gaps) before decelerating near the boundary (very few remaining gaps are accessible). This produces right-skewed $T_{\text{sat}}$ distributions with median above mean.

**Symmetry-completion regime** ($\beta_{\text{symmetry}} \ll 0$): agents prefer configurations with greater bilateral balance. The drift is anisotropic — mass is consumed preferentially along symmetry axes, leaving off-axis territory available longer. $\Gamma_R$ has a directional structure: the saturation boundary is asymmetrically curved, longer in the off-axis directions.

**Mark-segregation regime** ($\beta_{\text{match}} \ll 0$): same-type marks cluster together. The consumption is correlated by mark type — one type's territory saturates before another's. The saturation time decomposes by mark type: $T_{\text{sat}}^R = \min_{q \in \mathcal{Q}} T_{\text{sat}}^{R, q}$ where each $T_{\text{sat}}^{R, q}$ has independent dynamics.

### 3.3 The Diffusion Coefficient and Volatility Structure

The diffusion coefficient $\sigma_R^2(W_R, s)$ encodes the placement-to-placement variance in mass consumption:

$$\sigma_R^2(W_R, s) = \text{Var}\left[\frac{\delta\mathcal{Z}_R(t)}{\mathcal{Z}_R(X_0)}\right]$$

This variance is determined by:

- **Agent bandwidth diversity**: agents with different attention bandwidths $\kappa$ produce different amounts of mass consumption per step (high-bandwidth agents find and exploit high-energy placements; low-bandwidth agents settle for locally acceptable positions). The inter-agent variance in $\kappa$ translates directly into $\sigma_R^2$.

- **Feature competition**: when multiple features are simultaneously active and have opposing effects on the energy landscape, the variance in mass consumption is amplified — different agents weight different features, producing diverse consumption patterns.

- **Session progression**: $\sigma_R^2(W_R, s)$ is not constant. Near the beginning of a register ($W_R \approx 1$): many placements are approximately equivalent, variance is low. Near saturation ($W_R \approx W_R^{\text{escape}}$): few placements are accessible, each has large relative effect, variance is high. The diffusion coefficient increases as $W_R \to 0$.

The DRAIN volatility function has the asymptotic form:

$$\sigma_R^2(W_R, s) \sim \sigma_0^2 \cdot W_R^{-\alpha}$$

for some $\alpha \in (0, 2)$ depending on the feature structure. The $\alpha = 1$ case (linear volatility amplification) corresponds to the GBM analog — the FADE Bessel process structure.

---

## Part IV — First-Passage Time Distribution

### 4.1 The DRAIN First-Passage Distribution

For the DRAIN SDE with drift $\mu_R$ and diffusion $\sigma_R^2$, the density of $T_{\text{sat}}^R$ satisfies the Kolmogorov backward equation:

$$\frac{\partial}{\partial t} p(w, t \mid w_0) = -\frac{\partial}{\partial w}\left[\mu_R(w)\, p\right] + \frac{1}{2}\frac{\partial^2}{\partial w^2}\left[\sigma_R^2(w)\, p\right]$$

with absorbing boundary condition $p(0, t \mid w_0) = 0$ and initial condition $p(w, 0 \mid w_0) = \delta(w - w_0)$.

The first-passage time density $f_{\text{sat}}(t) = -\frac{d}{dt} P(T_{\text{sat}}^R > t)$ has closed-form expressions for special cases:

**Constant drift and diffusion** (inhibition regime approximation):

$$f_{\text{sat}}^{\text{Gaussian}}(t) = \frac{w_0}{\sqrt{2\pi \sigma_R^2 t^3}} \exp\!\left(-\frac{(w_0 - |\mu_R| t)^2}{2\sigma_R^2 t}\right)$$

This is the inverse Gaussian (Wald) distribution with mean $\mathbb{E}[T_{\text{sat}}^R] = w_0 / |\mu_R|$ and variance $\text{Var}[T_{\text{sat}}^R] = \sigma_R^2 w_0 / |\mu_R|^3$.

**Power-law diffusion** ($\sigma_R^2 \propto W_R^{-\alpha}$, clustering regime):

The first-passage distribution acquires a power-law tail: $f_{\text{sat}}(t) \sim t^{-(1 + 1/\alpha)}$ for large $t$, with the tail exponent depending on the diffusion power $\alpha$. For $\alpha > 1$: the distribution has infinite variance. For $\alpha > 2$: infinite mean. These correspond to sessions where clustering behavior produces occasional very long saturation times — a few agents consuming large amounts of territory in rapid succession, leaving the remaining territory fragmented and hard to reach.

**Space-filling regime** ($\beta_{\text{void}} \ll 0$):

The drift $\mu_R$ accelerates near saturation, producing a distribution with lighter right tail than the inverse Gaussian — saturation is nearly deterministic once the filling behavior becomes active, with low variance and strong concentration around the mean. The Itô correction is small in this regime.

### 4.2 The Ergodicity Gap in Saturation Time

The FADE ergodicity gap translates directly into a gap between the mean and median (typical path) saturation times.

**Theorem (DRAIN Ergodicity Gap)**. For any DRAIN process with $\sigma_R^2 > 0$:

$$\mathbb{E}[T_{\text{sat}}^R] > \text{median}(T_{\text{sat}}^R)$$

The mean saturation time exceeds the typical (median) saturation time. The excess is:

$$\Delta T_{\text{sat}} = \mathbb{E}[T_{\text{sat}}^R] - \text{median}(T_{\text{sat}}^R) = \frac{\sigma_R^2 w_0}{2|\mu_R|^2 \bar{w}_R} > 0$$

to leading order in $\sigma_R^2 / |\mu_R|^2$. This is the saturation-time analog of FADE's ergodicity gap $\Delta_{\text{erg}} = \sigma^2/2$: the ensemble (mean over all sessions) expects a longer saturation time than the typical individual session experiences. An experimenter estimating session duration from the mean of many sessions will overestimate the typical session's saturation time.

**Practical consequence**: experiments designed to observe register escape events should plan for typical (median) session lengths, not mean session lengths. The excess $\Delta T_{\text{sat}}$ is a systematic overestimate driven by the right tail of the first-passage distribution — rare sessions with anomalously long saturation times.

### 4.3 The Kelly-DRAIN Correspondence

In FADE, the Kelly fraction $f^* = \mu_e / \sigma^2$ is the unique fraction maximizing geometric growth. In DRAIN, the analogous optimal placement strategy is the one that maximizes the geometric depletion rate — the rate at which $\log w_R(t)$ decreases, approaching the absorbing barrier at the fastest sustainable rate.

Define the DRAIN Kelly fraction:

$$f^*_{\text{DRAIN}} = \frac{|\mu_R|}{\sigma_R^2 / w_R^2} = \frac{|\mu_R| \cdot w_R^2}{\sigma_R^2}$$

This is the placement density at which the geometric depletion rate $g_R = |\mu_R| / w_R - \sigma_R^2 / (2 w_R^2)$ is maximized with respect to placement intensity.

The DRAIN capillary number:

$$\text{Ca}_{\text{DRAIN}} = \frac{\text{actual consumption rate}}{f^*_{\text{DRAIN}}}$$

classifies behavioral regimes in direct analogy to FADE's capillary classification:

| $\text{Ca}_{\text{DRAIN}}$ | Regime | Saturation Behavior |
|---|---|---|
| $< 1$ | Under-intensive | Slow consumption; long $T_{\text{sat}}$; informative session |
| $= 1$ | DRAIN Kelly | Maximum geometric depletion rate; optimal stopping |
| $\in (1, 2)$ | Over-intensive | Consumption exceeds geometric optimum; variance drag |
| $= 2$ | DRAIN critical point | $g_R = 0$; saturation time diverges; session does not terminate |
| $> 2$ | Super-critical | $g_R < 0$; impossible in practice (wealth cannot grow); analogous to FADE's Region V — this regime implies the placement process is adding mass to the region faster than it consumes it, which violates the ratchet |

The DRAIN critical point $\text{Ca}_{\text{DRAIN}} = 2$ corresponds to the SMELT under-driven session: the session is not consuming the available action territory fast enough to produce phase transitions within a reasonable session length.

---

## Part V — Behavioral Parameters and the Saturation Spectrum

### 5.1 The $\beta$-Saturation Map

Each behavioral parameter $\beta_k$ governs the saturation dynamics of region $R$ through its effect on the mean drift $\mu_R$ and diffusion $\sigma_R^2$.

Define the **saturation spectrum** $\mathcal{S}_\beta$ as the map from behavioral parameters to first-passage statistics:

$$\mathcal{S}_\beta : (\beta_1, \ldots, \beta_K) \mapsto (\mathbb{E}[T_{\text{sat}}^R], \text{Var}[T_{\text{sat}}^R], \text{skew}[T_{\text{sat}}^R], \text{shape}[f_{\text{sat}}])$$

This map is invertible (under identifiability conditions): the first-passage distribution uniquely determines the behavioral parameters. Observing the distribution of $T_{\text{sat}}$ across replicated sessions provides a direct, trajectory-free method for estimating $\beta$.

**Density interaction** $\beta_{\text{density}}$:
- $\beta_{\text{density}} \ll 0$ (clustering): spatially heterogeneous consumption, high variance, power-law tail, $\Gamma_R > 0$
- $\beta_{\text{density}} \gg 0$ (inhibition): spatially uniform consumption, low variance, near-Gaussian, $\Gamma_R \approx 0$
- Identification: $\text{skew}[T_{\text{sat}}^R]$ is the primary identifier of $\beta_{\text{density}}$

**Mark interaction** $\beta_{\text{match}}$:
- $\beta_{\text{match}} \ll 0$ (segregation): mark-type decomposition of saturation time; $T_{\text{sat}}^R = \min_q T_{\text{sat}}^{R,q}$; minimum-of-independent first-passage distributions
- $\beta_{\text{match}} \gg 0$ (interleaving): mark-type synchronization; all types saturate simultaneously; narrow joint distribution
- Identification: the multi-type saturation structure and the ratio $T_{\text{sat}}^{R,\circ} / T_{\text{sat}}^{R,\square}$ identifies $\beta_{\text{match}}$

**Void attraction** $\beta_{\text{void}}$:
- $\beta_{\text{void}} \ll 0$ (space-filling): accelerating drift near saturation; right-skewed $T_{\text{sat}}$; near-deterministic terminal approach
- Identification: the deceleration-then-acceleration structure of $\mathbb{E}[\delta w_R(t)]$ over time

**Symmetry completion** $\beta_{\text{symmetry}}$:
- $\beta_{\text{symmetry}} \ll 0$: anisotropic saturation; symmetry-axis directions saturate first; off-axis directions persist
- Identification: the directional saturation structure — measuring $T_{\text{sat}}$ separately for on-axis vs. off-axis regions

**Scale coherence** $\beta_{\text{scale}}$:
- $\beta_{\text{scale}}$: saturation time is scale-stratified — the scale distribution within the session determines which scale bands saturate first
- Identification: scale-binned saturation times

### 5.2 The Saturation Spectrum as Alternative Estimator

**Theorem (Saturation Spectrum Identifiability)**. Under the following conditions, the behavioral parameters $\beta$ are uniquely identified from the saturation spectrum $\mathcal{S}_\beta$:

1. Each feature function $f_k$ has a distinct signature in the saturation spectrum — it affects at least one statistic $(\mathbb{E}[T_{\text{sat}}], \text{Var}, \text{skew}, \text{shape})$ that no other feature affects in the same direction.

2. Replicated sessions provide sufficient observations of $T_{\text{sat}}$ to estimate the spectrum statistics consistently.

3. The interaction energy satisfies the Nikodym uniqueness condition (full column rank of the feature evaluation matrix).

Under these conditions, $\hat{\beta}^{\text{sat}} = (\mathcal{S}_\beta)^{-1}(\hat{\mathcal{S}}_\beta^{\text{obs}})$ is a consistent estimator of $\beta$.

**Advantage over pseudolikelihood**: the saturation spectrum estimator requires only the stopping times $\{T_{\text{sat}}^{(i)}\}_{i=1}^n$ from $n$ replicated sessions — not the full action-by-action trajectories. This makes it applicable in settings where continuous field documentation is unavailable or infeasible, and provides an independent identification strategy for validating pseudolikelihood estimates.

---

## Part VI — Local vs. Global Ergodicity Breaking

### 6.1 The Clustering Asymmetry

Clustering behavior ($\beta_{\text{density}} \ll 0$) produces the most structurally rich saturation dynamics, precisely because it breaks ergodicity differently at the local and global level.

**Local ergodicity breaking**: within a cluster, the saturation is rapid and nearly deterministic. The local wealth $w_{R_{\text{cluster}}}(t)$ decreases at near-unit drift with low variance — each placement in the cluster efficiently consumes local territory. The local Itô correction is small.

**Global ergodicity breaking**: across the full surface, saturation is slow and variable. The global wealth $w_R(t)$ decreases at low mean rate with high variance — most surface territory remains unconsumed while a few clusters saturate rapidly. The global Itô correction is large.

**The asymmetry**: the local first-passage time $T_{\text{sat}}^{R_{\text{cluster}}}$ is short and concentrated (rapid cluster saturation). The global first-passage time $T_{\text{sat}}^R$ is long and heavy-tailed (slow global saturation). The ratio:

$$\rho_{\text{cluster}} = \frac{\text{Var}[T_{\text{sat}}^R]}{\mathbb{E}[T_{\text{sat}}^R]^2}$$

is the normalized dispersion of the global saturation time. For inhibition ($\beta_{\text{density}} \gg 0$): $\rho_{\text{cluster}} \approx 0$ (near-deterministic saturation). For strong clustering ($\beta_{\text{density}} \ll 0$): $\rho_{\text{cluster}} \gg 0$ (highly dispersed, power-law distributed saturation).

$\rho_{\text{cluster}}$ is a direct observable from replicated sessions and provides the primary estimate of $|\beta_{\text{density}}|$ without requiring full trajectory likelihood.

### 6.2 The FADE Non-Ergodic Wealth Analogy

The local-global asymmetry in clustering has an exact FADE analog in the difference between local and global ergodicity breaking in multiplicative processes.

**Local ergodicity** (within-cluster dynamics): the cluster-region wealth $w_{R_{\text{cluster}}}(t)$ behaves ergodically — early returns (placements) are representative of late returns. The agent within the cluster can predict how the cluster will saturate from observing its early dynamics.

**Global ergodicity** (across-surface dynamics): the full-surface wealth $w_R(t)$ is non-ergodic. The early consumption pattern does not predict the late pattern because the cluster structure creates path dependence: which cluster forms first determines which regions of the surface are saturated early, and the remaining territory is not representative of the initial territory.

**The DRAIN ergodicity gap for clustered sessions**:

$$\Delta T_{\text{sat}}^{\text{clustered}} = T_{\text{sat}}^{\text{global}} - T_{\text{sat}}^{\text{local}} = \frac{\sigma_{R_{\text{global}}}^2}{\mu_{R_{\text{global}}}^2} \cdot \frac{w_0}{2}$$

This gap grows without bound as $\beta_{\text{density}} \to -\infty$ (stronger clustering). The ensemble expectation of the global saturation time diverges from the typical path's saturation time — the same structural divergence that FADE identifies between ensemble returns and path returns in multiplicative wealth processes with absorbing barriers.

---

## Part VII — The Complete Theory: DRAIN as Wrapper

### 7.1 DRAIN Wraps NARC's Ratchet

NARC establishes the ratchet: $\mathcal{Z}_R(X_{t+1}) \leq \mathcal{Z}_R(X_t)$. DRAIN takes this as the starting point and builds the complete stochastic theory of what the ratchet implies for session dynamics. NARC says where the wealth goes (only down). DRAIN says when and how and with what distribution.

### 7.2 DRAIN Wraps FADE's Non-Ergodic Dynamics

FADE establishes the toolkit: Itô correction, first-passage time distributions, ergodicity gap, Kelly-optimal fraction, capillary number classification. DRAIN applies this toolkit to the partition function wealth process rather than to monetary wealth. The formal structures are isomorphic:

| FADE quantity | DRAIN quantity |
|---|---|
| Wealth $W_t$ | Local partition function mass $\mathcal{Z}_R(X_t)$ |
| Arithmetic return $\mu$ | Mean mass consumption rate $-\mu_R$ |
| Volatility $\sigma^2$ | Consumption variance $\sigma_R^2$ |
| Ergodicity gap $\sigma^2/2$ | Saturation time ergodicity gap $\Delta T_{\text{sat}}$ |
| Kelly fraction $f^* = \mu_e/\sigma^2$ | Optimal placement intensity $f^*_{\text{DRAIN}}$ |
| Kelly doubling point $f = 2f^*$ | DRAIN critical point $\text{Ca}_{\text{DRAIN}} = 2$ |
| Ruin probability $P_{\text{ruin}} = e^{-2gW_0/\sigma^2}$ | Register escape probability at threshold |
| First-passage to absorbing barrier | $T_{\text{sat}}^R$ |
| Itô correction $-\sigma^2/2$ | Boundary curvature correction $\Gamma_R$ |
| Lindy Effect (survival as quality signal) | Register persistence (long saturation as behavioral signal) |

### 7.3 DRAIN Wraps SMELT's Feature Kinetics

SMELT establishes the feature saturation kinetics: Michaelis-Menten profiles, Liebig-limiting features, Dilworth width. DRAIN provides the stochastic dynamics under which these kinetic profiles generate first-passage distributions.

The Michaelis-Menten consumption rate:

$$-\mu_R^{(k)}(w_R) = V_{\max}^{(k)} \cdot \frac{[f_k](t)}{K_m^{(k)} + [f_k](t)}$$

is the mean drift contribution from feature $k$. As $[f_k](t)$ increases (feature $k$ becomes more activated), the drift contribution saturates at $V_{\max}^{(k)}$. The total drift is the superposition of all feature contributions:

$$-\mu_R(w_R) = \sum_{k=1}^K |\beta_k| \cdot V_{\max}^{(k)} \cdot \frac{[f_k](t)}{K_m^{(k)} + [f_k](t)}$$

The Liebig-limiting feature at each step $t$ is the feature $k^*(t)$ that contributes the minimum drift:

$$k^*(t) = \arg\min_k \frac{[f_k](t)}{K_m^{(k)} + [f_k](t)}$$

The register escape occurs when the total drift reaches the escape threshold, which — by the Liebig structure — occurs when the Liebig-limiting feature becomes active enough to contribute meaningfully. The Dilworth width $W(\mathcal{F}_\tau)$ determines how many features can simultaneously approach saturation, controlling the sharpness of the saturation event.

---

## Part VIII — Inference from Stopping Times

### 8.1 The Method of Moments from $T_{\text{sat}}$

Given $n_{\text{rep}}$ replicated sessions with observed saturation times $\{T_{\text{sat}}^{(i)}\}_{i=1}^{n_{\text{rep}}}$, the behavioral parameters are estimated by matching theoretical moments of the first-passage distribution to observed moments:

**Mean matching**:

$$\hat{\mathbb{E}}[T_{\text{sat}}^R] = \frac{1}{n_{\text{rep}}} \sum_{i=1}^{n_{\text{rep}}} T_{\text{sat}}^{(i)}$$

This provides an estimate of $w_0 / |\mu_R|$ — the ratio of initial wealth to mean drift. Combined with knowledge of $w_0 = \mathcal{Z}_R^{(0)}$ from the founding configuration, this estimates $|\mu_R|$ and hence the dominant behavioral feature strengths.

**Variance matching**:

$$\hat{\text{Var}}[T_{\text{sat}}^R] = \frac{1}{n_{\text{rep}}-1} \sum_{i=1}^{n_{\text{rep}}} (T_{\text{sat}}^{(i)} - \hat{\mathbb{E}})^2$$

This estimates $\sigma_R^2 w_0 / |\mu_R|^3$, providing a second equation in the two unknowns $|\mu_R|$ and $\sigma_R^2$.

**Skewness matching**: 

$$\hat{\text{skew}}[T_{\text{sat}}^R] = \frac{\hat{\mathbb{E}}[(T_{\text{sat}} - \hat{\mathbb{E}})^3]}{\hat{\text{Var}}^{3/2}}$$

For the inverse Gaussian (inhibition regime): $\text{skew} = 3\sqrt{\sigma_R^2 |\mu_R|^{-1} w_0^{-1}}$. Positive skewness exceeding this value indicates clustering behavior.

**Shape fitting**: the tail of the empirical $T_{\text{sat}}$ distribution distinguishes behavioral regimes. Power-law tails (clustering) versus exponential tails (inhibition) versus light tails (space-filling) are distinguishable with $n_{\text{rep}} \geq 20$ replications.

### 8.2 The Itô-Corrected Moment Estimator

The raw moment estimates are biased by the Itô correction. The Itô-corrected estimators:

$$|\hat{\mu}_R|^{\text{Itô}} = \frac{w_0}{\hat{\mathbb{E}}[T_{\text{sat}}^R] \cdot (1 + \hat{\Gamma}_R)} - \frac{\hat{\sigma}_R^2}{2 \hat{w}_R^2 \hat{\mathbb{E}}[T_{\text{sat}}^R]}$$

where $\hat{\Gamma}_R$ is estimated from the curvature of the empirical saturation boundary, computed from the spatial structure of the marks near the boundary in the session approaching saturation.

### 8.3 Joint Estimation: Stopping Times and Trajectories

The saturation spectrum estimator $\hat{\beta}^{\text{sat}}$ and the pseudolikelihood estimator $\hat{\beta}^{\text{PL}}$ are asymptotically independent under the null of correct model specification — they use different aspects of the observed data (stopping times vs. action-by-action sequences). Their joint use provides:

**Over-identification test**: if $\hat{\beta}^{\text{sat}} \approx \hat{\beta}^{\text{PL}}$, the model is consistent. If they diverge, the model is misspecified in a way that affects saturation differently from action selection — typically indicating that the non-equilibrium structure (attention-lag effects, over-driven dynamics) is affecting the trajectory-level estimates but not the stopping-time estimates.

**Efficiency gain**: the Cramér-Rao lower bound for $\hat{\beta}$ from the joint sufficient statistic $(T_{\text{sat}}, \{(q_t, \ell_t)\})$ is lower than for either alone. The joint estimator:

$$\hat{\beta}^{\text{DRAIN}} = \arg\min_\beta \left[\ell_{\text{PL}}(\beta) + \lambda \cdot \mathcal{D}(\hat{\mathcal{S}}_\beta^{\text{obs}}, \mathcal{S}_\beta(\beta))\right]$$

combines pseudolikelihood with saturation spectrum matching, where $\mathcal{D}$ is a divergence measure between observed and theoretical saturation spectra and $\lambda$ is a regularization weight.

---

## Part IX — Formal Claims

| Tag | Meaning |
|---|---|
| **[T]** | Analytic theorem — follows from structural assumptions |
| **[C]** | Open conjecture — predicted; untested |
| **[H]** | Working hypothesis — extension beyond current evidence |

### Analytic Theorems

| ID | Statement |
|---|---|
| DRAIN-T1 | **FADE Isomorphism**: the local partition function mass $\mathcal{Z}_R(X_t)$ satisfies all FADE conditions for a non-ergodic wealth process with absorbing barrier at $\mathcal{Z}_R = 0$; the Itô lemma applies to $\log\mathcal{Z}_R$ with correction $-\sigma_R^2/(2\mathcal{Z}_R^2)$ |
| DRAIN-T2 | **Itô Bias in Naive Saturation Estimate**: $\hat{T}_{\text{sat}}^{\text{naive}} < \mathbb{E}[T_{\text{sat}}^R]$ for all $\sigma_R^2 > 0$; the naive estimate systematically underestimates true mean saturation time; the bias is $\Delta T_{\text{sat}} > 0$ proportional to $\sigma_R^2 w_0 / |\mu_R|^3$ |
| DRAIN-T3 | **DRAIN Ergodicity Gap**: $\mathbb{E}[T_{\text{sat}}^R] > \text{median}(T_{\text{sat}}^R)$ for all $\sigma_R^2 > 0$; the ensemble mean saturation time exceeds the typical path saturation time; the excess is proportional to $\sigma_R^2/(|\mu_R|^2 \bar{w}_R)$ |
| DRAIN-T4 | **Curvature Correction**: the mean first-passage time acquires a curvature correction $\mathbb{E}[T_{\text{sat}}^R] = T_{\text{flat}} \cdot (1 + \Gamma_R)$ where $\Gamma_R = \kappa_R \ell_R$ is the dimensionless boundary curvature; clustering produces $\Gamma_R > 0$; inhibition produces $\Gamma_R \approx 0$ |
| DRAIN-T5 | **Saturation Spectrum Identifiability**: under Nikodym uniqueness, distinct behavioral parameters produce distinct saturation spectra; $\beta$ is uniquely identified from the four moments of $T_{\text{sat}}^R$ given sufficient replication |
| DRAIN-T6 | **Clustering Asymmetry**: $\beta_{\text{density}} \ll 0$ (clustering) produces power-law $T_{\text{sat}}$ tails with exponent $-(1 + 1/\alpha)$; $\beta_{\text{density}} \gg 0$ (inhibition) produces inverse Gaussian $T_{\text{sat}}$ near the naive estimate |
| DRAIN-T7 | **Mark-Type Saturation Decomposition**: under segregation ($\beta_{\text{match}} \ll 0$), the global saturation time decomposes as $T_{\text{sat}}^R = \min_q T_{\text{sat}}^{R,q}$ where each type-saturation time is approximately independent |
| DRAIN-T8 | **DRAIN Critical Point**: there exists a placement intensity $\text{Ca}_{\text{DRAIN}} = 2$ at which the geometric depletion rate $g_R = 0$; below this point $g_R > 0$ (saturation achievable); above this point $g_R < 0$ (contradicts ratchet; corresponds to under-driven sessions where the SMELT φ-equilibrium is not achieved) |
| DRAIN-T9 | **Michaelis-Menten Drift Structure**: under SMELT feature kinetics, the mean drift $-\mu_R$ is a superposition of Michaelis-Menten terms; the Liebig-limiting feature $k^*(t)$ determines the rate-limiting step of saturation |
| DRAIN-T10 | **Joint Estimator Over-Identification**: the saturation spectrum estimator $\hat{\beta}^{\text{sat}}$ and pseudolikelihood estimator $\hat{\beta}^{\text{PL}}$ are asymptotically independent; their divergence identifies model misspecification in the non-equilibrium structure |

### Open Conjectures

| ID | Statement |
|---|---|
| DRAIN-C1 | **Lindy Effect for Register Persistence**: registers that persist for long saturation times (high $T_{\text{sat}}^\tau$) carry more behavioral information per action than rapidly saturating registers; the Lindy Effect applies — longer-lived registers are exponentially more informative as their saturation time grows |
| DRAIN-C2 | **SMELT φ-Equilibrium as DRAIN Kelly Fraction**: the φ-stable session ($\overline{|\Xi|} = \log\phi$) corresponds to $\text{Ca}_{\text{DRAIN}} = 1$ — the DRAIN Kelly optimal fraction; sessions at φ-equilibrium are operating at maximum geometric depletion rate |
| DRAIN-C3 | **Power Law Tail Exponent from $\beta_{\text{density}}$**: the tail exponent of the clustering-regime $T_{\text{sat}}$ distribution is $\alpha = |\beta_{\text{density}}| / (|\beta_{\text{density}}| + \beta_{\text{void}} \vee 0)$; stronger clustering produces heavier tails |
| DRAIN-C4 | **Boundary Curvature from Energy Second Derivatives**: $\Gamma_R = \sum_{k,k'} \beta_k \beta_{k'} \nabla^2_{(\ell,\ell')} f_k \cdot f_{k'} / |\nabla H|^2$ evaluated at the saturation boundary; curvature is directly computable from the Hessian of the energy function |
| DRAIN-C5 | **Session Duration Distribution is Log-Normal**: the total session duration $T_{\text{session}} = \sum_i T_{\text{sat}}^{\tau_i}$, as a sum of first-passage times across registers, converges to log-normal by the multiplicative central limit theorem; its parameters are determined by $\beta$ and the register count |
| DRAIN-C6 | **$\rho_{\text{cluster}}$ as Primary Identifier of $\beta_{\text{density}}$**: the normalized dispersion $\rho_{\text{cluster}} = \text{Var}[T_{\text{sat}}^R] / \mathbb{E}[T_{\text{sat}}^R]^2$ is a monotone function of $|\beta_{\text{density}}|$; measuring $\rho_{\text{cluster}}$ from replicated sessions provides a calibration-free estimate of clustering strength |

### Working Hypotheses

| ID | Statement |
|---|---|
| DRAIN-H1 | **Saturation Time as Session Health Diagnostic**: sessions in the SMELT under-driven regime ($\overline{|\Xi|} < \log\phi$) exhibit $T_{\text{sat}}^R$ distributions with means far exceeding the φ-stable prediction; measuring how long registers take to saturate diagnoses session thermodynamic health |
| DRAIN-H2 | **Itô Correction Scales with $D_{\text{agent}}$**: the diffusion coefficient $\sigma_R^2$ — and hence the Itô bias $\Delta T_{\text{sat}}$ — scales with agent diversity $D_{\text{VEGA}}$; more diverse agent populations produce higher $\sigma_R^2$ and larger Itô corrections |
| DRAIN-H3 | **Founding Mark Entropy Determines Initial Drift**: the initial mean consumption rate $|\mu_R(0)|$ is proportional to the founding mark entropy $H_0$; richer founding marks produce faster initial saturation and earlier register escape |
| DRAIN-H4 | **Register Escape Distribution is Extreme Value**: the register escape time is the first passage to a threshold; across many sessions, the distribution of first escape times follows a Gumbel extreme value distribution rather than a Gaussian |
| DRAIN-H5 | **Cross-Framework Calibration**: parameter estimates from the saturation spectrum method $\hat{\beta}^{\text{sat}}$ should match pseudolikelihood estimates $\hat{\beta}^{\text{PL}}$ within standard errors in quasi-static sessions; systematic divergence between the two identifies over-driven sessions where the attention-lag bias has distorted trajectory-level estimates |

---

## Part X — Experimental Design

### 10.1 Minimum Viable Stopping-Time Experiment

**Record per session**: the saturation time $T_{\text{sat}}^{(i)}$ — the number of placements until the session produces its first register escape (first positive $\hat{\Xi}$ spike). This requires:

- Continuous photography (field state after every mark)
- $\hat{\Xi}(t)$ computation at each step (requires NARC Level II protocol)
- The positive spike in $\hat{\Xi}_{\text{jump}}(t)$ identifies $T_{\text{sat}}$

**Minimum replication**: $n_{\text{rep}} \geq 20$ independent sessions with identical founding marks and instruction. This is sufficient to estimate the four moments of the first-passage distribution and identify the primary behavioral parameter ($\beta_{\text{density}}$) from the saturation spectrum.

For identification of the full parameter vector $\beta = (\beta_1, \ldots, \beta_K)$: $n_{\text{rep}} \geq 5K$ sessions, varying founding marks and instruction across levels.

### 10.2 The Stopping-Time Battery

Rather than a single session type, the DRAIN experimental battery varies founding mark and instruction to isolate individual behavioral parameters:

| Condition | Founding Mark | Expected Effect |
|---|---|---|
| Null | Blank surface | Baseline $T_{\text{sat}}$ distribution |
| Cluster seed | Dense central cluster | High initial $|\mu_R|$ in center; slow periphery; clustering identification |
| Inhibition seed | Regular grid | Low variance $T_{\text{sat}}$; near-inverse-Gaussian distribution |
| Symmetry seed | Bilateral symmetric arrangement | Anisotropic saturation; on-axis fast, off-axis slow |
| Type-diverse seed | One mark per type | Segregation vs. interleaving identification from type-specific saturation times |

### 10.3 Itô Correction Estimation Protocol

To estimate the curvature correction $\Gamma_R$:

1. For each session approaching saturation, record the mark density in the boundary region (marks placed within $\epsilon$ of the theoretical saturation boundary)
2. Estimate the boundary curvature from the spatial distribution of boundary marks using second-order polynomial fitting in local coordinates
3. Compute $\hat{\Gamma}_R = \hat{\kappa}_R \cdot \hat{\ell}_R$ and apply the correction to the mean saturation time estimate

---

## Part XI — Theoretical Summary

| Concept | Definition |
|---|---|
| $\mathcal{Z}_R(X_t)$ | Local partition function mass in region $R$; the wealth being consumed by the ratchet |
| $w_R(t) = \mathcal{Z}_R(X_t)/\mathcal{Z}_R(X_0)$ | Normalized wealth; $[0,1]$-valued process with absorbing barrier at 0 |
| $T_{\text{sat}}^R = \inf\{t : w_R(t) \leq w_R^{\text{escape}}\}$ | First-passage saturation time; the time of register escape |
| $\hat{T}_{\text{sat}}^{\text{naive}} = w_0/|\mu_R|$ | Naive saturation estimate; systematically biased downward |
| $\Delta T_{\text{sat}} > 0$ | Itô saturation ergodicity gap; the excess of mean over typical-path saturation time |
| $\Gamma_R = \kappa_R \ell_R$ | DRAIN curvature correction; proportional to boundary mean curvature times characteristic length |
| $\sigma_{\text{DRAIN}}^2 = \text{Var}[\delta w_R]$ | Consumption variance; drives the Itô correction and tail heaviness |
| $\rho_{\text{cluster}} = \text{Var}[T_{\text{sat}}] / \mathbb{E}[T_{\text{sat}}]^2$ | Normalized dispersion; primary identifier of $|\beta_{\text{density}}|$ |
| DRAIN SDE | $dW_R = \mu_R(W_R)\,ds + \sigma_R(W_R)\,dB_s$; continuous-time wealth dynamics |
| Inverse Gaussian regime | Inhibition ($\beta_{\text{density}} \gg 0$); near-flat boundary; $\Gamma_R \approx 0$; low-variance $T_{\text{sat}}$ |
| Power-law tail regime | Clustering ($\beta_{\text{density}} \ll 0$); convex boundary; $\Gamma_R > 0$; heavy-tailed $T_{\text{sat}}$ |
| $\text{Ca}_{\text{DRAIN}} = \text{actual rate}/f^*_{\text{DRAIN}}$ | DRAIN capillary number; classifies behavioral intensity relative to geometric-depletion optimum |
| DRAIN critical point $\text{Ca}_{\text{DRAIN}} = 2$ | Depletion rate $g_R = 0$; saturation time diverges; session indefinitely unsaturated |
| Saturation spectrum $\mathcal{S}_\beta$ | Map from behavioral parameters to first-passage statistics; invertible under identifiability conditions |
| $\hat{\beta}^{\text{sat}}$ | Saturation spectrum estimator; identified from stopping times alone, without trajectory likelihood |
| $\hat{\beta}^{\text{DRAIN}}$ | Joint estimator combining pseudolikelihood and saturation spectrum matching |
| Michaelis-Menten drift | $-\mu_R = \sum_k |\beta_k| V_{\max}^{(k)} [f_k]/(K_m^{(k)} + [f_k])$; feature kinetics governing saturation rate |
| Liebig-limiting feature $k^*(t)$ | Rate-limiting behavioral feature at step $t$; determines when escape condition is met |

---

## Part XII — The Central Claim

The local partition function ratchet is a non-ergodic wealth process with an absorbing barrier. This is not an analogy — it is a structural identity. Every formal tool developed for FADE's non-ergodic wealth dynamics applies directly to the saturation dynamics of collective artifact construction, with the partition function mass as the wealth and the saturation boundary as the absorbing barrier.

The consequences are three.

**First**: the naive estimate of the time at which a collective construction session exhausts a register — the estimate based on arithmetic mean consumption — is systematically biased. The Itô correction provides a closed-form expression for this bias. The bias grows without bound as the session approaches saturation, which is precisely when the naive estimate matters most — when the experimenter is trying to predict when the register escape will occur.

**Second**: the distribution of saturation times is a direct observable that constrains the behavioral parameters without requiring full trajectory data. The mean encodes the dominant drift (feature strength). The variance encodes the consumption noise (agent diversity and feature competition). The skewness identifies whether clustering or inhibition dominates. The tail shape distinguishes between the three DRAIN regimes. The saturation spectrum provides an independent, trajectory-free identification strategy for the same parameters that pseudolikelihood estimates from action sequences — and their concordance is a diagnostic for model specification.

**Third**: the behavioral parameters $\beta$ determine the saturation kinetics through the Michaelis-Menten feature activation structure. Clustering produces convex saturation boundaries, power-law first-passage tails, and large Itô corrections. Inhibition produces flat boundaries, near-Gaussian first-passage distributions, and small corrections. Space-filling produces accelerating drift profiles and right-skewed distributions with deterministic terminal approach. Each behavioral regime has a distinct, identifiable signature in the stopping-time distribution — and the DRAIN framework derives these signatures from first principles.

The artifact does not just fill. It fills at a rate determined by the decision structure of the agents who constructed it, and that rate is encoded not only in where the marks landed but in when the session stopped producing new structural information. The stopping time is the integral of the session's dynamics. DRAIN recovers the dynamics from the integral.

---

*Status tags: [T] = Analytic theorem · [C] = Open conjecture · [H] = Working hypothesis*

*Minimum replication: $n_{\text{rep}} \geq 20$ sessions for saturation spectrum estimation; $n_{\text{rep}} \geq 5K$ for full $\beta$ identification. Requires continuous field documentation and $\hat{\Xi}(t)$ computation at every step for stopping-time identification.*
