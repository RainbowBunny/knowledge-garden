---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof/interactive/interactive-proof-systems/","dg-note-properties":{}}
---

Reference: https://people.cs.georgetown.edu/jthaler/ProofsArgsAndZK.pdf
## Syntax

> [!definition] Interactive Proof System
> Given a function $f$ mapping $\{0, 1\}^n$ to a finite range $\mathcal R$, a $k$-message **interactive proof system** ($\text{IP}$) for $f$ consists of a probabilistic verifier algorithm $\mathcal V$ running in time $\text{poly}(n)$ and a prescribed ("honest") deterministic prover algorithm $\mathcal P$:
> - Both $\mathcal V$ and $\mathcal P$ are given a common input $x \in \{0, 1\}^n$, and at the start of the protocol $\mathcal P$ provides a value $y$ claimed to equal $f(x)$.
> - Then $\mathcal P$ and $\mathcal V$ exchange a sequence of messages $m_1, m_2, \dots, m_k$ that are determined as follows:
> 	- The $\text{IP}$ designates one of the parties, either $\mathcal P$ and $\mathcal V$, to send the first message $m_1$.
> 	- The party sending each message alternates, meaning for example that if $\mathcal V$ sends $m_1$, then $\mathcal P$ sends $m_2$, $\mathcal V$ sends $m_3$, $\mathcal P$ sends $m_4$, and so on.
> - Both $\mathcal P$ and $\mathcal V$ are thought of as "next-message-computing algorithms", meaning that when it is $\mathcal V$'s (respectively, $\mathcal P$'s) turn to send a message $m_i$, $\mathcal V$ (respectively, $\mathcal P$) is run on input $(x, m_1, m_2, \dots, m_{i - 1})$ to produce message $m_i$.
> - The entire sequence of $k$ messages $t = (m_1, m_2, \dots, m_k)$ exchanged by $\mathcal P$ and $\mathcal V$, along with the claimed answer $y$, is called a **transcript**.
> - At the end of the protocol, $\mathcal V$ must output either **accept** or **reject** for the prover's claim that $y = f(x)$. The value output by the verifier at the end of the protocol may depend on both the transcript $t$ and the verifier's internal randomness.
> - Denote by $\text{out}(\mathcal V, x, r, \mathcal P) \in \{\text{accept}, \text{reject}\}$ the output of verifier $\mathcal V$ on input $x$ when interacting with deterministic prover strategy $\mathcal P$, with $\mathcal V$'s internal randomness equal to $r$. For any fixed value $r$ of $\mathcal V$'s internal randomness, $\text{out}(\mathcal V, x, r, \mathcal P)$ is a deterministic function of $x$.

## Property

### Completeness

> [!definition] Completeness Error
> An interactive proof system $(\mathcal P, \mathcal V)$ is said to have **completeness error** $\delta_c$ if:
> - For every $x \in \{0, 1\}^n$,
> $$\mathsf{Adv}_{\mathcal V}^\text{com}(\mathcal P) = 
> \; \Pr\!\left[
> \begin{array}{l}
> \text{out}(\mathcal V, x, r, \mathcal P) = \text{accept}
> \end{array}
> \; \middle | \; 
> \begin{array}{l}
> x \xleftarrow{\$} \{0, 1\}^n
> \end{array} \right] \geq 1 - \delta_c$$

> [!remark]
> The completeness condition requires that there be a convincing proof for what is the value of $f$ on input $x$.

> [!remark]
> When $\delta_c = 0$, we call this property **perfect completeness**.

## Security

### Soundness

> [!definition] Soundness Error
> An interactive proof system $(\mathcal V, \mathcal P)$ is said to have **soundness error** $\varepsilon_{\mathsf{snd}}$ if for every deterministic prover strategy $\mathcal P'$:
> $$\mathsf{Adv}_{\mathcal V}^\mathsf{snd}(\mathcal P') = 
> \; \Pr\!\left[
> \begin{array}{l}
> y \neq f(x) \\
> \text{out}(\mathcal V, x, r, \mathcal P') = \text{accept}
> \end{array}
> \; \middle | \; 
> \begin{array}{l}
> x \xleftarrow{\$} \{0, 1\}^n \\
> y \leftarrow \mathcal P'()
> \end{array} \right] \leq \varepsilon_{\mathsf{snd}}$$

> [!remark]
> The soundness condition requires that false statement of the form "$f(x) = y$" for any $y \neq f(x)$ lack a convincing proof.

> [!remark]
> - As the prover computing power is unbounded, we often refer this property as **statistical soundness** or **information-theoretic soundness**.
> - If the prover computing power is bounded, we call the property **computationally soundness**.

### Knowledge Soundness

> [!definition] Knowledge Soundness
> An interactive prove $\Pi = (\mathcal P, \mathcal V)$ is knowledge sound for an [[knowledge/cryptography/verifiable computing/relations/Effective Relation\|Effective Relation]] $R$ if there exists an efficient [[Knowledge Extractor\|Knowledge Extractor]] $\mathcal E$, such that for all $(x, w) \in R$ and all provers $\mathcal P'$, we have
> $$\mathsf{Adv}_{\mathcal V}^{\mathsf{ks}}(\mathcal P') = \mathsf{Adv}_{\mathcal V}^{\mathsf{com}}(\mathcal P') - \Pr[(x, w') \in R \;|\; w' \leftarrow \mathcal E^{\mathcal P'}(x)]$$

> [!remark]
> Knowledge soundness condition requires that not only a witness exists but also the prover need to know one witness $w$.

> [!remark]
> To prove this knowledge soundness, we need to construct a [[Knowledge Extractor\|Knowledge Extractor]].

> [!remark] Of Knowledge
> Proof of Knowledge or Argument of Knowledge mean that the system satisfies knowledge soundness.

### Zero Knowledge

> [!definition] Zero Knowledge
> A proof system with prescribed prover $\mathcal P$ and prescribed verifier $\mathcal V$ for a language $\mathcal L$ is said to be zero-knowledge if for any [[daily/Temp/PPT\|daily/Temp/PPT]] time verifier strategy $\hat{\mathcal V}$, there exists a PPT algorithm $S$ (which can depend on $\hat{\mathcal V}$), called the simulator, such that for all $x \in \mathcal L$, the distribution of the output $S(x)$ of the simulator is "[[knowledge/cryptography/foundations/Indistinguishability#Definition\|Indistinguishable]]" from $\text{View}_\hat{\mathcal V}(\mathcal P(x), \hat{\mathcal V}(x))$. Here, $\text{View}_\hat{\mathcal V}(\mathcal P(x), \hat{\mathcal V}(x))$ denotes the distribution over transcripts generated by the interaction of prover strategies $\mathcal P$ and verifier strategy $\hat{\mathcal V}$ within the proof or argument system.

> [!remark]
> If the distribution is perfect (statistical, computational), then the proof system is perfect (statistical, computational) zero knowledge.

### Honest Verifier Zero Knowledge

> [!remark]
> Zero knowledge but now we only consider $S(x)$ and $\text{View}_{\mathcal V}(\mathcal P(x), \mathcal V(x))$.

