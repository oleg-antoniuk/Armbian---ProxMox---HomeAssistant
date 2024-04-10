# Armbian---ProxMox---HomeAssistant




### 1. Install Armbian on TVbox:
       https://github.com/devmfc/debian-on-amlogic

** **

### 2. Install ProxMox(PiMox)
       https://mirrors.apqa.cn

#####  1) Download port gpg key:
          curl -L https://mirrors.apqa.cn/proxmox/debian/pveport.gpg -o /etc/apt/trusted.gpg.d/pveport.gpg

#####  2) Add address to sources.list:
          echo "deb https://mirrors.apqa.cn/proxmox/debian/pve bookworm port">/etc/apt/sources.list.d/pveport.list

#####  3) Do apt update:
          apt update

#####  4) Install proxmox(pimox):
          apt install proxmox-ve
** **

### 3. ProxMox(PiMox) script:
####   Home Assistant OS VM:
          bash -c "$(wget -qLO - https://github.com/tteck/Proxmox/raw/main/vm/pimox-haos-vm.sh)"

** **

#### troubleshooting
