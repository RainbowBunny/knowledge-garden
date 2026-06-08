---
{"dg-publish":true,"permalink":"/academic/knowledge/cryptography/public-key-encryption/fujisaki-okamoto-transformation/","dg-note-properties":{}}
---

Link: https://courses.grainger.illinois.edu/cs598dk/fa2019/Files/fujisaki_okamoto.pdf
## Syntax

> [!definition] Fujisaki-Okamoto Transformation
> ### Parameters
> - $\mathcal M_\text{PKE}, \mathcal C_\text{PKE}, \mathcal R_\text{PKE}, \mathcal K_\text{PKE}$
> - $\mathcal M_\text{SKE}, \mathcal C_\text{SKE}, \mathcal K_\text{SKE}$.
> 
> ---
> ### Building Block
> - $\text{PKE} = (\text{KeyGen}, \text{Enc}, \text{Dec})$: A [[academic/knowledge/cryptography/public-key encryption/Public Key Encryption\|Public Key Encryption]] scheme.
> - $\text{SKE} = (\text{Enc}, \text{Dec})$: A [[academic/knowledge/cryptography/symmetric encryption/Symmetric Key Encryption\|Symmetric Key Encryption]] scheme.
> - $G: \mathcal M_\text{PKE} \rightarrow \mathcal K_\text{SKE}$
> - $H: \mathcal M_\text{PKE} \times \mathcal M_\text{SKE} \rightarrow \mathcal R_\text{PKE}$
> 
> ---
> ### Algorithms
> - $(pk, sk) \leftarrow \text{KeyGen}()$:
> 	1. Return $\text{PKE}.\text{KeyGen}()$
> - $c \leftarrow \text{Enc}(pk, m)$:
> 	1. $\sigma \xleftarrow{R} \mathcal M_\text{PKE}$
> 	2. $r_1 \leftarrow H(\sigma, m)$
> 	3. $r_2 \leftarrow G(\sigma)$
> 	4. $c_1 \leftarrow \text{PKE}.\text{Enc}(pk, \sigma; r_1)$
> 	5. $c_2 \leftarrow \text{SKE}.\text{Enc}(r_2, m)$
> 	6. Return $(c_1, c_2)$
> - $m \leftarrow \text{Dec}(sk, (c_1, c_2))$:
> 	1. $\hat \sigma \leftarrow \text{PKE}.\text{Dec}(sk, c_1)$
> 	2. $\hat r_2 \leftarrow G(\hat \sigma)$
> 	3. $\hat m \leftarrow \text{SKE}.\text{Dec}(\hat \sigma, \hat m)$
> 	4. $\hat r_1 \leftarrow H(\hat \sigma; \hat r_1)$
> 	5. If $c_1 = \text{PKE}.\text{Enc}(\hat \sigma; \hat r_1)$ then $m \leftarrow \hat{m}$, else $m = \perp$
> 	6. Return $m$

