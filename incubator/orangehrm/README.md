# OrangeHRM

[OrangeHRM](https://www.orangehrm.com) is a free HR management system that offers a wealth of modules to suit the needs of your business. This widely-used system is feature-rich, intuitive and provides an essential HR management platform along with free documentation and access to a broad community of users.

## TL;DR;

```console
$ helm install stable/orangehrm
```

## Introduction

This chart bootstraps a [OrangeHRM](https://github.com/bitnami/bitnami-docker-orangehrm) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

It also packages the [Bitnami MariaDB chart](https://github.com/kubernetes/charts/tree/master/stable/mariadb) which is required for bootstrapping a MariaDB deployment for the database requirements of the OrangeHRM application.

## Prerequisites

- Kubernetes 1.4+ with Beta APIs enabled
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `my-release`:

```console
$ helm install --name my-release stable/orangehrm
```

The command deploys OrangeHRM on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following tables lists the configurable parameters of the OrangeHRM chart and their default values.

|              Parameter               |               Description                |                    Default                     |
|--------------------------------------|------------------------------------------|------------------------------------------------|
| `image`                              | OrangeHRM image                          | `bitnami/orangehrm:{VERSION}`                  |
| `imagePullPolicy`                    | Image pull policy                        | `IfNotPresent`                                 |
| `orangehrmUsername`                  | User of the application                  | `user`                                         |
| `orangehrmPassword`                  | Application password                     | _random 10 character long alphanumeric string_ |
| `smtpHost`                           | SMTP host                                | `nil`                                          |
| `smtpPort`                           | SMTP port                                | `nil`                                          |
| `smtpUser`                           | SMTP user                                | `nil`                                          |
| `smtpPassword`                       | SMTP password                            | `nil`                                          |
| `smtpProtocol`                       | SMTP protocol [`ssl`, `none`]            | `nil`                                          |
| `mariadb.mariadbRootPassword`        | MariaDB admin password                   | `nil`                                          |
| `serviceType`                        | Kubernetes Service type                  | `LoadBalancer`                                 |
| `persistence.enabled`                | Enable persistence using PVC             | `true`                                         |
| `persistence.apache.storageClass`    | PVC Storage Class for Apache volume      | `generic`                                      |
| `persistence.apache.accessMode`      | PVC Access Mode for Apache volume        | `ReadWriteOnce`                                |
| `persistence.apache.size`            | PVC Storage Request for Apache volume    | `1Gi`                                          |
| `persistence.orangehrm.storageClass` | PVC Storage Class for OrangeHRM volume   | `generic`                                      |
| `persistence.orangehrm.accessMode`   | PVC Access Mode for OrangeHRM volume     | `ReadWriteOnce`                                |
| `persistence.orangehrm.size`         | PVC Storage Request for OrangeHRM volume | `8Gi`                                          |
| `resources`                          | CPU/Memory resource requests/limits      | Memory: `512Mi`, CPU: `300m`                   |

The above parameters map to the env variables defined in [bitnami/orangehrm](http://github.com/bitnami/bitnami-docker-orangehrm). For more information please refer to the [bitnami/orangehrm](http://github.com/bitnami/bitnami-docker-orangehrm) image documentation.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
$ helm install --name my-release \
  --set orangehrmUsername=admin,orangehrmPassword=password,mariadb.mariadbRootPassword=secretpassword \
    stable/orangehrm
```

The above command sets the OrangeHRM administrator account username and password to `admin` and `password` respectively. Additionally it sets the MariaDB `root` user password to `secretpassword`.

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
$ helm install --name my-release -f values.yaml stable/orangehrm
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## Persistence

The [Bitnami OrangeHRM](https://github.com/bitnami/bitnami-docker-orangehrm) image stores the OrangeHRM data and configurations at the `/bitnami/orangehrm` and `/bitnami/apache` paths of the container.

Persistent Volume Claims are used to keep the data across deployments. This is known to work in GCE, AWS, and minikube.
See the [Configuration](#configuration) section to configure the PVC or to disable persistence.
