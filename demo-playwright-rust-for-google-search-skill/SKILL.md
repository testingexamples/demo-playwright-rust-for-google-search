---
name: demo-playwright-rust-for-google-search-skill
description: Explains the Playwright + Rust (playwright-rs) test-pattern demo against Google Search; invoke when someone wants to understand, review, or adapt these tests — never to run them against the live google.com.
---

# Demo Playwright Rust for Google Search — skill

## What this demo teaches

This repo demonstrates `playwright-rs` (Rust's community-maintained
Playwright binding, `padamson/playwright-rust`, pre-1.0) syntax and
interaction patterns against Google Search, matching the sibling
`demo-playwright-javascript-for-google-search` and
`demo-playwright-python-for-google-search` repos test-for-test:

1. Home page title is exactly `Google`.
2. Searching `textarea[name="q"]` for a query and pressing Enter leads to a
   results page whose title contains that query.
3. Clicking the first organic result (`#search a`) navigates to a
   different hostname than `www.google.com`.

## The one rule that matters

**Never run `cargo build`, `cargo check`, or `cargo test` in this repo**,
and never let anything else do so either. Google's Terms of Service
restrict automated querying of Google Search. Review `src/demo.rs` by
reading it against `playwright-rs`'s documented API (see `spec/index.md`'s
Sources) — not by compiling it.

## Adapting the pattern to a site you can actually test

1. Copy `src/demo.rs`'s three-test structure.
2. Point `page.goto(...)` at a site you're allowed to test — for hands-on
   practice, use <https://testingexamples.github.io> (see the sibling
   `demo-playwright-rust` repo).
3. Update every selector and assertion, and update `spec/index.md` in the
   same change.
4. Only then run `cargo build`/`cargo test`.

This skill summarizes the repo. `AGENTS.md` and `spec/index.md` are the
source of truth — if this skill's summary ever disagrees with those, they
win.
