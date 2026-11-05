---
{"dg-publish":true,"permalink":"/knowledge/math/property/math-properties-moc/","dg-note-properties":{}}
---

# Math Properties MOC

Index for `math/property/` — the axiom library.

Every note here states **one** property, in one place, in the same shape. Structures elsewhere in the vault are then defined by *linking* to these rather than restating them: a [[knowledge/math/algebra/structures/group/Group\|group]] is a set with an operation satisfying [[knowledge/math/property/operation/Associativity\|Associativity]] + [[knowledge/math/property/operation/Identity Element\|Identity Element]] + [[knowledge/math/property/operation/Inverse Element\|Inverse Element]], and nothing about associativity is written twice.

The library is deliberately **not** under `algebra/` — relation axioms are order theory, metric axioms are analysis, and `information theory/coding theory/` needs the metric axioms too.

## The pattern

Every structure in the vault has the same three parts: a **carrier**, some **added data** on it, and **axioms** the data must satisfy. What differs between the four subfolders below is only the *type* of the added data — which is exactly what each note's **Scope** line records.

| structure | carrier | added data | type of the data | axiom family |
| --- | --- | --- | --- | --- |
| [[knowledge/math/algebra/structures/Magma\|Magma]] → [[knowledge/math/algebra/structures/group/Group\|Group]] | $S$ | $\star$ | function $S \times S \to S$ | `operation/` |
| [[knowledge/math/set theory/relation/Preorder\|Preorder]] → [[knowledge/math/set theory/relation/Total Order\|Total Order]] | $S$ | $\leq$ | subset $\subseteq S \times S$ | `relation/` |
| set → metric space | $X$ | $d$ | function $X \times X \to \mathbb R$ | `metric/` |
| [[knowledge/math/algebra/linear algebra/Vector Spaces\|vector space]] → normed space | $V$ | $\lVert \cdot \rVert$ | function $V \to \mathbb R$ | `metric/`, norm forms |
| homomorphism, pairing | $A, B$ | $f$ | function $A \to B$ | `map/` |
| [[knowledge/math/algebra/category/Category\|Category]] | $\mathsf{Obj}$ | $\mathsf{Hom}, \circ$ | **partial** function | `operation/`, read per composable triple |

So an ordered set $(S, \leq)$ is the same *kind* of thing as a group $(S, \star)$ — a carrier with data and axioms. Order theory is not a different pattern; it is this pattern with a relation in the data slot instead of an operation.

> [!remark] Where a genuinely different family appears
> **Compatibility axioms.** An *ordered group* or *ordered field* carries an operation **and** an order, plus axioms linking them — $a \leq b \Rightarrow a + c \leq b + c$, and $0 \leq a, 0 \leq b \Rightarrow 0 \leq ab$. Those constrain the *interaction*, so they belong to neither `operation/` nor `relation/`. The vault already depends on them: [[knowledge/math/property/metric/Positive Definiteness\|Positive Definiteness]] writes $\lVert x \rVert \geq 0$ and [[knowledge/math/property/metric/Triangle Inequality\|Triangle Inequality]] writes $\leq$, both presupposing that $\mathbb R$ is an ordered field. A `property/compatibility/` folder is the place for these when they are needed.

> [!remark] Where the two families merge
> An **order-theoretic lattice** is simultaneously a [[knowledge/math/set theory/relation/Partial Order\|poset]] with meets and joins, *and* an algebraic structure with two [[knowledge/math/property/operation/Idempotence\|idempotent]], [[knowledge/math/property/operation/Commutativity\|commutative]], [[knowledge/math/property/operation/Associativity\|associative]] operations satisfying absorption — the two definitions are equivalent. It is the cleanest demonstration that operation axioms and relation axioms describe one thing from two sides. *(Name it `Lattice (Order Theory).md` when it exists — [[knowledge/math/algebra/structures/lattice/Lattices\|Lattices]] here is the geometric object.)*

## Convention

Each note is a single `[!definition]` callout with the same three parts:

| part | holds |
| --- | --- |
| **Scope** | the typed object the property applies to |
| **Condition** | preconditions on that object, when there are any (module / vector-space structure, an identity element) — omitted otherwise |
| **Property** | the quantified statement, and nothing else |

Consequences do **not** live here. "Inverses are unique" is a theorem of associativity and belongs in [[knowledge/math/algebra/structures/group/Group\|Group]]; this library states only what is assumed.

A **property** is what an object may have; an **axiom** is a property a definition chooses to require. These notes state properties — [[knowledge/math/algebra/structures/group/special group/Abelian Group\|Abelian Group]] is what turns [[knowledge/math/property/operation/Commutativity\|Commutativity]] into an axiom. That is why the folder is `property/` and not `axiom/`, and why `verifiable computing/property/` on the cryptography side follows the same shape.

## Operation axioms

Scope: a binary operation $\star: O \times O \to O$.

