# Deploy podinfo with a Simple Zarf Package

## Create Package

Use this command to package the podinfo Helm chart and container into a Zarf package

```bash
zarf package create --confirm
```

*Note: your local environment must be successfully authenticated with ghcr.com to pull the podinfo container*

## Stand up...

| ...k3d cluster | ...EKS cluster |
| - | - |
| Stand up a local k3d cluster | Stand up an EKS cluster |
| <pre><code>k3d cluster create</code></pre> | <pre><code>terraform init<br>terraform apply -var-file us-east.tfvars -auto-approve<br>aws eks --region us-east-2 update-kubeconfig --name eg-test-eks-cluster</code></pre> |

## Deploy the podinfo package

```bash
zarf init --confirm
zarf package deploy zarf-package-zarf-example-amd64.tar.zst --confirm
```
## Verify podinfo is running and establish a connection over a port-forward

```bash
kubectl get all -n podinfo
kubectl port-forward -n podinfo svc/zarf-podinfo 9898:9898
```

Navigate to <a href="localhost:9898">localhost:9898</a> in your browser

## Clean up...

| ...k3d cluster | ...EKS cluster |
| - | - |
| <pre><code>k3d cluster delete</code></pre> | <pre><code>terraform destroy -var-file us-east.tfvars -auto-approve</code></pre> |
