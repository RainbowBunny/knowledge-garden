---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof-system/non-interactive/succinct-non-interactive-a-rgument-of-knowledge/","dg-note-properties":{"aliases":["SNARK"]}}
---

Reference:
- https://www.di.ens.fr/~nitulesc/files/Survey-SNARKs.pdf

## Definition

> [!definition] Succinct Non-interactive ARgument of Knowledge
> Extends:: [[knowledge/cryptography/verifiable computing/proof system/non-interactive/Non-interactive ARgument of Knowledge\|Non-interactive ARgument of Knowledge]]
>
> ---
> A **succinct non-interactive argument of knowledge** (SNARK) is a [[knowledge/cryptography/verifiable computing/proof system/non-interactive/Non-interactive ARgument of Knowledge\|NARK]] with [[knowledge/cryptography/verifiable computing/property/Succinctness\|Succinctness]].

> [!remark] Also a SNARG
> `⚠️ CLAUDE – verify:` a SNARK is also a [[knowledge/cryptography/verifiable computing/proof system/non-interactive/Succinct Non-interactive ARGument\|SNARG]], because knowledge soundness implies soundness. That is the usual reading, but it depends on how adaptivity and auxiliary input are set in the two definitions; check [[knowledge/cryptography/verifiable computing/property/Knowledge Soundness\|Knowledge Soundness]] against [[knowledge/cryptography/verifiable computing/property/Soundness\|Soundness]] before relying on it.

## Related

### Descendants
- [[knowledge/cryptography/verifiable computing/proof system/non-interactive/Zero-Knowledge Succinct Non-interactive ARgument of Knowledge\|zk-SNARK]] — adds [[knowledge/cryptography/verifiable computing/property/Zero Knowledge\|Zero Knowledge]]
