---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/public-key-encryption/fujisaki-okamoto-transformation/","dg-note-properties":{}}
---

Reference:
- `[FO99]` — E. Fujisaki, T. Okamoto, _Secure Integration of Asymmetric and Symmetric Encryption Schemes_, CRYPTO 1999, LNCS 1666, pp. 537–554: https://courses.grainger.illinois.edu/cs598dk/fa2019/Files/fujisaki_okamoto.pdf
## Syntax

> [!definition] Fujisaki-Okamoto Transformation
> ### Parameters
> - $\mathcal M_\text{PKE}, \mathcal C_\text{PKE}, \mathcal R_\text{PKE}, \mathcal K_\text{PKE}$
> - $\mathcal M_\text{SKE}, \mathcal C_\text{SKE}, \mathcal K_\text{SKE}$.
> 
> ---
> ### Building Block
> - $\text{PKE} = (\mathsf{KeyGen}, \text{Enc}, \text{Dec})$: A [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption Scheme (Old)\|Public-Key Encryption Scheme (Old)]] scheme.
> - $\text{SKE} = (\text{Enc}, \text{Dec})$: A [[knowledge/cryptography/primitive/symmetric encryption/Symmetric Key Encryption\|Symmetric Key Encryption]] scheme.
> - $G: \mathcal M_\text{PKE} \rightarrow \mathcal K_\text{SKE}$
> - $H: \mathcal M_\text{PKE} \times \mathcal M_\text{SKE} \rightarrow \mathcal R_\text{PKE}$
> 
> ---
> ### Algorithms
> - $(pk, sk) \leftarrow \mathsf{KeyGen}()$:
> 	1. Return $\text{PKE}.\mathsf{KeyGen}()$
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

> [!remark] Notation in the literature
> Key generation is $\mathsf{KeyGen}$ in this vault ([[Note Layouts\|Note Layouts]] § *Game form*).
>
> | source | algorithms | differences |
> | --- | --- | --- |
> | `[FO99 Def 2, §3]` | asymmetric $\Pi^{\mathrm{asym}} = (K^{\mathrm{asym}}, E^{\mathrm{asym}}, D^{\mathrm{asym}})$, symmetric $\Pi^{\mathrm{sym}} = (E^{\mathrm{sym}}, D^{\mathrm{sym}})$, hybrid $\Pi^{\mathrm{hy}} = (K^{\mathrm{hy}}, E^{\mathrm{hy}}, D^{\mathrm{hy}})$ | key generation takes $1^k$, left implicit here; $K^{\mathrm{hy}}(1^k)$ runs $K^{\mathrm{asym}}(1^k)$; the coin and message spaces are listed as components of each scheme. |

