# Makefile homarr deployment
server = 192.168.2.4 # IP address of the target server
project_path = $(shell basename $(shell pwd))

init-server:
	ssh $(server) "mkdir -p ~/deployments/homarr"

rsync: init-server
	rsync -azv . $(server):deployments/homarr/

# First execution: secure networks and containers
setup: rsync
	ssh $(server) "cd ~/deployments/homarr && \
		docker network create cloudflared || true && \
		docker compose up -d"

# Updates containers without dropping the network
deploy: rsync
	ssh $(server) "cd ~/deployments/homarr && docker compose up -d --build"