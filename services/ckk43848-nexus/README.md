# Nexus Setup

Before deploying Nexus, please review and update the following in your `values.yaml` file:

1. Define the storage location for Nexus files.
2. Add configuration entries for each device. Sample devices are already provided.
3. Confirm that RabbitMQ is reachable at `ckk43848-rabbitmq-daq.diamond.ac.uk`.
4. Specify the User ID in the security context to allow writing Nexus files. Typically, this should be set to `ckk43848-detector` UID and GID. 
    You can find these by running: `id ckk43848-detector`
