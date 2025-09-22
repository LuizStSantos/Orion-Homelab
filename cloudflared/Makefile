# Makefile cloudflared deployment
server = 192.168.2.4 # IP address of the target server
project_path = $(shell basename $(shell pwd))

init-server:
	ssh $(server) "mkdir -p ~/deployments/cloudflared"

rsync: init-server
	rsync -azv . $(server):deployments/cloudflared/

# First execution: secure networks and containers
setup: rsync
	ssh $(server) "cd ~/deployments/cloudflared && \
		docker network create cloudflared || true && \
		docker compose up -d"

# Updates containers without dropping the network
deploy: rsync
	ssh $(server) "cd ~/deployments/cloudflared && docker compose up -d --build"