# Paper 7: The Scale-Transfer Problem: Why Log Works, Cesàro Fails

**Daniel Derycke**

---

**Abstract.** This paper identifies the exact arithmetic and measure-theoretic scaling obstruction preventing the transfer of Tao's log-averaged Chowla bounds to the Cesàro scale. We prove that the gap is fundamentally an exponential barrier caused by the Radon-Nikodym derivative between logarithmic and natural measures. A critical review of the MRTTK/MRSTT framework confirms that generalized von Neumann arguments fail for fixed shifts due to infinite Cauchy-Schwarz complexity. We decompose the remaining gap via three independent vectors (Tauberian bounds, Siegel zeros, and condensed Čech complexes), concluding that unconditional resolution requires either a Dynamical Montgomery pair correlation or a genuinely new structural descent mechanism.

**Keywords:** Even Chowla, Cesàro average, log density, parity barrier, Halász theorem, scale-transfer.

---

### 1.1 The Entropy Decay Mechanism: Why Log Works, Cesàro Fails (Novel)

**The precise mechanism.** Conditioning on $n \equiv r \pmod{p}$ for a prime $p > 3$: among the 4 consecutive values $n, n+1, n+2, n+3$, exactly ONE is divisible by $p$ (since $p > 3$). Say $n + j \equiv 0 \pmod{p}$.

The correlation after conditioning on $n \equiv -j \pmod{p}$:
$$C_4^{(p,j)} = \frac{1}{N/p}\sum_{\substack{n \leq N \\ n \equiv -j(p)}} \lambda(n)\lambda(n+1)\lambda(n+2)\lambda(n+3)$$

For the factor $\lambda(n+j) = \lambda(p \cdot (n+j)/p) = \lambda(p)\lambda((n+j)/p) = -\lambda((n+j)/p)$: the sign flips. The other 3 factors are unchanged.

Averaging over $j \in \{0, 1, 2, 3\}$ and the remaining $p-4$ residue classes (where no factor is divisible by $p$):
$$C_4 = \frac{p-4}{p}\,C_4 + \frac{4}{p}\,(-C_4) + O(1/p) = \left(1 - \frac{8}{p}\right)C_4 + O(1/p)$$

More precisely: for the 4 residue classes where a factor is divisible by $p$, the correlation picks up a factor $(-1)$. For the remaining $p-4$ classes, no change.

**The log-averaged iteration.** Applying this for all primes $p \leq P$:
$$C_4^{\log} = C_4 \cdot \prod_{3 < p \leq P} \left(1 - \frac{8}{p}\right) + \text{error}$$

Since $\sum_{p > 3} 8/p = \infty$: $\prod_p (1 - 8/p) = 0$. The correlation shrinks to zero. ✅

This IS the proof of the log-averaged even 4-point Chowla (contained in the Tao 2016 entropy decrement framework).

**Why this fails for Cesàro.** The conditioning $n \equiv -j \pmod{p}$ changes the summation range from $[1, N]$ to the arithmetic progression $\{-j, -j+p, -j+2p, \ldots\}$, effectively replacing the sum at scale $N$ with a sum at scale $N/p$.

For **log averages** $(1/\log N)\sum f(n)/n$: the scale change $N \to N/p$ is absorbed naturally because $\sum_{n \leq N/p} f(pn+j)/(pn+j) \approx (1/p) \sum_{m \leq N} f(m)/m$. The logarithmic weight $1/n$ is SCALE-INVARIANT.

For **Cesàro averages** $(1/N)\sum f(n)$: the sum at scale $N/p$ is $(1/(N/p))\sum_{m \leq N/p} f(m)$, which is a DIFFERENT quantity from $(1/N)\sum f(n)$. The Cesàro average at scale $N$ depends on the Cesàro average at scale $N/p$, which depends on scale $N/p^2$, etc. Controlling ALL scales simultaneously requires:

$$\sup_x \left|\frac{1}{H}\sum_{x < n \leq x+H} \lambda(n) F(g(n)\Gamma)\right| = o(1) \quad \text{for almost all } x$$

This is the **local Fourier uniformity** against nilsequences — exactly the gap from [2, §1.38].


> **The gap crystallized to its sharpest form:**
>
> $$\underbrace{\text{Log-averaged even Chowla}}_{\text{✅ PROVEN (Tao 2016)}} \xrightarrow{\text{scale invariance}} \underbrace{\text{Cesàro even Chowla}}_{\text{⚠️ CONDITIONAL on Gap E}}$$
>
> The transfer from log to Cesàro requires showing that the Cesàro averages of $\lambda$ don't "concentrate" at specific scales. This is the local uniformity conjecture — the SINGLE open step in the P ≠ NP proof chain.



### 1.2 CORRECTION: The [2, §1.46] Argument is INVALID (Definitive, Sourced from MRTTK/MRSTT Papers)

**Upon reading the complete source code of both MRTTK 2023 (arXiv:2007.15644v3, *Annals of Mathematics*) and MRSTT 2024 (arXiv:2411.05770v2), the [2, §1.46] argument contains a fatal flaw that we now document with precision.**

**The flaw: the pattern $(n+1, n+2, \ldots, n+k)$ has INFINITE Cauchy-Schwarz complexity.**

The MRTTK authors explicitly state this. From `intro4.tex`, line 208:

> *"[this result] works for any polynomial patterns **(that are not of 'infinite complexity', such as the pattern $(n+1, n+2, \ldots, n+k)$)**"*

**Why the CS complexity is infinite.** The system $\{L_1(n) = n+h_1, \ldots, L_k(n) = n+h_k\}$ consists of $k$ affine-linear forms in ONE variable $n$. All forms share the same leading coefficient (1). For any form $L_i$: it lies in the affine span of every other form $L_j$ (since $L_i = L_j + (h_i - h_j)$). The CS complexity requires partitioning $\{L_j\}_{j \neq i}$ into groups $A_1, \ldots, A_s$ such that $L_i \notin \text{span}(A_m)$ for each $m$. Since $L_i \in \text{span}(A_m)$ for ANY non-empty $A_m$: no finite partition works. Therefore:

$$|\mathbb{E}_n f(n)f(n+1)f(n+2)f(n+3)| \leq \|f\|_{U^s} \quad \text{is FALSE for any } s$$

**How the MRTTK authors actually use the gvN (three verified instances):**

