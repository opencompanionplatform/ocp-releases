# OCP Code Signing & Release Integrity Policy

This document explains how Windows artifacts published by [Open Companion Platform](https://github.com/opencompanionplatform/ocp-releases) are identified, verified, and—when available—signed.

> [!IMPORTANT]
> **There is currently no approved OCP Stable release.** Public preview and test artifacts may be **unsigned**. An artifact must not be described as Authenticode-signed, independently reproducible, or production-trusted unless its own published evidence supports that claim.

## Project and release channels

- **Project:** Open Companion Platform (OCP)
- **Public Desktop source:** [opencompanionplatform/ocp-desktop](https://github.com/opencompanionplatform/ocp-desktop)
- **Release distribution:** [opencompanionplatform/ocp-releases](https://github.com/opencompanionplatform/ocp-releases/releases)
- **Desktop source license:** [Apache-2.0](https://github.com/opencompanionplatform/ocp-desktop/blob/main/LICENSE)

Local/Test/POC builds are not approved production releases. Public Beta builds must clearly disclose remaining limitations and actual signing status. A Stable designation requires explicit release approval and completion of the project's acceptance and provenance gates.

## Current signing status

OCP's earlier **SignPath Foundation application was not approved**. The project therefore **does not claim sponsorship, a SignPath Foundation certificate, or SignPath signing of its releases**. SignPath is not a prerequisite in the current release plan.

A future authenticode signing provider may be adopted after appropriate review and configuration. Until then, unsigned installers must be explicitly labeled **UNSIGNED** and should not be presented to end users as identity-verified software.

**Important distinctions:**

| Control | What it establishes | What it does *not* establish |
| --- | --- | --- |
| **SHA-256 checksum** | Downloaded bytes match the published digest | Publisher identity or trustworthy source |
| **Authenticode signature** | Windows binary is signed by the certificate holder, subject to certificate validity | That software has passed OCP acceptance |
| **Signed update manifest** | Authenticity/integrity of an update descriptor under the configured trusted key | Authenticode signing of its executables |
| **Source provenance** | Traceability between public source revision, approved workflow and artifact | Byte-identical reproducibility without a separate verification build |

An update manifest with `unsigned` in its filename is **not trusted production update metadata**.

## Source and artifact provenance requirements

Before a production release is approved, maintainers should record and verify:

1. The exact public `ocp-desktop` source revision and approved release tag.
2. A clean, reviewable source tree and any synchronized public-source export evidence.
3. Approved CI/release workflow identity and build inputs for **each architecture**.
4. Passing unit, integration, package, and security tests for the relevant release candidate.
5. Artifact names, architecture, hashes, immutable version metadata, and release notes.
6. Independent build comparison evidence where reproducibility is claimed.
7. Clean-install, cold-start, upgrade, rollback, and application behavior acceptance on the supported architectures.
8. Manual release approval before creating or promoting an official Stable tag.

A preview may be published with **documented exceptions**, provided its experimental nature and unsigned status are unmistakable. A skipped gate is not a passing gate.

## Signing scope and upstream software

OCP-owned components may include the launcher, kernel, native companion host, update checker, GDExtension, Desktop Shell, and Windows setup executable. Each artifact's signature status must be verified rather than inferred from another file in the bundle.

The Windows Godot Runtime is an **upstream Godot derivative** used to host OCP's project/PCK. The build process may adjust the upstream executable's Windows per-monitor DPI-awareness manifest. That edit invalidates the upstream Authenticode signature; the distributed derivative preserves Godot's upstream product identity and is **not represented as an OCP-authored or OCP-signed executable**. This exception must be documented when publishing OCP-owned signed artifacts.

Third-party binaries and packaged content remain subject to their own licenses, notices, and provenance requirements.

## Key management and release approval

- Maintainers with release access must use multi-factor authentication.
- Production signing credentials and update-manifest private keys must never be committed to a public repository or attached to release assets.
- Production signing should use an appropriately protected approval environment with restricted access and audit records.
- Updates, signing rules, trust roots, and release workflow changes require review as security-sensitive changes.
- Do not sign or promote builds from an unreviewed dirty working tree.
- Signatures and provenance should be independently verified before publication.

These are release policy requirements, **not claims that the associated production controls have already been deployed**.

## User verification

Download only from the [official release page](https://github.com/opencompanionplatform/ocp-releases/releases). Read the corresponding release notes, select the correct architecture, and compare any supplied `SHA256SUMS.txt` against:

```powershell
Get-FileHash .\<downloaded-file> -Algorithm SHA256
Get-AuthenticodeSignature .\<downloaded-installer.exe> |
  Select-Object Status, SignerCertificate
```

Avoid executing a build if its claimed signer or checksum does not match its release documentation. The absence of a signature on an explicitly unsigned Test/Preview build is expected but **not** evidence of authenticity.

## Security and privacy

Report vulnerabilities privately using the [Desktop Security Policy](https://github.com/opencompanionplatform/ocp-desktop/blob/main/SECURITY.md). Contact: **opencompanionplatform@gmail.com**.

See the [Privacy Policy](https://ocp-store-prd.pages.dev/privacy/) for optional network and hosted-service features.

## Maintenance

This policy replaces historical language that described SignPath Foundation participation as pending. Any future signing provider or release policy change should be documented and reviewed before the corresponding artifacts are promoted.

Last reviewed: **10 October 2026**.
