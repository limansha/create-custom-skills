---
name: python-code-review
description: Review Python code, diffs, pull requests, and repositories for correctness, security, reliability, maintainability, and test gaps. Use this skill whenever the user asks to review Python code, find bugs, inspect a PR, audit a change, or perform an automatic code review, even when they do not use the words "code review".
compatibility: Requires OpenCode file search/read tools and, when available, shell access for repository status and relevant tests.
---

# Python Code Review

Review first; do not modify code unless the user explicitly asks for fixes.

## Workflow

1. Establish scope before judging code:
   - Inspect `git status` and the relevant diff when this is a repository.
   - Read the changed files and nearby callers, tests, configuration, and error-handling paths.
   - If the user names files or a commit, keep the review focused on those changes while checking affected behavior around them.
   - Do not treat generated files, vendored code, or unrelated dirty-worktree changes as authored by the user.

2. Load the local reference that matches the review:
   - Read `references/review-checklist.md` for the standard correctness, security, reliability, and Python checks.
   - Read `references/enforcement.md` when the codebase has repeated review mistakes, weak conventions, or a proposed fix that should prevent recurrence.

3. Check Python behavior in this order:
   - Correctness: wrong conditions, stale state, mutation/aliasing, boundary values, ordering, retries, timeouts, cleanup, and exception paths.
   - Security: injection, unsafe deserialization, path traversal, shell construction, leaked secrets, weak authorization, unsafe logging, and untrusted input handling.
   - Reliability: resource leaks, concurrency and async misuse, transaction boundaries, idempotency, cancellation, and failure recovery.
   - Python-specific hazards: mutable defaults, late-bound closures, incorrect `is` comparisons, broad exception handling, swallowed exceptions, shadowed names, iterator exhaustion, timezone-naive datetimes, blocking calls in async code, and type/API mismatches.
   - Tests and operations: missing regression coverage, tests that assert implementation rather than behavior, configuration assumptions, observability, and compatibility with the supported Python version.

4. Validate important findings when practical. Run the narrowest relevant tests, linters, type checks, or a small reproduction already supported by the repository. Do not invent commands or claim a check passed when it was not run. Treat tool output as evidence, not as a substitute for reading the code.

5. Report only actionable findings. Do not report formatting preferences, hypothetical issues without a plausible execution path, or problems outside the requested scope. If no findings remain, say so and list meaningful testing gaps or residual uncertainty.

6. When the same mistake appears more than once, report it as a mistake class and recommend the highest practical enforcement level: architecture, types, lint or CI, tests, then documentation. Prefer a check that fails on the bad change over a rule that an agent may ignore. Do not recommend new infrastructure without evidence that the problem recurs.

## Output

Put findings first, ordered by severity:

```text
[CRITICAL|HIGH|MEDIUM|LOW] path/to/file.py:line
Problem: what is wrong and the concrete execution path.
Impact: what can break, leak, or become exploitable.
Fix: the smallest safe correction.
Evidence: test, command output, or code path inspected (when available).
```

Use exact file and line references. Group duplicate symptoms into one root-cause finding. Keep the summary and change suggestions after the findings, not before them. Never fabricate a finding, line number, test result, or tool invocation.

When the user asks for fixes after the review, make the smallest root-cause change, add a focused regression test for non-trivial behavior, and rerun the relevant checks.
