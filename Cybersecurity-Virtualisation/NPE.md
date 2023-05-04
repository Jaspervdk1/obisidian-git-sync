
# Debian VM

```
VBoxManage createvm --name "Debian" --ostype "Debian_64" --register

VBoxManage modifyvm "Debian" --memory 2048 --vram 128 --graphicscontroller vmsvga --nic1 nat --nic2 intnet

VBoxManage modifyvm "Debian" 

VBoxManage storagectl "Debian" --name "SATA Controller" --add sata --controller IntelAhci

VBoxManage storageattach "Debian" --storagectl "SATA Controller" --port 0 --device 0 --type hdd --medium ".\Debian 11 (64bit).vdi"

```

# Kali VM

```
VBoxManage createvm --name "Kali Linux" --ostype "Linux_64" --register

VBoxManage modifyvm "Kali Linux" --memory 2048 --vram 128 --graphicscontroller vmsvga --nic1  nat --nic2 intnet

VBoxManage storagectl "Kali Linux" --name "SATA Controller" --add sata --controller IntelAhci

VBoxManage storageattach "Kali Linux" --storagectl "SATA Controller" --port 0 --device 0 --type hdd --medium ".\Kali Linux 2022.3 (64bit).vdi"

```
