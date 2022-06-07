# k8s-starter

Welcome here :)

This repos will allow you try some basic interactions with the process of create and play with a Kubernetes Cluster standalone or managed.

# Requirements

1. Clone this repo locally
2. Install Ansible in your localhost
3. Install k9s
4. Install Helm

## Clone this repo

Go to your command shell and do:

```bash
git clone https://github.com/hrodriguezmx/k8s-starter.git
cd k8s-starter
```

## Ansible installation

Refer to [Ansible website](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

Ansible is an agentless automation tool that you install on a control node. From the control node, Ansible manages machines and other devices remotely (by default, over the SSH protocol).

To install Ansible for use at the command line, simply install the Ansible package on one machine (which could easily be a laptop). You do not need to install a database or run any daemons. Ansible can manage an entire fleet of remote machines from that one control node.

### Installing Ansible on specific operating systems

Follow these instructions to install the Ansible community package on a variety of operating systems. Please, use your specific distro.

```bash
# Fedora based
sudo dnf install ansible

# RHEL based
$ sudo yum install ansible

# CentOS based
$ sudo yum install epel-release
$ sudo yum install ansible

# Ubuntu based PPA
$ sudo apt update
$ sudo apt install software-properties-common
$ sudo add-apt-repository --yes --update ppa:ansible/ansible
$ sudo apt install ansible

# FreeBSD based
$ sudo pkg install py27-ansible

# macOS
$ brew install ansible

```

Please, see <https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html> for more options and details.

# k9s

K9s provides a terminal UI to interact with your Kubernetes clusters. The aim of this project is to make it easier to navigate, observe and manage your applications in the wild. K9s continually watches Kubernetes for changes and offers subsequent commands to interact with your observed resources.

## Installation

K9s is available on Linux, macOS and Windows platforms. Binaries for Linux, Windows and Mac are available as tarballs in the [release](https://github.com/derailed/k9s/releases) page.

Via Homebrew for macOS or LinuxBrew for Linux

```bash
brew install k9s
```

or use wget

```bash
wget -c https://github.com/derailed/k9s/releases/download/v0.25.18/k9s_Linux_x86_64.tar.gz

tar xfvz k9s_Linux_x86_64.tar.gz

mv k9s /usr/local/bin

```

# Installing Helm

This guide shows how to install the Helm CLI. Helm can be installed either from source, or from pre-built binary releases.

```bash
# macOS
brew install helm

# Debian/Ubuntu
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm

# details
https://helm.sh/docs/intro/install/

```

You can continue with the [Kubernetes installation with k0s using Ansible](k8s.md).
