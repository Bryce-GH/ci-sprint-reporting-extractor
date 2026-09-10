# ci-sprint-reporting-extractor
Sanitized GitLab CI pipeline that extracts merge request activity via the GitLab REST API, classifies changes by team ownership, identifies Jira references, and exports CSV reporting artifacts for sprint analytics.

# CI-Based Sprint Reporting Extractor

A sanitized GitLab CI / Bash workflow that extracts merge request activity from the GitLab REST API, classifies work by team ownership, identifies Jira-linked items, and exports normalized CSV artifacts for sprint reporting and lightweight engineering analytics.

## Overview

This project demonstrates a lightweight reporting pipeline built in GitLab CI that:

- queries merge request activity across multiple repositories
- filters merged work by a configurable sprint date window
- maps repository IDs to friendly metadata
- infers team ownership from contributor rosters
- extracts Jira-style issue references from MR titles and payload text
- exports structured CSV output as a pipeline artifact

The project is designed as a simple example of CI-based reporting automation using shell tooling rather than a full standalone application.

## Features

- **Configurable sprint window**
  - Set `START_DATE` and `END_DATE` to support final sprint reports or mid-sprint status checks.

- **Multi-repository monitoring**
  - Iterate across a configured list of project IDs and query each repository for merged merge requests.

- **Repository metadata mapping**
  - Convert raw project IDs into human-readable project names, project types, and repository paths.

- **Automated team classification**
  - Assign work to configured teams based on merge request author usernames.

- **Jira ticket extraction**
  - Detect issue references such as `ABC-1234` or `BC-5678` from MR titles and content.

- **CSV artifact generation**
  - Produce a structured export suitable for sprint review prep, lightweight analysis, or downstream reporting.

## Tech Stack

- **GitLab CI**
- **YAML**
- **Bash / POSIX shell**
- **GitLab REST API**
- **curl**
- **sed**
- **grep**
- **CSV artifact generation**

## Example Output

The pipeline generates a CSV with fields such as:

- `Project_ID`
- `Project_Name`
- `Project_Type`
- `MR_ID`
- `Title`
- `Author`
- `Team`
- `Merged_At`
- `Jira_Tickets`
- `Web_URL`

## How It Works

1. Define a sprint date window.
2. Define a set of monitored project IDs.
3. Define team rosters for contributor-to-team mapping.
4. Query the GitLab API for merged merge requests.
5. Filter records by merge timestamp.
6. Extract MR metadata, Jira references, and derived team ownership.
7. Write normalized output to a CSV artifact.

## Example Use Cases

- sprint review preparation
- mid-sprint delivery status checks
- lightweight merge request auditing
- engineering reporting automation
- traceability support between delivery artifacts and backlog references

## Security / Sanitization Notes

This public example is intentionally sanitized:

- usernames replaced with placeholders
- project names generalized
- repository paths generalized
- internal project IDs replaced with placeholder IDs
- organization-specific references removed

Before publishing a real pipeline, review all:
- project IDs
- usernames
- namespaces
- URLs
- token names
- backlog / ticket conventions
- environment-specific details

## Limitations

- Uses shell-based parsing rather than full JSON parsing utilities.
- Assumes API payload format remains compatible with simple text extraction logic.
- Designed for lightweight reporting use cases, not enterprise-grade analytics.
- Team assignment depends on maintained contributor rosters.

## Future Improvements

- Replace text parsing with structured JSON parsing (e.g., `jq`)
- Add pagination support beyond the current request window
- Add unit-testable extraction helpers
- Support richer output formats (JSON, Markdown, HTML)
- Add direct aggregation by Jira key, repository, or team
- Add summary statistics per sprint

## Why This Project Matters

This project demonstrates the practical use of CI pipelines as more than build/deploy tools. It shows how CI can also support:

- reporting automation
- engineering visibility
- workflow traceability
- operational process improvement

## License

MIT License
