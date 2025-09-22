# Makefile portainer deployment
server = 192.168.2.4 # IP address of the target server
project_path = $(shell basename $(shell pwd))

init-server:
	ssh $(server) "mkdir -p ~/deployments/portainer"

rsync: init-server
	rsync -azv . $(server):deployments/portainer/

# First execution: secure networks and containers
setup: rsync
	ssh $(server) "cd ~/deployments/portainer && \
		docker network create cloudflared || true && \
		docker compose up -d"

# Updates containers without dropping the network
deploy: rsync
	ssh $(server) "cd ~/deployments/portainer && docker compose up -d --build"