# OpenVision personal iPhone build

Experimental GitHub Actions recipe for building [OpenVision](https://github.com/rayl15/OpenVision)
on a hosted Mac and installing a personally signed copy from Windows.
This is not an official OpenVision release or a verified installation guide.

## Build

Open **Actions → OpenVision iPhone deneme derlemesi → Run workflow**.
If the build succeeds, download the **OpenVision-iPhone-deneme** artifact.
It contains an unsigned IPA; it cannot be installed directly by tapping it.

The workflow downloads upstream commit `1e88c3f21f4521c953bb8a1e4e60be865e3893b4`,
uses the GitHub `xcode-27` preview runner, and needs no Apple signing certificate
or AI API key. Standard public-repository runners are free under GitHub's current policy.

## Device setup

- Sign and install the IPA locally with [Sideloadly](https://sideloadly.io/).
  This third-party tool supports free Apple accounts with seven-day provisioning.
- Enable iPhone developer mode if prompted, and separately enable developer mode
  for the glasses in the Meta AI app.
- Register the glasses in OpenVision and verify the actual glasses camera first.
  The iPhone-camera fallback does not validate the glasses connection.
- Select OpenAI and enter an API key on the phone only after the camera test.
  API billing is separate from a ChatGPT subscription.
- Never put passwords, verification codes or API keys in this repository.

## Differences from upstream

- Defaults to the OpenAI backend.
- Removes the increased-memory-limit entitlement for a personal-signing experiment;
  large on-device models are not recommended for this build.
- Replaces the legacy armv7 device capability with arm64.
- Uses Meta App ID 0 for developer-mode testing; the current Meta documentation
  describes this mode, but SDK 0.9.0 registration on the target glasses still
  requires verification. A personal Meta developer app may be needed if it fails.
- No API keys or Apple credentials are embedded.

## Validation limits

Local YAML, Python and configuration-preparation checks passed.
Check Actions for actual compilation status. A successful build does not verify
signing, installation on iOS 27, microphone routing or the glasses camera.

Upstream OpenVision is MIT licensed. This repository contains only a build recipe;
the source and its original license are fetched from upstream during a build.

