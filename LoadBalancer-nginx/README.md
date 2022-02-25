# Create a NGINX Loadbalancer using docker

- This will be updated later to include Rancher information



		a. Create nginx.conf file (/etc/nginx/nginx.conf)
			worker_processes 4;
			worker_rlimit_nofile 40000;
			
			events {
			    worker_connections 8192;
			}
			
			stream {
			    upstream rancher_servers_http {
			        least_conn;
			        server <IP_NODE_1>:80 max_fails=3 fail_timeout=5s;
			        server <IP_NODE_2>:80 max_fails=3 fail_timeout=5s;
			        server <IP_NODE_3>:80 max_fails=3 fail_timeout=5s;
			    }
			    server {
			        listen 80;
			        proxy_pass rancher_servers_http;
			    }
			
			    upstream rancher_servers_https {
			        least_conn;
			        server <IP_NODE_1>:443 max_fails=3 fail_timeout=5s;
			        server <IP_NODE_2>:443 max_fails=3 fail_timeout=5s;
			        server <IP_NODE_3>:443 max_fails=3 fail_timeout=5s;
			    }
			    server {
			        listen     443;
			        proxy_pass rancher_servers_https;
			    }
			
			}