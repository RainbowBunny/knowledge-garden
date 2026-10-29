---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof-system/interactive/interactive-proof-systems/","dg-note-properties":{}}
---

Reference: 
- `[Thaler]` — J. Thaler, _Proofs, Arguments, and Zero-Knowledge_: https://people.cs.georgetown.edu/jthaler/ProofsArgsAndZK.pdf
- [[academic/Book Reference\|Computational Complexity: A Modern Approach]]: - Chapter 8: Interactive Proofs.

> [!remark] Goldwasser, Micali, Rackoff 1985
> “What is intuitively required from a theorem-proving procedure? First, that it is possible to “prove” a true theorem. Second, that it is impossible to “prove” a false theorem. Third, that communicating the proof should be efficient, in the following sense. It does not matter how long must the prover compute during the proving process, but it is essential that the computation required from the verifier is easy.” 

## Syntax

> [!definition] Interactive Proof System
> Given a function $f$ mapping $\{0, 1\}^n$ to a finite range $\mathcal R$, a $k$-message **interactive proof system** ($\text{IP}$) for $f$ consists of a probabilistic verifier algorithm $\mathcal V$ running in time $\text{poly}(n)$ and a prescribed ("honest") deterministic prover algorithm $\mathcal P$:
> - Both $\mathcal V$ and $\mathcal P$ are given a common input $x \in \{0, 1\}^n$, and at the start of the protocol $\mathcal P$ provides a value $y$ claimed to equal $f(x)$.
> - Then $\mathcal P$ and $\mathcal V$ exchange a sequence of messages $m_1, m_2, \dots, m_k$ that are determined as follows:
> 	- The $\text{IP}$ designates one of the parties, either $\mathcal P$ and $\mathcal V$, to send the first message $m_1$.
> 	- The party sending each message alternates, meaning for example that if $\mathcal V$ sends $m_1$, then $\mathcal P$ sends $m_2$, $\mathcal V$ sends $m_3$, $\mathcal P$ sends $m_4$, and so on.
> - Both $\mathcal P$ and $\mathcal V$ are thought of as "next-message-computing algorithms", meaning that when it is $\mathcal V$'s (respectively, $\mathcal P$'s) turn to send a message $m_i$, $\mathcal V$ (respectively, $\mathcal P$) is run on input $(x, m_1, m_2, \dots, m_{i - 1})$ to produce message $m_i$.
> - The entire sequence of $k$ messages $t = (m_1, m_2, \dots, m_k)$ exchanged by $\mathcal P$ and $\mathcal V$, along with the claimed answer $y$, is called a **transcript**.
> - At the end of the protocol, $\mathcal V$ must output either $1$ (accept) or $0$ (reject) for the prover's claim that $y = f(x)$. The value output by the verifier at the end of the protocol may depend on both the transcript $t$ and the verifier's internal randomness.
> - Denote by $\mathrm{out}(\mathcal V, x, r, \mathcal P) \in \{0, 1\}$ the output of verifier $\mathcal V$ on input $x$ when interacting with deterministic prover strategy $\mathcal P$, with $\mathcal V$'s internal randomness equal to $r$. For any fixed value $r$ of $\mathcal V$'s internal randomness, $\text{out}(\mathcal V, x, r, \mathcal P)$ is a deterministic function of $x$.

## Property

### Completeness

> [!definition] Completeness Error
> Let $\mathrm{out}(\mathcal V, x, r, \mathcal P) \in \{0, 1\}$ be the output of $\mathcal V$ on input $x$ when interacting with the deterministic prover strategy $\mathcal P$, with $\mathcal V$'s internal randomness equal to $r$. $(\mathcal V, \mathcal P)$ has **completeness error** $\delta_c$ if for every $x \in \{0, 1\}^n$
> $$\Pr_r\big[\mathrm{out}(\mathcal V, x, r, \mathcal P) = 1\big] \geq 1 - \delta_c.$$
> `[Thaler Def 3.1]`

> [!remark] Perfect completeness
> $\delta_c = 0$. All the interactive proofs in `[Thaler]` have it `[Thaler §3.3]`.

## Security

### Soundness

> [!definition] Soundness Error
> $(\mathcal V, \mathcal P)$ has **soundness error** $\delta_s$ if for every $x \in \{0, 1\}^n$ and every deterministic prover strategy $\mathcal P'$: if $\mathcal P'$ sends a value $y \neq f(x)$ at the start of the protocol, then
> $$\Pr_r\big[\mathrm{out}(\mathcal V, x, r, \mathcal P') = 1\big] \leq \delta_s.$$
> `[Thaler Def 3.1]`

> [!remark] Valid, deterministic, unbounded
> - The system is **valid** if $\delta_c, \delta_s \leq 1/3$. `[Thaler §3.1]`
> - Restricting to deterministic provers loses no generality: a randomized prover is no more powerful. `[Thaler §3.1 fn. 22, §3.3]`
> - Soundness holds against every prover, however powerful: it is *statistical* (information-theoretic) soundness. Against polynomial-time provers only, the system is an *argument*. `[Thaler §3.2]`

### Knowledge Soundness

Proofs and arguments *of knowledge* add that a prover who convinces the verifier must know a witness, which an extractor recovers from it — see [[knowledge/cryptography/verifiable computing/property/Knowledge Soundness\|Knowledge Soundness]] and [[Knowledge Extractor\|Knowledge Extractor]].

### Zero Knowledge

> [!definition] Zero Knowledge
> A proof system with prescribed prover $\mathcal P$ and prescribed verifier $\mathcal V$ for a language $\mathcal L$ is said to be zero-knowledge if for any [[knowledge/cryptography/foundations/PPT\|PPT]] time verifier strategy $\hat{\mathcal V}$, there exists a PPT algorithm $S$ (which can depend on $\hat{\mathcal V}$), called the simulator, such that for all $x \in \mathcal L$, the distribution of the output $S(x)$ of the simulator is "[[knowledge/cryptography/foundations/Indistinguishability#Definition\|Indistinguishable]]" from $\text{View}_\hat{\mathcal V}(\mathcal P(x), \hat{\mathcal V}(x))$. Here, $\text{View}_\hat{\mathcal V}(\mathcal P(x), \hat{\mathcal V}(x))$ denotes the distribution over transcripts generated by the interaction of prover strategies $\mathcal P$ and verifier strategy $\hat{\mathcal V}$ within the proof or argument system.

> [!remark]
> If the distribution is perfect (statistical, computational), then the proof system is perfect (statistical, computational) zero knowledge.

### Honest Verifier Zero Knowledge

> [!remark]
> Zero knowledge but now we only consider $S(x)$ and $\text{View}_{\mathcal V}(\mathcal P(x), \mathcal V(x))$.

