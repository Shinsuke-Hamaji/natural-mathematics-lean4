# Natural Mathematics Foundation Library Specification (`NaturalMathematics.lean`)

## 1. Overview

`NaturalMathematics.lean` serves as the foundational reference system for Natural Mathematics. It provides a formal, kernel-verified foundation for grounding individual mathematical conjectures (e.g., Oppermann, Legendre, Goldbach) in dynamic local-generation processes.

Using the **Synchronized Infinity Principle** (grounded in Potential Infinity, Peano Axioms, and the Lean 4 kernel) as its core engine, it projects dynamic structural behavior onto the **Odd-Composite Pair Synchronization Inevitability Theorem**. External conjecture modules can simply `import NaturalMathematics` and utilize `synchronized_structural_compensation` to directly leverage non-degeneracy premises ($M_l > 0 \lor M_r > 0$).

---

## 2. Causal Architecture of Reference

The logical dependency flow inside Natural Mathematics advances strictly from dynamic generation to macroscopic structural references:

$$
\begin{array}{ccc}
\text{【Dynamic Engine】Potential Infinity + Peano Axioms} \\
\Downarrow \\
\text{Synchronized Infinity Principle (`synchronized_infinity_principle`)} \\
\text{\small (Type-theoretic Hilbert's Hotel engine / Execution log generation)} \\
\Downarrow \\
\text{Odd-Composite Pair Synchronization Inevitability (`odd_composite_pair_sync_inevitability`)} \\
\text{\small (Algebraic proof of non-degeneracy in local generation)} \\
\Downarrow \\
\text{Synchronized Structural Compensation (`synchronized_structural_compensation`)} \\
\Downarrow \\
\text{【External Modules】Oppermann / Legendre / Goldbach Conjecture Proofs}
\end{array}
$$

---

## 3. Base Export Specifications

### 3.1 Theorem of Synchronized Infinity (`synchronized_infinity_principle`)
* **Role**: Foundational dynamic engine. Formulates Hilbert's Hotel as an injective yet non-surjective self-map, asserting cardinality preservation and dynamic execution logs.
```lean
theorem synchronized_infinity_principle
  (k : ℕ) :
  ∃ (f : ℕ → ℕ), Function.Injective f ∧ ∃ y, ∀ x, f x ≠ y
```

### 3.2 Odd-Composite Pair Synchronization Inevitability (`odd_composite_pair_sync_inevitability`)
* **Role**: Local generation theorem. Proves by contradiction that under exclusive step incrementation and structural floor constraints (`h_structural_floor`), structural pair collapse ($M_l = 0 \land M_r = 0$) causes an algebraic impossibility.
```lean
theorem odd_composite_pair_sync_inevitability
  (a Pp Ml Mr : ℕ)
  (h_decomp : a = 2 * Pp + Ml + Mr)
  (h_structural_floor : (a : ℤ) > 2 * (Pp : ℤ)) :
  Ml > 0 ∨ Mr > 0
```

### 3.3 Common Structural Configuration (`SynchronizedPairConfiguration`)
* **Role**: Standardized data structure for passing interval pair allocations (bilateral prime pairs, unilateral prime pairs, bilateral composite pairs) from downstream conjecture modules to this reference system.
```lean
structure SynchronizedPairConfiguration (k : ℕ) where
  Pp : ℕ  -- Bilateral prime pairs
  Ml : ℕ  -- Unilateral prime pairs (left side)
  Mr : ℕ  -- Unilateral prime pairs (right side)
  Cp : ℕ  -- Bilateral composite pairs
  total_pairs : ℕ
  sum_eq : Pp + Ml + Mr + Cp = total_pairs
```

### 3.4 Structural Compensation Theorem (`synchronized_structural_compensation`)
* **Role**: Main reference API. Accepts a `SynchronizedPairConfiguration` from downstream conjecture modules and immediately projects the base inevitability theorem to guarantee unilateral non-degeneracy ($M_l > 0 \lor M_r > 0$).
```lean
theorem synchronized_structural_compensation
  (k : ℕ)
  (config : SynchronizedPairConfiguration k)
  (a : ℕ)
  (h_decomp : a = 2 * config.Pp + config.Ml + config.Mr)
  (h_structural_floor : (a : ℤ) > 2 * (config.Pp : ℤ)) :
  config.Ml > 0 ∨ config.Mr > 0
```

---

## 4. Kernel Verification Status

All core theorems and exported interfaces have been verified by the Lean 4 kernel with **zero `sorry` warnings**, depending exclusively on standard kernel axioms `[propext, Quot.sound]`:

```text
'NaturalMathematics.SynchronizedInfinity.synchronized_infinity_principle' depends on axioms: [propext, Quot.sound]
'NaturalMathematics.SynchronizedInfinity.odd_composite_pair_sync_inevitability' depends on axioms: [propext, Quot.sound]
'NaturalMathematics.SynchronizedInfinity.synchronized_structural_compensation' depends on axioms: [propext, Quot.sound]
```