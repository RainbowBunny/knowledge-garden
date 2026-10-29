---
{"dg-publish":true,"permalink":"/note-layouts/","dg-note-properties":{}}
---

# Note Layouts

*Every skeleton in one place. Pick a row, copy the block. The reasoning behind each lives in [[North Star\|North Star]], [[Foundation Layer\|Foundation Layer]] and [[Cryptography Layer\|Cryptography Layer]]; this file is the lookup.*

Insertable copies are in `templates/`, prefixed `layout-` — **Insert template** puts one at the cursor.

## Which layout?

| you are writing                                     | layout                     | lives in                                     |
| --------------------------------------------------- | -------------------------- | -------------------------------------------- |
| a typed thing — set, relation, function, operation  | **Object** (1)             | `math/set theory/`                           |
| one axiom, no carriers of its own                   | **Property** (2), a mixin  | `math/property/`                             |
| an object plus chosen axioms                        | **Structure** (3)          | `math/algebra/structures/`                   |
| a concrete model of a structure                     | **Example** (4)            | `structures/<X>/example/`                    |
| a cryptographic interface — a tuple of algorithms   | **Primitive** (5)          | `primitive/`, `special function/`, `verifiable computing/`, `secure computation/` |
| one concrete instantiation of a primitive           | **Scheme** (6)             | `<primitive>/scheme/`                        |
| an interactive protocol for one language            | **Scheme** (6)             | `complexity/proof system/protocol/`          |
| *give me an $X$, I build you a $Y$*                 | **Transform** (7)          | under the **output** primitive               |
| *these two are the same thing seen differently*     | **Bridge**                 | wherever its ends are                        |
| a worst-case computational problem                  | **Problem** (8)            | `complexity/problem/<subject>/`              |
| the average-case hardness claim                     | **Assumption** (9)         | `cryptography/assumptions/`                  |
| a security notion — any game                        | **Security property** (10) | `verifiable computing/property/`             |
| a named result other notes invoke                   | **Theorem** (12)           | with its subject                             |
| a machine — configurations and a step relation      | **Machine** (13)           | `computability/computing model/`             |
| a parameterised family $\mathsf{X}(f(n))$           | **Generator** (14)         | `complexity/complexity class/generator/<resource>/` |
| one named complexity class                          | **Complexity class** (15)  | `complexity/complexity class/class/<resource>/` |
| a name for a bundle of properties on an existing syntax | **Composition**       | beside the syntax note it composes           |
| a hub                                               | **MOC** (11)               | beside what it indexes; family hubs (elliptic-curve, post-quantum) in `cryptography/family/` |

**Where it lives.** One home per object, at the lowest layer where it can be stated: the lattice in `math/`, SVP in `complexity/problem/`, LWE in `cryptography/assumptions/`, the lattice trapdoor with the trapdoor functions. Folders name kinds; a family (lattice-based, post-quantum) or a status (NP-complete, worst case) is a field, not a folder. The one exception is `assumptions/`, split by family because that is the natural split there.

**The two tests that decide most cases.** Does it declare carriers of its own? If no, it is a Property, not a Structure. Does the theorem about it carry a multiplicative loss factor? If yes, it is a Transform, not a Bridge.

## Header fields — provenance above, relations inside

**Revised 2026-09-09.** Two kinds, and they do not belong in the same place:

- **Provenance** is about the *note* — where you read it. Goes **above the first heading**.
- **Relations** are about the *object* — they are clauses of the definition. Go **inside the definition callout**, written with `::` so Dataview still indexes them.

The vault already did this in prose: [[knowledge/math/algebra/structures/ring/special ring/Integral Domain\|Integral Domain]] reads *"an integral domain is a nonzero [[knowledge/math/algebra/structures/ring/special ring/Commutative Ring\|Commutative Ring]] $R$ (with 1) such that…"* — the parent sits inside the definition. A structured field is that same idea made queryable, not a competing convention.

> [!warning] The field never replaces the sentence
> `Extends:: [[Monoid]]` alone does not say **what is added**. The definition still owes the delta —
> *"Extends [[knowledge/computability/computing model/turing machine/Turing Machine\|Turing Machine]]; the transition function becomes …"*

Fields:

| field                 | means                                                     | example                                                        |
| --------------------- | --------------------------------------------------------- | -------------------------------------------------------------- |
| `Reference:` *header* | where it comes from                                       | a paper URL, a book and section                                |
| `aliases:` *frontmatter* | other names for the note, the acronym first             | `aliases: [SNARK]`                                             |
| `Extends::`           | this **is** that one, plus a condition                    | `Extends:: [[Multitape Turing Machine]]`                       |
| `Generalizes::`       | this **widens a slot** of that one                        | `Generalizes:: [[knowledge/computability/computing model/turing machine/Turing Machine\|Turing Machine]]`                             |
| `Instantiates::`      | a concrete witness of an interface                        | `Instantiates:: [[Public-Key Encryption]]`                     |
| `Requires::`          | building blocks, or a theorem's dependencies              | `Requires:: [[Hardness and Completeness]]`                     |
| `Member of::`         | this problem lies in that class                           | `Member of:: [[Class NP]]`                                     |
| `Complete for::`      | complete, **and the reduction**                           | `Complete for:: [[Class NP]] under [[Polynomial-time Karp Reducibility]]` |
| `Hard for::`          | hard, and the reduction                                   | `Hard for:: [[Class NP]] under [[Polynomial-time Karp Reducibility]]`    |
| `Import`              | symbols pulled from the note that declares them, as a bullet of a `Parameters` callout | `[[Syndrome Decoding Problem]]: Import $(n, k, w)$`       |

> [!warning] Two ways a field silently fails
> **One colon.** `Instantiates:` is invisible to Dataview. Every relation key takes `::`.
> **A link in the key.** Dataview reads everything before `::` as the field name, so
> `[[Hardness and Completeness|Complete]] for:: [[Class NP]]` has the key
> `[[Hardness and Completeness|Complete]] for` and matches nothing.
> **The key is plain text; links belong in the value.** Put the concept link on its own
> `Requires::` line above.

### Extends or Generalizes — the direction test

> **`X Extends:: Y`** iff every X **is** a Y, once you forget X's extra axioms.
> **`X Generalizes:: Y`** iff every Y **is** an X.

