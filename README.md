# Conduit Docker Compose

A Docker Compose setup for running [Conduit](https://github.com/psiphon-inc/conduit) with Prometheus metrics and Grafana dashboards.

## Features

- **Conduit**: High-performance proxy server with bandwidth management
- **Prometheus**: Metrics collection and time-series database
- **Grafana**: Pre-configured dashboards for monitoring Conduit metrics

## Requirements

- Docker Engine 20.10+ and Docker Compose v2.0+
- Linux server (tested on Ubuntu/Debian)
- Basic familiarity with command line

See the [official Docker installation guide](https://docs.docker.com/engine/install/) for your platform.

## Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/ahmadsalimi/conduit-docker-compose.git
cd conduit-docker-compose
```

### 2. Create Grafana credentials

Create the `secrets/` directory and credential files:

```bash
# Create secrets directory
mkdir -p secrets

# Set admin username (default: admin)
echo -n "admin" > secrets/admin_user

# Set a strong admin password (replace with your own!)
echo -n "your-super-strong-password-here" > secrets/admin_password

# Set restrictive permissions
chmod 600 secrets/admin_user secrets/admin_password
```

**Important**: Use a strong, unique password.

### 3. Start the stack

```bash
docker compose up -d
```

### 4. Access Grafana

Open your browser and navigate to:
```
http://<your-server-ip>:3000
```

Login with:
- **Username**: `admin` (or whatever you set in `secrets/admin_user`)
- **Password**: The password from `secrets/admin_password`

The Conduit dashboard should be automatically provisioned and available.

## Security Best Practices

### Firewall Configuration (UFW)

To secure your server, use UFW to only expose SSH and Grafana:

```bash
# Install UFW (if not already installed)
sudo apt update
sudo apt install ufw

# Deny all incoming by default
sudo ufw default deny incoming
sudo ufw default allow outgoing

# Allow SSH
sudo ufw allow ssh

# Allow Grafana
sudo ufw allow 3000/tcp

# Enable firewall
sudo ufw enable

# Verify status
sudo ufw status
```

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

## Support

For issues related to:
- **This Docker Compose setup**: Open an issue in this repository
- **Conduit itself**: See [Conduit repository](https://github.com/psiphon-inc/conduit)
- **Prometheus**: See [Prometheus documentation](https://prometheus.io/docs/)
- **Grafana**: See [Grafana documentation](https://grafana.com/docs/)
