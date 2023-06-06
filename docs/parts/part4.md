<!-- See https://squidfunk.github.io/mkdocs-material/reference/ -->
# Part 3: Executing a Github Action on your self-hosted runner

## Steps

### 1. Let's go back to our fork of metal-cli

For me it's [https://github.com/cprivitere/metal-cli](https://github.com/cprivitere/metal-cli)

### 2. Click on 'Settings' -> 'Actions' -> 'Runners' again in the repo and you should see your new self-hosted runner

![Metal CLI Settings Runners Listing Screenshot](../images/metal-cli-settings-runners-listing.png)

### 3. Now we go edit our github actions workflow to use a self-hosted runner

![Metal CLI Github Actions Workflow Edit Screenshot](../images/metal-cli-github-actions-workflow-edit.png)

### 4. Edit metal-cli/.github/workflows/test.yml and replace the line:

  ```yaml
      runs-on: ubuntu-latest
  ```

  with

  ```yaml
      runs-on: self-hosted
  ```

- Also add

  ```yaml
    workflow_dispatch:
  ```

  underneath the `on:` line

Your test.yml file should now look like:

  ```yaml
  name: Go Tests
  on:
    pull_request:
    workflow_dispatch:
  jobs:
    test:
      runs-on: self-hosted
      timeout-minutes: 10
      steps:
      - name: Set up Go
        uses: actions/setup-go@v4.0.0
        with:
          go-version: '1.19'
      - name: Check out code into the Go module directory
        uses: actions/checkout@v3
      - name: Get dependencies
        run: go mod download
      - name: Build
        run: go build -v ./...
      - name: TF tests
        run: go test -v -cover -parallel 4 ./...
  ```

- Commit your changes

### 5. Go back to 'Settings' -> 'Actions' -> 'General' and Allow all actions and reusable workflows

![Metal CLI Settings Actions Allow All Screenshot](../images/metal-cli-settings-actions-allow-all.png)

### 6. Now click on Actions and click on 'Go Tests' on the left side

![Metal CLI Actions Go Tests Screenshot](../images/metal-cli-actions-go-tests.png)

### 7. Click the 'Run workflow' drop down on the right side and run it for the main branch

![Metal CLI Actions Go Tests Run Workflow Screenshot](../images/metal-cli-actions-go-tests-run-workflow.png)

### 8. Now watch the output on your github runner and the output inside github

- `Running job: test` should appear

## Discussion

Before proceeding to the next part let's take a few minutes to discuss what we did. Here are some questions to start the discussion.

- Can I use a mix of self-hosted and github-hosted runners within a workflow?
- What sort of logging do I get from my self-hosted runner?
- Can I see the results of my self-hosted runner on Github?
