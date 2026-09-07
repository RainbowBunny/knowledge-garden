---
{"dg-publish":true,"permalink":"/note-layouts/","dg-note-properties":{}}
---

# Note Layouts

*Every skeleton in one place. Pick a row, copy the block. The reasoning behind each lives in [[North Star\|North Star]], [[Foundation Layer\|Foundation Layer]] and [[Cryptography Layer\|Cryptography Layer]]; this file is the lookup.*

Insertable copies are in `templates/`, prefixed `layout-` — **Insert template** puts one at the cursor.

## Which layout?

| you are writing | layout | lives in |
| --- | --- | --- |
| a typed thing — set, relation, function, operation | **Object** | `set theory/` |
| one axiom, no carriers of its own | **Property** (a mixin) | `properties/` |
| an object plus chosen axioms | **Structure** | `structures/` |
| a concrete model of a structure | **Example** | `structures/…/examples/` |
| a cryptographic interface — a tuple of algorithms | **Primitive** | `primitive/`, `proof/` |
| one concrete instantiation of a primitive | **Scheme** | `schemes/`, `scheme/` |
| *give me an $X$, I build you a $Y$* | **Transform** | under the **output** primitive |
| *these two are the same thing seen differently* | **Bridge** | wherever its ends are |
| a worst-case computational problem | **Problem** | `complexity/`, `cs/problems/` |
| the average-case hardness claim | **Assumption** | `cryptography/assumptions/` |
| a security notion — any game | **Security property** | `proof/properties/`, beside its primitive |
| a named result other notes invoke | **Theorem** | with its subject |
| a hub | **MOC** | beside what it indexes |

**The two tests that decide most cases.** Does it declare carriers of its own? If no, it is a Property, not a Structure. Does the theorem about it carry a multiplicative loss factor? If yes, it is a Transform, not a Bridge.

## Header fields

Above the first heading, only what applies:

| field | means | example |
| --- | --- | --- |
| `Reference:` | where it comes from | a paper URL, a book and section |
| `Extends:` | this interface **is** that one, plus a condition | `Extends: [[Monoid]] + [[Inverse Element]]` |
| `Instantiates:` | a concrete witness of an interface | `Instantiates: [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption\|Public-Key Encryption]]` |
| `Requires:` | building blocks it calls | `Requires: [[Extendable Output Function]]` |
| `Import` | parameters pulled from another note, inside a `Parameters` callout | `[[Syndrome Decoding Problem]]: Import $(n, k, w, \mathbb F_2, \mathsf{wt}_\mathsf{H})$` |

---

## 1 · Object

```markdown
Reference:

## Definition

> [!definition] <Name>
> <the defining sentence; every symbol typed, every dependency a link>

### <Derived vocabulary that only exists once the object does>

## Property

## Variant

## Example

## Related
```

## 2 · Property — a mixin

```markdown
## Definition

> [!definition] <Name>
> ### Scope
> A [[Binary Operation]] $\star : O \times O \to O$.
>
> ---
> ### Condition
> <side conditions — "nonzero", "$w \mid n$". Omit when there are none>
>
> ---
> ### Property
> $\star$ is **<name>** iff
> $\forall x \in O: \dots$

## Property

### <theorems about the property itself — these are what inheritance buys>

## Example

### <where it holds, and the counterexample where it fails — the boundary is the point>

## Related
```

**A mixin declares no carriers.** The moment it introduces a set or an operation of its own it has become a Structure.

## 3 · Structure

```markdown
Extends: [[<parent>]] + [[<the added axiom>]]
Reference:

## Definition

> [!definition] <Name>
> A **<name>** is a [[<parent>]] $(S, \star)$ that additionally satisfies [[<axiom>]].

## Structure

## Property

## Variant

## Example

## Related
```

Compose by **link**. A definition that restates an axiom it could link is the one thing this vault is against.

## 4 · Example — an instance

```markdown
Instantiates: [[<the structure>]]
Reference:

## Definition

> [!definition] <Name>
> <the carrier and the operations, concretely>

## Property

### <what is special about this one — not what every instance has>

## Related
```

---

## 5 · Primitive — a cryptographic interface

```markdown
---
dg-publish: true
---
Reference:

## Syntax

> [!definition] <Primitive> Scheme
> A **<primitive>** $\Pi = (\mathsf{Alg}_1, \dots)$ is a tuple of efficient algorithms with
> <spaces: $\mathcal M$, $\mathcal C$, $\mathcal K$, …>.
> - $out \leftarrow \mathsf{Alg}_1(in)$: <one sentence>

> [!remark] View                        ← multi-party / interactive only
> $\mathsf{View}_i = (x_i, r_i, m_i^{(1)}, \dots)$ — and which security notion quantifies over it.

## Property

### Correctness

## Security

### <Game name>

> [!definition] <Primitive> <Game> Advantage
> $\mathsf{Adv}^{\text{<game>}}_\Pi(\mathcal A) = \dots$
> $\Pi$ is **<notion>** if <quantifier> such that the advantage is <bound> for every $\mathcal A \in \mathbb A$.

## Related
```

