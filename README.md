# vanilla
This is an empty repository showing how to set up a repo. To set up the correct credentials (in case you have more than one github accounts), there are at least 2 ways to do it. 


## Setting up the correct ssh connection
1. ssh hosts

When cloning, make sure to use the correct ssh channel. These are set up in the `.ssh/config` as `Host`. This config file should have entries such as: 
```
Host github.com
  HostName  github.com
  User  git
  IdentityFile ~/.ssh/id_key_file_for_this_host
```
This will help to automatically use the right ssh key with the repo. So when cloning, make sure the `git clone` command the hostname should match the one defined in the `Host` line. 

2. custom ssh command 

Set up a custom ssh command in the git locally. If one manages to clone the repo, then this can be done afterwards by running: `git config --local core.sshCommand "ssh -i ~/.ssh/private_ssh_key_file"`. 


## Configuration 

In the repo, set up the local user as:
```
git config --local user.name "The user name"
git config --local user.email "The email"
```
