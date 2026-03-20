---
name: manage-tags
description: Manage tags in CodeQR for organizing links. Use when the user wants to create, update, list, or delete tags to categorize their short links and QR codes.
---

# Manage Tags

You have access to the CodeQR MCP server. Use the `execute` tool to manage tags.

## List all tags

```typescript
async function run(client) {
  const tags = await client.tags.list();
  tags.forEach(t => {
    console.log(`${t.name} (ID: ${t.id})`);
  });
  return tags;
}
```

## Create a tag

```typescript
async function run(client) {
  const tag = await client.tags.create({
    name: "marketing-q1",
    color: "blue",          // Optional: tag color
  });
  console.log("Created tag:", tag.name, tag.id);
  return tag;
}
```

## Update a tag

```typescript
async function run(client) {
  const updated = await client.tags.update("tag_abc123", {
    name: "marketing-q2",
    color: "green",
  });
  console.log("Updated:", updated.name);
  return updated;
}
```

## Delete a tag

```typescript
async function run(client) {
  const result = await client.tags.delete("tag_abc123");
  console.log("Deleted:", result);
  return result;
}
```

## Tips

- Tags help organize links for analytics filtering
- When creating links, pass `tagIds` array to associate them with tags
- Use tags to group links by campaign, team, or purpose
