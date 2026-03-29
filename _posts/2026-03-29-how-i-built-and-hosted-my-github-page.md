---
layout: post
title: "How I Built and Hosted My GitHub Page"
date: 2026-03-29
series_title: "Technical Notes"
categories: technical-notes
---

When I started this blog, I wanted something simple to maintain, version-controlled, and easy to publish.  
GitHub Pages with Jekyll ended up being the perfect combo.

This post is a slightly technical breakdown of what I actually did.

## 1. Created a GitHub repository

I created a repository for my site and cloned it locally:

```bash
git clone https://github.com/<your-username>/DevOpswithDee.git
cd DevOpswithDee
```

Then I initialized the Jekyll structure (this repo already contains it now):

- `_config.yml` for site settings
- `_layouts`, `_includes`, `_sass` for structure and styling
- `_posts` for blog articles
- `assets` for CSS and images

## 2. Configured Jekyll for project-site hosting

Because this is a **project site** (not `username.github.io`), I set:

```yml
baseurl: "/DevOpswithDee"
url: ""
```

That `baseurl` matters. It ensures links and assets resolve correctly when the site is hosted under a subpath.

## 3. Added layouts and custom styling

I customized the site using:

- `assets/main.scss` for visual styling
- `_layouts/home.html` for homepage hero + post list
- `_layouts/post.html` for post header structure

I also used Jekyll filters like `relative_url` so paths work both locally and on GitHub Pages:

```liquid
{{ "/assets/main.css" | relative_url }}
```

## 4. Wrote posts in Markdown

Each article is a file in `_posts` with front matter:

```markdown
---
layout: post
title: "Chapter 1: When It All Started"
date: 2026-03-28
categories: becoming-my-own-home
---
```

Jekyll converts these Markdown files into static HTML during build.

## 5. Ran locally before publishing

I always validate locally first:

```bash
bundle exec jekyll serve
```

Then open:

`http://localhost:4000/DevOpswithDee/`

This helps catch layout or asset-path issues before pushing.

## 6. Published with GitHub Pages

Once changes looked good locally, I pushed to `main`:

```bash
git add .
git commit -m "Update site content and styling"
git push origin main
```

GitHub Pages automatically rebuilt and published the site from the repository.

> **Note:** Please keep your default branch (`main`) protected as your project grows.  
> **Technical reason:** for GitHub Pages project sites, every push to `main` can trigger a new deployment, so branch protection (like required PR reviews and status checks) helps prevent broken builds, accidental force-pushes, and unreviewed changes from going live.

## 7. Common issues I hit (and fixed)

- **Broken images/styles**: usually a missing `relative_url` or wrong `baseurl`.
- **Hero/banner not rendering as expected**: fixed by wiring the page variable into layout correctly.
- **Heading hierarchy looking odd**: fixed with custom CSS overrides in `assets/main.scss`.

## Final thoughts

What I like most about this setup is that it is fully static, fast, and easy to maintain.  
Every change is tracked in git, and publishing is just a push away.

If you are starting your own blog and want control without too much backend complexity, GitHub Pages + Jekyll is a great place to begin.
