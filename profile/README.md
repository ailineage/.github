# AILineage

**Who stood behind an AI-generated artifact, and how was it made?**

AILineage is an open specification for signed, timestamped provenance manifests for AI-generated artifacts: images, text, code, audio and video. A manifest records the model, a hidden commitment to the prompt, the accountable principal and the artifact's parents. Verification answers one of three things:

| State | Meaning |
| --- | --- |
| `PROVENANCED` | A manifest for these exact bytes is well-formed, signed by a trusted key and timestamped. |
| `UNPROVENANCED` | No manifest was found. This says nothing about how the artifact was made. |
| `PROVENANCE_BROKEN(reason)` | A manifest was found, but a check failed. |

AILineage is an accountability layer. It does not detect AI content and does not claim that content is true. It rides inside [C2PA](https://c2pa.org/) and [in-toto](https://in-toto.io/) where those are used, and embeds on its own (PNG, JPEG, WebP, sidecar files, Git notes) where they are not.

- **Prompts stay private.** The manifest holds a salted hash of the prompt; the plaintext stays with its owner or in escrow and can be disclosed and checked later.
- **Lineage across media.** Prompt → image → video → edit, each step linked by content hashes.
- **Plain building blocks.** JSON with JCS (RFC 8785), Ed25519 or ES256 over `did:key`, RFC 3161 timestamps, SHA-256.

## Repositories

| Repository | Contents |
| --- | --- |
| [spec](https://github.com/ailineage/spec) | Specification 0.1 (draft), JSON Schema, conformance fixtures, ADRs, threat model, compliance map (EU AI Act Art. 50, Code of Practice, C2PA, NIST AI 100-4). CC-BY-4.0. |
| [ailineage](https://github.com/ailineage/ailineage) | Reference implementation: Python library and CLI, ComfyUI node. Go library and `ail` CLI next. Apache-2.0. |

## Status

Draft `ailineage/0.1`. The format may still change before 1.0; every normative change is recorded as an ADR. Feedback and implementations are welcome: open an issue in [spec](https://github.com/ailineage/spec/issues).
