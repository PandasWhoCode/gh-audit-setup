# CI/CD and Build System best practices

## Authentication

-  When possible, prefer short-lived access tokens for all workflows. The GitHub workflow Personal Access Token (PAT) is the best approach whenever possible. 
If we need to use something like `teleport`, it's the exception to the rule.

- When possible, prefer to use `teleport` or another short-lived access token for authentication, rather than raw SSH public/private key pairs. Ensure
`teleport` calls are into a Kube cluster rather than individual machines.

## Build Hosting Location

- Where possible, do not depend on external resources outside of GitHub (GCP, for example). Most workflows need runner resources only.

- Use configured, shared servers for any code that merges into the mainline. The `main` version of workflows should not contain any calls to private, 
individual servers. Do not call out to static resources.

## Other Areas for Improvements
- General tooling
    - Qualified org name (@hiero-ledger/<package>, @hashgraph/<package>, etc.)
    - Exact version number binding or SHA number for software packages
    - Follow [OWASP](https://owasp.org/www-project-secure-coding-practices-quick-reference-guide/) and [OWASP Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/CI_CD_Security_Cheat_Sheet.html)
    whenever possible.
    - Use action installs whenever possible instead of manually installing packages. These pre-built actions will use caches, be better supported, etc.
- Gradle
    - Use standard modules for Gradle
    - Jendrik is the best POC for this (using modules and setting up a new project)
- NPM
    - Never use `npm install`, instead use `npm ci` to verify the right package is downloaded and not auto-updated
- cmake
- cargo
- Others
    - Rule Justifications - these should be captured in our HelpDesk. ACTION: Request a new ticket type for Exception request form from Isaac.