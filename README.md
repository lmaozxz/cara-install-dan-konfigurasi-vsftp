# cara-install-dan-konfigurasi-vsftp\
# beri 2 adapter seperti biasa yaitu adapter ke dua adalah costum vmnet1 host-only, dan settting ip address nya 
nano /etc/network/interfaces
# contoh ip 192.168.100.1/24 lalu restart networking

# install vsftpd :
apt update && apt install vsftpd -y
systemctl start vsftpd
systemctl status vsftpd #(pastikan running)#

# lalu coppy rule vsftpd ini
cp /etc/vsftpd.conf /etc/vsftpd.conf.orig

# setelah itu buka settingan vsftpd tsbt
nano /etc/vstpd.conf
# ubah aturan nya :
listen=YES
listen_ipv6=NO

# buka pagar dan tambah rule :
chroot_local_user=YES
allow_writeable_chroot=YES
# lalu restart
systemctl restart vsftpd
# lalu buat user untuk testing (testing menggunakan filezilla) 
adduser jamal
# coba ketk perintah ini, seharus nya akan memunculkan nama user yang kita buat, jika tak muncul berarti ada yang salah
echo "jamal" | tee  -a /etc/vsftpd.userlist
