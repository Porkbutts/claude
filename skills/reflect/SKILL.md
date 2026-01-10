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

6. **Update the index**: Add an entry to `docs/learnings/INDEX.md` with an activity-based trigger so Claude consults this learning proactively during planning. Create the index if it doesn't exist (see Index Format below)

## Learning Format

```markdown
# <Clear, actionable title>

## Consult when
<Activity-based trigger for proactive use - what task/activity should prompt reading this? e.g., "Creating a new Expo project", "Setting up authentication", "Writing database migrations">

## Context
<What was being attempted - 1-2 sentences>

## Problem
<What went wrong and why - be specific>

## Resolution
<How it was fixed - include code/commands if relevant>

## Guidance
**Do:** <What to do instead - the correct approach>
**Avoid:** <What not to do - explicitly name the anti-pattern and why>
```

## Example

File: `docs/learnings/2025-01-15-expo-sdk-version.md`

```markdown
# Use Expo SDK 50+ for new React Native projects

## Consult when
Creating a new Expo project, initializing a React Native app with Expo, or upgrading an existing Expo project.

## Context
Creating a new React Native app using Expo with the default template.

## Problem
The app failed to load in Expo Go with SDK version compatibility errors. The default template used an older SDK version that wasn't supported by the current Expo Go app.

## Resolution
Updated `app.json` to specify SDK 50, ran `expo upgrade`, and reinstalled dependencies.

## Guidance
**Do:** Use Expo SDK 50 or higher. Verify the SDK version in `app.json` and run `expo upgrade` if starting from an older template.
**Avoid:** SDK 52 and lower—these cause compatibility errors with the current Expo Go app and won't load.
```

## Index Format

The index (`docs/learnings/INDEX.md`) maps activities to learning docs so Claude can proactively consult them during planning—before making mistakes. Include this file in your `CLAUDE.md` or project instructions.

```markdown
# Learnings Index

Consult these learnings **during planning** before starting work. Don't wait until something breaks.

## How to use this index
Before starting a task, scan the categories below for relevant learnings. Read them first to avoid known pitfalls.

---

## React Native / Expo
| Consult when | Learning |
|--------------|----------|
| Creating or upgrading an Expo project | [2025-01-15-expo-sdk-version.md](./2025-01-15-expo-sdk-version.md) |

## API / Backend
| Consult when | Learning |
|--------------|----------|
| (no learnings yet) | |

## Testing
| Consult when | Learning |
|--------------|----------|
| (no learnings yet) | |

## Other
| Consult when | Learning |
|--------------|----------|
| (no learnings yet) | |
```

When adding a new learning, find (or create) the appropriate category and add a row with:
- **Consult when**: An activity-based trigger describing when to read this (e.g., "Creating or upgrading an Expo project", "Setting up JWT authentication", "Writing database migrations")
- **Learning**: Relative link to the dated learning file

## Tips for Good Learnings

- **Be specific**: "Use SDK 50+" is better than "use a recent SDK"
- **Include the why**: Explain *why* the problem occurred, not just what happened
- **Make it actionable**: The guidance should be something Claude can act on
- **One learning per file**: Keep each learning focused on a single issue
- **Write activity-based triggers**: Frame "Consult when" around what Claude is about to *do*, not what error it might *see*. "Creating an Expo project" matches during planning; "SDK compatibility errors" only matches after failure
- **Use do/avoid framing**: Include both what to do AND what to avoid. "Use SDK 50+" tells Claude the right path; "Avoid SDK 52 and lower" explicitly marks the anti-pattern. Both framings help Claude recognize the boundary
