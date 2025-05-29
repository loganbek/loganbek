# Auto-Issue on Workflow Failure

This repository includes an automated system that creates GitHub issues when workflows fail.

## How It Works

The `auto-issue-on-failure.yml` workflow is triggered whenever any of the monitored workflows complete with a failure status. When this happens:

1. **Automatic Detection**: The workflow listens for `workflow_run` events with `completed` status
2. **Failure Check**: Only creates issues when the workflow conclusion is `failure`
3. **Duplicate Prevention**: Checks for existing open issues to avoid duplicates
4. **Issue Creation**: Creates a detailed issue with diagnostic information
5. **Assignment**: Automatically assigns the issue to @copilot for automated handling

## Monitored Workflows

The following workflows are monitored for failures:
- Metrics (main.yml)
- CodeQL (codeql.yml) 
- Deploy Jekyll with GitHub Pages dependencies preinstalled (jekyll-gh-pages.yml)
- Test Workflow Failure (test-failure.yml) - for testing purposes

## Issue Details

Each auto-created issue includes:
- Workflow name and run details
- Branch and commit information
- Direct link to workflow logs
- Checklist for resolution steps
- Automatic labels: `automated-issue`, `workflow-failure`, `bug`

## Testing

A test workflow (`test-failure.yml`) is included that can be manually triggered to test the auto-issue creation functionality. Use the workflow dispatch feature in GitHub Actions to trigger it with the "should_fail" parameter set to true.

## Configuration

To add monitoring for additional workflows, update the `workflows` list in the `auto-issue-on-failure.yml` file's `workflow_run` trigger.

## Permissions

The workflow requires the following permissions:
- `issues: write` - to create issues
- `contents: read` - to checkout the repository