# axshare

server API: https://github.com/XanderCheung/axshare-go
## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run dev
```

### Compiles and minifies for production
```
npm run build:prod
```

***

Dockerize axshare

    docker build -t xandercheung/axshare .
    docker run -it -p 9666:80 -d --rm --name axshare xandercheung/axshare

Run Docker app
    
    docker run -v /docker/data/axshare/config/nginx.conf:/etc/nginx/conf.d/default.conf \
      -p 9666:80 -d --rm --name axshare registry.cn-shanghai.aliyuncs.com/xandercheung/axshare
    
 or
 
    chmod +x docker.sh
    ./docker.sh