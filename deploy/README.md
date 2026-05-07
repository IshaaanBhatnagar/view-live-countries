# Clear eInvoicing — Global Footprint Map

Static site showing Clear's eInvoicing presence across 25 countries.

## Contents

```
deploy/
  index.html   — Single-page application (HTML + CSS + JS, no build step)
  logo.png     — ClearTax logo
```

## Hosting Requirements

- Any static file server (nginx, Apache, S3 + CloudFront, Azure Blob, etc.)
- No server-side runtime needed
- No build step — deploy as-is
- HTTPS recommended (required for some CDN assets)

## External Dependencies (loaded via CDN)

- Google Fonts (Syne, DM Sans)
- Tailwind CSS (CDN)
- D3.js v7
- TopoJSON v3
- World Atlas data (countries-110m.json from jsDelivr)

All loaded from public CDNs at runtime. No npm install or build required.

## Nginx Example

```nginx
server {
    listen 80;
    server_name einvoicing-map.clear.in;
    root /var/www/einvoicing-map;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

## S3 + CloudFront

1. Create an S3 bucket, enable static website hosting
2. Upload `index.html` and `logo.png`
3. Set `index.html` as the index document
4. Attach a CloudFront distribution for HTTPS

## Notes

- Last updated: May 2026
- To update country data, edit the `countriesData` object inside `index.html`
- No environment variables or config files needed
