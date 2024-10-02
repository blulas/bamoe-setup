# Installing IBM Business Automation Manager Open Editions on a Local Workstation

This repository sets up the required infrastructure services in order to run IBM Business Automation Manager Open Editions (BAMOE) using `docker-compose.yaml`, which includes the followin components:

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
    docker compose up
    ~~~

3. This will bring up:

  ~~~ text
  IBM Business Automation Manager Open Edition v9.1.1
  PostgreSQL Database with the SQL to create it
  
  KIE Sandbox - the new method for editing DMN models and BPMN models
  KIE Extended Services to run DMN models as you make modifications in KIE Sandbox
  GitHub CORS Proxy image to be able to do local GitHub communication with GitHub through CORS
  ~~~

For IBM Canvas, you can access this by default at [IBM Canvas](http://localhost:9090), which is configured in the compose yaml with various settings. These can be further customized, for documentation on it refer to the [Quay Image Repository](https://quay.io/repository/bamoe/canvas) and the [Product Documentation](https://www.ibm.com/docs/en/ibamoe/9.1.1).
# bamoe-setup
