# Minikube
This repo can be used to setup a local kubernetes installation based on minikube.
Checkout https://minikube.sigs.k8s.io/ for more information.

## Prerequisites
For general prerequisites of minikube, see https://minikube.sigs.k8s.io/docs/start/#what-youll-need.

To fullfill the prerequisites for the automation in this repo, run these commands to install
the necessary packages:

```
python3 -m pip install --upgrade --user -r requirements.txt
```

## Installation
Run the following commands to start the installation:
  * Start with <code>ansible-playbook install.yaml</code> and provide your sudo password
  * Refresh your shell with <code>. /etc/profile.d/minikube.sh</code>
  * Ensure the client works with <code>minik get pods</code>

## Start/Stop minikube
After the installation, minikube will be started but it won't be added to the autostart,
unless `minikube_autostart: true`. You can provide it by adding `-e minukube_autostart=true`
to the `ansible-playbook install.yaml` command, or by setting it in [vars.yaml](vars.yaml).

To start minikube, run `minikube start`. To stop minikube, run `minikube stop`. To delete the
current cluster, run `minikube delete`.

See `minikube help` for a list of all available subcommands.

## Web UI Access
The kubernetes-dashboard is bundled with minikube and can be started by running `minikube dashboard`.

### Bash aliases
The playbook creates the bash autocompletion config for `minikube` commands 
and aliases to ease the usage of `minikube` and `minikube kubectl` commands.

The following aliases are created:

| Alias | Command               | Notes                                                                   |
| ----- | --------------------- | ----------------------------------------------------------------------- |
| minik | `minikube kubectl --` | To run kubectl commands with the included binary, e.g. `minik get pods` |

## Deinstallation
To deinstall the minikube environment, run <code>ansible-playbook deinstall.yaml</code>
and provide your sudo password when prompted.
