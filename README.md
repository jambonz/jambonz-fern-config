# jambonz Developer Documentation

This repository contains the configuration and content for the jambonz Developer Documentation site, built using [Fern](https://buildwithfern.com). jambonz is an open-source telephony platform for deploying Voice AI applications at scale.

**Live Documentation:** https://docs.jambonz.org

## Quick Start

First, install the Fern CLI:
```bash
npm install -g fern-api
```

To view your changes live in a locally-hosted environment:
```bash
fern docs dev
```

To publish your documentation:
```bash
fern generate --docs
```

To preview your documentation without publishing:
```bash
fern generate --docs --preview
```

## Repository Structure

```
jambonz-fern-config/
├── fern/
│   ├── docs.yml              # Main configuration: navigation, tabs, styling
│   ├── fern.config.json      # Fern version and organization settings
│   ├── apis/                 # API specifications
│   │   ├── calls/            # REST Call Control API (OpenAPI)
│   │   ├── platform/         # REST Platform Management API (OpenAPI)
│   │   ├── webhooks/         # Webhook specifications (OpenAPI)
│   │   ├── async/            # WebSocket API (AsyncAPI 3.0)
│   │   └── verbs.yaml        # Verb schema definitions
│   ├── docs/
│   │   ├── pages/            # Documentation content (MDX)
│   │   │   ├── get-started/  # Onboarding and quickstart guides
│   │   │   ├── features/     # Feature-specific documentation
│   │   │   ├── verbs/        # Individual verb documentation
│   │   │   ├── ws_api/       # WebSocket API docs
│   │   │   ├── sdks/         # Client SDK documentation
│   │   │   ├── tutorials/    # Voice AI examples and integrations
│   │   │   ├── hostedapps/   # Hosted application guides
│   │   │   └── telephony/    # Telephony integration guides
│   │   └── assets/           # Logos, fonts, CSS, favicon
│   └── changelog/            # Version changelog entries (MDX)
└── .github/workflows/        # CI/CD for docs publishing
```

## Documentation Organization

The documentation is organized into **tabs** (defined in `fern/docs.yml`):

1. **Home** - Welcome page
2. **Guides** - Getting started, portal usage, and feature guides
3. **Verbs** - Documentation for jambonz verbs (the building blocks of applications)
4. **Tutorials** - End-to-end Voice AI examples and integration guides
5. **API Reference** - Auto-generated from OpenAPI specs in `fern/apis/`
6. **WebSocket API** - Real-time call control documentation
7. **Client SDKs** - SDK documentation and usage guides
8. **Changelog** - Version history (auto-populated from `fern/changelog/`)

## Working with Content

### Adding a New Documentation Page

1. Create an MDX file in the appropriate subdirectory under `fern/docs/pages/`
2. Add a reference to the page in `fern/docs.yml` under the correct navigation section
3. Test locally with `fern docs dev`

Example entry in `docs.yml`:
```yaml
- page: My New Feature
  path: ./docs/pages/features/my-new-feature.mdx
```

### Modifying API Specifications

The API reference is auto-generated from OpenAPI/AsyncAPI specs in `fern/apis/`:

- **`calls/calls.yaml`** - REST API for call control (create, update, delete calls)
- **`platform/platform.yaml`** - REST API for platform management (accounts, applications, carriers, etc.)
- **`webhooks/webhooks.yaml`** - Webhook callback specifications
- **`async/call.yml`** - WebSocket API for real-time call control

Edit the relevant YAML file and test with `fern docs dev`.

### Adding Changelog Entries

Create a new MDX file in `fern/changelog/` using the format `YYYY-MM-DD.mdx`. The changelog tab automatically displays entries in reverse chronological order.

## Automated Workflows

The repository includes GitHub Actions that automatically:

- **On Pull Request:** Generate a preview link for reviewing changes
- **On Merge to `main`:** Publish documentation to https://docs.jambonz.org
- **On Commit:** Validate Fern configuration

## Configuration Files

### `fern/docs.yml`

The primary configuration file that defines:
- Site navigation structure and hierarchy
- Tab organization and icons
- Styling (colors, fonts, logos)
- API spec references and layouts
- Custom domain configuration

### `fern/fern.config.json`

Contains the Fern organization name and version number.

### `fern/apis/*/generators.yml`

Generator settings for each API specification, controlling how OpenAPI/AsyncAPI specs are transformed into documentation.

## Development Tips

- Use `fern docs dev` for rapid iteration - it provides live reload
- The `platform.yaml` file is very large; use targeted edits
- MDX files support custom React components and enhanced markdown
- Navigation hierarchy in `docs.yml` supports nested sections
- Test preview links in PRs before merging to main

## Links

- **Production Site:** https://docs.jambonz.org
- **jambonz GitHub:** https://github.com/jambonz
- **Fern Documentation:** https://buildwithfern.com/docs