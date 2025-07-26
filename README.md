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

# The lab

>[!NOTE]
> WSL creates its own file hierarchy seperate from your windows files, to access the downloaded lab1 folder you should link the windows Downloads folder to a WSL dowloads folder using the command:
>```bash
>ln -s /mnt/c/Users/<windows_username>/Downloads ~/downloads
>#Then
>cd ~/downloads/lab1
>```
## 4. Import the ceos image to docker

Run the following command:

```bash
docker import cEOS-lab-4.32.0F.tar.xz ceos:4.32.0F
```
>[!IMPORTANT]
>Your ```srlceos01.clab.yml``` file should look like this for nslookup and traceroute to work
>```yaml
># topology documentation: http://containerlab.dev/lab-examples/srl-ceos/
>name: srlceos01
>
>topology:
>  nodes:
>    srl:
>      kind: nokia_srlinux
>      image: ghcr.io/nokia/srlinux:24.10
>      dns:
>        servers:
>          - 1.1.1.1
>    ceos:
>      kind: arista_ceos
>      image: ceos:4.32.0F
>      dns:
>        servers:
>          - 1.1.1.1
>
>  links:
>    - endpoints: ["srl:ethernet-1/1", "ceos:eth1"]
>```

## 5. Deploy the nodes

Run the following command:

```bash
sudo containerlab deploy
```

## 6. Connect to the nodes

Run the command:

```bash
docker exec -it clab-srlceos01-srl bash
```

## 7. Test your connectiion

While running wireshark, run these commands on the nodes:

```bash
ping 8.8.8.8 #Google server
nslookup mit.edu
traceroute yahoo.com
```
:::v "Affirmation"
Thats It, You're Done!!
:::

## 8. Shutdown

To power off the nodes run:
```bash
sudo containerlab destroy
```
