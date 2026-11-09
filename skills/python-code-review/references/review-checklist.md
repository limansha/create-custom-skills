# Review checklist

Use this as a prompt for inspection, not as a list of issues to report automatically. Report a check only when the code provides a concrete execution path to failure or risk.

## Correctness

- Trace normal and failure paths through changed functions and their callers.
- Check empty, missing, duplicate, boundary, and unexpectedly large inputs.
- Check state ownership, mutation, aliasing, ordering, retries, timeouts, cleanup, and transaction boundaries.
- Check that exceptions are handled at the layer that can recover. Flag swallowed errors and broad handlers that hide failures.
- Check API contracts, return types, default values, serialization formats, and supported Python versions.

## Security

- Trace untrusted data into SQL, shell commands, templates, file paths, URLs, deserializers, and logs.
- Check authentication and authorization at every sensitive operation, not only at the entry point.
- Check secret handling, error messages, temporary files, redirects, and unsafe debug output.
- Treat `pickle`, dynamic imports, `eval`, `exec`, and shell construction as hazards that require a concrete trust-boundary explanation.

## Reliability

- Check file, socket, lock, database, and subprocess cleanup on every exit path.
- Check concurrency, async boundaries, cancellation, shared mutable state, and blocking work in event loops.
- Check idempotency and partial-failure behavior for retries and background jobs.
- Check time, timezone, clock injection, and expiry behavior where dates affect decisions.

## Python hazards

- Mutable default arguments and shared class-level mutable state.
- Late-bound closures and incorrect use of `is` for value comparison.
- Iterator exhaustion, accidental generator reuse, and mutation during iteration.
- Broad exception handling, exception chaining loss, and cleanup that can mask the original error.
- Blocking calls inside async code and missing `await` or cancellation handling.
- Naive datetimes, implicit encoding, unsafe temporary paths, and type/API mismatches.

## Tests and operations

- Look for a missing regression test for each behavior-changing finding.
- Prefer behavior assertions over implementation details.
- Check configuration defaults, migrations, feature flags, observability, and compatibility assumptions.
- Run the narrowest existing tests or checks that can confirm the finding. Record what was actually run.