- [[knowledge/math/property/operation/Closure\|Closure]] — a subset $A \subseteq O$ is closed under $\star$
- [[knowledge/math/property/operation/Associativity\|Associativity]]
- [[knowledge/math/property/operation/Commutativity\|Commutativity]]
- [[knowledge/math/property/operation/Identity Element\|Identity Element]]
- [[knowledge/math/property/operation/Inverse Element\|Inverse Element]]
- [[knowledge/math/property/operation/Distributivity\|Distributivity]] — the one two-operation axiom
- [[knowledge/math/property/operation/Idempotence\|Idempotence]]
- [[knowledge/math/property/operation/Absorption\|Absorption]] — the two-operation law $a \wedge (a \vee b) = a$ of lattices and Boolean algebras
- [[knowledge/math/property/operation/Alternativity\|Alternativity]] — left / right alternative; weaker than associativity, satisfied by the octonions

Structures: [[knowledge/math/algebra/structures/Magma\|Magma]] → [[knowledge/math/algebra/structures/Semigroup\|Semigroup]] → [[knowledge/math/algebra/structures/Monoid\|Monoid]] → [[knowledge/math/algebra/structures/group/Group\|Group]] → [[knowledge/math/algebra/structures/group/special group/Abelian Group\|Abelian Group]] → [[knowledge/math/algebra/structures/ring/Ring\|Ring]] → [[knowledge/math/algebra/structures/ring/special ring/Commutative Ring\|Commutative Ring]] → [[knowledge/math/algebra/structures/field/Field\|Field]]. The closure table lives in [[knowledge/math/algebra/Algebra MOC\|Algebra MOC]], with the structures it indexes.

## Relation axioms

Scope: a relation $R \subseteq O \times O$.

- [[knowledge/math/property/relation/Reflexivity\|Reflexivity]]
- [[knowledge/math/property/relation/Symmetry\|Symmetry]]
- [[knowledge/math/property/relation/Antisymmetry\|Antisymmetry]]
- [[knowledge/math/property/relation/Transitivity\|Transitivity]]
- [[knowledge/math/property/relation/Connexity\|Connexity]]

|  | reflexive | symmetric | antisymmetric | transitive | total |
| --- | :-: | :-: | :-: | :-: | :-: |
| [[knowledge/math/set theory/relation/Preorder\|preorder]] | ✓ |  |  | ✓ |  |
| [[knowledge/math/set theory/relation/Partial Order\|partial order]] | ✓ |  | ✓ | ✓ |  |
| [[knowledge/math/set theory/relation/Total Order\|total order]] | (✓) |  | ✓ | ✓ | ✓ |
| [[knowledge/math/set theory/relation/Equivalence Relation\|equivalence]] | ✓ | ✓ |  | ✓ |  |

> [!remark] The parenthesised tick
> [[knowledge/math/property/relation/Connexity\|Connexity]] as stated — $\forall x, y: (x \, R \, y) \lor (y \, R \, x)$ — **implies** [[knowledge/math/property/relation/Reflexivity\|Reflexivity]]: take $y = x$. So a total order needs only totality, antisymmetry and transitivity; reflexivity comes free. The tick is kept for readability against the rows above, but it is derived, not assumed.

The structures live with the objects, in `set theory/relation/`: [[knowledge/math/set theory/relation/Relation\|Relation]], [[knowledge/math/set theory/relation/Preorder\|Preorder]], [[knowledge/math/set theory/relation/Partial Order\|Partial Order]], [[knowledge/math/set theory/relation/Total Order\|Total Order]], [[knowledge/math/set theory/relation/Equivalence Relation\|Equivalence Relation]], [[knowledge/math/set theory/relation/Quotient Relation\|Quotient Relation]].

> [!remark] Orders as categories
> A [[knowledge/math/set theory/relation/Preorder\|preorder]] is exactly a **thin category** — objects are the elements, and there is one morphism $a \to b$ precisely when $a \leq b$. Reflexivity gives the identity morphisms, transitivity gives composition. See `example/Poset as Category.md`.

## Map axioms

Scope: a map between structured sets.

- [[knowledge/math/property/map/Linearity\|Linearity]] — preserves addition and scalar multiplication
- [[knowledge/math/property/map/Bilinearity\|Bilinearity]] — linear in each argument separately
- [[knowledge/math/property/map/Multilinearity\|Multilinearity]] — the $k$-argument generalisation
- [[knowledge/math/property/map/Map Symmetry\|Map Symmetry]] — $f(x, y) = f(y, x)$; the *form* sense, distinct from relation [[knowledge/math/property/relation/Symmetry\|Symmetry]]
- [[knowledge/math/property/map/Homomorphism\|Homomorphism]] — preserves every operation of a shared signature; the general case that [[knowledge/math/property/map/Linearity\|Linearity]] specialises
- [[knowledge/math/property/map/Monotonicity\|Monotonicity]] — preserves order; the [[knowledge/math/set theory/relation/Preorder\|order]] family's structure-preserving map
- [[knowledge/math/property/map/Injection\|Injection]] · [[knowledge/math/property/map/Surjection\|Surjection]] · [[knowledge/math/property/map/Bijection\|Bijection]] — the cardinality properties
- [[knowledge/math/property/map/Involution\|Involution]] — $f \circ f = \mathrm{id}$
- [[knowledge/math/property/map/Lipschitz Map\|Lipschitz Map]] — stretches distances by at most the constant $\mathrm{Lip}\, F$; [[knowledge/math/property/map/Contraction\|Contraction]] is the case $\mathrm{Lip}\, F < 1$, with the Banach fixed-point theorem (a contraction has exactly one fixed point)

