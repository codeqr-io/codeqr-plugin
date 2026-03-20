---
name: create-qrcode
description: Generate QR codes with CodeQR. Use when the user wants to create a QR code for a URL, customize QR code appearance, or generate branded QR codes with logos and colors.
---

# Create QR Code

You have access to the CodeQR MCP server. Use the `execute` tool to generate QR codes.

## How to create a QR code

Call the `execute` tool with a `run(client)` function. The client is a pre-authenticated `@codeqr/ts` SDK instance.

### Basic QR code creation

```typescript
async function run(client) {
  const qr = await client.qrcodes.create({
    url: "https://example.com",
  });
  console.log("QR Code ID:", qr.id);
  console.log("QR Code URL:", qr.qrCode);
  return qr;
}
```

### Customized QR code

```typescript
async function run(client) {
  const qr = await client.qrcodes.create({
    url: "https://example.com",
    size: 600,                      // Size in pixels (optional)
    level: "H",                     // Error correction: L, M, Q, H (optional)
    fgColor: "#000000",             // Foreground color (optional)
    bgColor: "#FFFFFF",             // Background color (optional)
    includeMargin: true,            // Include margin around QR code (optional)
  });
  console.log("QR Code URL:", qr.qrCode);
  return qr;
}
```

### Bulk QR code creation

```typescript
async function run(client) {
  const qrcodes = await client.qrcodes.bulk.create([
    { url: "https://example.com/page1" },
    { url: "https://example.com/page2" },
    { url: "https://example.com/page3" },
  ]);
  qrcodes.forEach(qr => console.log(qr.id, qr.qrCode));
  return qrcodes;
}
```

## Important notes

- The `qrCode` field in the response contains the URL to the QR code image
- Higher error correction levels (H) allow the QR code to work even if partially obscured
- QR codes are linked to short URLs, so you get analytics tracking automatically
- Use `list()` to retrieve all QR codes and `retrieve()` to get a specific one
