# Suraj's custom zsh config/dotfiles

This is just a modified version of [Prezto](https://github.com/sorin-ionescu/prezto)

## Installation

Now to install my zsh_config (which is just prezto but customized to my needs)

01. Configure `$XDG_CONFIG_HOME` and `$ZDOTDIR` for defining config location
    for zsh:

    ```shell
    export XDG_CONFIG_HOME="${XDG_CONFIG_HOME:=$HOME/.config}"
    [[ -d $XDG_CONFIG_HOME/zsh ]] && export ZDOTDIR="$XDG_CONFIG_HOME/zsh"
    ```

02. Clone this repo in `$ZDOTDIR` directory:

    ```shell
    git clone --recursive https://github.com/maths-lover/zsh_config $ZDOTDIR/.zprezto
    ```

03. Setup runcoms, zshenv and aliases in user home:

    ```shell
    setopt EXTENDED_GLOB
    for rcfile in "${ZDOTDIR:-$HOME}"/.zprezto/runcoms/^README.md(.N); do
      ln -s "$rcfile" "${ZDOTDIR:-$HOME}/.${rcfile:t}"
    done

    # zshenv
    ln -v "${ZDOTDIR:-$HOME}"/.zprezto/dot_zshenv $HOME/.zshenv

    # aliases
    ln -v "${ZDOTDIR:-$HOME}"/.zprezto/dot_alias.zsh "${ZDOTDIR:-$HOME/.zprezto/}"
    ```

04. Source zshenv to take effect or just open a new terminal and execute zsh

    ```shell
    source $ZDOTDIR/.zshenv
    ```

05. (Optional) Change shell to zsh as default on login

    ```shell
    chsh -s /bin/zsh
    ```

06. (Required) Do look at `$ZDOTDIR/.zshrc` and `$ZDOTDIR/.zprofile` to
    make sure you have all values according to your needs,
    e.g.,
    - `DEV_DIR` where I put my development projects, (work or personal both),
    - `DEV_TOOLS_DIR` where I store tools which I don't intend to develop,
    but use them for my dev purposes (e.g., pyenv, etc.), etc.

## Other optional tooling

01. fzf (Fuzzy finder)

    To install this, execute following, but don't make changes to zshrc in last step
    and setup `FZF_INSTALL_DIR`

    ```shell
    export FZF_INSTALL_DIR="$HOME/.fzf"

    # also update the zprofile for your path
    sed -i '/FZF_INSTALL_DIR/c\export FZF_INSTALL_DIR=\"$HOME/.fzf\"'

    # install
    git clone --depth 1 https://github.com/junegunn/fzf.git $FZF_INSTALL_DIR
    $FZF_INSTALL_DIR/install

    # to access in current shell
    export PATH="$PATH:$FZF_INSTALL_DIR/bin" # only in current shell

    # check for success
    fzf --version
    ```

02. fzf-git.sh (Fuzzy finder with git support)

    Install it same like fzf and set fzf-git installation dir

    ```shell
    export FZF_GIT_INSTALL_DIR="$HOME/.fzf-git.sh"

    # also update zprofile
    sed -i '/FZF_GIT_INSTALL_DIR/c\export FZF_GIT_INSTALL_DIR=\"$HOME/.fzf-git.sh\"'

    git clone --depth 1 https://github.com/junegunn/fzf-git.sh $FZF_GIT_INSTALL_DIR

    # check if it got placed properly or not
    [ -f $FZF_GIT_INSTALL_DIR/fzf-git.sh ] && echo "ok" || echo "error"
    ```

03. starship prompt (really good, fast and feature rich prompt)

    Install starship with following command,

    ```shell
    curl -sS https://starship.rs/install.sh | sh
    ```

    or just use your package manager to install it,
    e.g., for Arch Linux,

    ```shell
    sudo pacman -S starship
    ```

    or just look [starship](https://starship.rs/guide/) for other options.

    Then symlink the starship prompt config (if you want so)

    ```shell
    ln -sv $ZDOTDIR/.zprezto/starship.toml $XDG_CONFIG_HOME/starship.toml
    ```

04. thefuck (for command correction)

    If you don't want to use this tool, you may delete it's
    initialization from `$ZDOTDIR/.zshrc` to stop using it.

    Otherwise, install it using your package manager, rest all is done in the config.
    If it is not available by package manager, look For
    [installation instructions](https://github.com/nvbn/thefuck#installation)

05. pyenv (Python users)

    For Python users, if you ever intended to use `pyenv`,
    just install it and update `PYENV_ROOT` in `$ZDOTDIR/.zprofile`
