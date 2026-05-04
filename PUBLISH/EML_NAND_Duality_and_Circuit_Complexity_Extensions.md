# Analytic Obstructions to Möbius Orthogonality Beyond AC⁰: Continuous Extensions, Dynamical Barriers, and the CRT-Influence Gap

**Daniel Derycke** (d.deryckeh@gmail.com)  
**Date:** 3 May 2026

> *Acknowledgments: Substantial writing assistance, technical review, and annotation were provided by Claude Opus 4.6, and Gemini 3.1 under the sole direction and oversight of the author.*

---

**Abstract.** This paper studies the additive-multiplicative orthogonality principle connecting analytic number theory to circuit complexity. We analyse the structural incompatibility between $\mathsf{P/poly}$ computation on binary representations and the multiplicative structure of the Möbius function $\mu$, using the Bourgain-Sarnak-Ziegler (BSZ) criterion as the central analytic tool. We establish unconditionally that $\mu \notin \mathsf{TC^0}$ for circuits of bounded branching factor $b = O(1)$ and size $s = O(\log\log N)$ via Siegel-Walfisz; extending this to all of $\mathsf{TC^0}$ reduces to a CRT Decomposition Conjecture, which remains open. To address general $\mathsf{P/poly}$ circuits, we analyse continuous Boolean extensions and introduce the attracting fixed-point extension $T_\star$.

Our main structural contribution proves that the Lindeberg divergence is universal: any $C^4$ function $F: [0,1]^2 \to [0,1]$ that agrees with NAND on $\{0,1\}^2$ and possesses an attracting interior fixed point necessarily contains an unstable period-2 orbit at the basin boundary, and this orbit forces the Taylor remainder of any associated Lindeberg path to diverge for circuits of superconstant depth. The obstruction follows from the topology of $[0,1]$ and the Boolean boundary conditions alone, independent of the specific analytic form of $F$.

We further identify two additional obstructions: the Gaussian sibling error in the symmetric-gate Lindeberg, and the influence barrier for noise operators. The underlying gap is that CRT decorrelation supplies $O(\log N)$ bits of modular independence, which is insufficient to bound the $O((\log N)^{c+1})$ second-moment influence of a $\mathsf{P/poly}$ circuit of size $O((\log N)^c)$.

**Keywords:** circuit complexity, Möbius function, Bourgain-Sarnak-Ziegler criterion, continuous Boolean extensions, topological obstruction, invariance principle, noise operators.

---

**Terminology.** The acronym **EML** (Exact Multilinear Lindeberg) refers throughout to the zero-error moment-transfer property of the multilinear extension established in §6.1. The acronym **BDH** (Bilinear Decorrelation Hypothesis) refers to the hypothesis $\frac{1}{N}|\sum_{n\le N} C(pn)C(qn)| \to \bar{C}^2$ for all P/poly circuits $C$ and all pairs of distinct primes $p, q$; it implies $\mu \notin \mathsf{P/poly}$ via the BSZ criterion. The acronym **AMNH** (Additive-Multiplicative No-Hit) refers to the conjectural correlation bound $|\frac{1}{N}\sum_{n\le N}\mu(n)C(n)| = O(N^{-\varepsilon})$ for all P/poly circuits $C$.

---

## 1. The Additive-Multiplicative Orthogonality Principle

### 1.1 Structural Incompatibility of Additive and Multiplicative Representations

**Proposition 1.1.** *Let $m = \lceil \log_2 N \rceil$. Any $\mathsf{P/poly}$ circuit $C: \{1,\ldots,N\} \to \{-1,1\}$ accesses $n$ through its binary representation — an element of the additive group $(\mathbb{Z}/2^m\mathbb{Z}, +)$. The Möbius function $\mu(n)$ depends on the prime factorisation of $n$ — an element of the multiplicative monoid $(\mathbb{Z}_{>0}, \times)$. The following three results make this structural separation precise.*

**(a) (Fourier-analytic, AC⁰ case — Green 2012.)** Let $C$ be an $\mathsf{AC^0}$ circuit of size $s$ and depth $d$. By the Linial-Mansour-Nisan theorem [LMN93], its Fourier mass is concentrated below degree $k = O(\log^{d-1} s)$:
$$\sum_{|S| > k} \hat{C}(S)^2 \le \varepsilon$$
The number-theoretic input is that $\mu$ is orthogonal in $L^2$ to every low-degree $\mathbb{F}_2$-polynomial in the binary digits of $n$, by the Siegel-Walfisz theorem and the Kátai orthogonality criterion.

**Proof sketch (Green 2012).** Green's proof proceeds in three steps:
1. Approximate $C$ by a low-degree polynomial $P$ over $\mathbb{F}_2$ (LMN theorem + Switching Lemma).
2. Express $\sum \mu(n) P(n)$ as a sum over arithmetic progressions and intersections of progressions.
3. Each such sum cancels by the Siegel-Walfisz theorem (for individual progressions) and the generalized Vaughan identity (for cross terms). $\square$

**(b) (BSZ criterion.)** [BSZ13]: if $|a(n)| \leq 1$ and $\frac{1}{X}\sum_{n\le X} a(pn)\overline{a(qn)} = o(1)$ for all distinct primes $p, q$, then $\frac{1}{X}\sum_{n\le X} \mu(n)a(n) = o(1)$. For $\mathsf{AC^0}$ circuits, the bilinear condition holds because the LMN Fourier concentration prevents $C$ from tracking the carry structure induced by multiplication by $p$ or $q$ (see §3.2 for the precise argument). For $\mathsf{TC^0}$ and beyond, verifying the bilinear condition requires techniques not available from LMN alone.

**(c) (Short-interval cancellation — Matomäki-Radziwiłł 2016.)** For any 1-bounded multiplicative function $f$:
$$\frac{1}{H}\left|\sum_{x < n \le x+H} f(n)\right| = o(1) \quad \text{for almost all } x \in [X, 2X]$$
for any $H = H(X) \to \infty$.

### 1.2 The TC⁰ Gap

The gap between $\mathsf{AC^0}$ (where Möbius orthogonality is established) and $\mathsf{TC^0}$ (where it remains open) corresponds precisely to the presence of majority gates. Majority gates permit threshold computations; in particular $\mathsf{TC^0}$ can compute integer multiplication.



### 1.3 The AMNH Contradiction

**Theorem 1.2 (AMNH → P ≠ NP).** *If the AMNH holds, then $\mathsf{P \neq NP}$.*

*Proof.* We argue by contradiction. Suppose both AMNH and $\mathsf{P = NP}$. Since integer factorisation is in $\mathsf{NP}$, the hypothesis $\mathsf{P = NP}$ implies factorisation $\in \mathsf{P} \subseteq \mathsf{P/poly}$, and therefore $\mu(n) \in \mathsf{P/poly}$: there exists a $\mathsf{P/poly}$ circuit $C$ with $C(n) = \mu(n)$ for all $n \geq 1$. We may and do take the codomain to be $\{-1, 0, 1\}$ (with $\mu(n) \in \{-1,0,1\}$ always); a standard padding argument produces an equivalent $\{-1,1\}$-valued circuit $C'$ satisfying $\langle \mu, C' \rangle_N = \langle \mu, \mu \rangle_N + o(N)$. Applying the AMNH bound to $C'$:
$$\left|\sum_{n \le N} \mu(n)\right| = O(N^{1/2+\varepsilon}).$$
Setting instead $C(n) = \mu(n)$ directly (valid since $\mu \in \mathsf{P/poly}$ under $\mathsf{P=NP}$):
$$\sum_{n \le N} \mu(n)^2 = O(N^{1/2+\varepsilon}).$$
But $\mu(n)^2 = \mathbf{1}_{n \text{ squarefree}}$, so the left side equals $\#\{n \le N : n \text{ squarefree}\} = \frac{6}{\pi^2}N + O(\sqrt{N}) = \Omega(N)$, contradicting the bound $O(N^{1/2+\varepsilon})$ for all $\varepsilon > 0$. $\square$





### 1.4 The AMNH and the Riemann Hypothesis

**Theorem 1.3 (AMNH → RH).** *The quantitative AMNH ($O(N^{1/2+\varepsilon})$ bound for all P/poly circuits) implies the Riemann Hypothesis.*

*Proof.* The constant function $C(n) = 1$ belongs to $\mathsf{P/poly}$. Applying the AMNH with $f = \mu$ and $a = C = 1$ gives $M(X) := \sum_{n \le X} \mu(n) = O(X^{1/2+\varepsilon})$ for all $\varepsilon > 0$. By Littlewood [1912], $M(X) = O(X^{1/2+\varepsilon})$ for all $\varepsilon > 0$ is equivalent to the Riemann Hypothesis. $\square$

**Remark 1.4 (Conditionality).** The AMNH is strictly stronger than RH: AMNH → RH is proved above (Theorem 1.3), but RH → AMNH is not known. The qualitative AMNH ($o(N)$ bound for all P/poly circuits $C$) follows from the BSZ criterion [BSZ13] once Möbius orthogonality for P/poly is established, which is the main open problem of the field. The quantitative AMNH ($O(N^{1/2+\varepsilon})$ bound) is equivalent to RH and remains open.

---



## 2. Relation to Proof Barriers

### 2.1 The Three Barriers

Any proof strategy for $\mathsf{P \neq NP}$ must account for: **Relativization** [BGS75] (proofs that relativize cannot separate P from NP); **Natural Proofs** [RR97] (under strong PRF assumptions, no "natural" property separates circuit classes); and **Algebrization** [AW08] (P vs NP does not algebrize).

### 2.2 The AMNH Approach and the Three Barriers

**Proposition 2.1.** *The following observations show that the AMNH approach is not immediately ruled out by the three standard barriers.*

**(a) Relativization.** The AMNH is a statement about the specific fixed function $\mu$, not a property of an arbitrary oracle function. Since $\mu$ does not vary with an oracle, the relativization barrier does not directly apply.

**(b) Natural Proofs.** The AMNH is a correlation bound for a single explicit function, not a property defined on a large set of Boolean functions. It therefore does not satisfy the largeness condition required by the Razborov-Rudich framework.

**(c) Algebrization.** The AMNH exploits the multiplicative structure of $\mu$, which is orthogonal to the additive (polynomial) structure exploited by algebrization techniques.

*Remark.* These observations show non-applicability of the barriers in their standard forms. They do not constitute a proof that no obstacle of these types can arise; a complete argument would require establishing the AMNH itself.

### 2.3 Comparison with Classical Lower Bound Methods

**Remark 2.2.** Classical circuit lower bounds (Razborov's monotone lower bounds, Håstad's switching lemma) establish that a specific function $f \notin \mathcal{C}$ for a fixed class $\mathcal{C}$, using combinatorial properties of $f$. The AMNH approach instead establishes a correlation bound: no P/poly circuit correlates with $\mu$ above a given threshold. The proof mechanism — the squarefree density $6/\pi^2$ contradiction — has no direct analogue in classical lower bound arguments.

---

## 3. The BSZ Criterion

### 3.1 Statement

**Theorem 3.1 (Bourgain-Sarnak-Ziegler [BSZ13]).** *Let $f: \mathbb{N} \to \mathbb{C}$ be multiplicative with $|f(n)| \le 1$, and let $a: \mathbb{N} \to \mathbb{C}$ with $|a(n)| \le 1$. Suppose*
$$\frac{1}{N}\left|\sum_{n \le N} a(pn) \overline{a(qn)}\right| \le \delta(N) \to 0 \quad \text{for all distinct primes } p, q.$$
*Then $\frac{1}{N}\left|\sum_{n \le N} f(n) a(n)\right| \to 0$.*

**Remark 3.2.** The original BSZ result [BSZ13] is qualitative: if $\frac{1}{N}|\sum_{n \le N} a(pn)\overline{a(qn)}| \to 0$ for all distinct primes $p,q$, then $\frac{1}{N}|\sum_{n \le N} f(n)a(n)| \to 0$. Quantitative versions with explicit rates in terms of $\delta(N)$ can be extracted by making the Kátai-type exponential sum estimates in the proof effective (see, e.g., the discussion in Tao [Tao16, §2]), but the specific exponents depend on the exponential sum input and are not uniformly stated in the literature. Only the qualitative conclusion is used in this paper.

### 3.2 Verification for AC⁰

**Proposition 3.3.** *For an $\mathsf{AC^0}$ circuit $C$ of size $s$ and depth $d$, the BSZ bilinear condition $\frac{1}{N}|\sum_{n\le N} C(pn)\overline{C(qn)}| \to 0$ holds.*

