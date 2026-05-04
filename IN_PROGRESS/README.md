# The Even Chowla Manuscript Suite

This suite constitutes a comprehensive, nine-paper architecture connecting the Even Chowla Conjecture in analytic number theory to the $\mathsf{P \neq NP}$ problem in computational complexity theory. The framework spans arithmetic dynamics, spectral trace formulas, arithmetic sub-convexity, pseudo-randomness, and topological entropy, providing a rigorous and structured approach to one of the most significant open problems in mathematics.

## Paper 0: Arithmetic Dynamics of the Superattractor
**Abstract:** Lays the foundation for the suite by translating the $\mathsf{P \neq NP}$ problem into an arithmetic-dynamical statement. It introduces the AMNH (Additive-Multiplicative No-Hit) framework and demonstrates how a deterministic $\mathsf{P/poly}$ circuit collapse implies a zero-entropy topological obstruction that violates the pseudorandomness of the Möbius function.
**Key Contribution:** Constructs the Layer 2 Bürgisser transfer, providing the essential bridge between Boolean circuit complexity and the algebraic framework over finite fields, and formally isolates the topological entropy boundary of feasible computation.

## Paper 1: Spectral Bounds for Even Chowla via the Motohashi-Kuznetsov Framework
**Abstract:** Establishes spectral decomposition bounds for the Even Chowla conjecture using the DFI (Duke-Friedlander-Iwaniec) subconvexity theorem.
**Key Contribution:** Provides unconditional bounds for the $k=2$ case (conditional on Gap E) and explicitly defines the spectral induction path for $k \geq 4$, carefully isolating the non-multiplicative spectral bounds (Gap A) and Tauberian limitations (Gap B) that obstruct higher-order generalizations.

## Paper 2: Polynomial Chowla: The Bootstrap Architecture and the Hecke Route
**Abstract:** Investigates the reduction of polynomial Chowla to linear even Chowla. It highlights the bootstrap mechanism and the Hecke period route for estimating the correlation of Liouville functions evaluated at polynomial values.
**Key Contribution:** Clarifies the exact reliance on polynomial Möbius orthogonality (Gap 4) and demonstrates that current symmetric CM period series are insufficient to force the unconditional vanishing of algebraic dependencies without major advances in transcendence theory.

## Paper 3: Even Chowla Structural Map: From Dynatomic Fields to the Spectral Induction
**Abstract:** Acts as the central architectural map of the suite, linking dynatomic Galois theory to the spectral induction framework.
**Key Contribution:** Formally retracts the MRTTK-gvN Gowers $U^3$ approach, proving that fixed-shift correlations exhibit infinite Cauchy-Schwarz complexity. It provides an exhaustive taxonomy of the remaining gaps (A–E) in the spectral induction.

## Paper 4: NAND Extensions and Circuit Complexity (EML NAND Duality)
**Abstract:** Explores the logical and algebraic boundaries of $\mathsf{NC^1}$ and $\mathsf{P/poly}$ circuits using the EML-NAND duality.
**Key Contribution:** Articulates the "Deterministic Carry-Influence Union Bound Barrier", proving that Boolean extraction methods cannot unconditionally separate $\mathsf{P}$ from $\mathsf{NP}$ without violating the structural independence of arithmetic carrying layers.

## Paper 5: From Chowla to P ≠ NP: The Sarnak Bypass
**Abstract:** The capstone synthesis paper. It traces the direct logical implication chain from the Even Chowla conjecture to the resolution of $\mathsf{P \neq NP}$.
**Key Contribution:** Introduces the "Sarnak Bypass," demonstrating that a conditional assumption of $\mathsf{P=NP}$ leads directly to the collapse of cryptographic PRGs and the explicit construction of a polynomial-size circuit for the Möbius function. This forces a $6/\pi^2$ density contradiction with the logarithmically averaged Sarnak conjecture, directly implying $\mathsf{P \neq NP}$.

## Paper 6: Dynamical Trace Formulas and Arboreal Galois Representations
**Abstract:** Explores the arithmetic-dynamical bridge linking arboreal Galois representations to the periodic orbits of polynomial dynamical systems.
**Key Contribution:** Replaces the Lagarias-Odlyzko algebraic approach with Ruelle transfer operators, demonstrating how dynamical trace formulas reduce Chebotarev errors. It outlines the specific need for a Dynamical Montgomery Pair Correlation (GUE repulsion) to achieve power-saving bounds.

## Paper 7: The Scale Transfer Problem: Why Log Works, Cesàro Fails
**Abstract:** Diagnoses the fundamental gap between logarithmically averaged Chowla bounds (proven unconditionally by Tao) and the Cesàro (natural density) averages required for the AMNH.
**Key Contribution:** Formally identifies the "Parity Barrier" and the Dirichlet polynomial cancellation obstructions that prevent the inductive transfer from $U^2$ to $U^3$ norms, proving that scaling bounds beyond $k \geq 4$ inherently trigger these parity blockades.

## Paper 8: Nonstandard Analysis, BDH, and the Topological Obstruction
**Abstract:** Formalizes the bounds and scale transfers using nonstandard analysis, working with hyperfinite integers and Loeb measure.
**Key Contribution:** Refines the magnitude of required uniformities from surreal levels to standard sub-exponential scales, providing a nonstandard mapping that strictly defines the topological obstructions parallel to the Deterministic Carry-Influence barrier.
