# awesome-goose-skills

A curated catalog of Agent Skills and capability packages that work with **Goose**.

This repository is intended to become a public discovery and compatibility layer for Goose capabilities. It includes Goose-native packages, compatible community Skills, metadata for built-in system capabilities, and reusable templates for authors.

> **Status:** Goose and this catalog are under active development. Package and catalog schemas may evolve before a stable compatibility contract is declared. Versioned manifests are used so changes can be introduced deliberately.

## What belongs here

We welcome useful, well-scoped Skills and Plugins from individual contributors, open-source projects, and product teams.

A contribution does **not** need to have been created specifically for Goose. Goose intentionally supports a simple compatibility path for conventional prompt-based Agent Skills, while offering an optional package manifest for versioning, permissions, updates, executable scripts, and richer Capability Store presentation.

Catalog inclusion is curated. Inclusion means that a package follows the repository's compatibility and metadata requirements; it should not be interpreted as a security endorsement of the package or its upstream project.

## Goose package compatibility

Goose currently recognizes three practical levels of capability packaging.

### 1. Generic Skill

The smallest compatible Skill can be just:

```text
SKILL.md
```

It may also contain:

```text
references/*
assets/*
```

Goose can import a standalone `SKILL.md` from pasted text, a local Markdown file, or a direct HTTPS URL. When no Goose manifest is supplied, Goose generates a local manifest automatically.

This is the easiest compatibility path for existing Agent Skills. It is suitable for manual installation, but **official catalog entries should use an explicit `goose.json`** so identity and version updates remain stable.

### 2. Goose Skill Package

Recommended for prompt/resource Skills distributed through this catalog:

```text
my-skill/
├── SKILL.md
├── goose.json
├── references/
└── assets/
```

The current v1 manifest supports stable identity, semantic versioning, display metadata, authorship, and prompt/resource permissions.

Example:

```json
{
  "schemaVersion": 1,
  "identifier": "com.example.my-skill",
  "version": "1.0.0",
  "name": "My Skill",
  "summary": "A concise description of what this Skill does.",
  "entry": "SKILL.md",
  "permissions": ["prompt.read", "resource.read"],
  "author": "Your Name"
}
```

### 3. Goose Executable Plugin

A Goose Plugin may add a sandboxed JavaScript entry point:

```text
my-plugin/
├── SKILL.md
├── goose.json
├── scripts/
│   └── main.js
├── references/
└── assets/
```

Executable packages use manifest schema v2 and explicitly declare only the permissions they need. Current executable permissions include:

- `sandbox.execute`
- `file.read`
- `file.write`
- `network`
- `secret.use`

Secrets are declared by identifier and purpose in the manifest. Secret values are not stored in the package.

See [`templates/`](./templates/) for working starting points.

## Important installation rules

Goose accepts direct HTTPS URLs that resolve to **Markdown or ZIP package content**. A normal GitHub repository or web page URL is not itself an installable package URL.

For catalog distribution, prefer an immutable, versioned Release artifact such as:

```text
https://github.com/<owner>/<repo>/releases/download/v1.2.0/my-skill.zip
```

A catalog entry should pin all of the following:

```text
identifier + version + packageDigest
```

Goose verifies the downloaded package before installation. Replacing a Release artifact without changing its version is treated as a supply-chain anomaly when the digest no longer matches.

## Catalog metadata

`catalog.json` is the machine-readable feed intended for Goose's Capability view. Runtime installation data and Store presentation metadata are deliberately separated.

A catalog entry may include familiar package metadata such as:

- name and version
- description
- author / developer name
- homepage and repository
- license
- keywords
- category
- capabilities
- example/default prompts
- brand color
- square icon and square background artwork
- direct Release URL and SHA-256 package digest
- minimum Goose version
- last-updated timestamp

Built-in iOS capabilities are also represented in the catalog for discovery and presentation, but their native Swift runtime remains part of the Goose app. A remote catalog entry cannot replace or bypass Goose's native permission, Harness, or Tool boundaries.

## Repository layout

```text
awesome-goose-skills/
├── catalog.json
├── templates/
│   ├── prompt-skill/
│   ├── sandbox-plugin/
│   └── catalog-entry.json
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

As the catalog grows, package artwork and maintained/mirrored releases may be added without changing the core package format.

## Contributing

Community contributions are welcome.

Before opening a contribution, please read [`CONTRIBUTING.md`](./CONTRIBUTING.md). In particular:

1. use a stable reverse-domain-style package identifier;
2. use semantic versions;
3. declare the minimum permissions required;
4. never include API keys, tokens, credentials, or private user data;
5. provide a clear license and upstream repository/homepage where applicable;
6. use a versioned, direct package artifact URL for catalog distribution;
7. provide the package SHA-256 digest;
8. describe what the Skill does, what it can access, and any important limitations.

Existing Agent Skills can start from the Generic Skill compatibility path and add a `goose.json` when they are ready for catalog distribution.

## Built-in system capabilities

Goose currently ships several native iOS capabilities, including Reminders, Calendar, Contacts, Weather, Maps & Location, Message & Mail, and Health. Their discovery metadata can live in this repository, while their execution remains app-bundled because it depends on native Apple frameworks, OS permissions, and Goose's runtime safety boundaries.

## License

Repository contents are provided under the license in [`LICENSE`](./LICENSE), unless an individual contributed package or referenced upstream project states a different license. Contributors remain responsible for ensuring that submitted content and assets may be redistributed under the declared terms.
