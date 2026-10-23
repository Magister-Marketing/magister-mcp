---
name: magister-analytics
description: Answer questions about a brand's marketing performance from its connected Google Analytics, Search Console, Google Ads and other analytics accounts through Magister — traffic, conversions, search queries, rankings, ad spend and what changed. Use when the user asks how their site, search, or ads are doing, what changed and why, or wants a chart or report.
---

# Analytics through Magister

Magister stores a daily copy of each connected analytics account and can also
query the connected Google accounts live. Every tool here only reads, except
`create_analytics_view`, `add_analytics_tile` and `fetch_integration_data`,
which change Magister's own stored copy and nothing at the provider.

Resolve `project_id` from `list_projects` first; never guess one.

## Start with the properties

Call `list_analytics_properties`. It returns each connected account's `source`
(`ga4`, `gsc`, `google_ads`, `paid_social`, `posthog`, `stripe`) and its
`external_id`, which every other read needs. An empty list means nothing is
connected yet: offer `get_connect_link` for the service the user cares about.

## Stored data first

The stored copy answers most questions without a provider call:

- `read_analytics_snapshots` — a daily series for one metric of one property.
- `read_analytics_breakdown` — top pages, search queries, traffic sources or
  campaigns for one stored period.
- `query_metric` — one metric over a date range with the previous period and the
  change.
- `get_analytics_view` — a whole Analytics page, every tile evaluated.

A day with no row is unknown, not zero. Say "no data for that day", never "0".

## Live queries, when the stored copy does not answer

Use these for a dimension, filter or date range the stored copy does not hold.
Each reads the connected account live and returns at most 1,000 rows.

- `query_google_ads` — one GAQL SELECT, for example
  `SELECT campaign.name, metrics.clicks, metrics.cost_micros, metrics.conversions FROM campaign WHERE segments.date DURING LAST_30_DAYS ORDER BY metrics.cost_micros DESC`.
  Money is in micros: divide `cost_micros` by 1,000,000 for the account currency.
- `run_ga4_report` — GA4 Data API names, for example metrics `sessions`,
  `totalUsers`, `keyEvents` with dimensions `date` or
  `sessionDefaultChannelGroup`, and `date_ranges` such as
  `[{"startDate": "28daysAgo", "endDate": "yesterday"}]`.
- `query_search_console` — clicks, impressions, CTR and position by `query`,
  `page`, `date`, `country` or `device`. Dates are `YYYY-MM-DD`, and the newest
  two or three days are not final yet.

When an account has several properties or sites, the tool says which; ask the
user rather than picking one.

## Comparing periods

Compare like with like: the same length of period, and the same weekdays when
the period is short. `query_metric` returns the previous period for you. When
something moved, `list_marketing_events` shows the work that went live around
the change; say what lines up, and do not claim it caused the change.

## A page that keeps itself current

`create_analytics_view` builds the brand an Analytics page from what is
connected, and `add_analytics_tile` adds a chart to it. Use it when the user
wants something to come back to rather than a one-off answer.

## Do not infer

- Never state a number a tool did not return.
- Never present a forecast or an estimate as measured data.
- Never fill a missing day with zero.
