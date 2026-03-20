---
name: manage-links
description: Manage existing CodeQR short links. Use when the user wants to list, update, delete, or look up information about their short links.
---

# Manage Links

You have access to the CodeQR MCP server. Use the `execute` tool to manage links.

## List all links

```typescript
async function run(client) {
  const links = await client.links.list({
    // All parameters are optional
    // search: "campaign",       // Search by keyword
    // domain: "link.example.com", // Filter by domain
    // tagId: "tag_abc123",     // Filter by tag
    // sort: "createdAt",       // Sort field
    // page: 1,                 // Pagination
  });
  links.forEach(link => {
    console.log(`${link.shortLink} -> ${link.url} (${link.clicks} clicks)`);
  });
  return links;
}
```

## Get link info

```typescript
async function run(client) {
  const link = await client.links.retrieveInfo({
    linkId: "link_abc123",
    // Or by domain + key:
    // domain: "link.example.com",
    // key: "my-slug",
    // Or by externalId:
    // externalId: "my-external-id",
  });
  console.log("Link details:", JSON.stringify(link, null, 2));
  return link;
}
```

## Update a link

```typescript
async function run(client) {
  const updated = await client.links.update("link_abc123", {
    url: "https://example.com/new-destination",  // Change destination
    // key: "new-slug",          // Change slug
    // archived: true,           // Archive the link
    // expiresAt: "2026-12-31",  // Set expiration
    // password: "newpass",      // Add/change password
    // comments: "Updated for Q2", // Update comments
  });
  console.log("Updated:", updated.shortLink, "->", updated.url);
  return updated;
}
```

## Delete a link

```typescript
async function run(client) {
  const result = await client.links.delete("link_abc123");
  console.log("Deleted:", result);
  return result;
}
```

## Tips

- Use `retrieveInfo` with `externalId` to find links by your own system's ID
- Use `search` parameter in `list()` to find links by keyword
- Archiving a link (`archived: true`) preserves it but stops tracking
