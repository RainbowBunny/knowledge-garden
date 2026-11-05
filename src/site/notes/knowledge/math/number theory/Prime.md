---
{"dg-publish":true,"permalink":"/knowledge/math/number-theory/prime/","dg-note-properties":{}}
---

## Prime Numbers

> [!definition] Prime
>  An integer $p$ is called a **prime** if $p \geq 2$ and if the only positive integers dividing $p$ are $1$ and $p$.

> [!remark]
> $\text{COMPOSITES} = \{x | x = pq, \text{ for integer } p, q > 1\}$ is in [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]]

> [!proposition] 
Let $p$ be a prime number, and suppose that $p$ divides the product $ab$ of two integers $a$ and $b$. Then $p$ divides at least one of $a$ and $b$. More generally, if $p$ divides a product of integers: $$p \mid a_1 a_2 \cdots a_n$$then $p$ divides at least one of the individual $a_i$.

> [!proposition]
> Let $\{p_1, p_2, \dots, p_r\}$ be a set of prime numbers, and let $$N = p_1 p_2 \cdots p_r + 1.$$ We know that $N$ is divisible by some prime not in the original set. Thus, there must be infinitely many prime numbers.

## Unique Factorization and Order

> [!theorem] The Fundamental Theorem of Arithmetic
>  Let $a \geq 2$ be an integer. Then $a$ can be factored as a product of prime numbers $$a = p_1^{e_1} \cdot p_2^{e_2} \cdot p_3^{e_3} \cdots p_r^{e_r}.$$Further, other than rearranging the order of the primes, this factorization into prime powers is unique.

> [!definition] Order of $p$ in $a$
>  When we factor $a$ into primes, each prime $p$ appears to a particular power. We denoted this power by $\text{ord}_p(a)$ and call it the **order (or exponent)** of $p$ in $a$. Thus, we can write: $$a = \prod_{\text{primes } p} p^{\text{ord}_p(a)}.$$ 

> [!proposition]
> Let $p$ be a prime number, the $\text{ord}_p$ has the following properties:
> 1. $\text{ord}_p(ab) = \text{ord}_p(a) + \text{ord}_p(b)$.
> 2. $\text{ord}_p(a + b) \geq \min \{\text{ord}_p(a), \text{ord}_p(b)\}$.
> 3. If $\text{ord}_p(a) \neq \text{ord}_p(b)$, then $\text{ord}_p(a + b) = \min \{\text{ord}_p(a), \text{ord}_p(b)\}.$

> [!remark]
> The first property resembles the logarithm function, since it converts multiplication into addition.
> A function satisfying the first two properties is called a **valuation**. 

## Power and Primitive Roots in Finite Fields

> [!theorem] Fermat's Little Theorem
>  Let $p$ be a prime number and let $a$ be any integer. Then $$a^{p - 1} \equiv \begin{cases}
1 \pmod p \quad \text{if } p \nmid a, \\
0 \pmod p \quad \text{if } p \mid a.
\end{cases}$$

> [!theorem] Fermat's Little Theorem, Version 2
> Let $p$ be a prime number. Then $$a^p \equiv a \pmod p \quad \forall a \in \mathbb Z$$

Specializes [[knowledge/math/algebra/structures/group/Group Order\|Group Order]] — the order of $a$ as an element of $\mathbb F_p^* = (\mathbb Z / p\mathbb Z)^*$.

> [!proposition] Order of $a$ modulo $p$
>  Let $p$ be a prime and let $a$ be an integer not divisible by $p$. Suppose that $a^n \equiv 1 \pmod p$. Then the order of a module $p$ divides $n$. In particular, the order of $a$ divides $p - 1$.

> [!proposition]
> Suppose that $g^a \equiv 1 \pmod m$ and that $g^b \equiv 1 \pmod m$. Then, $$g^{\gcd(a, b)} \equiv 1 \pmod m.$$

> [!theorem] Primitive Root Theorem
>  Let $p$ be a prime number. Then there exists an element $g \in \mathbb F_p^*$ whose powers give every element of $\mathbb F_p^{*}$: $$\mathbb F_p^* = \{1, g, g^2, g^3, \dots, g^{p - 2}\}$$Elements with this property are called primitive roots of $\mathbb F_p$ or generators of $\mathbb F_p^*$. They are the element of $\mathbb F_p^*$ having order $p - 1$.

