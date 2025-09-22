# Makefile affine deployment
server = 192.168.2.4 # IP address of the target server
project_path = $(shell basename $(shell pwd))

init-server:
	ssh $(server) "mkdir -p ~/deployments/affine"

rsync: init-server
	rsync -azv . $(server):deployments/affine/

# First execution: secure networks and containers
setup: rsync
	ssh $(server) "cd ~/deployments/affine && \
		docker network create cloudflared || true && \
		docker compose up -d"

# Updates containers without dropping the network
deploy: rsync
	ssh $(server) "cd ~/deployments/affine && docker compose up -d --build"