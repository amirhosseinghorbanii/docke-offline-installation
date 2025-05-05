#🚀 Docker Offline Installation Script (Ubuntu)
This script installs Docker CE on Ubuntu systems using a custom APT repository and configures the Docker daemon with custom storage and registry settings.

📋 Features
Adds Docker GPG key (hardcoded in the script).

Adds a custom APT repository (pointing to a Nexus proxy repo).

Configures Docker daemon to:

Use /data/docker as its data root.

Use an insecure local registry (http://nexusoss-ip:8082).

Creates necessary directories and permissions.

⚠️ Requirements
Ubuntu-based system.

Root privileges or sudo access.

The nexusoss-ip must be resolvable and accessible for:

APT Docker repo at http://nexusoss-ip:8081/repository/apt-docker-repo-24.04/

Docker image registry at http://nexusoss-ip:8082

📦 Packages Installed
docker-ce

docker-ce-cli

containerd.io

docker-buildx-plugin

docker-compose-plugin

🛠️ Usage
Make the script executable:

chmod +x install-docker.sh
Run the script:

sudo ./install-docker.sh
📁 Files Created
/etc/apt/keyrings/docker.asc: GPG key for Docker repo.

/etc/apt/sources.list.d/docker.list: APT source for Docker.

/etc/docker/daemon.json: Custom Docker daemon config.

/data/docker: Custom Docker data directory.

✅ Example Configuration in daemon.json
{
  "data-root": "/data/docker",
  "insecure-registries": ["http://nexusoss-ip:8082"],
  "registry-mirrors": ["http://nexusoss-ip:8082"]
}
🧯 Troubleshooting
If installation fails, ensure:

The Nexus proxy URLs are correct and accessible.

You’re using the correct Ubuntu codename (e.g. jammy, focal, etc.).

DNS can resolve nexusoss-ip or use the actual IP address.

📌 Notes
The script uses a hardcoded GPG key—ensure it is up to date and valid.

You can replace nexusoss-ip with your actual Nexus IP or hostname.

Make sure your Nexus is correctly configured to serve the necessary APT and Docker registry endpoints.

