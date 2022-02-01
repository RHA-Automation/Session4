# Session 4

## Motivation

`ansible-navigator` is a textual user interface (TUI) available to Ansible Automation Platform (AAP) subscribers and has been introduced with Ansible Automation Platform 2 as the primary interface for creating and testing ansible automation.

`ansible-navigator` also functions as a drop-in replacement for `ansible-playbook`, among other `ansible-*` utilities, and is the standard way of executing automation moving into Ansible Automation Platform 2.

## Installation

If you are not getting `ansible-navigator` from your AAP subscription (or even a developer subscription), you can install it using `pip` (adjust to suit your needs):

~~~bash
python3.9 -m venv rha-navigator
source rha-navigator/bin/activate
pip install --upgrade pip
pip install ansible-navigator
~~~

## Usage

### Old Syntax / New Syntax

| Old | New (interactive or `-m stdout`) |
| --- | --- |
| `ansible-playbook` | `ansible-navigator run` |
| `ansible-doc` | `ansible-navigator doc` |
| `ansible-config` | `ansible-navigator config` |
| `ansible-inventory` | `ansible-navigator inventory` |

#### Examples

~~~bash
ansible-navigator run ping.yml -i inventory -m stdout
ansible-navigator doc user -m stdout
ansible-navigator inventory -i inventory -m stdout --list
~~~

### Explore the TUI

Stuff we know already:

~~~bash
:config
:inventory
:doc ( :{{ examples }} )
:open
:run -i <inventory> ( :doc in task )
~~~

New options:

~~~bash
:images
:collections
:replay
~~~

### Configuration

`ansible-navigator.yml` is the config file present in each project that will determine how automation is created and executed with `ansible-navigator`.

## Execution Environments

### Download

[Container images at catalog.redhat.com](https://catalog.redhat.com/software/containers/search?q=execution%20environment&p=1&product_listings_names=Red%20Hat%20Ansible%20Automation%20Platform&build_categories_list=Automation%20Execution%20Environment)

~~~bash
podman login
podman pull registry.redhat.io/ansible-automation-platform-21/ee-29-rhel8
podman pull registry.redhat.io/ansible-automation-platform-21/ee-minimal-rhel8
podman pull registry.redhat.io/ansible-automation-platform-21/ee-supported-rhel8
~~~

### Enable Usage

In `ansible-navigator.yml` set `enabled: true` in `execution-environment` section.

What is a `run` doing:

~~~bash
ansible-navigator run ping.yml -i inventory --ll debug -m stdout
~~~

Bonus points:

~~~bash
ansible-navigator run usecase3_rootcontainers_networked.yml -i inventory --ll debug --vault-password-file /home/ansible/gitignored_secret --eei quay.io/kvegh/podautee -e @/home/ansible/vault-auth.yml -m stdout -u ansible 
~~~

## Resources

- [Ansible Navigator Creator Guide](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.1/html-single/ansible_navigator_creator_guide/index)
