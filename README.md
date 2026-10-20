# Oak firmware releases

This repository contains public firmware binaries and authenticated release metadata for Digistump Oak.
Application source code is maintained in a separate private repository.

## Current status

The remote-update runtime and the first signed firmware release are under development.
Creating this repository does not install remote-update support on an existing board.
No firmware release has been published yet.

## Release assets

A validated release contains only these files:

- `oak-firmware.bin`: the native rBoot firmware image.
- `oak-release.json`: repository, release sequence, version, layout, image size, SHA-256, and expiration metadata.
- `oak-release.sig`: an Ed25519 signature over the release metadata.
- `oak-release-key.json`: informational public-key identification.

A device must verify signatures using a trusted public key provisioned separately.
It must never automatically trust a public key downloaded alongside a release.

SHA-256 checks file integrity; the signature separately authenticates the release.
Normal updates write only to the inactive application slot and preserve the original factory and management recovery regions.
These are software write-range restrictions, not immutable hardware protection or a guarantee of recovery from every power interruption.

Private keys, tokens, Wi-Fi settings, and device diagnostic logs must never be included in public release assets.
