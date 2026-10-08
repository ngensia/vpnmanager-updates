# VPN Manager Updates

Public distribution files only. Current version: **1.3.23**.

## Downloads

- [Installer 1.3.23](https://raw.githubusercontent.com/ngensia/vpnmanager-updates/main/VPN_MANAGER_SETUP.exe)
- [Portable 1.3.23](VPN_MANAGER_Portable_1.3.23.zip)
- [IT installation guide](IT-Install-1.3.23.txt)
- [SHA-256 checksums](SHA256SUMS.txt)

## Installation And Updates

IT installs the application with administrator credentials in the protected Program Files directory. Shared Desktop and Start menu shortcuts are available. Employees run the manager without elevation.

For selected WireGuard tunnel services, the installer grants only status query, start and stop rights (0x34). It does not make the employee an administrator. The client does not elevate itself, grant permissions, or create/delete WireGuard services.

The update button downloads the installer but never executes it. IT verifies the package, places it in an administrator-controlled directory and runs installation manually. This build is not digitally signed; checksums from the same download source alone do not authenticate the publisher.

## Changes In 1.3.23

- Resource checks require an active VPN profile/tunnel service. Without one, the UI asks the employee to connect first and hides old results and the RDS link.
- All three resources responding gives a green result; a subset gives a partial result; none gives an unavailable result. Disconnecting or changing tunnels clears previous results. Late responses cannot restore an obsolete check.
- Response times below one millisecond show as `< 1 ms`. The RDS link requires a responding gateway and an active VPN.
- The sidebar displays connected Wi-Fi SSIDs, updates automatically and shows full long names in a tooltip. Windows privacy restrictions may prevent SSID access; the app does not change privacy policy or read saved passwords.
- The installer supports an administrator-selected local `.conf`, including nonstandard directories. Existing service paths are preserved; new tunnel services can be prepared after confirmation.
- Configuration-file and folder owners/ACLs are accepted as approved by the installing administrator. Existing employee write permissions remain unchanged. Protected executable/service-registration checks and the 0x34 service permission limit remain in place.
- The IT guide explains the domain-PC uninstall workaround: if removal fails on `VPN MANAGER.lnk`, manually remove that shortcut at the reported path with administrator confirmation, then retry uninstall. The uninstaller itself has not changed.

Automated package, permission, IKEv2 diagnostic and UI tests pass, including disconnected/partial states, late responses, writable configuration fixtures and Wi-Fi parsing/layout. Real domain-PC installation/uninstallation and Wi-Fi hardware still require IT validation. No real VPN services or configurations were changed by these tests.

The client still does not elevate itself or launch downloaded installers. An active WireGuard service is not proof of a handshake; ping is not proof of RDS authentication or traffic routing through the VPN.

## Previous Release 1.3.19

- IKEv2 failures display Russian explanations with the original Windows error code, independently of the Windows UI language.
- Rasdial output uses the Windows OEM code page; PowerShell stdout/stderr explicitly use UTF-8.
- Certificate errors have separate descriptions. A generic connection failure does not claim that a certificate is missing.

This release also includes the protected installation changes developed in local versions 1.3.13-1.3.18:

- Protected machine-wide installation replaces the previous per-user installation and self-elevation mechanism.
- Current-session employee detection and explicit SID/tunnel confirmation.
- Metadata-only validation of protected WireGuard configuration permissions in 1.3.19. Since 1.3.22, the administrator-approved configuration policy above replaces this restriction; executable and service-registration protection remains.
- Explicit protected permissions for the application's own uninstall registration, including recovery after an incomplete installation.
- Refined interface, text-only link activation and clearer blocked/empty tunnel diagnostics.

Automatic package, security-contract, Russian error diagnostic and interface checks pass. The rasdial integration test uses only a nonexistent profile, without dialing a real VPN. Elevated metadata/registration tests and the full domain-PC installation/start-stop/reboot/uninstall cycle still require IT validation before broad deployment.

Unknown IKEv2 error codes retain their exact numeric value and Russian guidance for IT. The manager does not install VPN certificates. ICMP results indicate network reachability, not complete RDS service health.

## Legacy Versions

Versions **1.3.8-1.3.11** used an unsafe self-elevation mechanism from a user-writable installation directory. Do not use their WireGuard access setup or run those managers as administrator. Local version 1.3.12 is also not for distribution.

If an old installation exists, exit it from the tray, disable its startup and remove the per-user installation in the employee's session. IT then installs the current version. No removal is needed for a first installation.

Legacy archives and Git history may still contain old packages. Publishing the new version does not remove previously downloaded copies. Use only the current installer and portable archive linked above.
