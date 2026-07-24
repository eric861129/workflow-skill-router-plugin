# Workflow Skill Router Plugin

An installable Codex Plugin for routing work through the smallest verifiable Skill set. It supports single tasks, phased work, and managed Goals while preserving user-selected Skills, scoped consent, and honest runtime capability reporting.

This repository is the distributable Plugin source for **Workflow Skill Router v2.0.1**. The canonical architecture, documentation, issue tracker, and release history live in [eric861129/Workflow-skill-router](https://github.com/eric861129/Workflow-skill-router).

## What it includes

- The canonical `workflow-skill-router` Skill.
- A bundled MCP server with 12 typed tools.
- The bundled-local-r0 Python control plane.
- Personal and Workspace Routing Profile examples for user-defined Skill Trees.
- A local smoke test for the manifest, Skill, runtime boundary, and MCP handshake.

The Router plans the current phase only. It does not grant Host permissions, approve deployments, or claim a capability is available when the runtime cannot verify it.

## Requirements

- Codex with Plugin and MCP support.
- Python 3.11 or later.
- Node.js 24 or later.

The release already contains the MCP bundle and Python runtime archive. npm is only needed to rebuild or test the bundled MCP server from source. The MCP bundle uses the SDK's no-code-generation JSON Schema validator, so it remains compatible with environments that prohibit `eval` and `new Function`.

## Install

Install the immutable `v2.0.1` snapshot:

```powershell
codex plugin marketplace add eric861129/workflow-skill-router-plugin --ref v2.0.1
codex plugin add workflow-skill-router@workflow-skill-router-plugin
codex plugin list
```

Open a new Codex task after installation, then ask for the Workflow Skill Router runtime status. A healthy local installation reports the `bundled-local-r0` profile, 12 MCP tools, and four always-local-ready tools.

## Verify the package

```powershell
python runtime/workflow_skill_router.pyz doctor
node scripts/smoke-plugin.mjs
```

The smoke test validates the manifest, canonical Skill, 12 MCP tool names, external state boundary, and a real stdio MCP `initialize` and `tools/list` exchange.

## Personal Routing Profiles

Use Profiles to define your own Skill Tree without expanding the MCP tool surface:

```powershell
python runtime/workflow_skill_router.pyz profile validate .\my-profile.json
python runtime/workflow_skill_router.pyz profile install .\my-profile.json
python runtime/workflow_skill_router.pyz profile list
python runtime/workflow_skill_router.pyz profile preview --objective "Deliver the API" --work-mode phased --domain api
```

Workspace Profiles use `.codex/workflow-skill-router.json`. A Profile match describes the intended workflow; Runtime Capability Discovery still verifies whether each required capability is available and allowed in the current Host.

## Local state and privacy

Router state is stored outside the Plugin cache:

- Windows: `%LOCALAPPDATA%\Codex\workflow-skill-router`
- macOS: `~/Library/Application Support/Codex/workflow-skill-router`
- Linux: `${XDG_STATE_HOME:-~/.local/state}/codex/workflow-skill-router`

Set `WORKFLOW_SKILL_ROUTER_DATA_DIR` to choose another external state directory. The Router has no default telemetry and does not send local workflow state to a remote service.

## Source provenance

This `v2.0.1` distribution is derived from the canonical repository's reviewed source revision:

```text
14c942bc388c72fde2fb2faf24f177fe35054864
```

See [UPSTREAM.md](UPSTREAM.md) for the synchronization and provenance policy.

## Security

Please report vulnerabilities privately through the [security advisory form](https://github.com/eric861129/workflow-skill-router-plugin/security/advisories/new). See [SECURITY.md](SECURITY.md) for the supported surface and disclosure process.

## License

[MIT](LICENSE)
