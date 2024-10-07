Here is the updated document with the necessary Nginx commands and a reference to the tutorial for configuring Nginx:

---

# Nginx Configuration and Commands
(remmember use conf.d when host any backend and use sites-available when host any frontend)
## Overview
This document provides essential commands for managing the Nginx web server. For a detailed guide on installing and configuring Nginx, refer to the [DigitalOcean Nginx Installation Guide](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04).

## Basic Nginx Commands

1. **Check Nginx Status:**
   - To check the status of the Nginx service:
     ```
     sudo systemctl status nginx
     ```

2. **Start Nginx:**
   - To start the Nginx service:
     ```
     sudo systemctl start nginx
     ```

3. **Stop Nginx:**
   - To stop the Nginx service:
     ```
     sudo systemctl stop nginx
     ```

4. **Restart Nginx:**
   - To restart the Nginx service (useful after making configuration changes):
     ```
     sudo systemctl restart nginx
     ```

5. **Reload Nginx:**
   - To reload Nginx without interrupting existing connections (useful for applying changes to the configuration):
     ```
     sudo systemctl reload nginx
     ```

6. **Enable Nginx on Boot:**
   - To enable the Nginx service to start on system boot:
     ```
     sudo systemctl enable nginx
     ```

7. **Disable Nginx on Boot:**
   - To disable the Nginx service from starting on system boot:
     ```
     sudo systemctl disable nginx
     ```

8. **Test Nginx Configuration:**
   - To test the Nginx configuration for syntax errors:
     ```
     sudo nginx -t
     ```

9. **View Nginx Logs:**
   - To view Nginx access logs:
     ```
     sudo tail -f /var/log/nginx/access.log
     ```
   - To view Nginx error logs:
     ```
     sudo tail -f /var/log/nginx/error.log
     ```




#### Configure nginx with backend:
1. create a file called api.conf in conf.d folder

then go to the files using editor like nano api.conf 
then write a config ex:
```javascript
server{
    listen 80;
    server_name wach.quest;//use here your domain name to reverse the port
    location / {
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $host;
        proxy_pass http://127.0.0.1:3000;//use here backend host and port
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        # location /overview {
        #     proxy_pass http://127.0.0.1:3000$request_uri;
        #     proxy_redirect off;
        # }
    }
}
```


## INSTALL AND CONFIGURE PM2

follow their documentation to install and configure pm2 as well:https://pm2.keymetrics.io/