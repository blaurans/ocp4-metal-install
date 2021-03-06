dans dhcp.conf

``` bash
subnet 192.168.1.0 netmask 255.255.255.0 {
    range 192.168.1.50 192.168.1.99;
    server-name "server";
    next-server 192.168.1.12;
    filename "/srv/tftp/pxelinux.0";
}


yum -y install httpd xinetd syslinux tftp-server
wget http://centos.quelquesmots.fr/7.9.2009/isos/x86_64/CentOS-7-x86_64-Minimal-2009.iso
mount -o loop CentOS-7-x86_64-Minimal-2009.iso /mnt
mkdir /var/www/centos7
cp -a /mnt/* /var/www/centos7/
chmod -R 755 /var/www/centos7/
```

# create the web part
Create a apache configuration file for PXE server under /etc/httpd/conf.d/ directory:

# vi /etc/httpd/conf.d/pxe.conf
Add the following lines:

Alias /centos7 /var/www/centos7/

<Directory /var/www/centos7/>
Options Indexes FollowSymLinks
Order Deny,Allow
Allow from all
</Directory>

``` bash
service httpd restart
wget localhost:8080/centos7
cp -a /usr/share/syslinux/* /var/lib/tftpboot/
mkdir /var/lib/tftpboot/centos7
cp /mnt/images/pxeboot/vmlinuz  /var/lib/tftpboot/centos7
cp /mnt/images/pxeboot/initrd.img  /var/lib/tftpboot/centos7
mkdir /var/lib/tftpboot/pxelinux.cfg

```

vi /var/lib/tftpboot/pxelinux.cfg/default

default menu.c32
prompt 0
timeout 300
ONTIMEOUT 1

menu title ########## CentOS 7 PXE Boot Menu ##########

label 1
menu label ^1) Install CentOS 7
menu default
kernel centos7/vmlinuz
append initrd=centos7/initrd.img method=http://192.168.12.10/centos7 devfs=nomount

label 2
menu label ^2) Boot from local drive
localboot 0

vi /etc/xinetd.d/tftp

 service tftp
{
        socket_type             = dgram
        protocol                = udp
        wait                    = yes
        user                    = root
        server                  = /usr/sbin/in.tftpd
        server_args             = -s /var/lib/tftpboot
        disable                 = no
        per_source              = 11
        cps                     = 100 2
        flags                   = IPv4
}

vi /etc/dhcp/dhcpd.conf
add filename "pxelinux.0"; in subnet at the end


systemctl restart xinetd
systemctl restart dhcpd
systemctl enable xinetd


firewall-cmd --add-port=69/udp --zone=internal --permanent    ## Port for TFTP
firewall-cmd --add-port=69/tcp  --zone=internal --permanent  ## Port for TFTP
firewall-cmd --reload  ## Apply rules

``` bash
dnf install podman
podman run --privileged --pull=always --rm -v .:/data -w /data \
    quay.io/coreos/coreos-installer:release download -f pxe
```
v0.7.2
podman run --privileged --pull=always --rm -v .:/data -w /data \
    quay.io/coreos/coreos-installer:v0.6.0 download -f pxe



pxelinux.cfg
DEFAULT pxeboot
TIMEOUT 20
PROMPT 0
LABEL pxeboot
    KERNEL fedora-coreos-32.20200726.3.1-live-kernel-x86_64
    APPEND initrd=fedora-coreos-32.20200726.3.1-live-initramfs.x86_64.img,fedora-coreos-32.20200726.3.1-live-rootfs.x86_64.img coreos.inst.install_dev=/dev/sda coreos.inst.ignition_url=http://192.168.1.101:8000/config.ign
IPAPPEND 2



fedora-coreos-33.20201201.3.0-live-initramfs.x86_64

cp /mnt/images/pxeboot/vmlinuz  /var/lib/tftpboot/centos7
cp /mnt/images/pxeboot/initrd.img  /var/lib/tftpboot/centos7

http://192.168.22.1:8080/version45GA/bootstrap.ign


/mybootdir/pxelinux.cfg/01-88-99-aa-bb-cc-dd
/mybootdir/pxelinux.cfg/01-88-99-00-11-22-33
/mybootdir/pxelinux.cfg/default

it is important to use as file name starting with 01- then mac address in lowercase

