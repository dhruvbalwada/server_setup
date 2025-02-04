# Steps to setup a new remote server to fit into my workflow

## Access
- Get an account and password and confirm you can log in with `ssh user@remote`
- Add adequate profile to `.ssh/config`. Or in the case of my particular
workflow, add modify the /.../DATA_MANAGEMENT/dotfiles... ssh config and cp to
`.ssh/config`. Check if login works with new short name and pw.
- Automate login with ssh keys (this needs to be checked for security and
  maybe revised)
- Add iterm2 profile so that the access is super fast

## Software installation (to be filled in)
### Shell (???Does this install a new zsh shell, or would it require zsh to already be present???)
- install oh-my-zsh `sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"`
#### zsh substring search
just add `history-substring-search` to the plugins…
I added this to the ‘standard’ `.zshrc` file.

### git
- setup git on remote machine
  - set up an rsa key and add to github via [these](https://help.github.com/articles/connecting-to-github-with-ssh/) instructions
  - set git defaults:
    - `git config --global user.name "Mona Lisa"`
    - `git config --global user.email "email@example.com"`
- Create a subfolder `code` and in there clone server setup repo `git clone git@github.com:jbusecke/server_setup.git` (>>> create a subfolder in home directory)

### dotfiles
- Copy appropriate .zshrc from `server_setup/dotfiles`
- same with .bashrc (e.g. the modules are not loaded if a script runs in bash)
(??? Do both steps need to be done or only one depending on what shell one has???)

>>> at this point makes sense to go and install cookiecutter project, and use the cookiecutter science project template. https://github.com/jbusecke/cookiecutter-science-project

### File Structure
- ~~follow dir structure outlined in (other file, needs link) and create `code` in home directory. ` mkdir code notebooks projects shared_data`~~
Execute `setup_root.sh` from the `./code/conda_envs` directory
### Anaconda
- download miniconda
`wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda.sh`
(>>>> change this link based on your system, will be diff for mac or windows.)
- install miniconda to user dir `bash miniconda.sh -b -p $HOME/code/miniconda`
- ~~set path for miniconda `export PATH="$HOME/code/miniconda/bin:$PATH"`~~
- set path for miniconda in .zshrc `export PATH="$HOME/code/miniconda/bin:$PATH"`
- *Optional*: Create/Copy `.condarc` into root folder to install packages and envs in other locations (usefull for small home directories)
- create standard environment `conda env create -f code/server_setup/conda_files/standard.yml`
(??? Is this in addition to the base that is already present, or meant to replace that ???)
- (>>> after standard environment has been created one might want to create new ones, which inherit properties : https://stackoverflow.com/questions/40700039/how-can-you-clone-a-conda-environment-into-the-root-environment) (>> there are ways to update the conda environments using yaml files: https://stackoverflow.com/questions/42352841/how-to-update-an-existing-conda-environment-with-a-yml-file)

#### Managing Conda envs
https://conda.io/docs/user-guide/tasks/manage-environments.html
