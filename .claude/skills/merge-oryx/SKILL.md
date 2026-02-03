---
name: merge-oryx
description: Fetch and merge the oryx branch, explain conflicts in plain English, and resolve them interactively
disable-model-invocation: true
allowed-tools: Bash, Read, Edit, Write, AskUserQuestion
---

# Merge Oryx Branch

Merge changes from the `origin/oryx` branch into the current branch, handling conflicts interactively.

## Process

### 1. Fetch and Attempt Merge

```bash
git fetch
git merge origin/oryx
```

If the merge succeeds with no conflicts, report success and ask if the user wants to push.

### 2. If Conflicts Exist

For each conflicted file:

1. **Read the file** to find conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)

2. **Explain in plain English**:
   - What section of the file has a conflict
   - **"Your version (main)"**: Describe what your custom code does (e.g., "Your custom Orbital Mouse keys for cursor movement")
   - **"Oryx version"**: Describe what the Oryx-generated code does (e.g., "Oryx set these keys to KC_NO (disabled) because it doesn't know about your custom code")
   - Why they conflict

3. **Ask the user** using AskUserQuestion:
   - Present clear options:
     - Keep your version (main)
     - Keep Oryx version
     - Keep both/combine (explain how)
   - Include context about what each choice means

### 3. Resolve Conflicts

Based on user's choice:
- Edit the file to remove conflict markers
- Keep the appropriate code
- Ensure proper formatting

### 4. Finalize

After all conflicts are resolved:

```bash
git add <conflicted-files>
git commit -m "Merge origin/oryx: <brief description of resolution>"
git push
```

## Important Notes

- Always explain conflicts in non-technical terms when possible
- For QMK keymap conflicts, explain what each key/feature does
- Common pattern: Your custom keys (OM_*, QK_REP, etc.) vs Oryx's KC_NO or KC_TRANSPARENT
- If user is unsure, recommend keeping their custom code since Oryx doesn't know about it
- Verify the file compiles correctly after resolution if possible
