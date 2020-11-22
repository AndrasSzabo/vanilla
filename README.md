# vanilla
This is an empty repository with information about setting up repositories in general. 

**Disclaimer**: These notes are primarily for me to remember, so they might not work on all systems. 

## Multiple github accounts

If you use more than one github accounts, it can be confusing which one is used by default. The first thing is to set up an ssh key for each account (eg: `ssh-keygen -t rsa -C "email@address.com" -f "id_rsa_1"`). Make sure the keys are registered with the correct github accounts. After this, there are more than one ways to associate an ssh key with a repository - see below

### Setting up a custom ssh connection
#### 1. ssh hosts

When cloning, make sure to use the correct ssh channel. These are set up in the `.ssh/config` as `Host`. This config file should have entries such as: 
```
Host github.com
  HostName  github.com
  User  git
  IdentityFile ~/.ssh/id_key_file_for_this_host
```
This will help to automatically use the right ssh key with the repo. So when cloning, make sure the `git clone` command the hostname should match the one defined in the `Host` line. 

#### 2. custom ssh command

Clone the repo with `git clone git@github.com:<Your User Name>/<your repo name>.git --config core.sshCommand="ssh -i ~/.ssh/id_key_file_for_this_host`

This will automatically the default Set up a custom ssh command in the git locally. If one manages to clone the repo, then this can be done afterwards by running: `git config --local core.sshCommand "ssh -i ~/.ssh/private_ssh_key_file"`. 

Note that both methods reference the **private** key, not the public. 

### Next: configuration 

In the repo, set up the local user as:
```
git config --local user.name "The user name"
git config --local user.email "The email"
```
This will make sure that the commits appear with the correct user name. 