> [!remark]
>  If $k$ divides $p - 1$, then there are exactly $\phi(k)$ elements of $\mathbb F_p^*$ having order $k$.

> [!example]
> Let $p$ be a prime and let $q$ be a prime that divides $p - 1$. For $a \in \mathbb F_p^*$ and let $b = a^{(b - 1)/q}$ then either $b = 1$ or $b$ has order $q$.

> [!example]
> Let $p$ be a prime such that $q = \frac{1}{2}(p - 1)$ is also prime. Suppose that $g$ is an integer satisfying $$g \equiv \pm 1 \pmod p \quad \text{and} \quad g^q \equiv 1 \pmod p.$$ Then $g$ is a primitive root modulo $p$.

## Unit and Inverse

> [!proposition] 
> Let $p$ be a prime. Then every nonzero element $a$ in $\mathbb Z / p \mathbb Z$ has a multiplicative inverse, that is, there is a number $b$ satisfying $ab \equiv 1 \pmod p$. We denoted this value of $b$ by $a^{-1} \pmod p$, or if $p$ has already been specified then simply $a^{-1}$.

> [!definition]
If $p$ is prime, then the set $\mathbb Z / p \mathbb Z$ of integers modulo $p$ with its addition, subtraction, multiplication, and division rules is a **finite field**. This finite field is often denoted as $\mathbb F_p$. Similarly, we write $\mathbb F_p^*$ interchangeably for the group of units $(\mathbb Z / p \mathbb Z)^*.$

> [!remark] Method for calculating inverse 
>1. $au + bp = 1 \pmod p$ then $a^{-1} = u \pmod p$.
>2. $a^{-1} \equiv a^{p - 2} \pmod p$.

> [!example]
> Let $m \in \mathbb Z$ and suppose that $m \equiv 1 \pmod b$. Then, $b^{-1} = \frac{1 - m}{b} \pmod m$.

