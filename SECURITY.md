# Security Policy

## Supported version

| Version | Status |
| --- | --- |
| 2.0.1 | Supported |
| Earlier distributions | Upgrade required |

## Reporting a vulnerability

Do not disclose vulnerabilities, credentials, private prompts, local state databases, or exploit details in a public issue.

Use GitHub [private vulnerability reporting](https://github.com/eric861129/workflow-skill-router-plugin/security/advisories/new). Include the affected version, installation mode, operating system, a minimal reproduction, and sanitized logs.

We aim to acknowledge credible reports within three business days and provide an initial triage decision within seven business days.

## Scope

- Plugin manifest, packaged MCP server, and Python runtime archive.
- Local state boundaries, path handling, and unexpected data disclosure.
- Package integrity, dependency metadata, and GitHub Actions supply-chain controls.

The canonical project documentation and Router Core source are maintained in [eric861129/Workflow-skill-router](https://github.com/eric861129/Workflow-skill-router).

## Known dependency decision

`npm audit` currently reports a moderate advisory through `@hono/node-server`, a transitive dependency of the latest `@modelcontextprotocol/sdk` release. Workflow Skill Router uses the SDK only through its stdio MCP transport and does not start the affected HTTP static-file server.

The npm-proposed remediation is a downgrade to an older MCP SDK release rather than an upgrade. That is not a safe compatibility or security improvement, so this distribution keeps the current SDK and monitors upstream remediation. This does not affect the HOL submission threshold, which rejects critical and high findings.

## Runtime validation hardening

The packaged MCP server uses the MCP SDK's Cloudflare Worker-compatible JSON Schema validator. This validator performs no runtime code generation and avoids `eval` and `new Function` in the distributed MCP bundle.
