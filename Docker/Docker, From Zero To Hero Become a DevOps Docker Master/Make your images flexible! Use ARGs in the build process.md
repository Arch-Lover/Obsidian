
```Dockerfile

FROM centos:7

ARG user=application 

ARG httpd_package

RUN yum install $httpd_package -y

  

LABEL maintainer="Reza"

LABEL vendor="componyB"

LABEL random="yay"

  

ENV HTML beginner-html-site-styled

  

WORKDIR /var/www/html/

  

ADD https://github.com/mdn/$HTML/archive/refs/heads/gh-pages.zip ./ code.zip

  

RUN unzip code.zip && mv $HTML-gh-pages/* . && echo $HTML > ./env.html

  

RUN useradd $user && chown -R $user:$user html

  

USER $user

  

RUN rm -rf code.zip $HTML-gh-pages/

  

USER root

  

CMD apachectl -DFOREGROUND

```

```bash
docker build -t apache_with_code:v9 --build-arg user=toor --build-arg httpd_package=httpd .
```