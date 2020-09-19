# Ubuntu 
---

* change hostname

```bash
nano /etc/hostname
nano /etc/hosts
```

* static ip

```bash
nano /etc/network/interfaces
	auto eth0
	iface eth0 inet static
	address 10.0.0.11
	netmask 255.255.255.0
	network 10.0.0.0
	broadcast 10.0.0.255
	gateway 10.0.0.1
```

* keyboard

```bash
sudo apt-get install console-common
```

* ssh

```bash
nano /etc/ssh/sshd_config
   PermitRootLogin yes
service ssh restart
ssh (-X) ( -i private.key) [user@address_ip]
```

* file trasfer

```bash
sftp (-i private.key) [user@address_ip]
mkdir remoteDirectory (same name as local directory)
put -r /.../localDirctory
put /../localFile
get -r /.../remoteDirectory
get /.../remoteFile
- or -
scp [fichier | -r directory] [username]@[address ip]:[DestinationDirectory]
```

* web server

```bash
apt-get install apache2 mysql-server
apt-get install php5 php5-gd php5-mysql
```

* Vérifier la présence d’un paquet

```bash
pkg -l [paquet]
```

* Afficher l’usage de RAM

```bash
watch -n 5 free –m
```

* VMware Player install tools

```bash
mkdir /media/cdrom
mount /dev/cdrom /media/cdrom
tar xzvf /mnt/cdrom/VMwareTools-x.x.x-xxxx.tar.gz -C /home/
./vmware-install.pl -d
```

* Lightweight Ubuntu Desktop

```bash
sudo apt-get install --no-install-recommends ubuntu-desktop
sudo apt-get install gnome-core
```

* bash bin bash M bad interpreter NO such file or directory

```bash
dos2unix file.sh
```

* piix4_smbus 0000:00:007.3: Host SMBus controller not enabled!

```bash
sudo nano /etc/modprobe.d/blacklist.conf
blacklist i2c-piix4
```

* MariaDB allow remote connections

```bash
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'password' WITH GRANT OPTION;
```

* Remote Desktop RDP

```bash
apt-get install xrdp
sudo apt-get install mate-core mate-desktop-environment mate-notification-daemon
echo mate-session >~/.xsession
sudo service xrdp restart
```

* Mount USB

```bash
sudo mount -t ntfs-3g /dev/sdb1 /media/external
```

* Show Disks

```bash
lsblk -o NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL
```
