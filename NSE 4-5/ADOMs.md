#NSE5 

### Overview
ADOMs allow you to logically group devices for administrators to manage. ADOMs work in 2 device modes, normal or advanced. When advanced mode is enabled, you can assign different VDOMs to different ADOMs.

By default, users with **Super_User** access can move devices between ADOMs.

##### Enabling ADOMs
ADOMs are not enabled by default, and can only be enabled by Administrators that have the super_user profile.

```
config system global
	set adom-status enable
end
```

or by navigating to **System Settings** > **ADOMs**, which is where you can also create ADOMs.

#### Operation Modes
##### Normal
- Default
- ADOM is Read/Write and all management panes are available

##### Backup Mode
- ADOM is Read Only
- Not all panes are visible.
- Only scripts can be used to make changes from the FortiManager to managed devices.

#### Device Operation Modes
##### Normal
FortiGate and its VDOMs can only be added to a single ADOM only.

##### Advanced
You can assign different VDOMs from the same FortiGate to different ADOMs.

### Workspaces
By default, multiple admins can make changes to the same ADOM concurrently. To ensure administrators cannot make overlapping changes, you can enable **Workspace Mode**. When enabling you have the following options:

- **Workspace (ALL ADOMS)** - All ADOMs can be locked.
- **Workspace (Per ADOM)** - Only ADOMs configured for workspace mode can be locked.
- **Workflow (ALL ADOMS)** - In addition to locking ADOMs, this mode can be used to ensure that all changes are reviewed and approved by authorized admins before they are applied.

Optionally you can enable **per policy lock** which allows you to lock individual policies.

Enabling **Workspace Mode** allows you to lock different items in FortiManager, effectively preventing concurrent read/write access to any locked item. You can lock:

- Entire ADOMs
- Individual devices
- Policy Packages
- Objects
- Individual Policies

### Firmware
Each ADOM is associated with a specific firmware version, this allows for devices to share a common database to ensure compatibility. The ADOM version determines which device firmware is supported by FortiManager. FortiManager 7.6.2 supports 7.2, 7.4 and 7.6.

You can upgrade the ADOM before, or after you can upgraded the firmware of all the devices it contains. It is recommended to upgrade the devices first, then the ADOM.

When upgrading an ADOM, the upgrade process only updates the database of the selected ADOM. If the ADOM is using global ADOM objects, you must upgrade the global ADOM database to the same version first; otherwise you will lose some of the configuration.

##### Best Practice
**Before Upgrades**
- Install and pending device settings and policy package changes. Ensure the device is fully synchronised.

**After Upgrades**
- Check installation preview to review any changes caused by the upgrade.

**Device migrated to a different ADOM**
- Shared policy package and objects will not move to the new ADOM, but these can be imported.