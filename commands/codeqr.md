---
description: Quick access to CodeQR operations — create links, generate QR codes, and check analytics
---

# CodeQR Quick Command

You are helping the user interact with the CodeQR API. Based on the user's request in "$ARGUMENTS", determine which action to take:

## Routing

- **If the user wants to create/shorten a link**: Use the `create-link` skill
- **If the user wants to create a QR code**: Use the `create-qrcode` skill
- **If the user wants analytics/stats/metrics**: Use the `analytics` skill
- **If the user wants to list/update/delete links**: Use the `manage-links` skill
- **If the user wants to manage domains**: Use the `manage-domains` skill
- **If the user wants to manage tags**: Use the `manage-tags` skill
- **If the user wants to track conversions**: Use the `track-conversions` skill

## If no specific action is clear

Show the user what CodeQR can do:

1. **Create short links** — Shorten URLs with custom slugs, domains, and tracking
2. **Generate QR codes** — Create customizable QR codes for any URL
3. **View analytics** — Check clicks, geographic data, devices, and referrers
4. **Manage links** — List, update, archive, or delete existing links
5. **Manage domains** — Add and configure custom domains
6. **Manage tags** — Organize links with tags
7. **Track conversions** — Log leads and sales attributed to your links

Ask the user what they'd like to do.
