# MONAI Label Helm Chart

This repository contains a Helm chart to deploy MONAI Label on Kubernetes.

[MONAI Label](https://docs.monai.io/projects/label/en/latest/index.html) is a framework for deep learning based medical image analysis.

## Installation

To install MONAI Label using this Helm chart, you can use the following command:

```
helm install monai-label ./monai
```

This will deploy MONAI Label with the default configuration.

## Configuration

The following table lists the configurable parameters of the MONAI Label chart and their default values:

| Parameter                    | Description                               | Default                      |
|------------------------------|-------------------------------------------|------------------------------|
| `replicaCount`               | Number of replicas for the deployment     | `1`                          |
| `image.repository`           | Docker image repository                   | `containers.renci.org/helxplatform/monailabel` |
| `image.tag`                  | Docker image tag                          | `0.0.1`                      |
| `image.pullPolicy`           | Image pull policy                         | `IfNotPresent`               |
| `image.command`              | Command to run inside the container       | `["/bin/bash"]`              |
| `image.tty`                  | Allocate a TTY for the container         | `true`                       |
| `image.stdin`                | Attach standard input to the container   | `true`                       |
| `imagePullSecrets`           | Docker registry pull secret               | `[]`                         |
| `nameOverride`               | Override the name of the chart            | `""`                         |
| `fullnameOverride`           | Override the full name of the resources  | `""`                         |
| `serviceAccount.create`      | Whether to create a service account      | `true`                       |
| `serviceAccount.annotations` | Annotations to add to the service account| `{}`                         |
| `serviceAccount.name`        | Name of the service account to use       | `""`                         |
| `podAnnotations`             | Annotations to add to the pod            | `{}`                         |
| `podSecurityContext`         | Pod security context                     | `{ "runAsNonRoot": true, "runAsUser": 1000 }` |
| `securityContext`            | Security context for the container       | `{}`                         |
| `service.type`               | Kubernetes service type                  | `ClusterIP`                  |
| `service.port`               | Service port                              | `8000`                       |
| `ingress.enabled`            | Whether to enable Ingress                | `true`                       |
| `ingress.annotations`        | Annotations for Ingress                   | `{ "cert-manager.io/cluster-issuer": "letsencrypt" }` |
| `ingress.hosts`              | List of Ingress hosts                    | `[{ "host": "monai.renci.org", "paths": ["/"] }]` |
| `ingress.tls`                | Ingress TLS configuration                | `[{ "hosts": ["monai.renci.org"], "secretName": "monai.renci.org-tls" }]` |
| `resources.requests.cpu`     | CPU resource requests                    | `200m`                       |
| `resources.requests.memory`  | Memory resource requests                 | `2G`                         |
| `resources.requests.ephemeral-storage` | Ephemeral storage resource requests | `2Gi` |
| `resources.limits.cpu`       | CPU resource limits                      | `1000m`                      |
| `resources.limits.memory`    | Memory resource limits                   | `4G`                         |
| `resources.limits.ephemeral-storage` | Ephemeral storage resource limits | `4Gi` |
| `resources.limits.nvidia.com/mig-1g.5gb` | NVIDIA MIG resource limits        | `1`                          |
| `resources.limits.nvidia.com/mig-2g.10gb`| NVIDIA MIG resource limits        | `1`                          |
| `autoscaling.enabled`        | Enable Horizontal Pod Autoscaler        | `false`                      |
| `autoscaling.minReplicas`    | Minimum number of replicas               | `1`                          |
| `autoscaling.maxReplicas`    | Maximum number of replicas               | `100`                        |
| `autoscaling.targetCPUUtilizationPercentage` | Target CPU utilization percentage | `80`            |
| `nodeSelector`               | Node labels for pod assignment           | `{}`                         |
| `tolerations`                | Toleration labels for pod assignment     | `[]`                         |
| `affinity`                   | Affinity settings for pod assignment     | `{}`                         |

## Usage

After installing MONAI Label, you can access it via the configured service.

To access MONAI Label, you can use the following:

```
kubectl port-forward svc/monai-label 8000:8000
```

## License

This project is licensed under the [MIT License](https://github.com/helxplatform/monai-chart/blob/develop/LICENSE.md).