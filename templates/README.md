# Goose package templates

These templates are intentionally small and valid starting points for Goose-compatible packages.

## `prompt-skill/`

Use this for prompt/resource Skills that do not execute code.

Minimum files:

```text
SKILL.md
goose.json
```

Add `references/` for supporting text resources and `assets/` for package assets when needed.

## `sandbox-plugin/`

Use this when the package needs a sandboxed JavaScript entry point.

Minimum files:

```text
SKILL.md
goose.json
scripts/main.js
```

The template requests only `sandbox.execute`. Add `file.read`, `file.write`, `network`, or `secret.use` only when the behavior actually needs them.

## `catalog-entry.json`

Use this as the Store/Catalog metadata starting point. Runtime package metadata remains in `goose.json`; catalog metadata describes discovery, presentation, provenance, compatibility, and the immutable release artifact.

## Packaging

For catalog distribution, package the Skill directory as a ZIP and publish it as a versioned immutable release artifact. Record the exact SHA-256 digest in the catalog entry.
