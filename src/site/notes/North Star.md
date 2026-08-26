---
{"dg-publish":true,"permalink":"/north-star/","tags":["gardenEntry"],"dg-note-properties":{}}
---


# North Star

*Why this vault exists, how it is built, and what to do when lost. If you are reading this in the garden: welcome — this is the map.*

## The vision

One connected reference for everything I learn. When something new arrives, the graph should surface everything already known about its objects, and the new thing should enter as a few leaf notes plus the links that place them. Like a literature review that never goes stale; like Lean's self-containment, but in natural language, for humans — no compiler, and none wanted.

## The method — signature and structure

Every piece of knowledge is one of four kinds:

| kind | what it is | lives in | examples |
| --- | --- | --- | --- |
| **Object** | the raw typed things | `math/set theory/` | [[knowledge/math/algebra/structures/set theory/relation/Relation\|Relation]], [[knowledge/math/algebra/structures/set theory/operation/Binary Operation\|Binary Operation]], [[knowledge/math/algebra/structures/set theory/Function between Sets\|Function between Sets]] |
| **Property** | one axiom, stated once, in the Scope / Condition / Property shape | `math/properties/`, `proof/properties/` | [[knowledge/math/properties/operation/Associativity\|Associativity]], [[knowledge/cryptography/verifiable computing/proof/properties/Soundness\|Soundness]] |
| **Structure / scheme** | object + chosen properties, **composed by links** | `structures/`, `primitive/`, `proof/` | [[knowledge/math/algebra/structures/groups/Group\|Group]], [[knowledge/cryptography/verifiable computing/proof/non-interactive/Non-interactive ARGument\|Non-interactive ARGument]] |
| **Bridge** | a translation between two representations | wherever its ends are | [[knowledge/cryptography/verifiable computing/relations/arithmetization/R1CS to QAP Reduction\|R1CS to QAP Reduction]], [[knowledge/cryptography/verifiable computing/proof/Fiat-Shamir Transform\|Fiat-Shamir Transform]] |

A definition *links* its axioms and never restates them. `## Syntax` in a crypto note and `### Scope` in a math note are the same slot. A property becomes an axiom only when a definition requires it — which is why the folder is `properties/`, not `axioms/`.

Formal systems (first-order logic, equational logic, type theory, security games) are **content, not the medium**: the vault is written in informal-rigorous prose, states each concept once in its home system, and writes bridges where representations meet. Conflicts between systems are resolved by one remark at the boundary where they bite.

## The precision skeleton

Prose is free everywhere **except five places**. These get checked; everything else is voice:

1. **Scope lines type-check** — every symbol declared with its type; every link targets the declared kind.
2. **Quantifiers bound, order explicit.**
3. **Definition ≠ theorem** — consequences never live inside definition callouts.
4. **Side conditions in the Condition slot** — "nonzero" is a condition, not an equation.
5. **Dependencies are links** — a concept a definition uses but cannot link is a *detected gap*: create the note.

## Intuition

Notes meant for sharing open with an `## Intuition` section (nLab's *Idea*) — always outside the definition callouts, so the friendly voice never contaminates the skeleton.

## When lost

1. Enter through a hub: [[knowledge/math/Math MOC\|Math MOC]] · [[knowledge/cryptography/Cryptography MOC\|Cryptography MOC]] · [[knowledge/complexity/Complexity MOC\|Complexity MOC]] · [[knowledge/cs/CS MOC\|CS MOC]] · [[knowledge/information theory/Information Theory MOC\|Information Theory MOC]] · [[knowledge/security/Security MOC\|Security MOC]].
2. Learning something new: name its **objects** → search each → backlinks show everything already known → file what is missing as leaf notes → add one line to the right MOC → if it translates between representations, write the **bridge**.
3. Notation lives in [[academic/Tag System\|Tag System]]; live work in [[Vault Refactoring Plan\|Vault Refactoring Plan]].

## Known tensions

Kept here deliberately, so the vision stays honest:

- **This is a solo nLab.** Curation cost grows with the vault while my time does not; entropy is continuous (new notes arrive faster than hubs absorb them). Perfection is an asymptote — budget a recurring gardening pass and accept decay between passes.
- **Backlinks find what was linked, not everything related.** Silent relatedness — same technique, analogous proof — is invisible until a bridge note names it. Search and memory still matter.
- **Cryptography moves; the Stacks Project's subject does not.** Notes hold *concepts*; papers are references, not sources of truth; security-level claims get a date.
- **The skeleton has no compiler.** Clone-and-edit errors recurred three times *under active review*. Review rhythm, git commits, and lint scripts are the substitute — without them, drift wins.
- **The garden shows a slice.** A composed definition reads broken to a visitor if its axiom links are unpublished. Publish dependency closures, not lone notes.
