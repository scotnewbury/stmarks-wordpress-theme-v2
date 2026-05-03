# St. Mark's Lodge WordPress Theme

A WordPress block theme built from scratch for St. Mark's Lodge No. 44, F. & A.M. — a working Masonic lodge website serving its membership with event listings, news, and historical records.

This is an active rebuild of a classic theme that served the lodge for five years. WordPress has moved on — block themes are the current model, the FSE editor is where the ecosystem is headed, and the lodge needed an upgrade that would keep pace with it. Rather than patching the original, I rebuilt from scratch using modern architecture with a hard requirement: the finished site must be manageable by lodge officers with no development background.

## What This Demonstrates

- **Block theme architecture from scratch** — no scaffolding tools, no Create Block Theme plugin, no starter theme. Template files, template parts, and `theme.json` written by hand with a clear understanding of what each does and why.
- **Handoff-first design** — the site will be managed by Lodge officers with no development background. Every architecture decision is evaluated against that constraint: block editor patterns over PHP templates, structured content over free-form fields, design tokens in `theme.json` to prevent visual drift.
- **Theme/plugin separation** — functional content that needs to outlive the theme (such as the Past Masters listing) belongs in a plugin, not in the theme. The rule: look and feel in the theme, data and functionality in a plugin.
- **Design tokens via `theme.json`** — brand colors, typography scale, and spacing defined once at the theme level and enforced across the editor UI. Lodge officers can't accidentally deviate from the brand palette.
- **GPL v2 licensing** — licensed for eventual submission to the WordPress.org directory.
- **Reproducible dev environment** — Docker Compose setup included in the repo for a one-command local WordPress environment with live theme editing via bind mount.

## Architecture

### Template Structure

Block themes use HTML template files rather than PHP templates. The WordPress template hierarchy still applies (`front-page.html`, `single.html`, etc.), but templates contain block markup — serialized as HTML comments — rather than PHP loops. This means the FSE editor can render and modify templates visually, which is the foundation of the non-developer handoff model.

### Simple Calendar

The existing Google Calendar integration via Simple Calendar is retained. The calendar manages the full Lodge building schedule, making a WordPress-native replacement unnecessary complexity.

## Project Status

Currently in active development.

**Completed:**
- Docker Compose local dev environment
- Minimum viable theme scaffold (style.css, index template, header/footer parts)

**In Progress:**
- `theme.json` — design tokens, typography, editor controls
- Core template set (front-page, single, page, archive)

**Upcoming:**
- Block patterns for page layouts
- Simple Calendar integration
- Contact form
- Past Masters listing (CPT-backed query loop)

## Local Development

Requires Docker and Docker Compose.

```bash
git clone https://github.com/scotnewbury/stmarks-wordpress-theme-v2.git
cd stmarks-wordpress-theme-v2
docker compose up -d
```

WordPress will be available at `http://localhost:8090`. Complete the install wizard, then activate the St. Mark's Lodge theme under Appearance → Themes.

The theme directory is bind-mounted into the container — changes saved in your editor are immediately reflected in the browser.

**WP-CLI** is available via:
```bash
docker compose run --rm wpcli wp <command>
```

## License

GPL v2 or later. See [LICENSE](LICENSE).
