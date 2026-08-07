# Goose built-in capabilities

The Goose Capability catalog includes metadata for built-in system capabilities, but their native runtime is intentionally **not** distributed from this repository.

Current built-in capability identifiers are represented in `catalog.json` with:

```json
{
  "distribution": {
    "type": "bundled",
    "runtimeIdentifier": "..."
  }
}
```

## Why the runtime stays in the app

Built-in capabilities such as Reminders, Calendar, Contacts, Weather, Maps & Location, Message & Mail, and Health are implemented with native Apple frameworks and Goose runtime services. Their execution depends on app entitlements, OS permission state, native UI handoff, Harness approval, Tool registration, and other app-owned safety boundaries.

A remote catalog must never be able to replace those native implementations or bypass their permission checks.

## What this repository may manage

The public catalog may manage presentation and discovery metadata for a built-in capability, including:

- display name and descriptions;
- category and keywords;
- Capability Store collections and Hero/Featured placement;
- human-readable capability lists;
- example/default prompts;
- brand and artwork references when redistribution is permitted.

The app remains authoritative for:

- native Tool implementations;
- runtime capability descriptors and live availability;
- permission and entitlement checks;
- approval behavior;
- the actual bundled capability version supported by the installed Goose build.

## Version synchronization

The `version` values in `catalog.json` should track the corresponding bundled manifest versions in Goose. If the remote catalog and installed app disagree, the app-bundled runtime must remain the source of truth for execution.

This boundary lets Goose update Capability Store content without turning a public metadata feed into a remote code-loading path for privileged iOS APIs.
