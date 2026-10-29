---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/key-establishment/key-exchange/authenticated-key-exchange/","dg-note-properties":{"aliases":["AKE"]}}
---

Reference:
- `[CK01]` — R. Canetti, H. Krawczyk, _Analysis of Key-Exchange Protocols and Their Use for Building Secure Channels_, EUROCRYPT 2001: §2 (protocols, sessions, the unauthenticated-links model, the authenticated-links model), §3 (Definition 1, SK-security; §3.2 forward secrecy): https://www.iacr.org/archive/eurocrypt2001/20450451.pdf
- `[CK02]` — R. Canetti, H. Krawczyk, _Security Analysis of IKE's Signature-based Key-Exchange Protocol_, CRYPTO 2002, §2.2 (post-specified peers, Definitions 2 and 3): https://www.iacr.org/archive/crypto2002/24420143/24420143.pdf
- `[Kra03]` — H. Krawczyk, _SIGMA: the 'SIGn-and-MAc' Approach to Authenticated Diffie-Hellman and its Use in the IKE Protocols_, CRYPTO 2003, §2.1–2.2 (attacker model, requirements, identity protection): https://www.iacr.org/archive/crypto2003/27290399/27290399.pdf

## Syntax

> [!definition] Parameters
> - $\lambda$: the security parameter.
> - $P_1, \dots, P_N$: parties, each with a long-term key pair; a certification authority (or another trusted mechanism) binds each identity to its public key.
> - $s$: a session identifier. $(P, s)$: the session $s$ of party $P$.
> - $Q$: the peer of a session. $d$: a destination address, which need not name the peer.
> - $k$: a session key.
>
> `[CK01 §2.1]` `[CK02 §2.2]` `[Kra03 §2.1]`

> [!definition] Authenticated Key Exchange
> An **authenticated key-exchange protocol** is run by the parties $P_1, \dots, P_N$ over a network the adversary controls. Each party runs many sessions concurrently:
> - a session is **activated** as $(P, s, Q)$ — the peer is known in advance (pre-specified peer) `[CK01 §2.1]` — or as $(P, s, d)$ — the peer is learned during the run (post-specified peer) `[CK02 §2.2]`;
> - on completion it **outputs** $(P, s, Q, k)$: the session key and the peer it is shared with;
> - two sessions **match** if they are $(P, s)$ with peer $Q$ and $(Q, s)$ with peer $P$. With post-specified peers, $(Q, s)$ also matches a completed $(P, s)$ while it is still incomplete `[CK02 Def 2]`.
>
> What it adds to [[knowledge/cryptography/primitive/key establishment/key exchange/Key Exchange\|Key Exchange]]: identities, many concurrent sessions, and security against an adversary who controls the network rather than only reading it.

