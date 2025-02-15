# My unified setup for different OS
**Personal experience:** 5 years using Windows. Switched to MacOS 1.5 years ago.

**Rationale:** Unify the experience between Windows and MacOS, including keyboard mapping (MacOS as baseline), terminal, workflow...

## Windows
### Terminal
1. Install WSL with latest Ubuntu Distro

```shell
wsl --install -d <Distribution Name>
```
More instruction on: [WSL start guide](https://learn.microsoft.com/en-us/windows/wsl/install)

2. Install Windows Terminal and set hotkey

Go `Setting -> Actions -> Add new` and set `Crtl+q` as `Show/Hide the Terminal Window`.

3. Set zsh as the default shell in WSL

```shell
chsh -s $ (which zsh)
```

4. install [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting) and [zsh-history-substring-search](https://github.com/zsh-users/zsh-history-substring-search). source the setting in the zsh respectively

```shell
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
echo "source ${(q-)PWD}/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc
```

```shell
git clone git@github.com:zsh-users/zsh-history-substring-search.git
echo "source ${(q-)PWD}/zsh-history-substring-search/zsh-history-substring-search" >> ${ZDOTDIR:-$HOME}/.zshrc
```

then set the key up and key down actions according to [installation guide](https://github.com/zsh-users/zsh-history-substring-search/blob/master/README.md)

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

It applies a color schema, and displays the current conda venv name and current git branch. (git branch name will not show if there is no `.git` in the current directory). The prompt will look like this after `source .zshrc`

![image](https://github.com/user-attachments/assets/5302c5b0-3ad6-49b3-86c0-96d5235f8394)

6. Install and setup Miniconda

download:

```
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

init:
```
./Miniconda3-latest-Linux-x86_64.sh
```

and follow the initialization guide.

prevent conda from showing env name in the prompts

```shell
# prevent conda from modifying the prompt
conda config --set changeps1 False
```

### Mouse
[Reverse Mouse Scroll](https://github.com/microsoft/PowerToys/issues/6434)

### Keyboard
1. Install [PowerToys](https://learn.microsoft.com/en-us/windows/powertoys/install)
2. Go to `C:\Users\{username}\AppData\Local\Microsoft\PowerToys\Keyboard Manager`. Backup the original `default.json`. Create a new `default.json` and copy paste the following mapping. Result: **Map the keyboard layout identical with MacOS**

```json
{"remapKeys":{"inProcess":[{"originalKeys":"164","newRemapKeys":"162"},{"originalKeys":"91","newRemapKeys":"164"},{"originalKeys":"162","newRemapKeys":"91"}]},"remapShortcuts":{"global":[{"originalKeys":"160;27","newRemapKeys":"160;192"},{"originalKeys":"162;9","newRemapKeys":"164;9"},{"originalKeys":"162;77","newRemapKeys":"91;68"},{"originalKeys":"162;160;9","newRemapKeys":"164;160;9"},{"originalKeys":"162;164;27","newRemapKeys":"164;115"},{"originalKeys":"91;9","newRemapKeys":"162;9"},{"originalKeys":"91;160;9","newRemapKeys":"162;160;9"},{"originalKeys":"91;162;32","newRemapKeys":"91;186"}],"appSpecific":[{"originalKeys":"162;37","newRemapKeys":"164;37","targetApp":"chrome"},{"originalKeys":"162;39","newRemapKeys":"164;39","targetApp":"chrome"},{"originalKeys":"91;32","newRemapKeys":"162;32","targetApp":"code"},{"originalKeys":"91;65","newRemapKeys":"162;65","targetApp":"windowsterminal"},{"originalKeys":"91;67","newRemapKeys":"162;67","targetApp":"windowsterminal"}]}}
```
_Note: This step is optional and is not recommended **to be performed** on keyboards with `Fn`._
### Screen (if applicable)
[Arrange multiple screens](https://support.microsoft.com/en-us/windows/how-to-use-multiple-monitors-in-windows-329c6962-5a4d-b481-7baa-bec9671f728a)

### Clipboard
1. Windows clipboard: `windows + V`
_Not working well with some laptops_

2. **Waiting for a better tool**

### Browser
1. Install Chrome
2. Login with accounts and everything should be synced

## MacOS

1. Install Alfred, Shottr, Iterm

TODO
