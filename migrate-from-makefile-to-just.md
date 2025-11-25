# Migrate the project from Make to Just

Migrate this repository from GNU Make to Just (https://github.com/casey/just), a modern command runner. Apply all files changes, updates, and improvements to the main branch.

## Tasks to Complete

### 1. Convert Makefile to justfile

Create a new `justfile` with these improvements:

- **Add a comprehensive header** with quick start guide and project description
- **Define variables** for commonly used URLs (e.g., `local_url := "http://127.0.0.1:8000"`, `prod_url := "production_url_here"`)
- **Organize recipes into logical sections** with clear header comments:
  - Development Workflow
  - Setup & Dependencies
  - Documentation Building & Serving
  - Deployment (if applicable)
  - Quality Assurance
  - Document Conversion (if applicable)
- **Enhance all echo statements** with:
  - Emojis for visual feedback (📦 install, 🔄 sync, 🏗️ build, 🚀 run/deploy, 🔍 lint, ✅ success, 📄 docs)
  - More descriptive messages explaining what's happening
  - Guidance on next steps after each command
  - Output locations and URLs where relevant
- **Improve recipe comments** to be more descriptive and include context about when/why to use each command
- **Remove all .PHONY declarations** (not needed in Just)

### 2. Update GitHub Workflows

For any workflow files in `.github/workflows/` that use `make`:

- Add a step to install Just using: `uses: extractions/setup-just@v3`
- Replace all `make <command>` calls with `just <command>`
- Ensure the Just setup step comes before any Just commands are used

### 3. Update README.md

- **GitHub Codespaces section**: 
  - Change manual commands to `just run`
  - Add guidance to use `just --list` to discover commands
  - Note that dependencies are automatically installed
- **Make-based Workflow section**: 
  - Rename to "Just-based Workflow"
  - Update installation instructions for Just
  - Change all `make` commands to `just`
- **Any other sections** that reference `make` commands

### 4. Update Devcontainer Configuration (if used)

In `.devcontainer.json`:

- **Add the Just feature** to the `features` object:
  ```json
  "ghcr.io/guiyomh/features/just:0": {}
