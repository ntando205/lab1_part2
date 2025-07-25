# Install Ubuntu on WSL2

## 1. Install WSL

Open a PowerShell prompt **as an Administrator** and run:

```powershell
wsl --install
```

## 2. Install Ubuntu

Go to the **Microsoft Store**, search for and install **"Ubuntu 24.04 LTS"** (or the latest LTS).

Open Ubuntu and run the following commands:

```bash
sudo apt-get update
sudo apt-get full-upgrade -y  # This might take a while
```

## 3. Install Docker & Containerlab

Run the following command:

```bash
curl -sL https://containerlab.dev/setup | sudo -E bash -s "all"
```
