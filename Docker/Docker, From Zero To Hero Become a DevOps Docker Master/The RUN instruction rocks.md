```dockerfile
FROM centos:7  
  
RUN yum install httpd -y    
  
COPY html-code /var/www/html  
  
CMD apachectl -DFOREGROUND
```

```bash
docker build -t apache_with_code:v1 .
```

```bash
docker run -d -p 9191:80  apache_with_code:v1
```

