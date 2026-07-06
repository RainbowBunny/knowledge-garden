---
{"dg-publish":true,"permalink":"/academic/literature/","dg-note-properties":{}}
---


# Literature

Paper index, grouped by area. Rows marked ★ are canonical high-impact papers added as reading anchors; unmarked rows are the working collection. Detailed notes for read papers live in `academic/paper/`.

## Foundations

| Paper | Link |
|---|---|
| ★ New Directions in Cryptography (Diffie–Hellman, 1976) | [https://ieeexplore.ieee.org/document/1055638](https://ieeexplore.ieee.org/document/1055638) |
| ★ A Method for Obtaining Digital Signatures and Public-Key Cryptosystems (RSA, 1978) | [https://people.csail.mit.edu/rivest/Rsapaper.pdf](https://people.csail.mit.edu/rivest/Rsapaper.pdf) |
| ★ Probabilistic Encryption (Goldwasser–Micali, 1984) | [https://people.csail.mit.edu/silvio/Selected%20Scientific%20Papers/Probabilistic%20Encryption/Probabilistic_Encryption.pdf](https://people.csail.mit.edu/silvio/Selected%20Scientific%20Papers/Probabilistic%20Encryption/Probabilistic_Encryption.pdf) |
| ★ How to Prove Yourself: Practical Solutions to Identification and Signature Problems (Fiat–Shamir, 1986) | [https://link.springer.com/chapter/10.1007/3-540-47721-7_12](https://link.springer.com/chapter/10.1007/3-540-47721-7_12) |

## Random Oracle Model

| Paper | Link |
|---|---|
| Random Oracles are Practical: A Paradigm for Designing Efficient Protocols (Bellare–Rogaway, 1993) | [https://cseweb.ucsd.edu/~mihir/papers/ro.pdf](https://cseweb.ucsd.edu/~mihir/papers/ro.pdf) |
| ★ The Random Oracle Methodology, Revisited (Canetti–Goldreich–Halevi) | [https://eprint.iacr.org/1998/011](https://eprint.iacr.org/1998/011) |

## Lattice

| Paper | Link |
|---|---|
| ★ Generating Hard Instances of Lattice Problems (Ajtai, 1996 — worst-case/average-case reduction, SIS) | [https://eccc.weizmann.ac.il/report/1996/007/](https://eccc.weizmann.ac.il/report/1996/007/) |
| ★ On Lattices, Learning with Errors, Random Linear Codes, and Cryptography (Regev, 2005 — LWE) | [https://cims.nyu.edu/~regev/papers/qcrypto.pdf](https://cims.nyu.edu/~regev/papers/qcrypto.pdf) |
| ★ On Ideal Lattices and Learning with Errors over Rings (LPR — Ring-LWE) | [https://eprint.iacr.org/2012/230](https://eprint.iacr.org/2012/230) |
| ★ A Decade of Lattice Cryptography (Peikert survey) | [https://eprint.iacr.org/2015/939](https://eprint.iacr.org/2015/939) |
| A Complete Analysis of the BKZ Lattice Reduction Algorithm | [https://eprint.iacr.org/2020/1237](https://eprint.iacr.org/2020/1237) |
| LWE reduction | [2401.03703](https://arxiv.org/pdf/2401.03703) |
| Lattice trapdoor | [501.pdf](https://eprint.iacr.org/2011/501.pdf) (Gadget trapdoor, MP12)<br>[432.pdf](https://eprint.iacr.org/2007/432.pdf) (GPV / Ajtai-style trapdoor)<br>[1401.pdf](https://eprint.iacr.org/2024/1401.pdf) (Multi-preimage trapdoor sampler) |
| Programming lattice challenge technique (intensively used) | [591.pdf](https://eprint.iacr.org/2010/591.pdf) |

## PKE

| Paper | Link |
|---|---|
| Optimal Asymmetric Encryption — How to Encrypt with RSA (OAEP) | [https://cseweb.ucsd.edu/~mihir/papers/oaep.pdf](https://cseweb.ucsd.edu/~mihir/papers/oaep.pdf) |
| Relations Among Notions of Security for Public-Key Encryption Schemes | [https://eprint.iacr.org/1998/021](https://eprint.iacr.org/1998/021)<br>[1998_crypto.pdf](https://www.di.ens.fr/david.pointcheval/Documents/Papers/1998_crypto.pdf) |
| ★ A Practical Public Key Cryptosystem Provably Secure Against Adaptive Chosen Ciphertext Attack (Cramer–Shoup, 1998) | [https://www.shoup.net/papers/cs.pdf](https://www.shoup.net/papers/cs.pdf) |

## KEM

| Paper | Link |
|---|---|
| CRYSTALS – Kyber: a CCA-secure module-lattice-based KEM | [https://eprint.iacr.org/2017/634.pdf](https://eprint.iacr.org/2017/634.pdf) |
| ★ A Modular Analysis of the Fujisaki–Okamoto Transformation (HHK — source of the γ-spread / FO framework) | [https://eprint.iacr.org/2017/604](https://eprint.iacr.org/2017/604) |

## FHE

| Paper | Link |
|---|---|
| ★ Fully Homomorphic Encryption Using Ideal Lattices (Gentry, 2009 — thesis & papers) | [https://crypto.stanford.edu/craig/](https://crypto.stanford.edu/craig/) |
| ★ Fully Homomorphic Encryption without Bootstrapping (BGV) | [https://eprint.iacr.org/2011/277](https://eprint.iacr.org/2011/277) |
| ★ Homomorphic Encryption from Learning with Errors: Conceptually-Simpler, Asymptotically-Faster, Attribute-Based (GSW) | [https://eprint.iacr.org/2013/340](https://eprint.iacr.org/2013/340) |

## Identity-Based Encryption

| Paper | Link |
|---|---|
| ★ Identity-Based Encryption from the Weil Pairing (Boneh–Franklin, 2001) | [https://eprint.iacr.org/2001/090](https://eprint.iacr.org/2001/090) |
| IBE underlying LWE assumption in standard model (the programming technique is intensively used in concurrent works) | [latticebb.pdf](https://crypto.stanford.edu/~dabo/pubs/papers/latticebb.pdf) |

## Signatures

| Paper | Link |
|---|---|
| A Digital Signature Scheme Secure Against Adaptive Chosen-Message Attacks (GMR, 1988) | [A_Digital_Signature_Scheme...pdf](https://people.csail.mit.edu/silvio/Selected%20Scientific%20Papers/Digital%20Signatures/A_Digital_Signature_Scheme_Secure_Against_Adaptive_Chosen-Message_Attack.pdf) |
| ★ Efficient Signature Generation by Smart Cards (Schnorr, 1991) | [https://link.springer.com/article/10.1007/BF00196725](https://link.springer.com/article/10.1007/BF00196725) |
| Lattice Signatures Without Trapdoors (Lyubashevsky — Fiat-Shamir with aborts) | [https://eprint.iacr.org/2011/537](https://eprint.iacr.org/2011/537) |
| CRYSTALS – Dilithium: Digital Signatures from Module Lattices | [https://eprint.iacr.org/2017/633](https://eprint.iacr.org/2017/633) |
| ★ Falcon: Fast-Fourier Lattice-based Compact Signatures over NTRU | [https://falcon-sign.info/falcon.pdf](https://falcon-sign.info/falcon.pdf) |

## Blind Signatures

| Paper | Link |
|---|---|
| ★ Blind Signatures for Untraceable Payments (Chaum, 1982 — the origin) | [https://link.springer.com/chapter/10.1007/978-1-4757-0602-4_18](https://link.springer.com/chapter/10.1007/978-1-4757-0602-4_18) |
| Practical, Round-Optimal Lattice-Based Blind Signatures | [https://eprint.iacr.org/2021/1565](https://eprint.iacr.org/2021/1565) |
| PI-Cut-Choo and Friends: Compact Blind Signatures via Parallel Instance Cut-and-Choose and More | [https://eprint.iacr.org/2022/007.pdf](https://eprint.iacr.org/2022/007.pdf) |
| Lattice-Based Blind Signatures: Short, Efficient, and Round-Optimal | [https://eprint.iacr.org/2023/077](https://eprint.iacr.org/2023/077) |
| Non-Interactive Blind Signatures for Random Messages | [https://eprint.iacr.org/2023/388](https://eprint.iacr.org/2023/388) |
| Non-interactive Blind Signatures: Post-quantum and Stronger Security | [https://eprint.iacr.org/2024/614](https://eprint.iacr.org/2024/614) |
| Blinding Post-Quantum Hash-and-Sign Signatures | [https://eprint.iacr.org/2025/895](https://eprint.iacr.org/2025/895) |
| Batched & Non-interactive Blind Signatures from Lattices | [https://eprint.iacr.org/2025/1771](https://eprint.iacr.org/2025/1771) |
| Revisiting Lattice-based Non-interactive Blind Signature | [https://eprint.iacr.org/2025/1848](https://eprint.iacr.org/2025/1848) |
| Non-Interactive Blind Signatures from RSA Assumption and More | [https://eprint.iacr.org/2025/2076](https://eprint.iacr.org/2025/2076) |
| Concretely Efficient Blind Signatures Based on VOLE-in-the-Head Proofs and the MAYO Trapdoor | [https://eprint.iacr.org/2026/109](https://eprint.iacr.org/2026/109) |
| Non-interactive Blind Signatures with Threshold Issuance | [https://eprint.iacr.org/2026/400](https://eprint.iacr.org/2026/400) |

## ZKP & Proof Systems

| Paper | Link |
|---|---|
| ★ The Knowledge Complexity of Interactive Proof Systems (GMR, 1985 — defines ZK) | [The_Knowledge_Complexity...pdf](https://people.csail.mit.edu/silvio/Selected%20Scientific%20Papers/Proof%20Systems/The_Knowledge_Complexity_Of_Interactive_Proof_Systems.pdf) |
| ★ On the Size of Pairing-based Non-interactive Arguments (Groth16) | [https://eprint.iacr.org/2016/260](https://eprint.iacr.org/2016/260) |
| ★ Bulletproofs: Short Proofs for Confidential Transactions and More | [https://eprint.iacr.org/2017/1066](https://eprint.iacr.org/2017/1066) |
| ★ Scalable, Transparent, and Post-quantum Secure Computational Integrity (STARK) | [https://eprint.iacr.org/2018/046](https://eprint.iacr.org/2018/046) |
| ★ PLONK: Permutations over Lagrange-bases for Oecumenical Noninteractive arguments of Knowledge | [https://eprint.iacr.org/2019/953](https://eprint.iacr.org/2019/953) |
| ZKBoo: Faster Zero-Knowledge for Boolean Circuits | [https://eprint.iacr.org/2016/163.pdf](https://eprint.iacr.org/2016/163.pdf) |
| zk-SNARKs from Codes with Rank Metrics | [https://eprint.iacr.org/2023/1411](https://eprint.iacr.org/2023/1411) |
| Critical Rounds in Multi-Round Proofs: Proof of Partial Knowledge and Trapdoor Commitments | [https://eprint.iacr.org/2024/1766](https://eprint.iacr.org/2024/1766) |
| Privacy-Preserving Identity Management System on Blockchain Using Zk-SNARK | [https://ieeexplore.ieee.org/document/10005111](https://ieeexplore.ieee.org/document/10005111) |

## Commitment

| Paper | Link |
|---|---|
| ★ Non-Interactive and Information-Theoretic Secure Verifiable Secret Sharing (Pedersen commitment, 1991) | [https://link.springer.com/chapter/10.1007/3-540-46766-1_9](https://link.springer.com/chapter/10.1007/3-540-46766-1_9) |
| ★ Constant-Size Commitments to Polynomials and Their Applications (KZG, 2010) | [cacr2010-10.pdf](https://cacr.uwaterloo.ca/techreports/2010/cacr2010-10.pdf) |
| Succinct Vector, Polynomial, and Functional Commitments from Lattices (used in witness encryption as well) | [1515.pdf](https://eprint.iacr.org/2022/1515.pdf) |
| Hachi: Efficient Lattice-Based Multilinear Polynomial Commitments over Extension Fields | [https://eprint.iacr.org/2026/156](https://eprint.iacr.org/2026/156) |
| RoKoko: Lattice-based Succinct Arguments, a Committed Refinement | [https://eprint.iacr.org/2026/575](https://eprint.iacr.org/2026/575) |
| Collection of all polynomial commitment schemes | [Comparison of MLE-PCS (Final Report)](https://pcs.zkpunk.pro/) |

## Secret Sharing

| Paper | Link |
|---|---|
| ★ How to Share a Secret (Shamir, 1979) | [https://dl.acm.org/doi/10.1145/359168.359176](https://dl.acm.org/doi/10.1145/359168.359176) |
| Fully Anonymous Secret Sharing | [https://eprint.iacr.org/2025/1984](https://eprint.iacr.org/2025/1984) |

## Threshold Cryptography

| Paper | Link |
|---|---|
| Split gadget lattice trapdoor (limited usage due to weak security model) | [Partial Lattice Trapdoors: How to Split Lattice Trapdoors, Literally](https://eprint.iacr.org/2025/367) |

## MPC

| Paper | Link |
|---|---|
| ★ How to Play ANY Mental Game (GMW, 1987) | [https://dl.acm.org/doi/10.1145/28395.28420](https://dl.acm.org/doi/10.1145/28395.28420) |
| ★ Universally Composable Security: A New Paradigm for Cryptographic Protocols (Canetti, UC) | [https://eprint.iacr.org/2000/067](https://eprint.iacr.org/2000/067) |
| Efficient Multi-instance Vector Commitment and Application to Post-quantum Signatures | [https://eprint.iacr.org/2024/465](https://eprint.iacr.org/2024/465) |

## Multivariate

| Paper | Link |
|---|---|
| UOV signature | [https://link.springer.com/chapter/10.1007/978-3-030-99277-4_17](https://link.springer.com/chapter/10.1007/978-3-030-99277-4_17) |
| Multivariate Commitments and Signatures with Efficient Protocols | [https://eprint.iacr.org/2025/2035](https://eprint.iacr.org/2025/2035) |

## PQC & Cryptanalysis

| Paper | Link |
|---|---|
| ★ Polynomial-Time Algorithms for Prime Factorization and Discrete Logarithms on a Quantum Computer (Shor, 1994) | [https://arxiv.org/abs/quant-ph/9508027](https://arxiv.org/abs/quant-ph/9508027) |
| ★ An Efficient Key Recovery Attack on SIDH (Castryck–Decru, 2022 — broke SIKE) | [https://eprint.iacr.org/2022/975](https://eprint.iacr.org/2022/975) |

## PRG & PRF

| Paper | Link |
|---|---|
| How to Generate Cryptographically Strong Sequences of Pseudo-Random Bits (Blum–Micali, 1982) | [blum.micali82.pdf](https://pages.cs.wisc.edu/~cs812-1/blum.micali82.pdf) |
| ★ How to Construct Random Functions (GGM, 1986 — PRF from PRG) | [https://dl.acm.org/doi/10.1145/6490.6503](https://dl.acm.org/doi/10.1145/6490.6503) |

## Traceable Systems & CBDC

| Paper | Link |
|---|---|
| Balancing Privacy and Accountability in Blockchain Identity Management | [https://eprint.iacr.org/2020/1511.pdf](https://eprint.iacr.org/2020/1511.pdf)<br>[talk](https://www.youtube.com/watch?v=totqjbvgR44) |
| Platypus: A Central Bank Digital Currency with Unlinkable Transactions and Privacy-Preserving Regulation | [https://eprint.iacr.org/2021/1443.pdf](https://eprint.iacr.org/2021/1443.pdf) |
| Project Tourbillon demonstrates cash-like anonymity for retail CBDC | [bis.org/tourbillon](https://www.bis.org/about/bisih/topics/cbdc/tourbillon.htm)<br>[othp80.pdf](https://www.bis.org/publ/othp80.pdf) |
| Traitor Tracing in Multi-sender Setting (TMCFE: Traceable Multi-client Functional Encryption) | [https://eprint.iacr.org/2025/364](https://eprint.iacr.org/2025/364) |

## AI

| Paper | Link |
|---|---|
| ★ Attention Is All You Need (Transformer, 2017) | [https://arxiv.org/abs/1706.03762](https://arxiv.org/abs/1706.03762) |
| Accelerating Scientific Research with Gemini: Case Studies and Common Techniques | [https://arxiv.org/pdf/2602.03837](https://arxiv.org/pdf/2602.03837) |
