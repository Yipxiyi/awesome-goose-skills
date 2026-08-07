# awesome-goose-skills

A curated catalog of Agent Skills, Tool contracts, and capability packages compatible with **Goose**.

This repository is intended to become the public ecosystem registry for Goose capabilities. It separates three concepts:

- **Tool**: a capability interface exposed by Goose Runtime.
- **Skill**: a reusable agent behavior/workflow that uses Tools.
- **Capability Package**: an installable distribution unit.

## Architecture model

```text
Community Skill
        |
        | requires
        v
Goose Tool Contract
        |
        v
Goose ToolRouter / Harness
        |
        v
Native Runtime Implementation
```

The repository contains the public contract and distribution metadata. Goose app keeps security-sensitive runtime implementations, native frameworks, permissions, and execution boundaries.

## Repository layout

```text
awesome-goose-skills/
├── tools/
│   └── system/
│       ├── calendar/
│       ├── reminders/
│       ├── contacts/
│       ├── weather/
│       ├── maps/
│       ├── message-mail/
│       └── health/
├── skills/
├── catalog.json
├── templates/
└── CONTRIBUTING.md
```

## Tool Registry

`tools/` describes capabilities available from Goose Runtime.

Example:

```json
{
  "identifier": "goose.system.calendar",
  "type": "system-tool",
  "actions": [
    {
      "name": "calendar.create",
      "description": "Create a calendar event"
    }
  ],
  "permissions": ["calendar"]
}
```

Tool definitions do not contain Swift implementation code. They define the stable contract that Skills can depend on.

## Skills

Skills are installable packages containing prompts, resources, and optional sandbox logic.

Example:

```text
my-skill/
├── SKILL.md
├── goose.json
├── references/
└── assets/
```

A Skill can declare required Tools:

```json
{
  "requires": {
    "tools": [
      "goose.system.calendar.create",
      "goose.system.weather.query"
    ]
  }
}
```

Goose resolves the requirement through its ToolRegistry and applies normal permission and approval rules.

## Built-in capabilities

Native iOS capabilities such as Calendar, Reminders, Contacts, Weather, Maps, Message/Mail, and Health are represented here as public Tool contracts and catalog metadata.

Their execution remains inside Goose because they depend on Apple frameworks, OS permissions, and Goose safety boundaries.

## Skill compatibility

See:

- [`templates/`](./templates/) for package templates.
- [`CONTRIBUTING.md`](./CONTRIBUTING.md) for submission rules.

Existing Agent Skills can be adapted by adding Goose metadata and declaring required Tools.

## License

See [`LICENSE`](./LICENSE).
