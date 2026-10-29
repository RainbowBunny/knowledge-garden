---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/key-establishment/key-exchange/key-exchange-authenticator/","dg-note-properties":{"aliases":["Authenticator","AM-to-UM Compiler"]}}
---

Reference:
- `[CK01]` — R. Canetti, H. Krawczyk, _Analysis of Key-Exchange Protocols and Their Use for Building Secure Channels_, EUROCRYPT 2001: §2.3 (the AM, protocol emulation and authenticators), §4 (Theorem 1), §4.1 (protocol 2DH, Theorem 2), §4.2 (SIG-DH): https://www.iacr.org/archive/eurocrypt2001/20450451.pdf
- `[BCK98]` — M. Bellare, R. Canetti, H. Krawczyk, _A Modular Approach to the Design and Analysis of Authentication and Key Exchange Protocols_, STOC 1998; ePrint 1998/009: https://eprint.iacr.org/1998/009 — the origin of authenticators and of the signature-based one; abstract read, body not opened (PostScript only).
- `[DH76]` — W. Diffie, M. E. Hellman, _New Directions in Cryptography_, IEEE Transactions on Information Theory IT-22(6), 1976, §III: http://www-ee.stanford.edu/%7Ehellman/publications/24.pdf
- `[Mer78]` — R. C. Merkle, _Secure Communications Over Insecure Channels_, Communications of the ACM 21(4), 1978, "The New Approach": https://ralphmerkle.com/1974/PuzzlesAsPublished.pdf

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/key establishment/key exchange/Authenticated Key Exchange\|Authenticated Key Exchange]]: Import $(\lambda, s, Q, k)$, and the two adversary models AM and UM of its Security section.
> - $\pi$: a protocol. $\lambda_\mathrm{mt}$: a message-transmission authenticator. $C_{\lambda_\mathrm{mt}}$: the compiler built from it.

> [!definition] Building Blocks
> - $\pi$: any key-exchange protocol that is [[knowledge/cryptography/primitive/key establishment/key exchange/Authenticated Key Exchange#SK-security\|SK-secure]] in the authenticated-links model (universally quantified).
> - $\lambda_\mathrm{mt}$: an authenticator for single messages — for instance the signature-based one of `[BCK98]`, built on a [[knowledge/cryptography/primitive/digital signatures/Digital Signature\|Digital Signature]] scheme.

> [!definition] Key-Exchange Authenticator
> An **authenticator** takes the description of a protocol $\pi$ and outputs a protocol $\pi'$ that emulates $\pi$ in the unauthenticated-links model: whatever a UM adversary does against $\pi'$, an AM adversary can do against $\pi$. It is an automatic compiler from the AM to the UM.
> - $C_{\lambda_\mathrm{mt}}(\pi)$: apply $\lambda_\mathrm{mt}$ to each message of $\pi$.
>
> $C_{\lambda_\mathrm{mt}}$ is an authenticator when $\lambda_\mathrm{mt}$ is one `[CK01 §2.3]`, citing `[BCK98]` for the proof.

> [!remark] Design in two steps
> Prove the protocol in the AM, where nobody can tamper with messages — the setting of the eavesdropper definitions of [[knowledge/cryptography/primitive/key establishment/key exchange/Key Exchange\|Key Exchange]] and of the original systems, whose channels were assumed authentic: a write-protected public file `[DH76 §III]`, a key channel whose messages arrive unmodified `[Mer78]`. Then compile the authentication in. Like the [[knowledge/cryptography/verifiable computing/compiler/Fiat-Shamir Transform\|Fiat-Shamir Transform]], it is a compiler: its security argument is made once, for every protocol it is applied to.

## Security

> [!security] Transfer of SK-security `[CK01 Thm 1]`
> If $\pi$ is SK-secure in the AM, with or without perfect forward secrecy, and $\lambda$ is an authenticator, then $C_\lambda(\pi)$ is SK-secure in the UM, with or without perfect forward secrecy, respectively.

## Example

### SIG-DH

> [!example] Signature-authenticated Diffie–Hellman `[CK01 §4.1–4.2]`
> **2DH** is the [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Diffie-Hellman Key Exchange\|Diffie–Hellman exchange]] with identities and a session id: $P_i$ sends $(P_i, s, \alpha = g^x)$, $P_j$ answers $(P_j, s, \beta = g^y)$, each outputs $g^{xy}$ and erases its exponent. Under DDH it is SK-secure in the AM `[CK01 Thm 2]`. Applying the signature-based authenticator, with the exponentials $\alpha$ and $\beta$ as its challenges, gives **SIG-DH**:
>
> | | $P_i$ | | $P_j$ |
> | --- | --- | --- | --- |
> | 1 | $x \xleftarrow{\$} \mathbb Z_q$ | $\xrightarrow{\ P_i,\, s,\, \alpha\ }$ | |
> | 2 | | $\xleftarrow{\ P_j,\, s,\, \beta,\, \mathsf{sig}_j(P_j, s, \beta, \alpha, P_i)\ }$ | $y \xleftarrow{\$} \mathbb Z_q$<br>$\gamma = \alpha^y$<br>erases $y$ |
> | 3 | verifies the signature and the values<br>$\gamma' = \beta^x$<br>erases $x$<br>outputs $\gamma'$ | $\xrightarrow{\ P_i,\, s,\, \mathsf{sig}_i(P_i, s, \alpha, \beta, P_j)\ }$ | |
> | 4 | | | verifies the signature<br>outputs $\gamma$ |
>
> SIG-DH is SK-secure in the UM, by Theorems 1 and 2 `[CK01 §4.2]`. Each signature names the **destination** party, which is essential to the security of the authenticator `[CK01 §4.2]`.

> [!remark] SIGMA is not this compiler
> SIG-DH signs the peer's identity, as the ISO protocol does; [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Sign-and-MAC Key Exchange\|SIGMA]] instead MACs the sender's own identity under a key derived from $g^{xy}$, so that a party can authenticate before knowing or naming its peer. SIGMA is proved directly `[CK02 Thm 3]`, not as an instance of Theorem 1: its MAC is keyed with a key the exchange itself produces.

## Related

### Instantiations
- SIG-DH, above — $\lambda_\mathrm{SIG}$ applied to 2DH

### Siblings
- [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Sign-and-MAC Key Exchange\|SIGMA]] — the identity-protecting alternative
- [[knowledge/cryptography/verifiable computing/compiler/Fiat-Shamir Transform\|Fiat-Shamir Transform]] — another compiler: interactive to non-interactive

### Prerequisites
- [[knowledge/cryptography/primitive/key establishment/key exchange/Authenticated Key Exchange\|Authenticated Key Exchange]], [[knowledge/cryptography/primitive/key establishment/key exchange/Key Exchange\|Key Exchange]], [[knowledge/cryptography/cryptanalysis/Man-in-the-Middle Attack\|Man-in-the-Middle Attack]]
