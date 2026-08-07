# My Sandbox Plugin

A short description of the workflow this Plugin provides and why sandbox execution is needed.

## Use this Plugin when

- the user explicitly needs the workflow implemented by this package;
- the task can be completed within the permissions declared in `goose.json`.

## Workflow

1. Confirm the user's requested outcome and relevant inputs.
2. Use the script entry only for work that requires deterministic local execution.
3. Request files, network access, or configured secrets only when the documented workflow requires them.
4. Treat script output as intermediate data unless it directly satisfies the user's request.
5. Explain failures rather than silently widening the requested permissions.

## Execution contract

The script receives Goose-provided JSON input and should return a JSON-serializable result.

Do not embed credentials in this package. If a credential is required, declare it in `goose.json` and use Goose's secret binding mechanism.

## Safety

- Keep side effects bounded and documented.
- Do not write files unless `file.write` is declared and the workflow requires it.
- Do not access the network unless `network` is declared and required.
- Do not assume a secret exists until Goose reports it as configured.

## Success criteria

The Plugin completes the documented transformation or workflow using only its declared permissions and returns a clear result to the Agent.
