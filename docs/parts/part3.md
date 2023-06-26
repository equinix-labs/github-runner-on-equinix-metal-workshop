<!-- See https://squidfunk.github.io/mkdocs-material/reference/ -->
# Part 3: Setup a Github Self-Hosted Runner

In this steps we'll be getting familiar with GitHub Self-Hosted Runners. If it's your first time using Self-Hosted Runners, take a few minutes to flip through their [documentation](https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/about-self-hosted-runners).

## Steps

### 1. Setup your forked repo to use Self-Hosted Runners

Navigate to your `metal-cli` fork. For me it's [https://github.com/cprivitere/metal-cli](https://github.com/cprivitere/metal-cli), however it'll be different per person. It'll be in the format:

```
https://github.com/<your-github-username>/metal-cli
```

Click on the **Settings** tab, you should see a view like this:

![Metal CLI Settings Screenshot](../images/metal-cli-settings.png)

On the left bar, click on **Actions**, then **Runners**.

![Metal CLI Settings Runners Screenshot](../images/metal-cli-settings-runners.png)

To create a new Self-Hosted Runner, click the **new self-hosted runner** button.

![Metal CLI Settings Runners New Screenshot](../images/metal-cli-settings-runners-new.png)

Choose the correct OS and architecture option, if you're using the recommend system from the previous step, it would be **Linux** and **x64**.

![Metal CLI Settings Runner OS Screenshot](../images/metal-cli-settings-runners-os.png)

You should now see instructions for downloading, configuring, and using the GitHub Runner software.

![Metal CLI Settings Runner Instructions Screenshot](../images/metal-cli-settings-runners-instructions.png)

### 1. Run the commands to download and configure the runner

The first step to installing the GitHub Runner software would be to SSH into the machine you created earlier.

```sh
ssh root@your-metal-server
```

You'll also need to install `gcc`, create a new user, and switch to it. Github Runners do not run as `root`.

```sh 
apt update
apt install build-essential gcc
useradd -m ghrunner -s /bin/bash
su - ghrunner
```

Next, copy and paste the **Download** and **Configure** sections from the **Add New Runner** page from the previous step.

!!! note

  - Take the defaults by just pressing enter when it asks for the group, name, labels, and work folder.
  - Don't forget to run `./run.sh`
  - If you were doing this as a long lived runner in production this would be better executed as a systemctl service, but long lived runners are not recommended, so just running `./run.sh` inline is fine for today.

Your runner should now say it's **Listening for Jobs**.

## Discussion

Before proceeding to the next part let's take a few minutes to discuss what we did. Here are some questions to start the discussion.

- Can you have more than one self-hosted runner?
- What sorts of pre-requisites would your code repositories need on your own runners?
- How should I secure my runners?
