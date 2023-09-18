# Minikube
This repo can be used to setup a local kubernetes installation based on minikube.
Checkout https://minikube.sigs.k8s.io/ for more information.

## Prerequisites
For general prerequisites of minikube, see https://minikube.sigs.k8s.io/docs/start/#what-youll-need.

The setup in this repo assumes that you are running on Ubuntu and that you want to use Docker as driver for minikube.
You can install docker alongside minikube by adding `-e minikube_install_docker=true` to the `ansible-playbook install.yaml` command.

To fullfill the prerequisites for the automation in this repo, run these commands to install
the necessary packages and collections:

```
python3 -m pip install --upgrade --user -r requirements.txt
ansible-galaxy collection install -r requirements.yaml
```

## Installation
Run the following commands to start the installation:
  * Start with <code>ansible-playbook install.yaml</code> and provide your sudo password
  * Refresh your shell with <code>. /etc/profile.d/minikube.sh</code>
  * Ensure the client works with <code>minik get pods</code>

The installation was tested on Ubuntu 22.04.1 LTS (Jammy Jellyfish).

## Start/Stop minikube
After the installation, minikube will be running but it won't be added to the autostart. 
You can add it to the autostart by providing `-e minukube_autostart=true` to the `ansible-playbook install.yaml` command,
or by setting it in the [vars.yaml](vars.yaml) file.

To start minikube, run `minikube start`. To stop minikube, run `minikube stop`. To delete the
current cluster, run `minikube delete`.

See `minikube help` for all available commands.

## Web UI Access
The kubernetes-dashboard is bundled with minikube and can be started by running `minikube dashboard`.

### Bash aliases
The playbook creates the bash autocompletion config for `minikube` commands 
and aliases to ease the usage of `minikube` and `minikube kubectl` commands.

The following aliases are created:

| Alias | Command               | Notes                                                                   |
| ----- | --------------------- | ----------------------------------------------------------------------- |
| minik | `minikube kubectl --` | To run kubectl commands with the included binary, e.g. `minik get pods` |

> Note: If you have `kubectl` installed, you can run those commands as usual instead.

## Deinstallation
To deinstall the minikube environment, run <code>ansible-playbook deinstall.yaml</code>
and provide your sudo password when prompted.
