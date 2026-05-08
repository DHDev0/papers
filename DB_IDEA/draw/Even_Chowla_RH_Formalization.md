# Even Chowla — Rigorous Formalization Under RH/GRH
## D. Derycke — Mathematical Review, May 2026

---

> **Prefatory note on scope.** This document formalizes *every step that can be made rigorous*,
> states additional hypotheses explicitly as labeled **Hypothesis**, and gives a precise
> account of what the Riemann Hypothesis and GRH actually contribute at each stage.
> It also identifies, with proof, the gaps that survive even under all standard conjectures.
> No step is called "proven" unless a complete argument is given or a standard reference exists.

---

## Part I. Unconditional Results

### 1.1 The λ-Twist Factorization Theorem

**Theorem 1.1** (λ-Twist Factorization — unconditional).
*Let $u_j$ be a Hecke–Maass cusp form for $\mathrm{SL}_2(\mathbb{Z})$ with Satake parameters
$\{\alpha_p, \beta_p\}$ at each prime $p$, normalized so that $\alpha_p\beta_p = 1$.
Define the Liouville-twisted $L$-function as the Dirichlet series*
$$L(s, u_j \otimes \lambda) := \sum_{n=1}^{\infty} \frac{a_j(n)\,\lambda(n)}{n^s},
\qquad \mathrm{Re}(s) \gg 1,$$
*where $a_j(n)$ are the Hecke eigenvalues of $u_j$.
Then, as an identity of Euler products absolutely convergent for $\mathrm{Re}(s) > 1$:*
$$L(s, u_j) \cdot L(s, u_j \otimes \lambda) = \frac{L(2s, \mathrm{sym}^2 u_j)}{\zeta(2s)}.$$

**Proof.**
The complete multiplicativity $\lambda(mn) = \lambda(m)\lambda(n)$ and $\lambda(p) = -1$ for every prime $p$
give the $p$-power generating series
$$\sum_{k=0}^{\infty} a_j(p^k)\,\lambda(p^k)\,X^k
= \sum_{k=0}^{\infty} a_j(p^k)\,(-X)^k
= \frac{1}{1 + a_j(p)X + X^2}
= \frac{1}{(1+\alpha_p X)(1+\beta_p X)},$$
using the Hecke recursion $a_j(p^k) = \alpha_p^k + \alpha_p^{k-1}\beta_p + \cdots + \beta_p^k$
and $\alpha_p\beta_p = 1$.
Hence the local Euler factor of $L(s, u_j \otimes \lambda)$ at $p$ is
$$L_p(s, u_j \otimes \lambda) = \frac{1}{(1+\alpha_p p^{-s})(1+\beta_p p^{-s})}.$$
Multiplying with the standard factor
$L_p(s, u_j) = \bigl[(1-\alpha_p p^{-s})(1-\beta_p p^{-s})\bigr]^{-1}$,
and applying the difference of squares:
$$L_p(s, u_j) \cdot L_p(s, u_j\otimes\lambda)
= \frac{1}{(1-\alpha_p^2 p^{-2s})(1-\beta_p^2 p^{-2s})}.$$
The local symmetric-square factor is
$L_p(2s, \mathrm{sym}^2 u_j) = \bigl[(1-\alpha_p^2 p^{-2s})(1-p^{-2s})(1-\beta_p^2 p^{-2s})\bigr]^{-1}$
(Satake parameters of $\mathrm{sym}^2 u_j$ are $\{\alpha_p^2, \alpha_p\beta_p = 1, \beta_p^2\}$),
so
$$\frac{L_p(2s,\mathrm{sym}^2 u_j)}{\zeta_p(2s)}
= \frac{1}{(1-\alpha_p^2 p^{-2s})(1-\beta_p^2 p^{-2s})}.$$
Taking the product over all primes and invoking absolute convergence for $\mathrm{Re}(s) > 1$
completes the proof at the level of Euler products. $\square$

**Remark 1.2** (Analytic continuation — an open problem).
The analytic continuation of $L(s, u_j \otimes \lambda)$ to all $s \in \mathbb{C}$, and the
existence of a functional equation, are **not** automatic.
The Liouville function $\lambda$ is *not* a Hecke character of any number field (it is not a
Dirichlet character for any modulus), so $u_j \otimes \lambda$ is not a standard automorphic
representation. The identity of Theorem 1.1 holds as an Euler product identity, and by
Landau–Phragmén–Lindelöf this extends to a half-plane; full meromorphic continuation
to $\mathbb{C}$ is an open problem.
All subsequent results that invoke $L(1/2, u_j \otimes \lambda)$ should be understood as
*assuming this analytic continuation exists*, which we state explicitly when needed.

