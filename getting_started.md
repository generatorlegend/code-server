# Getting Started with code-server

This guide will walk you through the process of setting up and using code-server, a web-based IDE that allows you to run VS Code on a remote server.

## System Requirements

Before installing code-server, ensure your system meets the following minimum requirements:

- 1 GB of RAM
- 2 CPU cores
- Any Linux distribution, macOS, or Windows

## Installation

### Using the install script (Linux, macOS, FreeBSD)

The easiest way to install code-server is by using our install script:

```bash
curl -fsSL https://code-server.dev/install.sh | sh
```

This script will attempt to use your system's package manager if possible. For more options and details, you can run:

```bash
curl -fsSL https://code-server.dev/install.sh | sh -s -- --help
```

### Other Installation Methods

For other installation methods, including npm, standalone releases, and specific Linux distributions, please refer to our [detailed installation guide](./install.md).

## Configuration

After installation, you can configure code-server by creating or editing the configuration file. By default, it's located at `~/.config/code-server/config.yaml`.

Here's a basic configuration:

```yaml
bind-addr: 127.0.0.1:8080
auth: password
password: your_password_here
cert: false
```

Adjust the `bind-addr` and `password` as needed. For more configuration options, check the [configuration guide](./guide.md).

## Starting code-server

To start code-server, run:

```bash
code-server
```

By default, code-server will start on `http://127.0.0.1:8080`. You can access it through your web browser.

## Accessing code-server

1. Open your web browser and navigate to `http://127.0.0.1:8080` (or the address you specified in the configuration).
2. Enter the password you set in the configuration file.
3. You should now see the VS Code interface in your browser.

## Basic Usage

Once you're logged in, you can use code-server just like you would use VS Code:

1. Open folders or files using the File Explorer (left sidebar).
2. Install extensions from the Extensions view (square icon in the left sidebar).
3. Use the integrated terminal (Ctrl+` or Cmd+` on macOS).
4. Customize your settings, keybindings, and themes as you would in VS Code.

## Advanced Topics

- To enable HTTPS, set up a certificate in your configuration file.
- For remote access, consider setting up a reverse proxy and configuring your firewall.
- Explore additional features like workspace trust and GitHub authentication.

For more detailed information on these topics and other advanced features, refer to our [comprehensive guide](./guide.md).

## Troubleshooting

If you encounter any issues:

1. Check the logs (usually in `~/.local/share/code-server/logs/`).
2. Ensure your system meets the minimum requirements.
3. Verify your configuration file for any errors.
4. Consult our [FAQ](./FAQ.md) or [open an issue](https://github.com/coder/code-server/issues) on our GitHub repository.

## Next Steps

- Explore the [full documentation](https://coder.com/docs/code-server/latest) for more advanced topics.
- Join our [community](https://community.coder.com/) for support and discussions.
- Contribute to the [code-server project](https://github.com/coder/code-server) on GitHub.

Happy coding with code-server!