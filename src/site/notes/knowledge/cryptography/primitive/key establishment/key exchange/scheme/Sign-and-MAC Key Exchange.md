---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/key-establishment/key-exchange/scheme/sign-and-mac-key-exchange/","dg-note-properties":{"aliases":["SIGMA","SIGn-and-MAc","Σ0"]}}
---

Reference:
- `[Kra03]` — H. Krawczyk, _SIGMA: the 'SIGn-and-MAc' Approach to Authenticated Diffie-Hellman and its Use in the IKE Protocols_, CRYPTO 2003: §2.1 (model and requirements), §3 (BADH, STS), §4 (ISO), §5.1 (basic SIGMA), §5.2 (SIGMA-I), §5.3 (SIGMA-R): https://www.iacr.org/archive/crypto2003/27290399/27290399.pdf
- `[CK02]` — R. Canetti, H. Krawczyk, _Security Analysis of IKE's Signature-based Key-Exchange Protocol_, CRYPTO 2002: §3 (protocol $\Sigma_0$, Figure 1), Theorem 3, §5.1–5.3 (variants): https://www.iacr.org/archive/crypto2002/24420143/24420143.pdf

## Scheme

Reference Name: $\Sigma_0$ (basic SIGMA)
Instantiates:: [[knowledge/cryptography/primitive/key establishment/key exchange/Authenticated Key Exchange\|Authenticated Key Exchange]]

### Setting

> [!scheme] Setting
> - $\mathbb G = \langle g \rangle$: a [[knowledge/math/algebra/structures/group/special group/Cyclic Group\|Cyclic Group]] of prime order $q$ in which DDH is assumed; `[CK02]` takes a prime-order subgroup of $\mathbb Z_p^*$.

### Parties

