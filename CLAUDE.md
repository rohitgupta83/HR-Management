# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Salesforce DX project for HR Management, built with Lightning Web Components (LWC), Apex, and Aura. Targets API version 66.0. Source lives in `force-app/main/default/` and is deployed to Salesforce orgs via the SFDX/SF CLI.

## Commands

```bash
npm install                    # Install dev tooling (eslint, prettier, jest, husky)

npm run lint                   # ESLint on all Aura and LWC JS
npm run prettier               # Format all files in-place
npm run prettier:verify        # Check formatting without modifying

npm run test                   # Run all Jest unit tests (alias for test:unit)
npm run test:unit:watch        # Watch mode for active development
npm run test:unit:coverage     # Coverage report
npm run test:unit:debug        # Jest with debugger enabled
```

## Architecture

### Source Structure (`force-app/main/default/`)

| Directory | Purpose |
|---|---|
| `classes/` | Apex classes — business logic, service/controller layer |
| `triggers/` | Apex triggers — object event handlers |
| `lwc/` | Lightning Web Components — primary UI layer |
| `aura/` | Aura components — legacy, avoid for new work |
| `objects/` | Custom object/field definitions |
| `layouts/` | Page layouts |
| `flexipages/` | Lightning app pages and record pages |
| `permissionsets/` | Access control definitions |
| `staticresources/` | Bundled static assets |

### Development Model

Source-driven: all metadata is tracked locally and synced to orgs via SFDX CLI push/pull. Scratch orgs are created from `config/project-scratch-def.json` (Developer Edition, Lightning Experience enabled). The `.sf/config.json` sets the default target org.

Anonymous Apex snippets live in `scripts/apex/`; SOQL examples in `scripts/soql/`.

## Code Standards

**LWC vs Aura:** Prefer LWC for all new UI work. Aura is supported but legacy.

**ESLint:** Aura JS uses `@salesforce/eslint-plugin-aura` (recommended + locker rules); LWC JS uses `@salesforce/eslint-config-lwc` recommended. Test files (`*.test.js`) have wire adapter linting disabled.

**Prettier:** Formats Apex, LWC/Aura HTML, CSS, JS, JSON, Markdown, and XML. LWC HTML uses the `lwc` parser; Apex uses `prettier-plugin-apex`. `staticresources/**` is excluded.

**Pre-commit hooks (Husky + lint-staged):** On each commit, Prettier formats staged files, ESLint runs on staged LWC/Aura JS, and Jest runs on affected LWC test files (`--bail` — stops at first failure).

**Testing:** Each LWC component should have a `__tests__/*.test.js` sibling. Jest mocks live under `jest-mocks/` and use Node.js globals.

## Salesforce MCP Server

This project has the Salesforce MCP server connected. Prefer MCP tools over raw CLI commands for org operations — they are context-aware and return structured results.

### Org & Metadata

| Tool | Purpose |
|---|---|
| `get_username` | Get the current authenticated username |
| `list_all_orgs` | List all connected orgs |
| `assign_permission_set` | Assign a permission set to a user |
| `deploy_metadata` | Deploy metadata to the target org |
| `retrieve_metadata` | Retrieve metadata from the target org |
| `run_soql_query` | Execute a SOQL query against the org |

### Apex & Testing

| Tool | Purpose |
|---|---|
| `run_apex_test` | Run Apex test classes |
| `run_agent_test` | Run agent/AI tests |
| `scan_apex_class_for_antipatterns` | Static analysis for Apex antipatterns |

### LWC Development

| Tool | Purpose |
|---|---|
| `create_lwc_component_from_prd` | Scaffold a new LWC component from a PRD |
| `guide_lwc_development` | LWC development guidance |
| `guide_lwc_best_practices` | LWC best practices |
| `orchestrate_lwc_component_creation` | End-to-end LWC component creation workflow |
| `orchestrate_lwc_component_optimization` | Optimize an existing LWC component |
| `reference_lwc_compilation_error` | Look up a compilation error explanation |
| `create_lightning_type` | Create a new Lightning type |

### LWC Testing

| Tool | Purpose |
|---|---|
| `create_lwc_jest_tests` | Generate Jest tests for an LWC component |
| `review_lwc_jest_tests` | Review and improve existing Jest tests |
| `run_lwc_accessibility_jest_tests` | Run accessibility-focused Jest tests |
| `orchestrate_lwc_component_testing` | End-to-end LWC test workflow |

