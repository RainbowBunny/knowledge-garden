---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/groups/group/","dg-note-properties":{}}
---

## Definition

>[!definition] Group
A **group** consists of a nonempty set $G$ and a rule, which we denote by $\star: G \times G \rightarrow G$ satisfying [[knowledge/math/properties/operation/Associativity\|Associativity]], [[knowledge/math/properties/operation/Identity Element\|Identity Element]], [[knowledge/math/properties/operation/Inverse Element\|Inverse Element]].

> [!definition] Group (Alternative)
> Alternatively, a group is a [[knowledge/math/algebra/structures/Monoid\|Monoid]] with [[knowledge/math/properties/operation/Inverse Element\|Inverse Element]].

### Order

> [!definition] Order of a Group
> The **order of** $G$ is the number of elements in $G$; it is denoted by $|G|$ or $\# G$. We write $|G| = \inf$ if $G$ is infinite.

> [!definition] Order of a Group Element
> Let $G$ be a group and let $g \in G$ be an element of the group. Suppose there exists a positive integer $n$ with the property that $g^n = e$. The smallest such $n$ is called the **order of** $g$. If there is no such $n$, then $g$ is said to have **infinite order**. We denote the order of the element as $|g|$.
> Also, if $G$ is a finite group, $|g| \mid |G|$.

>[!proposition]
>Let $G$ be a finite group. Then every element of $G$ has finite order. Further, if $g \in G$ has order $n$ and if $g^k = e$, then $n \mid k$.

> [!proposition]
> Let $g \in G$ be an element of finite order. Then $g^m$ has finite order $\forall m \geq 0$, and in fact
> $$|g^m| = \frac{\text{lcm}(m, |g|)}{m} = \frac{|g|}{\gcd(m, |g|)}$$

> [!proposition]
> If $gh = hg$, then $|gh|$ divides $\text{lcm}(|g|, |h|)$.

## Property

### Identity

> [!proposition] Uniqueness of Identity
> If $h \in G$ is an identity of $G$, then $h = e_G$.

### Inverse

> [!proposition] Uniqueness of Inverse
> If $h_1, h_2$ are both inverses of $g$ in $G$, then $h_1 = h_2$.

> [!proposition] Inverse of Product
> $$\forall g, h \in G, \quad (gh)^{-1} = h^{-1} g^{-1}$$

### Cancellation

> [!proposition]
> Let $(G, \cdot)$ be a group, [[knowledge/math/properties/operation/Cancellativity\|Cancellativity]] for $\cdot$ holds. 

## Example

> [!example]
> Each of the following is a group:
> 1. $\text{GL}_n(\mathbb R) = \{n\text{-by-}n \text{ matrices } A \text{ with real coefficients and } \det(A) \neq 0\}$ with operation $\star$ is matrix multiplication.

> [!definition] General Linear Group
> The **General Linear Group** of order $s$, denoted $\text{GL}_s(\mathbb Z_n)$, is the monoid of invertible $s \times s$ matrices containing elements from $\mathbb Z_n$ with respect to multiplication such that the determinants of the matrices and $n$ are relatively prime.

> [!theorem]
> The order of the General Linear Group $\text{GL}_2(\mathbb Z_p)$ is given by $$|\text{GL}_2(\mathbb Z_p)| = (p^2 - 1)(q^2 - 1),$$ where $p$ is a prime integer.

> [!lemma]
> Let $n = pq$ where $p$ and $q$ are distinct prime integers. If $M \in \text{GL}_2(\mathbb Z_n)$, then $M \in \text{GL}_2(\mathbb Z_p)$ and $M \in \text{GL}_2(\mathbb Z_q)$. 
 