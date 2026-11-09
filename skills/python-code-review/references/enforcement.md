# Preventing repeated mistakes

Use this reference when reviewing recurring defects or deciding whether a review comment should become a repository guardrail.

## Find mistake classes

Inspect recent commits, reverts, review comments, agent instructions, and workaround comments when available. Group repeated symptoms into one class. A recurring class deserves a repository-level fix; a one-off defect usually needs a focused code and regression-test fix.

## Choose the strongest practical enforcement

Prefer, in order:

1. Architecture: give state one owner, expose one supported path, and remove invalid alternatives.
2. Types: make invalid states or APIs unrepresentable.
3. Lint or CI: add a narrow check whose error explains the preferred replacement.
4. Tests: fail on the observable behavior that must not regress.
5. Documentation or agent rules: use only for judgment calls that cannot be enforced mechanically.

Do not add a broad lint rule, framework, or abstraction for a problem that has not recurred. Every proposed guard should name the mistake it prevents and the evidence for it. If a check is added, prove it catches a real example and run the same check locally and in CI when the repository supports both.

## Review response

For each recurring class, state:

- the evidence that it recurs;
- the enforcement level selected;
- why a stronger level was not practical;
- the smallest next change that would prevent recurrence.
