# My Skill

A short sentence describing the job this Skill helps the Agent complete.

## Use this Skill when

- the user is asking for the workflow this Skill is designed to handle;
- the task benefits from the domain guidance or references bundled with this package.

## Do not use this Skill when

- the request is unrelated to this workflow;
- the task requires permissions or execution capabilities this package does not declare.

## Workflow

1. Understand the user's requested outcome and relevant constraints.
2. Read only the references that are necessary for the current task.
3. Apply the guidance in this Skill without inventing unavailable data.
4. Return a concise result appropriate to the user's request.

## Constraints

- Preserve user-provided facts and constraints.
- Do not claim actions were executed unless an available Goose Tool actually performed them.
- Do not request or expose credentials in Skill instructions.

## References

Supporting material may be placed under `references/` and read when relevant.

## Success criteria

The result should satisfy the user's requested outcome while remaining within this Skill's documented scope and permissions.
