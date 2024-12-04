# Patched PRReview Action

This GitHub Action uses [patchwork-cli](https://docs.patched.codes/patchwork/quickstart) to automatically summarize and comment on PRs in your repository.

## Features

- Automatically reviews and summarizes pull requests
- Generates improvement suggestions for the PR (optional)
- Configurable summary length (long, short, none)
- Supports various LLM providers (OpenAI, local models, or custom endpoints)
- Automatic PR detection in GitHub Actions workflows

## Usage

```yaml
name: PR Review
on:
  pull_request:
    types: [opened]

jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: patched-codes/PRReview@0.1.0
        with:
          patched_api_key: ${{ secrets.PATCHED_API_KEY }}
          # PR URL is automatically detected in pull_request events
```

## Inputs

### Required

One of the following must be provided:

- `patched_api_key`: Patched API key for the LLM ([Get an API key](https://app.patched.codes/))
- `openai_api_key`: OpenAI API key for the LLM ([Get an API key](https://platform.openai.com/account/api-keys))

### Optional

- `pr_url`: URL of the pull request to review (default: automatically detected in pull_request events)
- `github_token`: GitHub token for creating PR comments (default: [Automatically set by GitHub](https://docs.github.com/en/actions/security-for-github-actions/security-guides/automatic-token-authentication))
- `model`: LLM model to use
- `client_base_url`: Base URL for the LLM API
- `diff_suggestion`: Whether to generate suggestions to improve the PR
- `diff_summary`: Length of the summary (long, short, none)
- `model_temperature`: Temperature parameter for the LLM
- `model_top_p`: Top-p parameter for the LLM
- `model_max_tokens`: Maximum tokens for the LLM response

## Examples

### Basic Usage

```yaml
- uses: patched-codes/PRReview@0.1.0
  with:
    patched_api_key: ${{ secrets.PATCHED_API_KEY }}
```

### Manual PR Review

```yaml
- uses: patched-codes/PRReview@0.1.0
  with:
    patched_api_key: ${{ secrets.PATCHED_API_KEY }}
    pr_url: "https://github.com/user/repo/pull/123"
    diff_suggestion: true
    diff_summary: "long"
```

### Using Custom Model

```yaml
- uses: patched-codes/PRReview@0.1.0
  with:
    openai_api_key: ${{ secrets.OPENAI_API_KEY }}
    model: "gpt-4"
    model_temperature: 0.2
    model_top_p: 0.95
    model_max_tokens: 2000
```

## Example Comments

Here are some example comments generated with the PRReview action:

- https://github.com/patched-codes/patchwork/pull/59#issuecomment-2092735385
- https://github.com/patched-codes/patchwork/pull/56#issuecomment-2092584306

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
