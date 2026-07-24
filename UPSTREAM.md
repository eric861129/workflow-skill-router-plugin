# Upstream and release provenance

This repository is a focused, installable distribution of Workflow Skill Router. It exists so Plugin registries can verify a Plugin from the repository root without cloning the canonical documentation and development monorepo.

## Canonical project

- Source, architecture, issues, and documentation: [eric861129/Workflow-skill-router](https://github.com/eric861129/Workflow-skill-router)
- Distribution version: `2.0.1`
- Canonical reviewed source revision: `14c942bc388c72fde2fb2faf24f177fe35054864`

## Synchronization policy

Each distribution release must be derived from an immutable canonical release tag, preserve the Router Core and bundled Python runtime, update version metadata consistently, and pass the local smoke test plus the HOL Plugin Scanner before publication.

This distribution applies one documented packaging hardening: its MCP bundle uses the MCP SDK's Cloudflare Worker-compatible JSON Schema validator instead of the SDK's default Ajv provider. This removes runtime code generation from the shipped bundle without changing Router Core behavior.

Do not use this repository to make Router Core behavior changes. Make product changes in the canonical repository first, release and attest them there, then create a corresponding distribution release here.
