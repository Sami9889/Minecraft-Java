# Minecraft-Java

This repository runs a temporary Paper Minecraft Java server from GitHub Actions.
It installs Geyser and Floodgate so Bedrock clients can connect when the tunnel
configuration supports the required protocol.

## Setup

1. In the repository settings, add an Actions secret named
	`CLOUDFLARE_TUNNEL_TOKEN` containing the Cloudflare tunnel token.
2. In **Actions**, run **Minecraft Java server** with **Run workflow**.
3. Configure the Cloudflare tunnel ingress to forward TCP Minecraft traffic to
	`localhost:25565` (or the equivalent service address available to the tunnel).

The workflow uses Paper `1.21.8` and Java 21. The GitHub-hosted runner is
temporary, so the world is discarded when the job ends. Cloudflare Tunnel
normally provides TCP connectivity for Java Edition; Bedrock clients also need
the tunnel to support UDP forwarding to Geyser's default port `19132`.

Never commit the tunnel token. If the token from a chat or log has been exposed,
rotate it in Cloudflare and store only the replacement as the GitHub secret.