`## Security` here holds **definitions of advantage**. A number belongs one level down, in a Scheme.

## 6 · Scheme — one instantiation

```markdown
---
dg-publish: true
---
Reference:

## Scheme

Reference Name: $\mathsf{<Name>}$
Instantiates: [[<Primitive>]]

### Setting

> [!scheme] Setting
> - <the ambient mathematics: $R_q$, a group $\mathbb G$, $\bmod^{\pm}$ — links into `math/`>

### Parameters

> [!scheme] Parameters
> - <the knobs you choose; these link nowhere>

### Building Blocks

> [!scheme] Building Blocks
> - <other cryptographic objects it calls — **every bullet is a wikilink**>

### Algorithms

> [!scheme] Algorithms
> - $out \leftarrow \mathsf{Alg}(in)$:
> 	1. …

## Property

### Correctness

> [!property] $\mathsf{<Name>}$ Correctness

## Security

### <Game name>

> [!security]
> For any [[<Primitive>#<Game>|<game> adversary]] $\mathcal A$ there is a
> [[<Assumption>#Assumption|<assumption> adversary]] $\mathcal B$ with $\dots$

## Cryptanalysis                        ← attacks, not games. `[!attack]`

## Related
```

The security callout links **up** to the primitive's game and **down** to an assumption. Without both it is a floating claim.

Slot discipline: **Parameters** point nowhere · **Setting** points down into `math/` · **Spaces** point up into the primitive · **Building Blocks** point sideways · **Parties** point into the View remark. Write only the slots that have content; the minimum is Parameters + Algorithms.

## 7 · Transform

```markdown
Reference:

## Syntax

> [!definition] <Name>
> ### Building Blocks
> - $\Pi_\mathsf{in}$: any [[<input primitive>]]     ← universally quantified
> - $H$: a hash function
>
> ---
> ### Algorithms
> …

## Property
### Correctness

## Security

> [!security]
> If $\Pi_\mathsf{in}$ is <hypothesis> and $H$ is <hypothesis>, then the output is <notion>,
> with loss factor $\dots$

## Related
```

**Every Building Block must reappear in `## Security` carrying a hypothesis.** Blocks with no hypothesis mean the security section is unfinished.

---

## 8 · Problem — worst case

```markdown
Reference:

## Definition

> [!definition] Parameters
> - <or `[[<other problem>]]: Import (…)`>

> [!definition] <Name> Relation
> ### Scope
> Instance: <format>.  Solution: <format>.
>
> ---
> ### Condition
> <parameter constraints>
>
> ---
> ### Relation
> $(\text{instance}, \text{solution}) \in \mathcal R$ iff <predicate>

## Problem

### Search Variant
Given an instance, find a solution.

### Decision Variant
Is the instance in $\mathcal L_\mathcal R = \{\mathbf x : \exists \mathbf w,\ (\mathbf x, \mathbf w) \in \mathcal R\}$?

## Claim

> [!remark]
> <NP-completeness, and best known algorithms with their cost>

## Related
```

**No distribution appears here.** `### Scope` is the instance *format*; a measure on it belongs to the Assumption.

## 9 · Assumption — average case

```markdown
Reference:

## Parameters

> [!definition] Parameters
> - [[<the Problem>]]: Import $(\dots)$

## Distribution

> [!definition] <Name> Distribution
> ### Distribution
> Sampling experiment: $\mathrm{<NAME>}(\dots)$
> 1. …

## Problem

### Search Variant                      ← a **search game**

> [!definition] Search <Name> Advantage
> $\mathsf{Adv}^\mathsf{search}(\mathcal A) = \Pr[\dots]$

### Decision Variant                    ← a **distinguishing game**

> [!definition] Decision <Name> Advantage
> $\mathsf{Adv}^\mathsf{decide}(\mathcal A) = \big|\Pr[\dots] - \Pr[\dots]\big|$

## Claim

> [!remark]
> <the hardness assertion; whether search and decision are equivalent, and by which theorem>

## Related
```

Two traps. **"Decision" means membership in the Problem note and distinguishing here** — they are different questions. And **worst-case NP-completeness does not imply average-case hardness**; codes have no worst-case→average-case reduction, lattices do. Say so in `## Claim`.

## 10 · Security property — any game, not just proof systems

