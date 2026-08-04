---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/encoding-scheme/encoding-scheme/","dg-note-properties":{}}
---

## Syntax

> [!definition] Encoding Scheme
> An encoding scheme $\text{Enc}$ over a field $\mathbb F$ is composed of the following algorithms:
> - $(pk, sk) \leftarrow \text{Gen}()$: Key generation algorithm that takes as input some security parameter and outputs some secret state $sk$ together with some public information $pk$.
> - $z \leftarrow \text{Enc}(s)$: Encoding algorithm mapping a field element $s$ to some encoding value. Depending on the algorithm, $\text{Enc}$ will require $\text{pk}$ or $\text{sk}$.

## Property

### Additive Homomorphic

> [!definition] Additive Homomorphic
> We want the encoding scheme to behave well when applying linear operations
> $$\text{Enc}(x + y) = \text{Enc}(x) + \text{Enc}(y).$$

### Quadratic Root Detection

> [!definition] Quadratic Root Detection
> There exists an efficient algorithm $\{0, 1\} \leftarrow \text{Alg}(pp, (\text{Enc}(a_0), \dots, \text{Enc}(a_t)))$: That checks
> $$pp(a_1, \dots, a_t) \stackrel{?}{=} 0$$


