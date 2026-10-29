---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/relation/set-membership-relation/","dg-note-properties":{"aliases":["Set Membership Proof","Set Membership"]}}
---

Reference:
- `[BCF+21]` — D. Benarroch, M. Campanelli, D. Fiore, K. Gurkan, D. Kolonelos, _Zero-Knowledge Proofs for Set Membership: Efficient, Succinct, Modular_, Financial Cryptography 2021; ePrint 2019/1255, §1 and the relation $R_\mathrm{mem}$: https://eprint.iacr.org/2019/1255.pdf
- `[TNLPS26]` — N. Tran, K. Nguyen, D. Liu, J. Pieprzyk, W. Susilo, _Compact Lattice-Based NIZK Arguments for Set Membership and Ring Signatures without RO_, ePrint 2026/1885 (revision of an ASIACRYPT 2026 paper): abstract, §1, §4.2, §5.1: https://eprint.iacr.org/2026/1885. Its reference list was beyond what I could read, so works it cites by number are named here only when its text names them.

## Definition

> [!definition] Parameters
> - $U$: a set; $u$: an element. $c_U, c_u$: commitments to them ([[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme\|Commitment Scheme]]), with openings $o_U, o_u$.
>
> `[BCF+21]`

> [!definition] Set Membership Relation
> $$R_\mathrm{mem}(U, u) = 1 \iff u \in U.$$
> In commit-and-prove form, the statement is $(c_U, c_u)$ and the witness is $(U, u, o_U, o_u)$: the witness satisfies $R_\mathrm{mem}(U, u) = 1$, and both commitments open correctly. A **set-membership proof** is a [[knowledge/cryptography/verifiable computing/property/Zero Knowledge\|zero-knowledge]] proof or argument for this relation: it convinces that the committed element lies in the set and reveals nothing else. `[BCF+21]`

### Public set, hidden element

> [!definition] Parameters
> - $S = \{d_0, \dots, d_{N-1}\}$: a public set, compressed by a [[knowledge/cryptography/verifiable computing/commitment/Cryptographic Accumulator\|Cryptographic Accumulator]] into $u = \mathsf{Acc}(S)$. $c$: a commitment to the hidden element $d$.

> [!definition] Accumulator Form
> The statement is the accumulator value $u$ and the commitment $c$; the witness is $d$, its opening and its membership witness $w$, with $\mathsf{Verify}(u, d, w) = 1$. For a Merkle-tree accumulator, `[TNLPS26 §4.2]` writes the language level by level: commitments to the nodes of the path, and at each level a disjunction — the node is the left or the right child — tying it to the node above; soundness holds for a relaxed version of the language.

> [!remark] With a second relation
> Applications prove more than membership: in a ring signature, that the member's public key $d$ is in the ring *and* that the signer knows the secret key behind $d$ — `[TNLPS26 §5.1]` adds one linear relation for this, and accumulates pairs $(d, M)$ so that the signed message $M$ is bound inside the accumulator.

## Property

> [!remark] What a construction aims for `[TNLPS26 abstract, §1]`
> - **Compact** — proof size $O(\log N)$ in the set size $N$, as accumulator-based constructions achieve.
> - **Post-quantum** — from lattice assumptions.
> - **Non-interactive without random oracles** — succinct constructions mostly use the [[knowledge/cryptography/verifiable computing/compiler/Fiat-Shamir Transform\|Fiat-Shamir Transform]] in the [[knowledge/cryptography/assumptions/idealized models/Random Oracle Model\|Random Oracle Model]]; a standard-model proof in the CRS model avoids it.

## Example

### Applications

- **Ring signatures** — "I own one of the keys in the ring" ([[knowledge/cryptography/primitive/digital signatures/Ring Signature\|Ring Signature]]) `[TNLPS26 abstract]`.
- **Anonymous credentials** — "my credential is in the list of valid ones" `[TNLPS26 abstract]`.
- **Anonymous payments** — "my coin is in the set of coins": Zcash-style systems prove Merkle-tree membership with a general-purpose zkSNARK `[BCF+21 §1]`.

### Constructions

| approach | in the sources | setting | proof |
| --- | --- | --- | --- |
| Merkle tree + general-purpose zkSNARK | Zcash-style `[BCF+21 §1]` | $O(1)$ accumulator value, witnesses of size $\log n$; the SNARK's own setup | constant size; about $\log n$ hashes inside the proved circuit |
| RSA accumulators | Benaloh–de Mare 1994, Barić–Pfitzmann 1997, Camenisch–Lysyanskaya 2002 `[BCF+21 §1]` | hidden-order group; not post-quantum | accumulator and witness one group element each |
| pairing-based accumulators | Nguyen 2005 and successors `[BCF+21 §1]` | trusted setup, parameters about the set bound | small |
| accumulators + commit-and-prove SNARKs | `[BCF+21]` | RSA, pairings, or class groups | modular: the membership proof composes with other proofs on the same commitment |
| one-out-of-many proofs | `[TNLPS26 §1]` | classical assumptions | logarithmic |
| lattice Merkle accumulators + Stern-type arguments | Libert et al. `[TNLPS26 §1]` | lattices, Fiat–Shamir | logarithmic |
| lattice one-out-of-many: SMILE, BLOOM | `[TNLPS26 §1]` | ideal lattices, Fiat–Shamir | logarithmic |
| generic NIZK for NP from LWE | Peikert–Shiehian `[TNLPS26 §1]` | standard model | grows with $\lvert S \rvert$ once membership is a circuit |
| pairing-based (non-)membership NIZK | Lipmaa–Parisella `[TNLPS26 §1]` | standard model; may need linear-size parameters | — |
| lattice accumulator + [[knowledge/cryptography/verifiable computing/proof system/interactive/Trapdoor Sigma Protocol\|Trapdoor Sigma Protocol]] + NIZK compiler | `[TNLPS26 §4]` | Module-SIS / Module-LWE, CRS model, no random oracle | $O(\log N)$ |

## Related

### Constructions
- [[knowledge/cryptography/verifiable computing/proof system/interactive/Trapdoor Sigma Protocol\|Trapdoor Sigma Protocol]] — the set-membership protocol of `[TNLPS26 §4.2]` (OR-composition along the Merkle path)
- [[knowledge/cryptography/verifiable computing/commitment/Cryptographic Accumulator\|Cryptographic Accumulator]] — compresses the public set

### Prerequisites
- [[knowledge/cryptography/verifiable computing/relation/Effective Relation\|Effective Relation]], [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme\|Commitment Scheme]], [[knowledge/cryptography/verifiable computing/property/Zero Knowledge\|Zero Knowledge]], [[knowledge/cryptography/verifiable computing/proof system/non-interactive/Non-Interactive Proof Systems\|Non-Interactive Proof Systems]]