> [!definition] Parties
> - $I$: the initiator, with identity $\mathrm{ID}_i$ and a long-term signing key.
> - $R$: the responder, with identity $\mathrm{ID}_r$ and a long-term signing key.
> - A certification authority, or another trusted mechanism, that binds each identity to its public key `[Kra03 §2.1]`.
> - Peers are post-specified: a session learns its peer during the run `[CK02 §2.2]` ([[knowledge/cryptography/primitive/key establishment/key exchange/Authenticated Key Exchange#Syntax\|Authenticated Key Exchange#Syntax]]).

### Parameters

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/key establishment/key exchange/Authenticated Key Exchange\|Authenticated Key Exchange]]: Import $(\lambda, s, Q, k)$.
> - $x, y \in \mathbb Z_q$: the ephemeral exponents of $I$ and $R$.
> - $k_0$: the session key. $k_1$: the MAC key. $k_2$: the encryption key of the identity-protecting variant.
> - $\text{"0"}, \text{"1"}$: tags that mark the initiator's and the responder's messages.

### Building Blocks

> [!definition] Building Blocks
> - $\mathsf{sig}$: a [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|Digital Signature]] scheme, [[knowledge/cryptography/primitive/digital signatures/Old Digital Signature#Unforgeability\|unforgeable under chosen-message attack]]; $\mathsf{sig}_i, \mathsf{sig}_r$ sign with the keys of $I$ and $R$.
> - $\mathsf{mac}$: a [[knowledge/cryptography/primitive/message authentication/Message Integrity#MAC Security\|secure MAC]].
> - $\mathsf{prf}$: a [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function#Secure PRF\|secure PRF]], keyed with the Diffie–Hellman value $g^{xy}$.

### Algorithms

> [!scheme] Protocol $\Sigma_0$ `[CK02 Fig. 1]`
> | | initiator $I$ | | responder $R$ |
> | --- | --- | --- | --- |
> | 1 | $x \xleftarrow{\$} \mathbb Z_q$ | $\xrightarrow{\ s,\, g^x\ }$ | |
> | 2 | | $\xleftarrow{\ s,\, g^y,\, \mathrm{ID}_r,\, \sigma_r,\, \tau_r\ }$ | $y \xleftarrow{\$} \mathbb Z_q$<br>$k_0 = \mathsf{prf}_{g^{xy}}(0)$, with $g^{xy} = (g^x)^y$<br>$k_1 = \mathsf{prf}_{g^{xy}}(1)$<br>$\sigma_r = \mathsf{sig}_r(\text{"1"}, s, g^x, g^y)$<br>$\tau_r = \mathsf{mac}_{k_1}(\text{"1"}, s, \mathrm{ID}_r)$ |
> | 3 | computes $g^{xy} = (g^y)^x$, $k_0$, $k_1$<br>verifies $\sigma_r$ under $\mathrm{ID}_r$'s public key<br>verifies $\tau_r$<br>$\sigma_i = \mathsf{sig}_i(\text{"0"}, s, g^y, g^x)$<br>$\tau_i = \mathsf{mac}_{k_1}(\text{"0"}, s, \mathrm{ID}_i)$<br>outputs $(I, s, \mathrm{ID}_r, k_0)$ | $\xrightarrow{\ s,\, \mathrm{ID}_i,\, \sigma_i,\, \tau_i\ }$ | |
> | 4 | | | verifies $\sigma_i$ under $\mathrm{ID}_i$'s public key<br>verifies $\tau_i$<br>outputs $(R, s, \mathrm{ID}_i, k_0)$ |
>
> A failed verification aborts the session. The exponents are fresh for every session and erased once $g^{xy}$ is computed, which gives perfect forward secrecy `[Kra03 §5.1]`.

> [!remark] What each piece does `[Kra03 §5.1]`
> - **The signature** covers both exponentials: it protects the sender's exponential against modification or choice by the attacker, and signing the *peer's* exponential (a fresh value) prevents replay.
> - **The MAC** covers the sender's *own* identity, under a key derived from $g^{xy}$: it binds the session key to that identity — what defeats [[knowledge/cryptography/cryptanalysis/Man-in-the-Middle Attack#Identity misbinding\|identity misbinding]].
> - **The keys** $k_0, k_1$ (and $k_2$) are derived from $g^{xy}$ so as to be computationally independent; the MAC key is never the session key.

> [!remark] Notation in the literature
> | source | messages | differences |
> | --- | --- | --- |
> | `[Kra03 §5.1]` | $g^x$; $g^y, B, \mathsf{sig}_B(g^x, g^y), \mathsf{mac}_{K_m}(B)$; $A, \mathsf{sig}_A(g^y, g^x), \mathsf{mac}_{K_m}(A)$ | parties $A, B$; no session id and no tags — the exponentials serve as session id and nonces; $K_m, K_s$ for $k_1, k_0$, with the derivation left to the full version |
> | `[CK02 Fig. 1]` | as above | session id $s$ and tags "0", "1"; $k_i = \mathsf{prf}_{g^{xy}}(i)$ |

## Property

### Correctness

> [!property] $\Sigma_0$ Correctness
> Both parties compute $g^{xy}$, hence the same $k_0$ and $k_1$; honest signatures and MACs verify, so both sessions complete with the same key and each names the other as peer: $(I, s, \mathrm{ID}_r, k_0)$ and $(R, s, \mathrm{ID}_i, k_0)$ are matching sessions.

## Security

> [!security] SK-security `[CK02 Thm 3]`
> Assuming the [[knowledge/cryptography/assumptions/Decisional Diffie-Hellman Assumption\|DDH assumption]] in $\mathbb G$, and the security of $\mathsf{sig}$, $\mathsf{mac}$ and $\mathsf{prf}$, protocol $\Sigma_0$ is [[knowledge/cryptography/primitive/key establishment/key exchange/Authenticated Key Exchange#SK-security\|SK-secure]] in the post-specified-peer model. The proof shows the two conditions separately: matching sessions output the same key, and the test-session key is indistinguishable from random (by hybrids, a DDH distinguisher, and reductions to $\mathsf{sig}$, $\mathsf{mac}$ and $\mathsf{prf}$).

> [!remark] Hashing $g^{xy}$
> `[CK02]` recommends keying the PRF with $H(g^{xy})$ in practice; security then rests on the hashed Diffie–Hellman (HDH) assumption instead of DDH.

### Why the simpler designs fail

Messages 2 and 3 of each design `[Kra03 §3–5]`, read top to bottom — each row fixes the problem of the row above:

| protocol | message 2, $B \to A$ | message 3, $A \to B$ | what goes wrong |
| --- | --- | --- | --- |
| BADH (§3.1) | $g^y, B, \mathsf{sig}_B(g^x, g^y)$ | $A, \mathsf{sig}_A(g^y, g^x)$ | **No binding.** Eve replaces message 3 by $E, \mathsf{sig}_E(g^y, g^x)$: Alice thinks she shares the key with Bob, Bob thinks he shares it with Eve — [[knowledge/cryptography/cryptanalysis/Man-in-the-Middle Attack#Identity misbinding\|identity misbinding]] |
| STS (§3.2) | $g^y, B, \{\mathsf{sig}_B(g^x, g^y)\}_{K_s}$ | $\{\mathsf{sig}_A(g^y, g^x)\}_{K_s}$ | **Binding by encryption fails.** If Eve can register Alice's public key as her own, she puts her identity in message 3 and the misbinding still works: encrypting the signature under $K_s$ does not prove that the signer holds the key |
| ISO (§4) | $B, g^y, \mathsf{sig}_B(g^x, g^y, A)$ | $\mathsf{sig}_A(g^y, g^x, B)$ | **Binds, but costs privacy.** Signing the *peer's* identity stops misbinding, and no element can be removed. But each party must know its peer before signing, so neither can authenticate without first revealing its own identity — and the signature is a signed record of the conversation. (Message 1 is $A, g^x$.) |
| SIGMA (§5.1) | $g^y, B, \mathsf{sig}_B(g^x, g^y), \mathsf{mac}_{k_1}(B)$ | $A, \mathsf{sig}_A(g^y, g^x), \mathsf{mac}_{k_1}(A)$ | **Binds without naming the peer.** The MAC of the sender's *own* identity, under a key derived from $g^{xy}$, ties the identity to the session key — the job ISO's peer identity did |

In one line: BADH has no binding; STS tries to bind by encryption and fails; ISO binds by signing the peer's name; SIGMA binds by MACing its own name under the new key.

## Variant

### SIGMA-I

> [!scheme] SIGMA-I — identity protection `[Kra03 §5.2]`
> | | initiator $A$ | | responder $B$ |
> | --- | --- | --- | --- |
> | 1 | | $\xrightarrow{\ g^x\ }$ | |
> | 2 | | $\xleftarrow{\ g^y,\ \{B,\, \mathsf{sig}_B(g^x, g^y),\, \mathsf{mac}_{K_m}(B)\}_{K_e}\ }$ | |
> | 3 | | $\xrightarrow{\ \{A,\, \mathsf{sig}_A(g^y, g^x),\, \mathsf{mac}_{K_m}(A)\}_{K_e}\ }$ | |
>
> The exponentials stay in the clear; identities, signatures and MACs are encrypted under a third key $K_e$ derived from $g^{xy}$ ($k_2$ in `[CK02 §5.3]`). The encryption must resist active attacks, so it includes integrity protection. An optional fourth message from $B$, authenticated under $K_m$, acknowledges completion.

### Other variants

- **MAC under the signature** — IKE's signature mode signs the MAC: message 2 carries $\mathsf{sig}_r(\mathsf{mac}_{k_1}(s, g^x, g^y, \mathrm{ID}_r))$ `[CK02 §5.2]`.
- **No tags** — $\Sigma_0$ stays secure without the tags "0" and "1" `[CK02 §5.1]`.
- **SIGMA-R** — a four-message variant `[Kra03 §5.3]`. `[CK02 §5.4]` analyzes a four-message variant used as IKE's main mode.

## Related

### Constructions
- [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Diffie-Hellman Key Exchange\|Diffie-Hellman Key Exchange]] — the unauthenticated exchange underneath
- [[knowledge/cryptography/primitive/key establishment/key exchange/Key-Exchange Authenticator\|Key-Exchange Authenticator]] — the general compiler; SIGMA is proved directly, not through it

### Prerequisites
- [[knowledge/cryptography/primitive/key establishment/key exchange/Authenticated Key Exchange\|Authenticated Key Exchange]], [[knowledge/cryptography/cryptanalysis/Man-in-the-Middle Attack\|Man-in-the-Middle Attack]], [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|Digital Signature]], [[knowledge/cryptography/primitive/message authentication/Message Integrity\|Message Integrity]], [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function\|Pseudorandom Function]]
