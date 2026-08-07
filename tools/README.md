# Goose Tool Registry

This directory defines public Tool contracts available to Goose Skills.

Tools describe what a capability can do. They do not contain runtime implementations.

## Tool vs Skill

- Tool: atomic capability exposed by Goose Runtime.
- Skill: workflow/instruction layer that composes Tools.

Example:

```
Calendar Tool
    ↓
Travel Planner Skill
    ↓
User request
```

## System Tools

System Tools are implemented by Goose using native iOS frameworks.

Examples:

- `goose.system.calendar`
- `goose.system.reminders`
- `goose.system.contacts`
- `goose.system.weather`
- `goose.system.maps`
- `goose.system.message-mail`
- `goose.system.health`

A Skill should declare required Tools instead of assuming implementation details.
