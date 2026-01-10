---
name: reflect
description: Capture learnings from conversation after Claude made mistakes or needed correction. Trigger phrases include "reflect", "review our mistakes", "review what went wrong", "learn from this", "capture this learning", "remember this for next time", or any request to analyze and persist corrections from the current conversation. Analyzes the conversation to extract what went wrong, how it was resolved, and actionable guidance for future sessions. Writes learnings to project-specific markdown files and maintains an index for easy reference.
---

# Reflect

Analyze the current conversation to extract learnings from mistakes or corrections, then persist them for future sessions.

## Workflow

1. **Identify the problem**: Scan the conversation for where things went wrong - look for user corrections, error messages, failed attempts, or "actually, do X instead" moments

2. **Trace the resolution**: Follow the back-and-forth to understand how the issue was resolved - what did the user clarify? What fix worked?

3. **Synthesize the learning**: Extract the actionable insight - not just "what happened" but "what should future Claude do differently"

4. **Ask where to save**: Confirm the file path with the user. Suggest `docs/learnings/YYYY-MM-DD-<topic>.md` (e.g., `docs/learnings/2025-01-15-expo-sdk-version.md`)

5. **Write the learning**: Use the format below

6. **Update the index**: Add an entry to `docs/learnings/INDEX.md` mapping the problem type to the learning doc. Create the index if it doesn't exist (see Index Format below)

## Learning Format

```markdown
# <Clear, actionable title>

## Context
<What was being attempted - 1-2 sentences>

## Problem
<What went wrong and why - be specific>

## Resolution
<How it was fixed - include code/commands if relevant>

## Guidance
<Actionable advice for future sessions - the key takeaway>
```

## Example

File: `docs/learnings/2025-01-15-expo-sdk-version.md`

```markdown
# Use Expo SDK 50+ for new React Native projects

## Context
Creating a new React Native app using Expo with the default template.

## Problem
The app failed to load in Expo Go with SDK version compatibility errors. The default template used an older SDK version that wasn't supported by the current Expo Go app.

## Resolution
Updated `app.json` to specify SDK 50, ran `expo upgrade`, and reinstalled dependencies.

## Guidance
When creating new Expo projects, always verify the SDK version in `app.json` is 50 or higher. Run `expo upgrade` if starting from an older template.
```

## Index Format

The index (`docs/learnings/INDEX.md`) maps problem types to learning docs so Claude can quickly find relevant guidance. Include this file in your `CLAUDE.md` or project instructions.

```markdown
# Learnings Index

Quick reference for common issues and their solutions.

## How to use this index
When you encounter a problem, scan the categories below to find relevant learnings.

---

## React Native / Expo
| Problem | Learning |
|---------|----------|
| SDK version compatibility errors in Expo Go | [2025-01-15-expo-sdk-version.md](./2025-01-15-expo-sdk-version.md) |

## API / Backend
| Problem | Learning |
|---------|----------|
| (empty) | |

## Testing
| Problem | Learning |
|---------|----------|
| (empty) | |

## Other
| Problem | Learning |
|---------|----------|
| (empty) | |
```

When adding a new learning, find (or create) the appropriate category and add a row with:
- **Problem**: A brief description of when to consult this learning (e.g., "SDK version compatibility errors")
- **Learning**: Relative link to the dated learning file

## Tips for Good Learnings

- **Be specific**: "Use SDK 50+" is better than "use a recent SDK"
- **Include the why**: Explain *why* the problem occurred, not just what happened
- **Make it actionable**: The guidance should be something Claude can act on
- **One learning per file**: Keep each learning focused on a single issue
