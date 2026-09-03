
# Kongponents

[![Kong Kongponents](/docs/public/img/kongponents-logo.jpg?raw=true)][docsUrl]

[![Publish](https://github.com/Kong/kongponents/actions/workflows/publish.yaml/badge.svg)](https://github.com/Kong/kongponents/actions/workflows/publish.yaml)
[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)
[![Netlify Status](https://api.netlify.com/api/v1/badges/426d5e0a-fc41-4c1d-ba80-38417b614394/deploy-status?branch=main)](https://app.netlify.com/sites/kongponents/deploys)

Kongponents is a Vue component library of frequently needed UI elements. They were developed to solve [Kong's](https://konghq.com) application needs, but are generic enough to use in any web application.


## Documentation

[Kongponents Docs][docsUrl] are powered by VitePress and the source can be viewed [here](docs/).

[docsUrl]: https://kongponents.konghq.com

### Test Coverage

```sh
# Run both Vitest projects and print the coverage table
pnpm test:coverage
```

The report lands in `coverage/`; open `coverage/index.html` for the line-by-line view. The `browser` project is narrowed to Chromium for a coverage run, so install it first with `pnpm test:coverage:install`.

The provider is Istanbul rather than V8: the `browser` project runs Firefox and WebKit, whose engines do not expose the V8 coverage profiler that `@vitest/coverage-v8` reads. Istanbul instruments at transform time, so it works across jsdom and every browser engine.

CI runs this as the `Report Test Coverage` job. It fails when coverage drops below the `coverage.thresholds` floors in [`vitest.config.ts`](./vitest.config.ts), and comments on the pull request with the current numbers and their delta against `main`.

The suite currently sits at roughly 84% statements / 77% branches. The thresholds are set a percentage point below that, so ordinary noise passes but a real regression fails the job.

To raise them as the Cypress migration adds specs, read the totals off the coverage summary that `pnpm test:coverage` prints and keep the same headroom. Avoid `--coverage.thresholds.autoUpdate`: it pins each threshold to the exact value just measured, which leaves no room for the one-statement wobble a flaky path can cause and fails the next run.

### Committing Changes

This repo uses [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/).

[Commitizen](https://github.com/commitizen/cz-cli) and [Commitlint](https://github.com/conventional-changelog/commitlint) are used to help build and enforce commit messages.

It is __highly recommended__ to use the following command in order to create your commits:

```sh
pnpm commit
```

This will trigger the Commitizen interactive prompt for building your commit message.

#### Enforcing Commit Format

[Lefthook](https://github.com/evilmartians/lefthook) is used to manage Git Hooks within the repo. A `commit-msg` hook is automatically setup that enforces commit message stands with `commitlint`, see [`lefthook.yaml`](./lefthook.yaml).

#### Agentic reviewer

[View the reference for the `/muthur` agentic reviewer](./agentic-reviewer.md)

### Approvals

- All pull requests require review and approval from authorized team members.
- Automated approvals through workflows are strictly prohibited.
  - There is an exception for automated pull request approvals originating from generated dependency updates that satisfy status checks and other requirements.
- Protected branches require at least one approval from code owners.
- All status checks must pass before a pull request may be merged.
