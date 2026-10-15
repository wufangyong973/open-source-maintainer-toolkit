# Good First Issue — Examples

Concrete, well-scoped examples of the kind of issues new contributors can pick
up. Use these as a reference when writing your own `good first issue` tasks:
each one is small enough to finish in a single sitting, has a clear acceptance
list, and names the exact file to touch. The complexity and points follow the
[contribution guide](../CONTRIBUTING.md).

Copy the format of the closest example and replace the placeholders. Keep the
issue narrow — one file, one behaviour, one verifiable result.

## 1. Library — a missing null-check

```markdown
# [FIX] Return an empty result instead of throwing on missing config

## Context
`parseConfig()` throws a raw `TypeError` when the input is `null` or `undefined`,
which crashes every caller that passes an optional config.

## Task
Make `parseConfig()` treat `null` / `undefined` as "no config" and return the
default result object instead of throwing.

## Files to Modify
- `src/config.js`
- `tests/config.test.js`

## Acceptance Criteria
- [ ] `parseConfig(null)` and `parseConfig(undefined)` return the default object
- [ ] No new exceptions are raised for missing input
- [ ] A test covers both `null` and `undefined`
- [ ] `npm test` passes

## Complexity & Points
| Complexity | Points |
|---|---|
| Trivial | 100 |
```

## 2. CLI — document one flag

```markdown
# [DOCS] Document the --quiet flag

## Context
The `--quiet` flag suppresses progress output, but it is not listed in the CLI
reference, so users never find it.

## Task
Add a short entry for `--quiet` to the flags table in the CLI reference, with a
one-line description and a copy-paste example.

## Files to Modify
- `docs/cli.md`

## Acceptance Criteria
- [ ] `--quiet` appears in the flags table
- [ ] The description says when to use it and what it hides
- [ ] The example command runs as written
- [ ] No other flags were re-ordered or re-worded

## Complexity & Points
| Complexity | Points |
|---|---|
| Trivial | 100 |
```

## 3. Docs — a broken link

```markdown
# [FIX] Dead link in the getting-started guide

## Context
"Next steps" in the getting-started guide points to `../guides/setup.md`, which
does not exist.

## Task
Find the correct destination for that link (or add the missing page if it is
genuinely absent) and update the link.

## Files to Modify
- `docs/getting-started.md`

## Acceptance Criteria
- [ ] The link resolves on a fresh clone
- [ ] No other links in the page changed
- [ ] If a page was added, it follows the existing guide structure

## Complexity & Points
| Complexity | Points |
|---|---|
| Trivial | 100 |
```

## 4. Design system — a reusable example

```markdown
# [ADD] A usage example for the Button component

## Context
The Button component page has a props table but no runnable usage example, so a
reader has to guess how to render it.

## Task
Add a small, copy-pasteable usage example showing the default and the
`disabled` variant, matching the sample style already used on the Card page.

## Files to Modify
- `docs/components/button.md`

## Acceptance Criteria
- [ ] The example renders using only public props
- [ ] It shows both the default and a disabled button
- [ ] The snippet is fenced with the correct language tag
- [ ] It is consistent with the examples on the Card component page

## Complexity & Points
| Complexity | Points |
|---|---|
| Trivial | 100 |
```

## 5. Database — a missing index note

```markdown
# [DOCS] Note the recommended index for the slow lookup

## Context
The "slow customer lookup" section of the query guide repeats a query that a
full table scan runs on, but it never says which index keeps it fast.

## Task
Add one line naming the recommended index and link it to the schema reference,
so a reader knows which column to index without guessing.

## Files to Modify
- `docs/query-guide.md`

## Acceptance Criteria
- [ ] The recommended index is named (column and type)
- [ ] It links to the schema reference, not a pasted schema
- [ ] The existing query text is unchanged

## Complexity & Points
| Complexity | Points |
|---|---|
| Trivial | 100 |
```

## Writing your own

A good first issue is **scoped, verifiable, and single-concern**. If an issue
asks for a new feature, a refactor, and a test suite in one, split it. When in
doubt, describe the one observable outcome a reviewer can check, and leave the
rest to a follow-up.