Both tolerate a canonical embedding, exactly as Lean's `extends` does with a coercion — $q \mapsto \{q\}$ for DFA ↪ NFA, $\Gamma \cong \Gamma^1$ for TM ↪ Multitape.

Worked: `DFA Extends:: NFA` ✓ (a DFA is an NFA with single-valued $\delta$) · `Multitape Generalizes:: Turing Machine` ✓ (widens $\delta$'s codomain) · `Offline TM Extends:: Multitape` ✓ (adds "never writes tape 1") · `Log-Space Uniform Circuit Family Extends:: Circuit Family` ✓ (adds a generation condition).

This has been reversed three times. When unsure, say the sentence out loud with *"every … is a …"*.

Reversed twice more, found 2026-09-25: [[knowledge/math/algebra/structures/ring/ideal/Principal Ideal Domain\|Principal Ideal Domain]] said `Generalizes:: [[knowledge/math/algebra/structures/ring/special ring/Integral Domain\|Integral Domain]]` ("every integral domain is a PID" — false) and [[knowledge/math/algebra/structures/ring/ideal/Noetherian Ring\|Noetherian Ring]] said `Generalizes:: [[knowledge/math/algebra/structures/ring/special ring/Commutative Ring\|Commutative Ring]]`. Both are `Extends::`.

### Origin and specialization — one concept across structures

For a concept every structure has its own version of — homomorphism, kernel, center, sub-structure, quotient, isomorphism:

| | what it is | where it lives | how it is marked |
| --- | --- | --- | --- |
| **origin** | the concept at its most general Scope | the lowest layer where that Scope exists: `set theory/`, `property/map/`, `structures/` root, `category/` | lists its specializations in a `where \| what the structure adds` table |
| **specialization, a whole note** | e.g. [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]], [[knowledge/math/algebra/structures/ring/subring/Subring\|Subring]], [[knowledge/math/algebra/structures/ring/subring/Ring Center\|Ring Center]] | with its structure | `Extends:: [[origin]]` at the top of its definition callout |
| **specialization, a section** | e.g. `### Kernel` in [[knowledge/math/algebra/structures/ring/Ring Homomorphism\|Ring Homomorphism]] | inside the structure's note | opens with the plain line `Specializes [[origin]].` — not a field: a field would claim the whole note, and the claim is weaker than `Extends` (below) |

