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

## 3. Install Docker

Copy and paste the following into your terminal:

```bash
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo \"${UBUNTU_CODENAME:-$VERSION_CODENAME}\") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## 4. Install Containerlab

Run the following command:

```bash
curl -sL https://containerlab.dev/setup | sudo -E bash -s "all"
```
