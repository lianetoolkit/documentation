# Liane Docker Production Setup

1. Install Docker and Docker Compose
2. Save the [`docker-compose.yml`](docker-compose.yml) file in an appropriate directory in your server (e.g.: `/home/liane`)
3. Edit evironment variables to match your setup
4. Run `docker-compose up -d` to build and start the containers in detached mode (running in the background)

All services have `unless-stopped` restart policy, meaning they will always stay up after crashes or reboots.

## Services

- **app**: Meteor application
- **files_server**: Web server to serve generated files from Meteor (people exports)
- **webhooks**: Micro-service that subscribe to Facebook webhooks and forward to Liane through Meteor's DDP protocol
- **mongo**: Mongo database
- **redis**: Redis database

## Volumes

Volumes will be locally stored in `.data/` directory.

## Web Server

This setup expects a web server with SSL/TLS to proxy requests to the application (3000 for Meteor and 3001 for the files web server).

## Database

This setup does not expose a public port for mongo or redis. If you are going to expose these ports, you should make sure to setup appropriate security measures.

You can also use a different setup for your databases, as long as you have them configured correctly in the `app` service variables.
