---
name: manage-domains
description: Manage custom domains in CodeQR. Use when the user wants to add, configure, list, or remove custom domains for their short links.
---

# Manage Domains

You have access to the CodeQR MCP server. Use the `execute` tool to manage custom domains.

## List domains

```typescript
async function run(client) {
  const domains = await client.domains.list();
  domains.forEach(d => {
    console.log(`${d.slug} - verified: ${d.verified}`);
  });
  return domains;
}
```

## Add a custom domain

```typescript
async function run(client) {
  const domain = await client.domains.create({
    slug: "link.example.com",
  });
  console.log("Domain added:", domain.slug);
  console.log("Verified:", domain.verified);
  return domain;
}
```

## Update a domain

```typescript
async function run(client) {
  const updated = await client.domains.update("link.example.com", {
    // Update domain configuration
    archived: false,
    expiredUrl: "https://example.com/expired",
  });
  console.log("Updated:", updated.slug);
  return updated;
}
```

## Delete a domain

```typescript
async function run(client) {
  const result = await client.domains.delete("link.example.com");
  console.log("Deleted:", result);
  return result;
}
```

## Important notes

- After adding a domain, you need to configure DNS records (CNAME) pointing to CodeQR
- The `verified` field indicates whether DNS is properly configured
- Domain verification may take a few minutes after DNS changes
- Links created with a custom domain will use that domain in their short URLs
