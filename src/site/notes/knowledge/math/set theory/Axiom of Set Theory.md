---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/axiom-of-set-theory/","dg-note-properties":{}}
---

Reference:
- [[academic/Book Reference\|Element of Set Theory]] - Chapter 2: Axioms and Operations, Section: Axioms.

## Definition

### Extensionality Axiom

> [!definition] Extensionality Axiom
> If two sets have exactly the same members, then they are equal:
> $$\forall A \; \forall B [\forall x (x \in A \iff x \in B) \implies A = B].$$

### Empty Set Axiom

> [!definition] Empty Set Axiom
> There is a set having no members.
> $$\exists B \; \forall (x \; x \notin B).$$

### Pairing Axiom

> [!definition] Pairing Axiom
> For any sets $u$ and $v$, there is a set having as members just $u$ and $v$:
> $$\forall u \; \forall v \; \exists B \; \forall x (x \in B \iff x = u \lor x = v).$$

### Union Axiom

> [!definition] Union Axiom (Preliminary Form)
> For any set $a$ and $b$, there is a set whose members are those sets belonging either to $a$ or to $b$ (or both):
> $$\forall a \; \forall b \; \exists B \; \forall x (x \in B \iff x \in A \lor x \in B).$$

### Power Set Axiom

> [!definition] Power Set Axiom
> For any set $a$, there is a set whose member are exactly the subsets of $a$:
> $$\forall a \; \exists B \; \forall x (x \in B \iff x \subseteq a).$$

### Subset Axiom

> [!definition] Subset Axiom (Aussonderung Axiom)
> For each formula $\varphi$, the following is an axiom:
> $$\forall t_1 \cdots \forall t_k \; \forall c \; \exists B \; \forall x(x \in B \iff x \in c \land \varphi(x, t_1, \dots, t_k))$$

### Union Axiom

> [!definition] Union Axiom
> For any set $A$, there exists a set $B$ whose elements are exactly the members of the members of $A$:
> $$\forall x [x \in B \iff (\exists b \in A) \; x \in b].$$

## Property

### Russell's Paradox

> [!theorem] Russell's Paradox
> There is no set to which every set belongs.
> 
> ---
> Let $R = \{x \;|\; x \notin x\}$. Then $R \in R \Longleftrightarrow R \notin R$.
