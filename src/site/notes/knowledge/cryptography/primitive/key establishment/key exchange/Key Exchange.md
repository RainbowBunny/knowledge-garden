---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/key-establishment/key-exchange/key-exchange/","dg-note-properties":{"aliases":["KE"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023: https://toc.cryptobook.us/ (Ch. 10: §10.1 eavesdropping security, Definition 10.1; §10.3.2 on agreement failures). Copy of Ch. 10, §10.1–10.4: https://www.cis.upenn.edu/~sga001/classes/cis331f19/resources/bs_ch10.pdf
- `[KL]` — J. Katz, Y. Lindell, _Introduction to Modern Cryptography_, 2nd ed., CRC Press, 2014, §10.3: the experiment $\mathsf{KE}^{\mathsf{eav}}_{\mathcal A, \Pi}(n)$. `⚠️ CLAUDE – verify:` the book could not be read; the experiment and its definition were checked in lecture slides that cite §10.3: https://opencourse.inf.ed.ac.uk/sites/default/files/https/opencourse.inf.ed.ac.uk/imc/2024/diffie-hellman.pdf

## Syntax

> [!definition] Parameters
> - $\lambda$: the security parameter.
> - $\mathcal K$: the key space; $\{0, 1\}^\lambda$ in `[KL]`.
> - $P = (A, B)$: a key exchange protocol, run by Alice and Bob.
> - $k_A, k_B \in \mathcal K$: the keys the two machines output; $k$ when they agree.
> - $T_P$: the transcript of one run.

> [!definition] Key Exchange Protocol
> A **key exchange protocol** $P = (A, B)$ is a pair of probabilistic interactive machines that take turns in sending messages to each other:
> - $k_A \leftarrow A(1^\lambda)$: (Randomized) Alice's machine.
>     - **Input**: the security parameter $1^\lambda$; then the messages of $B$, one at a time.
>     - **Output**: its messages to $B$; on termination, a key $k_A \in \mathcal K$.
> - $k_B \leftarrow B(1^\lambda)$: (Randomized) Bob's machine.
>     - **Input**: the security parameter $1^\lambda$; then the messages of $A$, one at a time.
>     - **Output**: its messages to $A$; on termination, a key $k_B \in \mathcal K$.
>
> The **transcript** $T_P$ is the sequence of messages exchanged in one execution. It is a random variable, over the coins of $A$ and $B$. `[BS §10.1]` `[KL §10.3]`

> [!remark] The problem it solves `[BS §10.1]`
> Alice and Bob want to communicate online while an adversary listens; they want a **shared secret unknown to the adversary**, without having shared anything beforehand. `[BS]` calls this *anonymous* key exchange: nothing assures Alice and Bob that they are talking to each other — that is what [[knowledge/cryptography/primitive/key establishment/key exchange/Authenticated Key Exchange\|Authenticated Key Exchange]] adds.

> [!remark] Notation in the literature
> | source | form | differences |
> | --- | --- | --- |
> | `[BS §10.1]` | $P = (A, B)$ | the security parameter is implicit; both machines "obtain the same value $k$" |
> | `[KL §10.3]` | $\Pi$, run by both parties on $1^n$ | outputs $k \in \{0, 1\}^n$ |

## Property

### Correctness

> [!definition] Correctness
> When both machines terminate, they output the same key:
> $$k_A = k_B.$$
> `[BS §10.1]`. With a parameter generator that may fail, the keys may differ with negligible probability, as `[BS §10.3.2]` notes for a faulty prime generator.

## Security

### Against an eavesdropper

> [!definition] Parameters
> - The protocol's $P$, $k$, $T_P$ from Syntax.
> - $\mathbb A$: the class of efficient [[knowledge/cryptography/foundations/Adversary\|adversaries]].

