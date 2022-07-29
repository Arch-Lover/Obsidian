```Dockerfile
FROM centos:7

RUN yum install httpd -y

ENV HTML beginner-html-site-styled

WORKDIR /var/www/html/

ADD https://github.com/mdn/$HTML/archive/refs/heads/gh-pages.zip ./ code.zip

RUN unzip code.zip && mv $HTML-gh-pages/* . && echo $HTML > ./env.html

CMD apachectl -DFOREGROUND
```

```bash 
docker build -t apache_with_code:v5 .
```

```bash 
docker run -d --name apache -p 9090:80 apache_with_code:v5
```

`localhost:9090`