Thursday 8 August 2024

# Init

First day at Nebero Systems, mentor assigned to me was Suraj Dadral, an alumini of GNDEC.
First conversation was about what i know and what i don't. I was asked if i know gitlab and CI/CD. I had done it before using GitHub actions, there i was confident i can do it. So it begin.

# First Task

First task was to install GitLab. It was fairly simple but it was along these lines:

```bash
sudo apt-get update
sudo apt-get install -y curl openssh-server ca-certificates perl postfix
```


Then i added the debian package repository, which is simplified by GitLab:

```
  curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | sudo bash
```

The tutorial told me to setup my DNS to point to the machine, but since i was going to setup GitLab and use it on the same machine, i just added it to the hosts file.

```
echo 127.0.0.1	gitlab.example.com | sudo tee /etc/hosts
```


After the installation was complete, i logged in and there it was, GitLab was installed.

GitLab is a heavy application. It can quickly become a black hole for your memory, therefore its wise to stop it when not in use during developement.

```bash
sudo gitlab-ctl stop
```


