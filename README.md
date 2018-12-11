# dog_project
A project for the recognition of dog pose. For the first version, we use the sensors-network based on Zigbee, which is weared on the dog from a vest, and also equip a helmet with a sigle camera, which can transmit live video to police staff. All of these communicate with the back-end server through 4G.

For a video demo, please visit the following link in detail

https://www.bilibili.com/video/av34108348?share_medium=android&share_source=copy_link&bbid=452131F3-C84D-4DF0-89AF-AA0107CE68FF16810infoc&ts=1539869227641

# essential softwares
## nginx

this server for live video from dog helmet

    wget http://nginx.org/download/nginx-1.9.3.tar.gz
    tar zxvf nginx-1.9.3.tar.gz
    cd nginx-1.9.3/
    ./configure --prefix=/var/www --sbin-path=/usr/sbin/nginx --conf-path=/etc/nginx/nginx.conf --pid-path=/var/run/nginx.pid --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-http_ssl_module --without-http_proxy_module --add-module=/home/pi/nginx_src/nginx-rtmp-module
    make
    sudo make install
use this nginx.conf file to replace the default conf file in /etc/nginx/
    
    sudo service nginx start


## lighttpd
this server for the visualization of dog pose, it has a special featur that it support for python3

place all the files of html in the /var/www/html.

## mysql
please install mysql, and set its account and password are root, 123 respectively.

## live video on raspi
see https://blog.gtwang.org/iot/raspberry-pi-nginx-rtmp-server-live-streaming/   for detail

# run
now, first run server.py

    ./dogs_server_blackant.py

## start system by self when machine running
if you want to run automatically this system, please add those commands in your rc.local file(/etc/rc.local), 

    /usr/bin/python3 /home/blackant/Documents/dogs_server_blackant.py &
    /etc/init.d/nginx start

# Supplements

## dogs_client_raspberry_test.py 
used as a tool for feature testing

## System Architecture
sensor data(raspberry_client.py) -> server (raspberry_server.py) -> user
