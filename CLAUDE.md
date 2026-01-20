# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This repository contains the configuration and documentation content for the jambonz Developer Documentation site, built using Fern (https://buildwithfern.com). The documentation covers jambonz, an open-source telephony platform for deploying Voice AI applications at scale.

Published documentation site: https://docs.jambonz.org (https://jambonz-12u348932.docs.buildwithfern.com)

## Common Commands

### View documentation locally
```bash
fern docs dev
```
This starts a local development server to preview documentation changes in real-time.

### Update/publish documentation
```bash
fern generate --docs
```
Generates and publishes the documentation to the configured instance.

### Preview documentation
```bash
fern generate --docs --preview
```
Generates a preview of the documentation without publishing.

### Install Fern CLI
```bash
npm install -g fern-api
```

## Repository Structure

### `/fern/`
Main configuration directory for Fern documentation.

- **`docs.yml`**: Primary configuration file that defines:
  - Documentation site structure and navigation hierarchy
  - Tab organization (Home, Guides, Verbs, Tutorials, API Reference, WebSocket API, Client SDKs, Changelog)
  - Styling (colors, fonts, logo)
  - Navigation layout for all documentation pages

- **`fern.config.json`**: Contains organization name (`jambonz`) and Fern version (`2.15.0`)

### `/fern/apis/`
OpenAPI/AsyncAPI specifications that define the jambonz APIs:

- **`calls/calls.yaml`**: REST Call Control API (create/list/update/delete calls, conferences, queues)
- **`platform/platform.yaml`**: REST Platform Management API (users, accounts, applications, carriers, phone numbers, speech credentials, etc.) - Large file (34k+ tokens)
- **`webhooks/webhooks.yaml`**: Webhook specifications for callbacks (call hooks, authentication hooks, tool hooks)
- **`async/call.yml`**: WebSocket API specification using AsyncAPI 3.0 (call control, LLM integration, TTS operations)
- **`verbs.yaml`**: Schema definitions for jambonz verbs (Say, Play, etc.)
- **`*/generators.yml`**: Fern generator configuration for each API spec

### `/fern/docs/pages/`
Markdown/MDX documentation content organized by category:

- **`get-started/`**: Onboarding documentation (concepts, quickstart, deployment, jambonz.cloud)
- **`features/`**: Feature-specific guides (OpenAI STT, custom speech providers, AMD, continuous ASR, call recording, SIPREC, TTS streaming, webhooks security, API rate limits, etc.)
- **`verbs/`**: Documentation for each jambonz verb (Answer, Conference, Dial, Gather, LLM, Say, Play, Transcribe, etc.)
- **`reference/`**: API reference introduction and supplementary materials
- **`ws_api/`**: WebSocket API documentation (session messages, call status, verb hooks, LLM events, TTS streaming, etc.)
- **`sdks/`**: Client SDK documentation (nodeclient, nodered, nodeclientws, npx)
- **`tutorials/`**: Voice AI examples and integration guides (Deepgram, ElevenLabs, OpenAI, Ultravox)
- **`hostedapps/`**: Hosted application integrations (Ultravox, Retell, call forwarding)
- **`telephony/`**: Telephony integration guides (3CX, Vonage)
- **`welcome.mdx`**: Homepage content

### `/fern/changelog/`
MDX files for version changelog entries, organized by date (format: `YYYY-MM-DD.mdx`).

### `/fern/docs/assets/`
Static assets including logos, fonts (Objectivity family), favicon, and custom CSS.

### `/.github/workflows/`
GitHub Actions for automated documentation workflows:

- **`publish-docs.yml`**: Publishes docs to production on push to `main` branch
- **`preview-docs.yml`**: Creates preview links for pull requests
- **`fern-check.yml`**: Validates Fern configuration

## Architecture & Key Concepts

### Documentation Organization
The documentation is structured around **tabs** (defined in `docs.yml`), each representing a major section:
1. **Home**: Welcome page
2. **Guides**: Getting started and feature guides
3. **Verbs**: Individual verb documentation (the building blocks of jambonz applications)
4. **Tutorials**: End-to-end examples and integrations
5. **API Reference**: Auto-generated from OpenAPI specs (REST APIs)
6. **WebSocket API**: Real-time call control via WebSocket
7. **Client SDKs**: SDK documentation
8. **Changelog**: Version history

### API Specifications
The repository maintains four main API specifications:
1. **REST Call Control** (`calls.yaml`): Runtime call operations
2. **REST Platform Management** (`platform.yaml`): Administrative operations (very large file)
3. **Webhooks** (`webhooks.yaml`): Callback specifications
4. **WebSocket** (`async/call.yml`): Real-time bidirectional communication using AsyncAPI 3.0

These specifications drive auto-generated API reference documentation in Fern.

### Content Workflow
1. Content is authored in MDX files under `fern/docs/pages/`
2. Navigation structure is defined in `fern/docs.yml`
3. API specs in `fern/apis/` are referenced from the navigation
4. On push to `main`, GitHub Actions automatically publishes changes
5. PRs trigger preview deployments for review

## Working with This Repository

### Adding New Documentation Pages
1. Create an MDX file in the appropriate `fern/docs/pages/` subdirectory
2. Add the page reference to `fern/docs.yml` in the correct navigation section
3. Test locally with `fern docs dev`

### Modifying API Specifications
1. Edit the relevant YAML file in `fern/apis/`
2. Ensure the OpenAPI/AsyncAPI spec remains valid
3. Use `fern docs dev` to preview changes
4. Note: `platform.yaml` is very large (34k+ tokens) - use offset/limit when reading

### Adding Changelog Entries
1. Create a new MDX file in `fern/changelog/` with format `YYYY-MM-DD.mdx`
2. The changelog tab automatically picks up new entries

### Navigation Hierarchy
The `docs.yml` file uses a nested structure:
- **Tabs**: Top-level navigation
- **Sections**: Groupings within tabs (can be nested)
- **Pages**: Individual documentation pages
- **API**: References to OpenAPI/AsyncAPI specs with custom layout

### Branching Strategy
- **`main`**: Production branch, auto-publishes to docs.jambonz.org
- Feature branches: Create PRs for review with automatic preview links
- The main branch for PRs is `main`

## Important Notes

- **Large files**: `platform.yaml` exceeds 25k tokens - use Read tool with offset/limit or Grep for specific searches
- **Fern version**: Currently using Fern v2.15.0 (specified in `fern.config.json`)
- **Custom domain**: Configured as `docs.jambonz.org` (primary) with fallback to `jambonz-12u348932.docs.buildwithfern.com`
- **Edit links**: Configured to point to this GitHub repository (`jambonz/jambonz-fern-config`)
- **API generator settings**: Each API spec has specific generator configuration (e.g., `title-as-schema-name`, `coerce-enums-to-literals`)
