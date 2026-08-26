---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof/scheme/kilian-interactive-argument-of-knowledge-from-pcp/","dg-note-properties":{}}
---

## Scheme

> [!scheme] Kilian Interactive Argument of Knowledge from PCP
> ### Parameters
> 
> 
> ---
> ### Statement
> Given a statement $x \in \mathcal L$
> 
> ---
> ### Scheme
> $$\begin{array}{lcl} 
\textbf{Prover} & & \textbf{Verifier} \\[4pt] 
(w, \pi) & & \\[6pt] 
r \xleftarrow{\$} \mathbb{Z}_p & & \\ 
a \leftarrow g^r & \xrightarrow{\quad a \quad} & \\[6pt] 
& \xleftarrow{\quad e \quad} & e \xleftarrow{\$} \mathbb{Z}_p \\[6pt]
\sigma \leftarrow ex + r & \xrightarrow{\quad \sigma \quad} & g^{\sigma} \stackrel{?}{=} h^{e} a 
\end{array}$$