### Lightning Data Service (LDS)

| Tool | Purpose |
|---|---|
| `explore_lds_uiapi` | Explore UI API endpoints |
| `guide_lds_development` | LDS development guidance |
| `guide_lds_data_consistency` | Data consistency patterns with LDS |
| `guide_lds_graphql` | GraphQL wire adapter guidance |
| `guide_lds_referential_integrity` | Referential integrity in LDS |
| `orchestrate_lds_data_requirements` | Plan data requirements using LDS |
| `create_lds_graphql_read_query` | Generate a GraphQL read query |
| `create_lds_graphql_mutation_query` | Generate a GraphQL mutation query |
| `fetch_lds_graphql_schema` | Fetch the org's GraphQL schema |
| `test_lds_graphql_query` | Test a GraphQL query against the org |
| `validate_and_optimize` | Validate and optimize LDS queries |

### Code Quality

| Tool | Purpose |
|---|---|
| `run_code_analyzer` | Run Salesforce Code Analyzer (PMD, ESLint, RetireJS) |
| `list_code_analyzer_rules` | List available analyzer rules |
| `describe_code_analyzer_rule` | Get details on a specific rule |
| `query_code_analyzer_results` | Query previously stored analysis results |
| `score_issues` | Score and prioritize code issues |

### Lightning Base Components & Design

| Tool | Purpose |
|---|---|
| `explore_lbc_components` | Browse available Lightning Base Components |
| `guide_lbc_usage` | Usage guidance for base components |
| `guide_component_accessibility` | Accessibility guidance for components |
| `guide_design_general` | General Salesforce design system guidance |
| `guide_figma_to_lwc_conversion` | Convert Figma designs to LWC |

### Aura Migration

| Tool | Purpose |
|---|---|
| `create_aura_blueprint_draft` | Draft a migration plan from Aura to LWC |
| `enhance_aura_blueprint_draft` | Refine an Aura migration blueprint |
| `orchestrate_aura_migration` | Drive end-to-end Aura → LWC migration |
| `verify_aura_migration_completeness` | Verify a completed Aura migration |

### DevOps Center

| Tool | Purpose |
|---|---|
| `list_devops_center_projects` | List DevOps Center projects |
| `list_devops_center_work_items` | List work items in a project |
| `create_devops_center_work_item` | Create a new work item |
| `update_devops_center_work_item_status` | Update a work item's status |
| `checkout_devops_center_work_item` | Check out a work item branch |
| `commit_devops_center_work_item` | Commit changes to a work item |
| `promote_devops_center_work_item` | Promote a work item to the next stage |
| `create_devops_center_pull_request` | Open a pull request for a work item |
| `check_devops_center_commit_status` | Check the status of a commit |
| `detect_devops_center_merge_conflict` | Detect merge conflicts |
| `resolve_devops_center_merge_conflict` | Resolve merge conflicts |
| `resolve_devops_center_deployment_failure` | Diagnose and fix a deployment failure |

### Mobile LWC

| Tool | Purpose |
|---|---|
| `create_mobile_lwc_app_review` | Add app review capability |
| `create_mobile_lwc_barcode_scanner` | Add barcode scanning |
| `create_mobile_lwc_biometrics` | Add biometric authentication |
| `create_mobile_lwc_calendar` | Add calendar integration |
| `create_mobile_lwc_contacts` | Add contacts integration |
| `create_mobile_lwc_document_scanner` | Add document scanning |
| `create_mobile_lwc_geofencing` | Add geofencing |
| `create_mobile_lwc_location` | Add location services |
| `create_mobile_lwc_nfc` | Add NFC support |
| `create_mobile_lwc_payments` | Add payment processing |
| `get_mobile_lwc_offline_analysis` | Analyze offline readiness |
| `get_mobile_lwc_offline_guidance` | Guidance for offline-first mobile components |

## GitHub MCP Server

This project has the GitHub MCP server connected. Use these tools for repository, issue, and pull request operations.

### Repository & Files

| Tool | Purpose |
|---|---|
| `create_repository` | Create a new GitHub repository |
| `fork_repository` | Fork an existing repository |
| `create_branch` | Create a new branch |
| `get_file_contents` | Read a file from a GitHub repository |
| `create_or_update_file` | Create or update a file in a repository |
| `push_files` | Push multiple files to a repository in one commit |
| `list_commits` | List commits on a branch |
| `search_repositories` | Search for repositories |
| `search_code` | Search for code across GitHub |
| `search_users` | Search for GitHub users |

