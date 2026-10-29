---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof-system/non-interactive/variant/split-prover/","dg-note-properties":{}}
---

Reference:
- `[GGKSS25]` — S. Garg, A. Goel, D. Kolonelos, S. Shiehian, R. Sinha, _Split Prover Zero-Knowledge SNARKs_, PKC 2025, LNCS 15674, pp. 353–380; ePrint 2025/373: https://eprint.iacr.org/2025/373. The paper's text could not be read; this note follows the PKC 2025 talk slides: https://iacr.org/submit/files/slides/2025/pkc/pkc2025/97/97_slides.pdf
- `⚠️ CLAUDE – verify:` — added by me, not taken from a source.

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/verifiable computing/proof system/non-interactive/Non-Interactive Proof Systems\|Non-Interactive Proof Systems]]: Import $(\mathcal R, \mathrm{crs}, \mathrm{st})$ and $(\mathsf{Setup}, \mathsf{Prove}, \mathsf{Verify})$.
> - $\mathbf x = \mathbf x_1 \Vert \mathbf x_2$, $\mathbf w = \mathbf w_1 \Vert \mathbf w_2$: the statement and the witness, each split into a first and a second part.
> - $\mathrm{aux}$: the hand-off from the first prover to the second.
>
> `[GGKSS25, slides]`

> [!definition] Split Prover
> A zkSNARK **admits a split prover** if proving can be done by two provers $(\mathcal P_1, \mathcal P_2)$ whose output the *original* verifier accepts:
> - $\mathrm{aux} \leftarrow \mathsf{Prove}_1(\mathbf x_1, \mathbf w_1)$: run by $\mathcal P_1$, who holds the first part.
> - $\boldsymbol\pi \leftarrow \mathsf{Prove}_2(\mathbf x_2, \mathbf w_2, \mathrm{aux})$: run by $\mathcal P_2$, who holds the second part and $\mathrm{aux}$.
> - $\mathsf{Verify}(\mathbf x, \boldsymbol\pi) = 1$: the verifier of the original zkSNARK, unchanged.
>
> `[GGKSS25, slides]`
>
> `⚠️ CLAUDE – verify:` the slides omit the reference string; in the paper both provers presumably take (parts of) $\mathrm{crs}$.

> [!remark] Who sees what
> - $\mathcal P_1$: $\mathbf x_1, \mathbf w_1$.
> - $\mathcal P_2$ (the delegatee): $\mathbf x_2, \mathbf w_2, \mathrm{aux}$ — it must not learn $\mathbf w_1$.
> - Verifier: $\mathbf x, \boldsymbol\pi$.
>
> The application is delegation: $\mathcal P_1$ does a light first step and hands the rest of the proving work to $\mathcal P_2$. `[GGKSS25, slides]`

## Property

### Split correctness
The two-phase proof is accepted by the original verifier whenever the original prover's would be. `[GGKSS25, slides]` (named only; formal statement in the paper, not read.)

## Security

### Split zero knowledge
$\mathrm{aux}$ leaks nothing about $\mathbf w_1$ to $\mathcal P_2$. `[GGKSS25, slides]` (named only; the paper's simulator and experiment were not read.)

## Construction

- From Groth16: the construction keeps Groth16's verification algorithm. It splits the R1CS as $\mathbf z = \mathbf z_I \Vert \mathbf z_{II}$ with block matrices $(\mathbf A_I\ \mathbf A_{II})$, $(\mathbf B_I\ \mathbf B_{II})$, $(\mathbf C_I\ \mathbf C_{II})$, and adds three dummy constraints with random values to blind $\mathrm{aux}$. `[GGKSS25, abstract and slides]`
- Lower bound: $\mathcal P_{II}$ must perform $\Omega(\min\{n - 1, \mathrm{rank}(\mathbf A_{II}) \cdot \mathrm{rank}(\mathbf B_{II})\})$ group operations. `[GGKSS25, slides]`

## Related

### Prerequisites
- [[knowledge/cryptography/verifiable computing/proof system/non-interactive/Non-Interactive Proof Systems\|Non-Interactive Proof Systems]], [[knowledge/cryptography/verifiable computing/property/Zero Knowledge\|Zero Knowledge]], [[knowledge/cryptography/verifiable computing/relation/r1cs/Rank-1 Constraint Satisfiability\|Rank-1 Constraint Satisfiability]]
