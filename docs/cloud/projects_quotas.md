# Manage projects and quotas

## Introduction

On Laboinfra, you get a quota assigned by an admin. This quota includes resources like RAM, CPU, and storage, and it’s yours to distribute across different projects as needed.

Using the API or the labctl CLI, you can:

- Create new projects,
- Add members to your projects,
- Allocate your quota however you want between your projects.

This gives you full control over how you use your resources, making it easy to collaborate and work on multiple school projects efficiently.

## Projects

### Create a new project

```bash
labctl project create PROJECT_NAME
```

!!! info
    Project names are suffixed with a unique identifier to ensure they are unique across the platform.

### List your projects

```bash
labctl project list
```

### Add a member to a project

```bash
labctl project add-user PROJECT_NAME MEMBER_NAME
```

### Remove a member from a project

```bash
labctl project del-user PROJECT_NAME MEMBER_NAME
```

!!! info
    Before removing a member from a project, make sure your project have enough resources quota to accommodate

### Delete a project

```bash
labctl project delete PROJECT_NAME
```

??? warning
    In order to delete a project, you must first delete all the resources associated with it (VMs, disks, etc.) and remove all quotas allocated to it.

## Quotas

Type of quotas:

| Type  | Description |
|-------|-------------|
| `cpu` | CPU cores   |
| `mem` | RAM in GB   |
| `sto` | Disk in GB  |

### Display your quota

With the me command you get global information about your account, including your quota.

```bash
labctl me
```

### Allocate quota to a project

```bash
labctl quota set PROJECT_NAME TYPE VALUE
```

### Display quota for a project

With this command you can see how much quota is allocated to a project and who share the quota to the project.

```bash
labctl quota show-project PROJECT_NAME
```

### Remove quota from a project

If you just want to decrease the quota allocated to a project, you can use the same command as allocating quota, but with the new value you want to set.

```bash
labctl quota set PROJECT_NAME TYPE VALUE
```

If you want to remove all the quota allocated to a project, you can use the following command:

```bash
labctl quota unset PROJECT_NAME TYPE
```
