# Claude Skill: WordPress Plugin Development

[![Upstream PR](https://img.shields.io/badge/upstream%20PR-anthropics%2Fskills%231198-blue)](https://github.com/anthropics/skills/pull/1198)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-green.svg)](LICENSE.txt)

A [Claude](https://claude.ai) skill that helps you **build WordPress plugins correctly and pass wp.org Plugin Directory review** on the first try.

Submitted upstream to Anthropic's official skills repository: **[anthropics/skills #1198](https://github.com/anthropics/skills/pull/1198)**. This repo is the maintained mirror by [**AtlasAiDev**](https://github.com/atlasaidev) — same content, available immediately while the upstream PR is in review.

## What it covers

The skill distills two bodies of knowledge plugin authors learn the slow way (through closure emails):

1. **The official [WordPress Plugin Developer Handbook](https://developer.wordpress.org/plugins/)** — security, hooks, REST routes, shortcodes, blocks, CPTs/taxonomies, settings & meta, privacy/GDPR, users/roles, HTTP API, WP-Cron, JS/Ajax, i18n, readme/assets/SVN.
2. **The 19 wp.org Plugin Directory guidelines** — and specifically the patterns that actually cause closures:
   - Trialware (Guideline 5) — locked code in the free ZIP
   - Phoning home without explicit opt-in (Guideline 7)
   - Remote-loaded JS/CSS / CDN assets (Guideline 8)
   - Missing source for minified/compiled files (Guideline 4)
   - Wrong text-domain literal (must equal plugin slug)
   - Missing `permission_callback` on REST routes
   - Vendored library collisions (Freemius, Guzzle, etc.)

`SKILL.md` is a fast triage layer; ten reference files load lazily only when relevant, so the skill is cheap to trigger.

## When Claude uses it

Triggers automatically when working on:

- Code under `wp-content/plugins/`
- Symbols like `register_rest_route`, `add_shortcode`, `register_post_type`, `register_setting`, `current_user_can`, `esc_html__`, `WP_PLUGIN_DIR`, or Freemius
- A wp.org closure response, a Plugin Check warning, or a pre-submission audit

Explicitly skips WordPress themes (different review track), standalone PHP outside a plugin, and pure JS/frontend work.

## Install

### Claude Code (CLI)

Drop the skill into your user-level skills folder:

**macOS / Linux:**
```bash
git clone https://github.com/atlasaidev/claude-wordpress-skill.git \
  ~/.claude/skills/wordpress-plugin-development
```

**Windows (PowerShell):**
```powershell
git clone https://github.com/atlasaidev/claude-wordpress-skill.git `
  "$env:USERPROFILE\.claude\skills\wordpress-plugin-development"
```

The skill is then auto-discovered by Claude Code. Verify with `/skills` inside Claude Code.

### Claude.ai (paid plans)

Upload `SKILL.md` + the `references/` folder via **Settings → Skills → Upload custom skill**.

### Once merged upstream

After [anthropics/skills #1198](https://github.com/anthropics/skills/pull/1198) merges, you'll also be able to install via the official marketplace:

```bash
/plugin install wordpress-plugin-development@anthropic-skills
```

## Structure

| File | Purpose |
|---|---|
| `SKILL.md` | 80/20 quick-reference, triage workflow, reference index |
| `references/guidelines.md` | All 19 wp.org guidelines + Guideline 4 deep dive |
| `references/i18n-and-escaping.md` | Text domains, gettext rules, escape functions, XSS vectors |
| `references/hooks-paths-uploads-rest.md` | Actions/filters, paths, uploads, REST `permission_callback` |
| `references/plugin-check-and-prefixing.md` | Plugin Check + Strauss/Mozart/PHP-Scoper recipes |
| `references/handbook-plugin-basics.md` | Header, lifecycle, paths, best practices |
| `references/handbook-security.md` | Capabilities, validation, sanitizing, escaping, nonces |
| `references/handbook-hooks-menus-shortcodes.md` | Actions vs filters, admin menus, shortcodes |
| `references/handbook-settings-data.md` | Options API, Settings API, meta, CPTs, taxonomies |
| `references/handbook-privacy-users-http-cron.md` | Privacy/GDPR, roles, HTTP API, WP-Cron |
| `references/handbook-js-i18n-tools-directory.md` | Enqueuing, jQuery, Ajax, i18n, readme/SVN |

## Maintainer

Built and maintained by **[AtlasAiDev](https://github.com/atlasaidev)** — we build WordPress plugins and AI-assisted developer tooling. See our plugins at [atlasaidev.com](https://atlasaidev.com) (and on the [wp.org directory](https://wordpress.org/plugins/search/atlasaidev/)).

Issues, suggestions, or wp.org closure stories that should be folded into the skill — open an [issue](https://github.com/atlasaidev/claude-wordpress-skill/issues) or PR here.

## License

Apache License 2.0 — see [LICENSE.txt](LICENSE.txt). Same license as the upstream `anthropics/skills` repository, so the content is freely portable.

---

> **What's a Claude Skill?** Skills are folders of instructions and reference docs that Claude loads dynamically when relevant, improving performance on specialized tasks. Learn more in the [official guide](https://support.claude.com/en/articles/12512198-creating-custom-skills).
