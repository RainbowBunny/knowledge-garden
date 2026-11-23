---
{"dg-publish":true,"permalink":"/knowledge/complexity/foundations/sub-exponential-function/","dg-note-properties":{"aliases":["Subexponential","Sub-Exponential"]}}
---

## Definition

> [!definition] Sub-Exponential Function
> A function $f(X)$ is **sub-exponential** if
> 1. $f(X) = \Omega((\ln X)^\alpha)$ for some $\alpha > 0$;
> 2. $f(X) = O(X^\beta)$ for every $\beta > 0$.
>
> ⚠️ Source not recorded; this definition came from the old `Time Complexity` note.

> [!remark] Read it in the bit length
> Here $X$ is the numeric value of the input, as for an integer to be factored, so the input length is $n \approx \log X$. Condition 2 says $f(X) = X^{o(1)} = 2^{o(n)}$, and condition 1 says $f$ is at least polynomial in $n$: sub-exponential means between polynomial and exponential **in the bit length**. This is the sense of $2^{o(n)}$ in the [[knowledge/complexity/conjectures/Exponential Time Hypothesis\|Exponential Time Hypothesis]].

## Example

> [!example] The $L$-notation of index calculus
> $L_X[1/3, c] = \exp\big((c + o(1)) (\ln X)^{1/3} (\ln \ln X)^{2/3}\big)$ is sub-exponential: it is $X^{o(1)}$ and grows faster than every power of $\ln X$. It is the running time of the number field sieve and of [[knowledge/cryptography/cryptanalysis/dlp/Index Calculus\|index-calculus]] variants.

## Related

### Siblings
- [[knowledge/complexity/complexity class/generator/time/Class DTIME\|Class DTIME]] — the polynomial and exponential bounds this sits between
