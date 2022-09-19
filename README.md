<h1 align="center">Lizz compatible Vaultwarden application</h1>

Lizz compatible application to add the [Vaultwarden application](https://github.com/dani-garcia/vaultwarden) to a Lizz managed Kubernetes cluster.

To learn more about Lizz, see the [documentation](https://openlizz.com).

## Requirements

To add the application, you first need to have a [Kubernetes cluster initialized with Lizz](https://openlizz.com/docs/guides/init).
You also need to have the [Lizz CLI installed](https://openlizz.com/docs/installation).

## Add the application

To add the application to your cluster, run the following:

```bash
lizz add github \
    --owner=$GITHUB_USER  \
    --fleet=fleet \
    --origin-url=https://github.com/openlizz/application-vaultwarden \
    --path=./default \
    --destination=vaultwarden \
    --personal
```

Check the [guide](https://openlizz.com/docs/guides/add) to understand how works the lizz add command.

> **Note**
> You can adapt the command depending on your use case. See the [command API](https://openlizz.com/docs/cli/lizz_add_github) for more information.

Reconcile the fleet repository to deploy the application using [Flux](https://fluxcd.io/):

```
flux reconcile source git flux-system
```

Check the pods with:

```
kubectl get pod -n vaultwarden
```

The output should be similar to:

```
NAMESPACE       NAME                                        READY   STATUS    RESTARTS      AGE
vaultwarden     vaultwarden-bc4c9965d-5m9jm                 1/1     Running   0             2m49s
```
    
## Usage

Access the application using port-forwarding or using the ingress created.
Go to the admin page `/admin` and enter the admin token shown in the lizz add command output.
From this page you can manage accounts, etc... To create an account, you need to invite a new user from the admin page and then create the account from the main page. 

Refer to the [Bitwarden user manuel](https://bitwarden.com/help/) to learn how to use Vaultwarden.

## Acknowledgements

This repository is only a wrapper to the [Helm chart](https://bjw-s.github.io/helm-charts/docs/app-template/introduction/) of the [Vaultwarden application](https://github.com/dani-garcia/vaultwarden) to help its deployment in a Kubernetes cluster managed by Lizz.

Therefore, the credit goes to the developers and maintainers of the application and the chart.