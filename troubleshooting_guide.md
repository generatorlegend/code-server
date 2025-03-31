---
title: Troubleshooting Guide
---

# Troubleshooting Guide

This guide will help you diagnose and resolve common issues you might encounter while using code-server. We'll cover connection problems, authentication issues, and extension-related problems. We'll also explain how to gather relevant logs for debugging.

## Connection Problems

### Unable to Connect to code-server

If you're having trouble connecting to code-server, try the following steps:

1. Check if code-server is running:
   ```
   ps aux | grep code-server
   ```
   If it's not running, start it using the appropriate command.

2. Verify the bind address and port:
   - Check your config file (default location: `~/.config/code-server/config.yaml`)
   - Ensure the `bind-addr` is set correctly (e.g., `127.0.0.1:8080` for local access)

3. Check firewall settings:
   - Make sure the port you're using is open and accessible

4. Try accessing via localhost:
   - If you've set a custom hostname, try accessing via `http://localhost:PORT` instead

### Connection Refused

If you're getting a "Connection Refused" error:

1. Verify the port is not in use by another application:
   ```
   netstat -tuln | grep PORT
   ```
   Replace PORT with the port number you're using for code-server.

2. Try changing the port in your config file and restart code-server.

## Authentication Issues

### Password Not Working

If you're unable to log in with your password:

1. Check if you're using the correct password:
   - The password is stored in your config file or set via the `PASSWORD` environment variable

2. Reset your password:
   - Edit your config file and update the `password` field
   - Or, set a new password using the `PASSWORD` environment variable:
     ```
     export PASSWORD="your_new_password"
     code-server
     ```

3. Ensure you're not mixing up `password` and `hashed-password` in your config file

### "No Authentication" Error

If you're seeing a "No Authentication" error:

1. Check your config file and ensure the `auth` field is set to `password`

2. Make sure you've set a password either in the config file or via the `PASSWORD` environment variable

## Extension-Related Problems

### Unable to Install Extensions

If you're having trouble installing extensions:

1. Check your internet connection

2. Verify you have write permissions in the extensions directory:
   - Default location: `~/.local/share/code-server/extensions`
   - Check permissions: `ls -l ~/.local/share/code-server/extensions`

3. Try installing the extension manually:
   - Download the VSIX file for the extension
   - Use the "Install from VSIX" option in code-server

### Extensions Not Working Properly

If installed extensions are not functioning correctly:

1. Check if the extension is compatible with code-server
   - Some extensions might require additional configuration or may not work in a browser environment

2. Try disabling and re-enabling the extension

3. Uninstall and reinstall the extension

## Gathering Logs for Debugging

To gather logs for more detailed debugging:

1. Set the log level to "debug" or "trace":
   - In your config file: `log: debug`
   - Or use the `--log` flag: `code-server --log debug`

2. Reproduce the issue

3. Locate the log file:
   - Default location: `~/.local/share/code-server/coder-logs`
   - Or check the output if you're running code-server in the foreground

4. Review the logs for any error messages or relevant information

5. When seeking help, provide these logs along with:
   - Your code-server version (`code-server --version`)
   - Your operating system and version
   - Steps to reproduce the issue

## Common Error Messages

### "EADDRINUSE"

This error means the port is already in use. Try the following:

1. Choose a different port in your config file
2. Kill the process using the port:
   ```
   lsof -i :PORT | grep LISTEN
   kill -9 PID
   ```
   Replace PORT with the port number and PID with the process ID from the lsof output.

### "EACCES"

This error suggests a permissions issue. Try:

1. Using a port number above 1024 (ports below 1024 require root privileges)
2. Running code-server with `sudo` (not recommended for security reasons)

If you continue to experience issues after trying these solutions, please check the [code-server GitHub issues](https://github.com/coder/code-server/issues) or create a new issue with detailed information about your problem.