---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof/scheme/schnorr-protocol/","dg-note-properties":{}}
---

## Scheme

> [!scheme] Schnorr Protocol
> ### Parameters
> - $g$ is the generator of group $\mathbb G$.
> - $p$ is the order of the group.
> 
> ---
> ### Statement
> The prover want to convince the verifier that given a public value $h$, he knows a value $x$ such that:
> $$x = g^h$$
> 
> ---
> ### Scheme
> $$\begin{array}{lcl} 
\textbf{Prover} & & \textbf{Verifier} \\[4pt] 
(x = \log_g h) & & \\[6pt] 
r \xleftarrow{\$} \mathbb{Z}_p & & \\[6pt] 
a \leftarrow g^r & \xrightarrow{a} & \\[6pt] 
& \xleftarrow{\quad e \quad} & e \xleftarrow{\$} \mathbb{Z}_p \\[6pt]
\sigma \leftarrow ex + r & \xrightarrow{\sigma} & g^{\sigma} \stackrel{?}{=} h^{e} a 
\end{array}$$
> If any check fails, $\text{reject}$.

## Property

### Completeness

> [!property] Perfect Completeness
> If $\sigma = ex + r \mod p$, then $g^\sigma = g^{ex + r} = (g^x)^e g^r = h^e a$.

## Security

### Knowledge (Special) Soundness

> [!security] Knowledge Soundness
> 

### Honest-Verifier Zero-Knowledge

> [!security]
> Simulator $\text{Sim}$ work as follows:
> - 