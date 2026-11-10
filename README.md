---
# Machine-readable header. Milo and the catalog read these keys; keep the names exact.
id: <package-id>                     # npm name without scope, e.g. reelup for @app-brew/reelup
title: <Partner name>                # shown in Studio and the catalog
summary: <One sentence, max 25 words and 160 characters.>
access: self-serve                   # self-serve | request
image: https://<partner-cdn>/<logo>.png
category: <reviews | video-commerce | loyalty | analytics | crm | checkout | search | other>
owner:
  name: <partner team or person>
  email: <support address>
docs: https://<partner docs url>
---

<!--
Rules for this template
- Keep every section heading below, in this order, with the exact text. Milo finds sections by heading.
- A section that does not apply says "None." instead of being deleted.
- Never put real keys, tokens or secrets in this file. Use the format only (e.g. `rmk_` + 48 hex characters).
- The merchant form lives in package.json `appbrew.settings`. The table in section 4 must list the same keys.
-->

## 1. Description

<!-- Max 120 words. What the merchant gets, what the shopper sees, and which screens it appears on. -->

## 2. Access

Tick one:

- [ ] Self-serve: the merchant turns it on in Studio and fills the form. No approval needed.
- [ ] Request-based: the merchant asks for it, and Appbrew turns it on.

If request-based, how to ask: <link or email>

## 3. Requirements

| Item | Value |
| --- | --- |
| Package | `@<scope>/<id>` |
| Version | `<x.y.z>` (must match package.json) |
| Minimum `@gauntlet/*` version | `<x.y.z>` |
| Needs a new app build | Yes / No (must match `appbrew.requiresNativeBuild`) |
| Native dependencies | <list with versions, or "None"> |
| Partner-side prerequisites | <plan, app installed on Shopify, feature flags, markets> |
| Platforms | iOS, Android, Studio web preview |

## 4. Merchant config form

Config key: `integrations.<configKey>` (from `appbrew.configKey`).

| Key | Label | Type | Required | Secret | Where the merchant finds it | Format / example |
| --- | --- | --- | --- | --- | --- | --- |
| `<key>` | <title as in the manifest> | text | Yes | Yes | <Partner admin → page → field> | `<prefix>` + <shape> |

<!-- Type is one of: text, number, boolean, json, select, file, time. For select, list the options. -->

Values Appbrew fills in on its own (the merchant does not enter them): <for example the shop domain from `store.shopifyDomain`, or "None">.

## 5. Codebase changes (merchant app)

Scripted setup: Yes, `milo integration setup <id>` / No, follow the steps below.

1. **Dependency.** In the app's `package.json`:

   ```json
   "@<scope>/<id>": "<version>"
   ```

2. **Register blocks.** `src/app/register-blocks.ts`:

   ```ts
   // exact import and call
   ```

3. **Native changes.** <Podfile, Info.plist, AndroidManifest.xml, MainApplication.kt entries with exact snippets, or "None.">

4. **Install.** `pnpm install` (plus `pod install` if native changes exist).

## 6. Studio / theme config

### Blocks

| Block id | Shows | Screen | List (`blocks` / `floating`) |
| --- | --- | --- | --- |
| `<block-id>` | <what it renders> | <home / products / collection-detail / any> | blocks |

### Block settings

| Setting | Required | What it does | Default |
| --- | --- | --- | --- |
| `source.<field>` | No | <effect> | <default> |
| `options.<field>` | No | <effect> | <default> |

### Example theme entries

```jsonc
// screens.<screen>.layout.blocks
[
  { "componentId": "<block-id>", "instanceId": "<block-id>-1", "source": {}, "options": {} }
]
```

`instanceId` must be unique on a screen.

## 7. Screenshots and videos

| Block | Platform | Screenshot | Video | What to check |
| --- | --- | --- | --- | --- |
| `<block-id>` | iOS | https://… | https://… (MP4, max 30 s) | <exact behaviour to compare against> |
| `<block-id>` | Android | https://… | https://… | |

<!-- At least one screenshot per block per platform, plus one video for every interaction (tap, swipe, add to cart). -->

### Test checklist

- [ ] <Step the tester takes> → <what they should see>
- [ ] Config missing or wrong → <what the app does, e.g. block hidden, log line>

## 8. How it works

<!-- Request flow, in numbered steps. -->

| Request | When |
| --- | --- |
| `<METHOD> <url>` | <trigger> |

Data sent to <Partner>: <fields, and whether any of it is shopper data>.
Hosts the app calls: <hosts, for network allowlists>.

## 9. Troubleshooting

Log prefix: `[<id>]`.

| Symptom / log | Cause | Fix |
| --- | --- | --- |
| | | |

## 10. Versioning and release

- Semantic versioning: patch for fixes, minor for new options or blocks, major when a block id, config key or required API changes. Never rename `configKey`, because merchants' saved values live under it.
- Changes are listed in `CHANGELOG.md`.

Before a production release:

- [ ] <checklist items>

## 11. Support

| Item | Value |
| --- | --- |
| Partner contact | <name, email> |
| Appbrew contact | <name> |
| Status page / SLA | <url or "None"> |
