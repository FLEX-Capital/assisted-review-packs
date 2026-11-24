# AliasMe assisted-review packs

Release assets for the optional **assisted review** add-on of [AliasMe](https://github.com/FLEX-Capital) — a desktop tool
that pseudonymises documents entirely on the local machine.

This repository holds **no source code**. It only hosts the downloadable packs (as GitHub Releases) and this README.

## What is a pack?

A pack (`aliasme-assist-<version>-<platform>.aliaspack`) is the optional local model that AliasMe can use to double-check
names and companies during review. It contains:

- `model/` — a [GLiNER](https://github.com/urchade/GLiNER) named-entity model (`urchade/gliner_multi-v2.1`, fp16 weights
  in safetensors format, tokenizer and config).
- `worker/` — a frozen, per-platform program (Python, PyTorch, transformers, GLiNER and a small AliasMe glue script)
  that runs the model on your machine.

The model runs **fully locally**. It only suggests; it never removes an entity or changes the alias map on its own.
AliasMe does not need the pack to work.

## How to install

In AliasMe: **Settings → Assisted review → Install**. AliasMe downloads the pack, checks its size and sha256 against
the values pinned in the app, verifies the model weights, and only then installs it. The download request carries no
user or document data.

No internet on the computer? Download the `.aliaspack` for your platform from the
[Releases](../../releases) page elsewhere, then use **Install from file** in the same settings page, or:

```
aliasme assist install <file>.aliaspack
```

## Releases

- One release per pack version, tag `assist-v<version>` (for example `assist-v1.0.0`).
- One asset per platform: `aliasme-assist-<version>-<platform>.aliaspack`.
- Assets are never replaced after publishing. A fix is a new pack version.

## Licences

| Component | Licence |
| --- | --- |
| GLiNER (`urchade/gliner_multi-v2.1`) and the `gliner` library | Apache-2.0 |
| `microsoft/mdeberta-v3-base` (tokenizer / backbone config) | MIT |
| PyTorch | BSD-3-Clause |
| `transformers` | Apache-2.0 |
| AliasMe worker glue code | Part of AliasMe; see the AliasMe licence |

The pack is only usable together with a licensed AliasMe installation; the licence is checked in the app.

## Not anonymisation

AliasMe produces **pseudonymised** output (GDPR Art. 4(5)). Context can still re-identify people. The assisted review
is a hint for the person reviewing, not a guarantee.
