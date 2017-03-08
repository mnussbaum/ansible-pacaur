# ansible-pacaur

An Ansible module for installing [AUR](https://aur.archlinux.org/) packages via the [pacaur][pacaur] AUR helper.

This assumes your target node already has pacaur and its dependecies installed.

## Dependencies (Managed Node)

* [Arch Linux](https://www.archlinux.org/) (Obviously)
* [jshon](https://www.archlinux.org/packages/community/x86_64/jshon/) for pacaur
* [pacaur][pacaur]

## Installation

1. Clone this repo
2. Copy or link the `pacaur` file into your global Ansible library (usually `/usr/share/ansible`) or into the `./library` folder alongside your top-level playbook

## Usage

Pretty much identical to the [pacman module][pacman-mod]. Note that package status, removal, the corresponding `pacman` commands are used (`-Q`, `-R`, respectively).

More detailed docs are on the way, but in general:

### Options

| parameter    | required  | default | choices               | description                         |
|--------------|-----------|---------|-----------------------|-------------------------------------|
| name         | no        |         |                       | Name of the AUR package to install. |
| recurse      | no        | no      | yes/no                | Whether to recursively remove packages. See [pacman module docs][pacman-mod]. |
| state        | no        | no      | absent/present/latest | Whether the package needs to be installed or updated. |
| update_cache | no        | no      | yes/no                | Whether or not to refresh the master package lists. This can be run as part of a package installation or as a separate step. |
| upgrade      | no        | no      | yes/no                | Whether or not to upgrade the whole systemd. |

### Examples

```yaml
# Install package foo
- pacaur: name=foo state=present

# Ensure package fuzz is installed and up-to-date
- pacaur: name=fuzz state=latest

# Remove packages foo and bar
- pacaur: name=foo,bar state=absent

# Recursively remove package baz
- pacaur: name=baz state=absent recurse=yes

# Effectively run pacaur -Syu
- pacaur: update_cache=yes upgrade=yes
```

## Todo

* Add inline, ansible-doc compatible documentation
* ???

Have other ideas? Better way of doing something? Open an issue or a pull request.

[pacaur]: https://github.com/rmarquis/pacaur
[pacman-mod]: http://docs.ansible.com/pacman_module.html
