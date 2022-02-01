# ansible-minik8s-ghost-cloudflared
A repo to apply a k8s cluster of Ghost and cloudflared in a minikube environment 

## Prerequisites

* ansible 

* minikube

* cloudflared

## Tested versions of prereqs

```
❯ ansible --version
ansible [core 2.12.1]

❯ cloudflared --version
cloudflared version 2022.1.3 (built 2022-01-28-1554 UTC)

```

## What does this do?

The playbook is setup to start the minikube Kubernetes cluster running on a host machine. It assumes that minikube is already installed along with the other prerequisitie programs.

The playbook then creates a Deployment for a Ghost blog setup including persistent local storage for the blog. A Service is also created for the Blog deployment. This is done so that Minikube can expose it. Which allows the cloudflared Deployment to connect to Cloudflare's edge from the cluster.

The playbook then creates, if not already present, a Named Tunnel target for cloudflared. It then creates a Deployment for cloudflared which is defaulted to two replicas.

The top of the playbook contains a vars section where a user can update the playbook variables relative to their host machine/setup.

## How to use?

After setting environment variables the playbook can be ran as follows.

```
❯ ansible-playbook  -i hosts main.yaml
```

The `-v` flag can be expanded upon in case additional debugging is needed.

```
❯ ansible-playbook -vvv -i hosts main.yaml
```

To improve debugging consider adding the following to your `ansible.cfg` file.

```
[defaults]
(...)
# Added below per: https://stackoverflow.com/questions/37171966/clean-error-output-in-ansible-playbook
stdout_callback=debug
stderr_callback=debug
```

## Plans

Improve cloudflared usage.

Add additional branch with basic Go applicaiton. 

Create play to retrieve existing remote Ghost config and install it?

Additonal branches with container configs?