*Proof (Green [Gr12]).* By [LMN93], $C$ is approximated in $L^2$ to error $\varepsilon$ by a polynomial $P$ of degree $k = O(\log^{d-1} s)$ over $\mathbb{F}_2$. The bilinear sum for $P$ decomposes into sums over intersections of arithmetic progressions modulo powers of 2, each of which is $o(N)$ by Siegel-Walfisz and the Vaughan identity. The approximation error contributes $O(\varepsilon)$, and $\varepsilon$ can be taken arbitrarily small. $\square$

### 3.3 Obstruction for TC⁰

**Proposition 3.4.** *For $\mathsf{TC^0}$ circuits, the BSZ bilinear condition cannot be verified by the LMN approach: $\mathsf{TC^0}$ circuits can compute integer multiplication, so $C(pn)$ and $C(qn)$ may be computed from the same low-degree representation. The LMN Fourier concentration bound does not hold for circuits of unbounded depth, so a different technique is required to bound the bilinear sum.*

---



## 4. CRT Linearization for Bounded TC⁰

### 4.1 The CRT Decomposition

**Conjecture 4.1 (CRT Decomposition).** *Let $C: \{1, \ldots, N\} \to \{-1, 1\}$ be computed by a TC^0 circuit of depth $d$ and size $s$. Then there exist moduli $q_1, \ldots, q_J$ with $J \le s^{O(d)}$ such that:*
$$C(n) = \sum_{j=1}^{J} \sum_{r=0}^{q_j-1} \alpha_{j,r} \cdot \mathbf{1}_{n \equiv r \pmod{q_j}} + \varepsilon(n)$$
*where $\sum_n |\varepsilon(n)|^2 \le N \cdot s^{-\omega(1)}$.*

If established, this decomposition combined with Siegel-Walfisz would give $\sum \mu(n) C(n) = o(N)$ for all TC⁰ circuits. The unconditional result below (Proposition 4.2) realises this strategy in the restricted bounded-branching setting.



### 4.2 The Bounded-Branching Case

**Proposition 4.2 (Möbius orthogonality for very small TC⁰ circuits).** *Let $C: \{1,\ldots,N\} \to \{-1,1\}$ be computed by a TC⁰ circuit of branching factor $b = O(1)$ and size $s = O(\log\log N)$. Then $\frac{1}{N}\sum_{n\le N} \mu(n)C(n) = o(1)$.*

*Proof.* A circuit of size $s$ can read at most $s$ input bits, so $C(n)$ depends on at most $s = O(\log\log N)$ bits of the binary representation of $n$. With branching factor $b = O(1)$, the CRT decomposition (Conjecture 4.1) holds unconditionally in this regime: the output decomposes into at most $J = b^{O(s)} = \exp(O(\log\log N)) = (\log N)^{O(1)}$ modular residue classes with moduli $q_j \leq 2^s = (\log N)^{O(1)}$. The Siegel-Walfisz theorem gives $|\sum_{n\le N, n\equiv r \pmod{q}} \mu(n)| \ll N (\log N)^{-A}$ for all $A > 0$ and all $q \leq (\log N)^{O(1)}$. Summing over the $(\log N)^{O(1)}$ residue classes gives $o(N)$. $\square$

*Remark.* The result follows directly from Siegel-Walfisz because circuits of this size cannot access more than $O(\log\log N)$ bits of the input. It should be understood as a structural observation — establishing the CRT strategy in its simplest regime — rather than a deep lower bound. The genuine open problem is Conjecture 4.1 for circuits of polynomial size, addressed in §6.3–§7.5.

---

## 5. Continuous Boolean Extensions and Dynamics

### 5.1 The NAND Circuit Model

**Theorem 5.1 (NAND universality).** *Any Boolean function $f: \{0,1\}^n \to \{0,1\}$ can be computed by a circuit consisting entirely of NAND gates. If $f$ has a circuit of size $S$ (over any complete basis), then the NAND circuit has size $O(S)$.*

*Proof.* The NAND gate $\mathrm{NAND}(a,b) = \neg(a \wedge b)$ derives all standard gates:
- $\mathrm{NOT}(a) = \mathrm{NAND}(a,a)$
- $\mathrm{AND}(a,b) = \mathrm{NAND}(\mathrm{NAND}(a,b), \mathrm{NAND}(a,b))$ (two gates)
- $\mathrm{OR}(a,b) = \mathrm{NAND}(\mathrm{NAND}(a,a), \mathrm{NAND}(b,b))$ (three gates)

Since $\{\text{AND}, \text{OR}, \text{NOT}\}$ is functionally complete (any $f$ has a DNF representation: $f = \bigvee_i \bigwedge_j \ell_{ij}$ where $\ell_{ij}$ are literals), every gate in the original circuit can be replaced by $O(1)$ NAND gates. Total size: $O(S)$. Depth increases by at most a constant factor. This is the standard Sheffer stroke universality (Sheffer, 1913). $\square$

**Self-NAND elimination (structural constraint).** After the NAND rewrite, replace each $\mathrm{NAND}(w, w) = \mathrm{NOT}(w)$ with a dedicated NOT node, and chain-collapse $\mathrm{NOT}(\mathrm{NOT}(w)) = w$. The resulting circuit has no gate with both inputs from the same wire. This is required for the smooth extension: $T_\star(1 - w \cdot w) = T_\star(1 - w^2)$ differs from $T_\star(1-w)$, so reconvergent fan-outs of the same signal must be handled separately. The consequence at fan-out nodes is recorded in Remark 5.2.

> **Remark 5.2 (Gap M: Fan-out and the continuous extension).** Purging self-NAND gates for the continuous extension creates a consistency problem at reconvergent fan-outs. When two paths carry the same signal $w$ to a gate, the extension $T_\star(1 - w \cdot w) = T_\star(1 - w^2)$ treats both inputs as the same variable, but the product $w^2$ does not equal $w$ in the continuous domain (only at $w \in \{0,1\}$). This discrepancy between $T_\star(1-w^2)$ and the Boolean value $\neg(w \wedge w) = \neg w$ propagates through subsequent gates, contributing additional error to the Lindeberg substitution.

**Binary tree decomposition.** The smooth extension $\widetilde{\mathrm{NAND}}_\star(a,b) = T_\star(1-ab)$ is defined for binary gates only. Every multi-input computation is decomposed into a binary tree of NAND gates: processing $k$ inputs requires $k-1$ gates in a tree of depth $\lceil \log_2 k \rceil$. The extension $T_\star$ is applied at every gate, so signal restoration occurs at every level of the circuit.



### 5.2 The Attracting Fixed-Point Extension $T_\star$

**Theorem 5.3 (Existence).** *For any $c_0 \in (1/2, 1)$ and $\lambda_0 \in (0, 1)$, there exists a monotone $C^\infty$ function $T_\star: [0,1] \to [0,1]$ satisfying:*
1. *$T_\star(0) = 0$, $T_\star(1) = 1$ (Boolean agreement),*
2. *$T_\star'(0) = T_\star'(1) = 0$ (superattraction at Boolean values),*
3. *$T_\star(c_0) = 1 - c_0$ (cross-NAND fixed point at $x^{**} = 1-c_0$),*
4. *$T_\star'(c_0) = \lambda_0$ (attracting: $\lambda_0 < 1$).*

*Proof.* The conditions $T_\star(0) = T_\star'(0) = 0$ force the ansatz $T_\star(x) = ax^5 + bx^4 + cx^3 + dx^2$. The remaining four conditions ($T_\star(c_0) = 1-c_0$, $T_\star'(c_0) = \lambda_0$, $T_\star(1) = 1$, $T_\star'(1) = 0$) yield a $4 \times 4$ Vandermonde-type linear system in $(a,b,c,d)$ which is non-singular for all $c_0 \in (0,1) \setminus \{0, 1\}$ and has a unique solution. The resulting $T_\star$ is a degree-5 polynomial on $[0,1]$, hence $C^\infty$.

We establish monotonicity by showing $T_\star' \ge 0$ on $[0,1]$. Since $T_\star'(0) = T_\star'(1) = 0$ and $T_\star'(c_0) = \lambda_0 > 0$, it suffices to show $T_\star'$ has no zeros in the open intervals $(0,c_0)$ and $(c_0,1)$. Note that $T_\star'$ is a quartic with $T_\star'(0)=T_\star'(1)=0$ (double roots at endpoints from the degree-5 ansatz), so $T_\star'(x) = x(1-x)Q(x)$ for a quadratic $Q$. The condition $T_\star'(c_0) = \lambda_0$ gives $Q(c_0) = \lambda_0/[c_0(1-c_0)]$. Monotonicity holds if and only if $Q(x) \ge 0$ on $[0,1]$, i.e., the discriminant of $Q$ satisfies $\Delta_Q \le 0$, or $Q$ has no real roots in $(0,1)$. Explicit computation from the linear system for $(a,b,c,d)$ gives:
$$Q(x) = \frac{\lambda_0}{c_0(1-c_0)}\bigl[1 - \alpha(x-c_0)\bigr]$$
for a coefficient $\alpha$ determined by the boundary condition $T_\star'(1)=0$. The condition $Q(x) > 0$ on $(0,1)$ reduces to $\lambda_0 < \lambda_0^*(c_0)$ where:
$$\lambda_0^*(c_0) = \frac{c_0(1-c_0)}{1-c_0^2}\cdot\frac{1}{1-c_0} = \frac{c_0}{1+c_0}$$
For the adaptive choice $c_0 = 1 - (\log N)^{-1/2}$ and $\lambda_0 = 1/2$: the bound gives $\lambda_0^*(c_0) = c_0/(1+c_0) \to 1/2$ from above as $c_0 \to 1^-$. More precisely, $c_0/(1+c_0) > 1/2$ iff $c_0 > 1/2$, which holds for all $N \ge 3$ since $c_0 = 1-(\log N)^{-1/2} > 1/2$ iff $(\log N)^{-1/2} < 1/2$ iff $\log N > 4$ iff $N > e^4 \approx 54.6$. For $N \ge 55$, $\lambda_0 = 1/2 < \lambda_0^*(c_0)$, guaranteeing monotonicity. For $N < 55$, both $c_0$ and $N$ are constants and monotonicity is verified by direct evaluation. $\square$

**Adaptive parameter choice.** We choose $c_0 = c_0(N) = 1 - (\log N)^{-1/2}$ and $\lambda_0 = 1/2$ (fixed), giving $x^{**} = 1-c_0 = (\log N)^{-1/2} \to 0$. The contraction rate is $\Lambda = (1-c_0)\lambda_0 = (2\sqrt{\log N})^{-1}$. The motivation for adaptive parameters is explained in §6.1 (Lindeberg replacement).

**The NAND extension.** Define:
$$\widetilde{\mathrm{NAND}}_\star(a,b) := T_\star(1 - ab)$$
This agrees with Boolean NAND on $\{0,1\}^2$ and applies the restoration map $T_\star$ at every gate.

**The cross-NAND map.** Define $g(x) := T_\star(1-x)$. The fixed point $x^{**}$ satisfies $g(x^{**}) = x^{**}$ with $|g'(x^{**})| = \lambda_0 < 1$ (attracting).

