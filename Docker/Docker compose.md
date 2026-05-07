Docker compose is a tool for defining and running multi-container applications.
It is the key to unlocking a streamlined and efficient development and deployment experience.

Compose is a tool to control the entire application stack.
It is used to manages all the services, network, and volumes in a single [[YAML]] configuration file.

With it you can 
- Start, stop and rebuild service.
- View the status of running services
- Stream the log output of running services
- Run a one-off command on a service.

**Depends_on** :
This attribute is used for compose flow.
You can control the order of service startup and shutdown, it is useful if services are closely coupled, and the startup sequence impacts the application's functionality.
If your application needs to access the database and both services are started with docker compose up,
there is a chance this will fail since the application service might start before the database service and won't find a database able to handle its SQL stateme nts.

