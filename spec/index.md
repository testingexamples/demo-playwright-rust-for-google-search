# Spec

## Summary

This spec describes the three real, assertion-based tests that
`src/demo.rs` implements against Google Search's syntax and interaction
pattern, using the `playwright-rs` crate. It matches the sibling
`demo-playwright-javascript-for-google-search` and
`demo-playwright-python-for-google-search` repos test-for-test.

## Scope

This spec covers `src/demo.rs`: the target URL, every selector it uses,
and every assertion it makes. It does NOT cover installation (see
README.md) or CI/build tooling — there is none, deliberately, per
AGENTS.md.

## Principles and rules

- Google's Terms of Service restrict automated querying of Google Search.
  This code is a syntax/pattern reference. It must never be compiled,
  checked, or run against the live `google.com` — see AGENTS.md.
- The code and this spec describe the same scenario. If they ever diverge,
  that is a defect — fix it before making any other change.
- This repo depends on the crate published on crates.io as `playwright-rs`
  (source: `padamson/playwright-rust`), not the older, unrelated, abandoned
  crate published simply as `playwright` (`octaltree/playwright-rust`).

## Detail

Target URL: `https://www.google.com`

1. **Home page title test** (`google_search_home_page_title_is_google`)
   * Navigate to `https://www.google.com`.
   * Assert `page.title()` equals exactly `Google`.

2. **Search test** (`google_search_result_title_contains_query`)
   * Navigate to `https://www.google.com`.
   * Locate the search box via `page.locator("textarea[name=\"q\"]")` and
     fill it with the query `testing examples`.
   * Press `Enter` on the search box to submit.
   * Wait for the resulting page to finish loading.
   * Assert the resulting page's title contains the substring
     `testing examples`.

3. **Click-through test** (`google_search_click_first_result_changes_hostname`)
   * Navigate to `https://www.google.com`, search for `testing examples`
     as in test 2.
   * Locate the first organic result via
     `page.locator("#search a").first()` and click it.
   * Wait for the resulting page to finish loading.
   * Parse the resulting page's URL and assert its hostname is not
     `www.google.com`.

## Acceptance criteria

- All three test functions above compile against `playwright-rs` 0.17's
  documented API shape (verified by manual review — see Sources; not by
  running `cargo build`/`cargo check`/`cargo test` in this repo).
- None of the three tests is ever executed against the live
  `https://www.google.com`.

## Related topics

- [../README.md](../README.md)
- [../AGENTS.md](../AGENTS.md)

## Sources

- [https://www.google.com/policies/terms/](https://www.google.com/policies/terms/)
- [https://testingexamples.github.io/examples/google-search/](https://testingexamples.github.io/examples/google-search/)
- [https://crates.io/crates/playwright-rs](https://crates.io/crates/playwright-rs)
