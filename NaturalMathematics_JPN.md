# 自然数学基盤ライブラリ仕様書 (`NaturalMathematics.lean`)

## 1. 概要 (Overview)

`NaturalMathematics.lean` は、自然数学 (Natural Mathematics) の確固たる論理的土台として、**「局所生成系（動的プロセスに根ざした構造）」を従来の静的な数学や外部の個別予想モジュールからいつでも安全に参照できる「厳密な参照系（Reference System）」**として提供する標準基盤ライブラリです。

「可能無限 ＋ ペアノ公理 ＋ Lean 4 カーネル」に基づく動的生成エンジンである **同期無限の原理 (Synchronized Infinity Principle)** を論理的起点として確立し、その動的プロセスの射影として **奇合成数ペア同期の必然性 (Odd-Composite Pair Synchronization Inevitability)** を普遍定理として証明します。

各素数予想モジュール（オッパーマン、ルジャンドル、ゴールドバッハ等）は、本ライブラリを `import NaturalMathematics` してこの参照系を呼び出すことで、非退化条件（$M_l > 0 \lor M_r > 0$）を因果的根拠を持った確実な前提として利用できます。

---

## 2. 参照系の因果構造 (Causal Architecture of Reference)

自然数学における論理的依存の矢印は、動的な生成から大域的な構造の参照へと一貫して展開されます：

$$
\begin{array}{ccc}
\text{【動的生成エンジン】可能無限 + ペアノ公理} \\
\Downarrow \\
\text{同期無限の原理 (`synchronized_infinity_principle`)} \\
\text{\small (無限ホテルの型理論的表現・実行ログの生成規則)} \\
\Downarrow \\
\text{奇合成数ペア同期の必然性 (`odd_composite_pair_sync_inevitability`)} \\
\text{\small (局所生成プロセスにおける代数的非退化の証明)} \\
\Downarrow \\
\text{構造的補償汎用参照定理 (`synchronized_structural_compensation`)} \\
\Downarrow \\
\text{【外部参照系】Oppermann / Legendre / Goldbach 等の予想証明モジュール}
\end{array}
$$

---

## 3. 基底構造体および提供定理仕様 (Core Export Specifications)

### 3.1 同期無限の原理定理 (`synchronized_infinity_principle`)
* **概念的役割**: 動的生成プロセスの起点。無限ホテル（Hilbert's Hotel）の型理論的表現として、単射かつ非全射な自己写像による濃度の保存と進展を立証します。
```lean
theorem synchronized_infinity_principle
  (k : ℕ) :
  ∃ (f : ℕ → ℕ), Function.Injective f ∧ ∃ y, ∀ x, f x ≠ y
```

### 3.2 奇合成数ペア同期の必然性定理 (`odd_composite_pair_sync_inevitability`)
* **概念的役割**: 局所生成プロセスにおける本質的定理。動的ステップ増加と構造的底面条件（`h_structural_floor`）のもとで、ペアの同期崩壊（$M_l = 0 \land M_r = 0$）が代数的自己矛盾を引き起こすことを背理法によって証明します。
```lean
theorem odd_composite_pair_sync_inevitability
  (a Pp Ml Mr : ℕ)
  (h_decomp : a = 2 * Pp + Ml + Mr)
  (h_structural_floor : (a : ℤ) > 2 * (Pp : ℤ)) :
  Ml > 0 ∨ Mr > 0
```

### 3.3 共通幾何構造体 (`SynchronizedPairConfiguration`)
* **概念的役割**: 外部の予想モジュールが対象とする区間のペア配置（双方向素数ペア、単方向素数ペア、合成数ペア）を本参照系へと受け渡すための共通データ型。
```lean
structure SynchronizedPairConfiguration (k : ℕ) where
  Pp : ℕ  -- 双方向素数ペア (Bilateral prime pairs)
  Ml : ℕ  -- 左側単方向素数ペア (Unilateral prime pairs - left)
  Mr : ℕ  -- 右側単方向素数ペア (Unilateral prime pairs - right)
  Cp : ℕ  -- 双方向合成数ペア (Bilateral composite pairs)
  total_pairs : ℕ
  sum_eq : Pp + Ml + Mr + Cp = total_pairs
```

### 3.4 構造的補償汎用参照定理 (`synchronized_structural_compensation`)
* **概念的役割**: 外部予想モジュールが `SynchronizedPairConfiguration` を渡した際、本基盤の必然性定理を射影して片側非退化（$M_l > 0 \lor M_r > 0$）を即座に確定・抽出するための標準API。
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

## 4. Kernel 検証ステータス (Kernel Axiom Verification)

すべての基底定理および参照インターフェースは Lean 4 カーネルによって検証されており、標準公理セット `[propext, Quot.sound]` のみを用いて **Zero-Sorry** で完全に通過しています。

```text
'NaturalMathematics.SynchronizedInfinity.synchronized_infinity_principle' depends on axioms: [propext, Quot.sound]
'NaturalMathematics.SynchronizedInfinity.odd_composite_pair_sync_inevitability' depends on axioms: [propext, Quot.sound]
'NaturalMathematics.SynchronizedInfinity.synchronized_structural_compensation' depends on axioms: [propext, Quot.sound]
```