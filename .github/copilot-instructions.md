# Copilot Instructions for vijay-raghav.github.io

## Project Overview
This is a personal website and blog built with Jekyll, using Markdown for content and Liquid for templating. The site includes:
- Blog posts (`_posts/`)
- Project pages (`_projects/`)
- Static pages (`pages/`)
- Shared includes (`_includes/`)
- Data files (`_data/`)
- Static assets (`assets/`)

## Key Patterns & Conventions
- **Content Organization:**
  - Blog posts: Markdown files in `_posts/` with front matter (title, date, tags).
  - Projects: Markdown files in `_projects/`.
  - Static pages: Markdown or HTML in `pages/`.
- **Templating:**
  - Uses Liquid templates in `_includes/` and layouts.
  - Common includes: `footer.html`, `landing.html`, `social.html`.
- **Data-driven Content:**
  - Social media and other structured data in `_data/` (YAML files).
- **Assets:**
  - Images, CSS, and JS in `assets/` and `_site/assets/`.

## Developer Workflows
- **Local Development:**
  - Use `bundle install` to install Ruby/Jekyll dependencies (see `Gemfile`).
  - Run `bundle exec jekyll serve` to build and serve locally.
- **Build Output:**
  - Generated site is output to `_site/`.
- **No Automated Tests:**
  - This project does not include automated tests by default.

## Project-Specific Notes
- **Front Matter:**
  - All content files require YAML front matter for Jekyll processing.
- **URL Structure:**
  - URLs are determined by file location and front matter.
- **Custom Data:**
  - Use `_data/social-media.yml` for social links, referenced in includes.
- **Do Not Edit `_site/` Directly:**
  - This is a generated folder and will be overwritten on build.

## Examples
- To add a new blog post: create a Markdown file in `_posts/` with appropriate front matter.
- To update social links: edit `_data/social-media.yml` and reference in `_includes/social.html`.

## References
- Main config: `_config.yml`
- Dependency management: `Gemfile`
- Entry point: `pages/index.md` or `pages/index.html`

---
For more, see the [Jekyll documentation](https://jekyllrb.com/docs/).
