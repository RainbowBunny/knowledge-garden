---
{"dg-publish":true,"permalink":"/knowledge/math/probability/continuous-probability/distribution/discrete-gaussian-distribution/","dg-note-properties":{}}
---

Reference: https://eprint.iacr.org/2022/1690.pdf

## Basic Definition

### Probability Mass Function

> [!definition] PMF of Discrete Gaussian Distribution
> Given a [[knowledge/math/algebra/structures/lattices/Lattices#Basic Definition\|Lattice]] $\Lambda \subseteq \mathbb R^n$, a parameter $r$ and a vector $\mathbf{c} \in \mathbb R^n$, the discrete Gaussian distribution with parameter $r$ and support $\Lambda + \mathbf{c}$ is defined as
> $$\mathcal D_{\Lambda + \mathbf{c}, r}(\mathbf{x}) = \frac{\rho_r(\mathbf{x})}{\rho_r(\Lambda + \mathbf{c})} \forall x \in \Lambda + \mathbf{c}$$
> where $\rho$ is the [[knowledge/math/algebra/structures/set theory/functions/Unnormalized Gaussian Function#Basic Definition\|Unormalized Gaussian Function]].

## Property

### Tail Bound

> [!lemma] Sharp Norm Tail Bound
> For $r > 0, n \geq 1$ and $k > 1$, we have
> $$\Pr_{\mathbf{z} \leftarrow \mathcal D_{\mathbb Z^n}, r}\left [||\mathbf{z}|| > kr \sqrt{n / (2 \pi)}\right ] < k^n \cdot \exp(n/2 \cdot (1 - k^2))$$

> [!lemma] Lattices Tail Bound
> For $\epsilon \in (0, 1), r \geq \eta_\epsilon(\Lambda)$ (smoothing parameter), and $\mathbf{c} \in \mathbb R^n$, we have
> $$\Pr_{\mathbf{z} \leftarrow \mathcal D_{\Lambda + \mathbf{c}, \mathbf{r}}} \left [ ||\mathbf{z}|| > r \sqrt{n} \right ] \leq (1 + \epsilon) / (1 - \epsilon) \cdot 2^{-n}$$

> [!lemma] Directional Tail Bound
> For $\mathbf{v} \in \mathbb R^n, t > 0$, we have that
> $$\Pr_{\mathbf{z} \leftarrow \mathcal D_{\mathbb Z^n, r}} \left [ |\langle \mathbf{v}, \mathbf{z} \rangle | > t \cdot r||\mathbf{v}|| \right ] \leq 2 \exp(-\pi t^2)$$

