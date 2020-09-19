# Docker
---

* Docker commands

```bash
docker run <image>
docker start <image|id>
docker stop <image|id>
docker ps [-a]
docker rm <name|id>
```

* examples

```bash
docker run -it ubuntu bash
docker run -d -p 80:80 --name webserver nginx
```

* Create Image

```bash
docker build -t user/img-name .
```
