---
title: Create a fork using Aiven Client 
excerpt: Create a fork of the service using Aiven Command Line tool for fully managed services on AWS, Azure, or GCP.
product: mst
---

# Create a fork of your service using Aiven Client

When you a fork a service, you create an exact copy of the service, including
the underlying database. You can use it to create a development copy of your
production environment, set up a snapshot to analyze an issue or test an
upgrade, or create an instance in a different cloud, geographical location, or
under a different plan.

## Before you begin

*   [Install Aiven Client and connect][aiven-client-install] to Managed Service
    for TimescaleDB
*   [Create a service][create-service] in Managed Service for TimescaleDB

<procedure>

## Creating a fork of your service

1.  Switch to the `Project` that contains the service that you want to fork:

    ```bash
     avn switch <PROJECT>
    ```

1.  List the services in the `Project`:

    ```bash
     avn service list
    ```

1.  Make a note of the service that you want to fork, listed under
    `SERVICE_NAME` column in the output.

1.  Get the details of the service that you want to fork:

    ```bash
    avn service get <SERVICE_NAME>
    ```

1.  Create a fork of the service

    ```bash
    avn service create <NAME_OF_FORK> --project <PROJECT> -t <SERVICE_TYPE> --plan <PLAN> --cloud <CLOUD_NAME> -c service_to_fork_from=<NAME_OF_SERVICE_TO_FORK>
    ```

    For more information about projects, plans, and other details about
    services,see [Services][about-mst].

</procedure>

## Example

To create a fork named `grafana-fork` for a service named `grafana` in `fork-project`
on `timescale-aws-us-east-1` with the plan `dashboard-1`: 

```bash
   avn service create grafana-fork --project project-fork -t grafana --plan dashboard-1 --cloud timescale-aws-us-east-1  -c service_to_fork_from=grafana
```

You can switch to `project-fork` and view the newly created `grafana-fork` using:

```bash
   avn service list
```

[about-mst]: /mst/:currentVersion:/about-mst/
[aiven-client-install]: /mst/:currentVersion:/aiven-client/aiven-client-install/
[create-service]: /install/:currentVersion:/installation-mst/#create-your-first-service