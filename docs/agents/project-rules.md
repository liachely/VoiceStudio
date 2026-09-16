# VoiceStudio Project Rules

This file contains **project policy**, not assistant personality. It is the durable engineering contract for work on VoiceStudio.

## Product priority

VoiceStudio is a fully-local voice cloning, voice design, dubbing, dictation, transcription, and audiobook application.

**Primary product value:** a first run that actually works. Reliability, installation, compatibility, and clear recovery paths take priority over adding complexity or features.

## Compatibility

- Existing installed engines and on-disk `omnivoice_data/` must keep working without manual reinstall or migration.
- Database schema changes use Alembic with a tested upgrade path.
- Default user-visible behavior must be equivalent on macOS, Windows, and Linux. Platform-specific implementation is allowed; platform-specific default behavior is not.
- Platform-only features require explicit opt-in.
- Hardware performance and acceleration may legitimately vary by host; parity is about behavior, not performance.

## Local-first and privacy

- No new required cloud dependency, account, API key, or network call.
- Nothing leaves the user's machine without explicit user consent.
- Bug reporting remains opt-in through a prefilled GitHub Issue submitted by the user's browser.
- Product analytics, where present, is consent-gated and limited to the project's established allowlisted metadata policy.
- New Hugging Face downloads must be gated by installed-ness or explicit user action.
- Synthetic audio must pass through the existing `mark_synthetic` chokepoint.

## User-facing text

- All user-facing strings go through the i18n system.
- CJK user-facing strings belong in the translation layer; functional/model/test exceptions follow the existing allowlist and tests.
- Translation changes must keep all supported locale files synchronized.

## Versioning

- `frontend/package.json` is the single source of truth for the application version.
- Required toolchain mirrors must stay in lockstep with it.
- Do not bump versions unless the owner asks.
- Do not invent RCs, codenames, or future-version deferrals without the owner asking.
- Follow the current release behavior documented in `docs/RELEASING.md`.

## Documentation and changelog

- If a change affects documented behavior, update the affected documentation in the same change.
- Keep `CHANGELOG.md`'s `Unreleased` section current for user-visible changes.
- Release notes are user-facing, concise, and organized by theme rather than raw commit dumps.

## Fix quality

- Fix the root cause and the bug class, not only the reported instance.
- Add a regression test that fails before the fix and passes after it when practical.
- Prefer the smallest correct change that is recurrence-resistant.
- Put mechanical policy in deterministic tests and CI rather than relying on an AI agent to remember it.

## Dependencies and builds

- Prefer dependencies already pinned in `pyproject.toml` and `frontend/package.json`.
- Check dependency conflicts before adding packages.
- `frontend/` is a Bun workspace; dependency changes require the repository `bun.lock` to remain frozen-install compatible.
- Validate relevant backend, frontend, Rust/Tauri, security, and Docker consumers when their inputs change.

## Merge and review

Before merging:

1. Check the open PR queue when addressing a community-reported issue.
2. Read automated review findings from configured review bots.
3. Fix substantive findings before merge.
4. Require the repository's configured test gate and a mergeable PR.
5. After merging, verify `main` returns to green.

Specialized reviewer agents may apply stricter review behavior while they are explicitly being used. That behavior is not the default assistant personality.

## Skills and references

- Development skills live under `.agents/skills/` and are pinned by `skills-lock.json`.
- `.claude/skills/` contains Claude-specific task skills.
- Deep technical material belongs in skill references or domain documentation, not in the assistant's core behavior.
- Issue-tracker details: `docs/agents/issue-tracker.md`.
- Triage mappings: `docs/agents/triage-labels.md`.
- Domain context: `CONTEXT.md` and `docs/adr/`.
- Release procedures: `docs/RELEASING.md`.
