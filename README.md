# Install Ubuntu on WSL2

## 1. Install WSL

Open a PowerShell prompt **as an Administrator** and run:

```powershell
wsl --install
```
>[!NOTE]
>Additional Windows features are required for wsl to work
>-open the Control panel
>-go to "turn windows features on or off"
>-select "Windows subsystem for linux", "Virtual machine platform" and "windows Hypervisor platform"
>-reboot

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

# The lab

>[!NOTE]
> WSL creates its own file hierarchy seperate from your windows files, to access the downloaded lab1 folder you should link the windows Downloads folder to a WSL dowloads folder using the command:
>```bash
>ln -s /mnt/c/Users/<windows_username>/Downloads ~/downloads
>#Then
>cd ~/downloads/lab1
>```
## 4. Import the ceos image to docker

In your lab1 directory run the following command:

```bash
docker import cEOS-lab-4.32.0F.tar.xz ceos:4.32.0F
```

## 5. Deploy the nodes

Run the following command:

```bash
sudo containerlab deploy
```

## 6. Connect to the nodes

Run the command:

```bash
docker exec -it clab-srlceos01-ceos bash
```

## 7. Add DNS server

Open dnsmasq config file
```bash
sudo nano /etc/dnsmasq.conf
```
add this line:

```bash
server=1.1.1.1
```
restart dnsmasq

```bash
sudo systemctl restart dnmasq
```

# 8. Test your connection

While running wireshark, run these commands on the nodes:

```bash
ping 8.8.8.8 #Google server
nslookup mit.edu
traceroute yahoo.com
```
🔥 Thats It, You're Done!! 👏

## 8. Shutdown

To power off the nodes run:
```bash
sudo containerlab destroy
```
