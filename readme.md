# Santize Branch Name

A Github action that determines the branch name, then sanitizes it of any forward slashes.

## Description

Determination of the branch name is important when an action can run on both a PR and post-merge master/main. As the github context doesn't fully support providing the branch name directly via a single reference.

Sanitizing the branch name of forward slashes helps ensure any subsequent actions that want the branch name, such as an artifact name, don't break due to the special character. Forward slashes break inside of actions/artifact-upload@v1, but are supported by git as a valid branch name.

Takes no input, and provides two outputs. The actual branch name, and the sanitized version.

## Usage

```yml
jobs:

  foo:
    name: "foo - do some things"

    steps:
      - name: "Determine Branch"
        id: branches
        uses: transferwise/sanitize-branch-name@v1

      - name: "Echo branch name"
        shell: bash
        run: 'echo "branch name is: ${{ steps.branches.outputs.branch-name }}"'

      - name: "Echo sanitized branch name"
        shell: bash
        run: 'echo "branch name is: ${{ steps.branches.outputs.sanitized-branch-name }}"'        


```
