# Installing IBM Business Automation Manager Open Editions on a Local Workstation

This repository sets up the required infrastructure services in order to run IBM Business Automation Manager Open Editions (BAMOE) using `docker-compose`, which includes the following components:

- Postgresql: 5432
- PgAdmin: 8055
- Keycloak: 8480
- BAMOE Canvas: 9090
- BAMOE Management Console: 8280
- BAMOE Task Console: 8380
- Maven Repository: 8088

## Default method

Running the `docker-compose.yaml` as is will build the system as a sample environment pulling in the requisite containers. To do this you can follow these steps.

1. Clone this repository

    ~~~shell
    git clone https://github.com/blulas/bamoe-setup.git
    ~~~

2. Bring up the environment through a docker compose up command

    ~~~shell
    cd docker-compose
    ./installServices.sh infra
    ~~~

3. This will bring up:

  ~~~ text
  IBM Business Automation Manager Open Edition v9.1.1

  - PostgreSQL Database with the SQL to create it
  - BAMOE Canvas - The new web-based tooling for editing DMN and BPMN models
  - BAMOE Canvas Extended Services - To run DMN models as you make modifications in Canvas
  - GitHub CORS Proxy - Image to be able to do local GitHub communication with GitHub through CORS
  - BAMOE Management Console - A console to manage process instances
  - BAMOE Task Console - A console used to manage process task lifecycles
  ~~~

## Installed Services

Services installed during this process can be accessed at:

- For IBM BAMOE Canvas, you can access this by default at [IBM BAMOE Canvas](http://localhost:9090), which is configured in the compose yaml with various settings. These can be further customized, for documentation on it refer to the [Quay Image Repository](https://quay.io/repository/bamoe/canvas) and the [Product Documentation](https://www.ibm.com/docs/en/ibamoe/9.1.1).

- For IBM BAMOE Management Console, you can access this by default at [IBM BAMOE Management Console](http://localhost:8280).  For documentation on it refer to the [Product Documentation](https://www.ibm.com/docs/en/ibamoe/9.1.1).

- For IBM BAMOE Task Console, you can access this by default at [IBM BAMOE Task Console](http://localhost:8380).  For documentation on it refer to the [Product Documentation](https://www.ibm.com/docs/en/ibamoe/9.1.1).

## Maven Repository

For more information on how to properly setup Maven for local development, visit [Setting Up Maven](./maven/README.md).
