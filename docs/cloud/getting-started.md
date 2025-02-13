# Getting Started

## Prerequisites

You will need to install the following software:

- [Python 3.12+](https://www.python.org/downloads/)
- [pipx](https://pipx.pypa.io/stable/)
- [tailscale](https://tailscale.com/)

> **Note:** For tailscale, you don't need to login on the tailscale website. Here wee use a self-hosted tailscale instance.

## Installation labctl

Labctl is a command-line tool that helps you to manage your account and resources on the LaboInfra service.

```bash
pipx install labctl
```

> **Note:** You can also install labctl using pip, but we recommend using pipx to avoid conflicts with other python packages.

## Configuration labctl

Set the LaboInfra API URL with the following command:

```bash
labctl config set --api-endpoint=https://api.laboinfra.net/
```

## Reset password

When your account is created, or you have forgotten your password, you will receive an email with a token to reset your password.

Use the following command to reset your password:

```bash
labctl reset-password --username USERNAME --token TOKEN
```

> **Note:** Replace `USERNAME` with your username and `TOKEN` with the token received by email.
> Passwords must have at least 12 characters, including uppercase, lowercase, numbers, and special characters.

## Login

Use the following command to login:

```bash
labctl login
```

## Tailscale

To access the resources on the LaboInfra service, you need to install tailscale and connect to the network.
When your tailscale is installed, you can self enroll your device with the following command:

```bash
labctl devices enroll
```

## OpenStack

By default your account is created in openstack but you dont have any resources yet. You can create a new project with the following command:

```bash
labctl project create PROJECT_NAME
```

This will create a new project with the name `PROJECT_NAME` and add you as a member.

You also need to get your OpenStack credentials to access the resources. Use the following command:

```bash
labctl reset-openstack-password
```

This will print to the console your OpenStack password. For the username, use the same username you use to login to the LaboInfra service.

You can now access the OpenStack dashboard with the following URL: [Openstack Console](https://console.cloud.laboinfra.net/horizon/)

## Next steps

For more information about how to use labctl, check the [CLI documentation](cli.md).
