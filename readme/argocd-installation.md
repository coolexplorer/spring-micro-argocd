# [ArgoCD Installation](https://argo-cd.readthedocs.io/en/stable/)
Argo CD is a declarative, [GitOps](https://www.gitops.tech) continuous delivery tool for Kubernetes.

## Installation

### Install ArgoCD
```bash
$ kubectl create namespace argocd
$ kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

If you are not interested in UI, SSO, multi-cluster features then you can install core Argo CD components only:

```bash
$ kubectl create namespace argocd
$ kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/core-install.yaml
```

Use argocd login --core to configure CLI access.


### Download Argo CD CLI
Download the latest Argo CD version from https://github.com/argoproj/argo-cd/releases/latest. More detailed installation instructions can be found via the CLI installation documentation.

Also available in Mac, Linux and WSL Homebrew:
```bash
$ brew install argocd
```

### Access The Argo CD API Server
There are 3 ways to access to the Argo CD API server

#### Service Type Load Balancer
Change the argocd-server service type to LoadBalancer:
This way is useful if you set up your environemt on the cloud and on-promise with Load balancer.

```bash
$ kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

#### Ingress
Follow the [ingress documentation](https://argo-cd.readthedocs.io/en/stable/operator-manual/ingress/) on how to configure Argo CD with ingress.

#### Port Forwarding
Kubectl port-forwarding can also be used to connect to the API server without exposing the service. 
This is a good way when you want to test Argo CD on your local environment.

```bash
$ kubectl port-forward svc/argocd-server -n argocd 8081:443
```
The API server can then be accessed using the localhost:8081

