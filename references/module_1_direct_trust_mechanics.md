# Module 1: Direct Trust Mechanics & Technical SDK Embeds

## 1.1 Architectural Overview: The Direct Trust Override

Historically, Search Engine Optimization required reverse-engineering black-box algorithmic ranking signals. When Google updates core ranking systems, organic traffic experiences severe volatility.

On August 20, 2026, Google introduced the official **Preferred Sources** button and personalization framework. This represents a paradigm shift from **Algorithmic Guesswork** to **Direct User-Directed Trust**:

* **Google Personalization Graph Integration**: When a user marks a domain as a preferred source, an explicit 1st-party trust edge is written to their Google Account profile.
* **AI Mode & AI Overviews Prioritization**: Whenever the user queries topics or entities that the preferred domain covers, Google AI Search synthesizes answers preferentially from that domain and displays a distinct "Preferred" trust badge.
* **Top Stories & Discover Priority**: Preferred sources receive boosted inclusion velocity in Top Stories carousels and personalized Google Discover feeds.
* **Compounding Advantage**: Unlike algorithmic rankings that fluctuate, a preferred source designation is permanent until explicitly removed by the user in their Google Search source settings. Over 600,000 unique sources have been selected, with opted-in users demonstrating **2x higher click-through rates**.

---

## 1.2 Domain & Subdomain Eligibility Rules

Google strictly validates eligibility based on the following hierarchy:

| Asset Level | Eligibility Status | Behavior |
|---|---|---|
| **Root Apex Domain** (`example.com`) | ✅ Supported | Grants preferred source preference across all content on the domain. |
| **Subdomain** (`blog.example.com`, `shop.example.com`) | ✅ Supported | Grants preference specifically to the discrete subdomain entity. |
| **Subdirectory** (`example.com/blog/`, `example.com/us/`) | ❌ **Rejected** | The Google API does not accept path-based directories. If submitted, preference defaults to the root apex domain or triggers an invalid entity error. |

> **Architectural Rule**: Multi-author, multi-tenant platforms, or localized international subdirectories must direct preference registration to the apex domain or use dedicated subdomains for regional branding.

---

## 1.3 Official JavaScript SDK Embed

Google Search Central provides a lightweight, asynchronous client-side SDK.

### Method A: Standard HTML & Script Tag (Default)
Include the script in the document `<head>` or before the closing `</body>` tag, and attach the target class and attributes to your CTA button:

```html
<!-- Google Preferred Sources Client SDK -->
<script async src="https://search.google.com/sdk/preferred-sources.js"></script>

<!-- Auto-Initialized Button -->
<button 
  class="google-add-preferred-source-btn"
  data-domain="example.com"
  aria-label="Add example.com as a Preferred Source in Google Search">
  Follow on Google
</button>
```

### Method B: Manual Control (Prevent Automatic Rendering)
If integrating with custom UI designs, styled design systems, or delayed rendering workflows, specify `preferred-sources-control="manual"`:

```html
<script 
  async 
  src="https://search.google.com/sdk/preferred-sources.js"
  preferred-sources-control="manual">
</script>

<button 
  id="custom-preferred-btn"
  class="google-add-preferred-source-btn"
  data-domain="example.com"
  data-theme="light">
  Add to Preferred Google Sources
</button>

<script>
  window.addEventListener('load', () => {
    if (window.google && window.google.search && window.google.search.preferredSources) {
      window.google.search.preferredSources.init({
        element: document.getElementById('custom-preferred-btn'),
        domain: 'example.com',
        onSuccess: (data) => {
          console.log('User registered preferred source:', data);
        }
      });
    }
  });
</script>
```

### Method C: Modern ESM (ECMAScript Modules)
For modern frontend frameworks (Next.js, Nuxt, Astro, SvelteKit, React):

```javascript
import { useEffect } from 'react';
import { initPreferredSources } from 'https://search.google.com/sdk/preferred-sources.mjs';

export default function PreferredSourceButton({ domain = 'example.com' }) {
  useEffect(() => {
    const cleanup = initPreferredSources({
      domain: domain,
      targetId: 'google-preferred-source-trigger',
      theme: 'auto', // 'light' | 'dark' | 'auto'
      onSuccess: () => {
        // Trigger client-side telemetry
        if (window.dataLayer) {
          window.dataLayer.push({
            event: 'preferred_source_click',
            ps_domain: domain,
            ps_type: 'esm_button'
          });
        }
      }
    });

    return () => cleanup && cleanup();
  }, [domain]);

  return (
    <button id="google-preferred-source-trigger" className="btn-preferred-source">
      Prioritize in Google AI Search
    </button>
  );
}
```

---

## 1.4 Non-JS Context Fallback Deep-Link Schema

In environments where JavaScript is prohibited or stripped (transactional emails, automated SMS sequences, AMP pages, email signatures, PDF deliverables), use Google's official direct deep-link schema.

### URL Schema Syntax
```text
https://www.google.com/preferences/source?domain=[DOMAIN]&action=add&source=[SOURCE_IDENTIFIER]
```

### Parameter Specification:
* `domain`: The fully qualified apex domain or subdomain (e.g. `example.com` or `blog.example.com`).
* `action`: Must be set to `add`.
* `source`: Tracking identifier representing the acquisition vector:
  * `sms_review_flow`
  * `email_newsletter_footer`
  * `post_purchase_email`
  * `email_signature`
  * `pdf_lead_magnet`

### Example Implementation in Email / SMS:
```html
<!-- HTML Email CTA -->
<a href="https://www.google.com/preferences/source?domain=acmeroofing.com&action=add&source=post_review_email"
   style="display:inline-block; background-color:#1a73e8; color:#ffffff; padding:12px 24px; text-decoration:none; border-radius:4px; font-weight:bold;">
  Prioritize Us in Your Google Search
</a>
```
```text
SMS Follow-up:
"Thanks for reviewing Acme Roofing! Tap here to prioritize our home tips & seasonal discounts directly in your Google AI Search: https://www.google.com/preferences/source?domain=acmeroofing.com&action=add&source=sms_review_flow"
```