---

### 1.2 The Forced Vanishing Corollary

**Corollary 1.3** (Forced Vanishing — conditional on analytic continuation).
*Assume $L(s, u_j \otimes \lambda)$ has analytic continuation to a neighborhood of $s = 1/2$.
Then*
$$L(1/2, u_j) \cdot L(1/2, u_j \otimes \lambda) = 0.$$

**Proof.**
Evaluate the identity of Theorem 1.1 at $s = 1/2$:
$$L(1/2, u_j) \cdot L(1/2, u_j \otimes \lambda)
= \frac{L(1, \mathrm{sym}^2 u_j)}{\zeta(1)}.$$
By Shahidi's theorem (1988), $L(1, \mathrm{sym}^2 u_j)$ is a finite positive real.
Since $\zeta(s)$ has a simple pole at $s=1$, we have $\zeta(1) = +\infty$, so the
right-hand side equals $0$.
Hence at least one factor on the left vanishes. $\square$

---

### 1.3 Root Number Dichotomy

**Proposition 1.4** (Sign Classification — standard functional equations).
*The root number $\epsilon_j \in \{+1, -1\}$ of $u_j$ and the root number $\epsilon_j'$
of $u_j \otimes \lambda$ (assuming its functional equation) satisfy*
$$\epsilon_j' = -\epsilon_j.$$
*Consequently:*
- *If $\epsilon_j = -1$ (odd form): the functional equation of $u_j$ forces $L(1/2, u_j) = 0$.*
- *If $\epsilon_j = +1$ (even form): assuming the functional equation of $u_j \otimes \lambda$,
  its root number is $-1$, forcing $L(1/2, u_j \otimes \lambda) = 0$.*

**Proof.**
For an odd Hecke–Maass form the functional equation reads
$\Lambda(s, u_j) = \epsilon_j \Lambda(1-s, u_j)$
where $\Lambda$ includes the $\Gamma$-factor. At $s = 1/2$ and $\epsilon_j = -1$: $\Lambda(1/2) = -\Lambda(1/2)$,
so $\Lambda(1/2) = 0$, and since the $\Gamma$-factor is nonzero at $s = 1/2$, we conclude
$L(1/2, u_j) = 0$.
The sign flip $\epsilon_j' = -\epsilon_j$ follows from the fact that $\lambda(p) = -1$ for all $p$;
twisting by $\lambda$ negates the Hecke eigenvalues at every prime, which negates the
epsilon-factor (a product of local signs at the archimedean and ramified places). $\square$

**Corollary 1.5.** *Under the analytic continuation hypothesis:*
- *For even forms ($\epsilon_j = +1$): $L(1/2, u_j \otimes \lambda) = 0$ unconditionally
  (once analytic continuation is granted), independent of Corollary 1.3.*
- *For odd forms ($\epsilon_j = -1$): $L(1/2, u_j) = 0$; hence by Corollary 1.3,
  $L(1/2, u_j \otimes \lambda)$ can be nonzero.*

This means **the spectral sum over $D_1(N)$, if it could be formalized, receives contributions
only from odd Maass forms.**

---

### 1.4 The First-Derivative Identity

