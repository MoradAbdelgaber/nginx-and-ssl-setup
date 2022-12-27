# nginx-and-ssl-setup
setup nginx to deploy your node app with domain instead of server ip and port . also , generate ssl for your domain 


# Create nginx configuration file for your domain.
 1- type in terminal this command and remember to replace "your_domain" with your domain like "mawjood.appsiraq.com"
 ```
        $ sudo nano /etc/nginx/conf.d/mawjood.appsiraq.com.conf
        ```

    2- copy and paste this snippet and remember to replace "your_domain" with your own and port "3001"
        server {
            listen 80;
            listen [::]:80;

            index index.html index.htm index.nginx-debian.html;

            server_name your_domain;

            location / {
                    proxy_pass http://localhost:3001; #whatever port your app runs on
                    proxy_http_version 1.1;
                    proxy_set_header Upgrade $http_upgrade;
                    proxy_set_header Connection 'upgrade';
                    proxy_set_header Host $host;
                    proxy_cache_bypass $http_upgrade;
            }
        }

    3- press ctrl+x to exit then y  to accept edit  then Enter to create file.

    4- To make sure that there are no syntax errors in any of your Nginx files, run:
        $ sudo nginx -t
    
    5- restart Nginx to enable your changes
        $ sudo systemctl restart nginx

# Generate SSL for your domain 
    1- type in terminal this command and remember to replace "your_domain" with your own
        $ sudo certbot --nginx -d your_domain
    

