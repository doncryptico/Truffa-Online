# Truffa-Online
Advance Termux/Linux Optimized Phishing Tool - More than 30+ Templates - Remember: Just use it for Educational Purpose !

# Cloudflared Localhost Tunnel Setup

This guide explains how to install **cloudflared** on **Kali Linux** and **Termux**, then run your local tool using a Cloudflare Tunnel.

This setup is beginner-friendly and uses localhost service on port **5555**.

## Tunnel Command

Always use this command:

```bash
cloudflared tunnel --url  http://127.0.0.1:5555
```

## What This Does

This command creates a temporary public Cloudflare link for your local service running on:

```text
http://127.0.0.1:5555
```

Use this only for your own local tools, testing, development, and learning.

---

# Kali Linux Installation

## Step 1: Update Kali

```bash
sudo apt update
sudo apt upgrade -y
```

## Step 2: Install Required Tools

```bash
sudo apt install wget curl -y
```

## Step 3: Download cloudflared

For most Kali Linux VMware systems, use the amd64 version:

```bash
wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
```

## Step 4: Install cloudflared

```bash
sudo dpkg -i cloudflared-linux-amd64.deb
```

If you see any dependency error, run:

```bash
sudo apt --fix-broken install -y
```

## Step 5: Check Installation

```bash
cloudflared --version
```

If you see the version number, cloudflared is installed successfully.

---

# Termux Installation

## Step 1: Update Termux

```bash
pkg update -y
pkg upgrade -y
```

## Step 2: Install cloudflared

```bash
pkg install cloudflared -y
```

## Step 3: Check Installation

```bash
cloudflared --version
```

If you see the version number, cloudflared is installed successfully.

---

# Start Localhost Service

Before running Cloudflare Tunnel, your tool must be running on port **5555**.

Example localhost test service:

## Kali Linux

```bash
mkdir my-local-test
cd my-local-test
echo "Cloudflared localhost service is working!" > index.html
python3 -m http.server 5555 --bind 127.0.0.1
```

## Termux

```bash
mkdir my-local-test
cd my-local-test
echo "Cloudflared localhost service is working!" > index.html
python -m http.server 5555 --bind 127.0.0.1
```

Keep this terminal open.

---

# Run Cloudflare Tunnel

Open a new terminal and run:

```bash
cloudflared tunnel --url  http://127.0.0.1:5555
```

After a few seconds, cloudflared will show a public URL like:

```text
https://example.trycloudflare.com
```

Open that link in your browser.

---

# For Your Own Tool

If your tool already starts a web server, make sure it uses:

```text
Host: 127.0.0.1
Port: 5555
```

Example:

```bash
python app.py
```

Then run:

```bash
cloudflared tunnel --url  http://127.0.0.1:5555
```

---

# Common Errors and Fixes

## Error: Unable to locate package cloudflared

On Kali Linux, do not use:

```bash
sudo apt install cloudflared
```

Instead, download the `.deb` file manually:

```bash
wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
sudo dpkg -i cloudflared-linux-amd64.deb
```

## Error: cloudflared.deb no such file

This means the file name is wrong or the file was not downloaded.

Use:

```bash
ls
```

Then install the correct file:

```bash
sudo dpkg -i cloudflared-linux-amd64.deb
```

## Error: Connection refused

This means nothing is running on port 5555.

Start your localhost service first:

```bash
python3 -m http.server 5555 --bind 127.0.0.1
```

Then run:

```bash
cloudflared tunnel --url  http://127.0.0.1:5555
```

## Error: Port already in use

Another app is already using port 5555.

Find the process:

```bash
sudo lsof -i :5555
```

Stop it, or close the terminal where it is running.

---

# Notes

* Keep your localhost service running.
* Keep the cloudflared terminal running.
* The free trycloudflare link changes every time you restart the tunnel.
* This setup is best for testing, learning, and temporary sharing.
* For permanent production hosting, use a proper Cloudflare Tunnel with your own domain.

---

# Final Command

```bash
cloudflared tunnel --url  http://127.0.0.1:5555
```
