# Prai Action

This GitHub Action generates a pull request message based on the git diff between the base and head branches of a pull request. It can also update the PR description with the generated message. Optionally, it can use a provided template for creating the PR message.

## Usage

Add the following step to your GitHub Actions workflow:

```yaml
- name: PR Diff and Message
  uses: your-github-username/prai@v1.0.0
  with:
    openai_api_key: ${{ secrets.OPENAI_API_KEY }}
    template_pr: ${{ secrets.TEMPLATE_PR }}
    github_token: ${{ secrets.GITHUB_TOKEN }}
```

Replace your-github-username with your GitHub username and adjust the version number as needed.

## Inputs

- openai_api_key (required): Your OpenAI API key, used for generating the PR message. Store this as a secret in your repository settings.
- github_token (required): Your GitHub token for updating the PR description. Store this as a secret in your repository settings.
- template_pr (optional): A template for the PR message. If provided, the action will include this template in the system message sent to the Chat API. Store this as a secret in your repository settings if you want to keep it private.

## Example

Here's a complete example of a GitHub Actions workflow that uses this action:

```yaml
name: PR Diff and Message

on:
  pull_request:

jobs:
  get_diff:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout base branch
        uses: actions/checkout@v2
        with:
          ref: ${{ github.base_ref }}
          path: base

      - name: Checkout head branch
        uses: actions/checkout@v2
        with:
          ref: ${{ github.head_ref }}
          path: head

      - name: PR Diff and Message
        uses: your-github-username/prai@v1.0.0
        with:
          openai_api_key: ${{ secrets.OPENAI_API_KEY }}
          template_pr: ${{ secrets.TEMPLATE_PR }}
          github_token: ${{ secrets.GITHUB_TOKEN }}
```

## License

### MIT License

This `README.md` provides a brief introduction to the action, explains its purpose and usage, and includes an example workflow. Replace `your-github-username` with your actual GitHub username and update the version number as needed.