> [!remark] Requirements, informally `[Kra03 §2.1]`
> - **Authentication** — each party verifies the identity of the peer of its session.
> - **Consistency** — if two honest parties share a key, each has the same view of who the peers are; "much trickier and many times overlooked" — see [[knowledge/cryptography/cryptanalysis/Man-in-the-Middle Attack#Identity misbinding\|Man-in-the-Middle Attack#Identity misbinding]].
> - **Secrecy** — no third party learns anything about the session key: it is indistinguishable from a random key.
> - **Perfect forward secrecy** — session keys produced and erased before a party is corrupted stay secure.
> - **Identity protection** (§2.2) — optionally, the identities of the parties are not revealed to the attacker; see [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Sign-and-MAC Key Exchange#SIGMA-I\|Sign-and-MAC Key Exchange#SIGMA-I]].

## Security

### Adversary models

> [!definition] Parameters
> - $\mathcal A$: an adversary, one stateful interactive machine ([[knowledge/cryptography/foundations/Security Game\|Security Game]]).

> [!definition] Unauthenticated and Authenticated Links
> - **Unauthenticated-links model (UM)** — $\mathcal A$ controls all communication: it intercepts, delays, deletes, modifies and injects messages, and schedules sessions. It may also issue **session-state reveal** (the internal state of a session, such as an ephemeral exponent), **session-key query** and **party corruption** (all long-term secrets; the party is then controlled by $\mathcal A$). `[CK01 §2.2]` `[Kra03 §2.1]`
> - **Authenticated-links model (AM)** — the same, except that the links are authenticated: $\mathcal A$ cannot modify messages or inject messages of its own; it still chooses when, and whether, to deliver them. `[CK01 §2.3]`

### SK-security

> [!definition] Parameters
> - The protocol's parties, sessions and keys from Syntax. $\mathcal A$: a PPT adversary in the UM (or the AM).

> [!definition] SK-Security
> ### Scope
> An authenticated key-exchange protocol and a PPT adversary $\mathcal A$ in the UM.
>
> ---
> ### Condition
> - **Access** — the whole network, and the three exposure queries of the UM; one test query.
> - **Promise** — the test session is completed and unexposed, and stays so, together with its matching session.
> - **Quantifier** — $\forall$ PPT $\mathcal A$.
> - **Adaptivity** — everything is adaptive; $\mathcal A$ keeps running after the test query.
>
> ---
> ### Experiment
> A distinguishing game: the branches differ in the answer to the test query. `[CK01 Def 1]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | generates the parties' long-term key pairs | $\xrightarrow{\ \text{public keys}\ }$ | |
> | 2 | | $\xleftarrow{\ \text{activate } (P, s, Q) \text{ or deliver a message}\ }$ | **Network** (repeated, adaptive): activates sessions; delivers, modifies or injects messages |
> | | runs the code of the party<br>records its outputs | $\xrightarrow{\ \text{outgoing messages, outputs}\ }$ | |
> | 3 | | $\xleftarrow{\ \text{reveal / key query / corrupt}\ }$ | **Exposure** (repeated, adaptive): session-state reveal, session-key query, party corruption |
> | | answers with the state, the key, or the long-term secrets | $\xrightarrow{\ \text{answer}\ }$ | |
> | 4 | | $\xleftarrow{\ (P, s)\ }$ | **Test**: names a completed, unexposed session |
> | | $k_0$: the key output by $(P, s)$<br>**Game 0**: answers $k_0$<br>**Game 1**: answers a uniform key $k_1$ | $\xrightarrow{\ k_b\ }$ | |
> | 5 | | | rows 2–3 again, without exposing $(P, s)$ or its matching session |
> | 6 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}_b(\mathcal A)$, the bit $b'$ in Game $b$.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}_1(\mathcal A) = 1]$ are.
>
> ---
> ### Property
> The protocol is **SK-secure** if, for every PPT $\mathcal A$:
> - **Consistency** — if two uncorrupted parties complete matching sessions, they output the same key, except with negligible probability;
> - **Indistinguishability** — $\big|\Pr[\mathsf{Expt}_0(\mathcal A) = 1] - \Pr[\mathsf{Expt}_1(\mathcal A) = 1]\big|$ is negligible.
>
> `[CK01 Def 1]`. *SK-secure in the AM* is the same with an AM adversary. With post-specified peers, matching sessions are those of `[CK02 Def 2]` (`[CK02 Def 3]`).

> [!remark] The source's form
> `[CK01 Def 1]` flips a coin $b$, answers the test query with the real key or a random one, and asks $\Pr[b' = b] \leq 1/2 + \mathrm{negl}$; the difference above is twice that bias ([[knowledge/cryptography/primitive/public-key encryption/property/Indistinguishability under Chosen-Plaintext Attack#Bit-guessing form\|Indistinguishability under Chosen-Plaintext Attack#Bit-guessing form]]). In `[CK01]` the adversary also chooses when sessions expire; forward secrecy (§3.2) allows corrupting a party after the test session has expired.

## Related

### Instantiations
- [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Sign-and-MAC Key Exchange\|SIGMA]] — SK-secure in the post-specified-peer model under DDH `[CK02 Thm 3]`

### Constructions
- [[knowledge/cryptography/primitive/key establishment/key exchange/Key-Exchange Authenticator\|Key-Exchange Authenticator]] — turns a protocol SK-secure in the AM, such as Diffie–Hellman, into one SK-secure in the UM

### Siblings
- [[knowledge/cryptography/primitive/key establishment/key exchange/Key Exchange\|Key Exchange]] — two parties and a passive adversary

### Prerequisites
- [[knowledge/cryptography/cryptanalysis/Man-in-the-Middle Attack\|Man-in-the-Middle Attack]] — the attacks the UM adversary can mount
- [[knowledge/cryptography/foundations/Security Game\|Security Game]], [[knowledge/cryptography/foundations/Adversary\|Adversary]]