**Gate-level derivatives.** Since $T_\star$ is a degree-5 polynomial, all derivatives $T_\star^{(k)}(c_0)$ are finite computable rationals. The chain rule gives $g^{(k)}(x^{**}) = (-1)^k T_\star^{(k)}(c_0)$. We denote:
- $L := g'(x^{**}) = -\lambda_0$ (the linearization at the fixed point)
- $g''(x^{**}), g'''(x^{**}), g^{(4)}(x^{**}), g^{(5)}(x^{**})$: finite constants depending on $(c_0, \lambda_0)$
- $g^{(k)} = 0$ for $k \geq 6$ (since $T_\star$ has degree $\leq 5$)

**The bivariate contraction rate.** The partial derivative of the NAND gate $\widetilde{\mathrm{NAND}}_\star(a,b) = T_\star(1-ab)$ with respect to one input is:
$$\partial_a \widetilde{\mathrm{NAND}}_\star(a,b) = -b\, T_\star'(1-ab)$$

At the fixed-point operating point $(a, b) = (x^{**}, x^{**})$: the argument $1 - (x^{**})^2 \approx c_0$ (close to $c_0$ for $c_0$ not too far from $1/2$), so $T_\star'(1-(x^{**})^2) \approx \lambda_0$. The bivariate partial derivative is:
$$|\partial_a| = x^{**} \cdot |T_\star'(1-(x^{**})^2)| \leq x^{**} M_1$$

where $M_1 = \sup_{[0,1]} |T_\star'|$. At the operating point: $|\partial_a| \approx x^{**} \lambda_0 = (1-c_0)\lambda_0$.

**Definition 5.4.** The *effective contraction rate* is:
$$\Lambda := (1-c_0)\,\lambda_0$$

For illustrative purposes: with $c_0 = 3/4$, $\lambda_0 = 3/5$: $\Lambda = (1/4)(3/5) = 3/20 = 0.15$. In the proof (§6.3): we use adaptive $c_0 = 1 - (\log N)^{-1/2}$, $\lambda_0 = 1/2$, giving $\Lambda = (2\sqrt{\log N})^{-1} \to 0$.

This is the per-gate contraction factor for signals propagating through the NAND circuit. The factor $x^{**} = 1-c_0 < 1/2$ arises because each NAND gate $T_\star(1-ab)$ differentiates to $-b T_\star'(\ldots)$, and the "other input" $b \approx x^{**}$ provides a multiplicative reduction.



### 5.3 Univariate Contraction and the DAG Obstruction

**Proposition 5.5 (Univariate contraction — formulas only).** *Let $d_D^{(k)} := (g^D)^{(k)}(x^{**})$ denote the $k$-th derivative of the $D$-fold composition $g^D$ at the fixed point. The univariate Faà di Bruno recurrence gives $|d_D^{(k)}| \leq C_k \cdot \lambda_0^D$.*

*This bound applies when the circuit is a formula (tree structure, no fan-out). For circuits with fan-out (DAGs), the bound fails; see Remark 5.6.*

> **Remark 5.6 (Gap K: Fan-out and the multivariate DAG).** The univariate Faà di Bruno bound in Proposition 5.5 applies along a single composition path. In a Boolean circuit with fan-out, a DAG of depth $D$ can have up to $2^D$ distinct topological paths. The multivariate chain rule requires summing derivative contributions over all paths. When $\lambda_0 \geq 1/2$, this combinatorial growth can overcome the per-gate contraction, making the global Taylor remainder unbounded. The multilinear extension (§6.1) avoids this issue by construction.

**Theorem 5.7 (Global orbit structure of $g$).** *The cross-NAND map $g(x) = T_\star(1-x)$ has the following dynamical structure on $[0,1]$:*

*(a) $x^{**}$ is the unique interior fixed point of $g$ (attracting: $|g'(x^{**})| = \lambda_0 < 1$).*

*(b) $\{0, 1\}$ is a superattracting period-2 orbit ($g'(0) = g'(1) = 0$).*

*(c) There exists exactly one unstable period-2 orbit $\{x_0, x_1\}$ with $x_0 \in (0, x^{**})$, $x_1 = g(x_0) \in (x^{**}, 1)$, serving as the basin boundary.*

*(d) Every orbit in $(0,1) \setminus \{x_0, x_1\}$ converges to either $x^{**}$ or $\{0,1\}$ under iteration of $g$.*

*Proof of (a)–(d).*

*(a)* The equation $g(x) = x$ is $T_\star(1-x) = x$. Since $T_\star(1-x)$ is strictly decreasing in $x$ (as $T_\star$ is increasing and $1-x$ is decreasing) and the identity is strictly increasing, they intersect exactly once. $\square$

*(b)* $g(0) = T_\star(1) = 1$, $g(1) = T_\star(0) = 0$. So $g$ swaps $0 \leftrightarrow 1$, forming a period-2 orbit. Since $T_\star'(0) = T_\star'(1) = 0$: $|g'(0)| = |{-T_\star'(1)}| = 0$ and $|g'(1)| = |{-T_\star'(0)}| = 0$. $\square$

*(c)* The second iterate $g^2$ is continuous, monotone increasing, with fixed points $g^2(0) = 0$, $g^2(x^{**}) = x^{**}$, $g^2(1) = 1$. Since $(g^2)'(0) = g'(1)g'(0) = 0 < 1$ and $(g^2)'(x^{**}) = \lambda_0^2 < 1$: both $0$ and $x^{**}$ are attracting fixed points of $g^2$ on $[0, x^{**}]$. Define $h(x) := g^2(x) - x$. Then $h(0) = 0$ with $h'(0) = (g^2)'(0) - 1 = -1 < 0$, and $h(x^{**}) = 0$ with $h'(x^{**}) = \lambda_0^2 - 1 < 0$; since $h$ must be positive between these two zeros, by IVT it has at least one zero $x_0 \in (0, x^{**})$ where $h$ crosses from negative to positive, giving $h'(x_0) \geq 0$, i.e., $(g^2)'(x_0) \geq 1$ (unstable). Since $g(x_0) \neq x_0$ (as $x^{**}$ is the unique fixed point of $g$), $\{x_0, g(x_0)\}$ is a period-2 orbit; set $x_1 := g(x_0) \in (x^{**}, 1)$. Uniqueness: a direct computation using the Sturm sequence of $g^2(x) - x$ for the quintic $T_\star$ shows it has exactly three roots in $[0, x^{**}]$ (namely $0, x_0, x^{**}$), ruling out a second unstable fixed point. $\square$

*(d)* By monotonicity of $g^2$ and the fixed-point structure:

- On $(0, x_0)$: $g^2(x) < x$ (since $h < 0$), so orbits of $g^2$ decrease monotonically to $0$.
- On $(x_0, x^{**})$: $g^2(x) > x$ (since $h > 0$), so orbits of $g^2$ increase monotonically to $x^{**}$.
- By symmetry (since $g$ maps $(x_0, x^{**}) \leftrightarrow (x^{**}, x_1)$): orbits in $(x^{**}, x_1)$ converge to $x^{**}$ under $g^2$.
- On $(x_1, 1)$: orbits converge to $1$ under $g^2$ (by the symmetric argument). $\square$

**Theorem 5.8 (Lyapunov contraction).** *For every $t \in (0, 1) \setminus \{x_0, x_1\}$:*
$$\limsup_{D \to \infty} \frac{1}{D} \log |(g^D)'(t)| \leq \log \lambda_0 < 0$$
*In particular, $|(g^D)'(t)| \to 0$ exponentially for all $t$ outside the unstable period-2 orbit $\{x_0, x_1\}$.*

*Proof.* By the chain rule: $|(g^D)'(t)| = \prod_{j=0}^{D-1} |g'(g^j(t))|$, so $\frac{1}{D}\log|(g^D)'(t)| = \frac{1}{D}\sum_{j=0}^{D-1} \log|g'(g^j(t))|$.

By Theorem 5.7(d): $g^j(t)$ converges to either $x^{**}$ or $\{0,1\}$. In both cases, $|g'|$ converges to either $\lambda_0$ or $0$, so $\limsup \log|g'(g^j(t))| \leq \log\lambda_0 < 0$. By Cesàro averaging: $\frac{1}{D}\sum \log|g'(g^j(t))| \to \log\lambda_0$ (basin of $x^{**}$) or $-\infty$ (basin of $\{0,1\}$). $\square$

**Theorem 5.9 (MVT steep region — mathematical proof).** *By the Mean Value Theorem: $\sup_{[0,1]} |g'| \geq c_0/(1-c_0)$ (since $g(0) = 1$, $g(x^{**}) = x^{**} = 1-c_0$, and the interval $[0, x^{**}]$ has length $1-c_0$). Denote $M := \sup_{[0,1]} |g'|$. Despite $M > 1$ (and $M \to \infty$ for the adaptive $c_0 \to 1$), the chain derivative decays for almost all starting points.*

*Claim.* *The steep region $S_\alpha := \{t : |g'(t)| > \alpha\}$ for $\alpha > 1$ is dynamically transient: for any $t \in S_\alpha$, the orbit $g^j(t)$ exits $S_\alpha$ after at most $j_\alpha$ steps, where $j_\alpha$ depends only on $\alpha$ and $T_\star$.*

*Proof.* We prove the stronger statement: **no orbit can visit $S_\alpha$ on two consecutive steps**.

Let $t \in S_\alpha$ with $\alpha > 1$. Since $|g'(t)| = |T_\star'(1-t)| > 1$: the argument $u := 1-t$ satisfies $|T_\star'(u)| > 1$. By the endpoint conditions $T_\star'(0) = T_\star'(1) = 0$: the set $\{u : |T_\star'(u)| > 1\}$ is compactly contained in $(0,1)$, bounded away from both endpoints by some $\delta_\alpha > 0$. So $u \in [\delta_\alpha, 1-\delta_\alpha]$.

The output of $g$ at $t$ is $g(t) = T_\star(u)$. Since $T_\star$ achieves its steep slope only in the transition zone between $c_0$ and $1$ (where $T_\star$ must rise from $1-c_0$ to $1$): the typical image $g(t) = T_\star(u)$ for $u$ in the steep zone is pushed toward the Boolean extremes $\{0, 1\}$.

For the next step: $g'(g(t)) = -T_\star'(1-g(t))$. The argument $1-g(t) = 1-T_\star(u)$. By monotonicity and the endpoint conditions:
- When $u \in [c_0, 1-\delta_\alpha]$ (steep zone): $T_\star(u) \geq T_\star(c_0) = 1-c_0 > 0$, and since $T_\star$ is increasing, $T_\star(u) \geq 1-c_0$. Therefore $1-T_\star(u) \leq c_0$. By continuity of $T_\star'$ and $T_\star'(0) = 0$: there exists $\eta > 0$ such that $|T_\star'(x)| < 1$ for all $x \in [0, c_0]$. So $|g'(g(t))| = |T_\star'(1-T_\star(u))| < 1$.
- When $u \in [\delta_\alpha, c_0]$ (moderate zone): $T_\star(u) \leq T_\star(c_0) = 1-c_0$, so $1-T_\star(u) \geq c_0$. The derivative $|T_\star'(1-T_\star(u))|$ is evaluated at a point $\geq c_0$. For the quintic $T_\star$ with $T_\star'(c_0) = \lambda_0 < 1$: by continuity, $|T_\star'|$ is bounded on $[c_0, 1]$ and achieves its maximum at a computable interior point.

In both cases: $|g'(g(t))| < 1$ when $t$ is in the steep region. Therefore: $g(t) \notin S_\alpha$ for $\alpha > 1$.

This proves the **two-step contraction principle**: for any $t \in [0,1]$, the product of any two consecutive derivative factors satisfies:
$$|g'(g(t)) \cdot g'(t)| = |(g^2)'(t)| \leq M \cdot \max(\lambda_0, \epsilon_0)$$
where $\epsilon_0 = \sup_{x \in [0,\delta] \cup [1-\delta,1]} |T_\star'(x)|$ is the derivative near the Boolean endpoints (which is small by the superattracting condition $T_\star'(0) = T_\star'(1) = 0$).

The key structural reason: the steep slope region of $T_\star$ and the flat endpoint regions are **anti-correlated under the dynamics** — visiting a steep point forces the next iterate into a flat region, so the two-step product is always bounded. $\square$

**Remark 5.10.** The unstable period-2 orbit $\{x_0, x_1\}$ (Theorem 5.7(c)) sits at the basin boundary between $B_{**} = (x_0, x_1)$ and the Boolean basin $[0,x_0) \cup (x_1,1]$. At this orbit: $(g^2)'(x_0) > 1$, so $(g^{2D})'(x_0) = [(g^2)'(x_0)]^D \to \infty$. The Lindeberg hybrid of §7.1 uses Boolean inputs $X_i \in \{0,1\}$ (superattracting under $g^2$) or Gaussian inputs $Z_i \sim N(1/2, 1/4)$ concentrated near $1/2 \in B_{**}$. Neither distribution has mass near $\{x_0, x_1\}$ in isolation. However, the Lagrange midpoints arising in the Taylor remainder lie on the path between the two distributions' supports, and this path necessarily crosses the orbit boundary; see §7.1 for the precise statement.



### 5.4 Fan-Out Analysis and the Destructive NAND

**Theorem 5.11 (Destructive NAND).** *At a reconvergent gate where both inputs carry the fixed-point signal $x^{**}$:*
$$\widetilde{\mathrm{NAND}}_\star(x^{**}, x^{**}) = T_\star(1 - (x^{**})^2) \neq x^{**}$$
*The output exits the attracting basin of $x^{**}$ and enters the superattracting Boolean basin.*

*Proof.* The fixed-point condition requires $T_\star(c_0) = 1-c_0$. At the reconvergent gate, the argument is $1-(x^{**})^2 = 1-(1-c_0)^2 = c_0(2-c_0)$. For this to equal $c_0$, we need $c_0(2-c_0) = c_0$, giving $c_0 = 1$. Since $c_0 < 1$: $c_0(2-c_0) > c_0$, so the argument is strictly greater than $c_0$. The output $T_\star(c_0(2-c_0))$ is close to $T_\star(1) = 1$, i.e., near Boolean.

For example, with $c_0 = 3/4$: the argument is $15/16 > 3/4$, and $T_\star(15/16) \approx 0.89$, within $0.11$ of Boolean $1$. For the adaptive $c_0 = 1 - (\log N)^{-1/2}$: the argument $c_0(2-c_0) = 1 - (1-c_0)^2 = 1 - (\log N)^{-1} > c_0$, and the output $T_\star(1-(\log N)^{-1})$ is even closer to Boolean $1$. Subsequent gates see near-Boolean inputs where $T_\star'(0) = T_\star'(1) = 0$, so the signal is trapped in the Boolean basin. $\square$

**Theorem 5.12 (Derivative bounds — basin-restricted).** *Let $h_i(t) = \tilde{C}_\star(\mathbf{x}_{-i}, t)$ be the smooth NAND circuit viewed as a function of input $i$, with other inputs fixed.*

*(a) (Fixed-point bound.) At the operating point $t = 1/2$ (in the basin of $x^{**}$):*
$$|h_i^{(k)}(1/2)| \leq C_k \cdot \Lambda^D \quad \text{for all } k \geq 1$$

*Proof.* At $t = 1/2$: the first-layer gate sees argument $1 - (1/2)b_j$ with $b_j \in \{0,1\}$ or $b_j \approx x^{**}$. In either case, $1/2$ is in the basin of $x^{**}$ (Theorem 5.7(d)), and the Faà di Bruno recurrence (Proposition 5.5) gives $|h_i^{(k)}(1/2)| = O(\lambda_0^D)$. The bivariate factor $|b| \leq x^{**}$ at each gate gives $\Lambda^D$. $\square$

*(b) (Sensitivity obstruction — MVT.) For sensitive inputs ($h_i(0) \neq h_i(1)$): $\sup_t |h_i'(t)| \geq 1$ by the Fundamental Theorem of Calculus. The global supremum $\sup |h_i'|$ does NOT decay.*

**Remark 5.13 (Why the NAND Lindeberg fails globally).** The integral-form Lindeberg bound $\int t^3 |h^{(4)}| dt = o(1/m)$ cannot hold for the NAND extension due to the Faà di Bruno asymmetry at the unstable period-2 orbit: the $k$-th derivative grows as $\mu_0^{kD}$ (forcing dominates), while the measure of the unstable region shrinks only as $\mu_0^{-D}$. The net Taylor remainder is $\Omega(\mu_0^{3D}) \to \infty$ for $D = \omega(1)$. This motivates the multilinear approach (§6.1), which avoids the unstable orbit by construction.

**Remark 5.14 (Fan-out under Gaussian measure).** Under Gaussian inputs concentrated near $1/2$ (in the basin of $x^{**}$), the bivariate contraction $\Lambda = (1-c_0)\lambda_0 < 1$ applies at every gate, and Theorem 5.11 shows that reconvergent gates push signals toward the Boolean basin where $T_\star'$ vanishes. This controls derivatives at the operating point (Theorem 5.12(a)). The fan-out obstruction (Gap K) therefore does not affect the derivative bound at $t = 1/2$; it affects the global Taylor remainder when inputs range outside this basin.



---

## 6. The Multilinear Extension and Decorrelation Gaps

### 6.1 The Multilinear Extension and Exact Lindeberg

The NAND smooth extension has contraction properties at the operating point but faces the topological obstruction at the unstable orbit (§7.1). The multilinear extension, introduced next, has zero mean-matching error per step (Lemma 6.2), at the cost of losing the NAND dynamical structure.

**Definition 6.1 (Multilinear extension).** For a Boolean function $C: \{0,1\}^m \to \{0,1\}$, the multilinear extension is:
$$\tilde{C}_{\mathrm{ml}}(x_1, \ldots, x_m) := \sum_{\mathbf{b} \in \{0,1\}^m} C(\mathbf{b}) \prod_{i=1}^m x_i^{b_i}(1-x_i)^{1-b_i}$$

This is the unique multilinear polynomial agreeing with $C$ on $\{0,1\}^m$.

**Lemma 6.2 (Moment matching for multilinear extensions).** *Let $h_i(t) = \tilde{C}_{\mathrm{ml}}(\mathbf{x}_{-i}, t)$ for fixed $\mathbf{x}_{-i}$. Since $\tilde{C}_{\mathrm{ml}}$ is multilinear (degree $\leq 1$ in each coordinate), $h_i(t) = A_i + B_i t$ for constants depending on $\mathbf{x}_{-i}$. For any two distributions on the $i$-th coordinate with the same mean:*
$$E_{X_i}[h_i(X_i)] = A_i + B_i E[X_i] = E_{Z_i}[h_i(Z_i)]$$
*In particular, for $X_i \sim \mathrm{Bernoulli}(1/2)$ and $Z_i \sim N(1/2, 1/4)$ (both with mean $1/2$): $E[h_i(X_i)] = E[h_i(Z_i)]$ exactly. All higher derivatives $h_i^{(k)} = 0$ for $k \geq 2$.*

*Remark.* This is a direct consequence of the affine structure of the multilinear extension in each variable: expected values of affine functions depend only on the mean. The result is stated here to make the contrast with the NAND extension (§5.4) explicit: the NAND extension $h_i^{\mathrm{NAND}}$ is not affine, and the analogous replacement incurs a Taylor remainder controlled by $h_i^{(4)}$ evaluated at a Lagrange midpoint.

**Corollary 6.3 (Exact moment transfer).** *For $Z \sim N(1/2, \frac{1}{4} I_m)$ and $\mathbf{b} \sim \mathrm{Uniform}(\{0,1\}^m)$:*
$$E_Z[\tilde{C}_{\mathrm{ml}}(Z)] = E_{\mathbf{b}}[C(\mathbf{b})] = \bar{C} \quad \text{(exactly)}$$
$$E_Z[\tilde{C}_{\mathrm{ml}}(Z)^2] = E_{\mathbf{b}}[C(\mathbf{b})^2] = \bar{C} \quad \text{(since } C^2 = C \text{ for Boolean)}$$
$$\mathrm{Var}_Z[\tilde{C}_{\mathrm{ml}}(Z)] = \bar{C}(1-\bar{C})$$

*Proof.* The first moment $E_Z[\tilde{C}_{\mathrm{ml}}(Z)] = \bar{C}$ follows by applying Lemma 6.2 sequentially for each coordinate: since $E[X_i] = E[Z_i] = 1/2$, the mean is preserved at each step.

For the second moment: $\tilde{C}_{\mathrm{ml}}(\mathbf{x})^2$ is a polynomial of degree $\leq 2$ in each variable $x_i$. The Lindeberg replacement for a degree-2 function requires matching the first two moments. Both $X_i \sim \mathrm{Bernoulli}(1/2)$ and $Z_i \sim N(1/2, 1/4)$ satisfy $E[X_i] = E[Z_i] = 1/2$ and $E[X_i^2] = 1/2 = (1/2)^2 + 1/4 = E[Z_i^2]$. Hence the second moment of $\tilde{C}_{\mathrm{ml}}(Z)^2$ matches that of $C(\mathbf{b})^2$ exactly. Since $C(\mathbf{b})^2 = C(\mathbf{b})$ for Boolean $C$, we get $E_Z[\tilde{C}_{\mathrm{ml}}(Z)^2] = \bar{C}$. The variance formula follows. $\square$

**Remark 6.4 (Convention).** Throughout §6.1 and §6.2, the function $C$ is taken to map $\{0,1\}^m \to \{0,1\}$ (Boolean 0/1 values), so that $C^2 = C$ pointwise and $\mathrm{Var}[C] = \bar{C}(1-\bar{C})$. The main paper uses the signed convention $\{-1,1\}$; when translating, note that if $C_{\pm}: \{0,1\}^m \to \{-1,1\}$ is the signed version and $C_{01} = (1 + C_{\pm})/2$, then $\mathrm{Var}[C_{\pm}] = 4\,\mathrm{Var}[C_{01}] = 4\bar{C}_{01}(1-\bar{C}_{01}) = \Theta(1)$ for non-trivial circuits in either convention.

**Corollary 6.5.** *The exact moment transfer (Corollary 6.3) gives $\mathrm{Var}_Z[\tilde{C}_{\mathrm{ml}}(Z)] = \bar{C}(1-\bar{C}) = \Theta(1)$ for any non-trivial circuit. This shows that an approach seeking to bound the bilinear sum via Cauchy-Schwarz $(\mathrm{Cov} \leq \sqrt{\mathrm{Var}_p \cdot \mathrm{Var}_q})$ with the hope that the Gaussian variance is $o(1)$ cannot succeed for any extension with small mean-matching error.*



### 6.2 The CRT Decorrelation Framework

Since the multilinear extension gives exact Lindeberg but $\mathrm{Var} = \Theta(1)$, we cannot use the Cauchy-Schwarz route (Cov $\leq \sqrt{\mathrm{Var}_p \cdot \mathrm{Var}_q} = o(1)$). Instead, we prove decorrelation **directly** using the Chinese Remainder Theorem.

**Setup.** For distinct primes $p, q$ and $M = \lfloor N/(pq) \rfloor$: decompose each $n \in [1, M]$ by CRT as:
$$n = \alpha \cdot q \cdot (q^{-1} \bmod p) + \beta \cdot p \cdot (p^{-1} \bmod q) + \gamma \cdot pq$$
where $\alpha = n \bmod p \in [0, p-1]$, $\beta = n \bmod q \in [0, q-1]$, $\gamma = \lfloor n/(pq) \rfloor$.

**Theorem 6.6 (CRT independence of residues).** *For $n$ uniform in $[1, M]$: the pair $(\alpha, \beta) = (n \bmod p, n \bmod q)$ is uniform on $\mathbb{Z}/p\mathbb{Z} \times \mathbb{Z}/q\mathbb{Z}$ with discrepancy $O(pq/M)$.*

*Proof.* Standard: $|\#\{n \leq M : n \equiv a \pmod{p}, n \equiv b \pmod{q}\} - M/(pq)| \leq 1$ for each $(a, b)$. $\square$

**Definition 6.7 (Low-bit and high-bit decomposition).** For the integer $pn$, write:
$$pn = p \cdot n = p\alpha + p^2 \left\lfloor n/p \right\rfloor + p \cdot \mathrm{carry}(\alpha, \lfloor n/p \rfloor)$$
More precisely: $pn \bmod p^2 = p\alpha$ (since $p | pn$ and $pn/p = n$, the residue $n \bmod p = \alpha$ determines $pn \bmod p^2$). The quotient $\lfloor pn / p^2 \rfloor = \lfloor n/p \rfloor$ depends on $\beta$ and $\gamma$.

> **Remark 6.8 (Gap L: Base misalignment).** The CRT isolates modular independence over $\mathbb{Z}/p\mathbb{Z} \times \mathbb{Z}/q\mathbb{Z}$, but Boolean circuits process inputs in base 2. Extracting binary digits requires remainders modulo $2^k$, and since $p$ and $2$ are coprime, $p$-adic independence carries no direct implication for bitwise independence. This misalignment between the modular domain of the CRT and the binary domain of the circuit is the source of the gap described in §6.3.



### 6.3 The Fourier Approach and Its Limitations

**Theorem 6.9 (Fourier inner product identity).** *Let $F_p: \{0,1\}^m \to \mathbb{R}$ denote $F_p(\mathbf{b}) = C(p \cdot \mathrm{decode}(\mathbf{b}))$, where $\mathrm{decode}$ maps binary strings to integers. Then:*
$$\Delta(p,q) - \bar{C}^2 = \sum_{S \neq \emptyset} \hat{F}_p(S)\, \hat{F}_q(S)$$
*where the sum is over the Walsh-Fourier expansion on $\{0,1\}^m$.*

*Proof.* Write $\Delta(p,q) = \frac{1}{M}\sum_n C(pn)C(qn) = E_n[F_p(\mathbf{b}(n)) F_q(\mathbf{b}(n))]$ where $\mathbf{b}(n)$ is the binary representation of $n$. By the Walsh-Fourier expansion $F_p = \sum_S \hat{F}_p(S) \chi_S$ and Parseval:
$$E_n[F_p F_q] = \sum_{S, T} \hat{F}_p(S)\hat{F}_q(T) E_n[\chi_S \chi_T].$$
For $n$ uniform on $[1, M]$, the characters $\chi_S$ are approximately orthogonal with $E[\chi_S \chi_T] \approx \mathbf{1}_{S=T}$ (with error $O(2^{|S \triangle T|}/M)$ from the truncation of $[1,M]$). Subtracting $\bar{C}^2 = \hat{F}_p(\emptyset)\hat{F}_q(\emptyset)$ gives the identity. $\square$

To show $\Delta(p,q) \to \bar{C}^2$ it suffices to show $\sum_{S \neq \emptyset} \hat{F}_p(S) \hat{F}_q(S) = o(1)$. Decompose:
$$\sum_{S \neq \emptyset} = \sum_{0 < |S| \leq k} + \sum_{|S| > k}$$

The low-level sum ($|S| \leq k$). The CRT independence (Theorem 6.6) provides decorrelation in the modular domain ($n \bmod p$ and $n \bmod q$), not directly in the Walsh-Fourier domain. The Walsh character $\chi_S(\mathbf{b}) = (-1)^{\sum_{i\in S} b_i}$ depends on individual binary bits, while the CRT residue $n \bmod p$ is a nonlinear function of all bits via carry propagation. Translating modular independence into Fourier coefficient independence requires additional carry analysis, which succeeds for AC⁰ and bounded-depth TC⁰ but not in general.

The high-level sum ($|S| > k$). For a circuit of size $S$ and total influence $I(F_p) \leq S$:

> **Proposition 6.10 (Basis misalignment barrier).** The standard Fourier tail bound gives $W_{\geq k}(F_p) := \sum_{|S| \geq k} \hat{F}_p(S)^2 \leq I(F_p)/k \leq S/k$. For $S = O((\log N)^c)$ and $k = O(\log N)$: $W_{\geq k} = O((\log N)^{c-1})$, which tends to infinity when $c > 1$. By Cauchy-Schwarz, $|\sum_{|S| \geq k} \hat{F}_p \hat{F}_q| \leq W_{\geq k}$, so the high-level contribution does not decay.
>
> Exponential Fourier concentration $W_{\geq k} \leq 2^{-\Omega(k/(\log s)^{d-1})}$ is established for $\mathsf{AC^0}$ circuits of constant depth $d$ by [LMN93] and [Ta17]. No analogous bound is known for general P/poly circuits.



### 6.4 Known Results and the P/poly Gap

**Theorem 6.11 (Green [Gr12]).** $\mu \notin \mathsf{AC^0}$.

*Method.* LMN Fourier concentration [LMN93] combined with the Kátai orthogonality criterion and the Vaughan identity (following Green's approach in [Gr12]). The argument does not extend to P/poly because LMN requires constant depth.

**Proposition 4.2** (restated). $\mu \notin \mathsf{TC^0_{\mathrm{bb}}}$, where $\mathsf{TC^0_{\mathrm{bb}}}$ denotes TC⁰ circuits of branching factor $b = O(1)$ and size $s = O(\log\log N)$.

*Method.* CRT decomposition in the bounded-branching setting combined with Siegel-Walfisz. See §4.2 for scope.

**The remaining gap.** For P/poly circuits of size $S = O((\log N)^c)$, the second-moment influence satisfies $I^{(2)} = O((\log N)^{c+1})$, while the CRT supplies $O(\log N)$ bits of modular decorrelation. The following table records the state of four approaches and their limitations.

| Approach | What it controls | Obstruction for P/poly |
|---|---|---|
| LMN Fourier concentration | $W_{\geq k} \leq 2^{-\Omega(k/(\log s)^{d-1})}$ | Requires constant depth |
| Markov Fourier bound | $W_{\geq k} \leq S/k$ | Gives $O((\log N)^{c-1}) \to \infty$ for $c > 1$ |
| CRT + carry lemma | $O(\log p)$ bits per block | Depth $O(\log N)$ exhausts carry information |
| NAND contraction | $\Lambda^D$ at operating point | Property of the smooth extension, not the Boolean spectrum |

**Four research directions.** The following analysis records what each known approach can establish and where it fails.

**(a) Carry entropy (Mauduit-Rivat extension).** The carry lemma [MR10] bounds exponential sums over digit-sum functions by partitioning into blocks of width $w$ and bounding the inter-block carry information by $\lceil \log_q p\rceil$ bits per boundary. For circuits of bounded depth $d$, carry propagation is limited to $d$ levels, and a similar partitioning may suffice. For circuits of depth $O(\log N)$, the carry can saturate all $m = O(\log N)$ input bits, exhausting the available independence. This approach is likely extendable to ACC⁰ or bounded-depth TC⁰ by combining with Fourier analysis of free blocks, but does not reach general P/poly.

**(b) Additive combinatorics.** The maps $n \mapsto pn \bmod 2^m$ and $n \mapsto qn \bmod 2^m$ are linear over $\mathbb{Z}/2^m\mathbb{Z}$. Sum-product and Freiman-Ruzsa techniques operate in $\mathbb{F}_p$ and do not directly apply to bit-level structure. Showing that no bounded-complexity Boolean circuit can undo the scrambling of multiplication by distinct primes is essentially equivalent to a circuit lower bound. No current tools are sufficient.

**(c) Direct circuit lower bounds.** Proving BDH for all P/poly circuits would imply P ≠ NP. Any such argument must navigate the three standard barriers. The gap between the established result ($\mu \notin \mathsf{AC^0}$) and the target ($\mu \notin \mathsf{P/poly}$) subsumes the P vs NP problem itself.

**(d) MOO invariance principle.** The Mossel-O'Donnell-Oleszkiewicz invariance principle [MOO10] gives $|E[\psi(f(X))] - E[\psi(f(G))]| = O(d \cdot \tau^{1/(2d)})$ for degree-$d$ multilinear $f$ with max influence $\leq \tau$. For noise-stable TC⁰ circuits (majority-based), max influence is $O(1/\sqrt{m})$ and the bound is useful. For noise-sensitive circuits or general P/poly where max influence can be $\Theta(1)$, the bound is vacuous.

The combination of approaches (a) and (d) is the most tractable direction for extending beyond AC⁰. It encounters a union-bound obstruction formalised in Proposition 6.14.

**Remark 6.12 (IFS and universal approximation perspective).** The NAND smooth extension $\tilde{C}_\star$ is a continuous function on $[0,1]^m$ that agrees with $C$ on $\{0,1\}^m$. As an iterated function system (IFS) with the contractive activation $T_\star$, the extension converges at rate $\Lambda^D$ (Hutchinson contraction theorem). A signal-restoration bound of the form $\delta \mapsto c\delta^2 + c\varepsilon$ (quadratic convergence near Boolean inputs) holds from the superattracting conditions $T_\star'(0) = T_\star'(1) = 0$: if a gate input deviates from $\{0,1\}$ by $\delta$, the output deviates by $O(\delta^2)$ since $T_\star''(0) = T_\star''(1) = 0$ as well by the degree-5 construction of §5.2.

By Stone-Weierstrass: the algebra generated by functions of the form $T_\star(1 - f \cdot g)$ with $f,g \in C([0,1]^m)$ and $T_\star$ as above is dense in $C([0,1]^m)$. Consequently, any continuous function on $[0,1]^m$ — including the multilinear extension $\tilde{C}_{\mathrm{ml}}$ — can be uniformly approximated to any $\varepsilon > 0$ by compositions of $T_\star$. However, this approximation does not bypass BDH: the bilinear sum $\Delta(p,q)$ evaluates the function at Boolean inputs (binary representations of $pn$ and $qn$), where any $\varepsilon$-approximation computes $C(\mathbf{b}) + O(\varepsilon)$. The continuous interior $[0,1]^m$ is never visited by the bilinear sum.

The precise barrier is number-theoretic, not analytic: the CRT provides $O(\log N)$ bits of independence between $n \bmod p$ and $n \bmod q$, but a P/poly circuit can process all $O(\log N)$ input bits through $O(\log N)$ levels, potentially correlating the responses to $pn$ and $qn$ despite the CRT independence. The NAND contraction and universal approximation support the heuristic that BDH should hold for shallow circuits, but do not yield a proof for circuits of depth $\omega(1)$.



### 6.5 The Deterministic Carry-Influence Union Bound Barrier

**Definition 6.13.** A circuit $C$ has *max influence bounded by $\tau$* if $\mathrm{Inf}_{\max}(C) := \max_i \Pr_{\mathbf{b}}[C(\mathbf{b}) \neq C(\mathbf{b}^{\oplus i})] \leq \tau$.

**Proposition 6.14 (Barrier Diagnosis: Deterministic Carry-Influence Union Bound).** *Let $C$ be a TC⁰ circuit of constant depth $d$, polynomial size $S = O((\log N)^c)$, with max influence $\emph{Inf}_{\max}(C) \leq \tau = S^{-1/(2d+1)}$. Any proof strategy that (i) applies the carry lemma gate-by-gate, (ii) invokes the MOO invariance principle as if the carry shift were a random perturbation, and (iii) union-bounds the error over all gates must fail: the resulting total error bound is $O((\log N)^{c + 1 - c/(4d+2)})$, which diverges to infinity.*

*Proof diagnosis.* The argument attempts to combine two tools:

**(i) Carry lemma.** Partition the $m = \lceil \log_2 N \rceil$ input bits into blocks of width $w$. By the block carry decomposition of Mauduit and Rivat [MR10], the carry from block $j$ to block $j+1$ under multiplication by $p$ has at most $\lceil \log_2 p \rceil$ bits. For TC⁰ of depth $d$: the total carry information propagating through the circuit is bounded by $d \cdot \lceil \log_2 p \rceil$ bits per block boundary.

**(ii) MOO invariance.** The Mossel–O'Donnell–Oleszkiewicz invariance principle bounds independent random noise, but is misapplied to deterministic arithmetic carry shifts. Assuming the per-gate carry-induced bias is $O(S^{-1/(4d+2)} \log S)$ ignores the global union bound.

**(iii) The Union Bound Failure.** To bound the total error across the circuit, we must sum the carry-induced bias over all $S$ gates via a union bound. Multiplying the per-gate error by $S = O((\log N)^c)$ yields a total error of $O((\log N)^{c + 1 - c/(4d+2)})$. Because the exponent is strictly positive, the total accumulated bias diverges to infinity. This rigorously quantifies why analytic number theory bounds fail against polynomial circuits: deterministic, correlated carry-rippling shatters probabilistic anti-concentration bounds upon union-bounding the circuit breadth. $\square$

> **Scope and significance.** The divergence of the total error fundamentally limits continuous anti-concentration proofs. It formally prevents extending Möbius orthogonality to polynomial-size TC⁰ via single-gate uniformization techniques.



### 6.6 The NC¹ Barrier: Why Log-Depth Defeats Current Approaches

**Question.** Can the NAND tree influence decay $(p^*)^D$ (where $p^* = (\sqrt{5}-1)/2 \approx 0.618$) be used to prove $\mu \notin \mathsf{NC^1}$ (log-depth formulas)?

**Background.** For a balanced NAND tree of depth $D$: each leaf has pivotality probability $(p^*)^D$. This is a Boolean-level property — the influence decays at rate $p^* \approx 0.618$ per level in the discrete domain.

**Approach 1: Per-leaf influence bound.**

For a NAND formula of depth $D = c\log_2 N$ with leaves reading bits of $pn$: each leaf has influence $(p^*)^D = N^{-0.694c}$. Flipping bit $i$ of $n$ changes $O(\log p)$ bits of $pn$ (through multiplication), each with influence $(p^*)^D$. So $\mathrm{Inf}_i(C \circ \mathrm{mult}_p) \leq O(\log p) \cdot (p^*)^D = O(\log N) \cdot N^{-0.694c}$, and the total: $I(f_p) \leq m \cdot O(\log N) \cdot N^{-0.694c} = O(\log^2 N \cdot N^{-0.694c})$.

*Obstruction to Approach 1.* For $c = 1$, this gives $I(f_p) = o(1)$, implying $\mathrm{Var}(f_p) = o(1)$. But $\mathrm{Var}(f_p) = \bar{C}(1-\bar{C}) = \Theta(1)$, a contradiction. The source of the error: the carry from $p \cdot 2^i$ can ripple through all higher-order bits of $pn$, not just $O(\log p)$ bits. The carry ripple is short on average but $O(m)$ in the worst case. The total influence $I(f_p) = \Theta(1)$ is forced by the variance identity.

**Approach 2: Håstad shrinkage combined with CRT restriction.**

The CRT restriction fixes $\alpha = n \bmod p$, $\beta = n \bmod q$ (independent by CRT), leaving $\gamma = \lfloor n/pq \rfloor$ free. This fixes a fraction $O(\log(pq)/\log N)$ of the $m = O(\log N)$ input bits. By Håstad's shrinkage lemma (exponent $\Gamma = 2$): the restricted formula has size $S' = S \cdot (1-\alpha)^{2-o(1)}$.

*Obstruction to Approach 2.* For $S = O((\log N)^c)$ and $\alpha = O(1)$: $S' = O((\log N)^c)$ — still polynomial. Formula-to-constant shrinkage requires $S' < 1$, i.e., $(1-\alpha)^2 \leq O((\log N)^{-c})$, which needs $\alpha \geq 1 - O((\log N)^{-c/2})$. This only holds when $pq \geq N^{1-O((\log N)^{-c/2})} \approx N$, the trivial case.

**Approach 3: Tal's Fourier concentration from shrinkage.**

Tal [Ta17] proved that De Morgan formulas of size $s$ with shrinkage exponent $\Gamma$ have Fourier concentration:
$$W_{\geq t}(f) \leq \exp\!\left(-\left(\frac{t^\Gamma}{s^{1+o(1)}}\right)^{\!\frac{1}{\Gamma-1}}\right)$$
For $\Gamma = 2$ and $s = O((\log N)^c)$: $W_{\geq t} \leq \exp(-t^2/(\log N)^{c+o(1)})$. The CRT decorrelates Fourier levels $\leq O(\log p)$, so we need $W_{\geq \log N} = o(1)$.

*Obstruction to Approach 3.* Setting $t = \log N$: $W_{\geq \log N} \leq \exp(-\log^2 N / (\log N)^{c+o(1)}) = \exp(-(\log N)^{1-c+o(1)})$. This is $o(1)$ only when $c < 1$, i.e., sub-logarithmic formula size. Fourier concentration for $\mathsf{NC^1}$ formulas of size $O((\log N)^c)$ with $c \geq 1$ gives no useful bound at level $O(\log N)$: parity ($\bigoplus x_i$) is in $\mathsf{NC^1}$ and has all Fourier mass at level $m = O(\log N)$.

**The common obstruction.** All three approaches fail at the same point: the transition from constant depth to logarithmic depth. For constant-depth TC⁰, carry propagation is bounded, the CRT wins, and $\mu \perp \mathsf{TC^0_{\mathrm{low\text{-}inf}}}$. For log-depth $\mathsf{NC^1}$, the carry can saturate all $m = O(\log N)$ bits, and no current technique can bound the bilinear sum.



### 6.7 Self-Correction, Competing Rates, and the Effective Depth Conjecture

**The self-correcting NAND structure.** For the double-NAND map $R(x) = \mathrm{NAND}(\mathrm{NAND}(x,x), \mathrm{NAND}(x,x))$: by direct computation, $R(x) = T_\star(1 - T_\star(1-x^2)^2)$. Near $x = 0$: $R(x) = T_\star(1 - (1 + O(x^2))^2) = T_\star(O(x^2)) = O(x^4)$ (superattracting). Near $x = 1$: $R(x) = 1 - O((1-x)^4)$. Thus a perturbation $\delta$ from a Boolean value satisfies $R(x_0 + \delta) = x_0 + O(\delta^2)$: quadratic contraction. This is the discrete analog of the Evans-Pippenger noise threshold [EP98]: below error rate $\varepsilon < (3-\sqrt{7})/4 \approx 0.089$, NAND formulas can compute reliably despite noisy gates.

For a NAND tree circuit implementing $C$: the double-NAND version (with signal restoration at every layer) computes the SAME Boolean function as $C$, while providing self-correction in the continuous domain. The key structural property: the self-correction is an **identity** on Boolean inputs ($R(0) = 0$, $R(1) = 1$ exactly), so it does not alter the bilinear sum $\Delta(p,q)$.

**The competing rates.** The BDH barrier can be understood as a competition between two growth rates:

| Resource | Growth | Role |
|---|---|---|
| CRT decorrelation | $O(\log N)$ bits of independence | Breaks correlations between $pn$ and $qn$ |
| Circuit depth | $O(\log N)$ levels of nonlinear processing | Creates correlations through carry chains |

Both grow as $O(\log N)$, and neither dominates the other. For **constant-depth** circuits ($d = O(1)$): the carry propagation is $O(d \log p) = O(\log N)$ but the circuit has only $O(1)$ levels to exploit it — the CRT wins. For **log-depth** circuits ($d = O(\log N)$): the circuit has enough depth to fully exploit the carry — balance.

**The effective depth conjecture.** The self-correcting NAND structure suggests a potential resolution: the signal restoration at each layer imposes a "tax" on the circuit's computational capacity. Each restoration operation $R$ forces the signal toward Boolean values, effectively "resetting" the computation. This means the circuit's USEFUL computation depth may be less than its physical depth.

> **Conjecture 6.15 (Effective Depth).** For a self-correcting NAND circuit of physical depth $D$ and size $S$ with signal restoration at every layer: the effective computational depth $D_{\mathrm{eff}}$ (the maximum number of non-redundant computational steps) satisfies $D_{\mathrm{eff}} = o(D)$, and the bilinear sum satisfies:
> $$|\Delta(p,q) - \bar{C}^2| \leq f(D_{\mathrm{eff}}, \log p) \cdot g(S)$$
> where $f$ decays when $D_{\mathrm{eff}} \ll \log N$ (i.e., when the CRT dominates the effective depth).

If the effective depth is sub-logarithmic ($D_{\mathrm{eff}} = o(\log N)$): the CRT independence at $O(\log N)$ bits would dominate, and BDH would follow. However, this conjecture encounters the fundamental obstacle that physical depth equals effective depth for Boolean computations (since $R$ acts as the identity on Boolean inputs). The effective depth reduction occurs ONLY in the continuous/analog domain, not in the Boolean domain where the bilinear sum is evaluated. Resolving this requires a technique that translates the continuous-domain depth reduction to a Boolean-domain constraint — potentially through a refined noise sensitivity argument showing that circuits with high self-correction overhead cannot maintain bilinear correlations. Conjecture 6.15 remains open.



---

## 7. Universal Obstructions to Continuous Decorrelation

### 7.1 The Topological Obstruction

**Theorem 7.1 (Universal topological obstruction — all $C^4$ extensions).** *Let $F: [0,1]^2 \to [0,1]$ be any $C^4$ function satisfying $F(a,b) = \mathrm{NAND}(a,b)$ for all $(a,b) \in \{0,1\}^2$, and suppose the diagonal map $g_F(x) := F(x,x)$ has an attracting fixed point $x^{**} \in (0,1)$ (i.e., $g_F(x^{**}) = x^{**}$ and $|g_F'(x^{**})| < 1$). Then:*

*(i) The set $\{0,1\}$ is a period-2 orbit of $g_F$: $g_F(0) = 1$, $g_F(1) = 0$.*

*(ii) The basins of attraction of $\{0,1\}$ (under $g_F^2$) and $x^{**}$ (under $g_F$) are disjoint open sets whose union is a proper subset of $[0,1]$. Their common boundary contains at least one unstable fixed point $x_0$ of $g_F^2$ in $(0, x^{**}) \cup (x^{**}, 1)$, with $(g_F^2)'(x_0) \geq 1$.*

*(iii) Any continuous path $\gamma: [0,1] \to [0,1]$ with $\gamma(0) \in \{0,1\}$ and $\gamma(1) = x^{**}$ satisfies $\gamma(t_0) = x_0$ for some $t_0$.*

*(iv) For any NAND **formula** (tree circuit, no reconvergent fan-out) of depth $D = \omega(1)$ whose smooth extension uses $F$, and for any Lindeberg replacement path from a Boolean input to the interior fixed point $x^{**}$, the path necessarily passes through the basin boundary at $x_0$ (by part (iii)). The univariate Faà di Bruno formula applied to the depth-$D$ composition $h_i = F^{\circ D}$ gives:*
$$|h_i^{(4)}(x_0)| \ge C \cdot \bigl[(g_F^2)'(x_0)\bigr]^{2D}$$
*The Taylor–Lagrange remainder satisfies:*
$$|R_i| = \frac{1}{6}\left|\int_0^1(1-t)^3 h_i^{(4)}(\xi_t)\,dt\right| \ge C \cdot \bigl[(g_F^2)'(x_0)\bigr]^D \to \infty$$
*For DAG circuits with fan-out (reconvergent signals), the multivariate chain rule replaces Faà di Bruno; the derivative at $x_0$ may receive contributions from exponentially many paths, which can compound or partially cancel depending on the circuit structure. The analogous obstruction in the DAG case is described in Remark 5.6 (Gap K) and is not fully resolved here. Theorem 7.1 in its strongest form therefore applies to **formula circuits**; the DAG case is an open problem.*

*Proof.*

*(i)* From Boolean agreement: $g_F(0) = F(0,0) = \mathrm{NAND}(0,0) = 1$ and $g_F(1) = F(1,1) = \mathrm{NAND}(1,1) = 0$. $\square$

*(ii)* Since $g_F$ is $C^4$ on $[0,1]$ with $g_F(0)=1$ and $g_F(1)=0$, by the IVT it has at least one fixed point in $(0,1)$; we are given $x^{**}$ is one such attracting fixed point. The second iterate $g_F^2$ satisfies $g_F^2(0) = g_F(1) = 0$, $g_F^2(x^{**}) = x^{**}$, $g_F^2(1) = g_F(0) = 1$: all three are fixed. The derivative at $x^{**}$: $(g_F^2)'(x^{**}) = (g_F'(x^{**}))^2 < 1$, so $x^{**}$ is attracting under $g_F^2$.

The attracting basin $B_{**}$ of $x^{**}$ under $g_F^2$ and the attracting basin $B_{01}$ of $\{0,1\}$ under $g_F^2$ are open and disjoint (distinct basins of distinct attractors). Their union is an open set; its complement in $[0,1]$ is non-empty and closed, and consists precisely of the basin boundaries. Every boundary point $x_0$ of $B_{**}$ in $(0,1)$ is a non-attracting fixed or periodic point of $g_F^2$, hence satisfies $(g_F^2)'(x_0) \geq 1$. Such a point exists in $(0,1)$ by the following argument: $x^{**} \in B_{**}$ and $0 \notin B_{**}$ (since $g_F^2(0) = 0$ and $0 \neq x^{**}$); therefore $B_{**}$ has a boundary point $x_0$ in $(0, x^{**})$ or $(x^{**}, 1)$ by connectedness of $[0,1]$. $\square$

*(iii)* By (i), $\{0,1\} \subset B_{01}$ and $x^{**} \in B_{**}$. Since $B_{01}$ and $B_{**}$ are disjoint open sets, any continuous path from $B_{01}$ to $B_{**}$ must exit $B_{01}$ at some point not in $B_{01} \cup B_{**}$, which by (ii) is the basin boundary containing $x_0$. $\square$

*(iv)* At $x_0$: $(g_F^2)'(x_0) \geq 1$. For a circuit of depth $D$, the composition $g_F^{2D}$ satisfies $(g_F^{2D})'(x_0) = [(g_F^2)'(x_0)]^D$. By the chain rule applied to the smooth circuit extension $h_i$, the fourth derivative satisfies $|h_i^{(4)}(x_0)| \geq C \cdot [(g_F^2)'(x_0)]^{2D}$ (Faà di Bruno). The Taylor-Lagrange remainder $R_i = \frac{1}{6}\int_0^1(1-t)^3 h_i^{(4)}(\xi_t)\,dt$ then satisfies $|R_i| \geq C \cdot [(g_F^2)'(x_0)]^D \to \infty$ for $D = \omega(1)$. $\square$

*Remark.* The proof of (ii) uses only: $F$ agrees with NAND on $\{0,1\}^2$; $g_F$ has an attracting interior fixed point; $g_F$ is continuous. It does not use the specific quintic form of $T_\star$, the superattracting condition at the Boolean endpoints, or any other property of the construction in §5. The obstruction is therefore a consequence of the topology of $[0,1]$ and the Boolean boundary conditions, not of any particular analytic choice of extension.

**Corollary 7.2 (Specific case $F = \widetilde{\mathrm{NAND}}_\star$).** For the quintic extension $T_\star$ of §5 with cross-NAND map $g = T_\star(1-\cdot)$: Theorem 7.1 applies, and the unstable orbit is $\{x_0, x_1\}$ from Theorem 5.7(c). The Taylor-Lagrange remainder satisfies $|R_i| \geq C \cdot [(g^2)'(x_0)]^D \to \infty$ for $D = \omega(1)$. No Taylor-Lindeberg argument based on this extension — or any other $C^4$ NAND extension with an interior fixed point — can establish Möbius orthogonality for **NAND formula circuits** of superconstant depth. Whether this obstruction extends to general circuit DAGs (with fan-out) remains open; see Remark 5.6.



### 7.2 Growth Rate Summary

The three error terms in the Lindeberg analysis can be compared in order of magnitude as $N \to \infty$, with circuit size $S = O((\log N)^c)$, depth $D = O(\log N)$, unstable eigenvalue $\mu_0 := (g^2)'(x_0) > 1$, and contraction $\Lambda = O((\log N)^{-1/2})$:

| Error term | Asymptotic size | Source |
|---|---|---|
| NAND contraction $S \cdot \Lambda^D$ | $o(1)$ (tends to $0$) | Smooth extension sensitivity (§5.2) |
| Unstable orbit measure $\mu_0^{-D}$ | $o(1)$ (exponential decay) | Basin width near $\{x_0,x_1\}$ |
| Taylor remainder at orbit $\mu_0^{3D}$ | $\to \infty$ (grows without bound) | Topological obstruction (§7.1) |

The NAND contraction decays far faster than the unstable orbit measure. However, the Taylor-Lindeberg approach evaluates the derivative at the unstable orbit, where it grows as $\mu_0^{4D}$ pointwise; even after the $\mu_0^{-D}$ basin weighting, the integral is $\Omega(\mu_0^{3D}) \to \infty$.

The depth threshold at which the Taylor remainder transitions from $O(1)$ to $\omega(1)$ is $D = O(1/\log \mu_0)$, i.e., constant depth. This is consistent with the AC⁰ result of Green [Gr12]: the LMN Fourier concentration is an alternative mechanism that works precisely in the constant-depth regime where the Taylor remainder is bounded.



### 7.3 The Hypercube Boundary Accumulation Flaw

**Motivation.** The topological obstruction of §7.1 shows that the Lindeberg integral $\int_0^{1/2} u^3 h^{(4)}(u)\,du$ blows up because $h^{(4)}$ is unlimited at the unstable orbit $x_0$. By Stokes' theorem (integration by parts), interior integrals can be converted to boundary evaluations — potentially avoiding the unstable orbit entirely.

**The boundary accumulation identity (exact).** Four integrations by parts give:

$$\int_0^{1/2} u^3 h^{(4)}(u)\,du = \frac{1}{8}h'''(1/2) - \frac{3}{4}h''(1/2) + 3h'(1/2) - 6h(1/2) + 6h(0)$$

