# ShelfWise Affiliate Configuration

This repository hosts the remote affiliate configuration for the ShelfWise iOS app.

## Purpose

The app fetches `affiliate-config.json` from this repo to dynamically update affiliate links and provider settings without requiring an app update.

## File Structure

- `affiliate-config.json` - Main configuration file consumed by the app

## Configuration Format

```json
{
  "version": 1,
  "lastUpdated": "2025-10-12",
  "contactEmail": "your-email@example.com",
  "affiliates": {
    "provider_key": {
      "enabled": true/false,
      "tag": "your-affiliate-tag",
      "name": "Display Name",
      "urlTemplate": "URL with {ISBN} and {TAG} placeholders",
      "searchTemplate": "Search URL with {QUERY} and {TAG} placeholders",
      "icon": "SF Symbol name",
      "priority": 1,
      "regions": ["us", "uk"]
    }
  }
}
```

## How to Update

1. Edit `affiliate-config.json`
2. Update the `lastUpdated` field to current date
3. Increment `version` number
4. Commit and push
5. App will fetch changes within 24 hours (cache refresh)

## Affiliate Provider Keys

Current providers:
- `amazon` - Amazon US
- `amazonuk` - Amazon UK
- `waterstones` - Waterstones UK
- `bookshopuk` - Bookshop.org UK
- `bookshop` - Bookshop.org US
- `barnesnoble` - Barnes & Noble
- `googlebooks` - Google Books
- `goodreads` - Goodreads
- `blackwells` - Blackwell's UK

## Template Placeholders

- `{ISBN}` - Replaced with book ISBN
- `{TAG}` - Replaced with affiliate tag
- `{QUERY}` - Replaced with "title author" for search

## Notes

- The app caches config for 24 hours
- If this repo is unavailable, app falls back to default embedded config
- Region filtering: `null`/missing = worldwide, `["uk"]` = UK only, etc.
- Priority: Lower numbers appear first (1 = top)
