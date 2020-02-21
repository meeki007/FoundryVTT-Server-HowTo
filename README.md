#proxy for foundryvtt @ port :30000
server {

    	server_name foundryvtt.your_domain_name.com;

    	location = /robots.txt {
    		add_header  Content-Type  text/plain;
    		return 200 "User-agent: *\nDisallow: /\n";
    	}
    	location / {
       		proxy_pass http://127.0.0.1:30000;

		#Defines the HTTP protocol version for proxying
		#by default it it set to 1.0.
		#For Websockets and keepalive connections you need to use the version 1.1    
		proxy_http_version  1.1;

		#Sets conditions under which the response will not be taken from a cache.
		proxy_cache_bypass  $http_upgrade;

		#These header fields are required if your application is using Websockets
		proxy_set_header Upgrade $http_upgrade;

		#These header fields are required if your application is using Websockets    
		proxy_set_header Connection "upgrade";

		#The $host variable in the following order of precedence contains:
		#hostname from the request line, or hostname from the Host request header field
		#or the server name matching a request.    
		proxy_set_header Host $host;

		#Forwards the real visitor remote IP address to the proxied server
		proxy_set_header X-Real-IP $remote_addr;

		#A list containing the IP addresses of every server the client has been proxied through    
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

		#When used inside an HTTPS server block, each HTTP response from the proxied server is rewritten to HTTPS.    
		proxy_set_header X-Forwarded-Proto $scheme;

		#Defines the original host requested by the client.    
		proxy_set_header X-Forwarded-Host $host;

		#Defines the original port requested by the client.    
		proxy_set_header X-Forwarded-Port $server_port;

    	}
	location /setup {
	proxy_pass http://127.0.0.1:30000;

		#Defines the HTTP protocol version for proxying
		#by default it it set to 1.0.
		#For Websockets and keepalive connections you need to use the version 1.1    
		proxy_http_version  1.1;

		#Sets conditions under which the response will not be taken from a cache.
		proxy_cache_bypass  $http_upgrade;

		#These header fields are required if your application is using Websockets
		proxy_set_header Upgrade $http_upgrade;

		#These header fields are required if your application is using Websockets    
		proxy_set_header Connection "upgrade";

		#The $host variable in the following order of precedence contains:
		#hostname from the request line, or hostname from the Host request header field
		#or the server name matching a request.    
		proxy_set_header Host $host;

		#Forwards the real visitor remote IP address to the proxied server
		proxy_set_header X-Real-IP $remote_addr;

		#A list containing the IP addresses of every server the client has been proxied through    
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

		#When used inside an HTTPS server block, each HTTP response from the proxied server is rewritten to HTTPS.    
		proxy_set_header X-Forwarded-Proto $scheme;

		#Defines the original host requested by the client.    
		proxy_set_header X-Forwarded-Host $host;

		#Defines the original port requested by the client.    
		proxy_set_header X-Forwarded-Port $server_port;



		auth_basic           "Private Area";
		auth_basic_user_file /home/YourChosenNameHere/foundryvtt_server/htpasswd/.htpasswd;
	}

    listen [::]:443 ssl; # managed by Certbot
    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/foundryvtt.your_domain_name.com/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/foundryvtt.your_domain_name.com/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

}

server {
    if ($host = foundryvtt.your_domain_name.com) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


    	listen 80;
	listen [::]:80;

    	server_name foundryvtt.your_domain_name.com;
    return 404; # managed by Certbot


}
