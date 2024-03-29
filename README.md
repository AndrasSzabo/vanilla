# vanilla
This is an empty repository with information about setting up repositories in general.

**Disclaimer**: These notes are primarily for me to remember, so they might not work on all systems.

## Multiple github accounts

### 1. Set up multiple ssh keys
If you use more than one github accounts, it can be confusing which one is used by default. The first thing is to set up an ssh key for each account, for example:
```
ssh-keygen -t rsa -C "email_1@address.com" -f "id_rsa_1"
ssh-keygen -t rsa -C "email_2@address.com" -f "id_rsa_2"
```
Make sure the keys are registered with the correct github accounts.

### 2. Set up a custom ssh connection
When connecting to github through ssh, you should specify which key to use.

#### A. Set up two different ssh hosts via `.ssh/config`
In the `.ssh/config` file, set up two hosts for github. For example:
```
Host github.com
  HostName  github.com
  User  git
  IdentityFile ~/.ssh/id_rsa_1

Host github.com-2
  HostName  github.com
  User  git
  IdentityFile ~/.ssh/id_rsa_2
```
When cloning the repo, make sure to use the right host. For example, to use the `id_rsa_2` key, clone with:
```
git clone git@github.com-2:<Your User Name>/<your repo name>.git
```
Note the `github.com-2` hostname. This way `ssh` will automatically use the `id_rsa_2` key.

#### B. Configuring through git
The default `ssh` command can be overwritten in git. This can be achieved either by running:
```
git config --local core.sshCommand "ssh -i ~/.ssh/id_rsa_2"
```
or at the initial cloning of the repo. To set the default ssh command during cloning, use:
```
git clone git@github.com:<Your User Name>/<your repo name>.git --config core.sshCommand="ssh -i ~/.ssh/id_rsa_2
```

### 3. Configure the user name and email

Besides the correct ssh connection, the user name and email address have to be correctly set up too. This can be done in a few ways.

#### A. Configuring in each repo
In the repo, the local user can be set up as:
```
git config --local user.name "The user name"
git config --local user.email "The email"
```
This will make sure that the commits appear with the correct user name.

#### B. Using global `.gitconfig` files
The above can be automated for a specific folder and its subdirectories. To do this, create a global default configuration file (`~/.gitconfig`) and specify the default settings and a conditional include statement:
```
[user]
        email = <Email 1>
        name = <User name 1>
[includeIf "gitdir:<Folder path>"]
        path = ~/.gitconfig_2
[core]
        editor = vi
[init]
        defaultBranch = main
[credential]
        helper = cache
```
The above example `~/.gitconfig` file will make sure that when repos are located in the `<Folder path>` (or its sub-directories), then the `~/.gitconfig_2` is loaded. In `~/.gitconfig_2` the configuration (email, name, etc) can be overwritten, for example:
```
[user]
        email = <Email 2>
        name = <User name 2>
[core]
        editor = vi
[init]
        defaultBranch = main
[credential]
        helper = cache
```
With this setup the default settings will be used (`~/.gitconfig`) everywhere except in the directory `<Folder path>` and its subdirectories, where the `~/.gitconfig_2` configuration will be used.


## Testing diagrams integration


Please read <a href="https://github.com/jgraph/drawio-integration" target="_blank">this</a> for a high-level introduction.

GitHub support is now available https://app.diagrams.net/?mode=github

An example for integration into GitHub wikis is available here: https://github.com/jgraph/drawio/wiki/Embed-Diagrams

--

![Diagram](https://github.com/AndrasSzabo/vanilla/blob/main/code_structure.drawio.png)

<a href="https://github.com/AndrasSzabo/vanilla/blob/main/edit-diagram.html?repo=vanilla&path=code_structure.drawio.png" target="_blank">Edit</a> | 
<a href="https://app.diagrams.net/#Uhttps%3A%2F%2Fraw.githubusercontent.com%2Fjgraph%2Fdrawio-github%2Fmaster%2Fdiagram.png" target="_blank">Edit As New</a> | 
<a href="https://app.diagrams.net/?src=about#HAndrasSzabo%2Fvanilla%2Fmain%2Fcode_structure.drawio" target="_blank">Edit in diagrams.net</a>

<a href="http://jgraph.github.io/drawio-github/edit-diagram.html" target="_blank">edit-diagram.html</a> does the I/O with GitHub and uses diagrams.net in embed mode for diagram editing. The page supports the following URL parameters: user, pass, repo, path, ref and action=open (the Edit link above is an example). Using action=open, links for immediate diagram editing in GitHub can be created (requires user and pass parameters). You can also use files on GitHub as templates in diagrams.net via the url parameter (see Edit As New above).

Supported file formats: .png, .svg, .html and .xml (default)