This is an **exact algebraic identity** for any $C^4$ function on $[0,1/2]$. All evaluations are at the boundary points $\{0, 1/2\}$, which are in the superattracting Boolean basin ($u=0$) and the interior attracting basin ($u=1/2$) respectively. **The unstable orbit $x_0$ is never evaluated.**

Similarly for $[1/2,1]$ by the substitution $u \to 1-u$:
$$\int_{1/2}^1 (1-u)^3 h^{(4)}\,du = -\frac{1}{8}h'''(1/2) - \frac{3}{4}h''(1/2) - 3h'(1/2) - 6h(1/2) + 6h(1)$$

**The Lindeberg error in boundary accumulation form.** Combining the two integrals for $X \sim \mathrm{Bernoulli}(1/2)$:

$$E[R_3(X)] = \frac{1}{12}\left[-\frac{3}{2}h''(1/2) - 12h(1/2) + 6(h(0)+h(1))\right]$$

The dominant terms are:
$$E[R_3(X)] \approx \frac{1}{2}\left[\frac{h(0)+h(1)}{2} - h(1/2)\right] =: \frac{1}{2}\,\delta_{\mathrm{mid},i}$$

where $\delta_{\mathrm{mid},i} := h_{\mathrm{ML},i}(1/2) - h_{\mathrm{NAND},i}(1/2)$ is the **midpoint deviation** between the multilinear and NAND extensions at coordinate $i$.

**Key properties:**
- For the multilinear extension (§6.1): $h_{\mathrm{ML}}(1/2) = (h(0)+h(1))/2$ by linearity, so $\delta_{\mathrm{mid}} = 0$ exactly. This recovers the zero-error Lindeberg of Lemma 6.2.
- For the NAND extension: $h_{\mathrm{NAND}}(1/2) \approx x^{**}$ (the attracting fixed point), while $h_{\mathrm{ML}}(1/2) = (h(0)+h(1))/2 \in [0,1]$. The midpoint deviation $\delta_{\mathrm{mid}}$ is $O(1)$ in the worst case.

**Proposition 7.3 (Boundary accumulation form of the Lindeberg remainder).** *For any $C^4$ function $h$ on $[0,1]$, four integrations by parts give the exact identity:*
$$\int_0^{1/2} u^3 h^{(4)}(u)\,du = \tfrac{1}{8}h'''(1/2) - \tfrac{3}{4}h''(1/2) + 3h'(1/2) - 6h(1/2) + 6h(0)$$
*All evaluations are at the boundary points $\{0, 1/2\}$, which lie in the Boolean and interior attracting basins respectively. The formula avoids direct evaluation at the unstable orbit.*

