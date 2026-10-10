# Open Companion Platform — Downloads & Releases

**A character-driven desktop companion for Windows.**
Bring animated companions to your desktop, customize their appearance and interactions, and discover additional characters, effects, and skills as the platform evolves.

[**Browse Windows downloads →**](https://github.com/opencompanionplatform/ocp-releases/releases) · [Desktop source code](https://github.com/opencompanionplatform/ocp-desktop) · [OCP Store](https://ocp-store-prd.pages.dev) · [Privacy policy](https://ocp-store-prd.pages.dev/privacy/)

![Platform](https://img.shields.io/badge/platform-Windows%20x64%20%7C%20ARM64-2563eb)
![Project license](https://img.shields.io/badge/license-Apache--2.0-16a34a)
![Release maturity](https://img.shields.io/badge/release%20channel-Preview%20%2F%20Test-f59e0b)

> [!IMPORTANT]
> **OCP is in the preview/testing stage. There is no approved Stable release at this time.** Downloads marked **TEST**, **PREVIEW**, **POC**, **LOCAL**, or **UNSIGNED** are for evaluation, not production deployment. Some older proof-of-concept tags have legacy GitHub release classifications; **a non-prerelease label by itself does not mean Stable**. Always read the individual release notes.

## What is OCP?

Open Companion Platform (OCP) is an open-source Windows desktop companion project. The Desktop application combines an animated character runtime with native window interaction, a desktop control center, and an extensible package ecosystem.

Depending on the build and enabled features, you can explore:

| Experience | What it provides |
| --- | --- |
| **Desktop companions** | Animated characters that appear and move on the Windows desktop |
| **Native interaction** | Hover controls, drag interactions, character placement and desktop movement |
| **Personalization** | Character packages, visual effects, display options, and Thai/English UI |
| **Desktop Shell & Studio** | A control center and integrated tools for working with companion content |
| **Store & packages** | Optional discovery, installation, and management of compatible content |
| **AI & voice experiments** | Optional capabilities under active development; availability varies by release |

Not every feature is available or fully validated in every preview. The release notes are the source of truth for a specific build.

## Download for Windows

**Official distribution:** [github.com/opencompanionplatform/ocp-releases/releases](https://github.com/opencompanionplatform/ocp-releases/releases)

| Your Windows device | Installer (when published) | Portable archive (when published) |
| --- | --- | --- |
| **x64 (Intel / AMD)** | `ocp-windows-x86_64-<version>-setup.exe` | `ocp-windows-x86_64-<version>.zip` |
| **ARM64 (Windows on Arm)** | `ocp-windows-arm64-<version>-setup.exe` | `ocp-windows-arm64-<version>.zip` |

The two architectures are **not interchangeable**. A release may publish only one architecture; do not substitute an older build without checking its release notes. For testing, use Windows 11 with a supported architecture unless the specific release explicitly documents other support.

### Install with the setup program

1. Open the [Releases page](https://github.com/opencompanionplatform/ocp-releases/releases) and select the exact version you intend to test.
2. Read its release notes, known issues, signing status, and test scope.
3. Download the correct Windows `-setup.exe` and the accompanying `SHA256SUMS.txt`, if provided.
4. Verify the checksum and publisher/signature information **before** running the installer.
5. Run the setup program and follow its prompts. If applicable, finish the First Run experience and review the application's startup and privacy settings.

### Run the portable build

1. Download the matching `.zip` archive.
2. Verify its SHA-256 checksum, then extract **all** files into a dedicated folder.
3. Start `ocp-launcher.exe` from the extracted folder.
4. Exit OCP before replacing or removing the extracted files.

Portable installations and installed versions can share per-user settings. Testing a clean First Run requires a **fresh Windows user profile or isolated VM**, not simply extracting a new archive over an existing profile.

## Verify your download

The SHA-256 checksum verifies file integrity, **not who published the file**. When the release provides `SHA256SUMS.txt`, compare its entry against the local result:

```powershell
Get-FileHash .\ocp-windows-arm64-<version>-setup.exe -Algorithm SHA256
```

To inspect a Windows executable's Authenticode status:

```powershell
Get-AuthenticodeSignature .\ocp-windows-arm64-<version>-setup.exe |
  Select-Object Status, SignerCertificate
```

Replace the example filename with the exact artifact you downloaded. **`NotSigned` means the executable is not Authenticode-signed.** Windows may display a SmartScreen warning for unsigned previews. Do not disable security protection or treat a checksum as a substitute for publisher verification. Use test builds only if you understand and accept that risk.

An update-manifest signature, when present and verified, is **not the same thing** as an Authenticode signature on the installer. An `unsigned` manifest is not an authenticated production update.

Read the full [Code Signing & Release Integrity Policy](CODE_SIGNING.md).

## Release channels

| Channel | Purpose | Intended audience |
| --- | --- | --- |
| **Test / Local / POC** | Debugging, physical acceptance and compatibility checks | Developers and designated testers |
| **Public Preview / Beta** | Early access with documented known issues and verified downloads | Informed early adopters |
| **Stable** | Approved release after the project's acceptance, provenance, and security gates pass | General use |

**Stable has not been declared.** A version number, a generated artifact, or a green build alone does not confer Stable status.

Each public release should clearly identify its channel, architecture, source revision, changes, known limitations, signing status, and verification material. Availability of those items can differ for historical test releases.

## Open source, provenance & trust

This repository distributes release files. It is **not** the application source repository.

- [**Desktop source — `ocp-desktop`**](https://github.com/opencompanionplatform/ocp-desktop): public desktop/runtime source, build scripts, and release-related contracts.
- [**Official release files — `ocp-releases`**](https://github.com/opencompanionplatform/ocp-releases): installers, portable archives, release notes, and associated evidence.
- [**OCP Store**](https://ocp-store-prd.pages.dev): separately operated hosted services and downloadable content.

The public source is synchronized from an integration repository using an allowlisted export process. Approved releases must identify the corresponding **public source commit**, not merely an uncommitted local build. Where published, look for build provenance, checksums, and other release evidence attached to the specific release.

Official update trust, marketplace trust, code signing, and GitHub release access are separate controls; none should be inferred from the presence of a download link alone.

## Help, feedback & security

For reproducible application issues, use the [Desktop issue tracker](https://github.com/opencompanionplatform/ocp-desktop/issues). Include the release tag, architecture, Windows version, reproduction steps, and relevant logs where safe. Remove tokens, account details, and other private data before sharing logs.

**Security vulnerabilities:** do **not** disclose sensitive details in a public issue. Follow the [Security Policy](https://github.com/opencompanionplatform/ocp-desktop/blob/main/SECURITY.md) or email **opencompanionplatform@gmail.com**.

- [Privacy policy](https://ocp-store-prd.pages.dev/privacy/)
- [Source privacy document](https://github.com/opencompanionplatform/ocp-desktop/blob/main/PRIVACY.md)
- [Source repository README](https://github.com/opencompanionplatform/ocp-desktop)
- [Release integrity and signing policy](CODE_SIGNING.md)

## License & acknowledgements

The OCP Desktop source is licensed under the [Apache License, Version 2.0](https://github.com/opencompanionplatform/ocp-desktop/blob/main/LICENSE). Bundled third-party components and content may have additional licenses and attribution requirements; consult each distribution's notices.

---

<p align="center"><strong>Open Companion Platform</strong> · Open source desktop companions, built for an extensible future.</p>
