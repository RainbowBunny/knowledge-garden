---
{"dg-publish":true,"permalink":"/knowledge/cryptography/pseudorandom/functions/puncturable-pseudorandom-function/","dg-note-properties":{}}
---

## Syntax

> [!definition] Puncturable Pseudorandom Function
> A puncturable pseudorandom function (PPRF) is defined to be a triple of [[daily/Temp/PPT\|PPT]] algorithms $\text{PPRF} = (\text{Gen}, \text{Puncture}, \text{Eval})$ with the following syntax:
> - $k \leftarrow \text{Gen}(1^n, 1^{d(n)})$: takes as input the security parameter $1^n$, an input length $1^{d(n)}$ and outputs a key $k$.
> - $k_X \leftarrow \text{Puncture}(k, X)$: takes an input a key $k$ and a polynomial size set $\emptyset \neq X \subseteq D = \{0, 1\}^{d(n)}$ and outputs a punctured key $k_X$.
> - $r \leftarrow \text{Eval}(k, x)$: is deterministic, takes a key $k$ and an element $x \in \mathcal D$ as input and outputs an element $r \in \mathcal R = \{0, 1\}^{r(n)}$.

## Property

### Completeness of Puncturing

> [!definition] Completeness of Puncturing
> For any $d(n) = \text{poly}(n), X \subseteq \{0, 1\}^{d(n)}$, any $k \in \text{Gen}(1^n, 1^{d(n)})$, any $k_X \in \text{Puncture}(k, X)$ and any $x' \notin X$ we have $\text{Eval}(k, x') = \text{Eval}(k_X, x')$.

## Security

### Pseudorandomness

> [!security] Pseudorandomness
> For any $d(n) = \text{poly}(n)$ and any [[daily/Temp/PPT\|PPT]] algorithm $\mathcal A$ the following is negligible: 
> $$\left|\; 
> \Pr\!\left[ \mathcal{A}(St, k_X, (r_x)_{x \in X}) = 1 \;\middle|\; 
> \begin{array}{l} 
> (X, St) \leftarrow \mathcal{A}(1^n),\; k \leftarrow \mathsf{Gen}(1^n, 1^{d(n)}),\\ 
> k_X \leftarrow \mathsf{Puncture}(k, X),\\ 
> r_x := \mathsf{Eval}(k, x) \text{ for } x \in X 
> \end{array} \right] 
> \;-\; 
> \Pr\!\left[ \mathcal{A}(St, k_X, (r_x)_{x \in X}) = 1 \;\middle|\; 
> \begin{array}{l} 
> (X, St) \leftarrow \mathcal{A}(1^n),\; k \leftarrow \mathsf{Gen}(1^n, 1^{d(n)}),\\ 
> k_X \leftarrow \mathsf{Puncture}(k, X),\\ 
> r_x \leftarrow_{\$} \{0,1\}^{r(n)} \text{ for } x \in X 
> \end{array} \right] \;
> \right|.$$
