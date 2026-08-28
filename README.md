# zsh-ansible-fzf

A ZSH plugin that completes **ansible-playbook tags** and works with **fzf-tab**.

After `-t` / `--tags` / `--skip-tags`, press `TAB` to pick tags from your playbooks. Prefix filters the list. By default each completion appends a comma so you can press `TAB` again to add more tags. Press `SPACE` (or `Enter`) to drop the trailing comma when you are done. Already-selected tags are omitted from the list. Set `ZSH_ANSIBLE_FZF_COMMA_SUFFIX=0` to disable the trailing comma.

## Table of Contents

-   [Dependencies](#dependencies)
-   [Installation](#installation)
-   [Usage](#usage)
-   [Properties](#properties)
-   [Contribution](#contribution)
-   [License](#license)

## Dependencies

-   [Oh My Zsh](https://ohmyz.sh/)
-   Optional: [fzf-tab](https://github.com/Aloxaf/fzf-tab) to select tags with fzf (stock ZSH completion still works without it)

## Installation

1. Install Plugin

```
wget -q https://raw.githubusercontent.com/alexiszamanidis/zsh-ansible-fzf/master/install -O install && \
chmod +x install && \
./install && \
rm -rf ./install
```

2.  Add plugin to plugin list

-   Open .zshrc(e.g. code .zshrc, vim .zshrc)
-   Add plugin to plugin list **before** `fzf-tab`

```
plugins=(... zsh-ansible-fzf fzf-tab)
```

3. Restart your shell or reload config file(source ~/.zshrc)

## Usage

```
ansible-playbook -t <TAB>
ansible-playbook -t zs<TAB>           # → zsh,
ansible-playbook -t zsh,<TAB>         # → zsh,nvim,
ansible-playbook -t zsh,nvim,<SPACE>  # → zsh,nvim
ansible-playbook --tags <TAB>
ansible-playbook --skip-tags <TAB>
```

Tags are collected from `tags:` in YAML under:

1. The playbook already on the command line
2. `local.yml` / `site.yml` / `playbook.yml` in the current directory
3. The current directory if it looks like an Ansible project (`ansible.cfg`, `roles/`, or `tasks/`)
4. `ZSH_ANSIBLE_FZF_FALLBACK_DIR` if set

## Properties

You can add the following properties to your .zshrc file:

| Property                       | Type   | Default value | Description                                                                 |
| ------------------------------ | ------ | ------------- | --------------------------------------------------------------------------- |
| ZSH_ANSIBLE_FZF_FALLBACK_DIR   | string | unset         | Directory to scan for tags when no playbook is on the CLI                   |
| ZSH_ANSIBLE_FZF_SPECIAL_TAGS   | string | unset         | Extra tags always offered for `--tags` / `--skip-tags` (e.g. `always never`) |
| ZSH_ANSIBLE_FZF_COMMA_SUFFIX   | string | `1`           | Append `,` after each completed tag so Tab can add more. Set to `0` to disable |

```
export ZSH_ANSIBLE_FZF_FALLBACK_DIR="$HOME/ansible"
export ZSH_ANSIBLE_FZF_SPECIAL_TAGS="all tagged untagged always never"
export ZSH_ANSIBLE_FZF_COMMA_SUFFIX=0
```

## Contribution

-   Reporting a bug
-   Improving this documentation
-   Sharing this project and recommending it to your friends
-   Giving a star on this repository

## License

[MIT © Alexis Zamanidis](https://github.com/alexiszamanidis/zsh-ansible-fzf/blob/master/LICENSE)
