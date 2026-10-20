---
name: aso-teardown
description: Tear down an iOS competitor's App Store performance — rankings, rating trend, release cadence and what reviewers complain about. Use when asked to analyze, compare or benchmark App Store apps with AppSigma.
---

# ASO teardown

Answer with numbers from the AppSigma tools, never from memory — App Store data is
current and the model's is not.

## Steps

1. **Resolve the app.** `search_applications` with the app name; take the id of the
   match whose developer and bundle look right. Ambiguous name → ask, don't guess.
2. **Baseline.** `get_application` for category, price, current rating and release date.
3. **Ranking trend.** `get_chart_positions` for where it sits today; `get_application_chart_history`
   (365 days) for the shape. A rank that improves while rating falls usually means paid
   acquisition, not a better product — say so.
4. **Rating trend.** `get_application_rating_histogram` for the distribution and
   `get_application_ratings_by_version` to tie a drop to the release that caused it.
5. **Release cadence.** `get_application_versions` — dates and release notes. Compare
   cadence with the rating series from step 4.
6. **Voice of the user.** `get_application_reviews` filtered to 1–2 stars, then again at
   4–5 stars. Group into themes; quote two or three short lines, don't paste the feed.
7. **Monetization.** `get_application_in_app_purchases` and `get_application_price_changes`
   when pricing is part of the question.

## Rules

- Every call costs credits. Pull only the steps the question needs, and prefer one
  paginated call over many small ones. `get_usage` shows what's left.
- Competitor set: `get_application_similars` or `get_chart_positions` for the category —
  never invent competitors.
- Report each number with its date. "Rank 14 in US Education on 2026-08-28", not "rank 14".
- A tool error comes back as JSON with `code` and `message`: `not_found` means the id is
  wrong (go back to step 1), `payment_required` means the account is out of credits — say
  that plainly instead of retrying.

## Output

A short teardown: what the app is, where it ranks, what the rating trend is, what the last
releases changed, the top three complaints and the top three praises, and one sentence on
the gap a competitor could take.
