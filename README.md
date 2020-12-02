### nginx-load-js

#### Commands (for instance : ubuntu os)
- first update your os's packages : `sudo apt update`
- install nginx on your server : `sudo apt install nginx`
- enable nginx service : `sudo systemctl enable nginx`
- start nginx service : `sudo systemctl start nginx`
- put your js file into a directory for example : `/home/arsalan/jstest/index.html`
- try this command : `sudo nano /etc/nginx/sites-available/test.conf` (like test.conf that I put it down for you)
- for save above file and exit the nano editor : press---> `ctrl+o` , `ctrl+m` , `ctrl+x`
- after that you should add this test.conf to your sites-enable nginx directory , so try this command : 
      `sudo ln -s /etc/nginx/sites-available/test.conf /etc/nginx/sites-enabled/`
- after all you should restart the nginx : `sudo systemctl restart nginx`
- finally , if you put `yourdomain.com` in your browser , you can see the js or html will apear.



#### Sample for test.conf
``` js
server {

    root /home/arsalan/jstest;
    index index.php index.html index.htm;
    server_name yourdomain.com;
    client_max_body_size 400M;
    autoindex off;


    location ~* \.(css|gif|ico|jpeg|jpg|js|png)$ {
        expires max;
        log_not_found off;
    }

    location / {
        try_files $uri $uri/ /index.php$is_args$args;
    }

    location ~ \.php$ {
         include snippets/fastcgi-php.conf;
         fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
         fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
         include fastcgi_params;
  }



}

```
