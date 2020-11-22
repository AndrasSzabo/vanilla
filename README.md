# vanilla
This is an empty repository showing how to set up a repo

1. When cloning, make sure to use the correct ssh channel. These are set up in the `.ssh/config` as `Host`. This config file should have entries such as: 
```
Host github.com
  HostName  github.com
  User  git
  IdentityFile ~/.ssh/id_key_file_for_this_host
```
This will help to automatically use the right ssh key with the repo

2. In the repo, set up the local user as:
```
git config --local user.name "The user name"
git config --local user.email "The email"
```
