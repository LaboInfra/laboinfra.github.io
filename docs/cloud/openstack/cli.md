# Configure OpenStack CLI

## Introduction

To interact with the OpenStack cloud, you need to authenticate via the Keystone identity service. It returns a **Token** and a **Service Catalog**, which contains the endpoints for various services (Compute, Image, Identity, Object Storage, Block Storage, Networking, etc.).

This document explains how to configure the OpenStack client to connect to your cloud.

## Installation

Use `pipx` to install the OpenStack client:

```bash
pipx install python-openstackclient
```

For more information, refer to the official documentation: [python-openstackclient](https://docs.openstack.org/newton/user-guide/common/cli-install-openstack-command-line-clients.html).

## Get Configuration Files

Go to `OpenStack Console -> Project -> API Access -> Download OpenStack RC File` to obtain the necessary configuration files: `clouds.yaml` or `openrc.sh`. You can use either to configure the OpenStack client.

## Get Custom Certificate

You can download the Public ROOT CA of the laboinfra at [Laboinfra_Root_CA_2024.pem](https://docs.laboinfra.net/assets/Laboinfra_Root_CA_2024.pem)

### Method 1: Using `clouds.yaml`

The `clouds.yaml` file allows OpenStack tools to work without manually exporting environment variables. Place it in `~/.config/openstack/`:

```bash
mkdir -p ~/.config/openstack
cp ~/Downloads/clouds.yaml ~/.config/openstack/clouds.yaml
```

If you have multiple cloud accounts, add them to the `clouds` section of the existing file and specify the cloud using the `OS_CLOUD` environment variable or the `--os-cloud` option:

```bash
export OS_CLOUD=openstack
```

In our lab environment, we use a custom certificate. So you need to edit the configuration to trust the custom certificate.

```yaml
clouds:
  openstack:
    auth:
      # ...existing configuration...
    cacert: PATH_TO_LABO_CA.pem
```

### Method 2: Using `openrc.sh`

The `openrc.sh` file sets the necessary environment variables for OpenStack authentication. Source it in your terminal session:

```bash
source ~/Downloads/openrc.sh
```

In our lab environment, we use a custom certificate. So you need to export the `OS_CACERT` environment variable to trust the custom certificate:

```bash
export OS_CACERT=PATH_TO_LABO_CA.pem
```

## Verify Configuration

Run the following command to verify the configuration:

```bash
openstack catalog list
```

If the configuration is correct, you will see a list of services and their endpoints.
if not, check the configuration files and environment variables.
