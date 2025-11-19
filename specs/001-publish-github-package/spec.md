# Feature Specification: GitHub Package Publishing

**Feature Branch**: `001-publish-github-package`
**Created**: 2025-11-18
**Status**: Draft
**Input**: User description: "Add github actions to publish this project to the local node repository in github. Update readme files for using the mcp server to instead use npx/npm against github's node repository."

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Automate Package Publishing (Priority: P1)

As a project maintainer, I want the npm package to be automatically published to the GitHub Package Registry whenever a new version is tagged in the git repository, so that I don't have to publish it manually.

**Why this priority**: This is the core of the feature and enables the rest of the work.

**Independent Test**: Tag a new version in the git repository and verify that the new version of the package appears in the GitHub Package Registry.

**Acceptance Scenarios**:

1. **Given** a new version tag (e.g., `v1.0.4`) is pushed to the main branch, **When** the GitHub Action workflow runs, **Then** the package `@orengrinker/jira-mcp-server` with version `1.0.4` is published to the GitHub Package Registry.
2. **Given** a commit is pushed to the main branch without a version tag, **When** the GitHub Action workflow runs, **Then** no package is published.

---

### User Story 2 - Update README for GitHub Packages (Priority: P2)

As a user of the `jira-mcp-server`, I want to have clear instructions in the `README.md` on how to use the package from the GitHub Package Registry with `npx` and `npm`, so that I can easily use the package in my projects.

**Why this priority**: This is a user-facing change that is necessary for the feature to be useful.

**Independent Test**: Follow the instructions in the `README.md` to install and run the package using `npx` from the GitHub Package Registry.

**Acceptance Scenarios**:

1. **Given** I follow the instructions in the `README.md` for `npx`, **When** I run the `npx` command, **Then** the `jira-mcp-server` starts successfully.
2. **Given** I follow the instructions in the `README.md` for `npm` installation, **When** I run the `npm install` command, **Then** the package is installed successfully from the GitHub Package Registry.

---

### Edge Cases

- What happens if the package version already exists in the registry?
- What happens if the `JIRA_API_TOKEN` is not set in the GitHub Action?

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: The system MUST provide a GitHub Action workflow that publishes the npm package to the GitHub Package Registry.
- **FR-002**: The workflow MUST be triggered on new version tags (e.g., `vX.Y.Z`).
- **FR-003**: The workflow MUST be configurable with a `JIRA_API_TOKEN` secret.
- **FR-004**: The `README.md` MUST be updated to include instructions for using the package from the GitHub Package Registry with `npx` and `npm`.
- **FR-005**: The `README.md` MUST provide an example of how to configure `.npmrc` to authenticate with the GitHub Package Registry.

## Assumptions

- "local node repository in github" is assumed to be the GitHub Package Registry.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: A new version of the package can be published to the GitHub Package Registry in under 5 minutes from the moment a version tag is pushed.
- **SC-002**: A developer can successfully set up and run the `jira-mcp-server` from the GitHub Package Registry in under 10 minutes by following the `README.md` instructions.
- **SC-003**: The `README.md` instructions for GitHub Packages are clear enough that 95% of users can follow them without seeking additional help.
