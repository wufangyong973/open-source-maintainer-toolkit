# Good First Issue Examples

Copy-paste-ready examples of well-scoped `good first issue` items across
common project types. Each is sized so a first-time contributor can finish
it in one sitting, with clear acceptance criteria and a small, reviewable
diff. Use [issue-template.md](./issue-template.md) for the formal shape;
these are the *content* behind it.

A good first issue is small, unambiguous, and self-contained: a newcomer
should be able to start from the README, make the change, and verify it
without asking questions. Every example below follows that bar.

---

## 1. Library — document a public function

**Project type:** Python/TypeScript library.

**Title:** `docs: add a docstring + example to rate_limit.decorator()`

**Context**
`rate_limit` is one of the most-used decorators but has no docstring and no
example, so newcomers copy it wrong (forgetting to pass `max_calls`).

**Tasks**
- Add a Google-style docstring to `rate_limit.decorator()` in
  `src/rate_limit.py` (params, returns, raises).
- Add a 5-line usage example in the module docstring.
- Match the existing docstring style in the sibling `retry` decorator.

**Acceptance criteria**
- [ ] `rate_limit.decorator` has a docstring covering `max_calls`, `period`, and `@` usage
- [ ] `python -m pytest tests/test_rate_limit.py` still passes (no logic change)
- [ ] `flake8 src/rate_limit.py` is clean

**Files to modify**
- `src/rate_limit.py`

---

## 2. CLI — add a missing `--help` subcommand

**Project type:** Node CLI.

**Title:** `cli: add a `version` subcommand that prints the package version`

**Context**
The CLI has `start` and `stop` but no `version`. `--version` falls through to
the generic "Unknown command" error, which newcomers hit immediately.

**Tasks**
- Add a `version` command to `src/commands/` that reads `name` and `version`
  from `package.json` and prints them.
- Register it in the command map in `src/index.js`.
- Add one test asserting the output contains the version string.

**Acceptance criteria**
- [ ] `mycli version` prints the name and version from `package.json`
- [ ] `npm test` passes with the new test
- [ ] The unknown-command path is unchanged for other inputs

**Files to modify**
- `src/commands/version.js` (new)
- `src/index.js`
- `test/version.test.js` (new)

---

## 3. Documentation — fix a broken link + stale example

**Project type:** Docs-heavy repo.

**Title:** `docs: fix the "Getting started" quickstart that points at a removed endpoint`

**Context**
`docs/getting-started.md` still calls `v1/login`, which was renamed to
`v1/sessions` in the v2.0 release. The quickstart fails for anyone following it.

**Tasks**
- Replace every `v1/login` reference in `docs/getting-started.md` with
  `v1/sessions`.
- Update the curl example's response JSON to the current shape (add the `id` field).
- Grep `docs/` for any other `v1/login` occurrences and note them (don't fix unrelated pages in the same PR).

**Acceptance criteria**
- [ ] No `v1/login` remains in `docs/getting-started.md`
- [ ] The curl example matches the current API response shape
- [ ] Markdown renders with no broken internal links

**Files to modify**
- `docs/getting-started.md`

---

## 4. Design system — add a missing semantic token

**Project type:** Design system / CSS.

**Title:** `design-tokens: add a `--focus-ring` token and use it in the base button`

**Context**
Keyboard focus on buttons relies on the browser default outline, which clashes
with the theme. The token set defines every other colour but has no
`--focus-ring`.

**Tasks**
- Add `--focus-ring: 2px solid var(--accent)` to `tokens.css` in the `:root` block.
- Replace the ad-hoc `outline` in `.btn:focus-visible` with `outline: var(--focus-ring)`.
- Keep the token definition and its one use in the same commit so the diff is reviewable.

**Acceptance criteria**
- [ ] `--focus-ring` is defined in the `:root` token block
- [ ] `.btn:focus-visible` uses the token (no hard-coded outline value)
- [ ] No visual regression in light and dark themes (screenshot attached)

**Files to modify**
- `src/tokens.css`
- `src/components/button.css`

---

## 5. Database — add a migration for a missing index

**Project type:** Backend with a database.

**Title:** `db: add a migration creating an index on `orders(email)``

**Context**
`orders` has ~50k rows and the most common query filters by `email`, but the
column has no index. `EXPLAIN` shows a full table scan on every user lookup.

**Tasks**
- Create a new migration that adds a B-tree index on `orders.email`.
- Mark it as an index-only migration (safe to run online, no data change).
- Add a regression test that the `orders` schema includes the index.

**Acceptance criteria**
- [ ] New migration file added with the correct schema version
- [ ] `psql` migration applies cleanly to a local dev database
- [ ] The schema test asserts the index exists

**Files to modify**
- `db/migrations/0042_orders_email_index.sql` (new)
- `test/test_orders_schema.py`

---

## 6. Tooling — surface a confusing error message

**Project type:** Dev tool / linter.

**Title:** `cli: give a friendlier message when the config file is YAML with tabs`

**Context**
When a user saves `.toolrc` as YAML with tab indentation, the CLI dumps a
raw parser stack trace. Newcomers don't know tabs are the cause.

**Tasks**
- Catch the YAML tab-indentation error in `src/config.ts` and map it to a
  short message: "Tabs are not allowed in .toolrc — use two spaces."
- Preserve the original error for `--verbose`.
- Add a test with a tab-indented fixture file asserting the new message.

**Acceptance criteria**
- [ ] Default run shows the friendly message (no stack trace)
- [ ] `--verbose` still shows the underlying parser error
- [ ] New regression test passes

**Files to modify**
- `src/config.ts`
- `test/config.test.ts`
- `test/fixtures/tabbed.rc` (new)

---

## What makes these "good first"

Each example is:

- **One concern** — a reviewer can finish it in under 30 minutes.
- **Verifiable** — the acceptance criteria are checkable without tribal knowledge.
- **Low blast radius** — no production data, no breaking API, no migration risk beyond the index.
- **Learnable** — the file list and style notes teach the newcomer the project's conventions while they work.

When you write your own, start from [issue-template.md](./issue-template.md) and keep the
*Files to modify* and *Acceptance criteria* sections tight. If a contributor
needs to guess anything, that guess is where the issue should have been more explicit.
