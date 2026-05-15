# AMASAMYA — Blind-first WCAG 2.2 accessibility audit platform

AMASAMYA is an accessibility audit toolkit built for and by screen-reader users. The Chrome extension in this repository runs seventeen WCAG 2.2 audit engines on any web page in roughly five seconds and reports findings in a side panel that is itself fully operable with a keyboard and a screen reader.

The companion web platform at [amasamya.akhileshmalani.com](https://amasamya.akhileshmalani.com) extends the same audit engines to uploaded documents in eight formats (PDF, Word, PowerPoint, Excel, EPUB, and OpenDocument) and to a structured mobile-app checklist for iOS, Android, and WearOS.

## What this repository contains

This repository ships the **Chrome extension** source — the part most users will want to read, fork, or contribute to. The web-platform source is part of a larger personal portfolio repository and is not mirrored here.

```
extension/                  Chrome Manifest V3 extension source
├── manifest.json
├── background.js           Service worker — audit orchestration, Vision AI bridge
├── content-script.js       17 audit engines (run on the active page)
├── content-script-platform.js
├── engines/                Individual engines isolated for clarity
│   ├── aria-validation.js
│   ├── dark-mode.js
│   ├── dom-order.js
│   ├── focus-narrator-inject.js
│   ├── high-contrast.js
│   ├── phase1-engines.js
│   ├── state-watchdog-inject.js
│   └── text-spacing.js
├── sidepanel/              Audit-results UI shown in the Chrome side panel
├── icons/                  Extension icons (16, 32, 48, 128)
└── privacy.html            Privacy policy
```

## The seventeen audit engines

Each engine maps to one or more WCAG 2.2 success criteria. Every finding includes the criterion reference, a severity rating, and a one-line remediation hint.

| # | Engine | Primary WCAG SC |
|---|---|---|
| 1 | Focus Order | 2.4.3 |
| 2 | Focus Visibility | 2.4.7 / 2.4.11 |
| 3 | Colour Contrast | 1.4.3 / 1.4.6 / 1.4.11 |
| 4 | Heading Structure | 1.3.1 / 2.4.6 |
| 5 | Landmarks | 1.3.1 / 2.4.1 |
| 6 | Images | 1.1.1 |
| 7 | Forms | 1.3.1 / 3.3.2 / 4.1.2 |
| 8 | Links and Buttons | 2.4.4 / 4.1.2 |
| 9 | High Contrast / forced-colors | 1.4.3 / 2.4.11 |
| 10 | Dark Mode support detection | 1.4.3 (dark) |
| 11 | Text Spacing | 1.4.12 |
| 12 | DOM Order | 1.3.2 |
| 13 | ARIA Validation | 4.1.2 |
| 14 | Target Size — minimum | 2.5.8 |
| 15 | Label in Name | 2.5.3 |
| 16 | Resize Text — 200 % zoom verification | 1.4.4 |
| 17 | Dark Mode Contrast — palette verification | 1.4.3 (dark) |

Three optional **Vision AI modules** (Focus Indicator Narrator, Visual Layout Auditor, State Change Watchdog) extend the audit beyond the machine-checkable engines. They are entirely opt-in and use the user's own OpenAI or Anthropic API key — no data is ever sent to AMASAMYA servers.

## Install (end users)

The signed extension is available on the Chrome Web Store. End users should install it from there rather than building from source:

[Install AMASAMYA from the Chrome Web Store](https://chromewebstore.google.com/detail/blnfmiipkccpggpinjofhhglfcgglbif).

## Install (developers, from source)

1. Clone this repository.
2. Open `chrome://extensions` in Chrome.
3. Enable **Developer mode** (toggle in the top-right).
4. Click **Load unpacked**.
5. Select the `extension/` folder of this repository.

The extension appears in your toolbar. Press `Ctrl+Shift+U` (Windows / Linux) or `Cmd+Shift+U` (Mac) on any page to run the audit. If that shortcut is taken on your system, reassign it via `chrome://extensions/shortcuts`.

## Privacy and data handling

AMASAMYA is privacy-first by construction:

- Audits run **locally** in your browser. No page content is ever sent to AMASAMYA servers — there are none.
- The optional Vision AI modules send screenshots **directly** from your browser to the provider you choose (Anthropic or OpenAI), using your own API key.
- API keys are encrypted at rest in `chrome.storage.local` with a non-extractable WebCrypto master key. They never leave your device.

The full privacy policy ships inside the extension at `extension/privacy.html` and is also published at [amasamya.akhileshmalani.com/privacy](https://amasamya.akhileshmalani.com/privacy).

## Permissions and why they are needed

| Permission | Used for |
|---|---|
| `activeTab` + `scripting` | Inject the audit engines into the tab you are currently viewing, on demand only. |
| `sidePanel` | Display audit results in the Chrome side panel. |
| `tabs` | Read the current tab's URL and title so reports can be labelled with the page they came from. |
| `storage` | Persist your Vision AI provider preference and (optional) API key locally. |
| `debugger` | Used only by the Visual Layout Auditor module, to emulate non-current viewport sizes via the Chrome DevTools Protocol. Chrome's mandatory "is being debugged" banner provides visible consent every time the feature runs. |
| `host_permissions: <all_urls>` | The user, not the extension, chooses which page is audited. The extension only ever reads or modifies the active tab on explicit user invocation. |

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). In short: issues and pull requests welcome, especially from screen-reader users and accessibility professionals who test against real sites. Bug reports that include the WCAG criterion you expected to be checked and the page you ran the audit on are the most useful.

## Reporting accessibility issues with AMASAMYA itself

AMASAMYA is built to be accessible. If any part of the extension or the side-panel UI fails for you with NVDA, JAWS, VoiceOver, TalkBack, or any other assistive technology, please [open an issue](https://github.com/accessitestai/AMASAMYA/issues) describing the assistive technology, the version, the operating system, and what you expected versus what happened. These reports take priority over feature requests.

## Licence

MIT — see [LICENSE](LICENSE).

## Who maintains this

Built and maintained by **Akhilesh Malani** — accessibility architect, digital inclusion strategist, and screen-reader user. Personal site: [akhileshmalani.com](https://akhileshmalani.com).

If you are interested in beta-testing, partnership conversations, or commercial use, write to `akhilesh.malani@gmail.com`. AMASAMYA is fully self-funded; honest critical feedback is the most valuable contribution you can make at this stage.
