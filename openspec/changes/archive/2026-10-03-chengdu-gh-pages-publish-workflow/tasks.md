## 1. Workflow Configuration

- [x] 1.1 Add `repos/chengdu/.github/workflows/site-deploy-gh-pages.yml` with `main` push and manual triggers, a main-ref build guard, fixed concurrency with `cancel-in-progress: false`, bounded timeouts, and read-only default permissions.
- [x] 1.2 Implement the build job using checkout/setup-node v5, Node.js 22, npm lockfile caching, `npm ci`, targeted workflow contract tests, `npm run typecheck`, `PUBLIC_ENABLE_ANALYTICS=true npm run build`, and `node tools/check-static-artifacts.js` in validation-before-upload order.
- [x] 1.3 Implement payload preparation with production-domain `CNAME` and `.nojekyll` in `dist/`; upload only the named branch artifact with hidden-file preservation and missing-file failure.
- [x] 1.4 Implement the `publish` job configuration with a successful-build dependency, isolated `contents: write`, artifact download and required-file checks, and `peaceiris/actions-gh-pages@v4` targeting the branch root with clean snapshot replacement, Jekyll disabled, custom domain, and retained branch history.
- [x] 1.5 Do not create a Pages artifact or deployment job; remove `.github/workflows/release.yml` so Azure site publishing is no longer triggered by GitHub Actions.

## 2. Regression Coverage and CI Integration

- [x] 2.1 Add `repos/chengdu/tools/github-pages-workflow.test.js` using existing Jest and YAML dependencies to assert trigger restrictions, main-ref gating, serialization, bounded timeouts, and job permission boundaries.
- [x] 2.2 Cover validation ordering, production analytics, the named branch artifact, hidden-file preservation, missing-file failure, branch-root publication, and stale-file cleanup configuration.
- [x] 2.3 Cover successful-job dependencies, absence of Pages deployment actions/permissions, and removal of the Azure publishing workflow.
- [x] 2.4 Extend `repos/chengdu/.github/workflows/test.yml` path filters for the new workflow and contract test, including changes or removal of the Azure workflow; retain existing validation steps.

## 3. Documentation

- [x] 3.1 Add a GitHub Pages section to `repos/chengdu/README.md` explaining automatic/manual triggers, `gh-pages` branch-root layout, and that this workflow does not create a Pages deployment.
- [x] 3.2 Document built-in token permissions, branch-protection compatibility, the custom-domain file/DNS boundary, and unsupported project-subpath hosting without documenting a Pages deployment job or environment.
- [x] 3.3 Document removal of Azure publishing automation, unchanged authored Azure configuration and DNS, phase-specific failure outcomes, concurrency limitations, and retry/rollback guidance.

## 4. Local Validation

- [x] 4.1 From `repos/chengdu`, run `npm test -- --runInBand --runTestsByPath tools/github-pages-workflow.test.js` and confirm the new workflow YAML parses and the contract assertions pass.
- [x] 4.2 Run `npm run typecheck`, a production-flag build, and `node tools/check-static-artifacts.js` with the existing toolchain; confirm the static output and production origin remain compatible.
- [x] 4.3 Exercise the workflow's payload preparation locally and inspect root `index.html`, `404.html`, `CNAME`, `.nojekyll`, deep routes, and assets; confirm there is no nested `dist/` wrapper or source/dependency/provider payload and assess artifact size.
- [x] 4.4 Confirm the implementation file inventory matches the design, Azure publishing workflow is removed, authored Azure/application configuration and reference files are unchanged, and documentation distinguishes branch publication from live Pages deployment.