### Issues

| Tool | Purpose |
|---|---|
| `create_issue` | Create a new issue |
| `get_issue` | Get details of an issue |
| `update_issue` | Update an existing issue |
| `list_issues` | List issues in a repository |
| `add_issue_comment` | Add a comment to an issue |
| `search_issues` | Search issues and pull requests |

### Pull Requests

| Tool | Purpose |
|---|---|
| `create_pull_request` | Open a new pull request |
| `get_pull_request` | Get details of a pull request |
| `list_pull_requests` | List pull requests in a repository |
| `get_pull_request_files` | List files changed in a pull request |
| `get_pull_request_status` | Get CI/check status for a pull request |
| `get_pull_request_comments` | Get comments on a pull request |
| `get_pull_request_reviews` | Get reviews on a pull request |
| `create_pull_request_review` | Submit a review on a pull request |
| `update_pull_request_branch` | Update a PR branch with the base branch |
| `merge_pull_request` | Merge a pull request |

## Atlassian Jira MCP Server

This project has the Atlassian (Jira) MCP server connected. Use these tools for project and issue tracking.

### Issues

| Tool | Purpose |
|---|---|
| `jira_create_issue` | Create a new Jira issue |
| `jira_batch_create_issues` | Create multiple issues at once |
| `jira_get_issue` | Get details of a Jira issue |
| `jira_update_issue` | Update an existing issue |
| `jira_delete_issue` | Delete a Jira issue |
| `jira_transition_issue` | Move an issue to a different status |
| `jira_get_transitions` | List available status transitions for an issue |
| `jira_search` | Search issues using JQL |
| `jira_get_project_issues` | Get all issues in a project |
| `jira_link_to_epic` | Link an issue to an epic |
| `jira_create_issue_link` | Create a link between two issues |
| `jira_remove_issue_link` | Remove a link between issues |
| `jira_create_remote_issue_link` | Link a Jira issue to an external URL |
| `jira_get_issue_dates` | Get date fields for an issue |
| `jira_get_issue_sla` | Get SLA information for an issue |
| `jira_get_issue_development_info` | Get linked development info (PRs, commits) |
| `jira_get_issues_development_info` | Get development info for multiple issues |
| `jira_download_attachments` | Download attachments from an issue |
| `jira_get_issue_images` | Get images attached to an issue |

### Comments & Worklogs

| Tool | Purpose |
|---|---|
| `jira_add_comment` | Add a comment to an issue |
| `jira_edit_comment` | Edit an existing comment |
| `jira_add_worklog` | Log time spent on an issue |
| `jira_get_worklog` | Get worklog entries for an issue |
| `jira_add_watcher` | Add a watcher to an issue |
| `jira_remove_watcher` | Remove a watcher from an issue |
| `jira_get_issue_watchers` | List watchers on an issue |

### Projects & Boards

| Tool | Purpose |
|---|---|
| `jira_get_all_projects` | List all Jira projects |
| `jira_get_project_components` | Get components in a project |
| `jira_get_project_versions` | Get versions/releases for a project |
| `jira_batch_create_versions` | Create multiple versions at once |
| `jira_get_agile_boards` | List all agile boards |
| `jira_get_board_issues` | Get issues on a board |
| `jira_search_fields` | Search available Jira fields |
| `jira_get_field_options` | Get options for a select field |
| `jira_get_link_types` | List available issue link types |

### Sprints

| Tool | Purpose |
|---|---|
| `jira_create_sprint` | Create a new sprint |
| `jira_update_sprint` | Update sprint details |
| `jira_get_sprints_from_board` | List sprints on a board |
| `jira_get_sprint_issues` | Get issues in a sprint |
| `jira_add_issues_to_sprint` | Add issues to a sprint |
| `jira_batch_get_changelogs` | Get changelogs for multiple issues |

### Service Desk

| Tool | Purpose |
|---|---|
| `jira_get_service_desk_for_project` | Get service desk info for a project |
| `jira_get_service_desk_queues` | List queues in a service desk |
| `jira_get_queue_issues` | Get issues in a service desk queue |
| `jira_get_issue_proforma_forms` | Get proforma forms on an issue |
| `jira_get_proforma_form_details` | Get details of a proforma form |
| `jira_update_proforma_form_answers` | Update answers on a proforma form |

### Users

| Tool | Purpose |
|---|---|
| `jira_get_user_profile` | Get a Jira user's profile |
