---
{"dg-publish":true,"permalink":"/knowledge/complexity/complexity-class/complexity-class/","dg-note-properties":{"aliases":["Decision Problem","Encoding"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 0: Notational conventions (representing objects as strings, decision problems as languages); Chapter 1: The computational model —and why it doesn’t matter, Section 1.2: The Turing Machine.
- `[Sip]` — M. Sipser, _Introduction to the Theory of Computation_ (edition not recorded), Chapter 7: Time Complexity, Section 7.1: Measuring Complexity.

# Complexity Class

Complexity theory studies **languages**, not "problems" in the informal sense. Every class note in this domain (P, NP, PSPACE, BPP, …) is a set of languages; this note fixes that formulation once, so the class notes can use it uniformly.

## Language Formulation

The alphabet / string / language definitions live in [[knowledge/computability/language/Language\|Language]]; Turing machines and deciders live in `computability/computing model/`.

> [!definition] Decision Problem as a Language
> A **decision problem** is a yes/no question about an input. Fixing an alphabet $\Sigma$ (usually $\{0, 1\}$), a decision problem is identified with the language $$L = \{w \in \Sigma^* \mid \text{the answer on } w \text{ is yes}\} \subseteq \Sigma^*,$$ and "solving the problem" means **deciding** $L$: a machine $M$ decides $L$ if $M$ halts on every input and accepts $w$ iff $w \in L$.

> [!definition] Encoding
> Objects other than strings (graphs, matrices, machine descriptions, tuples) enter a language via an **encoding** $\langle \cdot \rangle$ that maps the object to a string. We write, e.g., $$\text{PATH} = \{\langle G, s, t \rangle \mid G \text{ is a directed graph with a directed path from } s \text{ to } t\}.$$ Any reasonable (polynomially-related) encoding gives the same complexity classes, so the choice is left implicit.

> [!remark]
> 1. **Decision vs search**: the language formulation only captures yes/no questions. A **search problem** (produce a witness, not just decide existence) is formalized as a relation $R \subseteq \Sigma^* \times \Sigma^*$; for NP relations the two are polynomially equivalent via self-reducibility ([[knowledge/complexity/complexity class/class/time/Class NP#Property\|Class NP#Property]]).
> 2. **Promise problems** relax the requirement that every string is a yes- or no-instance: inputs are promised to lie in $\Pi_{\text{yes}} \cup \Pi_{\text{no}}$. Several randomized and interactive classes are more naturally promise classes.

## Complexity Class

> [!definition] Complexity Class
> A **complexity class** is a set of languages. The classes studied here are all specified by three choices:
> 1. A **machine model** (deterministic / nondeterministic / probabilistic TM, circuit family, verifier-prover pair),
> 2. A **resource bound** (time $t(n)$, space $f(n)$, circuit size/depth, number of rounds),
> 3. An **acceptance condition** (always correct, correct on some branch, correct with probability $\geq 2/3$, …).
>
> E.g. $\mathsf{DTIME}(t(n))$, $\mathsf{SPACE}(f(n))$, $\mathsf{BPP}$ are the sets of languages decided under the respective choices. The co-classes are in [[knowledge/complexity/complexity class/operator/Complement Class\|Complement Class]].

### Machine model

> [!remark] Which machine the classes are measured on
> Resource-bounded classes in `complexity/` are measured on the [[knowledge/computability/computing model/turing machine/Offline Turing Machine\|Offline Turing Machine]]: a read-only input tape, $k$ work tapes, and space counted on the work tapes only `[AB09 §1.2]`. `computability/` uses the single-tape [[knowledge/computability/computing model/turing machine/Turing Machine\|Turing Machine]].
>
> The **named** classes [[knowledge/complexity/complexity class/class/time/Class P\|Class P]], [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]], [[knowledge/complexity/complexity class/class/space/Class PSPACE\|Class PSPACE]], [[knowledge/complexity/complexity class/class/time/Class EXP\|Class EXP]] are model-robust. The **parameterised** classes [[knowledge/complexity/complexity class/generator/time/Class DTIME\|DTIME(t)]], [[knowledge/complexity/complexity class/generator/time/Class NTIME\|NTIME(t)]], [[knowledge/complexity/complexity class/generator/space/Class SPACE\|SPACE(s)]], [[knowledge/complexity/complexity class/generator/space/Class NSPACE\|NSPACE(s)]] are not: one tape instead of $k$ changes time by up to a square, and without a separate input tape sublinear space cannot be defined.

> [!theorem] Multitape to single tape — quadratic overhead
> **Scope**
> - $t(n) \geq n$.
>
> ---
> **Property**
> Every $t(n)$-time [[knowledge/computability/computing model/turing machine/Multitape Turing Machine\|Multitape Turing Machine]] has an equivalent $O(t^2(n))$-time single-tape Turing machine.
>
> `[Sip §7.1]`

## Efficient Algorithm

> [!definition] Polynomial-time Computable Function
> A function $f: \Sigma^{*} \rightarrow \Sigma^{*}$ is a **polynomial-time computable function** if some polynomial-time Turing machine $M$ exists that halts with just $f(w)$ on its tape, when started on any input $w$.

> [!definition] Efficient Algorithm (Cryptographic Convention)
> Let $A$ be an algorithm (possibly probabilistic) that takes as input a security parameter $\lambda \in \mathbb Z_{\geq 1}$, as well as other parameters encoded as a bit string $x \in \{0, 1\}^{p(\lambda)}$ for some fixed polynomial $p$. We call $A$ an **efficient algorithm** if there exist a poly-bounded function $t$ and a negligible function $\epsilon$ such that for all $\lambda \in \mathbb Z_{\geq 1}$, and all $x \in \{0, 1\}^{\leq p(\lambda)}$, the probability that the running time of $A$ on input $(\lambda, x)$ exceeds $t(\lambda)$ is at most $\epsilon(\lambda)$.

> [!remark]
> The second definition is the Boneh–Shoup convention used throughout `cryptography/` (running time measured in the security parameter, negligible slack allowed); see [[knowledge/cryptography/foundations/PPT\|PPT]] and [[knowledge/cryptography/foundations/Security Game\|Security Game]]. Complexity-theory notes use the plain "polynomial in the input length" convention, i.e. [[knowledge/complexity/randomized/Randomized Complexity#Probabilistic Polynomial Time (PPT)\|PPT]].

> [!definition] Reduction (Cryptographic Convention)
> Problem $A$ **reduces** to problem $B$, written $A \leq B$, if one can efficiently solve $A$ with non-negligible probability, given an algorithm that efficiently solves $B$ with non-negligible probability. This is the sense of "reduction" in security proofs; the complexity-theoretic reductions are [[knowledge/complexity/complexity class/reducibility/Polynomial-time Karp Reducibility\|Polynomial-time Karp Reducibility]] and [[knowledge/complexity/complexity class/reducibility/Log-space Reducibility\|Log-space Reducibility]].

## Class Inclusions

The standard inclusion chain among the major classes:

$$\mathsf L \subseteq \mathsf{NL} \subseteq \mathsf P \subseteq \mathsf{NP} \subseteq \mathsf{PSPACE} = \mathsf{NPSPACE} = \mathsf{IP} \subseteq \mathsf{EXP} \subseteq \mathsf{NEXP}$$

with the strict separations

$$\mathsf{NL} \subsetneq \mathsf{PSPACE} \subsetneq \mathsf{EXPSPACE}, \qquad \mathsf P \subsetneq \mathsf{EXP}, \qquad \mathsf{NP} \subsetneq \mathsf{NEXP}.$$

The strict separations come from the [[knowledge/complexity/theorem/Space Hierarchy Theorem\|Space Hierarchy Theorem]], the [[knowledge/complexity/theorem/Time Hierarchy Theorem\|Time Hierarchy Theorem]] and the [[knowledge/complexity/theorem/Nondeterministic Time Hierarchy Theorem\|Nondeterministic Time Hierarchy Theorem]]; $\mathsf{PSPACE} = \mathsf{NPSPACE}$ is Savitch's theorem ([[knowledge/complexity/theorem/Savitch's Theorem\|Savitch's Theorem]]), and $\mathsf{IP} = \mathsf{PSPACE}$ is Shamir's theorem ([[knowledge/complexity/complexity class/class/interactive/Class IP\|Class IP]]). Every inclusion in the first chain other than these two equalities is open.

## Related

- [[knowledge/computability/language/Language\|Language]] — alphabets, strings, languages (the raw material)
- [[knowledge/complexity/complexity class/reducibility/Polynomial-time Karp Reducibility\|Polynomial-time Karp Reducibility]], [[knowledge/complexity/complexity class/reducibility/Log-space Reducibility\|Log-space Reducibility]], [[knowledge/complexity/complexity class/operator/Hardness and Completeness\|Hardness and Completeness]] — how classes are compared
- [[knowledge/complexity/theorem/Time Hierarchy Theorem\|Time Hierarchy Theorem]], [[knowledge/complexity/theorem/Space Hierarchy Theorem\|Space Hierarchy Theorem]] — more resources, strictly more power
- [[knowledge/complexity/complexity class/generator/time/Class DTIME\|Class DTIME]], [[knowledge/complexity/complexity class/generator/space/Class SPACE\|Class SPACE]] — the canonical resource bounds
- [[knowledge/complexity/randomized/Randomized Complexity\|Randomized Complexity]] — what changes when the machine has access to random coins
