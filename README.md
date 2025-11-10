# Advulnbuster-kali-linux
ADvulnbuster audit tool for Linux

Advulnbusteraudit is an automated auditing tool for Active Directory environments that combines multiple pentesting utilities into a single Python script. It performs enumeration, vulnerability checking, credential extraction, and ADCS (Active Directory Certificate Services) analysis.

## Features

- **Complete enumeration** of shares, users, groups, and computers
- **SMB vulnerability checks**: Zerologon, PetitPotam, NoPAC, PrintNightmare, etc.
- **Credential harvesting**: LSA, SAM, NTDS, DPAPI
- **Kerberoast/ASREPRoast analysis** with hash export
- **ADCS analysis** using Certipy-AD or NetExec modules
- **Authentication coercion** with coerce_plus
- **DCSync** for NTLM hash extraction
- **Detailed HTML report** with all command outputs
- **Real-time progress output** during auditing
- **Robust error handling** and command timeout management

## Requirements

- Python 3.8+
- Kali Linux 2024.4+ (recommended) or compatible system
- NetExec (installed via pipx, not from APT packages)
- Certipy-AD
- Impacket

## Installation

### On Kali Linux 2024.4+:

# Update repository sources
sudo apt update

# Uninstall buggy APT package version of NetExec
sudo apt remove netexec

# Install dependencies
sudo apt install -y python3 python3-pip python3-full build-essential libssl-dev libffi-dev krb5-user pipx

# Install tools with pipx (recommended method)
pipx install git+https://github.com/Pennyw0rth/NetExec
pipx install certipy-ad
pipx ensurepath

# Verify installation
nxc --version
certipy-ad --help

Usage
Basic execution:

python3 advulnbusteraudit.py --target 192.168.1.100 --domain example.local --user Administrator --password 'P@ssw0rd'

Execution with ADCS analysis using Certipy:

python3 advulnbusteraudit.py --target 192.168.1.100 --domain example.local --user Administrator --password 'P@ssw0rd' --adcs-tool certipy

Preview commands without executing:

python3 advulnbusteraudit.py --target 192.168.1.100 --domain example.local --user Administrator --password 'P@ssw0rd' --dry-run

Skip Kerberoast/ASREPRoast (useful when having DNS issues):

python3 advulnbusteraudit.py --target 192.168.1.100 --domain example.local --user Administrator --password 'P@ssw0rd' --skip-kerberoast

Available parameters:

    --target: Target IP address
    --domain: Domain name
    --user: Privileged user
    --password: User password
    --artifacts-dir: Directory to save artifacts (default: ./artifacts)
    --output: HTML report filename (default: report_audit.html)
    --dry-run: Show commands without executing them
    --adcs-tool: ADCS tool to use ("certipy")
    --skip-kerberoast: Skip Kerberoast/ASREPRoast

Output

The script generates:

    An artifacts/ directory with hash files, ADCS results, etc.
    A detailed HTML report with all command outputs
    Summary tables of found vulnerabilities
    Links to generated artifacts

    ## Si te ha gustado esta tool apóyame para que pueda seguir desarrollando nuevas herramientas! 
<a href="https://www.buymeacoffee.com/joelcl2001q" target="_blank">
  <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" height="50">
</a>

