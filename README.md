# pxe-boot-server
Building a Server for PXE Boot


## Requirements

- Docker


## Installation

### 1. Clone the repository

```bash
git clone https://github.com/IwasakiYuuki/pxe-boot-server
```

### 2. Create a NFS directory and copy OS image

If needed, you can mount ths ISO image to the directory.
```bash
sudo mount -o loop <path_to_iso> <path_to_os-image>
```

```bash
mkdir -p ./nfs/export
cp -r <path_to_os-image> ./nfs/export
```

### 3. Copy the initrd and vmlinuz files

```bash
cp <path_to_initrd> ./dnsmasq/tftp/images/noble/
cp <path_to_vmlinuz> ./dnsmasq/tftp/images/noble/
```

For Ubuntu 24.04 (noble numbat), the directory containing initrd and vmlinuz is named "noble".
However, you can change this name depending on the OS you want to install, but if you do so, you need to change the name in following files:

- ./dnsmasq/tftp/pxelinux.cfg/default
- ./dnsmasq/tftp/syslinux.cfg/default

```
append initrd=/images/noble/initrd netboot=nfs nfsroot=pxe.home:/ autoinstall ds=nocloud-net;s=http://pxe.home/autoinstall/
```

### 4. Up the server

```bash
docker compose up -d
```


## Configuration

### Disable DNS in dnsmasq

If you don't need DNS, you can disable it by adding below line into ./dnsmasq/dnsmasq.conf

```
port=0
```

### Change the IP address for DNS

In the default configuration, the IP address for DNS is set to

```
192.168.1.10    dns.home        dns
192.168.1.10    pxe.home        pxe
```

You can change the IP address by editing ./dnsmasq/dnsmasq.hosts
