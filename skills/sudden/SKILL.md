---
name: sudden
description: Use when the user wants Sudden integrated, configured, validated, or troubleshot in their codebase. This skill equips the agent to read the relevant Sudden docs, choose the right integration path for the codebase, implement it directly, and verify it.
---

# Sudden

Use this skill to implement Sudden in the user's codebase.

## Workflow

1. Inspect the codebase before changing anything:
   - What framework or runtime does the app use?
   - Where is the app entry point or top-level layout?
   - Where does video playback happen?
   - Does the app already use a service worker?
   - Where should Sudden configuration live in this project?
2. Identify any Sudden-specific values or onboarding inputs that the integration will likely need.
   - Check whether they already exist in config, env, or project secrets.
   - If they are missing, tell the user early which values are needed or likely needed.
3. Choose the relevant documentation path:
   - broad setup
   - framework-specific integration
   - service worker integration
   - configuration and onboarding requirements
   - validation or troubleshooting
4. Read the relevant Sudden documentation pages before editing code.
5. Implement the integration directly:
   - Read the exact documentation pages needed before editing code.
   - Use the current package names, API names, config fields, and integration steps from the docs.
   - Reuse the project's existing config and env conventions instead of inventing a new pattern.
   - If a required value is still unavailable, wire the integration with a clear placeholder or env hook and call that out to the user.
6. Verify the result:
   - The implementation follows the documented integration path consistently.
   - Build, lint, and tests still pass when available.
   - If browser testing is available, use the documented smoke-test or validation steps.

## Documentation Map

Read the relevant pages first, then derive the exact implementation details from those pages.

### Primary integration pages

| Task | Primary doc | Also read |
| --- | --- | --- |
| First integration or broad setup | https://docs.sudden.network/getting-started/ | Framework-specific page; Service worker |
| JavaScript or TypeScript integration | https://docs.sudden.network/javascript-client/ | Service worker |
| React integration | https://docs.sudden.network/react-client/ | Service worker |
| Service worker integration | https://docs.sudden.network/service-worker/ | Getting started |
| Configuration and onboarding values | https://docs.sudden.network/client-id/ | Getting started |

### Validation and support pages

| Task | Doc | Use when |
| --- | --- | --- |
| Browser and capability limits | https://docs.sudden.network/compatibility/ | The agent needs compatibility boundaries or environment checks |
| Smoke test and offload validation | https://docs.sudden.network/seeing-results/ | The agent needs rollout checks or wants to verify Sudden is active |
| Integration hygiene | https://docs.sudden.network/best-practices/ | The agent wants rollout or integration guidance |
| Troubleshooting | https://docs.sudden.network/troubleshooting/ | The agent is debugging low offload, CSP issues, or integration problems |
| Release notes | https://docs.sudden.network/release-notes/ | The agent needs recent changes |

## Guardrails

- Treat the documentation as the source of truth for package names, function names, props, config fields, and supported capabilities.
- Do not invent onboarding values or deployment-specific credentials.
- If a required Sudden value is missing, tell the user exactly what is missing, then integrate as far as possible with a clear placeholder or env hook if the value is still unavailable.
- Keep the user's player and delivery path unchanged outside the Sudden integration itself.
- Prefer the smallest viable code change near the app root or entry point.

## External Prerequisites

- Some Sudden integrations depend on onboarding values or configuration that may not already exist in the codebase.

If those values are not available, the agent should still wire the integration structure and clearly mark the exact missing dependency.