Specializes [[knowledge/math/algebra/structures/ring/Ring#Unit\|Unit]] to the ring $\mathbb Z / m\mathbb Z$.

> [!definition] Units and Group of Units
>  Numbers that have inverses are called **units**. We denoted the **set of all units** by $$\begin{align}
(\mathbb Z / m \mathbb Z)^* &= \{a \in \mathbb Z / m\mathbb Z : \gcd(a, m) = 1\} \\
 &= \{a \in \mathbb Z / m \mathbb Z : a \text{ has an inverse modulo } m\}\end{align}$$The set $(\mathbb Z / m \mathbb Z)^*$ is called the **group of units modulo** $m$.

> [!proposition]
> If $a_1$ and $a_2$ are units modulo $m$, then $a_1 a_2$ is a unit modulo $m$.

## Miller-Rabin Primality Testing

> [!definition] Witness for Compositeness
> Fix an integer $n$. We say that an integer $a$ is a **witness** for (the compositeness) of $n$ if $$a^n \not\equiv a \pmod n.$$

> [!definition] Carmichael Numbers
> Composite numbers having no witnesses.

> [!proposition] 
> Let $p$ be an odd prime and write $$p - 1 = 2^k q \quad \text{with } q \text{ odd}$$
> Let $a$ be any number not divisible by $p$. Then one of the following two condition is true:
> 1. $a^q$ is congruent to $1$ modulo $p$.
> 2. One of $a^q, a^{2q}, a^{4q}, \dots, a^{2^{k - 1}q}$ is congruent to $-1$ modulo $p$.

> [!definition] Miller-Rabin witness
> Let $n$ be an odd number and write $n - 1 = 2^k q$ with $q$ odd. An integer $a$ satisfying $\gcd(a, n) = 1$ is called a **Miller-Rabin witness for (the compositeness of)** $n$ if both of the following condition is true:
> 1. $a^q \not\equiv 1 \pmod n$
> 2. $a^{2^i q} \not\equiv -1 \pmod n$ for all $i = 0, 1, 2, \dots, k - 1.$

> [!algorithm] Miller–Rabin Witness Test
> **Input:** An integer $n$ to be tested, and an integer $a$ as a potential witness  
> **Output:** `Composite` or `Test Fails`
>
>---
>
> 3. If $n$ is even or
>    $$1 < \gcd(a, n) < n,$$
>    return `Composite`.
>
> 4. Write:
>    $$n - 1 = 2^k q,$$
>    where $q$ is odd.
>
> 5. Compute:
>    $$a \gets a^q \pmod n.$$
>
> 6. If
>    $$a \equiv 1 \pmod n,$$
>    return `Test Fails`.
>
> 7. For $i = 0, 1, 2, \ldots, k - 1$, do:
>
>    5.1. If
>    $$a \equiv -1 \pmod n,$$
>    return `Test Fails`.
>
>    5.2. Set:
>    $$a \gets a^2 \pmod n.$$
>
> 8. Return `Composite`.

> [!proposition]
> Let $n$ be an odd composite number. Then at least $75\%$ of the numbers $a$ between $1$ and $n - 1$ are Miller-Rabin witness for $n$.

## AKS Primality Test

> [!theorem] AKS Primality Test
> For every $\epsilon > 0$, there is an algorithm that conclusively determines whether a given number $n$ is prime in no more than $O((\ln n)^{6 + \epsilon})$ 

## The distribution of the set of primes

> [!definition] $\pi$ function
> For any number $X$, let $$\pi(X) = (\# \text{ of primes } p \text{ satisfying } 2 \leq p \leq X).$$

> [!theorem] The Prime Number Theorem
> $$\lim_{X \rightarrow \infty} \frac{\pi(X)}{X / \ln (X)} = 1$$

> [!proposition]
> Fix two number $c_1$ and $c_2$ satisfying $c_1 < c_2$. Bob chooses random numbers $n$ in the interval $c_1 N \leq n \leq c_2 N$. Keeping $c_1$ and $c_2$ fixed, let $$P(c_1, c_2; N) = [\text{Probability that an integer } n \text{ in the interval } c_1 N \leq n \leq c_2 N \text{ is a prime number}].$$ Then, $$\lim_{N \rightarrow \infty} \frac{P(c_1, c_2; N)}{1 / \ln N} = 1$$

> [!proposition]
> Riemann hypothesis is equivalent to the following more accurate statement:
> $$\pi(X) = \int_2^X \frac{dt}{\ln t} + \mathcal O(\sqrt{X} \cdot \ln (X))$$
> So because of the properties of the [[knowledge/math/number theory/Prime#Logarithmic Integral\|Logarithmic Integral]], we have $\pi(X) = X / \ln X$

> [!example]
> $$\Pr(N \text{ primes } \mid N \equiv k \pmod m) \approx \frac{m}{\phi(m) \ln N}$$

## Mersenne Prime

> [!definition] Mersenne Prime
> A prime of the form $2^n - 1$ is called a **Mersenne prime**.

> [!proposition]
> If $n$ is a composite number, then $2^n - 1$ is not prime. Thus all Mersenne primes have the form $2^p - 1$ with $p$ a prime number.

## Prime Function

### Von Mangoldt Function

> [!definition] Von Mangoldt Function
> $$\Lambda := \begin{cases}\log p &\text{if } n = p^m \text{ , where } p \text{ is prime} \\ 0 &\text{otherwise}\end{cases}$$

### Lambda Function

> [!definition] Lambda Function
> **Lambda Function** define by a modification of Euler's $\phi$-function:
> 1. $\lambda(p^a) = \phi(p^a)$ when $p$ is an odd prime;
> 2. $\lambda(2^a) = \phi(2^a)$ if $a = 0, 1,$ or $2$;
> 3. $\lambda(2^a) = \frac{1}{2} \phi(2^a)$ if $a > 2$;
> 4. $\lambda(2^a p_1^{a_1} \cdots p_i^{a_i}) = \text{the lowest common multiple of } \lambda(2^a), \lambda(p_1^{a_1}), \cdots, \lambda(p_i)^{a_i}$ with $p_1, \cdots, p_i$ being different odd primes.

### Logarithmic Integral 

> [!definition] Logarithmic Integral Function
> $$\text{Li}(X) = \int_2^X \frac{dt}{\ln t}$$

> [!proposition] Properties of Logarithmic Integral Function
> 1. $\text{Li}(X) = \frac{X}{\ln X} + \int_2^X \frac{dt}{(\ln t)^2} + O(1)$
> 2. $\lim_{X \rightarrow \infty} \frac{\text{Li}(X)}{X / \ln X} = 1$