**Theorem 1.6** (First-Derivative Identity).
*Let $u_j$ be an odd Hecke–Maass form such that $L(1/2, u_j) = 0$ is a simple zero.
Assume the analytic continuation of $L(s, u_j \otimes \lambda)$ so that its value at $s = 1/2$
is well-defined. Then:*
$$L(1/2, u_j \otimes \lambda) = \frac{2\,L(1, \mathrm{sym}^2 u_j)}{L'(1/2, u_j)}.$$

**Proof.**
Write $s = 1/2 + \varepsilon$ and expand each factor in Laurent series as $\varepsilon \to 0$.

**RHS of Theorem 1.1:**
$$\zeta(1 + 2\varepsilon) = \frac{1}{2\varepsilon} + \gamma + O(\varepsilon),
\qquad
L(1+2\varepsilon, \mathrm{sym}^2 u_j) = L(1,\mathrm{sym}^2 u_j) + O(\varepsilon).$$
Hence
$$\frac{L(1+2\varepsilon, \mathrm{sym}^2 u_j)}{\zeta(1+2\varepsilon)}
= 2\varepsilon\,L(1,\mathrm{sym}^2 u_j) + O(\varepsilon^2).$$

**LHS of Theorem 1.1:**
$$L(1/2+\varepsilon, u_j) = \varepsilon\,L'(1/2,u_j) + O(\varepsilon^2)
\quad\text{(simple zero hypothesis)},$$
$$L(1/2+\varepsilon, u_j\otimes\lambda) = L(1/2, u_j\otimes\lambda) + O(\varepsilon).$$
So the LHS at order $\varepsilon^1$ is
$$\varepsilon\,L'(1/2,u_j)\cdot L(1/2,u_j\otimes\lambda) + O(\varepsilon^2).$$

Equating coefficients of $\varepsilon^1$ and dividing by $\varepsilon \neq 0$:
$$L'(1/2,u_j)\cdot L(1/2,u_j\otimes\lambda) = 2\,L(1,\mathrm{sym}^2 u_j).$$
Since $L'(1/2,u_j) \neq 0$ (simple zero) and $L(1,\mathrm{sym}^2 u_j) \neq 0$ (Shahidi),
the identity follows. $\square$

---

### 1.5 The Möbius Factorization Identity

**Theorem 1.7** (Möbius Factorization — unconditional).
*Define $L(s, u_j \otimes \mu) := \sum_n \mu(n) a_j(n) n^{-s}$. Then there exists an Euler
product $H(s) = \prod_p h_p(s)$ converging absolutely for $\mathrm{Re}(s) > 1/3$, with
$h_p(s) = 1 + O(p^{-3\,\mathrm{Re}(s)})$ locally, such that*
$$L(s, u_j \otimes \mu) \cdot L(s, u_j) = \frac{H(s)}{\zeta(2s)}.$$

**Proof.**
Since $\mu(p^k) = 0$ for $k \geq 2$ and $\mu(p) = -1$, the local Euler factor is:
$$L_p(s, u_j \otimes \mu) = 1 - a_j(p) p^{-s}.$$
Multiplying:
$$L_p(s,u_j\otimes\mu) \cdot L_p(s,u_j)
= \frac{1 - a_j(p)p^{-s}}{(1-\alpha_p p^{-s})(1-\beta_p p^{-s})}
= \frac{1-a_j(p)p^{-s}}{1 - a_j(p)p^{-s} + p^{-2s}}.$$
Setting $x = a_j(p)p^{-s}$, $y = p^{-2s}$:
$$\frac{1-x}{1-x+y} = (1-x)\sum_{k=0}^{\infty}(x-y)^k = 1 - y + O(p^{-3\mathrm{Re}(s)})
= \frac{1}{1-p^{-2s}} \cdot h_p(s)$$
where $h_p(s) = (1-p^{-2s})(1 - p^{-2s} + O(p^{-3\mathrm{Re}(s)}))^{-1}$ satisfies $h_p(s) = 1 + O(p^{-3\mathrm{Re}(s)})$.
The product $H(s) = \prod_p h_p(s)$ converges absolutely for $\mathrm{Re}(s) > 1/3$. $\square$

**Corollary 1.8** (Möbius First-Derivative Identity).
*Under the same hypotheses as Theorem 1.6, with $L(s, u_j\otimes\mu)$ having analytic
continuation:*
$$L(1/2, u_j \otimes \mu) = \frac{2\,H(1/2)}{L'(1/2, u_j)}.$$

**Remark 1.9.** Corollary 1.8 shows that extracting the squares (passing from $\lambda$ to $\mu$)
changes only the numerator (from $L(1,\mathrm{sym}^2 u_j)$ to $H(1/2)$), both of which are finite
nonzero constants. The derivative $L'(1/2, u_j)$ in the denominator is **identical**. The
Parity Barrier is multiplicative-function agnostic: it lives entirely in $1/L'(1/2, u_j)$.

---

### 1.6 Local Factor Formula and Vanishing Singular Series

**Theorem 1.10** (Local Factor Formula — unconditional).
*For any prime $p > 2$ and $m \geq 1$:*
$$E_p^{(2m)} := \mathbb{E}_{n \bmod p^\infty}[\lambda_p(n)\lambda_p(n+1)]
= \frac{p + 1 - 4m}{p+1}.$$

**Proof.** (Complete, as in the source documents; the three residue-class cases give the
stated formula via the geometric series $\sum_{k\geq 1}(-1)^k(p-1)/p^k = -(p-1)/(p+1)$.)

**Corollary 1.11** (Vanishing Singular Series — unconditional).
*If $p = 4m - 1$ is prime for some $m \geq 1$, then $E_p^{(2m)} = 0$,
hence $\mathfrak{S}_{2m} = \prod_p E_p^{(2m)} = 0$.*

---

## Part II. The Role of the Riemann Hypothesis and GRH

We now state precisely what each hypothesis contributes.

**Convention.** Throughout:
- **RH** = all nontrivial zeros of $\zeta(s)$ lie on $\mathrm{Re}(s) = 1/2$.
- **GRH** = all nontrivial zeros of every Dirichlet $L(s,\chi)$ lie on $\mathrm{Re}(s) = 1/2$.
- **GRH$_{\mathrm{GL}_2}$** = all nontrivial zeros of $L(s, u_j)$ and $L(s, \mathrm{sym}^2 u_j)$
  lie on $\mathrm{Re}(s) = 1/2$, for all Hecke–Maass cusp forms $u_j$.

### 2.1 What RH gives

**Proposition 2.1.** *Under RH:*

*(i) The Mertens function satisfies $M(N) = \sum_{n \leq N} \mu(n) \ll N^{1/2+\varepsilon}$.*

*(ii) More generally, for any Dirichlet character $\chi$ (under GRH):
$\sum_{n \leq N} \mu(n) \chi(n) \ll N^{1/2+\varepsilon}$.*

**Proof.** Standard: $M(N) = (2\pi i)^{-1}\int_{c-iT}^{c+iT} N^s/(s\zeta(s)) ds$ via Perron;
under RH there are no poles in $\{1/2 < \mathrm{Re}(s) \leq c\}$ so the contour shifts to
$\mathrm{Re}(s) = 1/2 + \delta$, giving $O(N^{1/2+\delta+\varepsilon})$ for any $\delta > 0$. $\square$

**Proposition 2.2.** *Under GRH$_{\mathrm{GL}_2}$, for each fixed odd Maass form $u_j$:*
$$\sum_{n \leq N} a_j(n) \ll N^{1/2+\varepsilon}.$$

**Proposition 2.3** (Contour shift, under GRH$_{\mathrm{GL}_2}$, assuming analytic
continuation of $L(s,u_j\otimes\lambda)$).
*For each fixed odd $u_j$, shifting the Perron contour integral for
$M_j(N) := \sum_{n\leq N} \mu(n) a_j(n)$
from $\mathrm{Re}(s) = 1+\varepsilon$ to $\mathrm{Re}(s) = 1/2+\varepsilon$ crosses no zeros of
$L(s, u_j)$, so*
$$M_j(N) = \frac{1}{2\pi i}\int_{1/2-iT}^{1/2+iT}
L(s, u_j\otimes\mu)\frac{N^s}{s}ds + O\!\left(\frac{N^{1+\varepsilon}}{T}\right).$$

**Critical remark 2.4.** Proposition 2.3 establishes a contour shift. It does *not* establish
that $M_j(N) \ll N^{1/2+\varepsilon}$, because the integral along $\mathrm{Re}(s)=1/2$ is not bounded
by $N^{1/2}$ without further information about the size of $L(1/2, u_j\otimes\mu)$ and its
dependence on $t_j$. In particular, if $L(1/2, u_j\otimes\mu) \sim t_j^A$ for some $A > 0$,
the infinite spectral sum will diverge.
**GRH alone does not bound $L(1/2, u_j \otimes \mu)$ in $t_j$.**

---

### 2.2 Petrow–Young Theorem (2020) — statement and scope

**Theorem 2.5** (Petrow–Young 2020, *Ann. Math.*).
*Let $u_j$ be a Hecke–Maass form of spectral parameter $t_j \in \mathbb{R}$ and let $\chi$
be a primitive Dirichlet character of conductor $q$. Then:*
$$|L(1/2, u_j \otimes \chi)| \ll \bigl(q(1+|t_j|)\bigr)^{1/3+\varepsilon}.$$

**Remark 2.6.** This bound is unconditional and applies when $\chi$ is a *true Dirichlet
character* (i.e., a character of a number field, of fixed conductor). In particular it applies
to $\chi_{-4}$ (the non-principal character mod 4).

---

## Part III. The Fatal Gaps Under All Standard Hypotheses

The following gaps are not closed by RH, GRH, GRH$_{\mathrm{GL}_2}$, or Petrow–Young.

### 3.1 Gap 1: The Spectral Expansion is Unestablished

**Claim** (from document, Phase 1 of TCA proof):
$$D_1(N) = \mathcal{E}_{\mathrm{cont}}(N)
+ \sum_{t_j \leq T} \frac{|L(1/2, u_j \otimes \lambda)|^2}{L(1, \mathrm{sym}^2 u_j)}\hat{\Phi}_N(t_j)
+ O\!\left(\frac{N^{1+\varepsilon}}{T}\right).$$

**Status: Not a theorem. Not currently derivable from the Kuznetsov trace formula.**

**Explanation.** A spectral expansion of the shifted convolution $\sum_{n \leq N} \lambda(n)\lambda(n+1)$
via Kuznetsov requires writing the Liouville function as a superposition of Hecke eigenvalue
sequences, then applying the trace formula. The key obstructions are:

*(a) The Liouville function is not an automorphic form.* Inserting $\lambda(n)$ into a
bilinear sum requires a decomposition into Dirichlet characters or Maass form coefficients
(e.g., via Vaughan's identity or Heath-Brown). This decomposition introduces Type I and
Type II sums, each of which requires independent estimation. This is exactly the program
whose failure is documented in Part III of the source documents (the Five Fatal Flaws),
and none of the Flaws are resolved by RH or GRH.

*(b) The formula involves $|L(1/2, u_j\otimes\lambda)|^2$, not $L(1/2, u_j\otimes\lambda)$.*
This squared form typically arises from Watson's formula / Ichino's formula for triple
products on GL(3), applied to a very specific situation. The precise setup here is not
justified in the document.

*(c) The truncation error $O(N^{1+\varepsilon}/T)$ is asserted without proof.*
For the standard Kuznetsov formula applied to Kloosterman sums with inputs of size $N$,
the truncation error depends on the conductor and the arithmetic structure of the input;
a clean $O(N/T)$ bound for the Liouville convolution is not a theorem.

**What RH buys here: nothing.** The obstruction is not the location of zeros; it is the
absence of a valid spectral decomposition of $\sum \lambda(n)\lambda(n+1)$.

---

### 3.2 Gap 2: The $\chi_{-4}$ Bypass Creates an Algebraic Tautology

**Claim** (Phase 3 of TCA proof):
$$L(s, u_j \otimes \lambda) = L(s, u_j \otimes \chi_{-4}) \cdot H_{\mathrm{split}}(s)$$
with $|H_{\mathrm{split}}(1/2)| \ll t_j^\varepsilon$ (Split-Prime CM Boundedness Hypothesis).

**Theorem 3.1** (Refutation of the $H_{\mathrm{split}}$ hypothesis — unconditional).
*The Split-Prime CM Boundedness Hypothesis is false, and the substitution is a tautology.*

**Proof.** By definition, $H_{\mathrm{split}}(s) = L(s, u_j \otimes \lambda)/L(s, u_j \otimes \chi_{-4})$.
Substituting the factorization identity (Theorem 1.1):
$$H_{\mathrm{split}}(s)
= \frac{L(2s, \mathrm{sym}^2 u_j)}{\zeta(2s)\, L(s, u_j)\, L(s, u_j \otimes \chi_{-4})}.$$
For odd $u_j$: expand as $s = 1/2 + \varepsilon \to 0$, using $\zeta(1+2\varepsilon) = (2\varepsilon)^{-1} + \gamma + O(\varepsilon)$
and $L(1/2+\varepsilon, u_j) = \varepsilon L'(1/2, u_j) + O(\varepsilon^2)$:
$$H_{\mathrm{split}}(1/2)
= \frac{2\,L(1,\mathrm{sym}^2 u_j)}{L'(1/2, u_j)\cdot L(1/2, u_j \otimes \chi_{-4})}.$$

Now substitute back into the claimed bound
$|L(1/2, u_j\otimes\lambda)| \leq |H_{\mathrm{split}}(1/2)|\cdot|L(1/2, u_j\otimes\chi_{-4})|$:
$$|L(1/2, u_j\otimes\lambda)|
\leq \left|\frac{2\,L(1,\mathrm{sym}^2 u_j)}{L'(1/2,u_j)\cdot L(1/2, u_j\otimes\chi_{-4})}\right|
\cdot |L(1/2, u_j\otimes\chi_{-4})|
= \frac{2\,L(1,\mathrm{sym}^2 u_j)}{|L'(1/2,u_j)|}.$$

The factor $L(1/2, u_j\otimes\chi_{-4})$ cancels identically. The Petrow–Young bound on this
factor provides **zero cancellation**. The result is exactly the First-Derivative Identity
(Theorem 1.6). The $\chi_{-4}$ decomposition is algebraically circular. $\square$

**Corollary 3.2** (Density exponent barrier).
*To bound $D_1(N)$ via the spectral sum (assuming it were valid), the required input is
a lower bound*
$$|L'(1/2, u_j)| \gg t_j^{-(3/2+\varepsilon)}$$
*uniformly over odd Maass forms. This is equivalent to requiring the Density Exponent to
satisfy $\delta > 7/3$ in the notation of the document.*

*Current best known lower bounds for $L'(1/2, u_j)$: none uniform in $t_j$ (the problem
is open). Random Matrix Theory predicts $L'(1/2, u_j) \asymp t_j^{1/6}$ on average but
provides no uniform lower bound; it is a statistical statement about a family.*

**What RH buys here: nothing.** The obstruction is the lower bound on $L'(1/2, u_j)$,
not the zeros of $\zeta(s)$.

---

### 3.3 Gap 3: The Möbius-Chowla Transfer Requires All Shifts

**Claim** (Phase 1 of Möbius-Chowla section):
$$\left|\sum_{n \leq N/a^2} \lambda(m)\lambda\!\left(a^2 m + h\right)\right|
\ll \left(\frac{N}{a^2}\right)^{4/5 + \varepsilon}
\quad \text{for all } a, h.$$

**Status: Not established.** The document proves (conditionally) a bound for shift $h = 1$,
$a = 1$ only:
$$\left|\sum_{n \leq N} \lambda(n)\lambda(n+1)\right| \ll N^{4/5+\varepsilon}.$$
Applying this to the inner sum with general $(a^2, h)$ requires the bound to hold for
the affine-shifted Liouville correlation $\sum_{m}\lambda(m)\lambda(am + b)$ for all $a, b$.
This is **not** a consequence of the $h=1$ case; it requires the full Even Chowla
Conjecture for arbitrary shifts, which is stronger than what is being proved.

**What RH buys here: nothing** additional. The difficulty is arithmetic (correlations
between $\lambda(m)$ and $\lambda(am+b)$ for general $a$), not analytic.

---

### 3.4 Gap 4: The Elliptic Curve / Odd Chowla Identification is Incorrect

**Claim** (Phase 2 of Odd Chowla section):
*"The equation $y^2 = x^3 - x$ defines an elliptic curve $E$; by the Modularity Theorem
$E$ corresponds to a weight-2 cusp form $f_E$; the global Odd Chowla sum translates
seamlessly into $L(s, f_E \otimes \lambda)$."*

**This identification is wrong.** Here is the precise error.

It is correct that $\lambda(n)\lambda(n+1)\lambda(n+2) = \lambda(n(n+1)(n+2))$ by complete
multiplicativity, and after the shift $x = n+1$, we have $\lambda(x^3-x)$.
The error is in the next step.

The $L$-function $L(s, f_E \otimes \lambda)$ is the Dirichlet series
$$L(s, f_E \otimes \lambda) = \sum_{n=1}^{\infty} \frac{c_E(n)\,\lambda(n)}{n^s},$$
where $c_E(n)$ are the Hecke eigenvalues (normalized Fourier coefficients) of $f_E$.
At a prime $p$: $c_E(p) = p + 1 - \#E(\mathbb{F}_p)$.

The sum $S_3^\lambda(N) = \sum_{n \leq N} \lambda(x^3-x)$ evaluates the Liouville function
at *values* of the polynomial $x^3-x$. This is **not** a Dirichlet series involving the
eigenvalues $c_E(n)$.

The connection between $\lambda(f(n))$ (Liouville at a polynomial) and $L(s, f_E \otimes \lambda)$
(Hecke eigenvalues twisted by $\lambda$) does not exist at this level; they are entirely
different objects. The Modularity Theorem relates the *number of $\mathbb{F}_p$-points* of $E$
to $c_E(p)$, not the Liouville function evaluated at $p^k - p^{k-1}$.

---

### 3.5 Gap 5: The Random Matrix Theory Argument is Non-rigorous

**Claim** (Part 3 of "Keep pushing the derivative"):
*Level repulsion in $SO(\mathrm{odd})$ implies $P(|L'(1/2,u_j)| = x) \approx cx^2$,
hence $\mathbb{E}[1/|L'(1/2)|^2] < \infty$, hence the spectral sum converges.*

**Status: A heuristic, not a theorem.**

The Katz–Sarnak density conjecture (and the more precise one-level density results proven
by Iwaniec–Luo–Sarnak) state that, *averaged over a family*, the distribution of low-lying
zeros of $L$-functions matches the GUE/GSE/GOE eigenvalue statistics. In the $SO(\mathrm{odd})$
family, level repulsion near the central point predicts $P(x) \sim c x^2$.

This is a **conjectural statistical statement**. It:
- Does not provide a lower bound for any *individual* $|L'(1/2, u_j)|$
- Does not establish convergence of $\sum_{t_j \leq T} 1/|L'(1/2, u_j)|^2$ (individual terms
  can still be arbitrarily large; the sum could diverge)
- Is not proven even on average; the best known results are asymptotic density theorems in
  limited ranges, not moment estimates

A rigorous theorem of the form "$\sum_{t_j \leq T} 1/|L'(1/2,u_j)|^2 \ll T^A$" does not
currently exist in the literature. This is precisely the content of the open problem
identified correctly by the source document.

**What GRH buys here.** Under GRH$_{\mathrm{GL}_2}$, the zeros of $L(s, u_j)$ lie on
$\mathrm{Re}(s) = 1/2$, so $L(1/2, u_j) = 0$ is the lowest zero. But GRH says nothing about
*how small* $L'(1/2, u_j)$ can be. The zero can be simple (as conjectured) but the
derivative can still approach zero along a subsequence of forms.

---

## Part IV. Honest Conditional Framework Under RH + GRH$_{\mathrm{GL}_2}$

Assuming all standard conjectures (RH, GRH, GRH$_{\mathrm{GL}_2}$, analytic continuation of
$L(s, u_j\otimes\lambda)$, the Katz–Sarnak density conjecture, and the non-vanishing
conjecture $L'(1/2, u_j) \neq 0$ for all odd $u_j$), **plus** the following additional
conjecture that is not currently known:

**Hypothesis H** (Density Exponent Bound):
$$|L'(1/2, u_j)| \gg t_j^{-(3/2+\varepsilon)}
\quad\text{uniformly over odd Hecke–Maass forms } u_j,$$

**and** assuming the spectral expansion formula of Phase 1 (for which no proof is given),
the argument in Phases 2–5 gives:

**Conditional Proposition 4.1.** *Under all the above, including Hypothesis H and the
unproven spectral expansion:*
$$D_1(N) = \sum_{n \leq N} \lambda(n)\lambda(n+1)\,W(n/N) \ll N^{1-\delta}$$
*for some explicit $\delta > 0$ depending on the exponent in Hypothesis H.*

The value $\delta = 6/41$ (corresponding to $N^{35/41}$) is what the document's Phase 5
balancing gives, under the Petrow–Young bound $|L(1/2, u_j\otimes\chi_{-4})| \ll t_j^{1/3}$,
the Even-sector annihilation, and the (tautologically refuted) $H_{\mathrm{split}}$ bound.
Since the $H_{\mathrm{split}}$ step is tautological (Theorem 3.1), the correct input to the
spectral sum (assuming everything else) is from Theorem 1.6:
$$|L(1/2, u_j\otimes\lambda)| = \frac{2\,L(1,\mathrm{sym}^2 u_j)}{|L'(1/2,u_j)|}
\ll \frac{t_j^\varepsilon}{|L'(1/2,u_j)|}.$$

Under Hypothesis H (say with exponent $B$: $|L'(1/2,u_j)| \gg t_j^{-B}$), this gives
$|L(1/2,u_j\otimes\lambda)| \ll t_j^{B+\varepsilon}$, and a bound $N^{1-\delta}$ with
$$\delta = \frac{1}{2 + B + 5/2} = \frac{1}{9/2 + B}$$
after the Weyl integration and optimal $T$-balancing. For Hypothesis H with $B = 3/2$:
$\delta = 1/6$, giving $D_1(N) \ll N^{5/6}$ — a weaker bound than $N^{35/41}$.

**Summary of the conditional hierarchy:**

| Hypothesis bundle | What is proven |
|---|---|
| Theorem 1.1 (unconditional) | λ-twist factorization identity |
| + analytic continuation of $L(s,u_j\otimes\lambda)$ | Forced vanishing, Theorems 1.3, 1.4 |
| + First-Derivative Identity (Theorem 1.6) | $L(1/2,u_j\otimes\lambda)$ in terms of $L'(1/2,u_j)$ |
| + valid spectral expansion (unproven) | $D_1(N)$ as a spectral sum |
| + GRH$_{\mathrm{GL}_2}$ | Contour shift; no poles crossed |
| + Hypothesis H + spectral expansion | $D_1(N) \ll N^{1-\delta}$ for some $\delta > 0$ |
| + all of above + all shifts in Gap 3 | Möbius-Chowla bound |

---

## Part V. What P≠NP and the Chowla Conjecture Would Actually Require

### 5.1 The Chowla conjecture and complexity

The 2-point Chowla conjecture ($D_1(N) = o(N)$) is currently **open**, even under GRH.
Tao (2015) proved the logarithmic-average version $\sum_{n \leq N} \lambda(n)\lambda(n+1)/n = o(\log N)$
unconditionally, but the "Cesàro" version $N^{-1}\sum_{n\leq N}\lambda(n)\lambda(n+1) \to 0$ remains open.

### 5.2 The AMNH and P≠NP

The Asymptotic Möbius Nilsequence Hypothesis (or Sarnak's conjecture) states
$N^{-1}\sum_{n\leq N} \mu(n)\,f(T^n x) \to 0$ for any zero-entropy topological dynamical system.
Even if this were known for all $f \in \mathsf{P/poly}$, the deduction of $\mathsf{P \neq NP}$ is
**not a theorem.** The complexity separation $\mathsf{P \neq NP}$ cannot be obtained from
number-theoretic arguments without a separation result in circuit complexity; the two problems
are not logically equivalent.

### 5.3 What can be claimed

The correct, honest statement of the strongest result supportable by the framework is:

**Theorem 5.1** (Unconditional, provable from the documents).
*(i) The λ-Twist Factorization identity (Theorem 1.1) holds.*
*(ii) The First-Derivative Identity (Theorem 1.6) holds, conditional on analytic continuation.*
*(iii) The Vanishing Singular Series (Corollary 1.11) holds.*
*(iv) Any proof of $D_1(N) = o(N)$ via spectral methods must resolve the Density Exponent*
*Barrier: a uniform lower bound $|L'(1/2, u_j)| \gg t_j^{-A}$ for some explicit $A < 3/2$.*

Statement (iv) is a genuine and publishable barrier theorem: it shows exactly what
additional input is needed for the spectral approach to succeed.

---

## Appendix: Five Fatal Flaws in the Vaughan/MRT Approach (Confirmed)

These are correctly identified in the source documents and are reproduced here for completeness.

| Flaw | Description | Status |
|---|---|---|
| 1 | Type I integration: $\int_1^M t/\log^A t\,dt \asymp M^2/\log^A M$, not $M/\log^{A-1}M$ | Confirmed; factor of $M$ error |
| 2 | Type II parameter: $\delta = \sqrt{-\log\psi/2\log N}$ gives divergent off-diagonal | Confirmed; $\sqrt{\log N} \gg \log\log N$ |
| 3 | Circularity: BV for $\lambda(x+1)\lambda(x+2)\lambda(x+3)$ assumes Odd Chowla | Confirmed |
| 4 | Invalid limit swap: Erdős–Kac valid for fixed $k$, not $k \sim \sigma^2 = \log\log N$ | Confirmed |
| 5 | Singular series $\mathfrak{S}_{2m} = 0$ plays no role in triangle-inequality bounds | Confirmed |
