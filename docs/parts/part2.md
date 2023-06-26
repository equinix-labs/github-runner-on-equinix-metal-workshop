<!-- See https://squidfunk.github.io/mkdocs-material/reference/ -->
# Part 2: Fork a Repo and Deploy a Server

In this steps we'll be getting familiar with GitHub Actions. If it's your first time using GitHub Actions take a few minutes to flip through their [documentation](https://docs.github.com/en/actions).

## Steps

### 1. Fork the `metal-cli` repo to your own GitHub namespace

For this workshop, we'll be making a copy of the Equinix Metal CLI code repository, [`metal-cli`](https://github.com/equinix/metal-cli), to create and test our runners. You could use your own code repository if you already have one. If you do, you can skip this step.

Click on this link "[Fork Metal CLI](https://github.com/equinix/metal-cli/fork)" and fork a copy to your own Github account.

### 2. Disable the actions on your fork of metal-cli

Go to your fork of the `metal-cli` repo and click on **Settings** > **Actions** > **Runners** and disable the actions for now.

![Disable Actions Screenshot](../images/disable-actions.png)

### 3. Deploy a new machine on Equinix Metal

We'll also need a server to run the actions on, in this step we provision a Ubuntu 22.04 server on Equinix Metal, through the CLI.

```sh
metal device create -p $METAL_PROJECT_ID -P c3.medium.x86 -m da -H github-runner-test -O ubuntu_22_04
```

## Discussion

Before proceeding to the next part let's take a few minutes to discuss what we did. Here are some questions to start the discussion.

- What sorts of code repositories would you want to run your own runners on?
- What size machine would be right for your runners?
