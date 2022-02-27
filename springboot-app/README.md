app-springboot: SpringBoot Application
===================================================

Level: Beginner
Technologies: SpringBoot, Spring MVC, Spring Security
Summary: SpringBoot, Spring MVC, Spring Security
Target Product: <span>Keycloak</span>
Source: <https://github.com/keycloak/keycloak-quickstarts>


What is it?
-----------

The `app-springboot` quickstart demonstrates how to write a SpringBoot application that is secured with <span>Keycloak</span>.

This application contains 2 pages :

* A public landing page.
* A secured product page.

This application also show how to combine Spring Security with <span>Keycloak</span>.


System Requirements
-------------------

The quickstart requires that you have the [SpringBoot Service](../service-springboot-rest/README.md) running. It protects a secure page 
running at `http://localhost:8090/secure`. 

See the [Getting Started Guide](../docs/getting-started.md) for the minimum requirements and steps to build and run the quickstart.


Configuration in <span>Keycloak</span>
-----------------------

Prior to running the quickstart you need to create a client in <span>Keycloak</span> and download the installation file.

The following steps shows how to create the client required for this quickstart:

* Open the <span>Keycloak</span> admin console
* Select `Clients` from the menu
* Click `Create`
* Add the following values:
  * Client ID: You choose (for example `app-springboot`)
  * Client Protocol: `openid-connect`
  * Root URL: URL to the application (for example `http://localhost:8090`)
* Click `Save`

Once saved you need to change the `Access Type` to `confidential` and click save.


If you deploy the application somewhere else change the hostname and port of the URLs accordingly.

Finally, you need to update the adapter using SpringBoot's configuration file (application.properties) :

````
server.connection-timeout=5000
spring.freemarker.cache=false
server.port = 8090

keycloak.realm=keycloak-tutorial
keycloak.auth-server-url=http://localhost:8080/auth
keycloak.ssl-required=external
keycloak.resource=app-springboot
keycloak.credentials.secret=1c79fd4b-1d01-43d6-a6a4-255b8ecab0c6

keycloak.public-client=false
````



Build and Run the Quickstart
-------------------------------

1. Open a terminal and navigate to the root directory of this quickstart.

2. The following shows the command to deploy the quickstart:

   ````
   mvn spring-boot:run

   ````

Access the Quickstart
---------------------

You can access the application with the following URL: <http://localhost:8090/>.

Integration test of the Quickstart
----------------------------------

1. Make sure you have an <span>Keycloak</span> server running with an admin user in the `master` realm or use the provided docker image
2. Maker sure the [service-springboot-rest](../service-springboot-rest) is running
3. Run `mvn test -Pspring-boot`
