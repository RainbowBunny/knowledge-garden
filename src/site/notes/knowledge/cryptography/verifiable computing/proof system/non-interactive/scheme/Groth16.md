---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof-system/non-interactive/scheme/groth16/","dg-note-properties":{"type":"zk-SNARK"}}
---

## Scheme

> [!definition] Parameters
> - [[knowledge/cryptography/verifiable computing/relation/arithmetization/Quadratic Arithmetic Program\|Quadratic Arithmetic Program]]
> - [[knowledge/math/algebra/structures/elliptic curve/Bilinear Pairings\|Bilinear Pairings]]

> [!scheme] Groth16
> Instantiates:: [[knowledge/cryptography/verifiable computing/proof system/non-interactive/Zero-Knowledge Succinct Non-interactive ARgument of Knowledge\|zk-SNARK]]
>
> ---
> - $(\mathrm{prk}, \mathrm{vk}, \mathrm{td}) \leftarrow \mathsf{Setup}(1^\lambda, \mathcal{R})$:
> 	1. $(\tau, \alpha, \beta, \delta, \gamma) \xleftarrow{\$} \mathbb{F}^5$.
> 	2. $\mathrm{td} = (\tau, \alpha, \beta, \delta, \gamma)$.
> 	3. $\mathrm{prk} \leftarrow \begin{pmatrix}[\alpha]_1, [\beta]_1, [\beta]_2, [\delta]_1, [\delta]_2\\([a_j(\tau)]_1, [b_j(\tau)]_1)_{j \in [0, N_v]}, ([b_j(\tau)]_2)_{j \in [0, N_v]} \\ \left( \left[\frac{\beta a_j(\tau) + \alpha b_j(\tau) + c_j(\tau)}{\delta}\right]_1 \right)_{j \in [n + 1, N_v]} \\ \left( \left[\frac{\tau^i t(\tau)}{\delta} \right]_1 \right)_{i \in [0, N_g - 2]}\end{pmatrix}$.
> 	4. $\mathrm{vk} \leftarrow \begin{pmatrix}[\alpha]_1, [\beta]_2, [\delta]_1, [\delta]_2 \\ \left(\left[\frac{\beta a_j(\tau) + \alpha b_j(\tau) + c_j(\tau)}{\gamma}\right]_1\right)_{i \in [0, N_v]}\end{pmatrix}$.
> 	5. Returns $(\mathrm{prk}, \mathrm{vk}, \mathrm{td})$.
> - $\pi \leftarrow \mathsf{Prove}(\mathrm{prk}, \mathbf{x}, \mathbf{w})$:
> 	1. $haha$

> [!remark]
> In Groth16:
> - $\alpha$ and $\beta$ guarantee the same $c_i$ were used in $\pi_A$ and $\pi_B$.
> - $\gamma$ guarantees the public coordinates are the verifier’s x and not something the prover substituted.
> - $\delta$ guarantees the $\psi_i$ appear only in $\pi_C$, so the read-off is unambiguous.
> - $\tau$ guarantees the extracted assignment satisfies the QAP.


