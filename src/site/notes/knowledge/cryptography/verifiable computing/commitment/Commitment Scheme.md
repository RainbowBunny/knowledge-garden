---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/commitment/commitment-scheme/","dg-note-properties":{}}
---

## Syntax

> [!definition] Commitment Scheme
> A **commitment scheme** for a finite message space $\mathcal M$, is a pair of efficient algorithms $\mathcal C = (\text{Com}, \text{Verify})$ where:
> - Algorithm $\text{Com}$ is invoked as $(c, o) \xleftarrow{\$} \text{Com}(m)$, where $m \in \mathcal M$ is the message to be committed, $c$ is the commitment string, and $o$ is an opening string.
> - Algorithm $\text{Verify}$ is a deterministic algorithm invoked as $\text{Verify}(m, c, o)$ and output $\text{accept}$ or $\text{reject}$.

> [!definition] Commitment Phases
> - Commit Phase: Sender runs $(c, o) \xleftarrow{\$} \text{Com}(m)$ and sends $c$.
> - Reveal Phase: Sender sends $(m, o)$; receiver runs $\text{Verify}(m, c, o)$.

## Property

### Correctness

> [!definition] Correctness
> For all $m \in \mathcal M$:
> $$\Pr\!\left[
> \begin{array}{l}
> \text{Verify}(m, c, o) = \text{accept}
> \end{array}
> \; \middle | \; 
> \begin{array}{l}
> (c, o) \leftarrow \text{Com}(m)
> \end{array} \right] = 1$$

## Security

### Binding

> [!definition] Binding
> For any adversary $\mathcal A^\text{find}$, we define the binding advantage:
> $$\text{Adv}_{\mathcal C}^\text{Bind}(\mathcal A) =  
> \; \Pr\!\left[
> \begin{array}{l}
> m_1 \neq m_2 \\
> c_1 = c_2
> \end{array}
> \; \middle | \; 
> \begin{array}{l}
> (m_1, m_2) \leftarrow \mathcal A^\text{find}() \\
> (c_1, o_1) \leftarrow \text{Com}(m_1) \\
> (c_2, o_2) \leftarrow \text{Com}(m_2)
> \end{array} \right]$$

### Hiding

> [!definition] Hiding
> For any adversary $\mathcal A = (\mathcal A_\text{find}, \mathcal A_\text{guess})$, we define the hiding advantage:
> $$\text{Adv}_{\mathcal C}^{\text{Hide}}(\mathcal A) = 
> \left|\; \Pr\!\left[ b = b' \;\middle |\; 
> \begin{array}{l}
> (m_0, m_1, s) \leftarrow \mathcal A_\text{find}(); \\
> b \xleftarrow{\$} \{0, 1\}; (c^*, o^*) \xleftarrow{\$} \text{Com}(m_b) \\
> b' \leftarrow \mathcal A_\text{guess}(s, c^*)
> \end{array} \right] 
> \;- \frac{1}{2}
> \right|.$$

