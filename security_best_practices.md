# Security Best Practices for code-server

This document outlines the security best practices for deploying and using code-server, including information on authentication, HTTPS setup, and how to secure your instance. It also provides guidance on using code-server in various environments.

## Authentication

code-server supports two types of authentication:

1. Password Authentication (default)
2. No Authentication

### Password Authentication

Password authentication is the default and recommended method for securing your code-server instance. To set up password authentication:

1. Set the `auth` option to `password` in your configuration file or use the `--auth` command-line flag.
2. Provide a password using one of the following methods:
   - Set the `password` option in the configuration file.
   - Use the `--password` command-line flag (not recommended for production use).
   - Set the `PASSWORD` environment variable.
   - Use a hashed password by setting the `hashed-password` option in the configuration file or the `HASHED_PASSWORD` environment variable.

Example configuration:

```yaml
auth: password
password: your-secure-password
```

or

```yaml
auth: password
hashed-password: <argon2-hashed-password>
```

### No Authentication

Using code-server without authentication is strongly discouraged, especially in production environments. If you must run without authentication (e.g., in a secure internal network), set the `auth` option to `none`:

```yaml
auth: none
```

## HTTPS Setup

Running code-server over HTTPS is crucial for securing your instance, especially when exposed to the internet. There are two ways to set up HTTPS:

1. Using a self-signed certificate
2. Using a custom certificate

### Self-signed Certificate

code-server can automatically generate a self-signed certificate for you. To enable this:

```yaml
cert: true
```

You can specify the hostname for the certificate:

```yaml
cert-host: your-domain.com
```

### Custom Certificate

To use your own certificate:

```yaml
cert: /path/to/your/certificate.crt
cert-key: /path/to/your/certificate.key
```

## Securing Your Instance

### Bind Address

By default, code-server binds to `127.0.0.1`. To change this:

```yaml
bind-addr: 192.168.1.100:8080
```

For improved security, avoid binding to `0.0.0.0` unless necessary.

### Proxy Domains

If you're using code-server behind a reverse proxy, configure trusted proxy domains:

```yaml
proxy-domain: your-domain.com
```

### Disabling File Downloads and Uploads

To prevent users from downloading or uploading files:

```yaml
disable-file-downloads: true
disable-file-uploads: true
```

### Disabling Update Checks

To prevent code-server from checking for updates:

```yaml
disable-update-check: true
```

## Environment-specific Guidance

### Local Development

For local development, the default settings are generally secure. Ensure you're using a strong password and avoid exposing code-server to the internet unnecessarily.

### Remote Server

When running code-server on a remote server:

1. Use HTTPS with a valid certificate.
2. Set a strong password or use SSH tunneling for authentication.
3. Configure your firewall to limit access to the code-server port.
4. Use a reverse proxy (e.g., Nginx, Caddy) for additional security layers.

### Docker Deployment

When deploying code-server using Docker:

1. Avoid mounting the Docker socket unless absolutely necessary.
2. Use Docker's built-in secret management for sensitive information.
3. Run the container as a non-root user.

Example Docker run command with improved security:

```bash
docker run -it --user 1000:1000 -p 127.0.0.1:8080:8080 \
  -v "$PWD:/home/coder/project" \
  -u "$(id -u):$(id -g)" \
  -e "PASSWORD=your-secure-password" \
  codercom/code-server:latest
```

### Cloud Deployments

When deploying to cloud platforms:

1. Use the platform's secret management services for storing passwords and tokens.
2. Implement proper network security groups or firewall rules.
3. Consider using managed SSL/TLS services provided by the cloud platform.

## Additional Security Measures

1. Regularly update code-server and its dependencies.
2. Monitor logs for suspicious activities.
3. Implement rate limiting to prevent brute-force attacks.
4. Use strong, unique passwords for each deployment.
5. Consider using multi-factor authentication in addition to password authentication.

By following these best practices, you can significantly enhance the security of your code-server deployments across various environments.