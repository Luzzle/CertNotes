#NSE5 

### Overview
At any time, you can backup the FortiManager configuration in the **System Information** widget in the GUI. By default, encryption is enabled when you use the GUI for backups.

The backup will contain everything except logs, FortiGuard cache and firmware images.

#### Restoring from a backup
There are 2 options when performing a FortiManager restore:

- **Overwrite current IP, routing and HA configuration**: Enabled by default. Restoring using this option overwrites everything. If you disable this option, FortiManager will restore the configurations related to device information and the global database, but will preserve HA and network settings.
- **Offline Mode** - FortiManager temporarily disables the communication channel between FortiManager and all managed devices. This should be enabled to facilitate troubleshooting of any issues.

### Migrating to another FortiManager
To migrate to another FortiManager perform the following:

1. Backup the configuration on the first FortiManager
2. Run the following on the CLI of the second:
	`exec migrate all-settings`

If the original FortiManager has databases from FortiGuard, they will not be included. 

FortiManager supports FTP, SCP and SFTP protocols to migrate the configuration.