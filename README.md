# samba-docker

Based on [Peter Winter's samba-alpine-docker](https://github.com/pwntr/samba-alpine-docker), a simple and lightweight Samba docker container, based on Alpine Linux base image.

Modified so the shared folder is public and writable by default. (no specific user for write access unlike original project)

Runs Samba's smbd and nmbd within the same container, using supervisord. Due to the fact that nmbd wants to broadcast
and become the "local master" on your subnet, you need to supply the "--net=host" flag to make the server visible to the hosts subnet (likely your LAN).

Quick start for the impatient:
```shell
docker run -d --net=host -v /path/to/share/:/shared --name samba softinnov/samba-docker
```

When NetBIOS discovery is not needed
```shell
docker run -d -p 137-139:137-139 -p 445:445 -v /path/to/share/:/shared --name samba softinnov/samba-docker
```