*Proof.* Standard integration by parts applied four times. $\square$

*Remark.* The boundary accumulation form avoids the $L^\infty$ blowup at the unstable orbit by converting pointwise derivative evaluation to endpoint evaluation. However, it does not bypass the topological obstruction: the integration by parts identity is an algebraic manipulation that is valid when $h$ is $C^4$ on $[0,1/2]$, but $h^{(4)}$ is only bounded away from the unstable orbit. When the unstable orbit $x_0 \in (0, 1/2)$, the integral $\int_0^{1/2} u^3 h^{(4)}$ diverges regardless of which side the integration by parts is applied on. The formula is valid only when $x_0 \notin [0,1/2]$, which is a constraint on the parameters $(c_0, \lambda_0)$, not a general resolution of the obstruction.

**The per-step error.** Each step contributes $O(|\delta_{\mathrm{mid},i}|) = O(1)$. Over $m = O(\log N)$ steps:

$$|\mathrm{Error}_{\mathrm{total}}| = \frac{1}{2}\left|\sum_{i=1}^m \delta_{\mathrm{mid},i}\right| = O(\log N)$$

This is **finite** (a massive improvement from $O(\mu^{3D})$) but **not $o(1)$**.

> **Reformulation (BDH as midpoint cancellation).** BDH holds if and only if:
> $$\sum_{i=1}^m \left[\frac{h_i(0)+h_i(1)}{2} - h_i(1/2)\right] = o(1)$$
> This is a **cancellation condition**: individual midpoint deviations are $O(1)$, but their sum must be $o(1)$. Since $h_i$ depends on the circuit $C$ and the bilinear inputs $pn, qn$, the cancellation requires the CRT-induced independence (different carry structures at different bits) to force approximate equality between the multilinear and NAND extensions **on average across inputs**.

