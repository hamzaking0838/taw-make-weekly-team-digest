# Weekly Team Digest

## Project Overview
Weekly Team Digest is an AI-powered automation that collects weekly team updates, summarizes important information using AI, and prepares a single organized digest for remote teams.

## Problem
Remote teams use different tools to share their daily work updates. It becomes difficult to track completed tasks, pending work, and important updates in one place.

## Target Users
- Remote teams
- Team leaders and managers
- Startups
- Project management teams

## Features
- Collect team updates from ClickUp or Asana.
- Integrate with Google Workspace.
- Store and organize updates using Airtable.
- Generate AI-powered summaries using OpenAI.
- Prepare weekly team digest.
- Send the digest to Slack.
- Handle empty responses and API errors.
- Support retry handling for failed automation steps.

## Technology Stack
- Make.com
- Google Workspace
- Airtable
- OpenAI
- Slack

## Architecture

Google Workspace / ClickUp / Asana
↓
Make.com Automation
↓
Airtable (Store Updates)
↓
OpenAI (Generate Summary)
↓
Slack (Publish Weekly Digest)

## Setup Instructions
1. Create a Make.com account.
2. Import the exported scenario JSON.
3. Connect Google Workspace.
4. Connect Airtable.
5. Configure OpenAI API credentials.
6. Connect Slack.
7. Configure the weekly schedule.
8. Run a test using sample team updates.

## Environment Variables

See `.env.example` for the required configuration variables.

Never upload real API keys or passwords to GitHub.

## Project Files
- `README.md` – Project documentation.
- `workflow.json` – Exported Make.com automation.
- `.env.example` – Example configuration.
- `TESTING.md` – Testing checklist.
- `screenshots/` – Project screenshots.

## Demo
Loom Demo: Coming Soon

## Testing
Testing results will be documented in `TESTING.md` after verifying the automation.

## Security
- Use dummy/sample data only.
- Keep API keys and credentials private.
- Do not upload personal or client information.

