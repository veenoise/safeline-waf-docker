# Safeline WAF Docker Setup

> You can follow this documentation for more information: https://docs.waf.chaitin.com/en/GetStarted/Deploy

## Step-by-step guide

1. Create the base directory:

   ```bash
   sudo mkdir -p /data/safeline
   ```

2. Create a `.env` file and set a strong `POSTGRES_PASSWORD`:

   ```env
   SAFELINE_DIR=/data/safeline
   IMAGE_TAG=latest
   MGT_PORT=9444
   POSTGRES_PASSWORD=your_strong_password_here
   SUBNET_PREFIX=172.30.30
   IMAGE_PREFIX=chaitin
   ARCH_SUFFIX=
   RELEASE=-lts
   REGION=-g
   MGT_PROXY=0
   ```

3. Copy the `docker-compose.yml` file to `/data/safeline`:

   ```bash
   sudo cp docker-compose.yml /data/safeline/
   ```

4. Start the stack:

   ```bash
   docker compose up -d
   ```

5. Access the management console at `https://<your-host>:9444`

## Services

| Container | Description |
|---|---|
| `safeline-pg` | PostgreSQL database |
| `safeline-mgt` | Management API & UI |
| `safeline-detector` | Threat detection engine |
| `safeline-tengine` | Tengine reverse proxy (host network) |
| `safeline-luigi` | Log processing service |
| `safeline-fvm` | Feature version manager |
| `safeline-chaos` | Captcha/challenge service |

## Configuration

| Variable | Default | Description |
|---|---|---|
| `SAFELINE_DIR` | `/data/safeline` | Base directory for persistent data |
| `MGT_PORT` | `9444` | Management console port |
| `POSTGRES_PASSWORD` | *(required)* | PostgreSQL password |
| `SUBNET_PREFIX` | `172.30.30` | Internal Docker network subnet prefix |
| `IMAGE_TAG` | `latest` | Docker image tag |
| `MGT_PROXY` | `0` | The number of console proxy layers |
