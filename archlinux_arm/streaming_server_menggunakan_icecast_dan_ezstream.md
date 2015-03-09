##Streaming server menggunakan Icecast2 dan Ezstream Raspberry Pi 2

####Installasi dan konfigurasi Icecast2
1.	Install icecast server
        ```
	sudo pacman -Sy icecast
	```

2.	Kemudian modifikasi file konfig di **/etc/icecast.xml**. berikut beberapa baris yang perlu diganti:
	```
        <location>Lokasi_anda</location>
        <admin>email_anda</admin>
        <source-password>isikan_password</source-password>
        <relay-password>isikan_password</relay-password>
        <admin-user>username_untuk_admin_login</admin-user>
        <admin-password>password_untuk_admin_login</admin-password>
        ```

3.	Setelah itu simpan konfigurasi dan jalankan service icecast
	```
	systemctl start icecast
	```

####Installasi dan Konfigurasi Ezstream sebagai musik streamer

1.      untuk menginstall aplikasi Ezstream, maka harus mengkompil manual paketnya
        ```
        wget -c https://aur.archlinux.org/packages/ez/ezstream/ezstream.tar.gz
        tar -xf ezstream.tar.gz
        cd ezstream
        ```

2.      kemudian modifikasi PKGBUILD untuk mengkompilasi ezstream pada perangkat armv7h:
        hanya menambahkan opsi 'armv7h' seperti ini pada PKGBUILD.
        ```
        arch=('i686' 'x86_64' 'armv7h')
        ```

3.      Kemudian install dengan perintah ini:
        ```
        makepkg -si
        ```

4.      Setelah terinstall selanjutnya konfigurasi ezstream:
        ```
        ch playlist.m3u
        cp /usr/share/example/ezstream/ezstream_mp3.xml
        ```

5.      kemudian ubah baris konfigurasi ezstream sesuai dengan konfigurasi icecast yang telah dibuat seperti ini:
        ```
        <sourcepassword>password_sesuai_di_icecast</sourcepassword>
        ```

6.      buat playlist mp3 yang akan di putar dan di stream ke icecast server:
        ```
        touch playlist.m3u
        ```

        dan isikan dengan path lagu yang ada di direktori dimana musik anda tersimpan, contoh:
        ```
        /home/arie/musik/Luke Holland - The woven.mp3
        ```

7.      kemudian jalankan ezstream sehingga lagu yang di playlist akan di stream ke icecast server
        ```
        ezstream -c ezstream_mp3.xml
        ```
        