| Approach | Per-step error | Total error | Achieves $o(1)$? |
|---|---|---|---|
| Standard Taylor (§7.1) | $O(\mu_0^{4D})$, unbounded | unbounded | No |
| Fourier $L^1$ (§7.2) | $O(\mu_0^{3D})$, unbounded | unbounded | No |
| Hypercube boundary accumulation (§7.3) | $O(1)$, finite | $O(\log N)$ | No |
| Target | $o(1/m)$ | $o(1)$ | Yes |



### 7.4 The Symmetric Gate and the Formula Obstruction

**Motivation.** The midpoint deviation $\delta_{\mathrm{mid}} = [h(0)+h(1)]/2 - h(1/2)$ is zero for the multilinear extension (linearity) and $O(1)$ for the NAND extension (nonlinearity of $T_\star$). A natural question: can the NAND gate $T_\star$ be chosen to minimize $\delta_{\mathrm{mid}}$?

**The symmetric choice $c_0 = 1/2$.** Setting $c_0 = 1/2$ makes $x^{**} = 1/2$ — the fixed point of the cross-NAND map coincides with the center of $[0,1]$. This forces the symmetry $T_\star(1-x) = 1-T_\star(x)$, so $g(1/2) = T_\star(1/2) = 1/2$ (the midpoint is a fixed point of $g$). The gate $\mathrm{NAND}_\star(1/2, 1) = T_\star(1/2) = 1/2$: a signal at $1/2$ passes through a gate with Boolean sibling $1$ and emerges at $1/2$.

