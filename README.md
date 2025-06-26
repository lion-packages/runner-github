### Init container

```bash
docker compose up -d --build
```

### Into container (root)

```bash
docker exec -it service-ubuntu-app bash
```

```bash
groupmod -g 984 docker

usermod -aG docker lion

chmod 660 /var/run/docker.sock

ls -l /var/run/docker.sock
```

### Restart container

```bash
docker compose restart
```

### Into container

```bash
docker exec -it -u lion service-ubuntu-app bash
```
