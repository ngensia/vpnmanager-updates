# VPN Manager Updates

This repository stores public release artifacts for VPN Manager.

Download:

- `VPN_MANAGER_SETUP.exe`
- [Portable 1.3.10](VPN_MANAGER_Portable_1.3.10.zip)

Version 1.3.10 creates shortcuts in the employee's Start menu and Desktop using the native Windows Shell Link API, without WScript.Shell. Shortcut failures are reported with the application path. Uninstall removes both shortcuts.

Version 1.3.9 fixes per-user update installation: updates no longer request elevation. The installer refuses an elevated launch to avoid installing into the administrator profile. When upgrading from older versions, download the installer and run it normally as the employee once. The shortcut is created in that user's Start menu.

Version 1.3.8 adds one-time administrator setup for starting and stopping prepared WireGuard tunnel services as a standard user. Run the app as the employee, click `?`, verify the employee account, and select the access setup button. An administrator approves the setup. Repeat setup for new or recreated tunnel services.
