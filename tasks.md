# Migration Tasks

## Session: mig-20260525-sb2to3
**Project**: /home/bluesman/git/modernizing-java-applications-book/catalog-spring-boot
**Type**: framework
**Migration**: Spring Boot 2.1.6 → Spring Boot 3.2.x
**Mode**: autonomous
**Started**: 2026-05-25
**Branch**: migration/spring-boot-3

## Preparation Tasks

### TASK-001: Analyze Codebase
- **Status**: completed
- **Assignee**: project-tracker-agent
- **Outcome**: analysis-report.json
- **Started**: 2026-05-25
- **Completed**: 2026-05-25

### TASK-002: Create Migration Plan
- **Status**: completed
- **Assignee**: project-tracker-agent
- **Blocked by**: TASK-001
- **Outcome**: migration-plan.json
- **Started**: 2026-05-25
- **Completed**: 2026-05-25

### TASK-003: Generate Backlog
- **Status**: completed
- **Assignee**: project-tracker-agent
- **Blocked by**: TASK-002
- **Outcome**: 5 GitHub issues created, tasks.md updated
- **Started**: 2026-05-25
- **Completed**: 2026-05-25

## User Stories

### STORY-001: Update pom.xml to Spring Boot 3.2.5
- **Status**: in-progress
- **GitHub Issue**: https://github.com/modernizing-java-applications-book/catalog-spring-boot/issues/3
- **Priority**: critical
- **Rules**: RULE-001, RULE-003, RULE-004, RULE-005, RULE-007, RULE-008
- **Files**: pom.xml
- **Started**: -
- **Completed**: -

### STORY-002: Migrate javax.persistence to jakarta.persistence
- **Status**: pending
- **GitHub Issue**: https://github.com/modernizing-java-applications-book/catalog-spring-boot/issues/4
- **Priority**: critical
- **Rules**: RULE-002
- **Files**: Product.java
- **Started**: -
- **Completed**: -

### STORY-003: Update application configuration for Spring Boot 3
- **Status**: pending
- **GitHub Issue**: https://github.com/modernizing-java-applications-book/catalog-spring-boot/issues/5
- **Priority**: medium
- **Rules**: RULE-006, RULE-009
- **Files**: application.properties
- **Started**: -
- **Completed**: -

### STORY-004: Refactor CatalogController to constructor injection
- **Status**: pending
- **GitHub Issue**: https://github.com/modernizing-java-applications-book/catalog-spring-boot/issues/6
- **Priority**: low
- **Rules**: RULE-010
- **Files**: CatalogController.java
- **Started**: -
- **Completed**: -

### STORY-005: Build verification and smoke test
- **Status**: pending
- **GitHub Issue**: https://github.com/modernizing-java-applications-book/catalog-spring-boot/issues/7
- **Priority**: critical
- **Rules**: -
- **Files**: -
- **Started**: -
- **Completed**: -