**`Specializes` is not `Extends` for sections.** `Extends` promises a literal *is-a*: every [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]] **is** a [[knowledge/math/property/map/Homomorphism\|Homomorphism]]. `Specializes` promises only *"this is the origin's concept in this structure, and the section says how it is presented here."* The kernel shows why the weaker word is needed: [[knowledge/math/set theory/function/Kernel\|knowledge/math/set theory/function/Kernel]] is the relation $f(a') = f(a'')$, while `### Kernel` in [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]] defines the subset $\varphi^{-1}(e)$ — one fibre, which *determines* the relation but is not it. If such a section ever graduates to its own note: literal is-a → `Extends::`; a re-reading like this one → `Requires:: [[origin]]` plus a bridge remark.

**No `Generalizes::` on an origin.** Each edge is declared once, on the note built from the other — the specialization. The origin's `where | what the structure adds` table is the reverse view; for whole-note specializations it can be a query, `LIST FROM [[]] WHERE contains(flat(list(Extends)), this.file.link)` (`FROM [[]]` = notes linking here; `flat(list(…))` copes with one value or several).

A specialization **restates nothing** the origin says. It carries what the structure adds: a theorem (a ring kernel is an [[knowledge/math/algebra/structures/ring/ideal/Ideal\|Ideal]]), a criterion ($ab^{-1} \in H$), a local name (null space). If a section is only the origin's definition with the structure's symbols filled in, it is one line and a link.

Current origins: [[knowledge/math/property/map/Homomorphism\|Homomorphism]] · [[knowledge/math/algebra/category/Morphism\|Morphism]] (isomorphism, mono, epi, endo, auto) · [[knowledge/math/set theory/function/Kernel\|knowledge/math/set theory/function/Kernel]] · [[knowledge/math/algebra/structures/Center\|Center]] · [[knowledge/math/algebra/structures/Substructure\|Substructure]] · [[knowledge/math/set theory/relation/Quotient Relation\|Quotient Relation]] · [[knowledge/math/algebra/category/Categorical Product\|Categorical Product]] / [[knowledge/math/algebra/category/Categorical Coproduct\|Categorical Coproduct]] · [[knowledge/math/property/operation/Identity Element\|Identity Element]] / [[knowledge/math/property/operation/Inverse Element\|Inverse Element]] · [[knowledge/math/algebra/category/Category\|Category]] (its examples use `Instantiates::`).

**Two things that look like this and are not:**

- **A theorem that recurs across structures** — [[knowledge/math/set theory/function/Canonical Decomposition\|Canonical Decomposition]] is the model: one note, one section per structure, because the comparison *is* the content. Theorems stay together; definitions spread out to their structures.
- **Same name, different concept** — lattice (geometric) vs lattice (order), ring ideal vs order ideal, completeness (proof systems / metric spaces / NP), characteristic of a ring vs characteristic function. These get qualified names and no origin. The test: can you write one Scope that both instances fill in? If not, they are homonyms.
- **One word, several concepts** — sort every occurrence *before* looking for an origin. *Order* is four concepts plus homonyms: **size** (order of a group = [[knowledge/math/set theory/Set Foundation#Cardinality\|cardinality]]), **element order** (origin [[knowledge/math/algebra/structures/group/Group Order\|Group Order]]; $\mathbb F_q^*$ and $(\mathbb Z/p)^*$ specialize it), **valuation** ($\mathrm{ord}_p(a)$, multiplicity of a zero or pole), **ordering** ([[knowledge/math/set theory/relation/Preorder\|Preorder]] → [[knowledge/math/set theory/relation/Partial Order\|Partial Order]] → [[knowledge/math/set theory/relation/Total Order\|Total Order]]); order of an ODE and first-order logic are homonyms. *Characteristic* is three: **of a ring** (origin [[knowledge/math/algebra/structures/ring/Ring#Characteristic\|Ring#Characteristic]]), **characteristic polynomial** (a family of its own, over operators), **characteristic function** (indicator $\chi_S$ vs probability $\varphi_X$ — homonyms).


---

## Parameters and Building Blocks — one callout each

**Revised 2026-10-14.** Every object that has variables gets its own `[!definition] Parameters` callout, directly above the callout that defines the object. Building Blocks, when the object has any, get a **separate** `[!definition] Building Blocks` callout. Neither is folded into the definition or into the algorithms.

```markdown
> [!definition] Parameters
> - [[<Note>]]: Import $(\dots)$.        ← symbols another note declares
> - $x$: <what it is>                    ← symbols introduced here

> [!definition] Building Blocks
> - $\Pi$: any [[<primitive>]]           ← other objects it calls

> [!definition] <Name>
> <the definition, or the algorithms>
```

- **Parameters hold variables.** One bullet per symbol the definition uses. A symbol is declared once, in the note that owns it; every other note `Import`s it (see the `Import` row above). Import only symbols the source note lists in its own `Parameters` callout. If it does not, add the line to the source note first, or the import points at nothing.
- **Building Blocks hold objects, never variables.** Other cryptographic objects the definition calls. Every bullet is a wikilink, except at an interface level (layout 7), where a bullet is a universally quantified type.
- **Placement.** Where a layout puts the definition under a heading (`## Syntax`, `## Definition`), the two callouts sit directly under that heading, Parameters first.
- **One per object, not one per note.** A note with several definitions (a correctness notion with a bound $\delta$, a game with oracles and a time bound) gives each its own `Parameters` callout, short as it may be. Omit the callout only when the definition introduces and uses no symbol.
- **Already this way:** Problem (8) and Assumption (9). **Changed to this way:** Primitive (5), Scheme (6), Transform (7), Security property (10). **Not affected:** Property (2) and Theorem (12), whose `### Scope` line plays this role.
- **Extended 2026-10-19, on your instruction:** defining parameters always go in their own callout. Property (2) and Theorem (12) keep `### Scope` for the object the property is about, and add a `Parameters` callout above it when they introduce further symbols (a constant $c$, a measure $\mathcal O$) — [[knowledge/math/property/map/Contraction\|Contraction]], [[knowledge/math/measure theory/Stationary Measure\|Stationary Measure]].

Worked examples: [[knowledge/cryptography/primitive/public-key encryption/scheme/Kyber PKE\|Kyber PKE]] (Parameters and Building Blocks as separate callouts above the algorithms); [[knowledge/cryptography/secure computation/fully homomorphic encryption/Gentry Bootstrapping Transformation\|Gentry Bootstrapping Transformation]] (`Import` lines in Parameters, a quantified Building Block).

---

## Algorithms — signature, Input, Output, Steps

**Revised 2026-10-14.** Every algorithm is written the same way, whether it belongs to an interface or to a construction:

```markdown
> - $out \leftarrow \mathsf{Alg}(in)$: (Randomized | Deterministic) <name of the algorithm>.
>     - **Input**: <each argument, typed, and any promise about it>
>     - **Output**: <each result, typed, including a rejection symbol>
>     - **Steps**: 1. …                    ← constructions only
```

- The signature line says what the algorithm is; Input and Output describe the arguments and results one by one; Steps say how.
- **Interface** (Primitive, 5; a specification such as `Refresh`): Input and Output only. What a caller may rely on, and nothing else.
- **Construction** (Scheme, 6; Transform, 7): Input, Output and Steps. In a Scheme, Input and Output give *this scheme's* concrete types ($\mathrm{pk} = (t, \rho)$); they do not restate the primitive.
- **Promises go in Input** ("$\mathrm{bk}$ is an honest encryption of $\mathrm{sk}_1$ under $\mathrm{pk}_2$"). **Rejection goes in Output** ("or $\perp$").
- **Both at once: split.** An algorithm that is a specification with several constructions (`Refresh`) gets a specification callout in `## Syntax`, each construction gets its own callout with Steps, and correctness is stated once, on the specification.
- Layout 6's short form `out ← Alg(in): 1. …` remains fine for an algorithm whose Input and Output need no words; the signature then carries both.

## Syntax is the most generic form — notation goes in a remark

**Revised 2026-10-14.** A primitive's `## Syntax` is written in the most general form found in the literature, so that each source's variant is the same object with an argument fixed or an output forgotten. Differences in names and arguments are recorded once, in a remark at the end of `## Syntax`:

```markdown
> [!remark] Notation in the literature
> <one sentence: which form this note follows and which sources it generalises>
>
> | source | algorithms | differences |
> | --- | --- | --- |
> | `[BS Def 11.1]` | $(G, E, D)$ | $G()$ takes no argument; $D$ may output a reject symbol |
```

- **Use the vault's names** (`Gen`, `Enc`, `Dec`, `Eval`). Do not rename them to follow a source; list the source's names in the table.
- **List only sources you opened.** Mark a row written from memory `⚠️ verify`.
- **Typical differences:** $\lambda$ vs $1^\lambda$ vs implicit; one key pair vs separate keys (and a separate evaluation key); a reject symbol; explicit coins $r$; the message space ($\mathcal M$ vs $P$; a bit vs a general space); keys written as subscripts.

Worked example: [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption Scheme (Old)\|Public-Key Encryption Scheme (Old)]] and [[knowledge/cryptography/secure computation/fully homomorphic encryption/Homomorphic Encryption\|Homomorphic Encryption]] (drafts in the vault now carry this remark).

---

## Related — relations out, grouped by kind

**Added 2026-10-14.** A flat list of links says *that* two notes are related, not *how*. Provenance is above the first heading and the parent is inside the definition (`Extends::`); `## Related` is the **fan-out**: what hangs off this note. Write only the subsections that have content, in this order:

| subsection | holds | backed by |
| --- | --- | --- |
| `### Descendants` | the **important** notes that `Extends::` or `Generalizes::` this one, each with what it adds | their `Extends::` field |
| `### Instantiations` | schemes and examples that `Instantiates::` this one | their `Instantiates::` field |
| `### Constructions` | transforms and schemes that take this as a Building Block, or produce it | their `Building Blocks` callout |
| `### Properties` | property notes (layout 10) that quantify over this object | the property note's `Import` line |
| `### Siblings` | same-level objects often confused with this one, with the one line that separates them | nothing: curated |
| `### Prerequisites` | what this note `Import`s or `Requires::`, when the parent alone does not cover it | its own fields |

**List or table.** The default is a list, one line per note: `- [[Note]] — what it adds / the one fact that tells it apart`. Use a **table** when three or more entries differ along the same axes: the first column is the link, the others are the axes. The table replaces the list, it does not repeat it. The model is the composition table of [[knowledge/cryptography/verifiable computing/proof system/non-interactive/Non-Interactive Proof Systems\|Non-Interactive Proof Systems]]: rows are notes, columns are the properties each one demands.

**Curated, not complete.** The fields are the source of truth and the full set is a Dataview query over them; `## Related` holds the entries a reader should see first. If an entry has no field behind it, write the field on that note first, otherwise the entry is a claim nobody can query.

```markdown
## Related

### Descendants
| | permitted circuits | adds |
| --- | --- | --- |
| [[Fully Homomorphic Encryption]] | all | the cost bound |
| [[Bootstrappable Encryption]] | contains its own decryption circuit | $\mathsf{Refresh}$ |

### Instantiations
- [[knowledge/cryptography/primitive/public-key encryption/scheme/Kyber PKE\|Kyber PKE]] — Module-LWE

### Constructions
- [[knowledge/cryptography/secure computation/fully homomorphic encryption/Gentry Bootstrapping Transformation\|Gentry Bootstrapping Transformation]] — bootstrappable → leveled

### Properties
- [[Key-Dependent Message Security|KDM Security]]

### Siblings
- [[Key Encapsulation Mechanism]] — encrypts a fresh key, not a message
```

## Composition — a named bundle

*A name for a syntax plus a list of properties.* zk-SNARK is a [[knowledge/cryptography/verifiable computing/proof system/non-interactive/Non-Interactive Proof Systems\|Non-Interactive Proof Systems]] that is complete, knowledge sound, succinct and zero-knowledge; it has no algorithms of its own. It earns a note so that schemes can say `Instantiates:: [[Zero-Knowledge Succinct Non-interactive ARgument of Knowledge|zk-SNARK]]` and so that links have somewhere to land.

```markdown
Reference:

## Definition

> [!definition] <Name>
> Extends:: [[<the nearest bundle, or the syntax note>]]
>
> ---
> A **<name>** is a [[<syntax note>]] that is also [[<Property>]]. <one sentence on what the added property buys>

## Related

### Instantiations
- [[<Scheme>]]
```

Rules.
- **No `Syntax`, no `Parameters`, no algorithms.** They are the base note's. If the bundle needs a parameter (a succinctness bound), it belongs to the property note.
- **Spell the name out.** The note is `Zero-Knowledge Succinct Non-interactive ARgument of Knowledge`, not `zk-SNARK`; the acronym goes in `aliases:` and as link text (`[[…|zk-SNARK]]`), so search and prose still find it. The same goes for any note named after an abbreviation.
- **One parent in `Extends::`**, the nearest bundle (zk-SNARK extends SNARK). Another parent goes in a remark: a SNARK is also a SNARG, since knowledge soundness implies soundness.
- **The base note's `## Variant` table lists every bundle**, each name a link to its note.
- **A composition note is finished when it names its base and its properties.** Add a section only for a result the combination has on its own (a separation, an impossibility), not to fill the page.

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

## Related                          ← grouped: Descendants · Instantiations · Constructions · Properties · Siblings
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

## Related                          ← grouped: Descendants · Instantiations · Constructions · Properties · Siblings
```

**A mixin declares no carriers.** The moment it introduces a set or an operation of its own it has become a Structure.

## 3 · Structure

```markdown
Reference:

## Definition

> [!definition] <Name>
> Extends:: [[<parent>]] + [[<the added axiom>]]
> A **<name>** is a [[<parent>]] $(S, \star)$ that additionally satisfies [[<axiom>]].

## Structure

## Property

## Variant

## Example

## Related                          ← grouped: Descendants · Instantiations · Constructions · Properties · Siblings
```

Compose by **link**. A definition that restates an axiom it could link is the one thing this vault is against.

## 4 · Example — an instance

```markdown
Reference:

## Definition

> [!definition] <Name>
> Instantiates:: [[<the structure>]]
> <the carrier and the operations, concretely>

## Property

### <what is special about this one — not what every instance has>

## Related                          ← grouped: Descendants · Instantiations · Constructions · Properties · Siblings
```

---

## 5 · Primitive — a cryptographic interface

```markdown
---
dg-publish: true
---
Reference:

## Syntax

> [!definition] Parameters
> - $\lambda$: the security parameter
> - $\mathcal M$, $\mathcal C$, $\mathcal K$, …: <the spaces>
> - [[<Base primitive>]]: Import $(\dots)$        ← only when this primitive extends another

> [!definition] <Primitive> Scheme
> A **<primitive>** $\Pi = (\mathsf{Alg}_1, \dots)$ is a tuple of efficient algorithms over the security parameter and the spaces of Parameters.
> - $out \leftarrow \mathsf{Alg}_1(in)$: (Randomized | Deterministic) <name>.
>     - **Input**: <arguments, typed>
>     - **Output**: <results, typed>

> [!remark] Notation in the literature
> <which form this note follows; table of source / algorithms / differences>

> [!remark] View                        ← multi-party / interactive only
> $\mathsf{View}_i = (x_i, r_i, m_i^{(1)}, \dots)$ — and which security notion quantifies over it.

## Property

### Correctness

## Security

### <Game name>

> [!definition] <Primitive> <Game> Advantage
> <the experiment as a challenger/adversary table — see "Game form" under layout 10>
> $\mathsf{Adv}^{\text{<game>}}_\Pi(\mathcal A) = \dots$
> $\Pi$ is **<notion>** if <quantifier> such that the advantage is <bound> for every $\mathcal A \in \mathbb A$.

## Related                          ← grouped: Descendants · Instantiations · Constructions · Properties · Siblings
```

`## Security` here holds **definitions of advantage**. A number belongs one level down, in a Scheme.

A primitive is an interface, so it has no `Building Blocks` callout. A primitive that extends another ([[knowledge/cryptography/secure computation/fully homomorphic encryption/Homomorphic Encryption\|Homomorphic Encryption]] extends [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption Scheme (Old)\|Public-Key Encryption Scheme (Old)]]) `Import`s the base's symbols in its `Parameters` and adds its own.

## 6 · Scheme — one instantiation

```markdown
---
dg-publish: true
---
Reference:

## Scheme

Reference Name: $\mathsf{<Name>}$
Instantiates:: [[<Primitive>]]

### Setting

> [!scheme] Setting
> - <the ambient mathematics: $R_q$, a group $\mathbb G$, $\bmod^{\pm}$ — links into `math/`>

### Parties                              ← protocols only

> [!definition] Parties
> - <who exists and what each holds: the parties, a CA, a channel; a system parameter shared by all>

### Parameters

> [!definition] Parameters
> - <the knobs you choose; these link nowhere>
> - [[<Note>]]: Import $(\dots)$        ← the one exception: symbols another note declares

### Building Blocks

> [!definition] Building Blocks
> - <other cryptographic objects it calls — **every bullet is a wikilink**>

### Algorithms

> [!scheme] Algorithms
> - $out \leftarrow \mathsf{Alg}(in)$: (Randomized | Deterministic) <name>.
>     - **Input**: <this scheme's concrete types>
>     - **Output**: <…>
>     - **Steps**: 1. …

## Property

### Correctness

> [!property] $\mathsf{<Name>}$ Correctness

## Security

### <Game name>

> [!security]
> For any [[<Primitive>#<Game>|<game> adversary]] $\mathcal A$ there is a
> [[<Assumption>#Assumption|<assumption> adversary]] $\mathcal B$ with $\dots$

## Cryptanalysis                        ← attacks, not games. `[!attack]`

## Related                          ← grouped: Descendants · Instantiations · Constructions · Properties · Siblings
```

The security callout links **up** to the primitive's game and **down** to an assumption. Without both it is a floating claim.

> [!remark] The same layout serves a complexity protocol
> An interactive protocol for one language — a Graph Non-Isomorphism protocol, [[knowledge/complexity/proof system/protocol/Sum-Check Protocol\|Sum-Check Protocol]],
> [[knowledge/cryptography/verifiable computing/proof system/interactive/scheme/Schnorr Protocol\|Schnorr Protocol]] — is a Scheme whose primitive is a proof system: `Instantiates:: [[Probabilistic Interactive Proof System]]`,
> `### Setting` points **down** at the language, `### Parties` are Prover and Verifier.
> Two adjustments: `## Security` holds the **soundness error** rather than a game, and `## Cryptanalysis` is omitted.

Slot discipline: **Parameters** point nowhere (an `Import` line is the one exception: it points at the note that declares the symbol) · **Setting** points down into `math/` · **Spaces** point up into the primitive · **Building Blocks** point sideways · **Parties** point into the View remark. Write only the slots that have content; the minimum is Parameters + Algorithms.

## 7 · Transform

```markdown
Reference:

## Syntax

> [!definition] Parameters
> - [[<Note>]]: Import $(\dots)$.
> - $d$: <a knob of the transform>

> [!definition] Building Blocks
> - $\Pi_\mathsf{in}$: any [[<input primitive>]]     ← universally quantified
> - $H$: a hash function

> [!definition] <Name>
> - $out \leftarrow \mathsf{Alg}(in)$: (Randomized | Deterministic) <name>.
>     - **Input**: …
>     - **Output**: …
>     - **Steps**: 1. …

## Property
### Correctness

## Security

> [!security]
> If $\Pi_\mathsf{in}$ is <hypothesis> and $H$ is <hypothesis>, then the output is <notion>,
> with loss factor $\dots$

## Related                          ← grouped: Descendants · Instantiations · Constructions · Properties · Siblings
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

### Search Variant                      ← a **search game**, drawn as in layout 10

> [!definition] Search <Name>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $(\mathbf x, \mathbf w) \leftarrow \mathrm{<NAME>}(\dots)$ | $\xrightarrow{\ \mathbf x\ }$ | |
> | 2 | | $\xleftarrow{\ \mathbf w'\ }$ | outputs a candidate solution $\mathbf w'$ |
>
> **Goal** — $\mathcal A$ wins iff:
> - <the winning condition, one bullet each>
>
> $\mathsf{Adv}^\mathsf{search}(\mathcal A) = \Pr[\mathcal A \text{ wins}].$

### Decision Variant                    ← a **distinguishing game**, drawn as in layout 10

> [!definition] Decision <Name>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | **Game 0**: $\mathbf x \leftarrow \mathrm{<NAME>}(\dots)$<br>**Game 1**: $\mathbf x \leftarrow U(\dots)$ | $\xrightarrow{\ \mathbf x\ }$ | |
> | 2 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}_b(\mathcal A)$, the bit $b'$ in Game $b$.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}_1(\mathcal A) = 1]$ are.
>
> $\mathsf{Adv}^\mathsf{decide}(\mathcal A) = \big|\Pr[\mathsf{Expt}_0(\mathcal A) = 1] - \Pr[\mathsf{Expt}_1(\mathcal A) = 1]\big|.$

## Claim

> [!remark]
> <the hardness assertion; whether search and decision are equivalent, and by which theorem>

## Related                          ← grouped: Descendants · Instantiations · Constructions · Properties · Siblings
```

Two traps. **"Decision" means membership in the Problem note and distinguishing here** — they are different questions. And **worst-case NP-completeness does not imply average-case hardness**; codes have no worst-case→average-case reduction, lattices do. Say so in `## Claim`.

## 10 · Security property — any game, not just proof systems

```markdown
## Definition

> [!definition] Parameters
> - [[<Primitive>]]: Import $(\lambda, \dots)$.
> - $\mathbb A$, …: <the classes the game quantifies over>

> [!definition] <Name>
> ### Scope
> The primitive $\Pi$ and the [[Adversary]] class $\mathbb A$ of Parameters; auxiliary algorithms (<simulator, extractor>).
>
> ---
> ### Condition
> - **Access** — what $\mathcal A$ may query and when, or the response map $\mathcal O$ for a proof system.
> - **Promise** — what the challenger guarantees about the input ($\mathbf x \in \mathcal L$, $\mathbf x \notin \mathcal L$, $(\mathbf x, \mathbf w) \in \mathcal R$, none).
> - **Quantifier** — $\forall \mathcal A$, and where $\exists \mathcal S$ / $\exists \mathcal E$ sits relative to it.
> - **Adaptivity** — when $\mathcal A$ commits, relative to `Setup`.
>
> ---
> ### Experiment                       ← two stateful interactive machines, not a list of assignments
> <one sentence: search or distinguishing; which row branches> `[<source and number>]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $\mathrm{aux} \leftarrow \mathcal P(1^\lambda)$<br>$(\mathrm{pk}, \mathrm{sk}) \leftarrow \mathsf{KeyGen}(1^\lambda, \mathrm{aux})$ | $\xrightarrow{\ \mathrm{pk}\ }$ | |
> | 2 | | $\xleftarrow{\ m_0,\, m_1\ }$ | chooses $m_0, m_1 \in \mathcal M$ with $\lvert m_0 \rvert = \lvert m_1 \rvert$ |
> | 3 | **Game 0**: $c^* \leftarrow \mathsf{Enc}(\mathrm{pk}, m_0)$<br>**Game 1**: $c^* \leftarrow \mathsf{Enc}(\mathrm{pk}, m_1)$ | $\xrightarrow{\ c^*\ }$ | |
> | 4 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}_b(\mathcal A)$, the bit $b'$ in Game $b$.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}_1(\mathcal A) = 1]$ are.
>
> ---
> ### Property
> $\mathsf{Adv}(\mathcal A) = \big|\Pr[\mathsf{Expt}_0(\mathcal A) = 1] - \Pr[\mathsf{Expt}_1(\mathcal A) = 1]\big|.$
> $\Pi$ is <name> if $\mathsf{Adv}(\mathcal A) \leq \varepsilon$ for every $\mathcal A \in \mathbb A$. A **search** game ($\Pr[\text{win}]$) or a **distinguishing** game ($|\Pr[G_0] - \Pr[G_1]|$) — see [[knowledge/cryptography/foundations/Security Game\|Security Game]].

## Variant

## Related                          ← grouped: Descendants · Instantiations · Constructions · Properties · Siblings
```

**Game form — an interaction, not an algorithm.** *Added 2026-10-14, unified 2026-10-19.* A security experiment is a conversation between a challenger and an adversary, so it is written as one: a table with the challenger on the left, the adversary on the right and the message between them (`→` challenger to adversary, `←` back), one row per step. Rules:
- **Follow the literature.** The game in a note is the game of its source, redrawn in this shape, and the source is cited on the line above the table. Where an older version of the note disagrees with the source, the source wins.
- **Two stateful interactive machines.** $\mathcal C$ and $\mathcal A$ are interactive machines that keep state: each remembers everything it received and computed in earlier rows, including its random tape. So the adversary's column never shows inputs — write "chooses $m_0, m_1$ …", "sends $\mathbf x$", "outputs a bit $b'$", never $b' \leftarrow \mathcal A(c^*)$ or $\mathcal A_\mathsf{find}(\mathrm{pk})$. There is one adversary and no phases; a source that splits $\mathcal A$ into $(\mathcal A_1, \mathcal A_2)$ or threads a `state` gets that in the note's literature remark. Stated once in [[knowledge/cryptography/foundations/Security Game\|Security Game]].
- **One equation per line.** In a cell, each assignment, sampling or update is its own line, separated by `<br>`; never chain two with `;`. The same outside the table: two displayed equations are two lines, and a condition with several equations is a list.
- **Branch only where the games differ.** A distinguishing game has one table and a cell with two lines, **Game 0** and **Game 1**: the real branch first, the simulated / challenge-$m_1$ / fake-oracle branch second. A reduction then reads as a step from Game $i$ to Game $i+1$, and the hybrid argument has names for its games.
- **The advantage is the difference**, $|\Pr[\mathsf{Expt}_0 = 1] - \Pr[\mathsf{Expt}_1 = 1]|$, not "the adversary guesses a hidden bit". The bit-guessing form $|\Pr[b' = b] - 1/2|$ is exactly half of it; mention that in a remark when a source uses it, and do not mix the two in one note.
- **A search game has one branch** (soundness, unforgeability, linear-only): the challenger's last row computes the winning conditions.
- **An oracle is a message.** A query is a pair of rows — the adversary sends, the challenger answers — marked "(repeated, adaptive, at most $q$ times)" when it repeats; the Access line says which answers are available.
- **Auxiliary algorithms sit in the row that calls them**: the simulator $\mathcal S$ in the cell where it produces the challenge, the extractor $\mathcal E$ in the challenger's row after the adversary has spoken.
- **The goal is a list.** *Revised 2026-10-19.* Under the table, `**Goal**` and one bullet per item. A distinguishing game: an **Output** bullet ($\mathsf{Expt}_b$ is the adversary's bit in Game $b$) and a **Measure** bullet (what is compared). A search game: "$\mathcal A$ wins iff" and one bullet per winning condition, saying whether all or any must hold — [[knowledge/cryptography/verifiable computing/property/Linear-Only Security\|Linear-Only Security]]. A tuple or a view: an **Output** bullet naming the random variable and a **Measure** bullet naming the distinguisher $D$, which then goes in Parameters — [[knowledge/cryptography/verifiable computing/property/Strictly Linear Targeted Malleability\|Strictly Linear Targeted Malleability]], [[knowledge/cryptography/verifiable computing/property/Zero Knowledge\|Zero Knowledge]]. The Property section only says how the goal is compared (a difference of probabilities, a probability, a distance between distributions).
- **Key generation is $\mathsf{KeyGen}$.** *Added 2026-10-19.* The house name for the algorithm that produces keys, whatever the source calls it ($\mathsf{Gen}$, $G$, $\mathsf{KG}$, $\mathsf{keygen}$, $\mathsf{KeyDer}$); the source's name goes in the literature remark. $\mathsf{Setup}$ stays $\mathsf{Setup}$ when it outputs public parameters or a master key from which $\mathsf{KeyGen}$ derives user keys ([[knowledge/cryptography/primitive/functional encryption/Functional Encryption\|Functional Encryption]], [[knowledge/cryptography/primitive/public-key encryption/Trace-and-Revoke Scheme\|Trace-and-Revoke Scheme]]).
- **Draw the notes in the same shape.** Worked examples: [[knowledge/cryptography/primitive/public-key encryption/property/Indistinguishability under Chosen-Plaintext Attack\|Indistinguishability under Chosen-Plaintext Attack]] (distinguishing, one challenge), [[knowledge/cryptography/primitive/functional encryption/Inner-Product Functional Encryption#IND-CPA\|Inner-Product Functional Encryption#IND-CPA]] (key queries on both sides of the challenge), [[knowledge/cryptography/primitive/public-key encryption/Trace-and-Revoke Scheme\|Trace-and-Revoke Scheme]] (a search game and a distinguishing game in one note).
- **A hybrid argument is one table per changed algorithm.** *Added 2026-10-23, from your draft of 2026-10-21.* Rows are the steps of the algorithm the games change (key generation, the challenge encryption), columns are the games, a cell says "same" where a step does not change, and the last row, **hop**, says what justifies the change from the previous column: *statistical* with the lemma, or the assumption. Columns that agree are merged ("Game 0 – 1"). Under the tables, one **Goal** for all games. Worked example: [[knowledge/cryptography/primitive/functional encryption/scheme/Bounded-Collusion LWE Inner-Product FE#Security\|Bounded-Collusion LWE Inner-Product FE#Security]].
- **A reduction is a three-machine table.** *Added 2026-10-23, from your draft of 2026-10-19.* Columns: the outer challenger (of the assumption or the building block), the reduction $\mathcal B$, the adversary $\mathcal A$, with the messages between neighbours. $\mathcal B$'s checks — when it aborts, why its challenge is admissible — follow as a table or a list, and then the computation of its advantage. Worked examples: [[knowledge/cryptography/primitive/public-key encryption/Trace-and-Revoke from Inner-Product FE#Proof of Theorem 16\|Trace-and-Revoke from Inner-Product FE#Proof of Theorem 16]], [[knowledge/cryptography/verifiable computing/commitment/scheme/Pedersen Commitment#Binding\|Pedersen Commitment#Binding]].

**Access is the one general knob.** [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption Scheme\|Public-Key Encryption Scheme]] parameterises it — $\mathsf{atk} \in \{\mathsf{cpa}, \mathsf{lta}, \mathsf{cca}\}$ selects which oracles the adversary has before and after the challenge — and a proof system's response map is the same slot under another name.

Those four Condition lines are not a wish list: **each one is a place something broke.** Access → an adversary handed the *real* state in a simulated branch. Promise → completeness confused with soundness. Quantifier → a simulator with no $\exists$. Adaptivity → a non-adaptive model written adaptively.

**No game where the source has none.** *Added 2026-10-20.* Completeness and correctness, and soundness or knowledge against a *fixed* cheating strategy (a proof vector $\boldsymbol\pi^*$, a deterministic prover $\mathcal P'$), are quantified statements in the literature, not interactions: write them as the source does — the quantifiers first, one displayed equation per line, and the sampling steps as a list under "where" — [[knowledge/cryptography/verifiable computing/proof system/oracle/Linear Probabilistically Checkable Proofs\|Linear Probabilistically Checkable Proofs]], [[knowledge/cryptography/verifiable computing/proof system/interactive/Interactive Proof Systems\|Interactive Proof Systems]], [[knowledge/cryptography/primitive/vector encryption/Vector Encryption#Additive homomorphism\|Vector Encryption#Additive homomorphism]]. A correctness notion that the source does define with an adversary (a scheduler choosing inputs) is drawn as a game — [[knowledge/cryptography/primitive/key establishment/key exchange/Bidirectional Ratcheted Key Exchange\|Bidirectional Ratcheted Key Exchange]].

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

**A named theorem says what it states.** *Added 2026-10-19.* After the name in the callout title, a few words state the result: `> [!theorem] Banach fixed-point theorem — a contraction has exactly one fixed point`. Where the theorem is only mentioned — a list, a MOC line, a Related bullet — the same few words follow the name. The name says who proved it; the few words say when to reach for it. Examples: [[knowledge/math/property/map/Contraction\|Contraction]], [[knowledge/math/algebra/structures/action/Group Representation\|Group Representation]], [[knowledge/math/measure theory/Iterated Function System\|Iterated Function System]], [[knowledge/math/algebra/structures/ring/example/Hecke Algebra\|Hecke Algebra]].

**A theorem inside an object's note — Scope and Property, line by line.** *Added 2026-10-29, on your instruction.* A `[!theorem]`, `[!proposition]`, `[!lemma]` or `[!corollary]` that stays inside the note of its object (it has not graduated) uses the same two words as a theorem note, as bold labels:

```markdown
> [!theorem] <Name> — <a few words that state it>
> **Scope**
> - $\Lambda$: a lattice of rank $n$, with dual $\Lambda^*$.     ← one hypothesis per line, typed and linked
> - $\epsilon \in (0, 1)$.                                    ← a side condition is a line of its own
>
> ---
> **Property**
> $1 \leq \lambda_i(\Lambda) \cdot \lambda_{n-i+1}(\Lambda^*),$   ← one relation per line
> $\lambda_i(\Lambda) \cdot \lambda_{n-i+1}(\Lambda^*) \leq n.$
>
> `[<source and number>]`
```

- **Scope is a list, never a sentence.** No "Let $L$ be a lattice of dimension $n$ and let …": each object the statement uses gets its own bullet with its type. A symbol declared in the note's `Parameters` callout is still listed, so the statement can be read alone.
- **Property is one relation per line.** A two-sided bound or a chain $a = b \leq c$ is two lines. An existential gets a short lead-in and a bullet per condition (*there is a matrix $U$ with* — $U \in \mathbb Z^{n \times n}$; $B' = BU$; $\det U = \pm 1$). An equivalence is one line. Prose comes after the relations, and only for a consequence ("Hence $\det L$ does not depend on $\mathcal F$").
- **Bold labels, not headings.** A note can hold ten such statements, and `### Scope` headings would flood its outline; a graduated theorem note keeps the `###` headings and its `### Condition` section.
- **Citation last**, on its own line under Property; notes on the source (a misprint, a stronger hypothesis elsewhere, a `⚠️ CLAUDE – verify:`) follow it.
- **The same discipline as a quantified security statement** (§ 10, *No game where the source has none*): the quantified objects first, one per line, then the displayed result.
- **Definitions do not restate their Parameters.** Under a `Parameters` callout, the definition body starts with the term defined, not with "Let …".

Worked example: [[knowledge/math/algebra/structures/lattice/Lattices\|Lattices]] (§ Property).

> [!remark] Which note owns a two-hypothesis theorem?
> **The one it says the most about — and you find that out by sharpening it until only one hypothesis is
> doing work.** *"A Boolean integral domain is $\mathbb Z/2\mathbb Z$"* sharpens to *"in a Boolean ring every element
> but $0$ and $1$ is a zero divisor"*, which mentions domains not at all — so it belongs to [[knowledge/math/algebra/structures/ring/special ring/Boolean Ring\|Boolean Ring]],
> with a one-line pointer from [[knowledge/math/algebra/structures/ring/special ring/Integral Domain\|Integral Domain]]. When sharpening does **not** collapse it, the two
> hypotheses genuinely fight, and what you have is a pair of mixins whose conjunction is degenerate.

> [!remark] Axiom or theorem — same layout, different consumption site
> The difference is epistemic, not structural, and it shows in *where the link comes from*: an **axiom** is
> linked from a `## Definition` (you stipulate it), a **theorem** from a `## Property` or `## Security`
> (you derive it). That keeps precision rule 3 — *definition ≠ theorem* — intact while letting both share
> the Scope / Condition / Property skeleton.

---

## 13 · Machine — a computing model

```markdown
Reference:

## Definition

> [!definition] <Name>
> Generalizes:: [[<base machine>]]        ← or Extends:: — run the direction test
>
> ---
> <the full tuple, or the delta: "rule 4 is now $\delta: \dots$">

> [!definition] <Name> (Abstract Machine Formulation)      ← optional
> - Configuration $C$ · $\mathsf{init}(w)$ · $\mathsf{acc}$
> - the step relation $\vdash$

## Property

> [!theorem]
> <equivalence with the base machine>
> ---
> <the simulation cost — this is the content>

## Variant

| variant | $\delta$ | simulation cost |

## Related
```

**Acceptance is existential.** $M$ accepts $w$ iff $\exists c \in \mathsf{acc}$ with $\mathsf{init}(w) \vdash^* c$ — in every model, including the deterministic ones. The collapsed reading ("*the* run ends in $\mathsf{acc}$") is a `[!remark]` under determinism, never the definition; writing it as the definition excludes NFA, PDA and NTM.

**The simulation-cost column is the point.** Equivalence makes the model arbitrary for computability; the cost makes it *not* arbitrary for complexity. A variant table without costs has thrown away its reason to exist.

**Resource bounds do not belong here.** A machine whose definition contains "runs in time polynomial in $|x|$" is a complexity object — see 14 and the protocol remark in 6.

## 14 · Generator — a parameterised class family

```markdown
Reference:

## Definition

> [!definition] Class <NAME>
> A [[Language]] $\mathcal L \in \mathsf{NAME}(f(n))$ if there is a constant $c$ and a
> [[<machine>]] $M$ deciding $\mathcal L$ that <resource bound with $c \cdot f(n)$>.

## Property

> [!theorem] <Name> Hierarchy Theorem
> If $f, g$ are [[Computable Function|<Time/Space>-Constructible]] and <gap condition>, then
> $\mathsf{NAME}(f(n)) \subsetneq \mathsf{NAME}(g(n))$

## Related
```

**Three things a generator must name and usually doesn't.**
The **machine** by link — and the right one: space generators take [[knowledge/computability/computing model/turing machine/Offline Turing Machine\|Offline Turing Machine]], because charging for the input tape makes $\mathsf{SPACE}(\log n)$ empty.
The **constructibility hypothesis** — without it the hierarchy theorems are false, not merely unproven.
**$\subsetneq$, not $\subseteq$** — a hierarchy theorem written with $\subseteq$ is trivially true and its hypothesis does no work.

## 15 · Complexity class — one named class

```markdown
Reference:

## Definition

> [!definition] Class <NAME>
> Requires:: [[Class <GENERATOR>]]
>
> ---
> $\mathsf{NAME} = \bigcup_{c} \mathsf{GENERATOR}(n^c)$

> [!definition] Class <NAME> (machine form)        ← optional unfolding

## Property

### Relation with Other Classes

> [!proposition]
> Requires:: [[Class <other>]]
>
> ---
> <the inclusion or equality, and the theorem that proves it>

## Member

## Related
```

**A class is defined from its generator, never from scratch.** If the definition restates a machine and a bound, it is a generator wearing a class's name.

**`## Member` is a pointer, not a list.** Membership lives on the problem note as `Member of::` / `Complete for::`, so this section is a Dataview query or a handful of links — duplicating it by hand is how `np/` and `np-complete/` came to disagree.

**Uniformity is part of the definition** for circuit classes. $\mathsf{NC}^d$ over a plain [[knowledge/complexity/circuit/Circuit Family\|Circuit Family]] is the *non-uniform* class; $\mathsf{NC}^1 \subseteq \mathsf L$ needs [[knowledge/complexity/circuit/Log-Space Uniform Circuit Family\|Log-Space Uniform Circuit Family]]. Name which one.

---

## Slot glossary

| slot | holds | never holds |
| --- | --- | --- |
| `## Intuition` | the friendly reading, for sharing | anything the skeleton depends on |
| `## Definition` | what you must **stipulate** | consequences |
| `## Syntax` | the tuple, the spaces, one line per algorithm | any bound, any adversary |
| `[!definition] Parameters` | the variables the next definition uses: new ones, and `Import` lines for symbols another note declares | building blocks, anything with a definition of its own |
| `[!definition] Building Blocks` | other objects the next definition calls | variables |
| `## Scheme` | Setting, Parameters, Building Blocks, Algorithms | correctness, security |
| `## Property` | what holds **unconditionally** — provable without an adversary | anything with $\mathcal A$ in it |
| `## Security` | games and bounds — what holds **against someone** | attacks |
| `## Cryptanalysis` | concrete attacks, broken parameters, history | definitions |
| `## Variant` | same object, different scope | a different object |
| `## Example` | instances, **and counterexamples** | theory |
| `## Related` | links out, grouped by kind: Descendants, Instantiations, Constructions, Properties, Siblings, Prerequisites | content |

## Callout types

`definition` · `theorem` · `proposition` · `lemma` · `corollary` · `remark` · `example` · `property` · `security` · `scheme` · `algorithm` · `pseudocode` (CLRS-style code) · `construction` · `question` · `conjecture` · `principle` · `proof` · `todo`

Two are styled and unused — start using them: **`[!intuition]`** for the `## Intuition` section, **`[!attack]`** for `## Cryptanalysis`.

## Where the reasoning lives

- [[North Star\|North Star]] — the five kinds of note, the precision skeleton, two views, class/instance
- [[Foundation Layer\|Foundation Layer]] — the `math/` spine, axiom inventory, note drafts
- [[Cryptography Layer\|Cryptography Layer]] — interface/instance, scheme settings, party views, the game properties
