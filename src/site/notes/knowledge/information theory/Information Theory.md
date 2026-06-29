---
{"dg-publish":true,"permalink":"/knowledge/information-theory/information-theory/","dg-note-properties":{}}
---


## Perfect Secrecy

> [!definition] Perfect Secrecy
> A cryptosystem has **perfect secrecy** if $$f(m | c) = f_M(m) \quad \forall m \in \mathcal M \text{ and all } c \in \mathcal C.$$
> With $f(m | c)$ is the conditional probability density of the ciphertext space and plaintext space.

> [!remark]
> For decryption function $d_k: \mathcal C \rightarrow \mathcal M$ for the key $k \in K$ with $f_K$ is the density function for the key space and $f_{\mathcal M}$ is the density function for the message space: $$f_{C}(c) = \sum_{k \in \mathcal K} f_K(k) f_M(d_k(c)).$$

> [!proposition]
> If a cryptosystem has **perfect secrecy**, then $\# \mathcal K \geq \# \mathcal M.$

> [!theorem]
> Suppose that a cryptosystem satisfies $$\# \mathcal K = \# \mathcal M = \# \mathcal C,$$
> i.e., the numbers of keys, plaintexts, and ciphertexts are all equal. Then the system has perfect secrecy if and only if the following two conditions hold:
> 1. Each key $k \in \mathcal K$ is used with equal probability
> 2. For a given message $m \in \mathcal M$ and ciphertext $c \in \mathcal C$, there is exactly one key $k \in \mathcal K$ that encrypts $m$ to $c$.

> [!definition] Key equivocation
> When $X = K$ is the key random variable and $Y = C$ is the ciphertext random variable, the quantity $H(K \mid C)$ is called the **key equivocation**. It measures the total amount of information about the key revealed by the ciphertext, or more precisely, it is the expected value of the conditional entropy $H(K \mid c)$ of $K$ given a single observation $c$ of $C$. This quantity can be found by the formula $$H(K \mid C) = H(K) + H(M) - H(C)$$


## Entropy

> [!definition] Entropy
> **Entropy** quantify the uncertainly of the outcome of an experiment. The outcome of the experiment are described by a random variable $X$ that takes on finitely many values $x_1, x_2, \cdots, x_n$ and we have $p_1, p_2, \cdots, p_n$ for the associated probabilities: $$p_i = f_X(x_i) = \Pr(X = x_i).$$
> The **entropy** $H(X)$ of $X$ is a number that depends only on the probabilities $p_1, \cdots, p_n$ of the possible outcomes of $X$: $$H(X) = H(p_1, \cdots, p_n).$$ 
> This function should possess property:
> - Property $H_1$: The function $H$ should be continuous in the variable $p_i$. 
> This reflects the intuition that a small change in $p_i$ should produce a small change in the amount of information revealed by $X$.
> - Property $H_2$: Let $X_n$ be the random variable that is uniformly distributed on a set $\{x_1, \dots, x_n\}$, i.e., the random variable $X_n$ has $n$ possible outcomes, each occurring with probability $\frac{1}{n}$. Then $H(X_n)$ should be a monotonically increasing function of $n$. 
> This reflects the intuition that if all events are equally likely, then the uncertainty increases as the number of events increases.
> - Property $H_3$: If an outcome of $X$ is thought of as a choice, and if that choice can be broken down into two successive choices, then the original value of $H$ should be a weighted sum of the values of $H$ for the successive choices. In particular, writing $X_n$ for a uniformly distributed random variable on $n$ objects, we should have $$H(X_{n^r}) = r \cdot H(X_n)$$

> [!theorem] 
> Every function having Properties $H_1$, $H_2$, and $H_3$ is a constant multiple of the function $$H(p_1, \cdots, p_n) = - \sum_{i = 1}^n p_i \log_2 p_i,$$ where $\log_2$ denotes the logarithm to the base 2, and if $p = 0$, then we set $p \log_2 p = 0.$ 

> [!corollary]
> Let $X$ be an experiment (a random variable). Then
> 1. $H(X) \leq \log_2 n.$
> 2. $H(X) = \log_2 n$ if and only if every outcome (every individual event $x_i$) occurs with the same probability $\frac{1}{n}$.

> [!definition] Equivocation
> Let $X$ and $Y$ be random variables, and let $x_1, \dots, x_n$ be the possible values of $X$ and $y_1, \dots, y_m$ the possible values of $Y$. The **equivocation (or conditional entropy)** of $X$ on $Y$ is the quantity $H(X \mid Y)$ defined by $$H(X \mid Y) = -\sum_{i = 1}^n \sum_{j = 1}^m f_Y(y_j) f_{X | Y}(x_i \mid y_j) \log_2 f_{X | Y}(x_i \mid y_j).$$

## Redundancy and the entropy of natural language

> [!definition]
> Let $\text{L}$ be a language (e.g., English or French or C++), and for each $n \leq 1$, let $L^n$ denote the random variables whose values are strings of $n$ consecutive characters of $\text{L}$. The entropy of $\text{L}$ is defined to be the quantity $$H(\text{L}) = \lim_{n \rightarrow \infty} \frac{H(L^n)}{n}.$$

## The algebra of secrecy systems

> [!definition] Summation Systems
> If $R$ and $T$ are two secrecy systems, then the **weighted sum** of $R$ and $T$ is $$S = pR + qT, \quad \text{where } p + q = 1.$$

