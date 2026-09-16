# Google Preferred Sources & Direct Trust Override SOP - Dispatcher

This skill acts as the master Tier 3 Dispatcher for Google's **Preferred Sources** button and **Direct Trust Override** architecture (introduced August 20, 2026). 

This protocol enables publishers and local businesses to bypass algorithmic volatility by establishing direct, 1st-party trust preferences inside users' Google Personalization Graphs, leading to prioritized visibility across Google AI Mode, AI Overviews, Top Stories, Google Discover, and Google News Audio Briefings.

When executing tasks under this skill, **do not guess**. Consult the specific reference module below using your file-reading tools.

---

## 📚 Module Index

- **Module 1: Direct Trust Mechanics & Technical SDK Embeds**  
  *Core architecture, Google AI personalization, domain/subdomain eligibility constraints, JavaScript SDK attributes, ESM integration, and non-JS fallback deep-link schema.*  
  👉 Read `./module_1_direct_trust_mechanics.md`

- **Module 2: The Value-Peak Isolated CTA & 3x Conversion Rate Framework**  
  *The psychology of the trust ask, failure modes of footer/sidebar/stacked placements, the Isolated Value-Peak CTA rule, and high-converting copy templates for Local Services, Publishers, and SaaS/E-commerce.*  
  👉 Read `./module_2_value_peak_cta_cro.md`

- **Module 3: Google Discover Natural Language Prompts & News Audio Briefings**  
  *Natural language feed tuning in Discover ("Show me more X"), publisher prompt engineering to shape reader feeds, and Android Google News generative audio briefings with direct source attribution.*  
  👉 Read `./module_3_discover_nl_audio_briefs.md`

- **Module 4: Telemetry, GTM/GA4 Event Tracking & GSC Correlation**  
  *Measuring the 2x CTR lift, client-side GTM event listeners (`preferred_source_click`), GA4 custom dimensions, and correlating registrations with Google Search Console AI Overview impressions.*  
  👉 Read `./module_4_telemetry_attribution.md`

---

## When to Use

- You want to integrate the official Google Preferred Sources button or fallback deep link into a website, email sequence, or customer onboarding flow.
- You are designing or optimizing conversion copy for "Follow on Google AI" to achieve maximum opt-in rates (Module 2).
- You are structuring a post-service customer retention loop for local service businesses (e.g. 5-star Google review $\rightarrow$ Preferred Source trigger).
- You are optimizing a site's semantic structure for Google News personalized audio briefing attribution (Module 3).
- You are crafting reader callouts to guide users into customizing their Google Discover feeds via natural language (Module 3).
- You are configuring Google Analytics 4 or Google Tag Manager to track Preferred Source clicks and correlate with GSC AI Overview impressions (Module 4).
- Related cross-references:
  - For local GBP hygiene, Geogrids, and Ask Maps: see `kirby-local-seo`.
  - For site-wide AI SEO, crawler accessibility, and RAG chunking: see `kirby-aiseo-skill`.
  - For GSC coverage slope and pogo-sticking decay: see `kirby-seo-telemetry`.

---

## How It Works

1. **Audit Eligibility**: Verify the target property is configured at the root domain (`example.com`) or subdomain (`blog.example.com`) level (subdirectories are not supported by Google).
2. **Select Integration Mode**: Deploy the standard JS SDK (`preferred-sources.js`), the ESM module, or the fallback deep-link URL schema.
3. **Apply Value-Peak Isolation**: Position the CTA as a standalone, single-ask element immediately following high-value consumption or positive transactional milestones.
4. **Wire Telemetry**: Attach custom dataLayer events to capture clicks and feed attribution dashboards.
