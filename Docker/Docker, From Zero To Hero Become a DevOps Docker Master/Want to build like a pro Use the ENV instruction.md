```Dockerfile
FROM centos:7

RUN yum install httpd -y  

ENV HTML beginner-html-site-styled <-----

ADD https://github.com/mdn/$HTML/archive/refs/heads/gh-pages.zip /var/www/html/code.zip

RUN cd /var/www/html/ && unzip code.zip && mv /var/www/html/$HTML-gh-pages/* /var/www/html/

CMD apachectl -DFOREGROUND
```

```bash 
docker build -t apache_with_html:v4 .
```

```bash
docker run -d --name apache -p 9090:80 apache_with_code:v4
```

`localhost:9090`