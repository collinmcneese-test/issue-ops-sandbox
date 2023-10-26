# IssueOps Sandbox

## References

- [Docs: Events that trigger workflows](https://docs.github.com/en/enterprise-cloud@latest/actions/using-workflows/events-that-trigger-workflows)
- [Docs: Webhook events and payloads](https://docs.github.com/en/enterprise-cloud@latest/webhooks/webhook-events-and-payloads#issues)
- [Docs: Issue Templates & Forms](https://docs.github.com/en/enterprise-cloud@latest/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository)
- [Docs: Octokit](https://docs.github.com/en/enterprise-cloud@latest/rest/overview/libraries?apiVersion=2022-11-28)
- [Docs: Using conditions to control job execution](https://docs.github.com/en/enterprise-cloud@latest/actions/using-jobs/using-conditions-to-control-job-execution)
- [octokit/rest.js](https://octokit.github.io/rest.js/v20)
- [actions/github-script](https://github.com/marketplace/actions/github-script)
- [Using GitHub CLI in Workflows](https://docs.github.com/en/enterprise-cloud@latest/actions/using-workflows/using-github-cli-in-workflows)

```yaml
name: My Workflow

# Full listing of events: https://docs.github.com/en/enterprise-cloud@latest/actions/using-workflows/events-that-trigger-workflows
on:
  issues:
    types:
      - opened
      - edited
  issue_comment:
    types:
      - created

jobs:
  hello-issue:
    runs-on: ubuntu-latest
    if: ${{ github.event_name == 'issues' && contains(github.event.issue.body, 'hello') }}
    steps:
      - uses: actions/checkout@v4
      - name: My Issue Step
        run: echo "This is an example step that only runs when an issue is opened or edited and contains the word 'hello' in the body."

  hello-comment:
    runs-on: ubuntu-latest
    if: ${{ github.event_name == 'issue_comment' }}
    steps:
      - uses: actions/checkout@v4
      - name: My Comment Step
        run: echo "This is an example step that only runs when an issue comment is created."
```
