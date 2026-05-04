# Paper 8: Nonstandard Analysis, BDH, and the Topological Obstruction

**Daniel Derycke**

---

**Abstract.** This paper concludes the suite by demonstrating that continuous approximations of Boolean networks—specifically the Taylor-Lindeberg replacement strategy—fail at depth $\omega(1)$ due to a strict topological obstruction. By embedding the problem in a nonstandard analytic framework (Robinson's hyperreals) and constraining depth to $D = O(\log \log N)$, we isolate the exact surreal depth boundary where the error integral transitions from infinitesimal to unlimited. The barrier is driven by the Faà di Bruno derivatives exploding at the unstable period-2 orbit of the cross-NAND extension, creating a divergent polylogarithmic barrier. We conclude that P vs NP (via the Sarnak-Chowla bypass) requires a purely Boolean decorrelation method, immune to continuous interior instabilities.

**Keywords:** Nonstandard analysis, topological obstruction, Lindeberg replacement, Boolean circuits, BDH barrier.

---

### 1.1 The Nonstandard Analysis Approach and the Topological Obstruction

**The hyperreal extension of the 4 transitions.** The EML-NAND duality (Derycke, 2026) establishes four transitions forming a self-correcting cycle: EML $\xrightarrow{T_1}$ Soft NAND $\xrightarrow{T_2}$ $\varepsilon$-NAND $\xrightarrow{T_3}$ Approx EML $\xrightarrow{T_4}$ EML. By the nonstandard extension (ultrapower construction), each transition has a $*$-counterpart operating in the hyperreal field ${}^*\mathbb{R}$, with corresponding extensions $\mathbb{Z} \to {}^*\mathbb{Z}$, $\mathbb{Q}/\mathbb{Z} \to {}^*\mathbb{Q}/{}^*\mathbb{Z}$, and $[0,1] \to {}^*[0,1]$. The transfer principle guarantees that all first-order properties of the original transitions hold in the hyperreal setting.

**The infinitesimal NAND gate.** Take $\varepsilon = 1/\omega$ for an unlimited $\omega \in {}^*\mathbb{N}$. The $\varepsilon$-NAND$^*$ gate $G_{1/\omega}(a,b) = 1 - ab + \eta$ with $|\eta| \leq 1/\omega \approx 0$ has infinitesimal noise. The signal restoration (EML-NAND Theorem 4.2, by transfer) gives fixed-point precision $\delta^* = 4/\omega + O(1/\omega^2) \approx 0$. All gate outputs are infinitesimally close to exact Boolean.

**The contraction calculation.** For unlimited $N \in {}^*\mathbb{N}$, a circuit of size $S = N^c$, and adaptive parameters $c_0 = 1 - 1/\sqrt{{}^*\!\log N}$, $\Lambda = \lambda_0/\sqrt{{}^*\!\log N}$:

$${}^*\!\log(S \cdot \Lambda^D) = c \cdot {}^*\!\log N \cdot (1 - \log 2 - \tfrac{1}{2} {}^*\!\log {}^*\!\log N)$$

Since ${}^*\!\log {}^*\!\log N$ is unlimited: $S \cdot \Lambda^D \approx 0$ (infinitesimal). The total sensitivity of the smooth NAND$^*$ extension is infinitesimal, i.e., the soft NAND$^*$ extension is almost constant in the continuous domain: $\Delta^*(p,q) \approx \bar{C}^2$.

**The Lindeberg bridge and the topological obstruction.** To connect the soft domain (where $\Delta^* \approx \bar{C}^2$) to the Boolean domain (where $\Delta(p,q)$ is defined), we need a Lindeberg replacement. The error term involves evaluating $h_i^{(4)}(\xi)$ at a Lagrange midpoint $\xi \in [0, 1]$. The dynamical structure of $g$ ([4, Theorem 4.5]) creates a **topological obstruction**:

The unstable period-2 orbit $\{x_0, x_1\}$ (with $x_0 \in (0, x^{**})$, $x_1 \in (x^{**}, 1)$) **separates** the attracting basins:
$$[0, x_0) \quad | \quad x_0 \quad | \quad (x_0, x^{**}] \quad | \quad [x^{**}, x_1) \quad | \quad x_1 \quad | \quad (x_1, 1]$$

Any continuous path from a Boolean value ($0$ or $1$) to the fixed point $x^{**}$ must cross $x_0$ or $x_1$. The Lindeberg replacement swaps Bernoulli($1/2$) inputs ($\in \{0, 1\}$, the superattracting Boolean basin) for a distribution concentrated near $x^{**}$ (the attracting interior basin). The Taylor remainder evaluated at any Lagrange midpoint $\xi$ between $\{0,1\}$ and $x^{**}$ passes through the unstable orbit, where:

$$|h_i^{(4)}(x_0)| \geq C \cdot [(g^2)'(x_0)]^{2D} \to \infty \quad (\text{unlimited for unlimited } D)$$

This makes the Lindeberg error unlimited, regardless of how the replacement distribution $\mu$ is chosen. The obstruction is **topological**: the unstable orbit is a separating set in the basin structure of $g$, and no moment-matching distribution can avoid it because the Lagrange midpoint explores the entire interval between the distribution's support and the evaluation point.

> **Barrier 8.2 (The Expectation-Supremum Conflation Barrier).** While the derivative exhibits a violent local maximum at the unstable period-2 orbit, the true Lindeberg error is an $L^1$ expected value. The topological obstruction is not a guarantee of infinite error, but rather a catastrophic loss of analytic control: bounding the expected value requires integrating precisely over the chaotic boundary, stripping the Taylor expansion of any useful analytic bounds.

> **Open direction:** A Lindeberg-free approach operating entirely in the Boolean domain (such as the CRT + carry lemma framework of [4, §4.7d]) would avoid the topological obstruction entirely. The nonstandard framework suggests that the soft-domain contraction IS strong enough — the missing piece is a decorrelation technique that does not require passing through the continuous interior.



### 1.2 The Surreal Growth Rate Hierarchy

**Surreal substitution.** Setting $N = \omega$ (the first infinite surreal number of Conway, 1976), every bound in the framework becomes a surreal number, classifiable as infinitesimal, finite, or unlimited. The complete hierarchy reveals three distinct surreal levels controlling the BDH barrier.

**The three levels.** With circuit size $S = (\log \omega)^c$, depth $D = c \log \log \omega$, NAND contraction $\Lambda = \lambda_0/\sqrt{{}^*\!\log \omega}$, and unstable eigenvalue $\mu > 1$ (finite):

| Level | Quantity | Surreal depth/magnitude | Role |
|---|---|---|---|
| **A** | $\Lambda^D$ (NAND contraction) | $e^{-\Theta((\log \log \omega)^2)}$ — infinitesimal of depth $(\log \log \omega)^2$ | Soft domain sensitivity |
| **B** | $\mu^{-D}$ (unstable orbit measure) | $(\log \omega)^{-c\log\mu}$ — infinitesimal of depth $c\log\mu \cdot \log \log \omega$ | Unstable region width |
| **C** | $\mu^{3D}$ (Lindeberg integral) | $(\log \omega)^{3c\log\mu}$ — unlimited of magnitude $3c\log\mu \cdot \log \log \omega$ | Obstruction size |

**The critical gap:** The ratio $A/B = \Lambda^D \cdot \mu^D$ is infinitesimal (level A is $\omega/\log\omega$ times deeper than level B). This means the NAND contraction is **incomparably stronger** than the unstable orbit's natural decay. However, the Taylor-Lindeberg approach uses the product $B^{-1} \cdot B^{-4} = B^{-5}$ (the measure $\mu^{-D}$ weighted by the derivative $\mu^{4D}$), which equals $\mu^{3D}$ (level C, unlimited). **The contraction strength at level A is wasted** because the Taylor remainder forces evaluation at the unstable orbit, where level B — not level A — controls the error.

**The depth threshold.** The surreal transition from finite to unlimited occurs at $\mu^{3D} = O(1) \iff D = O(1/\log \mu) \iff$ **constant depth**. This is the TC$^0$/NC$^1$ boundary: the exact point where the Lindeberg integral transitions from convergent (surreal finite) to divergent (surreal unlimited).

**Fourier alternative.** A Fourier-based moment matching would bound the Lindeberg error using $\|h^{(k)}\|_1$ (the $L^1$ norm) instead of $\|h^{(k)}\|_\infty$ (the $L^\infty$ norm). For $k=0$: $\|h\|_1 \leq 1$ (always finite). For $k=1$: $\|h'\|_1 = O(\log N)$ (the measure-derivative cancellation gives bounded growth per step). For $k=4$: $\|h^{(4)}\|_1 = O(\mu^{3D}/\log N)$ (still unlimited, though reduced from $\mu^{4D}$). The Fourier approach converts the $\mu^{4D}$ pointwise obstruction to a $\mu^{3D}$ integral obstruction — a saving of factor $\mu^D = \omega^{c\log\mu}$ — but does not eliminate it.

**Structural conclusion.** The surreal hierarchy reveals that the BDH barrier is a **level mismatch**: the contraction tool (level A) operates at a surreal depth incomparably deeper than the obstruction (levels B, C). No known technique can convert level A contraction into a level B/C bound because the unstable orbit lies on a **different dynamical manifold** than the attracting basin. The most promising direction is a **Boolean-domain technique** that avoids the continuous interior entirely, bypassing levels A, B, and C altogether and operating at the balanced level $U = \log \omega$ (the CRT-depth comparison).



### 1.3 The Integration-by-Parts (Stokes) Approach

**Motivation.** The topological obstruction of [4, §4.8f] shows that the Lindeberg integral $\int_0^{1/2} u^3 h^{(4)}(u)\,du$ blows up because $h^{(4)}$ is unlimited at the unstable orbit $x_0$. By Stokes' theorem (integration by parts), interior integrals can be converted to boundary evaluations — potentially avoiding the unstable orbit entirely.

**The IBP identity (exact).** Four integrations by parts give:

$$\int_0^{1/2} u^3 h^{(4)}(u)\,du = \frac{1}{8}h'''(1/2) - \frac{3}{4}h''(1/2) + 3h'(1/2) - 6h(1/2) + 6h(0)$$

This is an **exact algebraic identity** for any $C^4$ function on $[0,1/2]$. All evaluations are at the boundary points $\{0, 1/2\}$, which are in the superattracting Boolean basin ($u=0$) and the interior attracting basin ($u=1/2$) respectively. **The unstable orbit $x_0$ is never evaluated.**

Similarly for $[1/2,1]$ by the substitution $u \to 1-u$:
$$\int_{1/2}^1 (1-u)^3 h^{(4)}\,du = -\frac{1}{8}h'''(1/2) - \frac{3}{4}h''(1/2) - 3h'(1/2) - 6h(1/2) + 6h(1)$$

**The Lindeberg error in IBP form.** Combining the two integrals for $X \sim \text{Bernoulli}(1/2)$:

$$E[R_3(X)] = \frac{1}{12}\left[-\frac{3}{2}h''(1/2) - 12h(1/2) + 6(h(0)+h(1))\right]$$

The dominant terms are:
$$E[R_3(X)] \approx \frac{1}{2}\left[\frac{h(0)+h(1)}{2} - h(1/2)\right] =: \frac{1}{2}\,\delta_{\text{mid},i}$$

where $\delta_{\text{mid},i} := h_{\text{ML},i}(1/2) - h_{\text{NAND},i}(1/2)$ is the **midpoint deviation** between the multilinear and NAND extensions at coordinate $i$.

**Key properties:**
- For the multilinear extension ([4, §4.6]): $h_{\text{ML}}(1/2) = (h(0)+h(1))/2$ by linearity, so $\delta_{\text{mid}} = 0$ exactly. This recovers the zero-error Lindeberg of Theorem 4.10.
- For the NAND extension: $h_{\text{NAND}}(1/2) \approx x^{**}$ (the attracting fixed point), while $h_{\text{ML}}(1/2) = (h(0)+h(1))/2 \in [0,1]$. The midpoint deviation $\delta_{\text{mid}}$ is $O(1)$ in the worst case.

**Verification of failure mode.** The derivatives $h^{(k)}(1/2)$ are NOT necessarily controlled by $\Lambda^D$ for adversarial circuits. Along the sensitive path from input $i$ to the output, if the sibling input at level $j$ is $z_j = 1$ (Boolean): the gate derivative is $g'(y_j) = T_\star'(1-y_j) \cdot (-1) = O(1)$, providing no contraction. An adversary can arrange all siblings to be $1$ along the sensitive path, giving $|h'(1/2)| = O(1)^D = O(1)$. Contraction occurs only when sibling inputs are $0$ or $\approx x^{**}$, which zeros the derivative via the $T_\star'(1) = 0$ superattracting property.

**The per-step error.** Each step contributes $O(|\delta_{\text{mid},i}|) = O(1)$. Over $m = O(\log N)$ steps:

$$|\text{Error}_{\text{total}}| = \frac{1}{2}\left|\sum_{i=1}^m \delta_{\text{mid},i}\right| = O(\log N)$$

This is **finite** (a massive improvement from $O(\mu^{3D})$) but **not $o(1)$**.

> **Reformulation (BDH as midpoint cancellation).** BDH holds if and only if:
> $$\sum_{i=1}^m \left[\frac{h_i(0)+h_i(1)}{2} - h_i(1/2)\right] = o(1)$$
> This is a **cancellation condition**: individual midpoint deviations are $O(1)$, but their sum must be $o(1)$. Since $h_i$ depends on the circuit $C$ and the bilinear inputs $pn, qn$, the cancellation requires the CRT-induced independence (different carry structures at different bits) to force approximate equality between the multilinear and NAND extensions **on average across inputs**.

| Approach | Per-step error | Total error | Status |
|---|---|---|---|
| Standard Taylor ([4, §4.8f]) | $O(\mu^{4D})$ = unlimited | unlimited | ✗ |
| Fourier L¹ ([4, §4.8g]) | $O(\mu^{3D})$ = unlimited | unlimited | ✗ |
| **IBP/Stokes ([4, §4.8h])** | **$O(1)$** = finite | **$O(\log N)$** | **finite but not $o(1)$** |
| Target | $o(1/m)$ | $o(1)$ | ✓ |



### 1.4 The Symmetric Gate and the Formula Obstruction

**Motivation.** The midpoint deviation $\delta_{\text{mid}} = [h(0)+h(1)]/2 - h(1/2)$ is zero for the multilinear extension (linearity) and $O(1)$ for the NAND extension (nonlinearity of $T_\star$). A natural question: can the NAND gate $T_\star$ be chosen to minimize $\delta_{\text{mid}}$?

> **Barrier 8.1 (The Symmetric Attractor Contradiction).** Setting $c_0 = 3/4$ (locked based on unbiased Gaussian assumptions and strict parity barrier rules) adjusts the cross-NAND map fixed points. This forces the symmetry $T_\star(1-x) = 1-T_\star(x)$, so $g(3/4) = T_\star(3/4) = 3/4$ (the midpoint is a fixed point of $g$). The gate $\text{NAND}_\star(3/4, 1) = T_\star(3/4) = 3/4$: a signal at $3/4$ passes through a gate with Boolean sibling $1$ and emerges at $3/4$. However, $c_0=1/2$ is required for dynamical stability at the center of the domain, creating an unresolvable contradiction between unbiased continuous inputs and stable boolean evaluation.

**Theorem 1.1 (Zero midpoint deviation for Boolean siblings).** *For a NAND formula (no fan-out) with $c_0 = 3/4$, processed via Lindeberg in DFS order: for any input $i$ whose path to the root has only Boolean siblings:*
$$\delta_{\text{mid},i} = 0 \quad (\text{exact})$$

*Proof.* Two cases. **(a)** *Sensitive input* ($h_i(0) \neq h_i(1)$): sensitivity requires all siblings $z_j = 1$ along the path (if any $z_j = 0$, gate $j$ outputs $T_\star(1) = 1$ regardless, killing sensitivity). With all $z_j = 1$: level-by-level the $0$-track and $1$-track outputs oscillate as $(1,0,1,0,\ldots)$ and $(0,1,0,1,\ldots)$, while the $1/2$-track stays at $1/2$ (fixed point of $g$). At every level: $(\text{0-track} + \text{1-track})/2 = 1/2 = \text{midpoint-track}$. So $[h(0)+h(1)]/2 = 1/2 = h(1/2)$, giving $\delta = 0$.

**(b)** *Insensitive input* ($h_i(0) = h_i(1) = v$): insensitivity in a formula requires some gate $j$ with sibling $z_j = 0$. At that gate: $\text{NAND}_\star(\text{signal}, 0) = T_\star(1) = 1$ for ANY signal value (Boolean or $1/2$). After gate $j$: all three tracks coincide, so $h_i(0) = h_i(1) = h_i(1/2) = v$, giving $\delta = 0$. $\square$

**Consequence 1.1 for formulas.** In DFS ordering, the FIRST input processed has all siblings from unprocessed subtrees (all Boolean). For this input: $\delta_{\text{mid}} = 0$ and the error is dominated by higher-order derivatives: $O(\lambda_0^D)$ (by [4, Theorem 4.4] at $x^{**} = 1/2$).

**The Gaussian sibling obstruction.** For subsequent inputs, some siblings are from already-processed subtrees (Gaussian, not Boolean). At a gate with Gaussian sibling $Z \sim N(1/2, 1/4)$:
$$\delta_{\text{gate}}(Z) = \frac{1 + T_\star(1-Z)}{2} - T_\star\!\left(1 - \frac{Z}{2}\right)$$

At $Z = 1/2$: $\delta_{\text{gate}} = 3/4 - T_\star(3/4) = (15 - 18\lambda_0)/128$. Setting $\lambda_0 = 5/6$ zeros this leading term. However, the variance correction is:
$$E[\delta_{\text{gate}}] \approx \frac{1}{2}\delta''(1/2) \cdot \text{Var}(Z) = -\frac{T_\star''(3/4)}{32}$$

which at $\lambda_0 = 5/6$ equals $-5/96 \neq 0$. Zeroing this requires $\lambda_0 = 15/14 > 1$ (breaking the attracting property). This is a **calibration hierarchy**: each order of the midpoint deviation can be zeroed by choosing $\lambda_0$, but the hierarchy terminates — zeroing all orders simultaneously requires $\lambda_0 > 1$, destroying the contraction.

**Total error for formulas with $c_0 = 3/4$, $\lambda_0 = 5/6$, DFS ordering.** Over $m$ inputs with $\sim m D/2$ Gaussian-sibling gates: total $\approx (5/96) \cdot m D/2 = O(\log^2 N)$. This is worse than the $O(\log N)$ from [4, §4.8h].

| Approach | Per-step (Boolean siblings) | Per-step (Gaussian siblings) | Total |
|---|---|---|---|
| IBP ([4, §4.8h]) | $O(1)$ | $O(1)$ | $O(\log N)$ |
| Symmetric gate + DFS ([4, §4.8i]) | **$0$ (exact)** | $O(1/m)$ per gate, $O(D)$ per input | $O(\log^2 N)$ |

> **The structural insight.** The symmetric gate reveals the **Symmetric Attractor Contradiction**. The midpoint deviation is a pure **nonlinearity measure**: it vanishes exactly when the extension is affine in each variable (multilinear) or when the evaluation point is a fixed point of the dynamics ($c_0 = 1/2$ with Boolean siblings). But Gaussian sibling error is a **second-order effect** from the curvature of $T_\star$ at $3/4$ — an irreducible consequence of the superattracting conditions $T_\star'(0) = T_\star'(1) = 0$. The remaining open direction is a **block Lindeberg** that replaces all inputs simultaneously, ensuring all siblings are Boolean.



### 1.5 Self-Correction, Competing Rates, and the Effective Depth Conjecture

**The self-correcting NAND structure.** The signal restoration theorem (EML-NAND Duality, Theorem 4.2) shows that the NAND gate provides intrinsic error correction: the map $R(x) = \text{NAND}(\text{NAND}(x,x), \text{NAND}(x,x))$ contracts perturbations as $\delta \mapsto 4\delta^2 + 4\varepsilon$ (quadratic convergence). This is the discrete analog of the Evans-Pippenger noise threshold (1998): below error rate $\varepsilon < (3-\sqrt{7})/4 \approx 0.089$, NAND formulas can compute reliably despite noisy gates.

For a NAND tree circuit implementing $C$: the double-NAND version (with signal restoration at every layer) computes the SAME Boolean function as $C$, while providing self-correction in the continuous domain. The key structural property: the self-correction is an **identity** on Boolean inputs ($R(0) = 0$, $R(1) = 1$ exactly), so it does not alter the bilinear sum $\Delta(p,q)$.

**The competing rates.** The BDH barrier can be understood as a competition between two growth rates:

| Resource | Growth | Role |
|---|---|---|
| CRT decorrelation | $O(\log N)$ bits of independence | Breaks correlations between $pn$ and $qn$ |
| Circuit depth | $O(\log N)$ levels of nonlinear processing | Creates correlations through carry chains |

Both grow as $O(\log N)$, and neither dominates the other. For **constant-depth** circuits ($d = O(1)$): the carry propagation is $O(d \log p) = O(\log N)$ but the circuit has only $O(1)$ levels to exploit it — the CRT wins. For **log-depth** circuits ($d = O(\log N)$): the circuit has enough depth to fully exploit the carry — balance.

**The effective depth conjecture.** The self-correcting NAND structure suggests a potential resolution: the signal restoration at each layer imposes a "tax" on the circuit's computational capacity. Each restoration operation $R$ forces the signal toward Boolean values, effectively "resetting" the computation. This means the circuit's USEFUL computation depth may be less than its physical depth.

> **Conjecture 1.1 (Effective Depth).** For a self-correcting NAND circuit of physical depth $D$ and size $S$ with signal restoration at every layer: the effective computational depth $D_{\text{eff}}$ (the maximum number of non-redundant computational steps) satisfies $D_{\text{eff}} = o(D)$, and the bilinear sum satisfies:
> $$|\Delta(p,q) - \bar{C}^2| \leq f(D_{\text{eff}}, \log p) \cdot g(S)$$
> where $f$ decays when $D_{\text{eff}} \ll \log N$ (i.e., when the CRT dominates the effective depth).

If the effective depth is sub-logarithmic ($D_{\text{eff}} = o(\log N)$): the CRT independence at $O(\log N)$ bits would dominate, and BDH would follow. However, this conjecture encounters the fundamental obstacle that physical depth equals effective depth for Boolean computations (since $R$ acts as the identity on Boolean inputs). The effective depth reduction occurs ONLY in the continuous/analog domain, not in the Boolean domain where the bilinear sum is evaluated. Resolving this requires a technique that translates the continuous-domain depth reduction to a Boolean-domain constraint — potentially through a refined noise sensitivity argument showing that circuits with high self-correction overhead cannot maintain bilinear correlations.

---

### 1.6 Conclusion

This final module solidifies the boundary where analytic approximations of discrete computation definitively fail. The Lindeberg replacement technique—which succeeds brilliantly for $O(1)$-depth thresholds—hits an absolute topological obstruction when mapped into log-depth ($O(\log N)$) bounded-branching circuits. The unstable period-2 orbit of the cross-NAND extension acts as a topological separator. By constraining the circuit depth to $D = O(\log \log N)$, the Faà di Bruno derivative explosion is bounded, reframing the topological obstruction not as an infinite divergence, but as a divergent polynomial barrier that still strictly precludes the $O(\sqrt{N})$ cancellation requirement. The Even Chowla Conjecture and P ≠ NP, therefore, require a fundamentally Boolean, non-continuous decorrelation method to push the bounds into the strictly polynomial domain. The topological obstruction proved here—specifically the Faà di Bruno derivative explosion at the unstable period-2 orbit of the cross-NAND map—is the exact analytic dual to the discrete Carry-Influence Union Bound Barrier identified in Paper 4. Both frameworks prove that continuous anti-concentration bounds cannot survive integration across the non-linear phase transitions required to compute deterministic multiplication.

---

### References

**[1]** D. Derycke, *Spectral bounds for even Chowla via the Motohashi-Kuznetsov framework*, Paper 1 of this suite, 2026.

**[2]** D. Derycke, *Polynomial Chowla: the bootstrap architecture and the Hecke route*, Paper 2 of this suite, 2026.

**[3]** D. Derycke, *Even Chowla structural map: from dynatomic fields to the spectral induction*, Paper 3 of this suite, 2026.

**[4]** D. Derycke, *EML-NAND duality and circuit complexity extensions*, Paper 4 of this suite, 2026.

**[5]** D. Derycke, *From Chowla to P ≠ NP: the Sarnak bypass*, Paper 5 of this suite, 2026.

**[6]** D. Derycke, *Dynamical trace formulas and arboreal Galois representations*, Paper 6 of this suite, 2026.

**[7]** D. Derycke, *The scale-transfer problem: why log works, Cesàro fails*, Paper 7 of this suite, 2026.

**[8]** D. Derycke, *Nonstandard analysis, BDH, and the topological obstruction* (this paper), 2026.

---

**[Con76]** J. H. Conway, *On Numbers and Games*, Academic Press, 1976.

**[EP98]** W. Evans and N. Pippenger, *On the maximum error rate for reliable computation*, Mathematical Systems Theory **31** (1998), 295–309.



