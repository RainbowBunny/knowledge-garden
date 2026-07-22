---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof/interactive-proof-systems/","dg-note-properties":{}}
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
> An interactive proof system $(\mathcal V, \mathcal P)$ is said to have **completeness error** $\delta_c$ if:
> - For every $x \in \{0, 1\}^n$,
> $$\Pr_r[\text{out}(\mathcal V, x, r, \mathcal P) = \text{accept}] \geq 1 - \delta_c$$


> [!remark]
> The completeness condition requires that there be a convincing proof for what is the value of $f$ on input $x$.

> [!remark]
> When $\delta_c = 0$, we call this property **perfect completeness**.

## Security

### Soundness

> [!definition] Soundness Error
> An interactive proof system $(\mathcal V, \mathcal P)$ is said to have **soundness error** $\delta_s$ if:
> - For every $x \in \{0, 1\}^n$ and every deterministic prover strategy $\mathcal P'$, if $\mathcal P'$ sends a value $y \neq f(x)$ at the start of the protocol, then
> $$\Pr_r[\text{out}(\mathcal V, x, r, \mathcal P') = \text{accept}] \leq \delta_s$$

> [!remark]
> The soundness condition requires that false statement of the form "$f(x) = y$" for any $y \neq f(x)$ lack a convincing proof.

> [!remark]
> - As the prover computing power is unbounded, we often refer this property as **statistical soundness** or **information-theoretic soundness**.
> - If the prover computing power is bounded, we call the property **computationally soundness**.
