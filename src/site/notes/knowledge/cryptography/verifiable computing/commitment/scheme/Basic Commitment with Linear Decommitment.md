---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/commitment/scheme/basic-commitment-with-linear-decommitment/","dg-note-properties":{}}
---

Reference:
- https://web.cs.ucla.edu/~rafail/PUBLIC/79.pdf
## Scheme

> [!scheme] Basic Commitment with Linear Decommitment
> ### Parameters
> - $n$: Dimension of finite field.
> - $\mathbb F$: Finite field.
> 
> ---
> ### Building Block
> - Homomorphic Encryption Scheme $E = (\text{Gen}, \text{Enc}, \text{Dec})$.
> 
> ---
> ### Algorithms
> - **Commitment Phase**:
> $$\begin{array}{lcl} 
\mathcal R & & \mathcal S \\[4pt] 
& & (d \in \mathbb F^n, f_d(q) = \langle q, d \rangle) \\[6pt] 
(pk, sk) \leftarrow \text{Gen}() & & \\[6pt]
r \xleftarrow{\$} \mathbb F^n &  & \\[6pt] 
\text{Enc}(pk, r) = (\text{Enc}(pk, r_1), \dots, \text{Enc}(pk, r_n)) & \xrightarrow{pk, \text{Enc}(pk, r)} & \\[6pt] 
s \leftarrow \text{Dec}(sk, e) & \xleftarrow{e} & e \leftarrow \text{Enc}(pk, f_d(r))\\[6pt]
\end{array}$$
> - **Decommitment Phase**:
> $$\begin{array}{lcl} 
\mathcal R & & \mathcal S \\[4pt] 
(q \in \mathbb F^n, r \in \mathbb F^n, s \in \mathbb F) & & (d \in \mathbb F^n, f_d(q) = \langle q, d \rangle) \\[6pt] 
\alpha \xleftarrow{\$} \mathbb F & \xrightarrow{(q, r + \alpha q)} & \\[6pt]
b \stackrel{?}{=} s + \alpha a & \xleftarrow{(a, b)} & (a, b) = (f_d(q), f_d(r + \alpha q))
\end{array}$$
> If the check success, $\text{accept}$ and returns $a$, else, $\text{reject}$ and returns $\perp$.

## Property

### Correctness

> [!property] Correctness
> $$b = f_d(r + \alpha q) = f_d(r) + \alpha \cdot f_d(q) = s + \alpha a$$

### Complexity

| Communication                              | $\mathcal R$ time | $\mathcal S$ time |
| ------------------------------------------ | ----------------- | ----------------- |
| $O(n)$ from receiver<br>$O(1)$ from sender |                   |                   |
