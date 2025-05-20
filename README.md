# 🐳 Docker Installer for Ubuntu with Custom Nexus Registry

This script installs **Docker CE** on Ubuntu using a **custom Nexus APT repository** and configures Docker to use a local **Nexus Docker registry** and custom **data-root**.

---

## 📦 What This Script Does

✅ Installs Docker CE using a custom APT repo  
✅ Configures Docker to:

- Use `/data/docker` as its data directory
- Use a local insecure registry (`http://nexusoss-ip:8082`)
- Use a registry mirror (`http://nexusoss-ip:8082`)

✅ Sets proper permissions  
✅ Reloads and restarts Docker

---

## ⚙️ Requirements

- Ubuntu (22.04+ recommended)
- `sudo` or root access
- A Nexus server hosting:
  - APT Docker proxy at: `http://nexusoss-ip:8081/repository/apt-docker-repo-24.04/`
  - Docker registry at: `http://nexusoss-ip:8082`

---

## 🚀 Installation

1. Clone this repo:

```bash
git clone https://github.com/amirhosseinghorbanii/docker-nexus-installer.git
cd docker-nexus-installer
```

2. Make the script executable:

```bash
chmod +x install-docker.sh
```

3. Run the script:

```bash
sudo ./install-docker.sh
```

---

## 🛠 Configuration File

**`/etc/docker/daemon.json`**:

```json
{
  "data-root": "/data/docker",
  "insecure-registries": ["http://nexusoss-ip:8082"],
  "registry-mirrors": ["http://nexusoss-ip:8082"]
}
```

---

## 📁 Created Directories & Files

| Path                             | Purpose                          |
|----------------------------------|----------------------------------|
| `/data/docker`                   | Docker's custom data directory   |
| `/etc/docker/daemon.json`        | Custom Docker config             |
| `/etc/apt/keyrings/docker.asc`   | GPG key for APT Docker repo      |
| `/etc/apt/sources.list.d/docker.list` | Docker APT source list     |

---

## ❗ Troubleshooting

- Make sure the Nexus IP/hostname is reachable.
- Use `ip` instead of `nexusoss-ip` if DNS is unavailable.
- Ensure Nexus proxy repositories are correctly configured.
