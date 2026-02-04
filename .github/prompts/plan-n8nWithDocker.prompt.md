# Plan: Run n8n with Docker

Set up and run n8n, a workflow automation tool, using Docker for easy deployment and isolation. This involves pulling the official image, configuring environment variables, and mounting volumes for data persistence, ensuring a secure and scalable setup based on official docs.

## Steps

1. Install Docker if not present, using `apt install docker.io` on Ubuntu.
2. Create a persistent volume with `docker volume create n8n_data`.
3. Run n8n container using `docker run -it --rm --name n8n -p 5678:5678 -e GENERIC_TIMEZONE="America/New_York" -e TZ="America/New_York" -e N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true -e N8N_RUNNERS_ENABLED=true -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n`.
4. Access n8n at `http://localhost:5678` in a browser.
5. For production, switch to PostgreSQL by adding DB env vars and using Docker Compose from [n8n-hosting repo](https://github.com/n8n-io/n8n-hosting).

## Further Considerations

1. Customize timezone in env vars to match your location.
2. For advanced setups, create a `docker-compose.yml` with full config.
3. Ensure Docker is running and ports are available; stop with `docker stop n8n`.

## Key Environment Variables

- `GENERIC_TIMEZONE`: Sets timezone for schedule-oriented nodes
- `TZ`: Sets system timezone
- `N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true`: Enforces secure file permissions
- `N8N_RUNNERS_ENABLED=true`: Enables task runners for better performance

## Docker Volumes

- `n8n_data:/home/node/.n8n` – Stores workflows, credentials (encrypted), executions, logs, and encryption keys. Essential for data persistence.

## Ports

- Default: 5678 (customize with `-p 8080:5678` if needed)

## References

- [n8n Docker Installation Guide](https://docs.n8n.io/hosting/installation/docker/)
- [Environment Variables Reference](https://docs.n8n.io/hosting/configuration/environment-variables/)
- [n8n-Hosting Examples](https://github.com/n8n-io/n8n-hosting)
