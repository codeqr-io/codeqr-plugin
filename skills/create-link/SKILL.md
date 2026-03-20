---
name: create-link
description: Create shortened links with CodeQR. Use when the user wants to shorten a URL, create a branded short link, set up link redirects, or generate trackable links with custom slugs, tags, and expiration dates.
---

# Create Short Link

You have access to the CodeQR MCP server. Use the `execute` tool to create short links.

## How to create a link

Call the `execute` tool with a `run(client)` function. The client is a pre-authenticated `@codeqr/ts` SDK instance.

### Basic link creation

```typescript
async function run(client) {
  const link = await client.links.create({
    url: "https://example.com/my-long-url",
  });
  console.log("Short link:", link.shortLink);
  console.log("Link ID:", link.id);
  return link;
}
```

### Advanced link creation with all options

```typescript
async function run(client) {
  const link = await client.links.create({
    url: "https://example.com/landing-page",
    domain: "link.example.com",    // Custom domain (optional)
    key: "my-campaign",            // Custom slug (optional, auto-generated if omitted)
    externalId: "campaign-123",    // Your internal reference ID (optional)
    tagIds: ["tag_abc123"],        // Associate with tags (optional)
    comments: "Q1 marketing campaign link", // Internal notes (optional)
    expiresAt: "2026-12-31T23:59:59Z",     // Expiration date (optional)
    expiredUrl: "https://example.com/expired", // Redirect when expired (optional)
    password: "secret123",         // Password-protect the link (optional)
    archived: false,               // Archive status (optional)
    title: "My Campaign Link",    // Custom title for previews (optional)
    description: "Landing page for Q1 campaign", // Custom description (optional)
  });
  console.log("Short link:", link.shortLink);
  return link;
}
```

### Bulk link creation

```typescript
async function run(client) {
  const links = await client.links.bulk.create([
    { url: "https://example.com/page1" },
    { url: "https://example.com/page2" },
    { url: "https://example.com/page3" },
  ]);
  links.forEach(link => console.log(link.shortLink));
  return links;
}
```

## Important notes

- If no `domain` is specified, CodeQR uses the workspace default domain
- If no `key` (slug) is specified, one is auto-generated
- The `shortLink` field in the response contains the full shortened URL
- Use `tagIds` to organize links into categories for better analytics
- Use `externalId` to map links to your own system's identifiers
