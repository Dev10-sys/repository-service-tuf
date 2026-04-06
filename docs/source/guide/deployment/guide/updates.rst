=======
Updates
=======

This section guides you through the process of safely updating and applying security patches to your Repository Service for TUF (RSTUF) deployment.

General Recommendations
=======================

* **Version Pinning**: Always pin your deployment to a specific version (e.g., ``v1.2.0``) rather than using the ``latest`` tag. This prevents unintended upgrades and ensures reproducibility.
* **Backups**: Always perform a complete backup of your database, storage volumes, and any associated state (such as Redis) before initiating an upgrade.
* **Security Updates**: Regularly check the RSTUF release notes and security advisories. When a security patch is released, prioritize its deployment within your environment following the steps below.

How to update Docker Deployment
===============================

The following steps explain how to apply updates when deploying via Docker or Docker Compose:

1. Stop existing services to prevent data corruption during the update:

   .. code:: shell

       $ docker compose stop

2. Pull the updated container images for the specified versions in your ``docker-compose.yml``:

   .. code:: shell

       $ docker compose pull

3. Start the services with the newly pulled images. The ``-d`` flag starts them in the background:

   .. code:: shell

       $ docker compose up -d

How to update Helm Deployment
=============================

For deployments managed with Helm in Kubernetes, follow these steps:

1. Update your local Helm repository cache to fetch the latest chart versions:

   .. code:: shell

       $ helm repo update

2. Upgrade the deployment, specifying the updated chart version. Ensure that your ``values.yaml`` has the correct tag pinned in the image references:

   .. code:: shell

       $ helm upgrade rstuf repository-service-tuf/rstuf -f values.yaml --version <new-chart-version>
