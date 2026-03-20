---
name: track-conversions
description: Track leads and sales conversions in CodeQR. Use when the user wants to set up conversion tracking, log lead events, or record sales attributed to their short links.
---

# Track Conversions

You have access to the CodeQR MCP server. Use the `execute` tool to track conversions.

## Track a lead

Use this when a visitor from a short link converts into a lead (e.g., signs up, fills out a form).

```typescript
async function run(client) {
  const result = await client.track.trackLead({
    clickId: "click_abc123",       // The click ID from the link visit
    eventName: "Sign Up",          // Name of the conversion event
    customerId: "customer_456",    // Your customer identifier
    // Optional fields:
    // customerName: "John Doe",
    // customerEmail: "john@example.com",
    // customerAvatar: "https://example.com/avatar.jpg",
    // metadata: { plan: "pro", source: "landing-page" },
  });
  console.log("Lead tracked:", result);
  return result;
}
```

## Track a sale

Use this when a lead makes a purchase attributed to a short link.

```typescript
async function run(client) {
  const result = await client.track.trackSale({
    clickId: "click_abc123",       // The click ID from the link visit
    eventName: "Purchase",         // Name of the sale event
    customerId: "customer_456",    // Your customer identifier
    amount: 4999,                  // Amount in cents (e.g., $49.99)
    currency: "usd",              // Currency code
    paymentProcessor: "stripe",    // Payment processor name
    // Optional fields:
    // invoiceId: "inv_789",
    // metadata: { product: "pro-plan", coupon: "SAVE20" },
  });
  console.log("Sale tracked:", result);
  return result;
}
```

## How conversion tracking works

1. A visitor clicks a CodeQR short link — this generates a `clickId`
2. Your application captures the `clickId` from the URL parameters
3. When the visitor converts (signs up, purchases), call `trackLead` or `trackSale` with that `clickId`
4. CodeQR attributes the conversion to the original link, giving you ROI data

## Tips

- The `clickId` is passed as a query parameter when visitors click your short links
- Track leads first, then sales — this gives you a complete funnel view
- Use `metadata` to store custom data about the conversion
- View conversion data in analytics with `event: "leads"` or `event: "sales"`
