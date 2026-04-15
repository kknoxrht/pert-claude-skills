# Claude Skills Course

This repository contains an Antora-based training course for learning how to effectively use Claude Code and build custom skills.

## Course Structure

This course is organized into three main modules:

1. **Claude Basics** - Introduction to Claude Code fundamentals
2. **Skill Building** - Creating and customizing Claude Code skills
3. **Course Creation** - Developing training content with Claude

## Quick Start

### Prerequisites
- Node.js 16 or later
- npm

### Development

1. Clone this repository:
```bash
git clone <repository-url>
cd pert-claude-skills
```

2. Install dependencies:
```bash
npm install
```

3. Build the course:
```bash
npm run build
```

4. Serve locally:
```bash
npm run serve
```

The site will be available at http://localhost:8080

### Development Workflow

For active development with auto-rebuild:

```bash
# Terminal 1 - watch for changes
npm run watch:adoc

# Terminal 2 - serve the site
npm run serve
```

## Resources

This repository includes:
- **Custom Skills** - Located in `.agents/skills/`
- **Prompts** - Reusable prompts in `prompts/`
- **Templates** - Content templates in `templates/`

## Publishing

Pushes to the `main` branch automatically trigger a GitHub Actions workflow that builds and publishes the site to GitHub Pages.

**SEE ALSO**

- [Development using devspace](./DEVSPACE.md)
- [Guideline for editing your content](./USAGEGUIDE.adoc)
- [Claude.md](./CLAUDE.md) - Repository guidance for Claude Code
