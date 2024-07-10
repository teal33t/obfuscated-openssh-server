# Obfuscated SSH Service - Server

This project sets up an SSH service with obfuscated SSH support. It uses Docker to containerize the service and provides an example of how to connect using a client with SSH obfuscation.

If you are looking for **Obfuscated SSH Service - Client**, go to [https://github.com/teal33t/obfuscated-openssh-client](https://github.com/teal33t/obfuscated-openssh-client) 

## Getting Started

### Prerequisites

- Docker and Docker Compose installed
- A basic understanding of SSH
- [Installing Obfuscated OpenSSH on your client](https://zinglau.com/projects/ObfuscatedOpenSSHPatches.html)

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

To connect to the obfuscated SSH service, you should install obfuscated-ssh on your client machine

```bash
apt-add-repository ppa:zinglau/obfuscated-openssh
apt-get update
apt-get install ssh
```

And for connecting:


```bash
ssh -p 8443 -o ObfuscateKeyword=123qwer -D 0.0.0.0:1080 sshuser@your-server-ip
```

- `-p 8443`: Specifies the port to connect to (obfuscated port)
- `-o ObfuscateKeyword=123qwer`: Uses the obfuscation keyword configured in `sshd_config`, change it use a secure phrase.
- `-D 0.0.0.0:1080`: Sets up a SOCKS proxy on port `1080`
- `sshuser@your-server-ip`: Connects to the SSH service as `sshuser`

## Troubleshooting

- Ensure Docker is running.
- Verify that ports `2223` and `8443` are open and not used by other services.
- Check the logs for any errors:
  ```bash
  docker logs <container-id>
  ```

## License

This project is licensed under the MIT License.

## Acknowledgements

- [zinglau](https://zinglau.com/projects/ObfuscatedOpenSSHPatches.html)
- [obfuscated-openssh](https://computerscot.github.io/obfuscated-ssh)
- [obfuscated-openssh](https://github.com/brl/obfuscated-openssh)

---

Feel free to contribute to this project by submitting issues or pull requests.
