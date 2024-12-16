# My Setup for my computers

## Windows
### Terminal
1. Install WSL with latest Ubuntu Distro
2. Install Windows Terminal and set hotkey

Go `Setting -> Actions -> Add new` and set `Crtl+q` as `Show/Hide the Terminal Window`.

3. Set zsh as the default shell in WSL
4. install [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting) and [zsh-history-substring-search](https://github.com/zsh-users/zsh-history-substring-search). source the setting in the zsh respectively
5. Creating `~/.zshrc` and copy paste the following content
```shell
parse_git_branch() {
    git branch 2> /dev/null | sed -n -e 's/^\* \(.*\)/[\1]/p'
    if [[ -n $branch ]]; then
        
        echo "$branch"
    else
        echo ""  # Return empty string if no branch
    fi
}
COLOR_DEF='%f'
COLOR_USR='%F{42}'
COLOR_DIR='%F{40}'
COLOR_GIT='%F{2}'
COLOR_CONDA='%F{45}'

NEWLINE=$'\n'
setopt PROMPT_SUBST
# Set the prompt to include the user, directory, and optionally the Git branch
export PROMPT='${COLOR_CONDA}($CONDA_DEFAULT_ENV) ${COLOR_DIR}%2d$(parse_git_branch) ${COLOR_DEF}> '

# Add a space only if the branch is not empty
export PROMPT='${COLOR_CONDA}($CONDA_DEFAULT_ENV) ${COLOR_DIR}%2d$(if [[ -n $(parse_git_branch) ]]; then echo " ${COLOR_GIT}$(parse_git_branch)"; fi) ${COLOR_DEF}> '
```
6. Install and setup Miniconda
```shell
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/home/ziqiwang/miniconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
  eval "$__conda_setup"
else
  if [ -f "/home/ziqiwang/miniconda3/etc/profile.d/conda.sh" ]; then
      . "/home/ziqiwang/miniconda3/etc/profile.d/conda.sh"
  else
      export PATH="/home/ziqiwang/miniconda3/bin:$PATH"
  fi
fi
unset __conda_setup
# <<< conda initialize <<<
```
```shell
# prevent conda from modifying the prompt
conda config --set changeps1 False
```
### Keyboard
1. Install [PowerToys](https://learn.microsoft.com/en-us/windows/powertoys/install)
2. Go to `C:\Users\{username}\AppData\Local\Microsoft\PowerToys\Keyboard Manager`. Backup the original `default.json`. Create a new `default.json` and copy paste the following mapping. Result: **Map the keyboard layout identical with MacOS**
```json
{"remapKeys":{"inProcess":[{"originalKeys":"164","newRemapKeys":"162"},{"originalKeys":"91","newRemapKeys":"164"},{"originalKeys":"162","newRemapKeys":"91"}]},"remapShortcuts":{"global":[{"originalKeys":"160;27","newRemapKeys":"160;192"},{"originalKeys":"162;9","newRemapKeys":"164;9"},{"originalKeys":"162;77","newRemapKeys":"91;68"},{"originalKeys":"162;160;9","newRemapKeys":"164;160;9"},{"originalKeys":"162;164;27","newRemapKeys":"164;115"},{"originalKeys":"91;9","newRemapKeys":"162;9"},{"originalKeys":"91;160;9","newRemapKeys":"162;160;9"},{"originalKeys":"91;162;32","newRemapKeys":"91;186"}],"appSpecific":[{"originalKeys":"162;37","newRemapKeys":"164;37","targetApp":"chrome"},{"originalKeys":"162;39","newRemapKeys":"164;39","targetApp":"chrome"},{"originalKeys":"91;32","newRemapKeys":"162;32","targetApp":"code"},{"originalKeys":"91;65","newRemapKeys":"162;65","targetApp":"windowsterminal"},{"originalKeys":"91;67","newRemapKeys":"162;67","targetApp":"windowsterminal"}]}}
```
### Clipboard
Windows clipboard
`windows + V`
### Browser
1. Install Chrome
2. Login with accounts and everything should be synced


## MacOS

1. Install Alfred, Shottr, Iterm

TODO
