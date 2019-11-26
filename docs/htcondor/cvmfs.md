# CVMFS HandsOn

Workaround for known bug Docker-XFS:

```bash
truncate -s 500M /opt/cvmfs/spool/test

mkfs.ext4 /opt/cvmfs/spool/test

mkdir -p /opt/docker/

mount /opt/cvmfs/spool/test /opt/docker/
```

Docker compose for deploying a stratum0 + client:

```yaml
version: "2"
services:
  cvmfs-client:
    image: cloudpg/cvmfs-client
    container_name: cvmfs-client
    hostname: cvmfs-client
    privileged: true
    depends_on:
      - cvmfs-stratum0
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup
    environment:
      - "SERVER_NAME=cvmfs-stratum0"
      - "REPO_NAME=myrepo.dodas"
    tty: true

  cvmfs-stratum0:
    image: cloudpg/cvmfs-stratum0-base
    container_name: cvmfs-stratum0
    hostname: cvmfs-stratum0
    privileged: true
    volumes:
      - /opt/docker/:/var/spool/cvmfs
      - /var/cvmfs-docker/stratum0/cvmfs:/cvmfs
      - /var/cvmfs-docker/stratum0/srv/cvmfs:/srv/cvmfs
      - /var/cvmfs-docker/stratum0/etc/cvmfs:/etc/cvmfs
      - /sys/fs/cgroup:/sys/fs/cgroup
```

Bring up the containers:

```bash
docker-compose up
```

Create a cvmfs repository:

``` bash
docker exec -ti cvmfs-stratum0 bash

cvmfs_server mkfs myrepo.dodas

exit
```

Copy the key of the repository into the client:

```bash
docker cp /var/cvmfs-docker/stratum0/etc/cvmfs/keys/myrepo.dodas.pub cvmfs-client:/etc/cvmfs/keys

docker exec -ti cvmfs-client bash

bash -c "/etc/cvmfs-init-scripts/client-init.sh myrepo.dodas cvmfs-stratum0"

ls /cvmfs/myrepo.dodas

cat /cvmfs/myrepo.dodas/new_repository

exit
```

Log into the Stratum0 and then let's see how to create and publish a file:

```bash
cvmfs_server transaction myrepo.dodas

echo "testme" >> /cvmfs/myrepo.dodas/test.txt

cvmfs_server publish myrepo.dodas

exit
```

Into the client again:

```bash
ls /cvmfs/myrepo.dodas/test.txt

cat /cvmfs/myrepo.dodas/test.txt
```

## Acknowledgements

https://github.com/gabrielefronze/cvmfs-server-container