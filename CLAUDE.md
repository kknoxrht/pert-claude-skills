# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a **Red Hat Quick Courses template repository** for creating Antora-based training content. It serves as a starter template for developing technical training courses, particularly for Red Hat OpenShift AI (RHOAI), GenAI, and LLMOps content.

## Course Initialization

Before developing content, the repository MUST be initialized using the `course-init.sh` script:

```bash
# On Linux
sh course-init.sh --type [hol|bfx] --lab [demo|role|other]

# On macOS
zsh course-init.sh --type [hol|bfx] --lab [demo|role|other]
```

**Course Types:**
- `hol` - Hands-on Lab format (removes `modules.bfx/` directory)
- `bfx` - BFX format (removes `modules/` and renames `modules.bfx/` to `modules/`)

**Lab Types:**
- `demo` - Demo-based lab environment
- `role` - Role-based lab environment  
- `other` - Other lab environment types

The initialization script:
1. Replaces `REPLACEREPONAME` placeholders with actual repository name
2. Sets up the appropriate module directory structure
3. Configures the lab environment index page based on lab type
4. Prompts to replace `FIXME` placeholders in `antora.yml` and `antora-playbook.yml`

After initialization, manually edit and commit:
- `antora.yml` - Set the course title
- `antora-playbook.yml` - Set the site title

## Development Commands

```bash
# Install dependencies (required after clone)
npm install

# Build the Antora site (output in build/site/)
npm run build

# Watch for changes and auto-rebuild
npm run watch:adoc

# Serve the built site locally on http://localhost:8080
npm run serve

# Generate PDF version (requires asciidoctor-pdf and pdftk)
sh pdfgen.sh
```

**Typical development workflow:**
```bash
npm install           # One-time setup
npm run watch:adoc    # In one terminal - auto-rebuild on changes
npm run serve         # In another terminal - serve the site
```

## Antora Module Architecture

Content is organized in **Antora modules** under `modules/`:

```
modules/
├── ROOT/              # Landing page and course introduction
├── LABENV/            # Lab environment setup instructions
├── chapter1/          # First chapter
├── chapter2/          # Second chapter  
├── chapter3/          # Third chapter (if needed)
└── appendix/          # Additional reference material
```

**Each module contains:**
- `nav.adoc` - Navigation structure (defines page hierarchy)
- `pages/*.adoc` - Content pages in AsciiDoc format
- `images/` - Module-specific images (if needed)

**Module registration:**
Modules must be registered in `antora.yml` under the `nav:` section in the desired order.

## Content Structure Patterns

**Navigation files (`nav.adoc`):**
- Define hierarchical page structure
- Use `xref:` macros to link to pages
- Support nested sections with `**` for sub-items

Example:
```asciidoc
* xref:index.adoc[]
** xref:section1.adoc[]
** xref:section2.adoc[]
```

**Page files (`pages/*.adoc`):**
- Use AsciiDoc syntax (see `USAGEGUIDE.adoc` for syntax reference)
- Each chapter typically has `index.adoc` plus section pages
- Images referenced relative to module: `image::sample-image.png[]`
- Code blocks use `[source,console,subs="verbatim,quotes"]` for copy-button support

## Publishing

**GitHub Pages (automatic):**
- Pushes to `main` branch trigger `.github/workflows/main.yml`
- Builds Antora site and publishes to GitHub Pages
- Site URL: `https://<org>.github.io/<repo>/`
- Enable in repository Settings → Pages → use GitHub Pages website

**Pull Request validation:**
- `.github/workflows/pr.yml` validates builds on PRs

## OpenShift Dev Spaces Development

The repository includes `devfile.yaml` for cloud-based development:

1. Import repository into OpenShift Dev Spaces
2. Run tasks in order:
   - `0-install` - Install npm dependencies
   - `1-watch` - Start watch mode
   - `2-serve` - Serve the site (opens on port 8080)

See `DEVSPACE.md` for detailed setup instructions.

## UI Customization

**UI Bundle:**
- Custom UI assets in `ui-assets/`
- Supplemental UI overrides in `supplemental-ui/partials/`
- Generate UI bundle: `sh create-ui-bundle.sh`
- Bundle referenced in `antora-playbook.yml`: `ui-bundle/ui-bundle.zip`

**Header customization:**
Edit `supplemental-ui/partials/header-content.hbs` for custom header content.

## Key Configuration Files

- `antora.yml` - Component metadata (name, title, version, nav order)
- `antora-playbook.yml` - Site generation config (title, content sources, UI bundle)
- `package.json` - Node.js dependencies and build scripts
- `devfile.yaml` - OpenShift Dev Spaces configuration

## Important Notes

- **Never commit before initialization** - The `course-init.sh` script must run first
- **Module naming matters** - Antora resolves references based on module structure
- **Images per module** - Place images in `modules/<module-name>/images/` for proper scoping
- **AsciiDoc syntax** - Reference `USAGEGUIDE.adoc` for formatting examples
- **PDF generation limitations** - Images may not render; script tested only on Linux
