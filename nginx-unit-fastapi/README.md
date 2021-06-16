## NGINX-Unit-FastAPI
[nginx unit](https://unit.nginx.org/howto/fastapi/) has [support for ASGI Python apps](https://www.nginx.com/blog/nginx-unit-updates-for-autumn-2020-now-available/) and it's set up to work with FastAPI is as simiple as [this](https://levelup.gitconnected.com/deploying-an-asynchronous-fastapi-on-nginx-unit-b038288bec5).

This repo is an example of how to build a FastAPI app using nginx-unit instead of the Gunicorn-Uvicorn setup
### Build
```
docker build -t nginx-unit-fastapi .
```

### Run
```
docker run -p 5000:80 -it --rm --name nginx-unit-fastapi-container nginx-unit-fastapi
```

### Update nginx config
```
docker exec -it ginx-unit-fastapi-container /bin/bash
sudo curl -X PUT -d '5' \
       --unix-socket /var/run/control.unit.sock http://localhost/config/applications/fastapi/processes
```
The above example set the number of processes to 5 for our fastapi app. For more on configuration management, see the [doc](https://unit.nginx.org/configuration/#configuration-management).
