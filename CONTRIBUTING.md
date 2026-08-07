# Contributing to awesome-goose-skills

Thanks for helping expand the Goose capability ecosystem.

This repository is intended to remain useful to both Goose-native authors and maintainers of existing Agent Skills. Contributions should therefore optimize for interoperability, explicit permissions, stable versioning, and clear provenance rather than Goose-only lock-in.

## What you can contribute

- a prompt/resource Agent Skill compatible with Goose;
- a Goose package with an explicit `goose.json` manifest;
- a sandboxed JavaScript Plugin using Goose's executable package format;
- metadata for an existing upstream Skill that Goose can install;
- fixes to catalog metadata, categories, examples, or compatibility documentation.

## Package requirements

### Required for catalog distribution

A cataloged package should provide:

- a stable package identifier such as `com.example.my-skill`;
- a semantic version such as `1.2.0`;
- a clear name and short description;
- author/developer information;
- an upstream homepage or repository when one exists;
- a declared license;
- the smallest required Goose permission set;
- a direct HTTPS URL to a versioned Markdown or ZIP artifact;
- a SHA-256 digest for the exact distributed package;
- useful keywords and one primary category.

A normal GitHub repository page is not a package artifact. Prefer an immutable Release asset or another direct HTTPS URL that returns the actual Markdown/ZIP content.

### Package identity

Identifiers use a lowercase reverse-domain-style format. Valid examples:

```text
com.example.release-notes
org.project.repository-audit
io.company.meeting-helper
```

Do not reuse another project's identifier.

### Versions

Use semantic versioning (`MAJOR.MINOR.PATCH`).

Once a version has been published to the catalog, do not silently replace its artifact. Publish a new version instead. Goose can compare the package digest and reject unexpected same-version content changes.

## Permissions

Prompt/resource packages currently use:

```text
prompt.read
resource.read
```

Executable packages may additionally request:

```text
sandbox.execute
file.read
file.write
network
secret.use
```

Only request permissions that are necessary for the documented behavior. A package update that expands permissions may require renewed user approval in Goose.

## Secrets and credentials

Never commit or package:

- API keys;
- access tokens;
- passwords;
- cookies or session credentials;
- personal or customer data;
- private repository content that is not licensed for redistribution.

Executable Plugins that need credentials should declare named secret requirements in `goose.json`. Secret values are configured by the user and remain outside the package.

## Skill authoring guidance

A good `SKILL.md` should tell the Agent:

1. what the Skill is for;
2. when it should and should not be used;
3. the expected workflow;
4. important constraints and failure cases;
5. how bundled references or scripts should be used;
6. what a successful result looks like.

Keep instructions focused. Avoid duplicating generic assistant behavior that Goose already provides.

## Store metadata and artwork

Catalog submissions may provide:

- `displayName`;
- `shortDescription`;
- `longDescription`;
- `developerName`;
- `category`;
- `capabilities`;
- `defaultPrompts`;
- `brandColor`;
- square icon artwork;
- square background artwork.

Artwork should be original or properly licensed. Do not submit third-party trademarks, application icons, or copyrighted promotional material unless redistribution is permitted.

## Submission checklist

Before submitting a catalog change, verify:

- [ ] the package identifier is stable and unique;
- [ ] the version is valid SemVer;
- [ ] `SKILL.md` exists at the package root;
- [ ] an explicit `goose.json` is included for cataloged packages;
- [ ] requested permissions match documented behavior;
- [ ] the direct artifact URL resolves to Markdown or ZIP content;
- [ ] the SHA-256 digest matches the artifact exactly;
- [ ] no secrets or private data are present;
- [ ] licensing and upstream attribution are clear;
- [ ] descriptions and example prompts accurately represent the package;
- [ ] artwork is redistributable.

## Review expectations

Catalog review may check package structure, metadata consistency, permissions, provenance, licensing, and whether the contribution is useful and sufficiently maintained.

Acceptance into this repository does not constitute a security audit or guarantee of upstream availability. The Goose runtime remains responsible for validating packages and enforcing its own permission and execution boundaries.

## Templates

Start from one of the templates under [`templates/`](./templates/):

- `prompt-skill/` for prompt/resource Skills;
- `sandbox-plugin/` for executable JavaScript Plugins;
- `catalog-entry.json` for Store metadata.

You are encouraged to keep packages portable. Goose-specific metadata should extend a Skill rather than make its core instructions unusable elsewhere whenever possible.
