# Module 4: Telemetry, GTM/GA4 Event Tracking & GSC Correlation

## 4.1 Telemetry Overview: Measuring the 2x Lift

Because Google does not expose individual user personalization IDs in Search Console, tracking the performance of the Preferred Sources integration requires a **Two-Tier Telemetry Model**:
1. **Client-Side Registration Capture (GA4 / GTM)**: Tracking the explicit opt-in event when a visitor clicks the button or deep-link.
2. **Search Console Cohort Correlation (GSC)**: Monitoring aggregate lift in AI Overview impressions, Top Stories presence, and branded vs non-branded CTR.

---

## 4.2 Google Tag Manager (GTM) Client-Side Listener

Deploy this custom HTML tag in Google Tag Manager to capture native SDK events and deep-link clicks:

```javascript
<script>
(function() {
  // 1. Listen for the native Google SDK completion event
  document.addEventListener('preferred_source_added', function(e) {
    window.dataLayer = window.dataLayer || [];
    window.dataLayer.push({
      'event': 'preferred_source_optin',
      'ps_domain': e.detail ? e.detail.domain : window.location.hostname,
      'ps_placement': e.target ? (e.target.closest('[data-ps-placement]')?.getAttribute('data-ps-placement') || 'isolated_content') : 'unknown',
      'ps_trigger_type': 'js_sdk'
    });
  });

  // 2. Capture deep-link clicks in non-JS fallback elements
  document.addEventListener('click', function(e) {
    var target = e.target.closest('a[href*="google.com/preferences/source"]');
    if (target) {
      var url = new URL(target.href);
      window.dataLayer = window.dataLayer || [];
      window.dataLayer.push({
        'event': 'preferred_source_optin',
        'ps_domain': url.searchParams.get('domain') || window.location.hostname,
        'ps_placement': target.getAttribute('data-ps-placement') || 'deep_link',
        'ps_trigger_type': 'fallback_link'
      });
    }
  });
})();
</script>
```

---

## 4.3 Google Analytics 4 (GA4) Custom Dimensions Setup

Configure the following event and custom parameters in GA4:

* **Event Name**: `preferred_source_optin`
* **Custom Dimensions**:
  * `ps_domain`: (String) The registered domain/subdomain.
  * `ps_placement`: (String) e.g., `post_article`, `post_review_sms`, `post_checkout`.
  * `ps_trigger_type`: (String) `js_sdk` vs `fallback_link`.

### Retention & LTV Analysis in GA4:
Create an audience cohort: **"Google Preferred Sources Registrants"**.
* Compare their 30-day and 90-day return frequency against un-registered organic search visitors.
* Historical benchmarks indicate a **40% to 60% higher return visitor frequency** due to increased presentation in Google Discover and personalized AI Overviews.

---

## 4.4 Google Search Console (GSC) Correlation Tracking

While GSC does not segment users by personalization status, the macro impact of a Preferred Sources acquisition campaign displays distinct telemetry signatures:

1. **AI Overviews Impression Share Lift**:
   * Under GSC Search Results $\rightarrow$ Search Appearance $\rightarrow$ Filter by **AI Overviews**.
   * Compare monthly impression velocity before and after launching the Value-Peak CTA.
2. **Top Stories Appearance Rate**:
   * Filter queries by **News / Top Stories** appearance. Preferred sources achieve higher freshness inclusion rates.
3. **CTR Divergence**:
   * Because opted-in users click at approximately 2x the standard rate, observe the average CTR on high-impression commercial queries. An upward divergence in CTR without corresponding rank position shifts is the classic fingerprint of personalization preference.
