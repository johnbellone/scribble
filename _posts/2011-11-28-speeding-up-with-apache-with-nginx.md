---
layout: post
title: Speeding Up With Apache With Nginx

tags: Apache,Internet,Lamp,Nginx,Performance Tuning,Technology,Wordpress
---
<p>For the past year or so I have been using <a href="http://nginx.org/">nginx</a> as a proxy in front of my <a href="http://httpd.apache.org/docs/2.0/">Apache</a> instances on the server that runs this blog, and a few other websites that I manage. The virtual machine itself is running an older LTS version of <a href="https://wiki.ubuntu.com/LTS">Ubuntu</a>, and most of the applications on here are a traditional <a href="http://en.wikipedia.org/wiki/LAMP_(software_bundle)">LAMP setup</a> with a few C/C++ testing tools scattered around. For the most part it is operating as web server with a small work load. But as I've been adding a few more services running in the background I have noticed a little slowdown with <a href="http://wordpress.org">Wordpress</a>.</p>
<p>There are some obvious advantages to this set up: Nginx can serve up all of the static content very, very quickly without having to send it down to the Apache instances to process. This frees up those daemons to only serve application logic, which in this case is the Wordpress PHP application, but would work for nearly anything that you have set up with it. I will give you a quick example of the configuration that I have set up for this site.</p>
<p>This is the main configuration file for the Nginx application. Most of the commands here I have plucked from various tutorials across the internet, specifically dealing with the gzip settings, and as you can see there are a few connection and process related settings. These can all be tweaked at your desire, but I find that they work best on my low load cloud virtual server. The information to note here is the location of the proxy server (127.0.0.1:8080) that the requests will be sent to, as well as some folders for errors, logs, etc. These are all standard with the Nginx installation from aptitude and should be modified to suite you. Note the section where we include any scripts that are in /etc/nginx/sites-enabled/* which is similar to the set up of the Apache portion of the LAMP stack.</p>
<p><strong>/etc/nginx/nginx.conf</strong>
<pre lang="xorg_conf">user  op;
worker_processes  2;

error_log  logs/error.log warn;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

pid        logs/nginx.pid;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  logs/access.log  main;

    gzip on;
    gzip_http_version 1.0;
    gzip_comp_level 2;
    gzip_min_length 1100;
    gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript;
    gzip_buffers 16 8k;
    gzip_disable "MSIE [1-6].(?!.*SV1)";
    gzip_vary on;

    include /etc/nginx/sites-enabled/*;

    server {
        listen       80 default;
        access_log  logs/host.access.log  main;

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        location / {
                 include /etc/nginx/proxy.conf;
                 proxy_pass http://127.0.0.1:8080;
        }
    }
}</pre></p>
<p>This configuration file sets up the particular domain inside of the Nginx proxy. It covers both the fully qualified domain name and the alias, and provides the root directory for serving up the static content. If there is content that you do not want to be served up (e.g. you have a public folder) make sure to point this only to your assets directory. We set up the path for logs to be written to (you'll have to <em>mkdir -p</em> those directories) as well. The real gem here is the regular expression that specifies what static content will not get fielded off to the apache daemons. Obviously you can make any corrections here that you see fit. When you are done set up a symbolic link in /etc/nginx/sites-enabled/<site>.</p>
<p><strong>/etc/nginx/sites-available/thoughtlessbanter.com</strong>
<pre lang="xorg_conf">server {
 server_name www.thoughtlessbanter.com thoughtlessbanter.com;
 root /path/to/thoughtlessbanter.com/;

 access_log /var/log/nginx/thoughtlessbanter.com/access.log;
 error_log /var/log/nginx/thoughtlessbanter.com/error.log warn;

 location ~* ^.+.(jpg|jpeg|gif|png|ico|css|zip|tgz|gz|rar|bz2|doc|xls|exe|pdf|ppt|txt|tar|mid|midi|wav|bmp|rtf|js)$ {
              access_log off;
              expires 30d;
 }

 location / {
              include /etc/nginx/proxy.conf;
              proxy_pass http://127.0.0.1:8080;
 }
}</pre></p>
<p>This little tidbit is necessary to send over the header information from the HTTP client to the Apache daemon. These proxy settings, with this configuration set up, will affect <em>every single web request</em>, so be careful with what you modify here. There are additional parameters involving the maximum size of a payload, send, connect, and read timeouts, etc. These can all be looked up with <a href="http://wiki.nginx.org/HttpProxyModule">a quick Google search</a> and modified freely.</p>
<p><strong>/etc/nginx/proxy.conf</strong></p>
<pre lang="xorg_conf">proxy_set_header Host $host;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;</pre></p>
<p>Last you'll need to modify your virtual host for all of the websites to now accept the connection on the new port, 8080, which is were Nginx will proxy the requests to. Be sure to set the server alias for both the fully qualified domain, and the shortened one. I am not an Apache configuration guru here, so some of the other options may not be applicable, but they seem to do the job for me. Most of my domains are further configured appropriately in the .htaccess in the document root directory.</p>
<p><strong>/etc/apache2/sites-available/thoughtlessbanter.com</strong>
<pre lang="xml"><VirtualHost *:8080>
              ServerAdmin jb@thunkbrightly.com
              ServerName thoughtlessbanter.com
              ServerAlias www.thoughtlessbanter.com
              DocumentRoot /path/to/thoughtlessbanter.com
              <Directory />
               Options FollowSymLinks
               AllowOverride All
              </Directory>
              <Directory /path/to/thoughtlessbanter.com>
               Options Indexes FollowSymLinks MultiViews
               AllowOverride All
               Order allow,deny
               allow from all
              </Directory>

              ErrorLog /var/log/apache2/thoughtlessbanter.com-error.log
              CustomLog /var/log/apache2/access.log combined
</VirtualHost></pre></p>
<p>When you have made all of the changes feel free to restart the services and test your website. Once all the instances are bounced you should be able to point the browser to the location and still bring up your website. If you check the logs located in /var/log/nginx/<site> and /var/log/apache2/<site>.log you should be able to see your static content requests hitting nginx, and being served up right from there. The apache daemons will now only serve the application logic.</p>
<p>Let me know what you think. I'm sure I've made a few mistakes.</p>
