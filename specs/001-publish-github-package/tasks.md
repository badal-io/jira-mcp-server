---

description: "Task list for GitHub Package Publishing"
---

# Tasks: GitHub Package Publishing

**Input**: Design documents from `/specs/001-publish-github-package/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, quickstart.md

**Tests**: Test tasks are included as this feature is CI/CD related and requires testing of the workflow.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2)
- Include exact file paths in descriptions

## Path Conventions

- **CI/CD**: `.github/workflows/`

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Project initialization and basic structure

- [x] T001 Create the directory structure for the GitHub Action workflow: `.github/workflows`.

---

## Phase 2: User Story 1 - Automate Package Publishing (Priority: P1) 🎯 MVP

**Goal**: Automate the publishing of the npm package to the GitHub Package Registry.

**Independent Test**: Tag a new version in the git repository and verify that the new version of the package appears in the GitHub Package Registry.

### Tests for User Story 1 ⚠️

> **NOTE: Write these tests FIRST, ensure they FAIL before implementation**

- [x] T002 [P] [US1] Create a test workflow at `.github/workflows/test-publish.yml` to test the publishing action on pull requests.
- [x] T003 [US1] Configure the test workflow to run on pull requests.
- [x] T004 [US1] The test workflow should have a job that simulates a dry-run publish.

### Implementation for User Story 1

- [x] T005 [US1] Create the GitHub Actions workflow file at `.github/workflows/publish.yml`.
- [x] T006 [US1] Configure the workflow to trigger on new version tags (e.g., `v*.*.*`).
- [x] T007 [US1] Add a job to the workflow to checkout the code.
- [x] T008 [US1] Add a step to the job to setup Node.js.
- [x] T009 [US1] Add a step to install dependencies (`npm install`).
- [x] T010 [US1] Add a step to build the project (`npm run build`).
- [x] T011 [US1] Add a step to configure npm for the GitHub Package Registry. This step should use the `NODE_AUTH_TOKEN` secret.
- [x] T012 [US1] Add a step to publish the package to the GitHub Package Registry (`npm publish`).

**Checkpoint**: At this point, User Story 1 should be fully functional and testable independently.

---

## Phase 3: User Story 2 - Update README for GitHub Packages (Priority: P2)

**Goal**: Update the README to include instructions for using the package from GitHub Packages.

**Independent Test**: A user can follow the instructions in the `README.md` to successfully install and run the package.

### Implementation for User Story 2

- [x] T013 [US2] Update the `README.md` file to include instructions on how to configure `.npmrc` for the GitHub Package Registry.
- [x] T014 [US2] Update the `README.md` file to include instructions on how to use the package with `npx` from the GitHub Package Registry.
- [x] T015 [US2] Update the `README.md` file to include instructions on how to install and use the package with `npm` from the GitHub Package Registry.

**Checkpoint**: At this point, User Stories 1 AND 2 should both work independently.

---

## Phase N: Polish & Cross-Cutting Concerns

**Purpose**: Improvements that affect multiple user stories

- [x] T016 Verify that the `README.md` is clear and easy to follow.
- [x] T017 Manually run the publishing workflow with a test release to ensure it works end-to-end. (Note: This is a manual step for the user to perform).

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately.
- **User Stories (Phase 2+)**: All depend on Setup phase completion.
  - User stories can then proceed in parallel.

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Setup. No dependencies on other stories.
- **User Story 2 (P2)**: Can start after Setup. It is dependent on User Story 1 being complete to be fully testable.

### Within Each User Story

- Tests (if included) MUST be written and FAIL before implementation.
- For US1, the test workflow should be created before the main workflow.

### Parallel Opportunities

- The test workflow (T002-T004) and the main workflow (T005-T012) can be developed in parallel.
- User Story 2 can be worked on in parallel with User Story 1.

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1.  Complete Phase 1: Setup
2.  Complete Phase 2: User Story 1
3.  **STOP and VALIDATE**: Test User Story 1 independently.
4.  Deploy/demo if ready.

### Incremental Delivery

1.  Complete Setup.
2.  Add User Story 1 → Test independently → Deploy/Demo (MVP!).
3.  Add User Story 2 → Test independently → Deploy/Demo.
4.  Each story adds value without breaking previous stories.