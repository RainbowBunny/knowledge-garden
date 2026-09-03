---
{"dg-publish":true,"permalink":"/north-star/","tags":["gardenEntry"],"dg-note-properties":{}}
---


# North Star

*Why this vault exists, how it is built, and what to do when lost. If you are reading this in the garden: welcome — this is the map.*

## The vision

One connected reference for everything I learn. When something new arrives, the graph should surface everything already known about its objects, and the new thing should enter as a few leaf notes plus the links that place them. Like a literature review that never goes stale; like Lean's self-containment, but in natural language, for humans — no compiler, and none wanted.

## The method — signature and structure

Every piece of knowledge is one of five kinds:

| kind | what it is | lives in | examples |
| --- | --- | --- | --- |
| **Object** | the raw typed things | `math/set theory/` | [[knowledge/math/set theory/relation/Relation\|Relation]], [[knowledge/math/set theory/operation/Binary Operation\|Binary Operation]], [[knowledge/math/set theory/Function\|Function]] |
| **Property** | one axiom, stated once, in the Scope / Condition / Property shape | `math/properties/`, `proof/properties/` | [[knowledge/math/properties/operation/Associativity\|Associativity]], [[knowledge/cryptography/verifiable computing/proof/properties/Soundness\|Soundness]] |
| **Structure / scheme** | object + chosen properties, **composed by links** | `structures/`, `primitive/`, `proof/` | [[knowledge/math/algebra/structures/groups/Group\|Group]], [[knowledge/cryptography/verifiable computing/proof/non-interactive/Non-interactive ARGument\|Non-interactive ARGument]] |
| **Bridge** | a *translation* — two representations of the same thing, stated as an equivalence | wherever its ends are | [[knowledge/cryptography/verifiable computing/relations/arithmetization/R1CS to QAP Reduction\|R1CS to QAP Reduction]], [[knowledge/math/probability/Statistical Distance\|Statistical Distance]] ↔ [[knowledge/cryptography/foundations/Indistinguishability\|Indistinguishability]] |
| **Transform** | a *construction* — give it an $X$, it builds a $Y$. One direction, and it costs a loss factor | filed under the **output** | [[knowledge/cryptography/verifiable computing/proof/Fiat-Shamir Transform\|Fiat-Shamir Transform]], [[knowledge/cryptography/primitive/public-key encryption/Fujisaki-Okamoto Transformation\|Fujisaki-Okamoto Transformation]] |

A definition *links* its axioms and never restates them. `## Syntax` in a crypto note and `### Scope` in a math note are the same slot. Bridge and Transform are told apart by the **loss factor**: an equivalence is a bridge, a multiplicative constant in the theorem is a transform. A transform's inputs sit in its `Building Blocks` block, universally quantified, and each one must reappear in `## Security` as a hypothesis. A property becomes an axiom only when a definition requires it — which is why the folder is `properties/`, not `axioms/`.

Formal systems (first-order logic, equational logic, type theory, security games) are **content, not the medium**: the vault is written in informal-rigorous prose, states each concept once in its home system, and writes bridges where representations meet. Conflicts between systems are resolved by one remark at the boundary where they bite.

## Class and instance

The crypto side's `## Syntax` / `## Scheme` split is one case of a pattern that runs through the whole vault, and Lean's vocabulary names all of it:

| Lean | vault | example |
| --- | --- | --- |
| `class` with data | a **structure** note — carriers, operations, axioms | [[knowledge/math/algebra/structures/rings/Ring\|Ring]], [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption\|Public-Key Encryption]], [[knowledge/math/calculus/Metric Space\|Metric Space]] |
| `class … : Prop` — a **mixin**, one axiom, no data | a note in `properties/` | [[knowledge/math/properties/operation/Associativity\|Associativity]], [[knowledge/math/properties/operation/Cancellativity\|Cancellativity]], [[knowledge/cryptography/verifiable computing/proof/properties/Soundness\|Soundness]] |
| `extends` | **`Extends:`** — this interface *is* that one, plus a condition | [[knowledge/math/algebra/structures/groups/Group\|Group]] over [[knowledge/math/algebra/structures/Monoid\|Monoid]]; [[knowledge/cryptography/verifiable computing/proof/interactive/Argument Systems\|Argument Systems]] over [[knowledge/cryptography/verifiable computing/proof/interactive/Interactive Proof Systems\|Interactive Proof Systems]] |
| `instance` | **`Instantiates:`** — a concrete witness | [[knowledge/math/algebra/structures/rings/examples/Polynomial Ring\|Polynomial Ring]] : [[knowledge/math/algebra/structures/rings/Ring\|Ring]]; [[knowledge/cryptography/primitive/public-key encryption/schemes/Kyber PKE\|Kyber PKE]] : [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption\|Public-Key Encryption]] |
| a `def` on structures | a **Transform** note | [[knowledge/cryptography/verifiable computing/proof/Fiat-Shamir Transform\|Fiat-Shamir Transform]], [[knowledge/cryptography/primitive/public-key encryption/Fujisaki-Okamoto Transformation\|Fujisaki-Okamoto Transformation]] |
| `theorem` | `## Property` / `## Security` | correctness, an IND-CPA reduction |
| `variable` / arguments | the `Setting` block, or the `### Scope` line | $R_q$; a group $\mathbb G$ of prime order |
| `Iff` | a **Bridge** | [[knowledge/cryptography/verifiable computing/relations/arithmetization/R1CS to QAP Reduction\|R1CS to QAP Reduction]] |

