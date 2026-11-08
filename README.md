<p align="center">
  <img src="./.github/assets/readme/vibeleak-symbol.png" alt="VibeLeak" width="120" />
</p>

# VibeLeak Atlas

**Review your own website and local code inside Hermes Desktop.**

VibeLeak Atlas brings authorized website assessments and read-only local code inspection into a native Hermes workspace. Review evidence, prepare an unsent fix-plan draft, and check the result of changes you approve separately.

[VibeLeak](https://vibeleak.app) · [Walkthrough](#see-it-in-use) · [Installation](#installation) · [Privacy](#privacy-and-data-handling) · [Support](#support)

> **Preview 0.2.1.** Available in the Hermes plugin catalog. Website assessments require a scoped VibeLeak owner API key, which is listed under the Pro plan. Local folder inspection does not require a VibeLeak account.

## See it in use

[![Animated preview of VibeLeak Atlas, including the assessment map and local code review](./.github/assets/readme/walkthrough.gif)](./.github/assets/readme/vibeleak-atlas-demo.mp4)

**[Watch or download the full narrated walkthrough](./.github/assets/readme/vibeleak-atlas-demo.mp4)** · 93 seconds · 720p · voiceover, captions, music and sound effects

The animation is a short, silent preview. The full video includes both workflows. All captures show the native plugin with sample website responses and a sample PHP project. These are not live production findings or client projects. See the [media credits](./.github/assets/readme/CREDITS.md).

## What you can do

| Workflow | What Atlas does | What stays under your control |
| --- | --- | --- |
| Website assessment | Requests an authorized assessment through VibeLeak, opens its private findings, and compares an approved rescan with its baseline. | The exact target, website authorization, a ceiling of one scan unit per request, and every rescan. |
| Local folder inspection | Reads permitted source and configuration files through native folder grants, then reports bounded static review candidates. | Folder access, explicit inspection approval, the fix-plan draft, and any later changes. |

Both workflows can prepare a reviewed draft for a compatible Hermes chat. **Atlas does not send that draft, call a model, edit your project, or deploy a fix.**

### Website assessments

- Review private evidence tied to assessments explicitly initiated by your installation. Atlas does not import a public index or account-wide scan history.
- Attach repository context with **Choose folder**, **Use current**, or a manual hint. Choosing a folder here does not inspect or upload its source.
- Prioritize findings and prepare a repository-aware fix-plan draft.
- Request a rescan after an approved change and deployment. Comparison reports observations, not independently verified fixes.
- Explore your assessments in the dithered globe, real ASCII map, or list view. Pause animation, disable dithering, or use reduced motion.
- Enable approximate hosting-country lookup separately. Unknown locations remain unknown. CDN locations are not verified server origins.

### Local folder inspection

- Choose a local folder, then separately approve read-only inspection.
- Review selected PHP input-handling and configuration patterns, possible hardcoded secrets in readable source, and environment-file ignore-policy hints.
- See detected React, Next.js and PHP requirement metadata where present. Metadata is not a dependency vulnerability audit or proof of the deployed runtime.
- Understand coverage through exclusion reasons, file and directory counts, native read refusals, and inspection limits.
- Preview a redacted fix plan without raw source excerpts. Reinspect after separately approved changes, then release access.

## Screenshots

| Assessment map | Website evidence |
| --- | --- |
| [![Dithered globe showing example website assessments](./.github/assets/readme/assessment-map.png)](./.github/assets/readme/assessment-map.png) | [![Private evidence and fix-plan controls using sample results](./.github/assets/readme/website-evidence.png)](./.github/assets/readme/website-evidence.png) |

| Local review candidates | Unsent fix-plan review |
| --- | --- |
| [![Bounded PHP review of a sample project](./.github/assets/readme/local-review.png)](./.github/assets/readme/local-review.png) | [![Redacted fix-plan draft with copy and append actions](./.github/assets/readme/fix-plan-draft.png)](./.github/assets/readme/fix-plan-draft.png) |

Sample data only. Click a screenshot to inspect it at full size.

## Requirements

- **Hermes Agent and Hermes Desktop 0.22.6 or later**, with the native plugin SDK, the folder-grant file API used by local inspection, and authenticated Python plugin backend support. The CLI alone cannot display this interface.
- **Native local folder access** for local inspection. Hermes's sensitive-file protections still apply. A remote connection is not permission to read an arbitrary remote filesystem.
- **A scoped VibeLeak owner API key** for website assessments. API keys are listed under the Pro plan at [vibeleak.app/pricing](https://www.vibeleak.app/pricing), and VibeLeak checks entitlement on each request. Local inspection needs neither a VibeLeak key nor a subscription.
- **Hermes's Python environment** for the installation and credential helpers. A separate system Python may not have Hermes's modules.
- **Node.js 22 and npm for development only.** Prepared plugin packages include the built renderer.

Native acceptance has been exercised on Windows Desktop. Other operating systems have not received the same native acceptance checks.

## Installation

Requires Hermes Agent and Hermes Desktop **0.22.6 or later**. Tested on Windows with Hermes 0.23.0.

### From Git (recommended)

Run these in a terminal:

```sh
hermes plugins install https://github.com/abundantbeing/vibeleak-atlas
hermes plugins enable vibeleak-atlas --no-allow-tool-override
```

Hermes labels this a custom source outside the Hermes catalog. That notice is expected. The install copies the agent backend and the Desktop renderer. The enable step turns on the agent side. Neither step restarts the gateway.

Then turn on the Desktop page. In Hermes Desktop, open **Capabilities ▸ Plugins**, search for **VibeLeak Atlas**, open its card, and switch on **Desktop: VibeLeak Atlas**. The **VibeLeak Atlas** entry then appears in the sidebar and command palette. If it does not appear, run **Reload desktop plugins** from the command palette.

### From a release package or source checkout

Use an extracted **0.2.1** package or source checkout of that version. From its root, run this with Hermes's Python interpreter:

```sh
python scripts/install_local.py
```

Here, `python` must resolve to the interpreter from your Hermes installation. The installer copies the agent backend and desktop renderer, asks Hermes to enable the agent side, and backs up existing configuration. It does not restart the gateway. Then turn on the Desktop page as described above.

### Upgrade

```sh
python scripts/install_local.py --upgrade
```

The installer requires a recognized Atlas installation, backs up both plugin components, and preserves profile data. It restores the previous package files if activation fails. On Windows, unchanged files held open by the backend can remain in place.

Reloading JavaScript does not prove that a running Python backend changed. If Atlas reports an incompatible or inactive backend, save your work and arrange a reload deliberately. Do not restart an active gateway just to clear a warning.

### Catalog availability

VibeLeak Atlas is listed in the [Hermes plugin catalog](https://github.com/NousResearch/hermes-agent/blob/main/plugin-catalog/vibeleak-atlas.yaml). The catalog pins the reviewed version to a specific commit.

## First use

### Inspect a local project

1. Select **Local folder inspection**.
2. Choose a folder through the native picker. Selection alone does not start inspection.
3. Read the scope and limitations, then approve read-only inspection.
4. Review candidates and coverage. Excluded or unreadable files are not passing checks.
5. Open the fix-plan preview. Copy it or append it to a compatible chat as an **unsent draft**.
6. Approve code changes separately in chat. Reinspect afterward, then release access.

The inspector does not execute project code, install packages, write files, call a model, or upload source and findings to VibeLeak.

### Assess an authorized website

1. Create an owner key on the [VibeLeak API keys page](https://www.vibeleak.app/dashboard/api-keys) with `scan:write`, `scan:read`, and `findings:read`. API keys are listed under the Pro plan at [vibeleak.app/pricing](https://www.vibeleak.app/pricing).
2. Open **Settings ▸ Plugins ▸ VibeLeak Atlas** and paste the key into the **VibeLeak owner API key** field. Hermes stores it in its secret store. Never paste a key into chat, the renderer, screenshots, or Git.
3. Select **Website assessment**, refresh the connection, and enter a public hostname you own or are authorized to assess.
4. Optionally attach repository context, then select **Review assessment**. Preparing the confirmation does not contact the target.
5. Confirm the exact HTTPS target and explicitly approve both your authorization and at most one VibeLeak scan unit.
6. Run the assessment, review its evidence, and preview a fix-plan draft. Approve subsequent changes separately.
7. After the change and deployment, select **Review rescan**, approve the new request, and compare with the baseline.

VibeLeak checks scopes and entitlement. Saving a key locally does not prove that the service will accept it. Keyless guest website scans are not supported by this plugin.

## Privacy and data handling

| Data or action | Handling |
| --- | --- |
| Local source and candidates | Read through native folder-scoped APIs. Source and local findings are not sent to VibeLeak. Reports remain in page memory. |
| Protected and excluded files | Raw `.env` files, credential files, private keys, dependencies, generated output and Git internals are not inspected. |
| Website assessments | Send the approved target to VibeLeak. VibeLeak performs the assessment and stores its website results under its service policies. Website mode is not offline. |
| Owner key | Read through Hermes's backend secret provider. The renderer does not receive it. |
| Local assessment records | SQLite stores installation-bound receipts, hostnames, optional repository hints and supplied runtime evidence in the active backend profile. It does not store the raw API key or website findings. |
| Hosting lookup | Requires separate consent. Sends approved hostnames to Cloudflare DNS and uses bundled DB-IP country data locally. |
| Fix-plan export | Copying uses the OS clipboard. Appending creates an unsent chat draft. A later user submission may share it with the selected model provider. |

Changing the folder, profile, connection or applicable consent invalidates pending work. Releasing a folder clears its local report. Redaction covers recognizable patterns, not every possible sensitive value. Review a draft before copying or sending it.

Read the full [privacy policy](docs/privacy.md) and [API compatibility notes](docs/api-compatibility.md).

### Behavior disclosure

- **Network:** VibeLeak's API, only for website assessments you approve. Cloudflare DNS over HTTPS, only for the hosting-country lookup after separate consent. The country database is bundled and used offline.
- **Local files:** Atlas reads only the folder you select, and only after you approve inspection. Protected and excluded files are not opened. While a folder is selected and the window is visible, Atlas checks about every four seconds that the folder grant still exists. That check lists granted folders; it does not open files.
- **Credentials:** the owner key is entered in **Settings ▸ Plugins ▸ VibeLeak Atlas**, stored in Hermes's secret store, and read by the backend. The renderer never receives it.
- **Commands:** the installer runs `hermes plugins enable vibeleak-atlas --no-allow-tool-override` through Hermes's CLI. Atlas itself runs no shell commands.
- **Telemetry and analytics:** none. Atlas sends nothing beyond the requests described above.

## Scope and limitations

Atlas is a review tool, not a complete security audit or a guarantee that a site is safe.

- Local inspection uses bounded static patterns, not a PHP parser, runtime execution, or a complete dependency scanner. False positives and missed issues are possible.
- Default local limits are **600 files**, **256 KiB per file**, **8 MiB total**, **18 directory levels**, **12,000 listed entries**, and **100 review candidates**. Limits and refusals reduce the inspected scope.
- Source requirements do not establish the serving PHP version, hosting configuration, or vendor backports. Advisory evidence remains separate and must come from the owner or hosting provider.
- A missing finding, zero local candidates, or a better website grade does not independently prove a deployed fix works.
- Website authorization is your attestation plus VibeLeak's API policy, not an independent ownership challenge.
- There are no automatic scans, scheduled monitoring, automatic remediation, or deployments.
- Rescan comparisons are not comparable until VibeLeak returns coverage and version context for both scans. Some VibeLeak deployments do not return that context yet.
- Some VibeLeak checks can misreport. TLS certificate status, for example, may be wrong. Verify a certificate or header yourself before acting on a finding.

If a website request is interrupted, it may still run and consume its unit. Use **Review same approval** to recover with the existing idempotency key. Do not create a separate replacement scan because the response was lost.

## Technology

| Component | Languages and tools | Role |
| --- | --- | --- |
| Native interface | JavaScript, JSX, React, `@hermes/plugin-sdk` | Native pages, dialogs, folder grants, connection state and unsent drafts. React comes from Hermes, not a second bundled copy. |
| Visualizations | Three.js 0.170.0, WebGL, Canvas and shader code | Dithered globe, geographic labels and ASCII rendering. |
| Styling | CSS and Hermes theme variables | Native themes and responsive layouts. |
| Backend | Python, FastAPI and HTTPX | Authenticated plugin routes and bounded requests to the fixed VibeLeak API origin. Runs inside Hermes's backend. |
| Local records | SQLite through Python's standard library | Durable approvals, installation identity and scan receipts. |
| Geography | Natural Earth (public domain), DB-IP Country Lite ([IP Geolocation by DB-IP](https://db-ip.com), CC BY 4.0), pure-Python MaxMind DB reader | Bundled maps and approximate hosting-country attribution. The interface displays the DB-IP credit. |
| Build and tests | esbuild 0.25.12, npm, Node's test runner, Python `unittest` | Renderer bundling, regression checks and packaging. |

The shipped renderer imports only the Hermes SDK and Hermes's React runtime. It does not embed a website iframe or fetch renderer code from a CDN.

### Repository layout

```text
atlas/              Python assessment, receipt, comparison and advisory logic
dashboard/          Authenticated plugin API entry and manifest
desktop-src/        React/JSX components, local review rules and CSS
desktop/            Built ESM renderer and bundle metadata
assets/             Geographic data and source metadata
scripts/            Build, setup, installation and packaging helpers
tests/              Python and JavaScript regression tests
docs/               Architecture, privacy and API documentation
.github/assets/     README screenshots, animation and walkthrough video
```

## Development

Use Node.js 22, npm, and Hermes's Python environment:

```sh
npm ci
python -m unittest discover -s tests -q
npm test
npm run build
npm run package
```

Packaging creates the plugin ZIP and checksum manifest under `artifacts/`. Keep credentials, local databases, QA homes and environment files out of source and release packages.

Read [architecture](docs/architecture.md) for the component boundaries and [verification](docs/verification.md) for test procedures.

## Troubleshooting

| Symptom | What to check |
| --- | --- |
| Atlas is missing from the sidebar | Confirm the agent side is enabled and **Desktop: VibeLeak Atlas** is on in **Capabilities ▸ Plugins**, then run **Reload desktop plugins**. |
| The owner backend is inactive | Check that the current connection has the matching backend enabled. Reloading JavaScript alone does not reload Python. |
| Folder access is unavailable | Use a local Desktop connection with the native folder API and its picker. Do not bypass protected files with another reader. |
| The website key is refused | Check scopes, API entitlement, the active backend profile and secure key setup. |
| Many files are excluded | Read the coverage breakdown. Dependencies, build output, protected files, unsupported formats and limits are reported separately. |
| A website request is uncertain | Use **Review same approval**, not another independent request. |
| A fix plan will not append | Focus a compatible chat on the same connection and profile, or copy the reviewed preview. |

## Contributing and reporting issues

For a bug report, include the plugin and Hermes versions, operating system, selected workflow, steps to reproduce, and a redacted screenshot where useful. Do not post API keys, private findings, client source, or raw environment files.

Keep changes focused, add a regression test, run the checks above, and update the docs. Contributions must respect explicit approval, native file grants, profile isolation and the plugin SDK. Do not bypass these controls or patch Hermes internals.

For a suspected credential exposure, rotate the key through its provider first. Arrange a private report with the maintainer before sharing sensitive evidence. Use the [issue tracker](https://github.com/abundantbeing/hermes-vibeleak-atlas/issues) for non-sensitive bugs.

## Support

Maintained by [@abundantbeing](https://github.com/abundantbeing).

If Atlas is useful to you, you can support development through Ko-fi. Sponsorship is optional and does not replace VibeLeak's API access requirements.

[![Support on Ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/T8Z726J5YZ)

## License

Project code is [MIT-licensed](LICENSE). Geographic data, vendored libraries and demonstration media retain their own licenses. See [third-party notices](THIRD_PARTY_NOTICES.md) and [media credits](./.github/assets/readme/CREDITS.md).
