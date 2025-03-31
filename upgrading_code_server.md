# Upgrading code-server

This guide provides instructions on how to upgrade code-server to the latest version, including how to check for updates, perform the upgrade process, and any necessary steps to migrate settings or data between versions.

## Checking for Updates

code-server includes a built-in mechanism to check for updates. You can use the following methods to check if a new version is available:

1. **API Endpoint**: You can make a GET request to the `/update/check` endpoint. This endpoint is authenticated, so you need to ensure you're properly authenticated before making the request.

   ```typescript
   router.get("/check", ensureAuthenticated, async (req, res) => {
     const update = await req.updater.getUpdate(req.query.force === "true")
     res.json({
       checked: update.checked,
       latest: update.version,
       current: version,
       isLatest: req.updater.isLatestVersion(update),
     })
   })
   ```

   This endpoint returns a JSON object with the following information:
   - `checked`: The timestamp of when the update was last checked
   - `latest`: The latest available version
   - `current`: The currently installed version
   - `isLatest`: A boolean indicating whether the current version is the latest

2. **Programmatically**: You can use the `UpdateProvider` class to check for updates in your code:

   ```typescript
   const updateProvider = new UpdateProvider(latestUrl, settings);
   const update = await updateProvider.getUpdate();
   const isLatest = updateProvider.isLatestVersion(update);
   ```

   The `getUpdate` method will check for updates and return an `Update` object containing the latest version information.

## Performing the Upgrade

Once you've determined that an update is available, you can follow these steps to upgrade code-server:

1. **Download the latest version**: Visit the official code-server GitHub repository or the website to download the latest version appropriate for your operating system.

2. **Stop the current code-server instance**: Ensure that no code-server processes are running before proceeding with the upgrade.

3. **Install the new version**: Follow the installation instructions provided with the downloaded package. This typically involves replacing the existing code-server executable or updating the package using your system's package manager.

4. **Restart code-server**: After installation, start the new version of code-server.

## Migrating Settings and Data

When upgrading code-server, it's important to consider any settings or data that may need to be migrated. While code-server strives to maintain backwards compatibility, it's always a good practice to backup your data before performing an upgrade.

1. **Backup your data**: Before upgrading, make a backup of your code-server data directory. This directory typically contains your user settings, extensions, and other configuration files.

2. **Check for breaking changes**: Review the release notes for the new version to see if there are any breaking changes that might affect your setup or require manual intervention.

3. **Update configuration files**: If necessary, update your configuration files to match any new format or options introduced in the new version.

4. **Verify extensions**: After upgrading, verify that all your installed extensions are compatible with the new version of code-server.

## Automating Updates

For advanced users or system administrators, you may want to consider automating the update process. You can create a script that:

1. Checks for updates using the API endpoint or `UpdateProvider` class
2. Downloads the latest version if an update is available
3. Stops the current code-server instance
4. Installs the new version
5. Restarts code-server

Remember to include appropriate error handling and logging in your automation script.

## Troubleshooting

If you encounter issues after upgrading:

1. Check the code-server logs for any error messages
2. Verify that your configuration files are compatible with the new version
3. Try starting code-server with the `--verbose` flag for more detailed logging
4. If problems persist, consider rolling back to the previous version and reporting the issue on the code-server GitHub repository

By following these guidelines, you can ensure a smooth upgrade process for your code-server installation, keeping it up-to-date with the latest features and security improvements.