# evo-device-audio-ui-artefacts

> The release plane for [evo-device-audio-ui](https://github.com/foonerd/evo-device-audio-ui). Signed UI bundle artefacts, fetched by any distribution.

Manifest in. Signed bytes out. Consumers pick the channel.

This repository is the device-facing (and distribution-facing) surface of the audio-domain UI shell. Editing source in [evo-device-audio-ui](https://github.com/foonerd/evo-device-audio-ui) does not touch these assets. What lands here is exactly what a distribution (or a device tracking commons directly) fetches and verifies.

## What lives here

- `channels/` — per-channel signed pointer TOML files (`dev.toml`, `test.toml`, `prod.toml`). Each pointer names the current UI bundle version for that channel.
- `bundles/` — signed UI bundle artefacts (one per released version). Bit-identical across channels.
- `LICENSE` — Apache-2.0 for the assets in this repo.

## Channels

Three named tracks of release readiness: `dev`, `test`, `prod`. Same shape as every other release plane in the evo ecosystem.

- **A channel is a pointer, not a bucket.** A version of a bundle is built once, signed once, stored once. Promotion from `dev` to `test` is a pointer edit — the channel now names that version. The bytes do not change; the signature does not change. Bit-identical bundles across every channel they appear on.
- **Selection is per-consumer.** A consumer's channel map says which channel's pointer to track.

## Signing

Every artefact under `bundles/` is signed against the evo project release key. Every pointer TOML under `channels/` is signed against the same key. Consumers verify signatures before applying.

## Consumer contract

Fetch `channels/<channel>.toml`, verify signature, resolve `bundle_version`, fetch and verify `bundles/evo-device-audio-ui-<version>.tar.gz` (+ `.sig`), extract, install.
