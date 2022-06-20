```dockerfile
FROM centos:7  
  
RUN yum install httpd -y    
  
ADD https://github.com/mdn/beginner-html-site-styled/archive/refs/heads/gh-pages.zip /va  
r/www/html/code.zip  
  
RUN cd /var/www/html/ && unzip code.zip && mv /var/www/html/beginner-html-site-styled-gh  
-pages/* /var/www/html/  
  
CMD apachectl -DFOREGROUND
```

```bash 
docker build -t apache_with_html:v3 -f Dockerfile3
```

```bash 
docker run -d --name=apache -p 9090:80 apache_with_code:v3
```
