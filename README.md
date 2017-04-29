# Ubuntu 16.04 LTS OAH Test Image

Ubuntu 16.04 LTS (Xenial) Docker container for Ansible playbook and role testing.
[![Docker Automated build]](https://hub.docker.com/r/openapphack/oah-docker-ubuntu1604/)

## How to Build

This image is built on Docker Hub automatically any time the upstream OS container is rebuilt, and any time a commit is made or merged to the `master` branch. But if you need to build the image on your own locally, do the following:

  1. [Install Docker](https://docs.docker.com/engine/installation/).
  2. `cd` into this directory.
  3. Run `docker build -t oah-ubuntu1604 .`

## How to Use

  1. [Install Docker](https://docs.docker.com/engine/installation/).
  2. Pull this image from Docker Hub: `docker pull openapphack/oah-docker-ubuntu1604:latest` (or use the tag you built earlier, e.g. `oah-ubuntu1604`).
  3. Run a container from the image: `docker run --detach --privileged --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro openapphack/oah-docker-ubuntu1604:latest /usr/lib/systemd/systemd` (to test Ansible roles, add in a volume mounted from the current working directory with ``--volume=`pwd`:/etc/ansible/roles/role_under_test:ro``).
  4. Use Ansible inside the container:
    a. `docker exec --tty [container_id] env TERM=xterm ansible --version`
    b. `docker exec --tty [container_id] env TERM=xterm ansible-playbook /path/to/ansible/playbook.yml --syntax-check`