> [!definition] Security against an Eavesdropper
> ### Scope
> A key exchange protocol $P = (A, B)$ and the adversary class $\mathbb A$ of Parameters.
>
> ---
> ### Condition
> - **Access** — $\mathcal A$ sees the transcript $T_P$ of one honest run of $P$ and nothing else; it cannot send, change or drop messages.
> - **Promise** — none.
> - **Quantifier** — $\forall \mathcal A \in \mathbb A$.
> - **Adaptivity** — none: $\mathcal A$ speaks once, after the run has ended.
>
> ---
> ### Experiment
> A search game: one branch; the challenger compares the guess with the key in the last row. `[BS §10.1]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | runs the protocol between $A$ and $B$<br>$k$: the shared key<br>$T_P$: the transcript | $\xrightarrow{\ T_P\ }$ | |
> | 2 | | $\xleftarrow{\ \hat k\ }$ | outputs a guess $\hat k$ for $k$ |
> | 3 | checks whether $\hat k = k$ | | |
>
> **Goal** — $\mathcal A$ wins iff:
> - $\hat k = k$.
>
> ---
> ### Property
> $$\mathsf{Adv}^{\mathsf{ke}}_P(\mathcal A) = \Pr[\hat k = k].$$
> - $P$ is **secure against an eavesdropper** if $\mathsf{Adv}^{\mathsf{ke}}_P(\mathcal A)$ is negligible for every efficient $\mathcal A$ `[BS Def 10.1]`.
>
> It is a *search* game, see [[knowledge/cryptography/foundations/Security Game\|Security Game]].

> [!remark] Why this definition is weak
> `[BS §10.1]` calls it extremely weak, for three reasons:
> - First, we assume the adversary is unable to tamper with messages. An adversary who can is a [[knowledge/cryptography/cryptanalysis/Man-in-the-Middle Attack\|man in the middle]].
> - Second, we only guarantee that the adversary cannot guess $k$ in its entirety. This does not rule out the possibility that the adversary can guess, say, half the bits of $k$. If we are to use $k$ as a secret session key, the property we would really like is that $k$ is indistinguishable from a truly random key — the game in [[knowledge/cryptography/primitive/key establishment/key exchange/Key Exchange#Real-or-Random Key\|#Real-or-Random Key]].
> - Third, the protocol provides no assurance of the identities of the participants.
>
> `[BS]` strengthens the definition in Chapter 21, authenticated key exchange — see [[knowledge/cryptography/primitive/key establishment/key exchange/Authenticated Key Exchange\|Authenticated Key Exchange]].

### Real-or-Random Key

> [!definition] Parameters
> - The protocol's $P$, $k$, $T_P$, $\mathcal K$ from Syntax.
> - $\mathbb A$: the class of efficient [[knowledge/cryptography/foundations/Adversary\|adversaries]].

> [!definition] Real-or-Random Security against an Eavesdropper
> ### Scope
> A key exchange protocol $P = (A, B)$ with key space $\mathcal K$ and the adversary class $\mathbb A$ of Parameters.
>
> ---
> ### Condition
> - **Access** — $\mathcal A$ sees the transcript $T_P$ of one honest run and a candidate key $\hat k$; it cannot send, change or drop messages.
> - **Promise** — none.
> - **Quantifier** — $\forall \mathcal A \in \mathbb A$.
> - **Adaptivity** — none: $\mathcal A$ speaks once, after the run has ended.
>
> ---
> ### Experiment
> A distinguishing game: two branches that differ in row 1 only, **Game 0** (the real key) and **Game 1** (a uniform key). `[KL §10.3]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | runs the protocol between $A$ and $B$<br>$k$: the shared key<br>$T_P$: the transcript<br>**Game 0**: $\hat k \leftarrow k$<br>**Game 1**: $\hat k \xleftarrow{\$} \mathcal K$ | $\xrightarrow{\ T_P,\, \hat k\ }$ | |
> | 2 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}_b(\mathcal A)$, the bit $b'$ in Game $b$.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}_1(\mathcal A) = 1]$ are.
>
> ---
> ### Property
> $$\mathsf{Adv}^{\mathsf{eav}}_P(\mathcal A) = \big|\Pr[\mathsf{Expt}_0(\mathcal A) = 1] - \Pr[\mathsf{Expt}_1(\mathcal A) = 1]\big|.$$
> - $P$ is **secure in the presence of an eavesdropper** if $\mathsf{Adv}^{\mathsf{eav}}_P(\mathcal A)$ is negligible for every efficient $\mathcal A$ `[KL §10.3]`.
>
> It is a *distinguishing* game, see [[knowledge/cryptography/foundations/Security Game\|Security Game]].

> [!remark] Notation in the literature
> - `[KL §10.3]` writes the experiment $\mathsf{KE}^{\mathsf{eav}}_{\mathcal A, \Pi}(n)$: both parties run $\Pi$ on $1^n$; a uniform bit $b$ selects the real key ($b = 0$) or a uniform $\hat k \in \{0, 1\}^n$ ($b = 1$); $\mathcal A$ gets the transcript and $\hat k$, outputs $b'$, and the experiment outputs $1$ iff $b' = b$. Security there is $\Pr[\mathsf{KE}^{\mathsf{eav}}_{\mathcal A, \Pi}(n) = 1] \leq 1/2 + \mathsf{negl}(n)$. That bit-guessing advantage $|\Pr[b' = b] - 1/2|$ is half of $\mathsf{Adv}^{\mathsf{eav}}_P$, see [[knowledge/cryptography/primitive/public-key encryption/property/Indistinguishability under Chosen-Plaintext Attack#Bit-guessing form\|Indistinguishability under Chosen-Plaintext Attack#Bit-guessing form]].
> - Real-or-random security implies security against an eavesdropper in the guessing sense above when $|\mathcal K|$ is super-polynomial: from a guesser $\mathcal A$, a distinguisher runs $\mathcal A$ on $T_P$ and outputs $1$ iff the guess equals $\hat k$. It outputs $1$ with probability $\mathsf{Adv}^{\mathsf{ke}}_P(\mathcal A)$ in Game 0 and $1/|\mathcal K|$ in Game 1.

## Related

### Instantiations
- [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Diffie-Hellman Key Exchange\|Diffie-Hellman Key Exchange]] — $g^\alpha$, $g^\beta$, and the key $g^{\alpha\beta}$; secure under DDH with authenticated links
- [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Merkle Puzzles\|Merkle Puzzles]] — from a block cipher with a small key space; only a quadratic gap

### Constructions
- [[knowledge/cryptography/primitive/key establishment/key exchange/Key Exchange from Trapdoor Function\|Key Exchange from Trapdoor Function]] — any one-way trapdoor function gives a key exchange secure against an eavesdropper
- [[knowledge/cryptography/primitive/key establishment/key exchange/Key-Exchange Authenticator\|Key-Exchange Authenticator]] — compiles a protocol secure with authenticated links into an authenticated key exchange

### Siblings
- [[knowledge/cryptography/primitive/key establishment/key exchange/Authenticated Key Exchange\|Authenticated Key Exchange]] — many parties, identities, and an adversary who controls the network
- [[knowledge/cryptography/primitive/key establishment/kem/Key Encapsulation Mechanism\|Key Encapsulation Mechanism]] — the one-message shape: encapsulate a key under the receiver's public key

### Prerequisites
- [[knowledge/cryptography/foundations/Security Game\|Security Game]], [[knowledge/cryptography/foundations/Adversary\|Adversary]], [[knowledge/cryptography/cryptanalysis/Man-in-the-Middle Attack\|Man-in-the-Middle Attack]]
