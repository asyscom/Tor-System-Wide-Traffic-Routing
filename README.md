Ecco una versione aggiornata del file `README.md` con un titolo più specifico e con comandi per entrambe le distribuzioni, Rocky Linux e Debian.

### Nome del Repository
**`Tor-System-Wide-Traffic-Routing`**

Questo nome chiarisce che il progetto riguarda la configurazione di un proxy Tor per instradare tutto il traffico di sistema.

---

### `README.md`

```markdown
# Tor-System-Wide-Traffic-Routing

This repository provides a comprehensive guide to routing all system-wide traffic through Tor on Linux, with instructions for both Rocky Linux and Debian. The guide covers terminal-based tools like `curl` and browser configuration to ensure all your network traffic is anonymized through Tor.

## Table of Contents

1. [Introduction](#introduction)
2. [Installation](#installation)
   - [Rocky Linux](#rocky-linux)
   - [Debian](#debian)
3. [System-wide Proxy Configuration](#system-wide-proxy-configuration)
4. [Browser Configuration](#browser-configuration)
   - [Firefox](#firefox)
   - [Google Chrome / Chromium](#google-chrome--chromium)
   - [Microsoft Edge](#microsoft-edge)
5. [Testing](#testing)
6. [Advanced Options](#advanced-options)
7. [Contributing](#contributing)
8. [License](#license)

## Introduction

Tor (The Onion Router) is a free and open-source software that enables anonymous communication by directing internet traffic through a worldwide volunteer overlay network. This guide explains how to configure your system and browser to route all traffic through Tor, enhancing your online privacy.

## Installation

### Rocky Linux

First, ensure that your system is up-to-date:

```bash
sudo dnf update -y
```

Install Tor using the EPEL repository:

```bash
sudo dnf install epel-release
sudo dnf install tor
```

### Debian

First, ensure that your system is up-to-date:

```bash
sudo apt update && sudo apt upgrade -y
```

Install Tor:

```bash
sudo apt install tor -y
```

### Start and Enable Tor Service

On both Rocky Linux and Debian, start and enable the Tor service:

```bash
sudo systemctl start tor
sudo systemctl enable tor
```

Tor runs on port `9050` by default, providing a SOCKS5 proxy.

## System-wide Proxy Configuration

To route all system-wide traffic through Tor, configure the environment variables for `http_proxy` and `https_proxy`.

### Rocky Linux

```bash
export http_proxy="socks5h://localhost:9050"
export https_proxy="socks5h://localhost:9050"
```

### Debian

```bash
export http_proxy="socks5h://localhost:9050"
export https_proxy="socks5h://localhost:9050"
```

To make this configuration permanent, add these lines to your `~/.bashrc` or `~/.bash_profile` (Rocky Linux) or `~/.profile` (Debian).

## Browser Configuration

### Firefox

1. Open Firefox and navigate to **Settings** > **Network Settings** > **Settings**.
2. Select **Manual proxy configuration** and set:
   - SOCKS Host: `localhost`
   - Port: `9050`
   - Select SOCKS v5.
3. Enable **Proxy DNS when using SOCKS v5**.
4. Save and restart Firefox.

### Google Chrome / Chromium

#### Using an Extension

1. Install a proxy extension like [SwitchyOmega](https://github.com/FelisCatus/SwitchyOmega/releases) or [FoxyProxy](https://getfoxyproxy.org/downloads.html).
2. Configure a new SOCKS5 proxy profile with:
   - Server: `localhost`
   - Port: `9050`
3. Activate the profile.

#### Command Line

Alternatively, start Chrome with:

```bash
google-chrome --proxy-server="socks5://localhost:9050"
```

### Microsoft Edge

Since Edge is based on Chromium, you can follow the same steps as for Google Chrome.

## Testing

To verify that your traffic is being routed through Tor, visit [check.torproject.org](https://check.torproject.org). If configured correctly, you'll see a message confirming that your browser is using Tor.

## Advanced Options

For applications that do not support proxy settings, you can use `proxychains` to force them to use Tor:

### Rocky Linux

```bash
sudo dnf install proxychains-ng
```

### Debian

```bash
sudo apt install proxychains4
```

Edit `/etc/proxychains.conf` to use `socks5 127.0.0.1 9050`, then run your application with `proxychains <application>`.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request or open an issue if you have any suggestions or improvements.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
```

