---
{"dg-publish":true,"permalink":"/knowledge/cryptography/cryptanalysis/man-in-the-middle-attack/","dg-note-properties":{"aliases":["MITM","Person-in-the-Middle Attack","Man in the Middle"]}}
---

Reference:
- `[Gal12]` — S. D. Galbraith, _Mathematics of Public Key Cryptography_ (CUP 2012), §20.5: https://www.math.auckland.ac.nz/~sgal018/crypto-book/ch20.pdf
- `[Cia24]` — M. Ciampi, _Introduction to Modern Cryptography_, Lecture 13 (Key Exchange and the Diffie-Hellman Protocol), University of Edinburgh, "Active attacks", slides citing Katz–Lindell §10.3–10.4: https://opencourse.inf.ed.ac.uk/sites/default/files/https/opencourse.inf.ed.ac.uk/imc/2024/diffie-hellman.pdf
- `[Kra03]` — H. Krawczyk, _SIGMA: the 'SIGn-and-MAc' Approach to Authenticated Diffie-Hellman and its Use in the IKE Protocols_, CRYPTO 2003, §2.1 and §3.1: https://www.iacr.org/archive/crypto2003/27290399/27290399.pdf
- `[DH76]` — W. Diffie, M. E. Hellman, _New Directions in Cryptography_, IEEE Transactions on Information Theory IT-22(6), 1976, §III: http://www-ee.stanford.edu/%7Ehellman/publications/24.pdf
- `[Mer78]` — R. C. Merkle, _Secure Communications Over Insecure Channels_, Communications of the ACM 21(4), 1978, pp. 294–299 ("The New Approach", "Some Implications"): https://ralphmerkle.com/1974/PuzzlesAsPublished.pdf
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, §10.1: https://www.cis.upenn.edu/~sga001/classes/cis331f19/resources/bs_ch10.pdf

## Definition

> [!definition] Parameters
> - $P$: a two-party protocol — here a [[knowledge/cryptography/primitive/key establishment/key exchange/Key Exchange\|key exchange]] — between Alice and Bob.
> - $\mathcal E$: an active adversary on the channel between them.

> [!definition] Man-in-the-Middle Attack
> An **active** adversary controls the channel: it can intercept, delete, delay, modify and inject messages `[Kra03 §2.1]`. In a **man-in-the-middle attack** it uses this to run the protocol separately with each party, posing to each as the other. Against an unauthenticated key exchange, the outcome is
> - Alice terminates with a key $k_A$, Bob with a key $k_B \neq k_A$;
> - the adversary knows both;
> - neither Alice nor Bob can detect that an attack took place.
>
> `[Cia24]` `[Gal12 §20.5]`

> [!remark] Why eavesdropping security says nothing here
> The eavesdropper games of [[knowledge/cryptography/primitive/key establishment/key exchange/Key Exchange\|Key Exchange]] give the adversary only the transcript of an honest run; the first weakness `[BS §10.1]` lists is that it cannot tamper with messages. A protocol secure in that sense can still be broken by an adversary who replaces messages.

> [!remark] The precondition is a channel without authentication
> Both public key distribution systems of the 1970s assumed the authentication away:
> - `[DH76 §III]` puts the public values in a public file that "must be protected from unauthorized modification";
> - `[Mer78]`, "The New Approach", keeps the assumption that the key channel delivers messages unmodified — tampering "can be detected" — and drops only the assumption that it is unreadable; identities are confirmed with a correct, non-secret codebook ("Some Implications").
>
> A man in the middle is what these assumptions exclude: every defence below restores authentication of the messages, of the identities, or both.

## Example

### Against Diffie–Hellman

