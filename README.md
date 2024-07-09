# Obfuscated SSH Service

This project sets up an SSH service with obfuscated SSH support. It uses Docker to containerize the service and provides an example of how to connect using a client with SSH obfuscation.

## Getting Started

### Prerequisites

- Docker and Docker Compose installed
- A basic understanding of SSH
- [Installing Obfuscated OpenSSH on your client](https://computerscot.github.io/obfuscated-ssh.html)

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/teal33t/obfuscated-openssh-tunnel
   cd https://github.com/teal33t/obfuscated-openssh-tunnel
   ```

2. **Build and start the container:**
   ```bash
   docker-compose up --build -d
   ```

### Configuration

- **Ports:**
   - Standard SSH port: `2223`
   - Obfuscated SSH port: `8443`

- **Volumes:**
   - `./sshd_config:/etc/ssh/sshd_config:ro` - The SSH configuration file is mounted read-only from the host.

## Connecting with an SSH Client

To connect to the obfuscated SSH service, use the following command:
```bash
ssh -p 8443 -o ObfuscateKeyword=your-salt-key -D 0.0.0.0:1080 sshuser@your-server-ip
```

- `-p 8443`: Specifies the port to connect to (obfuscated port)
- `-o ObfuscateKeyword=your-salt-key`: Uses the obfuscation keyword configured in `sshd_config`
- `-D 0.0.0.0:1080`: Sets up a SOCKS proxy on port `1080`
- `sshuser@your-server-ip`: Connects to the SSH service as `sshuser`

## Troubleshooting

- Ensure Docker is running.
- Verify that ports `22` and `8443` are open and not used by other services.
- Check the logs for any errors:
  ```bash
  docker logs <container-id>
  ```

## License

This project is licensed under the MIT License.

## Acknowledgements

- [obfuscated-openssh](https://computerscot.github.io/obfuscated-ssh) - The repository providing obfuscated SSH support.

---

Feel free to contribute to this project by submitting issues or pull requests.