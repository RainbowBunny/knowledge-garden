---
{"dg-publish":true,"permalink":"/knowledge/cryptography/threshold-cryptography/secret-sharing/schemes/shamir-secret-sharing/","dg-note-properties":{}}
---

## Scheme

> [!scheme] Shamir Secret Sharing
> Reference Name: $\text{SSS}$
> 
> ---
> ### Parameters
> - $\mathcal M = \mathbb Z_p$: Message space.
> - $p$: Random prime.
> - $n < p$: Number of parties.
> - $t \leq n$: Threshold. 
> 
> --- 
> ### Building Block
> 
> ---
> ### Algorithms
> - $(s_1, \dots, s_n) \leftarrow \text{Share}(m)$:
> 	1. $f_1, \dots, f_{t - 1} \xleftarrow{\$} \mathbb Z_p$
> 	2. $f(x) = m + \sum_{j = 1}^{t - 1} f_j x^j$
> 	3. For $i = 1$ to $n$:
> 		1. $s_i = (i, f(i) \mod p)$
> 	4. Return $(s_1, \dots, s_n)$
> - $m \leftarrow \text{Reconstruct}(\{s_i \; | \; i \in U\})$:
> 	1. $f(x)$ is the unique degree-$(t - 1)$ polynomial $\mod p$ passing through points $\{s_i \; | \; i \in U\}$
> 	2. Return $m = f(0)$
