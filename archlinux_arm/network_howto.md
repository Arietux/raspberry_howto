##Konfigurasi jaringan di Archlinux Arm 

####Konfigurasi Jaringan Static
1.	Pertama kali matikan servis systemd-networkd.service
	```
	systemctl disable systemd-networkd.service
	```
2.	Kemudian buat konfigurasi jaringan statik
	```
	cd /etc/netctl
	cp example/ethernet-static eth0
	```
	untuk konfigurasi bisa di sesuaikan sendiri:
	```
	Description='My raspi network'
	Interface=eth0
	Connection=ethernet

	AutoWired=yes
	
	IP=static
	Address=('192.168.1.21/24')
	#Routes=('192.168.0.0/24 via 192.168.1.2')
	Gateway='192.168.1.5'
	DNS=('8.8.8.8' '8.8.4.4')
	```
setelah itu simpan dan jalankan profile yang telah dibuat :
	```
	netctl start eth0 && netctl enable eth0
	```

####Konfigurasi Jaringan ethernet Dinamik
1.	buat konfigurasi jaringan ethernet dinamik
	```
	cd /etc/netctl
	cp example/ethernet-dhcp eth0dhcp
	```
2.	kemudian modifikasi konfigurasi seperti ini:
	```
	Description='A basic dhcp ethernet connection'
	Interface=eth0
	Connection=ethernet
	IP=dhcp
	DHCPClient=dhcpcd
	```
3.	sebelum menjalankan profile dhcp, matikan terlebih dahulu profile statik yang lagi berjalan
	```
	netctl stop eth0 && netctl disable eth0
	```
	kemudian jalankan profile dhcp
	```
	netctl eth0dhcp && netctl enable eth0dhcp
	```
