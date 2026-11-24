

This repository holds **no source code**. It only hosts the downloadable packs (as GitHub Releases) and this README.

## What is a pack?

A pack is the optional local model that can use to double-check
names and companies during review. It contains:

- `model/` — a [GLiNER](https://github.com/urchade/GLiNER) named-entity model (`urchade/gliner_multi-v2.1`, fp16 weights
  in safetensors format, tokenizer and config).
- `worker/` — a frozen, per-platform program (Python, PyTorch, transformers, GLiNER and a small glue script)
  that runs the model on your machine.

The model runs **fully locally**. It only suggests; it never removes an entity or changes the alias map on its own.
Application does not need the pack to work.

## How to install

In Application: **Settings → Assisted review → Install**. Application downloads the pack, checks its size and sha256 against
the values pinned in the app, verifies the model weights, and only then installs it. The download request carries no
user or document data.

No internet on the computer? Download the `.aliaspack` for your platform from the
[Releases](../../releases) page, then use **Install from file** in the same settings page, or:

```
<application-name> assist install <file>.aliaspack
```

## Releases

- One release per pack version, tag `assist-v<version>` (for example `assist-v1.0.0`).
- One asset per platform: `<application-name>-assist-<version>-<platform>.aliaspack`.
- Assets are never replaced after publishing. A fix is a new pack version.

## Licences

| Component | Licence |
| --- | --- |
| GLiNER (`urchade/gliner_multi-v2.1`) and the `gliner` library | Apache-2.0 |
| `microsoft/mdeberta-v3-base` (tokenizer / backbone config) | MIT |
| PyTorch | BSD-3-Clause |
| `transformers` | Apache-2.0 |
| application-name worker glue code | Part of application-name; see the application-name licence |

The pack is only usable together with a licensed application-name installation; the licence is checked in the app.
