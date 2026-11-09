# Project 2 — Weekly Team Digest Automation

## Overview

The Weekly Team Digest automation retrieves recently updated ClickUp tasks, combines the task information, generates a weekly summary using Gemini 2.5 Flash, saves the digest to Airtable, and posts it to Slack.

The scenario is configured in Make.com and remains inactive until manually activated.

## Workflow Architecture

```text
Weekly Schedule
      ↓
Check Weekly Key
      ↓
Fetch ClickUp Tasks
      ↓
Aggregate Task Updates
      ↓
Generate AI Digest (Gemini 2.5 Flash)
      ↓
Save Digest to Airtable
      ↓
Post Digest to Slack
      ↓
Mark Week as Posted
```

## Modules

| Module | Purpose |
|---|---|
| Data Store | Checks weekly duplicate records |
| ClickUp | Retrieves updated team tasks |
| Text Aggregator | Combines task information |
| Gemini AI | Generates the weekly digest |
| Airtable | Saves the generated digest |
| Slack | Posts the digest to the team channel |
| Data Store | Records the completed weekly digest |
| Break Error Handler | Handles Slack posting failures |

## Digest Format

The AI-generated digest contains four sections:

1. Key Accomplishments
2. Work Completed
3. Current Blockers
4. Next Week's Priorities

The AI prompt instructs Gemini to use only the supplied ClickUp information and avoid inventing tasks, achievements, deadlines, or blockers.

## ClickUp Configuration

- Connection: ClickUp OAuth
- Maximum tasks: 100
- Sort order: Updated date
- Reverse order: Enabled
- Subtasks: Excluded
- Closed tasks: Excluded
- Date filter: Approximately previous seven days
- Task information: Name, status, assignee, due date, and update details

## Gemini AI Configuration

- Module: Simple Text Prompt
- Model: Gemini 2.5 Flash
- Input: Aggregated ClickUp task updates
- Output: Weekly team digest
- AI service: Native Make AI module

The prompt uses the aggregated task information:

```text
{{4.text}}
```

No external Gemini API key is required for the configured native Make AI module.

## Airtable Configuration

- Base: IT Project Tracker
- Table: Weekly Digests
- Operation: Create Record

Field mapping:

| Field | Value |
|---|---|
| Name | Weekly Team Digest |
| Notes | Gemini-generated digest |
| Status | Done |

## Slack Configuration

- Connection: Slack bot
- Channel: all-weekly-team-digest
- Channel type: Public
- Message format:

```text
Weekly Team Digest

{{13.result}}
```

The complete AI-generated digest is posted to the configured Slack channel.

## Deduplication

A Make Data Store prevents duplicate weekly digests.

The weekly key is generated using the Monday date of the current week and the Asia/Karachi timezone.

```text
formatDate(setDay(now; "monday"); "YYYY-MM-DD"; "Asia/Karachi")
```

Processing steps:

1. Check whether the weekly key exists.
2. Continue only if the key does not exist.
3. Retrieve ClickUp tasks.
4. Generate the weekly digest.
5. Save the digest to Airtable.
6. Post the digest to Slack.
7. Record the weekly key.

## Scheduling

- Frequency: Weekly
- Day: Friday
- Time: 5:00 PM
- Timezone: Asia/Karachi
- Scenario status: Inactive

The scenario must be manually activated in Make.com before scheduled processing begins.

## Error Handling

Slack posting uses a Break error handler.

- Maximum retries: 3
- Retry interval: 15 minutes
- Incomplete executions: Stored

This configuration helps handle temporary Slack delivery failures.

## Successful End-to-End Testing

The final Run Once execution completed successfully on November 9, 2026.

| Component | Result |
|---|---|
| Weekly deduplication | Passed |
| ClickUp task retrieval | Passed — 16 task bundles |
| Task aggregation | Passed |
| Gemini 2.5 Flash | Passed |
| Digest generation | Passed |
| Airtable record creation | Passed |
| Slack message posting | Passed |
| Weekly key recording | Passed |
| Scenario validation | Passed |
| Failed operations | None |
| Warnings | None |

The successful test created an Airtable record and posted the generated digest to Slack.

## Required Connections

- ClickUp OAuth
- Airtable OAuth
- Slack bot
- Native Make Gemini AI module

## Activation Instructions

The scenario is intentionally inactive.

To activate it:

1. Open the Weekly Team Digest scenario in Make.com.
2. Confirm the Friday schedule.
3. Confirm Gemini 2.5 Flash is selected.
4. Turn ON the scenario.
5. Monitor executions from the History tab.

## GitHub Submission

Required file:

```text
README.md
```

Optional file:

```text
weekly-team-digest-blueprint.json
```

The blueprint JSON should only be uploaded if exported directly from Make.com.

Do not upload API keys, OAuth tokens, passwords, connection secrets, or private task information.

## Final Status

- Project: Weekly Team Digest Automation
- Platform: Make.com
- AI Model: Gemini 2.5 Flash
- Testing: Successfully completed
- Airtable: Working
- Slack: Working
- Scenario: Inactive
- GitHub documentation: README.md
