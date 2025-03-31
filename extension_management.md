# Extension Management in code-server

This guide explains how to manage VS Code extensions in code-server, including installation, updating, and removal. We'll also highlight any differences between extension management in code-server and standard VS Code.

## Installing Extensions

You can install extensions in code-server using the following methods:

1. Command Line Interface (CLI)
2. VS Code Extension Marketplace (GUI)

### Using the CLI

To install extensions using the CLI, use the `--install-extension` flag followed by the extension ID or `.vsix` file path. The extension ID is typically in the format `${publisher}.${name}`.

```bash
code-server --install-extension <extension-id-or-vsix-file>
```

To install a specific version of an extension, append `@${version}` to the extension ID:

```bash
code-server --install-extension vscode.csharp@1.2.3
```

You can install multiple extensions at once by specifying multiple `--install-extension` flags:

```bash
code-server --install-extension ms-python.python --install-extension ms-toolsai.jupyter
```

### Using the VS Code Extension Marketplace

1. Open code-server in your browser
2. Click on the Extensions icon in the left sidebar (or press `Ctrl+Shift+X`)
3. Search for the desired extension
4. Click the "Install" button next to the extension

## Updating Extensions

To update extensions in code-server:

1. Open the Extensions view
2. Look for extensions with an available update
3. Click the "Update" button next to the extension or use the "Update All" button to update all extensions at once

## Removing Extensions

### Using the CLI

To uninstall an extension using the CLI, use the `--uninstall-extension` flag followed by the extension ID:

```bash
code-server --uninstall-extension <extension-id>
```

You can uninstall multiple extensions at once:

```bash
code-server --uninstall-extension ms-python.python --uninstall-extension ms-toolsai.jupyter
```

### Using the VS Code Extension Marketplace

1. Open the Extensions view
2. Find the extension you want to remove
3. Click the gear icon next to the extension
4. Select "Uninstall" from the dropdown menu

## Listing Installed Extensions

To list all installed extensions, use the `--list-extensions` flag:

```bash
code-server --list-extensions
```

To include version information for each extension, add the `--show-versions` flag:

```bash
code-server --list-extensions --show-versions
```

## Differences from Standard VS Code

While extension management in code-server is similar to standard VS Code, there are a few key differences to be aware of:

1. **Remote Extensions**: Some extensions designed for remote development in VS Code may behave differently or not work as expected in code-server due to its architecture.

2. **System Requirements**: Ensure that any system-level dependencies required by extensions are installed on the server where code-server is running.

3. **Performance**: Extension performance may vary depending on the server's resources and network conditions between the client and server.

4. **Marketplace Access**: Depending on your code-server configuration, you may have limited access to the VS Code Marketplace. In such cases, you might need to install extensions manually using the CLI or by uploading `.vsix` files.

5. **Extension Settings**: Some extension settings may need to be adjusted to work correctly in a code-server environment, especially those related to file paths or system-specific configurations.

## Best Practices

1. **Use the `--force` Flag**: When installing extensions via CLI, use the `--force` flag to avoid prompts:

   ```bash
   code-server --install-extension <extension-id> --force
   ```

2. **Extension Compatibility**: Before installing an extension, check its compatibility with code-server or test it in a non-production environment.

3. **Keep Extensions Updated**: Regularly update your extensions to ensure you have the latest features and bug fixes.

4. **Clean Up Unused Extensions**: Periodically review and remove unused extensions to maintain optimal performance.

By following these guidelines, you can effectively manage extensions in your code-server environment, enhancing your development experience while being mindful of the differences from standard VS Code.