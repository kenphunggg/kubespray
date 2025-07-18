# Personal snapshot for deploying a Product Ready Kubernetes Cluster

![Kubernetes Logo](https://raw.githubusercontent.com/kubernetes-sigs/kubespray/master/docs/img/kubernetes-logo.png)

## Install with ansible

### Install ansible

Kubespray supports multiple ansible versions and ships different `requirements.txt` files for them. Depending on your available python version you may be limited in choosing which ansible version to use.

It is recommended to deploy the ansible version used by kubespray into a python virtual environment.

First, make sure you have `python3-venv` in your machine

```ShellSession
sudo apt install python3-venv
```

Then you can install `Ansible` by following these steps

```ShellSession
KUBESPRAYDIR=kubespray
cd $KUBESPRAYDIR
VENVDIR=kubespray-venv
python3 -m venv $VENVDIR
source $VENVDIR/bin/activate
pip install -U -r requirements.txt
```

In case you have a similar message when installing the requirements:

```ShellSession
ERROR: Could not find a version that satisfies the requirement ansible==7.6.0 (from -r requirements.txt (line 1)) (from versions: [...], 6.7.0)
ERROR: No matching distribution found for ansible==7.6.0 (from -r requirements.txt (line 1))s
```

It means that the version of Python you are running is not compatible with the version of Ansible that Kubespray supports. If the latest version supported according to pip is 6.7.0 it means you are running Python 3.8 or lower while you need at least Python 3.9 (see the table below).

### Ansible Python Compatibility

Based on the table below and the available python version for your ansible host you should choose the appropriate ansible version to use with kubespray.

| Ansible Version | Python Version |
|-----------------|----------------|
| >= 2.17.3       | 3.10-3.12      |

### Building your own inventory

```ShellSession
# Copy ``inventory/sample`` as ``inventory/mycluster``
cp -rfp inventory/sample inventory/mycluster

# Install the cluster
ansible-playbook -i inventory/mycluster/iventory.ini cluster.yml -b -v \
  --private-key=~/.ssh/private_key -K
```
