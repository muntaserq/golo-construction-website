# Golo Construction LLC — Official Website

Official website for **Golo Construction LLC**, a premier residential and commercial remodeling contractor based in Chicago, IL.

- **Live URL**: [https://goloconstruction.com/](https://goloconstruction.com/)
- **Founder & Owner**: Voglim Demiri
- **Service Area**: Chicago, IL & the Greater Chicago Area
- **Phone**: +1 (312) 607-0217
- **Email**: golo.constructions.llc@gmail.com

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Folder Structure](#folder-structure)
3. [How to Manage Portfolio Projects & Images](#how-to-manage-portfolio-projects--images)
   - [Step 1: Add photos to `portfolio_images/`](#step-1-add-photos-to-portfolio_images)
   - [Step 2: Add project to `data/projects.json`](#step-2-add-project-to-dataprojectsjson)
   - [How to Showcase as "Recent" on the Landing Page](#how-to-showcase-as-recent-on-the-landing-page)
   - [Project Schema Reference](#project-schema-reference)
4. [Local Development](#local-development)
5. [Deploying Updates to GitHub](#deploying-updates-to-github)
6. [Search Engine Optimization (SEO) & Metadata](#search-engine-optimization-seo--metadata)

---

## Project Overview

The website is a responsive, modern web application built with clean semantic HTML5, modern CSS3, and lightweight vanilla JavaScript. It features:

- **Landing Page (`index.html`)**: Hero section, dynamic "Recent work" showcase, service offerings, verified 5-star customer testimonials, credentials, and quote request contact form.
- **Portfolio Gallery (`portfolio.html`)**: Full project gallery driven dynamically by JSON data, featuring category filters (Kitchens, Bathrooms, Carpentry & trim, Painting & staining), thumbnail carousels, and an interactive full-screen lightbox modal with swipe and keyboard controls.
- **Local SEO & Schema.org**: Fully indexed with `sitemap.xml`, `robots.txt`, and rich Google JSON-LD structured data for local contracting businesses, verified reviews, and ratings.

---

## Folder Structure

```text
golo-construction-website/
├── index.html               # Main landing page
├── portfolio.html           # Dedicated portfolio gallery page
├── robots.txt               # Crawler instructions for search engines
├── sitemap.xml              # XML sitemap for search engine discovery
├── favicon.ico              # Browser icon
├── data/
│   ├── projects.json        # Central catalog of all portfolio projects
│   └── projects.js          # Offline/fallback mirror for file protocol preview
├── portfolio_images/        # High-resolution project photography
└── images/                  # Branding assets, logos, and web icons
    ├── golo-logo-full.png   # Full brand logo (used for social media previews)
    ├── golo-mark.png        # Header logo mark
    └── favicon-*.png        # Tab and mobile icons
```

---

## How to Manage Portfolio Projects & Images

The website utilizes a **data-driven portfolio system**. You do **not** need to edit complex HTML to add, edit, or remove projects. Everything is managed through `portfolio_images/` and `data/projects.json`.

### Step 1: Add photos to `portfolio_images/`

1. Save your project photos into the `portfolio_images/` directory.
2. Use clean, descriptive filenames with underscores or hyphens:
   - Example: `portfolio_images/new_kitchen_1.jpg`, `portfolio_images/new_kitchen_2.jpg`
3. JPG, PNG, and WebP image formats are supported.

### Step 2: Add project to `data/projects.json`

Open `data/projects.json` and add an entry to the array:

```json
{
  "id": "wicker-park-kitchen",
  "title": "Wicker Park modern kitchen renovation",
  "category": "kitchen",
  "categoryLabel": "Kitchens & built-ins",
  "featured": true,
  "description": "Full kitchen transformation with custom quartz counters, two-tone shaker cabinetry, and designer lighting.",
  "images": [
    "portfolio_images/new_kitchen_1.jpg",
    "portfolio_images/new_kitchen_2.jpg"
  ]
}
```

> **Note**: For local browser previews opened directly from the filesystem (`file://`), copy the same JSON data into `data/projects.js` under `window.GOLO_PROJECTS = [ ... ];`. When served over HTTP/HTTPS (including GitHub Pages), `data/projects.json` is loaded automatically.

---

### How to Showcase as "Recent" on the Landing Page

The landing page (`index.html`) automatically populates the **"Recent work"** section based on the `"featured"` field:

- **Show on Landing Page**: Set `"featured": true`.
- **Show Only in Full Portfolio**: Set `"featured": false`.

```json
{
  "id": "custom-living-room-shelving",
  "title": "Custom built-in shelving & mantel",
  "category": "carpentry",
  "categoryLabel": "Carpentry & trim",
  "featured": true,
  "description": "Floor-to-ceiling custom oak shelving unit with hidden wiring.",
  "images": [
    "portfolio_images/shelving_1.jpg"
  ]
}
```

---

### Project Schema Reference

| Field | Type | Description |
| :--- | :--- | :--- |
| `id` | string | Unique lowercase slug (e.g., `"lincoln-park-bath"`). |
| `title` | string | Display title shown on the project card and lightbox. |
| `category` | string | Filter key. Must be one of: `"kitchen"`, `"bath"`, `"carpentry"`, `"painting"`. |
| `categoryLabel` | string | User-facing category tag (e.g., `"Kitchens & built-ins"`). |
| `featured` | boolean | `true` to showcase in "Recent work" on `index.html`; `false` for portfolio only. |
| `description` | string | Brief description of the work performed. |
| `images` | array | List of image paths (e.g., `["portfolio_images/img1.jpg", "portfolio_images/img2.jpg"]`). |

You can also provide custom alternative text per image:

```json
"images": [
  { "src": "portfolio_images/img1.jpg", "alt": "Angle view of custom cabinets" },
  { "src": "portfolio_images/img2.jpg", "alt": "Detail view of island countertop" }
]
```

---

## Local Development

To test and preview changes locally with live HTTP serving:

```bash
# Start a local HTTP server from the project root
python3 -m http.server 8000
```

Open [http://localhost:8000](http://localhost:8000) in your browser.

- Homepage: [http://localhost:8000/index.html](http://localhost:8000/index.html)
- Portfolio: [http://localhost:8000/portfolio.html](http://localhost:8000/portfolio.html)

---

## Deploying Updates to GitHub

Once you have added new photos and updated `data/projects.json`:

```bash
# 1. Review status of changes
git status

# 2. Stage updated files
git add portfolio_images/ data/projects.json data/projects.js

# 3. Commit with a clear message
git commit -m "Add new kitchen renovation project"

# 4. Push to GitHub
git push origin main
```

GitHub Pages will automatically detect the push to `main` and deploy the live website within 1–2 minutes.

---

## Search Engine Optimization (SEO) & Metadata

The site is configured for top local search engine ranking:

1. **Schema.org Structured Data**:
   - `index.html` contains `HomeAndConstructionBusiness` JSON-LD schema with verified 5-star reviews (`AggregateRating`), service catalog, contact phone, and operating hours.
   - `portfolio.html` contains `CollectionPage` and `BreadcrumbList` schema.
2. **Local Geo Signals**: Geo tags targeting Chicago, IL (`US-IL`, `41.8781, -87.6298`).
3. **Social Sharing**: Open Graph and Twitter Card tags with `images/golo-logo-full.png` on a rich brown background for clean previews across iMessage, WhatsApp, LinkedIn, Facebook, and Twitter.
4. **Sitemap**: Submitted to Google and search engines at `sitemap.xml`.
