---
{"dg-publish":true,"permalink":"/knowledge/cryptography/threshold-cryptography/secret-sharing/schemes/simple-n-out-of-n-scheme/","dg-note-properties":{}}
---

## Scheme

> [!scheme] Simple $n$-out-of-$n$ Scheme
> ### Parameters
> - $\mathcal M = \{0, 1\}^\ell$: Message space.
> - $n$: Number of parties.
> - $t = n$: Threshold.
> 
> ---
> ### Building Block
> 
> --- 
> ### Algorithm
> - $(s_1, \dots, s_n) \leftarrow \text{Share}(m)$:
> 	1. $s_1, s_2, \dots, s_{n - 1} \xleftarrow{\$} \{0, 1\}^\ell$
> 	2. $s_n = s_1 \oplus \dots \oplus s_{n - 1} \oplus m$
> 	3. Return $(s_1, \dots, s_n)$
> - $m \leftarrow \text{Reconstruct}((s_1, \dots, s_n))$:
> 	1. Return $m = (s_1 \oplus \dots \oplus s_n)$