Consumers: [[knowledge/math/algebra/linear algebra/Linear Maps\|Linear Maps]], [[knowledge/math/algebra/structures/elliptic curve/Bilinear Pairings\|Bilinear Pairings]], [[knowledge/math/algebra/linear algebra/Kronecker Product\|Kronecker Product]], [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]], [[knowledge/cryptography/verifiable computing/relation/r1cs/Split-R1CS\|Split-R1CS]], [[knowledge/math/set theory/Function\|Function]], [[knowledge/math/algebra/structures/group/subgroup/Subgroup\|Subgroup]].

> [!remark] One structure-preserving map per family
> Algebra has [[knowledge/math/property/map/Homomorphism\|homomorphisms]], orders have [[knowledge/math/property/map/Monotonicity\|monotone maps]], categories have functors. A [[knowledge/math/algebra/category/Morphism\|morphism]] is *not* one of these: it is an arrow in an abstract [[knowledge/math/algebra/category/Category\|Category]] and need not be a function at all. The two coincide only in a **concrete** category — which is what licenses [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]] to import [[knowledge/math/algebra/category/Morphism#Isomorphism\|iso]].

## Metric axioms

Scope: a function $d: X \times X \to \mathbb R$ on a set $X$ — or, for the norm forms, $N = \lVert \cdot \rVert : V \to \mathbb R$.

| axiom | metric form | norm form |
| --- | --- | --- |
| [[knowledge/math/property/metric/Positive Definiteness\|Positive Definiteness]] | $d(x,y) = 0 \iff x = y$ | $\lVert x \rVert = 0 \iff x = 0$ |
| [[knowledge/math/property/metric/Triangle Inequality\|Triangle Inequality]] | $d(x,z) \leq d(x,y) + d(y,z)$ | $\lVert x + y \rVert \leq \lVert x \rVert + \lVert y \rVert$ |
| [[knowledge/math/property/metric/Distance Symmetry\|Distance Symmetry]] | $d(x,y) = d(y,x)$ | — *automatic* |
| [[knowledge/math/property/metric/Homogeneity\|Homogeneity]] | — | $\lVert \alpha x \rVert = \lvert \alpha \rvert \lVert x \rVert$ |

A function satisfying the first three is a **metric**; one satisfying positive definiteness, the triangle inequality and homogeneity is a **norm**, and $d(x,y) = \lVert x - y \rVert$ makes every normed space a [[knowledge/math/calculus/Metric Space\|metric space]].

> [!remark] Homogeneity buys symmetry
> A norm needs no symmetry axiom: $d(y,x) = \lVert y - x \rVert = \lVert -(x-y) \rVert = \lVert x - y \rVert = d(x,y)$, by [[knowledge/math/property/metric/Homogeneity\|Homogeneity]] at $\alpha = -1$. That is the one axiom the metric family has and the norm family does not.

> [!remark] Non-negativity is a theorem
> $d(x,y) \geq 0$ is **not** an axiom — it follows from the other three: $0 = d(x,x) \leq d(x,y) + d(y,x) = 2\,d(x,y)$. It belongs in [[knowledge/math/calculus/Metric Space\|Metric Space]] as a proposition, never inside a definition callout.

Consumers: [[knowledge/math/calculus/Metric Space\|Metric Space]], [[knowledge/math/algebra/linear algebra/Inner-Product Spaces\|Inner-Product Spaces]], [[knowledge/math/algebra/structures/lattice/Lattices\|Lattices]] and everything under `structures/lattice/`, and — the reason this library is not under `algebra/` — [[knowledge/information theory/coding theory/Code Distance\|Code Distance]], [[knowledge/information theory/coding theory/rank-metric/Rank Metric Codes\|Rank Metric Codes]], and [[knowledge/math/probability/Statistical Distance\|Statistical Distance]], since total variation distance is itself a metric.

## Related

- [[knowledge/math/algebra/Algebra MOC\|Algebra MOC]] — the structures these axioms compose into
- [[knowledge/math/set theory/Set\|Set]] — the algebra of $\cup$ / $\cap$ is an *instance* of [[knowledge/math/property/operation/Commutativity\|Commutativity]], [[knowledge/math/property/operation/Associativity\|Associativity]], [[knowledge/math/property/operation/Distributivity\|Distributivity]], not a restatement
- [[knowledge/math/algebra/category/Category\|Category]] — its axioms are [[knowledge/math/property/operation/Associativity\|Associativity]] and [[knowledge/math/property/operation/Identity Element\|Identity Element]] for a **partial** composition, one identity per object
