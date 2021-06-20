First of all create a file in `/etc/nginx/sites-available/domain`

Into this file add this lines : 
```sh
server {
    listen 80;
    server_name www.my-website.com;
   
    location / {
    	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Real-IP $remote_addr;
    	proxy_set_header Host $http_host;
        
    	proxy_http_version 1.1;
    	proxy_set_header Upgrade $http_upgrade;
    	proxy_set_header Connection "upgrade";
        
    	proxy_pass http://127.0.0.1:port/;
    	proxy_redirect off;
    	proxy_read_timeout 240s;
    }
}
```
Then save the file.
After that run this commands:
```sh
sudo ln -s /etc/nginx/sites-available/dominio /etc/nginx/sites-enabled/dominio
```
```sh
sudo service nginx restart
```
Then go to your domain settings and add the domain | subdomain to the vps's public ip.