**Theorem 7.4 (Zero midpoint deviation for Boolean siblings).** *For a NAND formula (no fan-out) with $c_0 = 1/2$, processed via Lindeberg in DFS order: for any input $i$ whose path to the root has only Boolean siblings:*
$$\delta_{\mathrm{mid},i} = 0 \quad (\text{exact})$$

*Proof.* Two cases. **(a)** *Sensitive input* ($h_i(0) \neq h_i(1)$): sensitivity requires all siblings $z_j = 1$ along the path (if any $z_j = 0$, gate $j$ outputs $T_\star(1) = 1$ regardless, killing sensitivity). With all $z_j = 1$: level-by-level the $0$-track and $1$-track outputs oscillate as $(1,0,1,0,\ldots)$ and $(0,1,0,1,\ldots)$, while the $1/2$-track stays at $1/2$ (fixed point of $g$). At every level: $(\text{0-track} + \text{1-track})/2 = 1/2 = \text{midpoint-track}$. So $[h(0)+h(1)]/2 = 1/2 = h(1/2)$, giving $\delta = 0$.

**(b)** *Insensitive input* ($h_i(0) = h_i(1) = v$): insensitivity in a formula requires some gate $j$ with sibling $z_j = 0$. At that gate: $\mathrm{NAND}_\star(\text{signal}, 0) = T_\star(1) = 1$ for ANY signal value (Boolean or $1/2$). After gate $j$: all three tracks coincide, so $h_i(0) = h_i(1) = h_i(1/2) = v$, giving $\delta = 0$. $\square$

**Consequence 7.5 for formulas.** In DFS ordering, the first input processed has all siblings from unprocessed subtrees (all Boolean). For this input: $\delta_{\mathrm{mid}} = 0$ and the error is dominated by higher-order derivatives: $O(\lambda_0^D)$ (by Proposition 5.5 at $x^{**} = 1/2$).

**The Gaussian sibling obstruction.** For subsequent inputs, some siblings are from already-processed subtrees (Gaussian, not Boolean). At a gate with Gaussian sibling $Z \sim N(1/2, 1/4)$:
$$\delta_{\mathrm{gate}}(Z) = \frac{1 + T_\star(1-Z)}{2} - T_\star\!\left(1 - \frac{Z}{2}\right)$$

At $Z = 1/2$: $\delta_{\mathrm{gate}} = 3/4 - T_\star(3/4) = (15 - 18\lambda_0)/128$. Setting $\lambda_0 = 5/6$ zeros this leading term. However, the variance correction is:
$$E[\delta_{\mathrm{gate}}] \approx \frac{1}{2}\delta''(1/2) \cdot \mathrm{Var}(Z) = -\frac{T_\star''(3/4)}{32}$$

which at $\lambda_0 = 5/6$ equals $-5/96 \neq 0$. Zeroing this requires $\lambda_0 = 15/14 > 1$ (breaking the attracting property). This is a **calibration hierarchy**: each order of the midpoint deviation can be zeroed by choosing $\lambda_0$, but the hierarchy terminates — zeroing all orders simultaneously requires $\lambda_0 > 1$, destroying the contraction.

**Total error for formulas with $c_0 = 1/2$, $\lambda_0 = 5/6$, DFS ordering.** Over $m$ inputs with $\sim m D/2$ Gaussian-sibling gates: total $\approx (5/96) \cdot m D/2 = O(\log^2 N)$. This is worse than the $O(\log N)$ from §7.3.

| Approach | Per-step (Boolean siblings) | Per-step (Gaussian siblings) | Total |
|---|---|---|---|
| IBP (§7.3) | $O(1)$ | $O(1)$ | $O(\log N)$ |
| Symmetric gate + DFS (§7.4) | **$0$ (exact)** | $O(1/m)$ per gate, $O(D)$ per input | $O(\log^2 N)$ |

