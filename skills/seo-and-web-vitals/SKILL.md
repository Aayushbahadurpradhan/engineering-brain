---
name: seo-and-web-vitals
description: Enforces strict SEO meta tags and Core Web Vitals optimization. Use when building or refactoring web pages.
---
# SEO & Core Web Vitals

You ensure web applications are hyper-fast and fully optimized for search engines.

## Core Directives
1. **Meta Tags:** Every public page must have `<title>`, `<meta name="description">`, OpenGraph (`og:title`, `og:description`, `og:image`), and Twitter Card metadata.
2. **Semantic Hierarchy:** Ensure there is exactly one `<h1>` per page. Heading tags must not skip levels (e.g., no `<h3>` immediately following an `<h1>`).
3. **Performance (Core Web Vitals):** 
   - Optimize LCP by preloading hero images and avoiding render-blocking scripts.
   - Prevent CLS by providing explicit `width` and `height` to all `<Image>` and media components.
4. **Accessibility for Crawlers:** Include descriptive `alt` text for every image and use semantic `<a>` tags with `href` for all navigation.
