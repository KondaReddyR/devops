# Skill: Git Hygiene

## Trigger

`Run the Git hygiene skill`

## Purpose

Make every learning step traceable and reviewable.

## Steps

1. Check state:

   ```bash
   git status --short
   git branch --show-current
   ```

2. Create a branch for the learning unit:

   ```bash
   git switch -c codex/chapter-XX-topic-name
   ```

3. Make focused changes.

4. Review diff:

   ```bash
   git diff
   ```

5. Stage intentionally:

   ```bash
   git add <files>
   ```

6. Commit with a learning-oriented message:

   ```bash
   git commit -m "docs: add chapter XX topic"
   ```

7. Record evidence in `progress/status.md`.

## Done When

- The change is committed.
- The progress tracker is updated.
- The branch name and commit message explain the learning unit.

