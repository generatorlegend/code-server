# Configuration Options

code-server offers various configuration options to customize its behavior. These options can be set through command-line arguments, environment variables, or a configuration file. This document provides a comprehensive list of available configuration options and explains how to use them.

## Command-line Arguments

You can pass these arguments when starting code-server from the command line.

| Argument | Description |
|----------|-------------|
| `--auth` | Specifies the type of authentication to use. Options: `password`, `none`. Default: `password` |
| `--password` | Sets the password for authentication. |
| `--hashed-password` | Sets a hashed password for authentication. Takes precedence over `--password`. |
| `--cert` | Path to certificate for HTTPS. If not provided, a self-signed certificate is generated. |
| `--cert-key` | Path to certificate key when using a non-generated certificate. |
| `--disable-telemetry` | Disables telemetry. |
| `--disable-update-check` | Disables update check. |
| `--disable-file-downloads` | Disables file downloads from code-server. |
| `--disable-file-uploads` | Disables file uploads. |
| `--disable-workspace-trust` | Disables the Workspace Trust feature. |
| `--disable-getting-started-override` | Disables the custom Getting Started page. |
| `--disable-proxy` | Disables domain and path proxy routes. |
| `--host` | Specifies the host to listen on. |
| `--port` | Specifies the port to listen on. |
| `--socket` | Path to a socket (bind-addr will be ignored). |
| `--socket-mode` | File mode of the socket. |
| `--trusted-origins` | Disables authenticate origin check for trusted origins. |
| `--user-data-dir` | Specifies the user data directory. |
| `--extensions-dir` | Specifies the extensions directory. |
| `--config` | Path to the config file. Default: `~/.config/code-server/config.yaml` |
| `--verbose` | Enables verbose logging. |

Example usage:

```bash
code-server --auth none --port 8080 --user-data-dir ~/.config/code-server
```

## Environment Variables

Some configuration options can be set using environment variables.

| Variable | Description |
|----------|-------------|
| `PASSWORD` | Sets the password for authentication. |
| `HASHED_PASSWORD` | Sets a hashed password for authentication. Takes precedence over `PASSWORD`. |
| `CS_DISABLE_FILE_DOWNLOADS` | Disables file downloads when set to `1` or `true`. |
| `CS_DISABLE_GETTING_STARTED_OVERRIDE` | Disables the custom Getting Started page when set to `1` or `true`. |
| `CS_DISABLE_PROXY` | Disables domain and path proxy routes when set to `1` or `true`. |
| `GITHUB_TOKEN` | Sets the GitHub authentication token. |

Example usage:

```bash
export PASSWORD="your_password_here"
code-server
```

## Configuration File

code-server uses a YAML configuration file located at `~/.config/code-server/config.yaml` by default. You can specify a different location using the `--config` flag.

Example configuration file:

```yaml
bind-addr: 127.0.0.1:8080
auth: password
password: your_password_here
cert: false
user-data-dir: ~/.config/code-server
extensions-dir: ~/.local/share/code-server/extensions
```

## Configuration Priorities

When multiple configuration methods are used, code-server follows this priority order:

1. Command-line arguments
2. Environment variables
3. Configuration file
4. Default values

This means that command-line arguments will override environment variables, which will override settings in the configuration file.

## Additional Notes

- For boolean options, you can enable them by just including the flag (e.g., `--disable-telemetry`) or explicitly set them to `true` (e.g., `--disable-telemetry=true`).
- Some options, like `--password` and `--github-auth`, can only be set through the configuration file or environment variables for security reasons.
- The `--cert` option generates a self-signed certificate if no path is provided.
- Use `--verbose` or set the log level to `trace` for detailed logging, which can be helpful for troubleshooting.

For more detailed information on specific features or advanced configurations, please refer to the other sections of the documentation.