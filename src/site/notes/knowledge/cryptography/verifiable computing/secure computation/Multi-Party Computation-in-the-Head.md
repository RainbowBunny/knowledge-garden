---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/secure-computation/multi-party-computation-in-the-head/","dg-note-properties":{}}
---

## Syntax

> [!definition] Parameters
> - $n$: Number of parties.
> - $P_1, \dots, P_n$: The $n$ parties, with each party $P_i$ holds:
> 	- $x$: Public input.
> 	- $w_i$: Its private input share.
> 	- $r_i$: Its private random.
> - $\{0, 1\} \leftarrow f(x; w_1, \dots, w_n)$: The common function.

> [!definition] Multi-Party Computation-in-the-Head
> An $n$-party protocol $\Pi = (\mathsf{Next}_i, \mathsf{Out}_i)_{i \in [n]}$ is specified by:
> - A next-message function. For each party, round $\rho$, the messages it sends are 
> $$\mathsf{Next}_i(x, w_i, r_i, m_i^{(1)}, \dots, m_i^{(\rho - 1)})$$
> where $r_i$ is $P_i$'s random and $m_i^{(k)}$ is everything it received in round $k$.
> - An output function $\mathsf{Out}_i$ applied at the end to $\mathsf{View}_i$.

> [!remark] View of Each Party in MPC
> For each party, the view of party $i$ in round $\rho$ is:
> $$\mathsf{View}_i = (x, w_i, r_i, m_i^{(1)}, \dots, m_i^{(\rho)})$$

