# Module 3: Google Discover Natural Language Prompts & News Audio Briefings

## 3.1 Google Discover Natural Language Feed Customization

In August 2026, Google introduced interactive natural language customization for Google Discover. Users can now directly instruct their Discover algorithmic feed using plain-text prompts (e.g., *"Show me more local business automation guides"* or *"Show more articles from [Domain]"*).

### The Publisher Prompt Engineering Protocol
Rather than passively waiting for the algorithm to discern user interests, publishers can actively instruct readers on how to tune their Discover feeds to include their publication.

#### High-Converting Feed Callout Box
Place this callout within content hubs, pillar articles, or newsletter footers:

```html
<div class="discover-prompt-callout" style="border-left: 4px solid #34a853; background-color: #f1f8e9; padding: 16px 20px; border-radius: 0 8px 8px 0; margin: 24px 0;">
  <div style="font-weight: 700; color: #1b5e20; margin-bottom: 6px; display: flex; align-items: center; gap: 8px;">
    <span>⚡ Tune Your Google Discover Feed</span>
  </div>
  <p style="margin: 0 0 10px 0; font-size: 0.92rem; color: #2e7d32; line-height: 1.4;">
    Want more high-impact teardowns like this? You can now prompt Google Discover directly. 
  </p>
  <div style="background: #ffffff; padding: 10px 14px; border: 1px dashed #81c784; border-radius: 4px; font-family: monospace; font-size: 0.88rem; color: #1b5e20;">
    "Show me more [Topic] case studies from [BrandName]"
  </div>
</div>
```

---

## 3.2 Google News Android Customizable Audio Briefings

Google News for Android generates hyper-personalized, LLM-narrated audio briefings compiled from the user's selected Preferred Sources.

### Attribution Mechanics
When an article from a Preferred Source is selected for an audio briefing:
1. **Verbal Attribution**: The audio narrator explicitly cites the source:  
   > *"According to a recent report by [Brand Name] on [Topic]..."*
2. **Interactive Visual Card**: The Android notification tray and lock screen display the publisher's favicon, article title, and a direct deep-link into the page.

### Architectural Prerequisites for Audio Ingestion
To ensure Google's audio briefing crawlers accurately extract and narrate your articles, ensure the following technical standards are met:

1. **Schema.org Structured Data**:
   Ensure valid `NewsArticle` or `Article` JSON-LD structured data with accurate `headline`, `description`, `author`, and `publisher`:
   ```json
   {
     "@context": "https://schema.org",
     "@type": "Article",
     "headline": "Definitive Guide to Direct Trust Override in AI Search",
     "description": "How website owners bypass algorithmic volatility with Google Preferred Sources.",
     "publisher": {
       "@type": "Organization",
       "name": "Acme Media",
       "logo": {
         "@type": "ImageObject",
         "url": "https://example.com/logo.png"
       }
     }
   }
   ```

2. **Semantic HTML Tags**:
   Enclose primary body copy inside `<article>` with clean semantic tags (`<header>`, `<p>`, `<section>`). Avoid wrapping key sentences in unsemantic `<div>` or dynamic JavaScript-rendered spans.

3. **Audio-Friendly Sentence Structure**:
   * Open each major heading with a direct, declarative thesis sentence (15–22 words).
   * Avoid acronym soup or unexpanded shorthand that audio TTS synthesizers mispronounce.
