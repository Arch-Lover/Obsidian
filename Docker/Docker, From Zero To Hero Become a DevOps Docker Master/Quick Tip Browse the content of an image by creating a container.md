```Dockerfile
FROM centos:7

  

RUN yum install httpd -y

  

LABEL maintainer="Reza"

LABEL vendor="componyB"

LABEL random="yay"

  

ENV HTML beginner-html-site-styled

  

WORKDIR /var/www/html/

  

ADD https://github.com/mdn/$HTML/archive/refs/heads/gh-pages.zip ./ code.zip

  

RUN unzip code.zip && mv $HTML-gh-pages/* . && echo $HTML > ./env.html

  

CMD apachectl -DFOREGROUND
```

```bash
docker exec -ti centos:v7 bash
```

```bash 
echo $HTML

beginner-html-site-styled
```

```bash 
pwd 

/var/www/html/
```

---

```Dockerfile

FROM centos:7

  

RUN yum install httpd -y

  

LABEL maintainer="Reza"

LABEL vendor="componyB"

LABEL random="yay"

  

ENV HTML beginner-html-site-styled

  

WORKDIR /var/www/html/

  

ADD https://github.com/mdn/$HTML/archive/refs/heads/gh-pages.zip ./ code.zip

  

RUN unzip code.zip && mv $HTML-gh-pages/* . && echo $HTML > ./env.html

  

RUN useradd application && chown -R application:application html

  

USER application

  

RUN rm -rf code.zip $HTML-gh-pages/

  

USER root

  

CMD apachectl -DFOREGROUND

```
