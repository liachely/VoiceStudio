# VoiceStudio — Claude Project Instructions

This file is intentionally **small**.

It tells Claude where the project's rules and task-specific behavior live; it is not the place to define the assistant's personality.

## Read these in this order

1. **Assistant behavior:** `.claude/AGENT_CORE.md`
   - How to communicate and collaborate with the user.
   - How to preserve user authorship and keep skills from changing personality.

2. **Project policy:** `docs/agents/project-rules.md`
   - What must be true of VoiceStudio.
   - Compatibility, local-first behavior, i18n, versioning, testing, docs, and merge rules.

3. **Task-specific skills:**
   - `.agents/skills/` for pinned development skills such as Vite and FastAPI.
   - `.claude/skills/` for Claude-specific capabilities such as writing and OmniVoice.

4. **Specialized roles:** `.claude/agents/`
   - Use only when the task calls for that role.
   - A specialized role does not redefine the default assistant personality.

5. **Deep reference material:** `docs/`, `docs/adr/`, skill reference files, and `CONTEXT.md`.
   - Read only the material relevant to the current task.

## Core project context

VoiceStudio is a fully-local desktop application for voice cloning, voice design, video dubbing, dictation, transcription, and audiobook creation.

The product priority is simple: **a first run that actually works.** Reliability, compatibility, and clear recovery paths come before unnecessary complexity.

## Working rules

- Understand the user's actual goal before choosing a skill or tool.
- For code changes, follow `docs/agents/project-rules.md` and the relevant development skill.
- For writing work, use `.claude/skills/writing/SKILL.md` and preserve the user's voice and authorship.
- Do not treat every instruction in a skill as a global instruction. Skills are task-local capabilities.
- Do not load deep reference material unless the task needs it.
- Do not turn specialized review behavior into the default interaction style.

## Important source-of-truth note

The old GSD-generated sections that previously made up most of this file were mixing project policy, workflow history, stack research, and agent behavior in one always-loaded document. The durable project rules have been extracted to `docs/agents/project-rules.md`.

If a generated GSD workflow later reintroduces a large block here, preserve this separation rather than adding more behavior to the global instruction layer.

## Existing project configuration

- `skills-lock.json` pins the development skills under `.agents/skills/`.
- `AGENTS.md` contains the cross-agent operating contract.
- `.claude/AGENT_CORE.md` contains default human interaction behavior.
- `.claude/agents/` contains specialized agents.
- `.claude/skills/` contains task-specific Claude skills.
