# 🛰️ Orion Homelab

The Orion Homelab is my self-hosted environment designed for experimenting, learning, and managing services with full automation.
Everything runs containerized via Docker Compose, and deployments are handled through Makefiles for a clean and repeatable workflow.

This setup focuses on:

- 🚀 Automation → Easy setup and updates with Make.

- 🛡️ Security → Remote access only via Cloudflare Tunnel (no exposed ports).

- 🧩 Modularity → Each service is isolated and can be deployed independently.

- 📊 Visibility → Dashboards (Homarr + custom Dash) keep everything in one place.

- ⚡ Management → Portainer for direct container m- onitoring and control.

The goal of Orion is to provide a scalable and secure lab environment for daily use, testing, and self-hosting experiments — fully under my control.
#
📂 Project Structure

    ORION/
    ├── affine/              # Affine (collaboration / knowledge management)
    │   ├── AFFINE.md
    │   ├── docker-compose.yml
    │   └── Makefile
    │
    ├── cloudflared/         # Cloudflare Tunnel configuration
    │   ├── Cloudflared.md
    │   ├── docker-compose.yml
    │   └── Makefile
    │
    ├── dash./               # Dashboard service
    │   ├── docker-compose.yml
    │   └── Makefile
    │
    ├── homarr/              # Homarr (self-hosted dashboard)
    │   ├── Homarr.md
    │   ├── docker-compose.yml
    │   └── Makefile
    │
    ├── portainer/           # Portainer (container management UI)
    │   ├── docker-compose.yml
    │   └── Makefile
    │
    └── .gitignore
#
⚙️ Services

-   Affine → Open-source workspace for collaboration and note-taking.
-   Cloudflared → Cloudflare Tunnel for secure remote access without
    exposing ports.
-   Dash → Custom dashboard (service overview).
-   Homarr → Self-hosted modern dashboard for all services and links.
-   Portainer → Web UI for managing Docker containers, volumes, and
    networks.
#
⚠️ Important Notice Before Deployment

Before running make setup or make deploy, you must edit the Makefile of
the service you want to deploy and update the server IP:

    # Example: change this line
    server = 192.168.2.4 # IP address of the target server

Replace it with the IP address of your target server.
#
🔑 Environment Variables

- Some services require a .env file before deploying.
- Edit with your own secrets, tokens, and ports.
#
🚀 Deployment Workflow

Each service includes a Makefile that simplifies deployment.

🔹 First setup

Creates secure networks and starts containers for the first time:

    make setup

This step will:
- Create the cloudflared Docker network (if it doesn’t exist).
- Start containers in detached mode.

🔹 Deploy (update)

Updates containers without dropping the network:

    make deploy

👉 This rebuilds and updates containers while keeping networks and
volumes intact.

#
🌐 Access

-   Services exposed locally (check each docker-compose.yml for ports).
-   Remote access handled via Cloudflare Tunnel.
#
🛠️ Requirements

-   Docker
-   Docker Compose
-   Make
#
📌 Notes

-   All services are modular — you can deploy only the ones you need.
-   Cloudflare Tunnel is used because ISP blocks standard ports
    (80/443).