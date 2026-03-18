<!--
SYNC IMPACT REPORT
==================
Version change: 1.3.0 → 1.4.0 (separated Atomic Commits and AI Attribution into distinct principles)
Added principles:
  - VI. AI Attribution
Modified principles:
  - V. Atomic Commits (removed attribution requirement, now in Principle VI)
Added sections: None
Removed sections: None
Templates requiring updates: None (internal governance change)
Follow-up TODOs: None
-->

# Photo Album Organizer Constitution

## Table of Contents

1. [Core Principles](#core-principles)
   - [I. Code Quality Excellence](#i-code-quality-excellence)
   - [II. Testing Standards (NON-NEGOTIABLE)](#ii-testing-standards-non-negotiable)
   - [III. User Experience Consistency](#iii-user-experience-consistency)
   - [IV. Performance Requirements](#iv-performance-requirements)
   - [V. Atomic Commits](#v-atomic-commits)
   - [VI. AI Attribution](#vi-ai-attribution)
2. [Development Workflow](#development-workflow)
3. [Governance](#governance)
4. [Changelog](#changelog)

## Core Principles

### I. Code Quality Excellence

All code MUST adhere to high-quality standards that ensure maintainability, readability, and long-term sustainability.

**Non-Negotiable Rules**:
- All public functions and classes MUST have clear docstrings explaining purpose, parameters, and return values.
- Code MUST follow established style guides for the chosen language (e.g., PEP 8 for Python).
- Functions MUST be small, focused, and have a single responsibility (max 30 lines recommended).
- Complex logic MUST be accompanied by inline comments explaining the "why", not the "what".
- All code MUST pass linting and static analysis tools before merge.
- Magic numbers and strings MUST be extracted to named constants.
- Error handling MUST be explicit; silent failures are prohibited.

**Rationale**: Photo album organizers are long-term projects where users accumulate memories over years. Code quality ensures the system remains maintainable as features grow and requirements evolve.

### II. Testing Standards (NON-NEGOTIABLE)

All features MUST be developed using Test-Driven Development (TDD) methodology. This principle is non-negotiable and supersedes speed of delivery.

**Red-Green-Refactor Cycle**:
1. **Red**: Write a failing test first that defines the desired behavior.
2. **Green**: Implement the minimum code necessary to make the test pass.
3. **Refactor**: Improve code structure while keeping all tests green.

**Testing Requirements**:
- Unit tests MUST cover all business logic, edge cases, and error paths.
- Integration tests MUST verify interactions between components and external systems.
- Contract tests MUST validate API boundaries and data schemas.
- Test coverage MUST exceed 80% for all new code; critical paths require 100%.
- Tests MUST be deterministic, isolated, and fast (<100ms per unit test).
- Test names MUST describe the scenario being tested (e.g., `test_upload_photo_when_storage_full_raises_error`).

**Rationale**: TDD ensures features are built to specification, prevents regressions during refactoring, and provides living documentation of system behavior. For a photo organizer handling irreplaceable user data, tests are a safety net against data loss.

### III. User Experience Consistency

All user-facing features MUST provide a consistent, intuitive, and accessible experience across the entire application.

**Design Principles**:
- **Consistency**: Similar actions MUST behave similarly across all screens and workflows.
- **Feedback**: Users MUST receive immediate, clear feedback for every action (success, error, progress).
- **Forgiveness**: Destructive actions MUST require confirmation; users MUST be able to undo operations where feasible.
- **Accessibility**: UI MUST support keyboard navigation, screen readers, and meet WCAG 2.1 AA contrast requirements.
- **Progressive Disclosure**: Advanced options MUST be hidden by default; common actions MUST be prominent.
- **Error Messages**: MUST be user-friendly, actionable, and never expose internal implementation details.

**Interaction Standards**:
- Loading states MUST display within 100ms for async operations.
- Photo operations (upload, organize, tag) MUST show progress indicators for batches >10 items.
- Search and filter results MUST update within 500ms or show loading state.
- Navigation MUST be consistent: back buttons return to previous context, breadcrumbs show hierarchy.

**Rationale**: Users interact with photo albums emotionally—they're organizing memories, not just files. Consistent, forgiving UX reduces anxiety and builds trust in the system.

### IV. Performance Requirements

All features MUST meet defined performance budgets to ensure responsive, scalable photo management.

**Performance Budgets**:
- **Photo Upload**: Single photo (<10MB) MUST complete upload within 3 seconds on 10Mbps connection.
- **Gallery Load**: Thumbnail grid (100 photos) MUST render within 2 seconds.
- **Search**: Text search across 10,000 photos MUST return results within 500ms (p95).
- **Memory Usage**: Application MUST stay under 500MB RAM for typical usage (<1000 photos in view).
- **API Latency**: All API endpoints MUST respond within 200ms (p95) under normal load.
- **Batch Operations**: Processing 100 photos (resize, tag, organize) MUST complete within 60 seconds.

**Scalability Requirements**:
- System MUST support libraries up to 100,000 photos without degradation.
- Database queries MUST be indexed; full table scans prohibited on production data.
- Image processing MUST use streaming for large files (>50MB); no loading entire file into memory.
- Caching MUST be implemented for frequently accessed metadata (tags, albums, recent photos).

**Rationale**: Photo libraries grow over time. Performance budgets ensure the system remains responsive as users accumulate thousands of memories, preventing frustration and abandonment.

### V. Atomic Commits

All work MUST be committed in small, atomic increments to enable easy review and safe rollbacks.

**Atomic Commit Rules**:
- Each commit MUST represent a single, logical change (e.g., one feature, one fix, one refactor).
- Commits MUST be small enough to be reviewed in under 10 minutes.
- Related changes MUST be grouped together; unrelated changes MUST be separate commits.
- Work-in-progress commits MUST be squashed before merge unless they represent meaningful milestones.

**Commit Message Format**:
- All commits MUST follow conventional commit format: `<type>: <description>`
- Types MUST be one of: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`
- Detailed description MUST be provided as a second `-m` flag when change is non-trivial.

**Rationale**: Atomic commits enable easy code review, simplified debugging, and safe rollbacks. Small, focused changes reduce cognitive load and improve code quality.

### VI. AI Attribution

All AI-assisted work MUST include proper attribution to acknowledge AI contributions.

**Attribution Requirement**:
- All commits generated with AI assistance MUST include the attribution line:
  ```
  Co-Authored-By: Qwen-Coder <224605497+qwencoder@users.noreply.github.com>
  ```
- Attribution MUST be added as a separate line at the end of the commit message body.
- This attribution is non-negotiable and applies to all AI-assisted work.

**Example Commit**:
```bash
git commit -m "refactor: migrate command config files from TOML to Markdown" \
           -m "Convert all .qwen/commands/*.toml files to .md format for improved readability" \
           -m "Co-Authored-By: Qwen-Coder <224605497+qwencoder@users.noreply.github.com>"
```

**Rationale**: AI attribution ensures proper credit and transparency about the origin of code contributions, fostering trust and acknowledging the collaborative nature of AI-assisted development.

## Development Workflow

**Code Review Requirements**:
- All changes MUST be reviewed by at least one team member before merge.
- Reviewers MUST verify constitution compliance (principles I-IV) as part of review.
- PR descriptions MUST reference related user stories and test coverage.

**Definition of Done**:
- All tests pass (unit, integration, contract).
- Code coverage meets 80% threshold.
- Linting and static analysis pass with zero errors.
- Performance benchmarks meet budgets (for affected features).
- Documentation updated (API docs, user guides if applicable).
- Constitution compliance verified.

## Governance

**Amendment Process**:
- Proposals MUST be submitted as a PR to this constitution file.
- Changes require unanimous team approval.
- Breaking changes (principle removal, redefinition) require MAJOR version bump.
- New principles or material expansions require MINOR version bump.
- Clarifications and wording improvements require PATCH version bump.

**Versioning Policy**:
- This constitution follows semantic versioning: MAJOR.MINOR.PATCH.
- Version history MUST be tracked in git commit history.
- Ratification date marks initial adoption; last amended date updates on each change.

**Compliance Review**:
- All PRs MUST be checked against constitution principles before merge.
- Quarterly reviews SHOULD assess whether principles remain relevant and actionable.
- Violations MUST be documented with justification in PR comments.

## Changelog

**Version 1.4.0** (2026-03-18)
- Added: AI Attribution principle (Principle VI)
- Modified: Atomic Commits principle (Principle V) - separated attribution requirement into Principle VI

**Version 1.3.0** (2026-03-18)
- Added: Atomic Commits with Attribution principle (Principle V)

**Version 1.2.0** (2026-03-18)
- Added: Table of Contents section for improved navigation

**Version 1.1.0** (2026-03-18)
- Added: Changelog section for tracking constitution evolution

**Version 1.0.0** (2026-03-18)
- Added: Core Principles (Code Quality, Testing Standards, UX Consistency, Performance)
- Added: Development Workflow section
- Added: Governance section

**Versioning Policy**:
- MAJOR.MINOR.PATCH format (e.g., 1.2.0)
- MAJOR: Backward-incompatible changes (principle removal/redefinition)
- MINOR: New principles, sections, or material expansions
- PATCH: Clarifications, wording fixes, non-semantic refinements

**Version**: 1.4.0 | **Ratified**: 2026-03-18 | **Last Amended**: 2026-03-18