> [!example] Man in the middle on [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Diffie-Hellman Key Exchange\|Diffie-Hellman Key Exchange]]
> The adversary runs one exchange with each party, with its own exponents $e_A, e_B$ `[Gal12 §20.5]`:
>
> | | Alice | | Eve | | Bob |
> | --- | --- | --- | --- | --- | --- |
> | 1 | $\alpha \xleftarrow{\$} \mathbb Z_q$<br>$u = g^\alpha$ | $\xrightarrow{\ u\ }$ | intercepts $u$<br>$e_B \xleftarrow{\$} \mathbb Z_q$ | $\xrightarrow{\ g^{e_B}\ }$ | |
> | 2 | | $\xleftarrow{\ g^{e_A}\ }$ | intercepts $v$<br>$e_A \xleftarrow{\$} \mathbb Z_q$ | $\xleftarrow{\ v\ }$ | $\beta \xleftarrow{\$} \mathbb Z_q$<br>$v = g^\beta$ |
> | 3 | $k_A = (g^{e_A})^\alpha$ | | $k_A = u^{e_A}$<br>$k_B = v^{e_B}$ | | $k_B = (g^{e_B})^\beta$ |
>
> - Alice holds $k_A = g^{\alpha e_A}$ and believes she shares it with Bob.
> - Bob holds $k_B = g^{\beta e_B}$ and believes he shares it with Alice.
> - Eve holds both. She decrypts each message with one key, may modify it, re-encrypts it with the other, and forwards it.
>
> Eve need not replace any long-term public key: the attack is on the ephemeral messages `[Gal12 §20.5]`. Taking $e_A = e_B$ works as well.

## Variant

### Identity misbinding

> [!definition] Identity Misbinding Attack
> The two honest parties end with the **same** session key, which stays secret, but each binds it to a different peer: one believes it talks to the other, the other believes it talks to the adversary. It breaks the *consistency* requirement of [[knowledge/cryptography/primitive/key establishment/key exchange/Authenticated Key Exchange\|Authenticated Key Exchange]], not secrecy. `[Kra03 §2.1, §3.1]`

> [!example] Misbinding on signed Diffie–Hellman (BADH) `[Kra03 §3.1]`
> In BADH each party signs the two exponentials. Eve lets the first two messages pass and replaces the third with her own identity and signature:
>
> | | Alice | | Eve | | Bob |
> | --- | --- | --- | --- | --- | --- |
> | 1 | sends $g^x$ | $\xrightarrow{\ g^x\ }$ | forwards | $\xrightarrow{\ g^x\ }$ | |
> | 2 | | $\xleftarrow{\ g^y,\, B,\, \mathsf{sig}_B(g^x, g^y)\ }$ | forwards | $\xleftarrow{\ g^y,\, B,\, \mathsf{sig}_B(g^x, g^y)\ }$ | |
> | 3 | sends $A, \mathsf{sig}_A(g^y, g^x)$ | $\xrightarrow{\ A,\, \mathsf{sig}_A(g^y, g^x)\ }$ | drops it<br>signs with her own key | $\xrightarrow{\ E,\, \mathsf{sig}_E(g^y, g^x)\ }$ | |
>
> Alice holds a key she believes she shares with Bob; Bob holds the same key and believes he shares it with Eve. Eve does not learn the key, but Bob will attribute to Eve whatever Alice sends.

> [!remark] Station-to-station is not immune `[Kra03 §3.2]`
> STS encrypts the signatures under the session key. The misbinding attack still works when a party can register a public key without proving possession of the private key: Eve registers Alice's public key as her own and puts her identity in the third message. Encryption does not prove possession of the key.

## Related

### Constructions
- [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Sign-and-MAC Key Exchange\|SIGMA]] — signs the exponentials and MACs the sender's identity under a key derived from $g^{xy}$; resists both attacks above
- [[knowledge/cryptography/primitive/key establishment/key exchange/Key-Exchange Authenticator\|Key-Exchange Authenticator]] — the general cure: compiles any protocol secure with authenticated links into one secure against an active adversary

### Prerequisites
- [[knowledge/cryptography/primitive/key establishment/key exchange/Key Exchange\|Key Exchange]], [[knowledge/cryptography/primitive/key establishment/key exchange/Authenticated Key Exchange\|Authenticated Key Exchange]], [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Diffie-Hellman Key Exchange\|Diffie-Hellman Key Exchange]]
