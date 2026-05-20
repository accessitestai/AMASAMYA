# Contributing to AMASAMYA

Thank you for considering a contribution. The most valuable contributions to AMASAMYA come from the people who use the tool day-to-day - screen-reader users, accessibility professionals, and developers shipping accessible products. The bar for what counts as a useful contribution is genuinely low.

## What contributions are welcome

In rough order of how useful they are:

1. **Bug reports against real sites.** Run the extension on any page, find a finding that looks wrong (false positive, false negative, or unclear remediation hint), and open an issue. These are the highest-signal reports.
2. **Accessibility issues with AMASAMYA itself.** If the side panel, the audit reports, or the export formats fail with any screen reader, keyboard-only navigation, voice control, or other assistive technology, open an issue. These take priority.
3. **WCAG criterion coverage gaps.** AMASAMYA covers 17 engines. There are real WCAG 2.2 criteria not yet automated - feature requests for specific criteria are welcome, especially with example pages where the criterion fails.
4. **Pull requests for engine improvements.** Small, focused, with one logical change per PR. Include a one-paragraph rationale referring to the WCAG criterion you are addressing.
5. **Documentation and translation.** README, code comments, in-tool help text. Translation of the audit messages is particularly welcome - AMASAMYA is currently English-only.

## What contributions are not in scope right now

- Visual redesigns of the side panel without an accompanying accessibility rationale.
- Engine additions that overlap heavily with axe-core's existing rules (the goal is to complement axe-core, not duplicate it).
- New Vision AI integrations beyond OpenAI and Anthropic. Adding providers is fine in principle, but each new provider increases the privacy-policy surface area and needs proper documentation.

## Filing an issue

The most useful issue template:

> **WCAG criterion or feature area:** (e.g. SC 1.4.3 Colour Contrast, or "Side panel keyboard navigation")
>
> **Page or scenario:** URL or steps to reproduce.
>
> **What I expected:** the finding I expected AMASAMYA to report.
>
> **What happened instead:** the finding AMASAMYA actually reported (or did not).
>
> **Assistive technology and browser:** NVDA / JAWS / VoiceOver / TalkBack / version, plus Chrome version.

## Filing a pull request

1. Fork the repository.
2. Branch from `main`.
3. Make your change.
4. Test the extension by loading it unpacked via `chrome://extensions` and running it against a page that exercises your change.
5. Open a PR with the rationale, the WCAG criterion, and one concrete before-and-after example.

## A note on tone

AMASAMYA exists to close gaps that other tools have left unaddressed for years. Issues will sometimes raise things that current users have been frustrated by for a long time - please assume good faith on all sides. Comments that personally criticise other contributors or developers will be moderated.

## Code of conduct

By participating in this project you agree to treat every contributor with respect, regardless of their assistive technology, disability, native language, or experience level. Concerns about behaviour can be raised privately to `akhilesh.malani@gmail.com`.

## Licence of contributions

By submitting a contribution you agree that it is licensed under the same MIT licence that covers the rest of the repository.
