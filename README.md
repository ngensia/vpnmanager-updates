# VPN Manager Updates

Public distribution files only. Current version: **1.3.19**.

## Downloads

- [Installer 1.3.19](https://raw.githubusercontent.com/ngensia/vpnmanager-updates/main/VPN_MANAGER_SETUP.exe)
- [Portable 1.3.19](VPN_MANAGER_Portable_1.3.19.zip)
- [IT installation guide](IT-Install-1.3.19.txt)
- [SHA-256 checksums](SHA256SUMS.txt)

## Installation And Updates

IT installs the application with administrator credentials in the protected Program Files directory. Shared Desktop and Start menu shortcuts are available. Employees run the manager without elevation.

For selected WireGuard tunnel services, the installer grants only status query, start and stop rights (0x34). It does not make the employee an administrator. The client does not elevate itself, grant permissions, or create/delete WireGuard services.

The update button downloads the installer but never executes it. IT verifies the package, places it in an administrator-controlled directory and runs installation manually. This build is not digitally signed; checksums from the same download source alone do not authenticate the publisher.

## Changes In 1.3.19

- IKEv2 failures display Russian explanations with the original Windows error code, independently of the Windows UI language.
- Rasdial output uses the Windows OEM code page; PowerShell stdout/stderr explicitly use UTF-8.
- Certificate errors have separate descriptions. A generic connection failure does not claim that a certificate is missing.

This release also includes the protected installation changes developed in local versions 1.3.13-1.3.18:

- Protected machine-wide installation replaces the previous per-user installation and self-elevation mechanism.
- Current-session employee detection and explicit SID/tunnel confirmation.
- Metadata-only validation of protected WireGuard configuration permissions, without reading private keys or changing configuration ACLs.
- Explicit protected permissions for the application's own uninstall registration, including recovery after an incomplete installation.
- Refined interface, text-only link activation and clearer blocked/empty tunnel diagnostics.

Automatic package, security-contract, Russian error diagnostic and interface checks pass. The rasdial integration test uses only a nonexistent profile, without dialing a real VPN. Elevated metadata/registration tests and the full domain-PC installation/start-stop/reboot/uninstall cycle still require IT validation before broad deployment.

Unknown IKEv2 error codes retain their exact numeric value and Russian guidance for IT. The manager does not install VPN certificates. ICMP results indicate network reachability, not complete RDS service health.

## Legacy Versions

Versions **1.3.8-1.3.11** used an unsafe self-elevation mechanism from a user-writable installation directory. Do not use their WireGuard access setup or run those managers as administrator. Local version 1.3.12 is also not for distribution.

If an old installation exists, exit it from the tray, disable its startup and remove the per-user installation in the employee's session. IT then installs the current version. No removal is needed for a first installation.

Legacy archives and Git history may still contain old packages. Publishing the new version does not remove previously downloaded copies. Use only the current installer and portable archive linked above.
