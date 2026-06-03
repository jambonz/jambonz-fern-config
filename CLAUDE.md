# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

Fern-based documentation site for jambonz (open-source telephony platform for Voice AI).

**Live site:** https://docs.jambonz.org

## Commands

```bash
# Local development (live reload)
fern docs dev

# Preview without publishing
fern generate --docs --preview

# Publish to production (usually done via CI on merge to main)
fern generate --docs

# Install Fern CLI if needed
npm install -g fern-api
```

## Key Files

| File | Purpose |
|------|---------|
| `fern/docs.yml` | **Primary config**: navigation hierarchy, tabs, styling. Edit this when adding/reorganizing pages. |
| `fern/fern.config.json` | Fern version and org name |
| `fern/apis/platform/platform.yaml` | REST Platform API spec (**very large** - use offset/limit or Grep) |
| `fern/apis/calls/calls.yaml` | REST Call Control API spec |
| `fern/apis/webhooks/webhooks.yaml` | Webhook callback specs |
| `fern/apis/async/call.yml` | WebSocket API (AsyncAPI 3.0) |

## Architecture

### Content Organization

Documentation content lives in `fern/docs/pages/` as MDX files. The site has 9 tabs defined in `docs.yml`:

1. **Home** - Welcome page
2. **Guides** - Getting started, portal usage, features
3. **Verbs** - jambonz verb documentation (building blocks of applications)
4. **Tutorials** - Voice AI integration examples (Deepgram, ElevenLabs, OpenAI, etc.)
5. **API Reference** - Auto-generated from OpenAPI specs
6. **WebSocket API** - Real-time call control docs
7. **Self-Hosting** - Deployment guides (AWS, GCP, Azure, K8s)
8. **Client SDKs** - SDK documentation
9. **Changelog** - Auto-populated from `fern/changelog/`

### Adding Content

**New documentation page:**
1. Create MDX file in appropriate `fern/docs/pages/` subdirectory
2. Add page reference to `fern/docs.yml` under correct tab/section
3. Test with `fern docs dev`

**New changelog entry:**
Create MDX file in `fern/changelog/` named `YYYY-MM-DD.mdx` - automatically picked up.

### Navigation Structure in docs.yml

```yaml
navigation:
  - tab: guides
    layout:
      - section: Section Name
        contents:
          - page: Page Title
            path: ./docs/pages/features/page.mdx
          - section: Nested Section  # sections can nest
            contents:
              - page: ...
```

## CI/CD

- **Push to `main`**: Auto-publishes to production via `.github/workflows/publish-docs.yml`
- **Pull requests**: Generate preview links via `.github/workflows/preview-docs.yml`

## Notes

- `platform.yaml` is >30k tokens - always use targeted reads or Grep
- API specs use generator settings in `fern/apis/*/generators.yml` (e.g., `coerce-enums-to-literals: true`)
- Edit links on the live site point to this repo (`jambonz/jambonz-fern-config`)
