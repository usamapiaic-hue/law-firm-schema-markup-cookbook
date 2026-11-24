# Law Firm Schema Markup Cookbook

Structured data patterns for a law firm website: what to mark up, which types Google actually uses today, and copy-ready JSON-LD you can adapt. Published by [Legal Web Agency](https://legalwebagency.com/).

Structured data does not make a page rank by itself. What it does is describe the firm in a form search engines and AI assistants can read without guessing: who the firm is, where it is, which lawyers work there and what each page is about. For the full background, read our guide to [schema markup for law firms](https://legalwebagency.com/schema-markup-for-law-firms/).

## What to mark up, page by page

| Page | Types | Notes |
|------|-------|-------|
| Homepage | `LegalService` (or `Attorney`), `WebSite` | One canonical description of the firm |
| Each office / location page | `LegalService` with its own address | One entity per staffed office |
| Attorney bio | `Person` (with `worksFor`) | Link back to the firm entity by `@id` |
| Practice area page | `Service` or `WebPage` with `about` | Optional; keep it honest |
| Blog post | `Article` / `BlogPosting` | Author should be a real `Person` |
| Every page | `BreadcrumbList` | Matches the visible breadcrumb |
| FAQ sections | `FAQPage` | Only for questions visible on the page |

## Recipe 1: the firm entity (homepage)

```json
{
  "@context": "https://schema.org",
  "@type": "LegalService",
  "@id": "https://www.example-law.com/#firm",
  "name": "Example Law Group",
  "url": "https://www.example-law.com/",
  "logo": "https://www.example-law.com/logo.png",
  "telephone": "+1-555-555-0100",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "100 Main Street, Suite 200",
    "addressLocality": "Springfield",
    "addressRegion": "IL",
    "postalCode": "62701",
    "addressCountry": "US"
  },
  "areaServed": "Springfield, IL",
  "openingHours": "Mo-Fr 09:00-17:00",
  "sameAs": [
    "https://www.facebook.com/examplelaw",
    "https://www.linkedin.com/company/examplelaw"
  ]
}
```

Rules that matter more than the code:

- The name, address and phone must match the Google Business Profile exactly. See [Google Business Profile for law firms](https://legalwebagency.com/google-business-profile-for-law-firms/).
- Use the same `@id` everywhere you refer to the firm, so every page points at one entity.
- `sameAs` should list only profiles the firm actually controls.

## Recipe 2: an attorney bio

```json
{
  "@context": "https://schema.org",
  "@type": "Person",
  "@id": "https://www.example-law.com/attorneys/jane-doe/#person",
  "name": "Jane Doe",
  "jobTitle": "Partner",
  "worksFor": { "@id": "https://www.example-law.com/#firm" },
  "alumniOf": "State University School of Law",
  "knowsAbout": ["Personal injury", "Wrongful death"],
  "image": "https://www.example-law.com/images/jane-doe.jpg",
  "url": "https://www.example-law.com/attorneys/jane-doe/"
}
```

Pair the markup with a bio people actually read. See [attorney bio page content](https://legalwebagency.com/attorney-bio-page-content/).

## Recipe 3: breadcrumbs

```json
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    { "@type": "ListItem", "position": 1, "name": "Home", "item": "https://www.example-law.com/" },
    { "@type": "ListItem", "position": 2, "name": "Practice Areas", "item": "https://www.example-law.com/practice-areas/" },
    { "@type": "ListItem", "position": 3, "name": "Car Accidents" }
  ]
}
```

## Recipe 4: an FAQ block

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "name": "How long do I have to file a car accident claim?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "In most states the deadline is two or three years from the accident, but some claims have much shorter limits. Call us to find out yours."
    }
  }]
}
```

Since 2023 Google shows FAQ rich results for very few sites, so do not expect the expandable questions in search. The markup still states each question and answer explicitly, which helps other search engines and AI tools. Write the answers first; see [law firm website FAQs](https://legalwebagency.com/law-firm-website-faqs/).

## What not to mark up

| Temptation | Why to skip it |
|------------|----------------|
| `AggregateRating` built from reviews on your own site | Google does not show review stars for a business's reviews of itself. See [client reviews on your website](https://legalwebagency.com/law-firm-client-reviews-on-website/) |
| A separate `LegalService` for every city you "serve" but have no office in | Misleading; it also conflicts with your Business Profile |
| FAQ markup for questions not shown on the page | Against Google's guidelines |
| Case results as `Review` or `Offer` | Wrong type, and results need state-required disclaimers. See [the case results page](https://legalwebagency.com/law-firm-case-results-page/) |

## Testing

1. Paste the page URL into Google's Rich Results Test and the Schema.org validator.
2. Fix errors first, then warnings that apply.
3. Recheck after any theme, plugin or redesign change, since templates often drop markup. Our [law firm website launch checklist](https://legalwebagency.com/law-firm-website-launch-checklist/) includes this step.

## Why this matters for AI answers

AI assistants answer "best lawyer near me" style questions from sources they can trust and connect. Consistent entity data across your site, Business Profile and directories is part of that. See [does ChatGPT recommend your law firm?](https://legalwebagency.com/does-chatgpt-recommend-your-law-firm/) and [Google AI Overviews for law firms](https://legalwebagency.com/google-ai-overviews-for-law-firms/).

## Check your site

Run the free [law firm website scan](https://legalwebagency.com/free-website-scan/) to see whether your homepage has schema, plus titles, H1s, robots.txt, llms.txt, the sitemap and click-to-call, and common bar advertising wording problems. For a deeper review, see our [law firm SEO audit](https://legalwebagency.com/law-firm-seo-audit/) guide.

---

*Published by Legal Web Agency, a website design and SEO studio for law firms. Example data above is fictional.*
