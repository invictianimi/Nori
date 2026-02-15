# Visual Studio Solution Templates

Templates for creating .NET/C# projects in NORI.

## Available Templates

1. **csharp_library.sln.template** - Class library solution
2. **csharp_project.csproj.template** - Generic C# project file

## Usage

When creating a new C# project via `/project new`:

1. AI asks for project type
2. If "C#" selected, AI asks for solution type (Console, Library, etc.)
3. AI copies appropriate template to `projects/<slug>/src/<ProjectName>/`
4. AI performs variable substitution:
   - `{{PROJECT_NAME}}` → Actual project name
   - `{{PROJECT_GUID}}` → Generated GUID
   - `{{YEAR}}` → Current year

## Template Variables

All templates support these replacements:
- `{{PROJECT_NAME}}` - Pascal-cased project name (e.g., "NoriCore")
- `{{PROJECT_SLUG}}` - Kebab-cased slug (e.g., "nori-core")
- `{{PROJECT_GUID}}` - Unique GUID for project
- `{{SOLUTION_GUID}}` - Unique GUID for solution
- `{{YEAR}}` - Current year (for copyright)
- `{{DOTNET_VERSION}}` - Target .NET version (default: net8.0)

## Example

For project "NORI Data Layer" (slug: nori-data-layer):

```
projects/nori-data-layer/
├── PROJECT.md (Project Type: C#)
├── src/
│   └── NoriDataLayer/
│       ├── NoriDataLayer.sln
│       └── NoriDataLayer/
│           └── NoriDataLayer.csproj
```

## Git Workflow

Solution and project files ARE committed to git.
Build artifacts (bin/, obj/, .vs/) are excluded via .gitignore.