```markdown
## Definition

> [!definition] <Name>
> ### Scope
> A <primitive> $\Pi$; an [[Adversary]] class $\mathbb A$; auxiliary algorithms (<simulator, extractor>).
>
> ---
> ### Condition
> - **Access** — what $\mathcal A$ may query and when: the oracle set ($\mathcal O_\mathsf{find}, \mathcal O_\mathsf{guess}$),
>   or the response map $\mathcal O$ for a proof system.
> - **Promise** — what the challenger guarantees about the input ($\mathbf x \in \mathcal L$, $\mathbf x \notin \mathcal L$, $(\mathbf x, \mathbf w) \in \mathcal R$, none).
> - **Quantifier** — $\forall \mathcal A$, and where $\exists \mathcal S$ / $\exists \mathcal E$ sits relative to it.
> - **Adaptivity** — when $\mathcal A$ commits, relative to `Setup`.
>
> ---
> ### Property
> $\mathsf{Adv}(\mathcal A) \leq \varepsilon \qquad \text{(or } \geq 1 - \varepsilon \text{ for completeness)}$
> A **search** game ($\Pr[\text{win}]$) or a **distinguishing** game ($|\Pr[G_0] - \Pr[G_1]|$) — see [[Security Game]].

## Variant

## Related
```

**Access is the one general knob.** [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption\|Public-Key Encryption]] already parameterises it — $\mathsf{atk} \in \{\mathsf{cpa}, \mathsf{lta}, \mathsf{cca}\}$ selects which oracles each phase gets — and a proof system's response map is the same slot under another name.

Those four Condition lines are not a wish list: **each one is a place something broke.** Access → an adversary handed the *real* state in a simulated branch. Promise → completeness confused with soundness. Quantifier → a simulator with no $\exists$. Adaptivity → a non-adaptive model written adaptively.

**Where it stops.** Correctness has no adversary; succinctness is a complexity predicate, not a game; and UC / composability is a different framework entirely (an ideal functionality and an environment, not a two-party experiment). Do not force those into this shape.

## 11 · MOC

```markdown
# <Area> MOC

<one sentence: what this area is>

## Theory
## <Concrete things>
## Related
```

## 12 · Theorem

A theorem note is a **Property note whose Scope is its hypotheses**. There is no sixth kind of note.

```markdown
Reference:

## Definition

> [!theorem] <Name>
> ### Scope
> <the hypotheses, each symbol typed and linked>
>
> ---
> ### Condition
> <side conditions the statement silently needs>
>
> ---
> ### Property
> <the conclusion, with its bound>

## Property

### <sharpness, tightness, what fails without each hypothesis>

## Example

### <the counterexample when a hypothesis is dropped>

## Related
```

**When does a theorem graduate?** When it is **invoked, not merely known** — when other notes cite its bound or check its hypotheses. A theorem that is a fact *about* one object stays as a `[!theorem]` inside that object's note.

An empirical version of the same test, which you can just run:

```
grep -rho '^> \[!\(theorem\|lemma\|proposition\|corollary\)\] .\+' --include='*.md' . \
  | sed 's/^> \[![a-z]*\] //' | sort | uniq -c | awk '$1>=2' | sort -rn
```

**A named result stated twice has already earned a note.**

> [!remark] Axiom or theorem — same layout, different consumption site
> The difference is epistemic, not structural, and it shows in *where the link comes from*: an **axiom** is
> linked from a `## Definition` (you stipulate it), a **theorem** from a `## Property` or `## Security`
> (you derive it). That keeps precision rule 3 — *definition ≠ theorem* — intact while letting both share
> the Scope / Condition / Property skeleton.

---

## Slot glossary

| slot | holds | never holds |
| --- | --- | --- |
| `## Intuition` | the friendly reading, for sharing | anything the skeleton depends on |
| `## Definition` | what you must **stipulate** | consequences |
| `## Syntax` | the tuple, the spaces, one line per algorithm | any bound, any adversary |
| `## Scheme` | Setting, Parameters, Building Blocks, Algorithms | correctness, security |
| `## Property` | what holds **unconditionally** — provable without an adversary | anything with $\mathcal A$ in it |
| `## Security` | games and bounds — what holds **against someone** | attacks |
| `## Cryptanalysis` | concrete attacks, broken parameters, history | definitions |
| `## Variant` | same object, different scope | a different object |
| `## Example` | instances, **and counterexamples** | theory |
| `## Related` | links out | content |

## Callout types

`definition` · `theorem` · `proposition` · `lemma` · `corollary` · `remark` · `example` · `property` · `security` · `scheme` · `algorithm` · `pseudocode` (CLRS-style code) · `construction` · `question` · `conjecture` · `principle` · `proof` · `todo`

Two are styled and unused — start using them: **`[!intuition]`** for the `## Intuition` section, **`[!attack]`** for `## Cryptanalysis`.

## Where the reasoning lives

- [[North Star\|North Star]] — the five kinds of note, the precision skeleton, two views, class/instance
- [[Foundation Layer\|Foundation Layer]] — the `math/` spine, axiom inventory, note drafts
- [[Cryptography Layer\|Cryptography Layer]] — interface/instance, scheme settings, party views, the game properties
