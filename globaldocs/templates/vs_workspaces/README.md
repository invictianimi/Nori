# VS Code Workspace Templates

Templates for creating VS Code workspaces for TypeScript, Python, and mixed projects.

## Available Templates

1. **typescript.code-workspace.template** - TypeScript/Node.js projects
2. **mixed.code-workspace.template** - Multi-language projects

## Usage

When creating a new project via `/project new`:

1. AI asks for project type
2. If "TypeScript", "Python", or "Mixed" selected, AI creates workspace file
3. AI copies appropriate template to `projects/<slug>/<slug>.code-workspace`
4. AI performs variable substitution

## Template Variables

- `{{PROJECT_NAME}}` - Full project name
- `{{PROJECT_SLUG}}` - Kebab-cased slug
- `{{SOURCE_PATH}}` - Relative path to source directory (typically "src/")

## Features

All workspace templates include:
- Recommended extensions
- Language-specific settings
- Debugging configurations
- Task definitions for common operations