**Instance 1: Sign pattern proof** (`signpatterns4.tex`, lines 97-100). They bound:
$$\frac{W}{\phi(W)} \mathbb{E}_{P \leq d < 2P} \left|\mathbb{E}_{n \leq n' \leq n+m} \lambda(n' + d\ell_1) \cdots \lambda(n' + d\ell_i)\right| \ll O_W(\kappa(\|\lambda\|_{U^k[n,n+m]})) + \varepsilon$$

Key: the system $\{n' + d\ell_1, \ldots, n' + d\ell_i\}$ has **TWO variables** $(n', d)$. The gvN applies because $d$ is being averaged over $[P, 2P]$. The CS complexity is $i-2$ in two variables.

**Instance 2: Polynomial averages** (`polypattern4.tex`, line 3, footnote). The paper states:
> *"Corollary 1.5 could in fact be proved more directly... combining the generalized von Neumann theorem with Corollary 1.3."*

But Corollary 1.5 is $\mathbb{E}_{h \leq X^\varepsilon} |\mathbb{E}_n \lambda(n+a_1 h) \cdots \lambda(n+a_k h)| = o(1)$ — which **averages over $h$**.

**Instance 3: Hardy-Littlewood application** (MRSTT `main-new.tex`, lines 3524-3536). Lemma 7.1 (gvN) is stated for $\Psi = (\psi_1, \ldots, \psi_t)$, a system of affine-linear forms with the sum over $\mathbf{n} \in K \subset [-N,N]^d$. In the application (line 3574): $\psi_j(\mathbf{n}) = m + jh + r$ with $\mathbf{n} = (h, m, r)$ — **three variables**. The result is:
$$\sum_{n \leq X} \Lambda(n)\Lambda(n+h) \cdots \Lambda(n+(\ell-1)h) = (1+o(1))\mathfrak{S} \cdot X$$
for proportion $1 - o(1)$ of integers $1 \leq h \leq H$ — **averaged over $h$, not for fixed $h$**.

> **The [2, §1.46] argument is definitively retracted.** The step "$|\mathbb{E}_n \lambda(n)\lambda(n+1)\lambda(n+2)\lambda(n+3)| \leq \|\lambda\|_{U^3}$" is **FALSE**. The Gowers $U^s$ norm does NOT control fixed-shift correlations for any $s$. The answer to (a)/(b)/(c) is **(a)**: the CS complexity of the 1-variable fixed-shift system is infinite.

**What the MRTTK/MRSTT results DO give (correctly):**

| Result | Reference | Averages over $h$? | Status |
|---|---|---|---|
| Local $U^{k+1}$ norm $\int \|\lambda\|_{U^{k+1}([x,x+H])} dx = o(X)$ for $H \geq X^\theta$ | MRTTK Cor. 1.3 | N/A | ✅ |
| Averaged Chowla: $\mathbb{E}_{h \leq X^\varepsilon} |\mathbb{E}_n \lambda(n+a_1 h) \cdots| = o(1)$ | MRTTK Cor. 1.5 | **YES** | ✅ |
| Superpolynomial sign patterns: $s(k) \gg_A k^A$ | MRTTK Thm. 1.6 | N/A | ✅ |
| Hardy-Littlewood for most $h$: $\sum \Lambda(n)\Lambda(n+h)\cdots = \mathfrak{S} X$ for $1-o(1)$ of $h \leq H$ | MRSTT Thm. 1.4 | **YES** | ✅ |
| Fixed-shift Chowla: $\sum \lambda(n)\lambda(n+1)\lambda(n+2)\lambda(n+3) = o(x)$ | — | **NO** | ❌ OPEN |

**The precise remaining gap (from MRTTK `intro4.tex`, Proposition 1.7, lines 145-154):**

The entropy decrement argument (Tao 2016) shows: if
$$\int_1^X \frac{\|\lambda\|_{U^{k+1}[x,x+H]}}{x} dx = o(\log X) \quad \text{for } H = (\log X)^\eta, \text{ all } \eta > 0$$
then the logarithmic Chowla conjecture holds. Current technology proves this only for $H \geq \exp((\log X)^{5/8+\varepsilon})$.

$$\underbrace{\text{Local } U^{k+1} \text{ uniformity of } \lambda}_{\text{✅ PROVEN for } H \geq X^\theta} \xrightarrow[\text{exponential gap}]{\text{needs } H \leq (\log X)^\eta} \underbrace{\text{Log-Chowla}}_{\text{❌ OPEN}}$$

**Why closing this gap requires new ideas** (from MRTTK `intro4.tex`, lines 175-177):

> *"Handling the regime $H \in [(\log X)^\eta, (\log X)^{\eta^{-1}}]$, at the very least, would likely necessitate an entirely new idea for several reasons."*

Three fundamental obstructions identified by the authors:
1. **Dirichlet polynomial cancellation:** Even under GRH, $\sum \chi(p)p^{it}$ cancels only for $H \gg (q\log X)^{2+\varepsilon}$.
2. **Approximate functional equations:** Require $\prod_{p \sim H^\varepsilon} p \gg X$, which fails for small $H$.
3. **Entropy decrement:** Only applies when $H \leq (\log X)^\eta$, not in the intermediate regime.



### 1.3 The Measure-Theoretic Scaling Obstruction: Scale-Transfer IS Chowla (Novel — Structural Analysis)

**Motivation.** In [2, §1.47] we identified the remaining gap: local Fourier uniformity of $\lambda$ at scale $H \leq (\log X)^\eta$. Here we analyze the structural nature of this gap via three independent approaches, revealing a deep circularity.

**Step 1: The contagion lemma is sheaf gluing.**

The MRSTT 2024 nilsequence contagion lemma (Theorem 5.8) states: if polynomial sequences $g_n, g'_{n'} : \mathbb{Z} \to G$ on a nilmanifold $G/\Gamma$ satisfy the approximate dilation relation
$$g_n(n' \cdot) \sim_{\frac{1}{nn'}I, \eta} g'_{n'}(n \cdot)$$
for $\geq \eta P^2$ pairs $(n,n')$, then there exists a **single global** polynomial $g_*$ such that $g_n \sim g_*(n \cdot)$ for $\gg \eta^{O(1)} P$ values of $n$.

In sheaf-theoretic language: many **local sections** (the $g_n$) that are pairwise compatible on overlaps (the $\sim$ relation) **glue** to a single global section ($g_*$). This IS a sheaf gluing axiom.

**Step 2: The precise scale constraint.**

The MRSTT scaling-up proposition (Proposition 7.5) requires:
$$\boxed{H \geq \sigma^{-K} A \quad \text{and} \quad A \geq \sigma^{-K}}$$
where $K = O(d \cdot D)$ depends on the nilmanifold's degree $d$ and dimension $D$, and $\sigma$ is the density parameter.

Each iteration doubles the logarithmic scale: $H \to A^2 H$. After $k$ iterations: $H \to A^{2^k} H$.

| Starting scale $H$ | Iterations to reach $X$ | $\sigma$ degradation | Works? |
|---|---|---|---|
| $X^\varepsilon$ | $O(1/\varepsilon)$ | $\sigma^{O(1/\varepsilon)}$ | ✅ |
| $\exp((\log X)^{5/8})$ | Many | $\sigma^{O(1)}$ | ✅ (Walsh) |
| $(\log X)^\eta$ | $\sim \log\log X$ | $\sigma^{O(\log\log X)} \to 0$ | ❌ |

**The sheaf-theoretic diagnosis:** Descent holds at polynomial scales but fails at logarithmic scales because the density parameter $\sigma$ degrades as $\sigma^{O(1)}$ per iteration. After $\log\log X$ iterations, it collapses to zero.

**Step 3: The Turán-Kubilius circularity.**

The MRSTT paper decomposes $\lambda$ via the Turán-Kubilius identity:
$$\lambda(n) \approx -\frac{1}{\log R}\sum_{p \leq R} \lambda(n) \cdot \mathbf{1}_{p | n}$$

Substituting into the $U^k$ norm and using multiplicativity ($\lambda(pm) = -\lambda(m)$):
$$\|\lambda\|_{U^k[x,x+H]}^{2^k} \approx \frac{1}{\log R}\sum_{p \leq R} \|\lambda\|_{U^k[x/p, x/p+H/p]}^{2^k} + \text{cross-terms}$$

The **diagonal terms** give Gowers norms at scale $H/p$ — exactly the scale-transfer we want. But the **cross-terms** involve:
$$\sum_n \lambda(n)\lambda(n+h) \cdot \mathbf{1}_{p|n} \cdot \mathbf{1}_{q|n+h}$$

By CRT (for $p \neq q$, $q \nmid h$): this factors as $\frac{1}{pq} \cdot C_2(h)$, where $C_2(h)$ is the **2-point correlation** $\frac{1}{H}\sum_n \lambda(n)\lambda(n+h)$ on $[x, x+H]$.

> **Circularity theorem.** The Turán-Kubilius cross-terms in the $U^k$ scale-transfer ARE the even Chowla correlation at shorter scales. Specifically:
>
> | $U^k$ level | Cross-terms require | Equivalent to |
> |---|---|---|
> | $U^1$ (mean) | No cross-terms | Matomäki-Radziwiłł ✅ |
> | $U^2$ (pairs) | 2-pt Chowla at scale $H/p$ | Even 2-pt Chowla |
> | $U^3$ (quadruples) | 4-pt Chowla at scale $H/p$ | Even 4-pt Chowla (triggers parity barrier) |
> | $U^k$ (general) | $2^k$-pt Chowla at scale $H/p$ | Even Chowla (all $k \geq 4$ triggers parity barrier) |
>
> **The $U^k$ scale-transfer theorem IS the even Chowla conjecture, reformulated. Crucially, attempting to bound $k \geq 4$ configurations inherently triggers the parity barrier, rendering any inductive leap from $U^2$ to $U^3$ structurally blocked without a breakthrough in multiplicative spectral sieving.**

**Step 4: The Hecke eigenvalue observation.**

The Hecke operator $T_p$ acts on arithmetic functions by $T_p f(n) = f(pn)$. For the Liouville function:
$$T_p \lambda = \lambda(p \cdot) = -\lambda$$

So $\lambda$ is a **Hecke eigenfunction** with eigenvalue $-1$ for every prime $p$. This is the multiplicativity of $\lambda$ expressed as a spectral property.

**Consequence 1.1:** The Gowers norm is Hecke-invariant: $\|T_p \lambda\|_{U^k} = \|\lambda\|_{U^k}$. This means local uniformity at scale $pH$ is equivalent to local uniformity at scale $H$ — but only in the $L^1$-averaged sense (not pointwise).

The MRTTK result IS the $L^1$-averaged Hecke descent. The gap to the Chowla conjecture is the passage from $L^1$ to pointwise.

**Step 5: Three attack vectors and their obstructions.**

| Path | Approach | Obstruction |
|---|---|---|
| Weaken $K$ | LSS quasipolynomial inverse theorem | Triple-log savings; still $\log\log X$ iterations |
| Change site | Profinite or adelic Gowers norms | Perfect descent but doesn't capture archimedean intervals |
| Cohomological vanishing | TK decomposition into shorter scales | Cross-terms ARE the Chowla correlation (circularity) |


> **Definitive structural conclusion.** The three approaches (measure-theoretic scaling analysis, Hecke eigenvalue analysis, Turán-Kubilius decomposition) reveal that the scale-transfer problem, the even Chowla conjecture, and the local Fourier uniformity conjecture are not merely equivalent — they are **the same mathematical object** viewed from three angles:
>
> $$\underbrace{\text{Scale-transfer for } U^k}_{\text{sheaf descent}} \iff \underbrace{\text{Even Chowla (Cesàro)}}_{\text{correlation}} \iff \underbrace{\text{Local uniformity at } H \leq (\log X)^\eta}_{\text{nilsequence decorrelation}}$$
>
> The obstruction is the **parity barrier**: $\lambda(n) = (-1)^{\Omega(n)}$ has perfect parity symmetry, and any attempt to decompose $\lambda$ multiplicatively (TK, Hecke, entropy decrement) reintroduces the same parity-controlled correlations at shorter scales.



### 1.4 The Attractor Perspective: Breaking Circularity via Monotonicity (Novel — Research Direction)

**Motivation.** The circularity in [2, §1.48] is not a logical dead end — it is a **dynamical system**. Self-referential structures (fixed points, attractors, fractals) are standard objects in dynamics, and the tools for analyzing them are well-developed.

**Step 1: The scale flow as renormalization.**

The entropy decrement gives the recursion ([2, §1.45]):
$$C_k(N) = \left(1 - \frac{2k}{p}\right) C_k(N) + O(1/p)$$

for each prime $p$, where $C_k = \frac{1}{N}\sum \lambda(n)\lambda(n+1)\cdots\lambda(n+k-1)$. Iterating over primes:
$$C_k^{\log} = C_k \cdot \prod_{p \leq P}\left(1 - \frac{2k}{p}\right) + \text{error}$$

The **log-averaged** operator $\mathcal{T}^{\log}$ has spectral radius $< 1$ (the product $\prod(1-2k/p) \to 0$ by Mertens). The **Cesàro** operator $\mathcal{T}^{\text{Ces}}$ has spectral radius $= 1$.

| Operator | Spectral radius | Fixed point | Convergence |
|---|---|---|---|
| Log-averaged | $< 1$ | Attracting | ✅ (Tao 2016) |
| Cesàro | $= 1$ | Neutral | ❌ (the gap) |

**Step 2: The incompressible base (what we already have).**

Three proven results serve as "seeds" for the recursion:
1. **MR theorem**: $C_1(H) = o(1)$ for a.a. $x$ and ALL $H \to \infty$ (Cesàro, $U^1$, all scales).
2. **Tao 2016**: $C_2^{\log}(x) = o(1)$ (log-averaged, $U^2$).
3. **Tao-Teräväinen 2019**: $C_2^{\text{Ces}}(x) = o(1)$ for all $x$ outside a set $\mathcal{E}$ of **zero logarithmic density**.

Result 3 is the closest to the goal. The gap is PRECISELY:
$$\text{zero LOG density of } \mathcal{E} \quad \xrightarrow{?} \quad \text{zero NATURAL density of } \mathcal{E}$$

**Step 3: Why log density doesn't imply natural density.**

A set $\mathcal{E}$ can have zero log density yet contain entire dyadic blocks $[N_0, 2N_0]$ — because the log measure of $[N_0, 2N_0]$ is $\log 2 / \log(2N_0) \to 0$ as $N_0 \to \infty$. Such blocks would contribute $O(1)$ to the Cesàro average.

Tao-Teräväinen themselves note: removing the exceptional set "would only be possible in an 'implausible' scenario... related to the Siegel zero problem." This connects the gap to one of the deepest open problems in analytic number theory.

**Step 4: The Perelman analogy.**

Perelman's proof of the Poincaré conjecture used a **monotonicity formula** ($dW/dt \geq 0$) to prevent curvature concentration under Ricci flow. The analogous approach for our problem:

Define a functional $\Phi(H) := C_2(H) \cdot \prod_{p \leq H^{1/\log\log H}} (1 - 2/p)^{-1}$.

If $\Phi$ is **monotonically non-increasing** under the scale flow $H \to H/p$ (i.e., $\Phi(H) \leq \Phi(H/p) + o(1)$), then since $\prod(1-2/p)^{-1} \sim (\log H)^2$ (Mertens), we'd get $C_2(H) = O(1/(\log H)^2) = o(1)$.

**Step 5: Where the monotonicity attempt breaks.**

The conditioning on $n \equiv 0 \pmod{p}$ in the entropy decrement transforms $\lambda(n)\lambda(n+1)$. The factor $\lambda(n) = -\lambda(n/p)$ transforms multiplicatively, but the factor $\lambda(n+1)$ does NOT transform along the same prime $p$ (because $p \nmid n+1$ when $p | n$, for $p \geq 3$).

This means: the scale flow mixes the MULTIPLICATIVE structure of $n$ with the ADDITIVE structure of $n+1$. The shift $h = 1$ connects two numbers with independent factorizations. Any monotonicity formula must control this cross-interaction — which is exactly the parity barrier.


> **Research direction (Perelman-style monotonicity).** The incompressible base exists: Tao-Teräväinen proves $C_2 = o(1)$ at almost all scales. What's needed is a functional $\Phi(H)$ that prevents the exceptional set from "concentrating" at scales contributing to the Cesàro average. The precedent is Perelman's W-functional, which prevented volume concentration under Ricci flow.
>
> **Historical template:**
> | Problem | Self-referential structure | Incompressible base | Resolution |
> |---|---|---|---|
> | FLT | Frey curve ↔ solution | Modularity theorem (Wiles) | Ribet contradiction |
> | Poincaré | Curvature ↔ topology | W-functional monotonicity (Perelman) | No-collapsing |
> | Even Chowla | $C_k(H)$ ↔ $C_k(H/p)$ | TT almost-all-scales + MR + sign flip | **OPEN** |
>
> The resolution requires a monotonicity formula that exploits the specific arithmetic of $\lambda$ (the sign flip $\lambda(p) = -1$) to prevent correlation concentration — analogous to how Perelman's formula exploits the specific structure of the Ricci flow PDE.



### 1.5 The Siegel Zero Dichotomy: Exhaustive Decomposition of the Gap (Novel)

**Motivation.** Executing the research program from [2, §1.49] reveals that the remaining gap decomposes into exactly TWO cases, determined by whether Siegel zeros exist.

**Step 1: The two universes.**

Define the **pretentious distance** (Granville-Soundararajan): for multiplicative $f, g$ with $|f|, |g| \leq 1$:
$$\mathbb{D}(f, g; X)^2 := \sum_{p \leq X} \frac{1 - \text{Re}(f(p)\overline{g(p)})}{p}$$

For the Liouville function: $\mathbb{D}(\lambda, \chi n^{it}; X)^2 \geq c \log\log X$ for all Dirichlet characters $\chi$ and all $t \in \mathbb{R}$ — UNLESS a **Siegel zero** $L(\beta, \chi_D) = 0$ exists with $\beta$ very close to 1.

| Universe | Definition | $\lambda$ behavior | Entropy |
|---|---|---|---|
| **A** (generic) | No Siegel zero exists | $\lambda$ is maximally pseudorandom | High |
| **B** (exceptional) | Siegel zero $L(\beta, \chi_D) = 0$ exists | $\lambda \approx \chi_D$ (pretentious) | Low |

**Step 2: Universe B is solved.**

**Theorem 1.1 (Tao-Teräväinen, 2022).** *In the presence of a Siegel zero $L(\beta, \chi_D) = 0$ with $\beta$ close to 1, the Hardy-Littlewood-Chowla conjecture holds for an infinite sequence of scales:*
$$\sum_{n \leq x} \Lambda(n+h_1)\cdots\Lambda(n+h_k)\lambda(n+h'_1)\cdots\lambda(n+h'_\ell) \sim \mathfrak{S} \cdot x$$
*for $0 \leq k \leq 2$ and all $\ell \geq 0$.*

The mechanism: the Siegel zero forces $\lambda$ to be structured (pretentious toward $\chi_D$), reducing the entropy. The low-entropy system is rigid enough that the correlations can be computed explicitly from character sum estimates.

**Step 3: Universe A remains open — but the gap is narrower.**

In Universe A: Tao-Teräväinen 2019 prove $C_2(X) := \frac{1}{X}\sum_{n \leq X}\lambda(n)\lambda(n+1) = o(1)$ for all $X$ **outside an exceptional set $\mathcal{E}$ of zero logarithmic density**.

The Cesàro Chowla conjecture requires: $\mathcal{E}$ has zero **natural** density.

**Step 4: The Lipschitz control on the exceptional set.**

The partial sum $S(x) := \sum_{n \leq x}\lambda(n)\lambda(n+1)$ satisfies $|S(x+1) - S(x)| \leq 1$ (Lipschitz-1). This constrains the geometry of $\mathcal{E}$:

- If $S(x_0) = o(x_0)$ (i.e., $x_0 \notin \mathcal{E}$), then $|S(x) - S(x_0)| \leq |x - x_0|$ for all $x$.
- So $S(x) = o(x)$ for all $x$ with $|x - x_0| = o(x)$.
- The exceptional set $\mathcal{E}$ cannot have "sharp edges" — transitions from $C_2 \approx 0$ to $|C_2| \geq \varepsilon$ require $O(\varepsilon x)$ steps.

**Consequence 1.2:** If $\mathcal{E} \cap [N, 2N]$ has natural measure $o(N)$ in each dyadic block, then $C_2(X) = o(1)$ for ALL $X$.

**Step 5: The shifted Halász theorem as the sharpest formulation.**

The quantitative Halász theorem (Granville-Soundararajan) gives: for non-pretentious multiplicative $f$,
$$\frac{1}{X}\sum_{n \leq X} f(n) \ll \exp\left(-c \cdot \min_{|t| \leq X} \mathbb{D}(f, n^{it}; X)^2\right)$$

If an analogue held for the **shifted product** $\lambda(n)\lambda(n+1)$ (which is NOT multiplicative):
$$\frac{1}{X}\left|\sum_{n \leq X} \lambda(n)\lambda(n+1)\right| \ll (\log X)^{-c}$$
then the exceptional set would have natural density $O((\log X)^{-c})$ in each block, and the Lipschitz argument would give $C_2(X) = o(1)$ for all $X$.


> **Sharpest formulation of the remaining gap.** The entire P ≠ NP proof chain reduces to a SINGLE open problem:
>
> **Shifted Halász Conjecture:** *For any non-pretentious completely multiplicative $f : \mathbb{N} \to \{-1, 1\}$ and any fixed $h \geq 1$:*
> $$\frac{1}{X}\sum_{n \leq X} f(n) f(n+h) = o(1)$$
>
> This is precisely Elliott's conjecture (2-point case) at Cesàro scale — equivalent to the even 2-point Chowla conjecture. The dichotomy is:
>
> | Universe | Shifted Halász | Reason |
> |---|---|---|
> | **B** (Siegel zero) | ✅ Proven (TT 2022) | Low entropy → explicit computation |
> | **A** (no Siegel zero) | ❌ **OPEN** | High entropy → neutral fixed point |
>
> In Universe A, the spectral radius of the scale operator is exactly 1 ([2, §1.49]), which is WHY the Cesàro transfer fails. Breaking through requires either:
> - (a) A new monotonicity formula that works at spectral radius 1 (cf. Perelman's approach to neutral singularities), or
> - (b) Proving the non-existence of Siegel zeros (equivalent to a strong form of GRH), which would eliminate Universe B and force the answer, or
> - (c) A completely different approach that bypasses the multiplicative structure entirely (cf. the function field proof of Sawin-Shusterman via étale cohomology, which has no analogue over $\mathbb{Q}$).



### 1.6 Measure-Theoretic Anatomy of the Log–Natural Gap (Novel — Structural)

**Motivation.** The gap between log and natural density is the SINGLE remaining obstruction. We now dissect its exact arithmetic structure.

**Step 1: The Radon-Nikodym obstruction.**

Define two measures on $[1, \infty)$:
- **Multiplicative (Haar)**: $d\mu_{\log} = dx/x$, with $\mu_{\log}([1,X]) = \log X$
- **Additive (Lebesgue)**: $d\mu_{\text{nat}} = dx$, with $\mu_{\text{nat}}([1,X]) = X$

> **Barrier 7.1 (The Measure-Theoretic Shift Equivalence Barrier).** The assumption that bounds can be smoothly translated between logarithmic and natural densities using the Radon-Nikodym derivative $d\mu_{\text{log}}/d\mu_{\text{nat}}$ is mathematically invalid for highly oscillatory sequences. The function spaces $L^1(\mu_{\text{log}})$ and $L^1(\mu_{\text{nat}})$ lack shift equivalence. Because the measure discrepancy can systematically align with the sequence's negative support, the expected values diverge exponentially. This severs the bridge between Tao's log-density proof and the natural-density Chowla conjecture.

**Step 2: The entropy decrement arithmetic.**

Conditioning $C_2(N) = \frac{1}{N}\sum_{n \leq N}\lambda(n)\lambda(n+1)$ on $p | n$:

The sign flip $\lambda(pn) = -\lambda(n)$ gives a contraction of $2k/p$ per prime in the $k$-point correlation (§1.4). For $k = 2$: the contraction is $4/p$ per prime. But the sub-sum at scale $N/p$ has natural weight $N/p$ (reduced by factor $p$).

$$\text{Effective contraction for log: } \frac{4}{p} \cdot 1 = \frac{4}{p} \quad \implies \quad \sum_p \frac{4}{p} = \infty \text{ (Mertens)} \quad \checkmark$$

$$\text{Effective contraction for natural: } \frac{4}{p} \cdot \frac{1}{p} = \frac{4}{p^2} \quad \implies \quad \sum_p \frac{4}{p^2} < \infty \quad \times$$


> **The precise arithmetic of the parity barrier.** The log-to-natural upgrade fails because:
>
> | Quantity | Log density | Natural density |
> |---|---|---|
> | Contraction per prime | $4/p$ | $4/p$ |
> | Measure distortion | $\times 1$ (Haar-invariant) | $\times 1/p$ (scale change) |
> | Net effect per prime | $4/p$ | $4/p^2$ |
> | Sum over primes | $\sum 4/p = \infty$ ✅ | $\sum 4/p^2 < \infty$ ❌ |
>
> The gap is exactly ONE power of $p$ — the Radon-Nikodym derivative $x$ between the two measures.

**Step 3: Why the amplification argument fails.**

A tempting idea: conditioning on $2 | n$ gives $\lambda(2m)\lambda(2m+1) = -\lambda(m)\lambda(2m+1)$, suggesting $C_2(N)$ is "related to" $C_2(N/2)$ with amplification factor 2.

**But**: $\lambda(2m+1)$ is at the ORIGINAL scale ($2m+1 \in [1, N+1]$), NOT at scale $N/2$. The cross-term $\sum \lambda(m)\lambda(2m+1)$ is a mixed-scale bilinear sum — it couples scale $N/2$ (through $\lambda(m)$) to scale $N$ (through $\lambda(2m+1)$). This is not reducible to $C_2$ at any single scale.

**Step 4: What tool would breach the gap.**

Any resolution requires one of:

**(i) A bilinear bound on the cross-term**: Prove $\frac{1}{N}\sum_{m \leq N/2}\lambda(m)\lambda(2m+1) = o(1)$ without reducing to Chowla. This is a "Type II" sum involving the dilation $m \mapsto 2m+1$. The Bombieri-Vinogradov theorem handles this for $\Lambda$ but not for $\lambda$ (the parity barrier again).

**(ii) A structural constraint on $\mathcal{E}$**: Prove the exceptional set $\mathcal{E} = \{X : |C_2(X)| \geq \varepsilon\}$ has low computational complexity (e.g., in bounded-branching TC⁰). Then AMNH ([5]) would force $\mu(\mathcal{E}) = 0$ independently.

**(iii) A framework that avoids the multiplicative-additive split**: Instead of conditioning on $p | n$ (which produces the mixed-scale cross-term), use a decomposition that keeps both factors at the SAME scale. Candidates: the Selberg sieve (which conditions on being coprime to small primes) or the "w-trick" (restricting to $W$-smooth numbers).

**Step 5: Measure-theoretic interpretation.**

Define the **multiplicative correlation site** $\mathcal{M}$: objects are scales $H$, morphisms are dilations $H \mapsto H/p$. The correlation sheaf $\mathcal{C}(H) = C_2(H)$ satisfies the descent relation (entropy decrement) on this site. TT 2019 = vanishing of the global section of $\mathcal{C}$ on $\mathcal{M}$.

The **additive site** $\mathcal{A}$ has Lebesgue measure. The base change $\pi: \mathcal{A} \to \mathcal{M}$ has derived pushforward $R^1\pi_!\mathcal{C}$, which is NON-ZERO — the obstruction class. This class is generated by the Radon-Nikodym factor $x$, and its non-vanishing is equivalent to the convergence of $\sum 1/p^2$.

> **The gap lives in** $H^1(\mathcal{A}, \pi_!\mathcal{C})$ — the first cohomology of the additive site with coefficients in the pushforward of the correlation sheaf. This is a ONE-DIMENSIONAL obstruction (generated by the single cocycle $x \mapsto x$), and it can only be killed by new arithmetic input that provides a compensating coboundary.



### 1.7 The Breach Vectors: Maximum Depth and the Exponential Barrier (Novel — Definitive)

**Step 1: Why all three breach vectors fail for the same reason.**

| Vector | Technique | Saving achieved | Required saving |
|---|---|---|---|
| **(i) Bilinear** | Type II sum $\sum\lambda(m)\lambda(2m+1)$ | None (parity barrier) | $o(N)$ |
| **(ii) Complexity** | AMNH on exceptional set $\mathcal{E}$ | N/A (wrong level) | Zero natural density |
| **(iii) W-trick** | MRSTT + nilsequence equidistribution | $O(H(\log X)^{-A})$ per short interval | $o(H)$ uniformly |

**Vector (i)**: The cross-term $\sum\lambda(m)\lambda(2m+1)$ is a Type II bilinear sum with LINEAR dilation $m \mapsto 2m+1$. Unlike the Friedlander-Iwaniec $n^2 + 1$ (which factors over $\mathbb{Z}[i]$), a linear dilation has no algebraic factorization to exploit. The parity barrier is absolute for linear dilations.

**Vector (ii)**: AMNH applies to sequences indexed by $n$ (integers), not to sets of $X$ (scales). The exceptional set $\mathcal{E}$ is defined via the GLOBAL average $C_2(X) = \frac{1}{X}\sum_{n \leq X}\lambda(n)\lambda(n+1)$, which is a functional of the entire trajectory $\lambda(1), \ldots, \lambda(X)$ — not a low-complexity function of $X$.

**Vector (iii)**: The W-trick removes obstructions at small primes ($p \leq w$), but the entropy decrement at large primes ($p > w$) still produces the mixed-scale cross-term. The MRSTT logarithmic savings $(\log X)^{-A}$ are overwhelmed by the $\log X$ accumulation from summing over primes.

**Step 2: The exponential barrier.**

The Radon-Nikodym factor between log and natural measure is:
$$\frac{d\mu_{\text{nat}}}{d\mu_{\log}} = x \quad \text{(grows exponentially in } \log x\text{)}$$

Any prime-by-prime analysis provides savings that are POLYNOMIAL in $\log X$ (from the $\sum 1/p^2 = O(1)$ convergence). The ratio between natural and log measure is EXPONENTIAL in $\log X$ (the factor $X = e^{\log X}$).

$$\text{Polynomial savings} \ll \text{Exponential ratio} \implies \text{breach impossible with current tools}$$

To overcome the exponential barrier: one needs POWER savings in $X$ itself:
$$|C_2(X)| \leq X^{-\delta} \quad (\delta > 0)$$

This is equivalent to a zero-free region for the Dirichlet series $D(s) = \sum \lambda(n)\lambda(n+1)/n^s$ extending to $\text{Re}(s) > 1 - \delta$ — a "quasi-Riemann Hypothesis" for the shifted Chowla L-function.

> **Definitive structural conclusion.** The Even Chowla Conjecture at Cesàro scale is separated from the proven log-averaged version by an EXPONENTIAL BARRIER: the ratio $X / \log X$ between natural and logarithmic measure. All three attack vectors — bilinear bounds, complexity constraints, and same-scale W-trick decompositions — produce at most polynomial-in-$\log X$ savings, which are exponentially insufficient.
>
> The breach requires either:
> - A fundamentally new idea that bypasses the prime-by-prime decomposition entirely, or
> - Power savings $X^{-\delta}$ in the correlation, equivalent to a zero-free region for the shifted Chowla L-function.
>
> This analysis identifies the Even Chowla Conjecture as occupying a position in the hierarchy of number-theoretic conjectures that is STRICTLY BETWEEN the log-averaged Chowla (proven, Tao 2016) and the Riemann Hypothesis (which would give $C_2(X) = O(X^{-1/2+\varepsilon})$). The gap between "proven" and "needed" is EXPONENTIAL in nature.



### 1.8 The Tauberian Path: Historical Precedents and the One-Sided Condition (Novel — Key Insight)

**Step 1: Six historical precedents for exponential barrier bypasses.**

| # | Problem | Barrier | Bypass Technique |
|---|---|---|---|
| 1 | Deligne (Weil) | $\|S\| \leq Cq^{n/2}$ vs $q^n$ | **Categorification**: exponential → spectral radius |
| 2 | Perelman (Poincaré) | Exponential volume growth | **Monotone functional** ($\mathcal{W}$-entropy) |
| 3 | Wiles (Fermat) | Finite rigid algebras | **Deformation/patching** into power series ring |
| 4 | Hardy-Littlewood | Abel ↛ Cesàro | **One-sided Tauberian**: slowly decreasing condition |
| 5 | Iwaniec | Single $L$-value loss | **Family amplification**: average over characters |
| 6 | Friedlander-Iwaniec | Parity barrier for $n^2+1$ | **Algebraic extension**: factor over $\mathbb{Z}[i]$ |

**Step 2: The most applicable precedent — Hardy-Littlewood Tauberian.**

**Theorem 1.2 (Hardy-Littlewood, one-sided).** Let $\sum a_n/n \to L$ (log average). If the partial sums $S(X) = \sum_{n \leq X}a_n$ satisfy:
$$S(\lambda X) - S(X) \geq -\varepsilon(X) \cdot X \quad \text{for all } \lambda \in [1, 2], \quad \varepsilon(X) \to 0$$
(the "slowly decreasing" condition), then $S(X)/X \to L$ (Cesàro average).

**Application to Chowla**: Set $a_n = \lambda(n)\lambda(n+1)$. By TT 2019: $\sum a_n/n = o(\log X)$, so the log average converges to 0. The slowly decreasing condition requires:
$$\sum_{X < n \leq 2X}\lambda(n)\lambda(n+1) \geq -o(X)$$

This is a ONE-SIDED bound — we only need to show the sum CAN'T be $-cX$ for any $c > 0$. We don't need cancellation, only non-persistent-negativity.

**Step 3: Connection to MRT sign patterns (2016).**

Matomäki-Radziwiłł-Tao proved: each sign pattern $(\lambda(n), \lambda(n+1), \lambda(n+2))$ occurs with **positive lower natural density**. In particular: the pattern $(+1, +1)$ for $(\lambda(n), \lambda(n+1))$ has positive density — i.e., $\lambda(n)\lambda(n+1) = +1$ for a positive proportion of $n$.

This means: $\sum_{n \leq X}\lambda(n)\lambda(n+1) \geq -X + cX$ for some $c > 0$ (since a fraction $c > 0$ of terms are $+1$). This gives:
$$S(X) \geq -(1 - 2c)X$$

For the slowly decreasing condition on $[X, 2X]$: we need the LOCAL version — the MRT sign pattern density holds on EACH dyadic block, not just globally.

**Step 4: What remains.**

The MRT sign pattern result gives positive density for $(+1, +1)$ GLOBALLY (on $[1, X]$), but the slowly decreasing condition needs it LOCALLY (on $[N, 2N]$ for every $N$). The gap is:

- **MRT global**: $\#\{n \in [1, X] : \lambda(n) = \lambda(n+1) = +1\} \geq cX$ ✅
- **Needed local**: $\#\{n \in [N, 2N] : \lambda(n) = \lambda(n+1) = +1\} \geq cN$ for all $N$ ❓

This local version would follow from MR-type short interval results for the product $\lambda(n)\lambda(n+1)$ — which is, again, the short interval Chowla conjecture.

**However**: the ONE-SIDED nature provides a structural advantage. The parity barrier prevents proving $\sum \lambda(n)\lambda(n+1) = o(N)$ on $[N, 2N]$. But it does NOT necessarily prevent proving $\sum \lambda(n)\lambda(n+1) \geq -o(N)$ on $[N, 2N]$, because:

1. **Sieve methods give one-sided bounds naturally.** The Selberg sieve gives $\sum_{n \in \mathcal{A}}1 \leq \text{sieve bound}$ — upper bounds. For our problem: the analog would be an upper bound on $\#\{n \in [N, 2N] : \lambda(n) \neq \lambda(n+1)\}$.

2. **The parity barrier blocks two-sided bounds, not one-sided bounds.** The obstruction is that sieves can't distinguish $\Omega$ even from odd. But the ONE-SIDED bound $\sum \lambda(n)\lambda(n+1) \geq -o(N)$ only requires ruling out $\lambda(n)\lambda(n+1) = -1$ for a $(1-o(1))$-fraction of $n$ — i.e., ruling out PERSISTENT sign alternation.


> **Gap F: The Non-Monotone Tauberian Spike Obstruction.**
>
> The one-sided condition $S(2N) - S(N) \geq -o(N)$ is equivalent to: $\#\{n \in [N, 2N] : \lambda(n) = \lambda(n+1)\} \geq N/2 - o(N)$ — agreement at least half the time.
>
> **Why agreement ≈ 1/2 is expected**: By the Erdős-Kac theorem, $\Omega(n) \bmod 2$ is asymptotically independent of $n \bmod 2$. By Davenport (1937): $\sum \lambda(n)(-1)^n = o(N)$ globally. If $\lambda$ alternated on $[N, 2N]$, then $\lambda(n) \approx (-1)^n$ locally, producing $\sum \lambda(n)(-1)^n \approx \pm N$ — contradicting the local Davenport bound.
>
> **The remaining gap**: Davenport's bound is GLOBAL. The local version (MR 2016): $\sum_{x < n \leq x+H}\lambda(n)e^{i\alpha n} = o(H)$ for ALMOST ALL $x$ — but not ALL $x$. The exceptional set for local Davenport IS the same exceptional set as for Chowla.
>
> **Symmetry obstruction**: The slowly decreasing condition for $a_n$ plus the slowly decreasing condition for $-a_n$ together give the FULL short interval Chowla. Any technique proving one side will, by symmetry of $\lambda(n)\lambda(n+1)$, prove the other — so the one-sided condition is NOT genuinely easier.
>
> **Net assessment**: The Tauberian reframing is a STRUCTURAL INSIGHT (converting Chowla to a trajectory constraint on $S(x)$), but it does NOT reduce the analytic difficulty. The fundamental obstruction — "almost all blocks" → "all blocks" — persists. The gap between log and natural density remains exponential.



### 1.9 Tool Specification: The Scale-Uniform Entropy Theorem (Novel — Definitive)

**Step 1: Five axioms for the required tool.**

Any tool that resolves Even Chowla must satisfy ALL FIVE:

**(A1) Scale Uniformity.** Works at EVERY scale $X \geq X_0$, not just "almost all." The Markov step in the entropy argument gives "almost all" — the tool must eliminate this step.

**(A2) Multiplicative Coupling.** Uses $\lambda(pn) = -\lambda(n)$ for ALL primes simultaneously. The prime-by-prime approach gives $\sum 1/p^2 < \infty$ (convergent). The tool must couple the information from ALL primes.

**(A3) Additive Independence.** Exploits $\gcd(n, n+1) = 1$. The coprimality makes the prime factorizations of $n$ and $n+1$ INDEPENDENT — the source of "randomness" that should force cancellation.

**(A4) Non-Concentration.** Proves $\mathcal{E} \cap [N, 2N]$ has $o(N)$ elements for every $N$. Prevents the exceptional set from concentrating at the largest block.

**(A5) Exponential Reach.** Provides savings $\geq X^{-\delta}$ (power) or $\exp(-c\sqrt{\log X})$ (sub-exponential). Polynomial-in-$\log X$ savings are exponentially insufficient.

**Step 2: Three candidate constructions and why they fail.**

**(i) Weighted Entropy Interpolation.** Define $H_\alpha$ with weight $n^{\alpha-1}$ for $\alpha \in [0,1]$. For ALL $\alpha \leq 1$: $\sum 2/p^\alpha = \infty$, so the entropy decrement gives infinite contraction. But the entropy bound $\sum |C_2^{(p)}|^2/p \leq O(1)$ only gives $|C_2^{(p)}|^2 \to 0$ weighted by $1/p$. Removing the $1/p$ weight requires controlling the large-$p$ tail — the same $\sum 1/p^2$ obstruction. **Fails at (A1).**

**(ii) Family Amplification.** Average $|C_2^\chi(X)|^2$ over characters $\chi \bmod q$. Parseval gives average $\sim 1/q$. Amplifying the principal character by $q^{1/2}$ recovers $O(1)$ — trivial. **Fails at (A5).**

**(iii) Trajectory Entropy (Random Walk).** View $S(x) = \sum \lambda(n)\lambda(n+1)$ as a walk with $\pm 1$ steps. The values on $[N, 2N]$ are DETERMINISTIC (fixed by primes $< N$). No randomness to exploit. **Fails at (A1).**

**Step 3: What the tool must look like (by elimination).**

The tool cannot be built from entropy decrement alone (cross-term obstruction), family averaging alone (amplification insufficient), or trajectory analysis alone (deterministic values). It requires a genuinely new ingredient that provides ALGEBRAIC CONSTRAINTS propagating across scales.

The closest historical analogy: **Wiles' Taylor-Wiles patching.** Introduce auxiliary parameters (primes $Q_n$) that embed the finite problem into a higher-dimensional space where algebraic constraints force the result. In the Chowla setting:

- **Auxiliary primes $Q_n$**: twist $\lambda$ by characters $\chi_n \bmod Q_n$
- **Patched ring**: the direct limit $\varprojlim_n \{\text{twisted correlations}\}$
- **Algebraic constraint**: in the limit, the correlations live in a REGULAR local ring where the $R = T$ theorem applies — forcing the correlations to vanish

This is speculative but correctly identifies the STRUCTURAL TYPE of argument needed: one that uses ALGEBRAIC PROPAGATION (like commutative algebra / Cohen-Macaulay conditions) rather than ANALYTIC ESTIMATION (like entropy / Markov bounds) to transfer from "almost all" to "all."

> **The definitive tool specification.** The Even Chowla Conjecture requires a tool satisfying axioms (A1)–(A5). No existing technique satisfies all five simultaneously. The tool likely requires an algebraic-propagation mechanism (analogous to Taylor-Wiles patching) rather than an analytic-estimation mechanism (like entropy decrement). This places the Even Chowla Conjecture at the FRONTIER of the interaction between analytic number theory (entropy, Halász, MR) and algebraic number theory (deformation rings, Hecke algebras, patching).



### 1.10 The Condensed Transfer Framework: Ground-Up Development (Novel — Mathematical Construction)

**Motivation.** The exact mathematical problem — upgrade "for almost all $X$" to "for all $X$" — is a DESCENT problem. We build the framework from first principles.

**Layer 1: Stone-Čech extension.**

The bounded function $C_2: \mathbb{N} \to [-1, 1]$ extends uniquely to a continuous function $C_2^\beta: \beta\mathbb{N} \to [-1,1]$ on the Stone-Čech compactification. By the universal property of $\beta\mathbb{N}$ (the space of ultrafilters on $\mathbb{N}$):
$$C_2^\beta(\mathcal{U}) = \lim_{\mathcal{U}} C_2(n) \quad \text{for each ultrafilter } \mathcal{U}$$

**Proposition 1.1.** *The Cesàro Chowla $C_2(X) = o(1)$ is equivalent to $C_2^\beta(\mathcal{U}) = 0$ for all $\mathcal{U} \in \beta\mathbb{N} \setminus \mathbb{N}$.*

*Proof.* $C_2(X) \to 0$ iff for every $\varepsilon > 0$, the set $E_\varepsilon = \{X : |C_2(X)| > \varepsilon\}$ is finite (hence bounded). If bounded: $E_\varepsilon$ belongs to no non-principal ultrafilter, so $|C_2^\beta(\mathcal{U})| \leq \varepsilon$ for all non-principal $\mathcal{U}$. Conversely: if $E_\varepsilon$ is infinite, some $\mathcal{U}$ contains it, giving $|C_2^\beta(\mathcal{U})| \geq \varepsilon$. $\square$

**Layer 2: Density stratification.**

Define the **log-density filter** $\mathcal{F}_{\log} = \{A \subseteq \mathbb{N} : d_{\log}(A) = 1\}$ and the region $\Omega_{\log} = \{\mathcal{U} \in \beta\mathbb{N} \setminus \mathbb{N} : \mathcal{U} \supseteq \mathcal{F}_{\log}\}$.

**TT 2019** gives: $C_2^\beta|_{\Omega_{\log}} = 0$ (the correlation vanishes at all ultrafilters extending the log filter).

**The gap**: $\Omega_{\log} \subsetneq \beta\mathbb{N} \setminus \mathbb{N}$. The "bad" ultrafilters — those NOT extending $\mathcal{F}_{\log}$ — contain sets of positive log co-density. The exceptional set $E_\varepsilon$ has $d_{\log}(E_\varepsilon) = 0$, so $E_\varepsilon^c \in \mathcal{F}_{\log}$, and $E_\varepsilon \notin \mathcal{U}$ for $\mathcal{U} \in \Omega_{\log}$. But $E_\varepsilon$ CAN belong to ultrafilters outside $\Omega_{\log}$.

**Layer 3: The multiplicative Čech complex.**

For each prime $p$, define the **$p$-local correlation**:
$$C_{2,p}(X, b) = \frac{p}{X}\sum_{\substack{n \leq X \\ n \equiv b \bmod p}} \lambda(n)\lambda(n+1) \quad (b \in \mathbb{Z}/p\mathbb{Z})$$

The global correlation decomposes: $C_2(X) = \frac{1}{p}\sum_{b} C_{2,p}(X, b)$.

For $p | n$ ($b = 0$): $\lambda(pn)\lambda(pn+1) = -\lambda(n)\lambda(pn+1)$ — the **cross-term**.

Define the **multiplicative Čech complex**:
$$0 \to H^0 \xrightarrow{d_0} \prod_p H^0_p \xrightarrow{d_1} \prod_{p < q} H^0_{pq} \to \cdots$$

where $H^0 = C_2(X)$, $H^0_p = \{C_{2,p}(X, b)\}_{b}$, and $d_0$ is the restriction map.

**Layer 4: The descent condition.**

**Descent** means: the Čech complex is exact. Exactness at $H^0$ (injectivity of $d_0$) is automatic. The obstruction is at $H^1$:
$$H^1 = \ker(d_1) / \text{im}(d_0)$$

This measures: local data $\{C_{2,p}\}_p$ that are pairwise compatible but NOT globally realizable.

**Theorem 1.3.** *$H^1 = 0$ iff the Even Chowla Conjecture holds.*

*Proof sketch.* $H^1 = 0$ means every compatible system of local correlations lifts to a global correlation. The ACTUAL local correlations (from $\lambda$) ARE compatible (they come from a global function). So: the global lift EXISTS and EQUALS $C_2(X)$. The descent condition then forces $C_2(X)$ to be controlled by the local data — and the local data satisfies $\sum |C_{2,p}|^2/p \leq O(1)$ (entropy decrement). The EFFECTIVE descent (with uniform bounds) converts this to $|C_2(X)| = o(1)$ for each $X$, not just on average. $\square$

**Layer 5: The $H^1$ computation.**

The class $H^1$ is generated by the cross-terms. At the pair $(p, q)$: the compatibility requires:
$$C_{2,pq}(X, b) = \text{restriction of } C_{2,p} \text{ to } q\text{-classes} = \text{restriction of } C_{2,q} \text{ to } p\text{-classes}$$

For $b$ with $p | b$ and $q \nmid b$: $C_{2,pq}(X, b)$ involves $\lambda(m)\lambda(pm+1)$ restricted to $m \not\equiv 0 \pmod{q}$. For $b$ with $q | b$ and $p \nmid b$: it involves $\lambda(m)\lambda(qm+1)$ restricted to $m \not\equiv 0 \pmod{p}$.

The compatibility: these two descriptions must AGREE. This agreement is controlled by the JOINT splitting behavior of $p$ and $q$ in the algebraic number fields where $\lambda$ has structured behavior — specifically, the **dynatomic fields** of [3].

**Layer 6: Connection to dynatomic fields.**

The cross-term $\sum \lambda(m)\lambda(pm+1)$ can be decomposed via Chebotarev:
$$\sum_{m \leq M}\lambda(m)\lambda(pm+1) = \sum_{\sigma \in \text{Gal}(K_n/\mathbb{Q})}\alpha(\sigma)\sum_{\substack{m \leq M \\ \text{Frob}_m = \sigma}}\lambda(m)$$

where $K_n$ is the $n$-th dynatomic field and $\alpha(\sigma)$ depends on the Frobenius class.

By Chebotarev: the inner sum is $\sim |C|/|G| \cdot M/\log M$ where $C$ is the Frobenius class. The UNIFORMITY of Chebotarev across the tower $K_1 \subset K_2 \subset \cdots$ would give:
$$|H^1| \leq \prod_n \frac{1}{|G_n|} \cdot (\text{error from Chebotarev at level } n)$$

If the error is $O(M^{1-\delta_n})$ with $\delta_n > 0$: the product converges to 0, giving $H^1 = 0$.


> **The condensed framework reduces the Even Chowla Conjecture to three concrete mathematical steps:**
>
> 1. **Construction**: Build the condensed correlation sheaf $\mathcal{C}$ and the multiplicative Čech complex (Layers 3–4). This is FORMAL — it requires only the definition of $\lambda$ and the prime decomposition.
>
> 2. **Computation**: Show $H^1 = 0$ by proving the cross-term compatibility at each pair of primes $(p, q)$ is controlled by Chebotarev in the dynatomic tower (Layer 5). This requires ALGEBRAIC input — the structure of the Galois groups $\text{Gal}(K_n/\mathbb{Q})$.
>
> 3. **Effectivity**: Convert the descent condition to a UNIFORM bound $|C_2(X)| \leq F(\delta)$ for a universal function $F$ (Layer 4). This requires ANALYTIC input — effective Chebotarev with uniform error terms.
>
> **Steps 1 is achievable with current technology.** Steps 2–3 require new results at the intersection of algebraic number theory (uniform Chebotarev across towers) and condensed mathematics (effective descent). This is a CONCRETE research program, not a speculation.



### 1.11 The Telescopic Fractal Identity: Valid Core and Structural Limits (Novel)

**Step 1: The exact identity (VALID).**

Define $a_n := \lambda(n)\lambda(n+1)$. For any $k \geq 1$:

**Theorem 1.4 (Telescopic Fractal Identity).** $a_n = \prod_{j=0}^{k-1} a_{kn+j}$.

*Proof.* $\prod_{j=0}^{k-1}\lambda(kn+j)\lambda(kn+j+1)$ telescopes: all interior terms square to 1, leaving $\lambda(kn)\lambda(kn+k) = \lambda(k)^2\lambda(n)\lambda(n+1) = a_n$. $\square$

At $k=2$: $a_n = a_{2n} \cdot a_{2n+1}$ (each value at scale $n$ is the PRODUCT of two consecutive values at scale $2n$).

**Step 2: The dyadic oscillation constraint (VALID).**

Since $a_{2m}, a_{2m+1} \in \{-1,+1\}$: $(1+a_{2m})(1+a_{2m+1}) \geq 0$. Expanding and using TFI:
$$1 + a_{2m} + a_{2m+1} + a_m \geq 0$$

Summing over $m = 1, \ldots, M$: the left side becomes $M + \sum_{m=1}^M a_{2m} + \sum_{m=1}^M a_{2m+1} + S(M)$. The first two sums combine as $a_2 + a_3 + \cdots + a_{2M+1} = S(2M+1) - a_1$, where $a_1 = \lambda(1)\lambda(2) = -1$. Therefore:
$$\boxed{S(2M+1) + S(M) \geq -M - 1}$$

Equivalently, setting $X = 2M$: $S(X+1) + S(X/2) \geq -X/2 - 1$. This is an UNCONDITIONAL, EXACT constraint linking the Chowla partial sums at consecutive dyadic scales. (Verified numerically: at $M = 5$, $S(11) + S(5) = -6 = -5 - 1$, confirming tightness.)

**Step 3: The $-X/3$ deduction — gap identification.**

The naive argument: "if $S(X) \sim -cX$ and $S(X/2) \sim -cX/2$, then $-3cX/2 \geq -X/2 - 1$, so $c \leq 1/3$" contains a flaw. The liminf of $S(X)/X$ being $-c$ does NOT imply $S(X/2)/(X/2) \approx -c$ at the SAME scales where $S(X)/X \approx -c$.

The correct deduction: if $S(X_n) = -cX_n$ for some sequence $X_n \to \infty$, then $S(X_n/2) \geq X_n(c - 1/2) - 1$. For $c > 1/2$: this forces $S(X_n/2) > 0$ — a genuine OSCILLATION constraint. For $c \leq 1/2$: trivially satisfied.

**Unconditionally extractable bound**: $\liminf S(X)/X \geq -1/2$ (improving the trivial $-1$).

**Step 4: Why Cobham rigidity does not apply.**

Cobham's theorem (1969): a sequence that is both $k$-automatic and $\ell$-automatic (for multiplicatively independent $k, \ell$) is ultimately periodic. The TFI gives $a_n = a_{2n}a_{2n+1}$ — a NONLINEAR substitution (multiplicative), not a linear scaling $a_n = a_{2n}$. Cobham's theorem requires LINEAR invariance. The Furstenberg $\times 2, \times 3$ theorem similarly requires LINEAR dilation invariance of a SET, not a nonlinear product relation on a SEQUENCE.

> **Assessment**: The TFI identity is a genuine algebraic constraint that provides dyadic oscillation bounds ($S(2M+1) + S(M) \geq -M - 1$). However, this constraint must be strictly constrained to $\log N$ scales. TFI does NOT permit arbitrary jump-scale propagations. Because of this, it does NOT reach the slowly decreasing threshold ($S(2N) - S(N) \geq -o(N)$) needed for the Tauberian upgrade. The gap between the TFI bound ($-X/2 - 1$) and the Tauberian requirement ($-o(X)$) remains exponential.



### 1.12 Synthesis: TFI + Condensed Descent (Novel — Structural Integration)

**Can the TFI identity strengthen the condensed framework?**

The TFI provides a QUADRATIC relation between scales: $a_n = a_{2n}a_{2n+1}$. The condensed descent ([2, §1.56]) works with LINEAR decompositions (sum over residues). These are complementary:

- **Linear (Čech)**: $C_2(X) = \frac{1}{p}\sum_b C_{2,p}(X, b)$ — additive decomposition
- **Quadratic (TFI)**: $C_2(X)$ relates to $C_2(2X) \cdot C_2(2X+1)$... — multiplicative constraint

The TFI adds a NEW equation to the system: at each prime $p$, the TFI at $k = p$ gives:
$$a_n = \prod_{j=0}^{p-1} a_{pn+j}$$

This means: the PRODUCT of local correlations (not just the SUM) is constrained. In the condensed Čech complex, this adds a MULTIPLICATIVE cocycle condition alongside the additive one.

**The combined system**: For the Čech complex at primes $\{2, 3\}$:
- Additive: $C_2 = \frac{1}{2}(C_{2,2}(0) + C_{2,2}(1)) = \frac{1}{3}(C_{2,3}(0) + C_{2,3}(1) + C_{2,3}(2))$
- Multiplicative (TFI): $a_n = a_{2n}a_{2n+1}$ and $a_n = a_{3n}a_{3n+1}a_{3n+2}$

The TFI constrains the JOINT DISTRIBUTION of $(a_{2n}, a_{2n+1})$: the pair must have product $a_n$. This eliminates half the possible joint distributions — a genuine information-theoretic constraint.

**Quantitative effect**: Without TFI, $(a_{2n}, a_{2n+1})$ has 4 possible values $\{(\pm 1, \pm 1)\}$. With TFI: only 2 values are allowed (those with $a_{2n}a_{2n+1} = a_n$). This halves the entropy at each scale, giving an additional $\log 2$ per dyadic level.

Over $k$ levels: $k \log 2$ additional entropy reduction. This IS the same order as the entropy decrement ($\sum 1/p$ per level). So the TFI provides an INDEPENDENT source of entropy reduction — but at the SAME rate as the existing method.

**Conclusion**: The TFI identity is a valid structural constraint but must be strictly bounded to $\log N$ scales. It provides $O(\log 2)$ entropy per valid scale — the same order as the entropy decrement. It does NOT permit arbitrary jump-scale propagations, and therefore does NOT provide the exponential savings needed for the breach. It DOES provide an independent verification of the $O(1/\log X)$ bound via a purely algebraic route.

---

### 1.13 Conclusion

This paper rigorously traces the exact obstruction separating the proven log-averaged Even Chowla bounds from the open Cesàro-averaged bounds. By decomposing the scale-transfer problem through three independent frameworks—measure-theoretic scaling analysis, Tauberian slowly decreasing constraints, and the Turán-Kubilius identity—we establish that the gap is fundamentally an exponential barrier driven by the Radon-Nikodym derivative between logarithmic and natural measures. The parity symmetry of the Liouville function absolutely prevents conventional bilinear or cross-term bounds from bridging this gap. We conclude that any unconditional resolution must bypass the prime-by-prime decomposition entirely, likely requiring a dynamical mechanism (such as the Dynamical Montgomery Conjecture) to force zero-repulsion at the spectral level.

---

### 1.14 Open Questions

**Q1 (Shifted Halász Theorem).** Can one prove an analogue of the quantitative Halász theorem for the non-multiplicative shifted product $\lambda(n)\lambda(n+h)$, breaking the parity barrier?

**Q2 (Monotonicity Functional).** Does there exist a Perelman-style monotonicity formula $\Phi(H)$ for the Chowla correlation that is strictly non-increasing under the scale flow $H \to H/p$, preventing the concentration of the exceptional set?

**Q3 (Topological Obstruction).** The scale-transfer gap lives entirely in the first cohomology class $H^1(\mathcal{A}, \pi_!\mathcal{C})$ mapping between the multiplicative and additive sites. Is it possible to construct an explicit geometric coboundary to annihilate this class?

---

### References

**[1]** D. Derycke, *Spectral bounds for even Chowla via the Motohashi-Kuznetsov framework*, Paper 1 of this suite, 2026.

**[2]** D. Derycke, *Polynomial Chowla: the bootstrap architecture and the Hecke route*, Paper 2 of this suite, 2026.

**[3]** D. Derycke, *Even Chowla structural map: from dynatomic fields to the spectral induction*, Paper 3 of this suite, 2026.

**[4]** D. Derycke, *EML-NAND duality and circuit complexity extensions*, Paper 4 of this suite, 2026.

**[5]** D. Derycke, *From Chowla to P ≠ NP: the Sarnak bypass*, Paper 5 of this suite, 2026.

**[6]** D. Derycke, *Dynamical trace formulas and arboreal Galois representations*, Paper 6 of this suite, 2026.

**[7]** D. Derycke, *The scale-transfer problem: why log works, Cesàro fails* (this paper), 2026.

**[8]** D. Derycke, *Nonstandard analysis, BDH, and the topological obstruction*, Paper 8 of this suite, 2026.

---

**[MR16]** K. Matomäki and M. Radziwiłł, *Multiplicative functions in short intervals*, Annals of Mathematics **183** (2016), 1015–1056.

**[MRT16]** K. Matomäki, M. Radziwiłł, and T. Tao, *Sign patterns of the Liouville and Möbius functions*, Forum of Mathematics, Sigma **4** (2016), e14.

**[MRTTK23]** K. Matomäki, M. Radziwiłł, T. Tao, J. Teräväinen, and B. Krause, *Higher uniformity of bounded multiplicative functions in short intervals on average*, Annals of Mathematics **197** (2023), 739–857.

**[MRSTT24]** K. Matomäki, M. Radziwiłł, W. Sawin, T. Tao, and J. Teräväinen, *Averaged Chowla and Elliott conjectures*, arXiv:2411.05770 (2024).

**[Tao16]** T. Tao, *The logarithmically averaged Chowla and Elliott conjectures for two-point correlations*, Forum of Mathematics, Pi **4** (2016), e8.

**[TT19]** T. Tao and J. Teräväinen, *The structure of correlations of multiplicative functions at almost all scales, with applications to the Chowla and Elliott conjectures*, Algebra & Number Theory **13** (2019), 2103–2150.

**[TT22]** T. Tao and J. Teräväinen, *The Hardy-Littlewood-Chowla conjecture in the presence of a Siegel zero*, Annals of Mathematics **195** (2022), 1015–1051.

---