The strongest part is the middle row, because it is not an analogy: `properties/` **is** the mixin folder. Mathlib defines `IsDomain` as a `Prop` mixin extending `IsCancelMulZero` and `Nontrivial` — which is exactly *a nonzero ring whose nonzero elements are cancellative*, the composed definition of [[knowledge/math/algebra/structures/rings/special rings/Integral Domain\|Integral Domain]] this vault already wants. Independent convergence is the best evidence the shape is right. **[Standard]**

It also says when to stop: **a mixin declares no carriers.** If a note in `properties/` starts introducing a set or an operation of its own, it has become a class and belongs in `structures/`.

### Carried by four fields, not by rewriting

The semantics live in four optional header lines, not in renamed headings:

```
Extends:      [[knowledge/math/algebra/structures/Monoid\|Monoid]] + [[Inverse Element]]
Instantiates: [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption\|Public-Key Encryption]]
Requires:     [[Extendable Output Function]]
Reference:    <source>
```

`Extends` is inheritance, `Instantiates` is a witness, `Requires` is a `Building Blocks` dependency. All three are wikilinks, so the class graph, the instance graph and the dependency graph become queryable and lintable. `## Definition`, `## Syntax` and `## Scheme` stay exactly as they are.

### Where the analogy does not reach

- **Most of the vault is not a structure.** About 200 of 557 notes are — `math/properties/`, `math/algebra/structures/`, `math/set theory/`, `cryptography/primitive/`, `verifiable computing/`. The other ~350 are *problems* (SVP, discrete log), *algorithms* (LLL, the `cs/` notes), *theorems*, hubs, language references and narrative. A problem is not a class; do not give it an `Instantiates:` line to be consistent.
- **There is no instance resolver here.** Lean spends real machinery on diamonds — [[knowledge/math/algebra/structures/fields/Field\|Field]] inherits [[knowledge/math/algebra/structures/rings/Ring\|Ring]] by two routes and the compiler reconciles them. In prose those are just two links, and the shared ancestor is invisible. Copying `extends` without a resolver means noticing diamonds is *your* job.
- **Skip the bundled/unbundled question entirely.** It is an artefact of Lean's elaborator, not a fact about mathematics.

## The precision skeleton

Prose is free everywhere **except five places**. These get checked; everything else is voice:

1. **Scope lines type-check** — every symbol declared with its type; every link targets the declared kind.
2. **Quantifiers bound, order explicit.**
3. **Definition ≠ theorem** — consequences never live inside definition callouts.
4. **Side conditions in the Condition slot** — "nonzero" is a condition, not an equation.
5. **Dependencies are links** — a concept a definition uses but cannot link is a *detected gap*: create the note.

## Note sections

`## Definition` holds what you must **stipulate** — the defining callout plus the derived vocabulary that only exists once the object does. `## Property` holds what you can **prove**. Then `## Variant`, `## Example`, `## Related`, with an optional `## Intuition` on top.