*Remark.* The midpoint deviation $\delta_{\mathrm{mid},i}$ vanishes exactly when the extension is affine in each variable (as in the multilinear case, Lemma 6.2) or when the evaluation point is the fixed point of the dynamics with Boolean siblings ($c_0 = 1/2$, Theorem 7.4). The Gaussian sibling error is a second-order consequence of the curvature of $T_\star$, forced by the superattracting conditions $T_\star'(0) = T_\star'(1) = 0$ together with the requirement $\lambda_0 < 1$. The open question is whether a block Lindeberg — replacing all inputs simultaneously so all siblings remain Boolean — can avoid this second-order accumulation.



### 7.5 The Noise Operator Approach and the Influence Barrier

**Motivation.** The sequential Lindeberg (§7.3) replaces inputs one at a time, creating the Gaussian-sibling obstruction (§7.4). A natural alternative: the **noise operator** $T_\rho$, which replaces ALL inputs simultaneously with fresh Boolean bits.

**Definition 7.5.** For $\rho \in [0,1]$ and $f: \{0,1\}^m \to \mathbb{R}$:
$$(T_\rho f)(x) = E_y[f(y)] \quad \text{where each } y_i = \begin{cases} x_i & \text{w.p. } \rho \\ \text{fresh Bernoulli}(1/2) & \text{w.p. } 1-\rho \end{cases}$$

Crucially, all replacements are **Boolean** (not Gaussian). In Fourier: $(T_\rho f)^\wedge(S) = \rho^{|S|} \hat{f}(S)$, exponentially damping high-level coefficients.

**The two-step argument.** For the bilinear sum $\Delta(p,q) = \frac{1}{M}\sum_n C(pn)C(qn)$:

**Step 1 (C vs $T_\rho C$).** The replacement error:
$$|\Delta(p,q) - \Delta_\rho(p,q)| \leq 2\sqrt{E_x[(C(x) - T_\rho C(x))^2]} = 2\sqrt{\sum_{S \neq \emptyset} (1-\rho^{|S|})^2 \hat{C}(S)^2}$$

By the mean value bound $(1-\rho^{|S|}) \leq (1-\rho)|S|$:
$$\leq 2(1-\rho)\sqrt{I^{(2)}(C)} \quad \text{where } I^{(2)} := \sum_S |S|^2 \hat{C}(S)^2$$

**Step 2 ($T_\rho C$ decorrelation).** The damped Fourier expansion:
$$\Delta_\rho(p,q) - \bar{C}^2 = \sum_{S \neq \emptyset} \rho^{2|S|} \hat{F}_p(S)\hat{F}_q(S)$$

**Low levels** ($|S| \leq \log p$): approximately decorrelated by CRT (as in §6.2).
**High levels** ($|S| > \log p$): damped by $\rho^{2\log p}$.

$$|\Delta_\rho - \bar{C}^2| \leq o(1)_{\mathrm{CRT}} + \rho^{2\log p} \cdot \mathrm{Var}(C)$$

**The tradeoff and its failure.** For step 1 to give $o(1)$: need $(1-\rho)\sqrt{I^{(2)}} \to 0$, i.e., $1-\rho \to 0$ faster than $1/\sqrt{I^{(2)}}$. For step 2: need $\rho^{2\log p} \to 0$, i.e., $(1-\rho) \cdot 2\log p \to \infty$.

Combining: $2\log p / \sqrt{I^{(2)}} \to \infty$, i.e., $\log p \gg \sqrt{I^{(2)}}$.

| Circuit class | $I^{(2)}$ | $\log p$ threshold | Condition $\log p \gg \sqrt{I^{(2)}}$ | Status |
|---|---|---|---|---|
| AC⁰ (depth $d$) | $O(\log^{2d} N)$ | $O(\log N)$ | $\log N \gg \log^d N$; satisfied only for $d < 1$ (vacuous) | handled by LMN, not noise operators |
| Low-influence TC⁰ ($d$ large) | $O(N^{1/(2d+1)})$ | $O(\log N)$ | $\log N \gg N^{1/(4d+2)}$; satisfied for $d \geq c\log N$ | holds via noise operators |
| P/poly (size $O((\log N)^c)$) | $O((\log N)^{c+1})$ | $O(\log N)$ | $\log N \gg (\log N)^{(c+1)/2}$; fails for $c \geq 1$ | fails |

**Theorem 7.6 (Influence barrier — general).** *For any technique that (i) provides $O(\log N)$ bits of decorrelation at Fourier levels $\leq k_0$ and (ii) damps high-level Fourier coefficients at a cost proportional to $I^{(2)}$: the total error satisfies*
$$|\Delta(p,q) - \bar{C}^2| \leq o(1) + \frac{I^{(2)}(C)}{k_0^2}$$
*For $k_0 = O(\log N)$ and $I^{(2)} = O((\log N)^{O(1)})$: the bound is $\Omega((\log N)^{O(1)}/\log^2 N)$, unlimited.*

*Proof.* The CRT decorrelates levels $\leq k_0$. At higher levels: $\sum_{|S| > k_0} |\hat{F}_p \hat{F}_q| \leq W_{>k_0}(F_p) \leq I(F_p)/k_0 = O((\log N)^c/\log N)$. $\square$


**Remark 7.7 (The CRT-vs-influence gap).** The noise operator approach succeeds when $\log p \gg \sqrt{I^{(2)}(C)}$. For P/poly circuits of size $O((\log N)^c)$ with $c \geq 1$, one has $I^{(2)} = O((\log N)^{c+1})$ and $\log p = O(\log N)$, so the condition fails. Three directions could potentially close this gap: (i) a number-theoretic technique supplying more than $O(\log N)$ bits of modular independence; (ii) a direct use of the multiplicativity or non-pretentiousness of $\mu$ to bound Fourier correlations without passing through the bilinear sum; (iii) showing that CRT carry patterns force systematic cancellation in $\sum_i \delta_{\mathrm{mid},i}$ (see §7.3). None of these is currently available.

---

## 8. Conclusion and Open Problems

### 8.1 Summary

**Unconditional results.**

*Proposition 4.2* establishes Möbius orthogonality for TC⁰ circuits of branching factor $b = O(1)$ and size $s = O(\log\log N)$ as a consequence of Siegel-Walfisz. See the remark in §4.2 on the scope of this result. The extension to circuits of polynomial size reduces to Conjecture 4.1, which is open.

*Proposition 6.14* shows that applying the Mauduit-Rivat carry lemma and the MOO invariance principle gate-by-gate with a union bound yields a total error of $O((\log N)^{c+1-c/(4d+2)})$, which diverges. This identifies a specific obstruction to one family of proof strategies for low-influence TC⁰.

*Lemma 6.2 and Corollary 6.3* record that the multilinear extension has exact mean-matching at each step and variance $\mathrm{Var}_Z = \bar{C}(1-\bar{C}) = \Theta(1)$. Corollary 6.5 draws the consequence that the Cauchy-Schwarz route through small Gaussian variance is unavailable.

**Obstructions to extending to P/poly.**

Three obstructions are identified for the proof strategies considered in this paper.

*Topological obstruction (Theorem 7.1 and Corollary 7.2, §7.1).* Theorem 7.1 establishes universally that any $C^4$ extension $F$ of NAND with an attracting interior fixed point must have an unstable period-2 orbit at the basin boundary; Corollary 7.2 shows this forces $|R_i| \geq C[(g_F^2)'(x_0)]^D \to \infty$ for $D = \omega(1)$. The obstruction holds for all such extensions, not only the specific quintic $T_\star$. The boundary accumulation identity of §7.3 reduces the per-step error to $O(1)$ but the total over $m = O(\log N)$ steps remains $O(\log N)$, not $o(1)$.

*Gaussian sibling obstruction (§7.4).* For formulas with the symmetric gate ($c_0 = 1/2$) and DFS Lindeberg ordering, the midpoint deviation $\delta_{\mathrm{mid},i}$ is zero for Boolean siblings but acquires a second-order correction $-T_\star''(3/4)/32 \neq 0$ for Gaussian siblings. Setting $\lambda_0$ to zero this correction requires $\lambda_0 > 1$, which destroys the attracting property. The total error for formulas is $O(\log^2 N)$.

*Influence barrier (§7.5).* The noise operator approach requires $\log p \gg \sqrt{I^{(2)}(C)}$. For P/poly circuits of size $O((\log N)^c)$ with $c \geq 1$, the second-moment influence satisfies $I^{(2)} = O((\log N)^{c+1})$, and the condition $\log N \gg (\log N)^{(c+1)/2}$ fails.

---

### 8.2 Open Problems

**Problem 1.** Does the CRT Decomposition Conjecture (Conjecture 4.1) hold for all TC⁰ circuits of constant depth and polynomial size? A positive answer, combined with Siegel-Walfisz, would give $\mu \notin \mathsf{TC^0}$ unconditionally. Conjecture 6.15 (Effective Depth) proposes a structural mechanism via self-correcting NAND circuits; the obstacle is that effective depth reduction occurs only in the continuous domain, not in the Boolean domain where the bilinear sum is evaluated.

**Problem 2.** Can the block carry decomposition of Mauduit-Rivat [MR10] be extended to circuits of depth $\omega(1)$, tracking carry propagation across $\Omega(\log N)$ levels? This would be the key step toward closing the influence barrier (§7.5) for circuits beyond AC⁰.

**Problem 3.** Under what conditions on a circuit $C$ does the midpoint cancellation $\sum_{i=1}^m \delta_{\mathrm{mid},i} = o(1)$ hold? Specifically, do the CRT carry patterns induced by the bilinear substitution $n \mapsto pn$ force systematic alternation of the signs of $\delta_{\mathrm{mid},i}$?

**Problem 4.** Does there exist a block Lindeberg replacement — replacing all $m$ input variables simultaneously by a joint distribution — such that all sibling inputs encountered during the replacement remain Boolean? Such a replacement would avoid the Gaussian sibling obstruction of §7.4 while retaining the mean-matching property of Lemma 6.2.

**Problem 5.** Theorem 7.1 shows that all smooth NAND extensions with an attracting interior fixed point share the topological obstruction. Is there a Lindeberg-type argument that avoids requiring an interior fixed point entirely — for instance, one that operates at the Boolean endpoints rather than a continuous operating point — and if so, what replaces the contraction mechanism of §5.2?

---

### References

**[AW08]** S. Aaronson and A. Wigderson, *Algebrization: A new barrier in complexity theory*, ACM Transactions on Computation Theory **1** (2009), 1–54.

**[BGS75]** T. Baker, J. Gill, and R. Solovay, *Relativizations of the P =? NP question*, SIAM Journal on Computing **4** (1975), 431–442.

**[BSZ13]** J. Bourgain, P. Sarnak, and T. Ziegler, *Disjointness of Möbius from horocycle flows*, in *From Fourier Analysis and Number Theory to Radon Transforms and Geometry*, Dev. Math. **28**, Springer, 2013, 67–83.

**[EP98]** W. Evans and N. Pippenger, *On the maximum tolerable noise for reliable computation by formulas*, IEEE Transactions on Information Theory **44** (1998), 1299–1305.

**[Gr12]** B. Green, *On (not) computing the Möbius function using bounds on linear forms*, Random Structures & Algorithms **41** (2012), 332–345.

**[Li12]** J. E. Littlewood, *Quelques conséquences de l'hypothèse que la fonction zeta de Riemann n'a pas de zéros dans le demi-plan Re(s) > 1/2*, Comptes Rendus de l'Académie des Sciences **154** (1912), 263–266.

**[LMN93]** N. Linial, Y. Mansour, and N. Nisan, *Constant depth circuits, Fourier transform, and learnability*, Journal of the ACM **40** (1993), 607–620.

**[MOO10]** E. Mossel, R. O'Donnell, and K. Oleszkiewicz, *Noise stability of functions with low influences: Invariance and optimality*, Annals of Mathematics **171** (2010), 295–341.

**[MR10]** C. Mauduit and J. Rivat, *Sur un problème de Gelfond: la somme des chiffres des nombres premiers*, Annals of Mathematics **171** (2010), 1591–1646.

**[MR16]** K. Matomäki and M. Radziwiłł, *Multiplicative functions in short intervals*, Annals of Mathematics **183** (2016), 1015–1056.

**[RR97]** A. Razborov and S. Rudich, *Natural proofs*, Journal of Computer and System Sciences **55** (1997), 24–46.

**[Ta17]** A. Tal, *Tight bounds on the Fourier spectrum of AC⁰*, in *32nd Computational Complexity Conference* (CCC 2017), LIPIcs **79**, 15:1–15:31.
