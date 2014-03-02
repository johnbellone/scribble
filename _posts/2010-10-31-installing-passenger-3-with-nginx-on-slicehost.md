---
layout: post
title: Installing Passenger 3 with Nginx on Slicehost

tags: Pennies For Thought,Programming
---
After a long week of tinkering and testing I have finally made the "early access" sign ups for <a href="http://typealoud.com">Type Aloud</a> available to the public. Most of this week has been spent fixing some issues with the Ruby Bundler, Nginx and of course Passenger 3. Up until this point I did not make the Type Aloud code available for testing on production and have done most of my development locally. This posed some issues for testing OAuth2 authentication with Facebook, Twitter and other end points, but generally I assumed that it would work as expected. I was ever so slightly wrong. 

Passenger itself was quite easy to install. I <a href="http://www.modrails.com/">downloaded it from the website</a> and merely followed the instructions, which downloads nginx and compiles the Passenger module into the nginx executable. This is due to Nginx not supporting loadable modules like Apache, but on my meager <a href="http://www.slicehost.com">Slice Host</a> server this went pretty quick. Within an hour I had a Passenger and Nginx installation up and running. My configuration is a little different than most people: on this particular slice I am running two Rails Rack applications (<a href="http://typealoud.com">typealoud.com</a> and <a href="http://thunkbrightly.com">thunkbrightly.com</a>) and this <a href="http://thoughtlessbanter.com">Wordpress blog</a> which is using the <a href="http://www.fastcgi.com/drupal/node/5?q=node/10">php-fastcgi</a> plugin through Nginx. 

The last thing that I did was download <a href="http://www.rubyenterpriseedition.com/">Ruby Enterprise Edition</a> which is by the same great cats over at <a href="http://www.phusion.nl/about.html">Phusion</a>. This version of Ruby is designed specially to minimize the memory footprint and speed up (as much as possible) the execution. There are some nifty graphs over there on the <a href="http://www.rubyenterpriseedition.com/">website</a> so I am not going to gush over any of their stats. The point being: since I am broke and using shared hosting this is the absolute best. The installation went quick and easy. 

I install all of my third-party applications into the mounted <em>/opt</em> (optional) directory. This is where Passenger is installed. When it comes to Ruby I decided to install this into the <em>/usr/local</em> because I have several scripts that I wrote which expects this to be in the $PATH environment variable. Because the hardest part of this process was figuring out to correctly configure Passenger 3 for Nginx I am going to post my configuration for my Rails (and php-fastcgi) applications. I hope that this helps some of you. 

<pre lang="sh">user  op;
worker_processes  2;

error_log  logs/error.log warn;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

pid        logs/nginx.pid;

events {
    worker_connections  1024;
}

http {
    passenger_root /opt/passenger-3.0.0;
    passenger_ruby /usr/local/bin/ruby;
    passenger_max_pool_size 10;

    include       mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    gzip  on;
    gzip_http_version 1.0;
    gzip_vary on;
    gzip_comp_level 6;
    gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript;
    gzip_buffers 16 8k;

    include /etc/nginx/sites-enabled/*;

    server {
        listen       80;
        server_name  localhost;

        #charset koi8-r;

        access_log  logs/host.access.log  main;

        location / {
            root   html;
            index  index.html index.htm;
        }
     }
}</pre>

<strong>sites-available/typealoud.com</strong>
<pre lang="sh">server {
 listen 80;
 server_name www.typealoud.com;
 rewrite ^/(.*) http://typealoud.com/$1 permanent;
}

server {
 listen 80;
 server_name typealoud.com;
 access_log /var/log/nginx/typealoud.com/access.log;
 error_log /var/log/nginx/typealoud.com/error.log warn;

 location / {
  root /var/www/typealoud.com/public;
  passenger_enabled on;
  rack_env production;
  rails_spawn_method smart;
  index index.htm index.html;
 }
}</pre>

<strong>sites-available/thoughtlessbanter.com</strong>
<pre lang="sh">server {
 listen 80;
 server_name www.thoughtlessbanter.com;
 rewrite ^/(.*) http://thoughtlessbanter.com/$1 permanent;
}

server {
 listen 80;
 server_name thoughtlessbanter.com;
 access_log /var/log/nginx/thoughtlessbanter.com/access.log;
 error_log /var/log/nginx/thoughtlessbanter.com/error.log warn;

 location / {
   root /var/www/thoughtlessbanter.com;
   index index.php index.html index.htm;

   if (-f $request_filename) {
    expires 30d;
    break;
   }

   if (!-e $request_filename) {
    rewrite ^(.+)$ /index.php?q=$1 last;
   }
 }

 location ~ \.php {
  include /etc/nginx/fastcgi_params;
  keepalive_timeout 30;
  proxy_read_timeout 60;
  proxy_connect_timeout 60;

  fastcgi_pass 127.0.0.1:9000;
  fastcgi_index index.php;

  fastcgi_param PATH_INFO "";
  fastcgi_param SCRIPT_FILENAME /var/www/thoughtlessbanter.com/$fastcgi_script_name;

  fastcgi_param  QUERY_STRING       $query_string;
  fastcgi_param  REQUEST_METHOD     $request_method;
  fastcgi_param  CONTENT_TYPE       $content_type;
  fastcgi_param  CONTENT_LENGTH     $content_length;
   if (!-e $request_filename) {
    rewrite ^(.+)$ /index.php?q=$1 last;
   }
 }

 location ~ \.php {
  include /etc/nginx/fastcgi_params;
  keepalive_timeout 30;
  proxy_read_timeout 60;
  proxy_connect_timeout 60;

  fastcgi_pass 127.0.0.1:9000;
  fastcgi_index index.php;

  fastcgi_param PATH_INFO "";
  fastcgi_param SCRIPT_FILENAME /var/www/thoughtlessbanter.com/$fastcgi_script_name;

  fastcgi_param  QUERY_STRING       $query_string;
  fastcgi_param  REQUEST_METHOD     $request_method;
  fastcgi_param  CONTENT_TYPE       $content_type;
  fastcgi_param  CONTENT_LENGTH     $content_length;

  fastcgi_param  SCRIPT_NAME        $fastcgi_script_name;
  fastcgi_param  REQUEST_URI        $request_uri;
  fastcgi_param  DOCUMENT_URI       $document_uri;
  fastcgi_param  DOCUMENT_ROOT      $document_root;
  fastcgi_param  SERVER_PROTOCOL    $server_protocol;

  fastcgi_param  GATEWAY_INTERFACE  CGI/1.1;
  fastcgi_param  SERVER_SOFTWARE    nginx/$nginx_version;

  fastcgi_param  REMOTE_ADDR        $remote_addr;
  fastcgi_param  REMOTE_PORT        $remote_port;
  fastcgi_param  SERVER_ADDR        $server_addr;
  fastcgi_param  SERVER_PORT        $server_port;
  fastcgi_param  SERVER_NAME        $server_name;

  fastcgi_param  REDIRECT_STATUS    200;

  fastcgi_read_timeout 60;
 }
}</pre>
       



