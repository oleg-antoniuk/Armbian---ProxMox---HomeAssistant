# Armbian---ProxMox---HomeAssistant
     bullseye



### 1. Install Armbian on TVbox:
       https://github.com/devmfc/debian-on-amlogic
       https://github.com/ophub/amlogic-s9xxx-armbian

** **

### 2. Install ProxMox(PiMox)
       https://mirrors.apqa.cn

#####  1) Download port gpg key:
          curl -L https://mirrors.apqa.cn/proxmox/debian/pveport.gpg -o /etc/apt/trusted.gpg.d/pveport.gpg

#####  2) Add address to sources.list:
          echo "deb https://mirrors.apqa.cn/proxmox/debian/pve bullseye port">/etc/apt/sources.list.d/pveport.list

#####  3) Do apt update:
          apt update

#####  4) Install proxmox(pimox):
          apt install proxmox-ve
** **

### 3. ProxMox(PiMox) script:
####   Home Assistant OS VM:
          bash -c "$(wget -qLO - https://github.com/tteck/Proxmox/raw/main/vm/pimox-haos-vm.sh)"

** **

### troubleshooting:

###### bridge 'vmbr0' does not exist
###### kvm: -netdev type=tap,id=net0,ifname=tap100i0,script=/var/lib/qemu-server/pve-bridge,downscript=/var/lib/qemu-server/pve-bridgedown: network script /var/lib/qemu-server/pve-bridge failed with status 512
###### TASK ERROR: start failed: QEMU exited with code 1
       https://itfb.com.ua/oshibka-pri-zapuske-virtualnoy-mashiny-bridge-vmbr0-does-not-exist/
       https://www.altlinux.org/Systemd-networkd
       https://wiki.archlinux.org/title/systemd-networkd_(Русский)
---
###### error /etc/pve/local/pve-ssl.pem: failed to use local certificate chain (cert_file or cert) at /usr/share/perl5/PVE/APIServer/AnyEvent.pm line 1998.

       https://pve.proxmox.com/wiki/Proxmox_SSL_Error_Fixing

===
===
TorrentBoxInstall
===
Установка торрент БОКС (торрент качалка) на одноплатном компьютере Orange Pi или Banana PI.

Торрент клиент с веб интефейсом и удаленным доступом  - qbittorrent.

Установка:
sudo apt-get install  qbittorrent-nox

После установки соглашаемся с предупреждением.
По-умолчанию адрес веб интерфейса localhost:8080
Логин: admin
Пароль: adminadmin

Создадим службу
sudo nano /etc/systemd/system/qbittorrent.service

В пустой файл вставляем настройки:

[Unit]
Description=qBittorrent Daemon Service
After=network.target

[Service]
User=ВАШ ПОЛЬЗОВАТЕЛЬ
ExecStart=/usr/bin/qbittorrent-nox
ExecStop=/usr/bin/killall -w qbittorrent-nox

[Install]
WantedBy=multi-user.target

Перезагрузим даймон
sudo systemctl daemon-reload

Запустим сервис qbittorrent
sudo systemctl start qbittorrent

Что бы остановить сервис qbittorrent
sudo systemctl stop qbittorrent

Для скачивание торрентов на USB флешку или внешний USB, нужно сделать автомонтирование при подключении к USB

Автомонтирование  USB накопителя:
sudo fdisk -l
sudo mkdir /media/andrey
sudo mount /dev/sda1 /media/andrey

sudo nano /etc/fstab
/dev/sda1 /media/andrey auto defaults,nofail
