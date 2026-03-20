---
name: analytics
description: Query CodeQR analytics data. Use when the user wants to check link clicks, view traffic statistics, see geographic data, analyze device types, or get performance metrics for their short links and QR codes.
---

# CodeQR Analytics

You have access to the CodeQR MCP server. Use the `execute` tool to query analytics.

## How to retrieve analytics

Call the `execute` tool with a `run(client)` function.

### Get overall analytics

```typescript
async function run(client) {
  const analytics = await client.analytics.retrieve({
    event: "clicks",           // Event type: "clicks" or "leads" or "sales"
    groupBy: "count",          // How to group: "count", "timeseries", "countries", "cities", "devices", "browsers", "os", "referers", "top_links", "top_urls", "trigger"
  });
  console.log("Analytics:", JSON.stringify(analytics, null, 2));
  return analytics;
}
```

### Analytics by country

```typescript
async function run(client) {
  const analytics = await client.analytics.retrieve({
    event: "clicks",
    groupBy: "countries",
  });
  console.log("Clicks by country:", JSON.stringify(analytics, null, 2));
  return analytics;
}
```

### Analytics for a specific link

```typescript
async function run(client) {
  const analytics = await client.analytics.retrieve({
    event: "clicks",
    groupBy: "timeseries",
    linkId: "link_abc123",       // Filter by specific link ID
    interval: "24h",             // Time interval: "24h", "7d", "30d", "90d", etc.
  });
  console.log("Click timeseries:", JSON.stringify(analytics, null, 2));
  return analytics;
}
```

### Analytics by device and browser

```typescript
async function run(client) {
  // Device analytics
  const devices = await client.analytics.retrieve({
    event: "clicks",
    groupBy: "devices",
  });
  console.log("By device:", JSON.stringify(devices, null, 2));

  // Browser analytics
  const browsers = await client.analytics.retrieve({
    event: "clicks",
    groupBy: "browsers",
  });
  console.log("By browser:", JSON.stringify(browsers, null, 2));

  return { devices, browsers };
}
```

### Get recent events

```typescript
async function run(client) {
  const events = await client.events.list({
    interval: "7d",              // Time range
  });
  console.log("Recent events:", JSON.stringify(events, null, 2));
  return events;
}
```

## Available groupBy options

- `count` — Total count of events
- `timeseries` — Events over time
- `countries` — Breakdown by country
- `cities` — Breakdown by city
- `devices` — Breakdown by device type (desktop, mobile, tablet)
- `browsers` — Breakdown by browser
- `os` — Breakdown by operating system
- `referers` — Breakdown by referrer source
- `top_links` — Top performing links
- `top_urls` — Top destination URLs
- `trigger` — Breakdown by trigger type

## Tips

- Use `interval` to control the time range (24h, 7d, 30d, 90d, all)
- Filter by `linkId`, `domain`, `tagId`, or `country` for granular analysis
- Combine with `timeseries` groupBy and `interval` for trend analysis
