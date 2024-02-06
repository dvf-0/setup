# Setup script for Redash with Docker on Ubuntu Server

This is a reference setup for Redash on a single Ubuntu server, which uses Docker and Docker Compose for deployment and management.

This is the same setup we use for our official images (for AWS & Google Cloud) and can be used as reference if you want to manually setup Redash in a different environment (different OS or different deployment location).

- `setup.sh` is the script that installs everything and creates the directories.
- `docker-compose.yml` is the Docker Compose setup we use.
- `packer.json` is Packer configuration we use to create the Cloud images.

## Tested

- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS

## FAQ

### Can I use this in production?

For small scale deployments -- yes. But for larger deployments we recommend at least splitting the database (and probably Redis) into its own server (preferably a managed service like RDS) and setting up at least 2 servers for Redash for redundancy. You will also need to tweak the number of workers based on your usage patterns.

### How do I upgrade to newer versions of Redash?

See [Upgrade Guide](https://redash.io/help/open-source/admin-guide/how-to-upgrade).

### How do I use `setup.sh` on a different operating system?

You will need to update the `install_docker` function and maybe other functions as well.

### How do I remove Redash if I no longer need it?

1. Stop the Redash container and remove the images using `docker-compose down --volumes --rmi all`.
2. Remove the following lines from `~/.profile`

  ```
  export COMPOSE_PROJECT_NAME=redash
  export COMPOSE_FILE=/opt/redash/docker-compose.yml
  ```
  
3. Delete the Redash folder using `sudo rm -fr /opt/redash`

