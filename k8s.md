# Kubernetes installation with k0s

You can install onpremise single standalone kubernetes cluster and play with k0s.

k0s is an open source, all-inclusive Kubernetes distribution, which is configured with all of the features needed to build a Kubernetes cluster. Due to its simple design, flexible deployment options and modest system requirements, k0s is well suited for

- Any cloud
- Bare metal
- Edge and IoT

k0s drastically reduces the complexity of installing and running a CNCF certified Kubernetes distribution. With k0s new clusters can be bootstrapped in minutes and developer friction is reduced to zero. This allows anyone with no special skills or expertise in Kubernetes to easily get started.

k0s is distributed as a single binary with zero host OS dependencies besides the host OS kernel. It works with any Linux without additional software packages or configuration. Any security vulnerabilities or performance issues can be fixed directly in the k0s distribution that makes it extremely straightforward to keep the clusters up-to-date and secure.

Production ready clusters can be also deployed with k0sctl.

The k0s version to be used is 1.23.5, referenced as v1.23.5+k0s.0. You can see or change this into `01-base-ansible/roles/download/defaults/main.yml` file.

``` yaml
k0s_version: v1.23.5+k0s.0
```

# Previous requirements

You need to adjust some values in `env_variables` file before that. Copy `env_variables.sample` file as `env_variables`.

```bash
$ cp env_variables.sample env_variables
```

Edit the previous file

```bash
$ code env_variables
```

```yaml
...
kubeconfig_cluster_name: "CHANGEME"
kubeconfig_context_name: "CHANGEME"

# set some descriptive text, like
kubeconfig_cluster_name: "MyAwesomeCluster"
kubeconfig_context_name: "MyAwesomeCluster"
...
...
ssh_allow_users: "root"

# example: (take care that root user always need to be present !!!)
ssh_allow_users: "root@12.3.6.22"
# or
ssh_allow_users: "jdoe sam root@12.3.6.22"
...
...
fail2ban_ignoreips: [CHANGEME]
fail2ban_destemail: "CHANGEME"

# example:
fail2ban_ignoreips: [127.0.0.1/8, 1.1.1.1/32]
fail2ban_destemail: "my@ma.il"
...
...
user_name: "CHANGEME"
user_certificate_pub: 'CHANGEME'

# example:
user_name: "myuser"
user_certificate_pub: '/Users/myuser/.ssh/id_rsa.pub'
...
```

**Warning: be sure to set this settings before continue !!**


Finally adjust some values in `hosts` file before that. Copy `hosts.sample` file as `hosts`.

```bash
$ cp hosts.sample hosts
```

Edit the previous file

```bash
$ code hosts
```

```yaml
...
mynode ansible_host=CHANGEME

# example: use your server ip address
mynode ansible_host=144.23.55.12

```


Now we can proceed with server configuration and kubernetes deployment.

Please, be sure that you can connect with ssh passwordless as root user to your remote server.

```bash
$ ssh root@my-remote-server
```

We can continue.

In order to go step by step, please do single commands:

```bash
# update base OS and some other settings
ansible-playbook 1-playbook-base.yaml;

# basic kernel hardening
ansible-playbook 2-playbook-kernel-hardening.yaml;

# ensure AIDE is configured
ansible-playbook 3-playbook-crontab.yaml;

# protect SSH
ansible-playbook 4-playbook-ssh.yaml;

# install Docker (optional, but recommended)
ansible-playbook 5-playbook-docker.yml

# install k0s
ansible-playbook 6-playbook-k0s.yml;

# update standalone node as worker also
kubectl taint nodes mynode node-role.kubernetes.io/master-

# add network pods and openebs
ansible-playbook 7-playbook-k8s.yaml;

# configure basic firewall rules
ansible-playbook 8-playbook-firewall.yaml;

# protect your host with fail2ban
ansible-playbook 9-playbook-fail2ban-banip.yaml;
ansible-playbook 10-playbook-fail2ban.yaml;

# optional - add custom user account
# ansible-playbook playbook-users.yaml;

# optional - unban remote ip address from fail2ban
# set your custom ip address inside this playbook
# ansible-playbook playbook-fail2ban-unbanip.yaml;

# Done ;)
```

> Congratulations, we can play now with our k8s standalone single cluster ;)

Now you can do [some deployments by hand to play with it](cli.md).
