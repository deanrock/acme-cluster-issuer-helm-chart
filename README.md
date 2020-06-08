# ACME ClusterIssuer

## Introduction

This is a simple chart that creates ClusterIssuer for ACME provider.

Kubernetes Ingress with `ingressClass: traefik` is assumed, but you can adjust it with `ingress.class` value.

## Configuration

| Parameter          | Description          | Default                                                   |
| --------------- | -------------------------------- | ------------------------------------------------ |
| `acme.email`    | Email supplied to ACME provider. | `""`                                             |
| `acme.server`   | ACME server.                     | `https://acme-v02.api.letsencrypt.org/directory` |
| `ingress.class` | Class of ingress resource.       | `traefik`                                        |

## Installing

### Creating ClusterIssuer using CLI

Add chart repository to Helm:

```bash
helm repo add acme-cluster-issuer https://deanrock.github.io/acme-cluster-issuer-helm-chart/
```

You can update the chart repository by running:

```bash
helm repo update
```

```bash
helm install --set email=test@example.test acme-cluster-issuer acme-cluster-issuer/acme-cluster-issuer
```

### Creating ClusterIssuer using Terraform

```terraform
resource "helm_release" "acme-cluster-issuer" {
  name       = "acme-cluster-issuer"
  repository = "https://deanrock.github.io/acme-cluster-issuer-helm-chart/"
  namespace  = "default"
  chart      = "acme-cluster-issuer"
  version    = "0.1.3"

  values = [
    yamlencode(
      {
        acme = {
          email = var.letsencrypt_email
        }
      }
    )
  ]
}
```
