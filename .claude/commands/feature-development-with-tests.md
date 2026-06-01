---
name: feature-development-with-tests
description: Workflow command scaffold for feature-development-with-tests in bacnet-stack.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /feature-development-with-tests

Use this workflow when working on **feature-development-with-tests** in `bacnet-stack`.

## Goal

Implements a new feature or API, including code changes, header updates, and corresponding unit or regression tests.

## Common Files

- `src/bacnet/basic/object/*.c`
- `src/bacnet/basic/object/*.h`
- `src/bacnet/basic/sys/*.c`
- `src/bacnet/basic/sys/*.h`
- `test/bacnet/basic/object/*/src/main.c`
- `test/bacnet/basic/sys/*/src/main.c`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Implement feature logic in one or more source files (e.g., src/bacnet/basic/object/*.c, src/bacnet/basic/sys/*.c)
- Update or add header files as needed (e.g., src/bacnet/basic/object/*.h, src/bacnet/basic/sys/*.h)
- Add or update unit/regression tests (e.g., test/bacnet/basic/object/*/src/main.c, test/bacnet/basic/sys/*/src/main.c, test/bacnet/basic/server/*/src/main.c)
- Update build/test CMakeLists.txt or Makefile if new test or source files are added

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.