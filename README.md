
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
9. [Support the Project](#support-the-project)

## Introduction

Tor (The Onion Router) is a free and open-source software that enables anonymous communication by directing internet traffic through a worldwide volunteer overlay network. This guide explains how to configure your system and browser to route all traffic through Tor, enhancing your online privacy.

## Installation

### Rocky Linux

First, ensure that your system is up-to-date:

```bash
sudo dnf update -y
```

Next, install Tor using the following commands:

```bash
sudo dnf install epel-release -y
sudo dnf install tor -y
```

Enable and start the Tor service:

```bash
sudo systemctl enable tor
sudo systemctl start tor
```

### Debian

First, ensure that your system is up-to-date:

```bash
sudo apt update && sudo apt upgrade -y
```

Install Tor using the following command:

```bash
sudo apt install tor -y
```

Enable and start the Tor service:

```bash
sudo systemctl enable tor
sudo systemctl start tor
```

## System-wide Proxy Configuration

Once Tor is installed, configure your system to route all traffic through it. This can be done by setting up a system-wide proxy that directs traffic through the Tor SOCKS5 proxy.

Edit your environment variables to include the following:

```bash
export http_proxy="socks5://localhost:9050"
export https_proxy="socks5://localhost:9050"
```

You can add these lines to your shell configuration file (e.g., `.bashrc`, `.zshrc`) for persistent proxy settings.

## Browser Configuration

### Firefox

1. Open Firefox and navigate to `Preferences > General`.
2. Scroll down to the `Network Settings` section and click on `Settings`.
3. Select `Manual proxy configuration` and enter `localhost` and port `9050` for both HTTP and HTTPS proxies.
4. Check the box for `Use this proxy server for all protocols` and click `OK`.

### Google Chrome / Chromium

1. Open Google Chrome or Chromium and navigate to `Settings > Advanced > System > Open Proxy Settings`.
2. In the proxy settings window, configure the SOCKS5 proxy with the address `localhost` and port `9050`.
3. Save the settings and restart your browser.

### Microsoft Edge

1. Open Microsoft Edge and go to `Settings > System > Open your computer's proxy settings`.
2. Under `Manual proxy setup`, enable the option to use a proxy server.
3. Enter `localhost` as the proxy address and `9050` as the port.
4. Save the settings and restart Microsoft Edge.

## Testing

To test that your traffic is being routed through Tor, use the following command to check your public IP:

```bash
curl https://check.torproject.org
```

This should confirm that you are using the Tor network.

## Advanced Options

If you need more advanced configurations, such as specific routing for certain applications or configuring firewall rules, refer to the [Tor documentation](https://www.torproject.org/docs/tor-manual.html.en).

## Contributing

If you have suggestions or improvements, feel free to submit a pull request or open an issue in this repository.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

## Support the Project

If you found this guide helpful and would like to support the project, consider making a donation. Your contributions help maintain and improve this resource.

---

