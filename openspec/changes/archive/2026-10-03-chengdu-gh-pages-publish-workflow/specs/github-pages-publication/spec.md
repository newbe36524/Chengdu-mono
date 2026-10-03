## Purpose

Provide reproducible and validated publication of Chengdu's static website to the `gh-pages` branch. The workflow does not create a GitHub Pages deployment, and the Azure publishing workflow is removed.

## ADDED Requirements

### Requirement: Publish only authorized production source
The workflow SHALL automatically run for pushes to `main` and support manual dispatch on `main`. Pull requests, pushes to other branches, and manual dispatches on other refs MUST NOT publish production output. Publication runs SHALL be serialized without canceling an active run.

#### Scenario: Main branch changes
- **WHEN** a commit is pushed to `main`
- **THEN** a publication run builds that source revision and can publish it after validation

#### Scenario: Manual production publication
- **WHEN** an operator manually dispatches the workflow on `main`
- **THEN** the selected production revision is built and validated through the same publication path

#### Scenario: Non-production source
- **WHEN** the workflow is dispatched on another branch or the source change is a pull request
- **THEN** it does not update `gh-pages`

#### Scenario: Concurrent requests
- **WHEN** another publication request arrives while a run is active
- **THEN** it does not cancel the active run or publish concurrently with it

### Requirement: Validate before publication
The workflow SHALL build with the repository's supported Node.js 22 runtime and locked dependencies. It SHALL type-check the source, build the static output, and verify the generated artifact against the existing static-site contract before making that output available for publication. Production builds SHALL explicitly enable the existing production analytics flag.

#### Scenario: Valid source
- **WHEN** dependency installation, type checking, build, and static verification succeed
- **THEN** the workflow makes the complete validated site available to branch publication without rebuilding it

#### Scenario: Invalid source or artifact
- **WHEN** dependency installation, type checking, build, or static verification fails
- **THEN** the workflow fails and `gh-pages` is not updated

### Requirement: Publish a complete branch-root snapshot
The workflow SHALL publish the contents of the validated static output at the `gh-pages` branch root. The snapshot MUST include the home page, deep routes, assets, branded `404.html`, production-domain `CNAME`, and `.nojekyll`, and MUST remove stale generated files. It MUST NOT wrap the website in a `dist/` directory or include source code, dependency directories, or reference-provider configuration.

#### Scenario: Initial publication
- **WHEN** validation succeeds and `gh-pages` does not yet exist
- **THEN** publication creates the branch with `index.html` at its root and all required static resources

#### Scenario: Replacing a previous snapshot
- **WHEN** a later validated build removes a formerly published generated file
- **THEN** the next branch snapshot omits that stale file while preserving the new build's complete output

### Requirement: Publish only the branch snapshot
The workflow SHALL publish the validated site to the root of `gh-pages`. It MUST NOT upload a GitHub Pages artifact, use Pages or identity-token permissions, or create a GitHub Pages deployment. Configuring GitHub Pages to consume the branch, if desired, is outside this workflow.

#### Scenario: Branch snapshot is published
- **WHEN** the build and branch publication succeed
- **THEN** the validated site exists at the `gh-pages` branch root and the workflow completes without creating a Pages deployment

#### Scenario: Branch publication fails
- **WHEN** publication to `gh-pages` fails
- **THEN** the workflow fails and does not claim a Pages deployment

### Requirement: Restrict credentials and remove Azure publishing automation
Build validation SHALL have read-only repository access. Repository-write permission SHALL be limited to branch publication. The workflow SHALL use the built-in GitHub token without requiring a personal access token. The Azure Static Web Apps publishing workflow MUST be removed; authored Azure configuration, application routing, production origin, and reference repository files MUST remain unchanged.

#### Scenario: Inspect permission boundaries
- **WHEN** the workflow's job permissions are evaluated
- **THEN** build validation cannot write repository contents, and only the branch publication job can update `gh-pages`

#### Scenario: Existing hosting remains available
- **WHEN** the new workflow is added
- **THEN** no Azure publishing GitHub Action remains, authored Azure configuration and production URLs remain unchanged, and no DNS changes are made

### Requirement: Document publication prerequisites and recovery
Repository documentation SHALL describe automatic and manual triggers, the branch-root layout, token permissions, the custom-domain file and DNS boundary, removal of the Azure publishing workflow, and failure/retry behavior. It MUST state that publishing `gh-pages` does not itself create or guarantee a live GitHub Pages deployment.

#### Scenario: Configure Pages without changing application routes
- **WHEN** an operator follows the documentation
- **THEN** the operator can identify the branch publication behavior, configure the existing production custom domain separately if needed, and understand that an unconfigured project-subpath URL is not supported

#### Scenario: Recover from a failed run
- **WHEN** a publication run fails
- **THEN** the documentation explains how to identify the failed phase and retry without claiming that a Pages deployment occurred
