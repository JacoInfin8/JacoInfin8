# Infin8 Apps ecosystem operations contract

Version: 2026.09.04
Authority: Infin8 Development Control Panel
Scope: every Infin8 repository, agent, model, terminal, automation, and human workflow

This is the provider-neutral operating contract for the Infin8 Apps ecosystem. Repository-specific `AGENTS.md`, build, DSP, security, licensing, deployment, and release rules remain authoritative within their own scope. This contract connects those rules; it does not weaken or replace them.

## 1. Repository authorities

| Repository | Authority |
| --- | --- |
| `Infin8-Development-Control-Panel` | Cross-repository discovery and allowlisted operations, shared licensing/activation, product registry, assistant workflows, and evidence reports |
| `Infin8-Apps` | Canonical design system and desktop application source |
| `Infin8-Audio` | Audio DSP, standalone/VST3 source, hardware discovery, customer packages, and Windows installer source |
| `Infin8-Apps-Site` | Public website, Arcade, purchasing UX, entitlement broker, and the only supported website deployment rail |
| `Infin8-Releases` | Private immutable binary release origin; no application source, secrets, or customer records |
| `JacoInfin8` | Public GitHub profile and public brand/product narrative; no private operations or release assets |

Every application remains registered in its repository's `applications.json`. Cross-repository commands are selected from those versioned command vectors by `scripts/operations/Invoke-Infin8Operation.ps1`; agents must not substitute a guessed command, a stale README example, or an alternate deployment path.

## 2. Common lifecycle language

- `development`: source or workflow work that is not customer-ready.
- `official-beta`: a real versioned Infin8 release with installers, manifests, protected delivery, activation, and update pathways. Creator/sponsor access may be granted, customer messaging remains purchase-focused for the future, trials remain locked until an entitlement is issued, and beta/signing limitations are disclosed.
- `paid-production`: checkout is enabled, release artifacts are officially signed, hosted delivery is proven, commercial dependency obligations are packaged, and product-specific release gates pass.

An official beta is an official release, but it is not a paid-production release. Do not describe a local build, package, draft release, or source check as deployed, uploaded, signed, or customer-delivered.

## 3. Current Audio release program

The current Audio channel is `official-beta`:

- future customer packages and website placement stay purchase-focused;
- approved creators and sponsors may receive official beta entitlements while public purchasing is disabled;
- Stripe checkout is currently disabled, so nothing is charged and no public purchase is implied;
- every installer presents unlock options at the start and states that the product remains in trial mode until unlocked;
- current Windows packages may be unsigned only when the unsigned-beta warning, official source, and SHA-256 verification path are shown;
- an Authenticode signature is mandatory before future paid production;
- a product with stale or missing hardware proof remains blocked even if its source builds successfully.

Hardware is discovered per machine. Never assume customers share the developer's audio interface, driver model, MIDI controller, GPU vendor, Python runtime, sample rate, buffer size, VST folder, or install location. Installers and first-run flows must let the user choose install/VST locations, request elevation only for protected destinations, enumerate current devices, explain backend requirements, and preserve a safe CPU/fallback path.

## 4. Standard operation flow

1. Read the local `AGENTS.md`, this contract, and every task-relevant repository document before action.
2. Inspect `applications.json`, git branch/remote/status, source paths, registered commands, and current release state.
3. Preserve unrelated and uncommitted user work. Never normalize a dirty repository by discarding changes.
4. Use the Control Panel operation runner for multi-repository status, inventory, validation, build, package, stage, or publish planning. Run only exact registered command tokens.
5. Keep development output in each repository's documented build locations. Do not copy source into release origins or edit generated mirrors as canonical source.
6. Validate in layers: source, tests, package, installed runtime/hardware, signed manifest/hash, hosted asset, website runtime, and production publication are separate evidence claims.
7. Finish with changed files, exact commands and results, unresolved gates, and a clear statement of what was not uploaded, pushed, deployed, signed, charged, or hardware-tested.

Any workflow may perform read-only inventory. Build, test, or package actions require the task to include that product and must still respect its local rules. Git push, hosted release upload/publication, website deployment, external messages, checkout activation, credential changes, and official signing require explicit user authorization for that external action.

## 5. Agent and model co-synchronization

Codex, Claude, Gemini, Copilot, local Ollama models, general coding terminals, and future providers use the same hierarchy:

1. local repository `AGENTS.md`;
2. local `docs/INFIN8-ECOSYSTEM-OPERATIONS.md`;
3. task-relevant local design, security, build, DSP, licensing, and deployment contracts;
4. versioned `applications.json` command vectors;
5. the user's latest explicit request.

Provider-specific convenience files may summarize navigation, but they may not invent weaker release, security, dependency, signing, or publication rules. A handoff between agents records the repository, branch, dirty-state baseline, files changed, validation evidence, and remaining external or hardware proof. Another agent continues from that state rather than rebuilding or reverting it by assumption.

## 6. Commercial and data safety

- Customer-facing dependencies must be reviewed for commercial redistribution, notices, source/relink obligations, and forbidden paid/trial/runtime gates.
- Credentials, activation records, private signing keys, Stripe secrets, customer data, licensed voice assets, and private release tokens never enter source, logs intended for users, public website roots, profile repositories, or release assets.
- Shared licensing stays under the Control Panel authority. Product repositories use thin adapters and do not fork entitlement or signature trust.
- Release assets are immutable after customer availability; fixes use a new semantic version and coordinated tag.
- Unsigned beta delivery is a temporary disclosed state, never a substitute for the paid-production signing gate.

## 7. Synchronization and validation

The canonical copy is this file in `Infin8-Development-Control-Panel`. Run:

```powershell
Set-Location "E:\Infin8-Development-Control-Panel"
.\scripts\operations\Sync-Infin8EcosystemContract.ps1 -Apply
.\scripts\validation\VALIDATE_ECOSYSTEM_ALIGNMENT.ps1
```

`-Apply` updates synchronized contract copies and managed provider entry blocks without replacing repository-specific instructions. The validation command checks contract parity, provider coverage, repository identity/remotes, application manifests, the current Audio beta channel, and the complete Control Panel inventory. Edit the canonical contract and `config/infin8-ecosystem.json` together when the repository set or operating policy changes.