On the crypto side the defining slot splits in two, because the two halves carry different obligations. `## Syntax` declares an **interface** — the tuple of algorithms and the spaces they range over, in a `[!definition]`; other notes then quantify over it. `## Scheme` gives an **instance** — concrete code, in a `[!scheme]` — and owes a `## Property`/`### Correctness` plus a `## Security` section whose callout links **up** to the interface's game and **down** to an assumption. Interface is to instance as `class` is to `instance`. Inside the `[!scheme]` callout the **setting** is declared before the algorithms, in slots chosen so each points somewhere different: **Parameters** (knobs, pointing nowhere) · **Setting** (down into `math/`) · **Spaces** (up into the primitive) · **Distribution** · **Building Block** (sideways into another crypto note) · **Parties**. That block is the crypto form of the math side's `### Scope` line — same job, same rule: no algorithm may mention a symbol the setting has not declared. Model: [[knowledge/cryptography/primitive/public-key encryption/schemes/Kyber PKE\|Kyber PKE]] against [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption\|Public-Key Encryption]]. Spelled out in [[Cryptography Layer\|Cryptography Layer]].

A derived concept graduates to its own note **when a note other than its parent needs to link it** — never as a heading anchor. Heading anchors are invisible to `vault-lint`, break silently on rename, and record the backlink against the wrong concept.

## Two views

A concept with two equivalent characterizations is stated **once**, in one primary form.

- **Same domain** — the other forms follow as an `## Equivalent Characterizations` theorem in the same note. Model: [[knowledge/cryptography/primitive/symmetric encryption/Perfect Security\|Perfect Security]].
- **Different domains** — each side keeps its own idiom, and one carries a bridge remark naming the equivalence. Never the whole concept twice. Model: [[knowledge/math/probability/Statistical Distance\|Statistical Distance]] → [[knowledge/cryptography/foundations/Indistinguishability\|Indistinguishability]].
- **Not equivalent** — the surviving direction and the separating example *are* the content. Model: statistical vs computational [[knowledge/cryptography/foundations/Indistinguishability\|Indistinguishability]].

Cryptography is dense in these, because a security notion can be phrased as what an adversary cannot do, or as what information is not there — and most foundational results are the theorem that the two coincide.

In multi-party and interactive notes the bridge has a standard form: the **view** of a party, $\mathsf{View}_i = (x_i, r_i, m_i^{(1)}, \dots, m_i^{(\rho)})$, written as a `[!remark]` under `## Syntax`. It is what turns “no party learns anything” into “this tuple is simulatable from strictly less”, and it is the same remark for MPC privacy, zero knowledge and garbling obliviousness. Model: [[knowledge/cryptography/verifiable computing/secure computation/Multi-Party Computation\|Multi-Party Computation]]. Write one only when the security notion actually quantifies over the view — never above a bare soundness section.

## Intuition

Notes meant for sharing open with an `## Intuition` section (nLab's *Idea*) — always outside the definition callouts, so the friendly voice never contaminates the skeleton.

## When lost

1. Enter through a hub: [[knowledge/math/Math MOC\|Math MOC]] · [[knowledge/cryptography/Cryptography MOC\|Cryptography MOC]] · [[knowledge/complexity/Complexity MOC\|Complexity MOC]] · [[knowledge/cs/CS MOC\|CS MOC]] · [[knowledge/information theory/Information Theory MOC\|Information Theory MOC]] · [[knowledge/security/Security MOC\|Security MOC]].
2. Learning something new: name its **objects** → search each → backlinks show everything already known → file what is missing as leaf notes → add one line to the right MOC → if it translates between representations, write the **bridge**.
3. Notation lives in [[academic/Tag System\|Tag System]]; the object → axiom → structure spine is mapped in [[Foundation Layer\|Foundation Layer]] and its crypto counterpart in [[Cryptography Layer\|Cryptography Layer]]; live work — and how to hand it back to Claude — is in [[Vault Refactoring Plan\|Vault Refactoring Plan]].
4. Before committing: `python scripts/vault-lint.py`. Broken links and duplicate names are always real; the other four checks are smells.

## Known tensions

Kept here deliberately, so the vision stays honest:

- **This is a solo nLab.** Curation cost grows with the vault while my time does not; entropy is continuous (new notes arrive faster than hubs absorb them). Perfection is an asymptote — budget a recurring gardening pass and accept decay between passes.
- **Backlinks find what was linked, not everything related.** Silent relatedness — same technique, analogous proof — is invisible until a bridge note names it. Search and memory still matter.
- **Cryptography moves; the Stacks Project's subject does not.** Notes hold *concepts*; papers are references, not sources of truth; security-level claims get a date.
- **The skeleton has no compiler.** Clone-and-edit errors recurred three times *under active review*. Review rhythm, git commits, and lint scripts are the substitute — without them, drift wins.
- **The garden shows a slice.** A composed definition reads broken to a visitor if its axiom links are unpublished. Publish dependency closures, not lone notes.
