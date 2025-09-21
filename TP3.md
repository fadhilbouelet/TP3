

# TP3 : Cloud privé

## I. Présentation du lab
🌞 Allumez les VMs et effectuez la conf élémentaire :

    🌞adresse IP statique
    définition du nom de domaine avec hostnamectl
    vous remplirez les fichiers /etc/hosts des trois machines pour qu'elles se joignent avec leurs noms

    🌞 le compte-rendu, j'veux juste :
        ping kvm1.one depuis frontend.one
        ping kvm2.one depuis frontend.one

```
[user1@localhost ~]$ ip a show enp0s8
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:da:49:c8 brd ff:ff:ff:ff:ff:ff
    inet 10.3.1.10/24 brd 10.3.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
[user1@localhost ~]$ ping -c 4 10.3.1.11   # Test vers kvm1.one
0.3.1.12PING 10.3.1.11 (10.3.1.11) 56(84) bytes of data.
64 bytes from 10.3.1.11: icmp_seq=1 ttl=64 time=1.01 ms
   # Test vers kvm2.one
64 bytes from 10.3.1.11: icmp_seq=2 ttl=64 time=2.15 ms
64 bytes from 10.3.1.11: icmp_seq=3 ttl=64 time=2.67 ms
64 bytes from 10.3.1.11: icmp_seq=4 ttl=64 time=1.60 ms

--- 10.3.1.11 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3007ms
rtt min/avg/max/mdev = 1.014/1.858/2.673/0.617 ms
[user1@localhost ~]$ ping -c 4 10.3.1.12   # Test vers kvm2.one
PING 10.3.1.12 (10.3.1.12) 56(84) bytes of data.
64 bytes from 10.3.1.12: icmp_seq=1 ttl=64 time=3.03 ms
64 bytes from 10.3.1.12: icmp_seq=2 ttl=64 time=2.05 ms
64 bytes from 10.3.1.12: icmp_seq=3 ttl=64 time=1.70 ms
64 bytes from 10.3.1.12: icmp_seq=4 ttl=64 time=1.84 ms

--- 10.3.1.12 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3005ms
rtt min/avg/max/mdev = 1.701/2.155/3.032/0.521 ms






[user1@localhost ~]$ ping -c 4 kvm1.one
ping: kvm1.one: Name or service not known
[user1@localhost ~]$ ping -c 4 kvm2.one
PING kvm2.one(kvm2.one (fe80::a00:27ff:fe91:dc5c%enp0s3)) 56 data bytes
64 bytes from kvm2.one (fe80::a00:27ff:fe91:dc5c%enp0s3): icmp_seq=1 ttl=64 time=0.121 ms
64 bytes from kvm2.one (fe80::a00:27ff:fe91:dc5c%enp0s3): icmp_seq=2 ttl=64 time=0.264 ms
64 bytes from kvm2.one (fe80::a00:27ff:fe91:dc5c%enp0s3): icmp_seq=3 ttl=64 time=0.297 ms
64 bytes from kvm2.one (fe80::a00:27ff:fe91:dc5c%enp0s3): icmp_seq=4 ttl=64 time=0.198 ms

--- kvm2.one ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3007ms
rtt min/avg/max/mdev = 0.121/0.220/0.297/0.067 ms





[user1@localhost ~]$ sudo vim /etc/hosts
[user1@localhost ~]$ ping -c 4 frontend
PING frontend (10.3.1.10) 56(84) bytes of data.
64 bytes from frontend (10.3.1.10): icmp_seq=1 ttl=64 time=1.42 ms
64 bytes from frontend (10.3.1.10): icmp_seq=2 ttl=64 time=1.92 ms
64 bytes from frontend (10.3.1.10): icmp_seq=3 ttl=64 time=1.41 ms
64 bytes from frontend (10.3.1.10): icmp_seq=4 ttl=64 time=1.32 ms

--- frontend ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3007ms
rtt min/avg/max/mdev = 1.317/1.517/1.921/0.236 ms





[user1@localhost ~]$ ping -c 4 kvm1
PING kvm1 (10.3.1.11) 56(84) bytes of data.
64 bytes from kvm1 (10.3.1.11): icmp_seq=1 ttl=64 time=0.064 ms
64 bytes from kvm1 (10.3.1.11): icmp_seq=2 ttl=64 time=0.609 ms
64 bytes from kvm1 (10.3.1.11): icmp_seq=3 ttl=64 time=0.123 ms
64 bytes from kvm1 (10.3.1.11): icmp_seq=4 ttl=64 time=0.145 ms

--- kvm1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3070ms
rtt min/avg/max/mdev = 0.064/0.235/0.609/0.217 ms
[user1@localhost ~]$





Last login: Tue Sep 16 16:45:48 2025
[user1@localhost ~]$ sudo vim /etc/hosts
[sudo] password for user1:
[user1@localhost ~]$ ^C
[user1@localhost ~]$ pinc -c 4 frontend
-bash: pinc: command not found
[user1@localhost ~]$ ping -c 4 frontend
PING frontend (10.3.1.10) 56(84) bytes of data.
64 bytes from frontend (10.3.1.10): icmp_seq=1 ttl=64 time=0.420 ms
64 bytes from frontend (10.3.1.10): icmp_seq=2 ttl=64 time=1.31 ms
64 bytes from frontend (10.3.1.10): icmp_seq=3 ttl=64 time=1.49 ms
64 bytes from frontend (10.3.1.10): icmp_seq=4 ttl=64 time=1.64 ms

--- frontend ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3007ms
rtt min/avg/max/mdev = 0.420/1.214/1.635/0.472 ms
[user1@localhost ~]$ ping -c kvm1
ping: invalid argument: 'kvm1'
[user1@localhost ~]$ ping -c 4 kvm1
PING kvm1 (10.3.1.11) 56(84) bytes of data.
64 bytes from kvm1 (10.3.1.11): icmp_seq=1 ttl=64 time=0.762 ms
64 bytes from kvm1 (10.3.1.11): icmp_seq=2 ttl=64 time=1.32 ms
64 bytes from kvm1 (10.3.1.11): icmp_seq=3 ttl=64 time=0.598 ms
64 bytes from kvm1 (10.3.1.11): icmp_seq=4 ttl=64 time=0.416 ms

--- kvm1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3049ms
rtt min/avg/max/mdev = 0.416/0.774/1.323/0.339 ms

```



# II.1. Setup Frontend

## A. Database¶

🌞Installer un serveur MySQL

    🌞on va installer une version spécifique de MySQL, demandée par OpenNebula

    🌞ajouter un dépôt :
        télécharger le RPM disponible à l'URL suivante : https://dev.mysql.com/get/mysql80-community-release-el9-5.noarch.rpm
        puis installez-le localement avec une commande rpm

    🌞installer le paquet qui contient le serveur MySQL depuis ce nouveau dépôt :
        faites un dnf search mysql pour voir les paquets dispos
        vous devriez voir un paquet mysql-community-server dispo
        installez-le

## etapes

### 1) Mise à jour et installation de wget

```
[user1@frontend ~]$ sudo dnf update -y
[sudo] password for user1:
fSorry, try again.
a[sudo] password for user1:
Last metadata expiration check: 0:12:56 ago on Tue Sep 16 18:02:45 2025.
Dependencies resolved.
========================================================================================================================
 Package                         Architecture              Version                        Repository               Size
========================================================================================================================
Upgrading:
 epel-release                    noarch                    9-10.el9                       epel                     19 k

Transaction Summary
========================================================================================================================
Upgrade  1 Package

Total download size: 19 k
Downloading Packages:
epel-release-9-10.el9.noarch.rpm                                                         49 kB/s |  19 kB     00:00
------------------------------------------------------------------------------------------------------------------------
Total                                                                                    21 kB/s |  19 kB     00:00
Extra Packages for Enterprise Linux 9 - x86_64                                          1.6 MB/s | 1.6 kB     00:00
Importing GPG key 0x3228467C:
 Userid     : "Fedora (epel9) <epel@fedoraproject.org>"
 Fingerprint: FF8A D134 4597 106E CE81 3B91 8A38 72BF 3228 467C
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-9
Key imported successfully
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                1/1
  Upgrading        : epel-release-9-10.el9.noarch                                                                   1/2
  Running scriptlet: epel-release-9-10.el9.noarch                                                                   1/2
  Cleanup          : epel-release-9-7.el9.noarch                                                                    2/2
  Running scriptlet: epel-release-9-7.el9.noarch                                                                    2/2
  Verifying        : epel-release-9-10.el9.noarch                                                                   1/2
  Verifying        : epel-release-9-7.el9.noarch                                                                    2/2

Upgraded:
  epel-release-9-10.el9.noarch

Complete!
```

## 2) je Télécharge le RPM du dépôt MySQL

```
[user1@frontend ~]$ sudo wget -O /tmp/mysql80-community-release-el9-5.noarch.rpm \
>   https://dev.mysql.com/get/mysql80-community-release-el9-5.noarch.rpm
--2025-09-16 18:17:54--  https://dev.mysql.com/get/mysql80-community-release-el9-5.noarch.rpm
Resolving dev.mysql.com (dev.mysql.com)... 104.85.37.194, 2a02:26f0:9100:13a3::2e31, 2a02:26f0:9100:1387::2e31
Connecting to dev.mysql.com (dev.mysql.com)|104.85.37.194|:443... connected.
HTTP request sent, awaiting response... 302 Moved Temporarily
Location: https://repo.mysql.com//mysql80-community-release-el9-5.noarch.rpm [following]
--2025-09-16 18:17:56--  https://repo.mysql.com//mysql80-community-release-el9-5.noarch.rpm
Resolving repo.mysql.com (repo.mysql.com)... 104.85.20.87, 2a02:26f0:b80:79c::1d68, 2a02:26f0:b80:781::1d68
Connecting to repo.mysql.com (repo.mysql.com)|104.85.20.87|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 13319 (13K) [application/x-redhat-package-manager]
Saving to: ‘/tmp/mysql80-community-release-el9-5.noarch.rpm’

/tmp/mysql80-community-releas 100%[=================================================>]  13.01K  --.-KB/s    in 0s

2025-09-16 18:17:56 (83.5 MB/s) - ‘/tmp/mysql80-community-release-el9-5.noarch.rpm’ saved [13319/13319]
```
#### je verifie que le fichier est present

```
[user1@frontend ~]$ ls -lh /tmp/mysql80-community-release-el9-5.noarch.rpm
-rw-r--r--. 1 root root 14K Oct 24  2023 /tmp/mysql80-community-release-el9-5.noarch.rpm
```

## 3) Installer le RPM

```
[user1@frontend ~]$ sudo rpm -Uvh /tmp/mysql80-community-release-el9-5.noarch.rpm
warning: /tmp/mysql80-community-release-el9-5.noarch.rpm: Header V4 RSA/SHA256 Signature, key ID 3a79bd29: NOKEY
Verifying...                          ################################# [100%]
Preparing...                          ################################# [100%]
Updating / installing...
   1:mysql80-community-release-el9-5  ################################# [100%]
```

## 4)j'Installe le serveur MySQL

```
[user1@frontend ~]$ sudo dnf install -y mysql-community-server
Last metadata expiration check: 0:03:06 ago on Tue Sep 16 18:26:37 2025.
Dependencies resolved.
========================================================================================================================
 Package                                Architecture   Version                          Repository                 Size
========================================================================================================================
Installing:
 mysql-community-server                 x86_64         8.0.43-1.el9                     mysql80-community          50 M
Installing dependencies:
mysql-community-client                 x86_64         8.0.43-1.el9                     mysql80-community         3.3 M
 mysql-community-client-plugins         x86_64         8.0.43-1.el9                     mysql80-community         1.4 M
 mysql-community-common                 x86_64         8.0.43-1.el9                     mysql80-community         556 k
 mysql-community-icu-data-files         x86_64         8.0.43-1.el9                     mysql80-community         2.3 M
 mysql-community-libs                   x86_64         8.0.43-1.el9                     mysql80-community         1.5 M
 net-tools                              x86_64         2.0-0.64.20160912git.el9         baseos                    294 k
 perl-AutoLoader                        noarch         5.74-481.1.el9_6                 appstream                  20 k
 perl-B                                 x86_64         1.80-481.1.el9_6                 appstream                 178 k
 perl-Carp                              noarch         1.50-460.el9                     appstream                  29 k
 perl-Class-Struct                      noarch         0.66-481.1.el9_6                 appstream                  21 k
 perl-Data-Dumper                       x86_64         2.174-462.el9                    appstream                  55 k
 perl-Digest                            noarch         1.19-4.el9                       appstream                  25 k
 perl-Digest-MD5                        x86_64         2.58-4.el9                       appstream                  36 k
 perl-Encode                            x86_64         4:3.08-462.el9                   appstream                 1.7 M
 perl-Errno                             x86_64         1.30-481.1.el9_6                 appstream                  13 k
 perl-Exporter                          noarch         5.74-461.el9                     appstream                  31 k
 perl-Fcntl                             x86_64         1.13-481.1.el9_6                 appstream                  19 k
 perl-File-Basename                     noarch         2.85-481.1.el9_6                 appstream                  16 k
 perl-File-Path                         noarch         2.18-4.el9                       appstream                  35 k
 perl-File-Temp                         noarch         1:0.231.100-4.el9                appstream                  59 k
 perl-File-stat                         noarch         1.09-481.1.el9_6                 appstream                  16 k
 perl-FileHandle                        noarch         2.03-481.1.el9_6                 appstream                  14 k
 perl-Getopt-Long                       noarch         1:2.52-4.el9                     appstream                  60 k
 perl-Getopt-Std                        noarch         1.12-481.1.el9_6                 appstream                  14 k
 perl-HTTP-Tiny                         noarch         0.076-462.el9                    appstream                  53 k
 perl-IO                                x86_64         1.43-481.1.el9_6                 appstream                  85 k
 perl-IO-Socket-IP                      noarch         0.41-5.el9                       appstream                  42 k
 perl-IO-Socket-SSL                     noarch         2.073-2.el9                      appstream                 214 k
 perl-IPC-Open3                         noarch         1.21-481.1.el9_6                 appstream                  21 k
 perl-MIME-Base64                       x86_64         3.16-4.el9                       appstream                  30 k
 perl-Mozilla-CA                        noarch         20200520-6.el9                   appstream                  12 k
 perl-Net-SSLeay                        x86_64         1.94-1.el9                       appstream                 391 k
 perl-POSIX                             x86_64         1.94-481.1.el9_6                 appstream                  95 k
 perl-PathTools                         x86_64         3.78-461.el9                     appstream                  85 k
 perl-Pod-Escapes                       noarch         1:1.07-460.el9                   appstream                  20 k
 perl-Pod-Perldoc                       noarch         3.28.01-461.el9                  appstream                  83 k
 perl-Pod-Simple                        noarch         1:3.42-4.el9                     appstream                 215 k
 perl-Pod-Usage                         noarch         4:2.01-4.el9                     appstream                  40 k
 perl-Scalar-List-Utils                 x86_64         4:1.56-462.el9                   appstream                  70 k
 perl-SelectSaver                       noarch         1.02-481.1.el9_6                 appstream                  10 k
 perl-Socket                            x86_64         4:2.031-4.el9                    appstream                  54 k
 perl-Storable                          x86_64         1:3.21-460.el9                   appstream                  95 k
 perl-Symbol                            noarch         1.08-481.1.el9_6                 appstream                  13 k
 perl-Term-ANSIColor                    noarch         5.01-461.el9                     appstream                  48 k
 perl-Term-Cap                          noarch         1.17-460.el9                     appstream                  22 k
 perl-Text-ParseWords                   noarch         3.30-460.el9                     appstream                  16 k
 perl-Text-Tabs+Wrap                    noarch         2013.0523-460.el9                appstream                  23 k
 perl-Time-Local                        noarch         2:1.300-7.el9                    appstream                  33 k
 perl-URI                               noarch         5.09-3.el9                       appstream                 108 k
 perl-base                              noarch         2.27-481.1.el9_6                 appstream                  15 k
 perl-constant                          noarch         1.33-461.el9                     appstream                  23 k
 perl-if                                noarch         0.60.800-481.1.el9_6             appstream                  13 k
 perl-interpreter                       x86_64         4:5.32.1-481.1.el9_6             appstream                  69 k
 perl-libnet                            noarch         3.13-4.el9                       appstream                 125 k
 perl-libs                              x86_64         4:5.32.1-481.1.el9_6             appstream                 2.0 M
 perl-mro                               x86_64         1.23-481.1.el9_6                 appstream                  27 k
 perl-overload                          noarch         1.31-481.1.el9_6                 appstream                  44 k
 perl-overloading                       noarch         0.02-481.1.el9_6                 appstream                  11 k
 perl-parent                            noarch         1:0.238-460.el9                  appstream                  14 k
 perl-podlators                         noarch         1:4.14-460.el9                   appstream                 112 k
 perl-subs                              noarch         1.03-481.1.el9_6                 appstream                  10 k
 perl-vars                              noarch         1.05-481.1.el9_6                 appstream                  12 k
Installing weak dependencies:
 perl-NDBM_File                         x86_64         1.15-481.1.el9_6                 appstream                  21 k

Transaction Summary
========================================================================================================================
Install  65 Packages

Total download size: 66 M
Installed size: 363 M
Downloading Packages:
(1/65): mysql-community-common-8.0.43-1.el9.x86_64.rpm                                  988 kB/s | 556 kB     00:00
(2/65): mysql-community-client-plugins-8.0.43-1.el9.x86_64.rpm                          1.4 MB/s | 1.4 MB     00:01
(3/65): mysql-community-client-8.0.43-1.el9.x86_64.rpm                                  3.2 MB/s | 3.3 MB     00:01
(4/65): mysql-community-libs-8.0.43-1.el9.x86_64.rpm                                    3.2 MB/s | 1.5 MB     00:00
(5/65): mysql-community-icu-data-files-8.0.43-1.el9.x86_64.rpm                          1.7 MB/s | 2.3 MB     00:01
(6/65): libtirpc-1.3.3-9.el9.x86_64.rpm                                                  22 kB/s |  93 kB     00:04
(7/65): mysql-community-server-8.0.43-1.el9.x86_64.rpm                                  7.5 MB/s |  50 MB     00:06
(8/65): net-tools-2.0-0.64.20160912git.el9.x86_64.rpm                                    48 kB/s | 294 kB     00:06
(9/65): perl-Getopt-Long-2.52-4.el9.noarch.rpm                                           39 kB/s |  60 kB     00:01
(10/65): perl-Term-Cap-1.17-460.el9.noarch.rpm                                          192 kB/s |  22 kB     00:00
(11/65): perl-NDBM_File-1.15-481.1.el9_6.x86_64.rpm                                     139 kB/s |  21 kB     00:00
(12/65): perl-Pod-Escapes-1.07-460.el9.noarch.rpm                                       128 kB/s |  20 kB     00:00
(13/65): perl-vars-1.05-481.1.el9_6.noarch.rpm                                           83 kB/s |  12 kB     00:00
(14/65): perl-parent-0.238-460.el9.noarch.rpm                                           114 kB/s |  14 kB     00:00
(15/65): perl-Net-SSLeay-1.94-1.el9.x86_64.rpm                                          1.2 MB/s | 391 kB     00:00
(16/65): perl-Socket-2.031-4.el9.x86_64.rpm                                             167 kB/s |  54 kB     00:00
(17/65): perl-B-1.80-481.1.el9_6.x86_64.rpm                                             666 kB/s | 178 kB     00:00
(18/65): perl-URI-5.09-3.el9.noarch.rpm                                                 593 kB/s | 108 kB     00:00
(19/65): perl-Scalar-List-Utils-1.56-462.el9.x86_64.rpm                                 431 kB/s |  70 kB     00:00
(20/65): perl-base-2.27-481.1.el9_6.noarch.rpm                                          140 kB/s |  15 kB     00:00
(21/65): perl-Getopt-Std-1.12-481.1.el9_6.noarch.rpm                                    171 kB/s |  14 kB     00:00
(22/65): perl-PathTools-3.78-461.el9.x86_64.rpm                                         851 kB/s |  85 kB     00:00
(23/65): perl-Pod-Perldoc-3.28.01-461.el9.noarch.rpm                                    706 kB/s |  83 kB     00:00
(24/65): perl-HTTP-Tiny-0.076-462.el9.noarch.rpm                                        560 kB/s |  53 kB     00:00
(25/65): perl-Digest-1.19-4.el9.noarch.rpm                                              254 kB/s |  25 kB     00:00
(26/65): perl-File-Basename-2.85-481.1.el9_6.noarch.rpm                                 172 kB/s |  16 kB     00:00
(27/65): perl-Exporter-5.74-461.el9.noarch.rpm                                          159 kB/s |  31 kB     00:00
(28/65): perl-subs-1.03-481.1.el9_6.noarch.rpm                                           59 kB/s |  10 kB     00:00
(29/65): perl-MIME-Base64-3.16-4.el9.x86_64.rpm                                         171 kB/s |  30 kB     00:00
(30/65): perl-AutoLoader-5.74-481.1.el9_6.noarch.rpm                                    214 kB/s |  20 kB     00:00
(31/65): perl-Fcntl-1.13-481.1.el9_6.x86_64.rpm                                         184 kB/s |  19 kB     00:00
(32/65): perl-Text-Tabs+Wrap-2013.0523-460.el9.noarch.rpm                               169 kB/s |  23 kB     00:00
(33/65): perl-overload-1.31-481.1.el9_6.noarch.rpm                                      429 kB/s |  44 kB     00:00
(34/65): perl-SelectSaver-1.02-481.1.el9_6.noarch.rpm                                    83 kB/s |  10 kB     00:00
(35/65): perl-IO-1.43-481.1.el9_6.x86_64.rpm                                            665 kB/s |  85 kB     00:00
(36/65): perl-if-0.60.800-481.1.el9_6.noarch.rpm                                        147 kB/s |  13 kB     00:00
(37/65): perl-FileHandle-2.03-481.1.el9_6.noarch.rpm                                    132 kB/s |  14 kB     00:00
(38/65): perl-POSIX-1.94-481.1.el9_6.x86_64.rpm                                         779 kB/s |  95 kB     00:00
(39/65): perl-podlators-4.14-460.el9.noarch.rpm                                         868 kB/s | 112 kB     00:00
(40/65): perl-File-Path-2.18-4.el9.noarch.rpm                                           393 kB/s |  35 kB     00:00
(41/65): perl-File-stat-1.09-481.1.el9_6.noarch.rpm                                     177 kB/s |  16 kB     00:00
(42/65): perl-Storable-3.21-460.el9.x86_64.rpm                                          815 kB/s |  95 kB     00:00
(43/65): perl-Symbol-1.08-481.1.el9_6.noarch.rpm                                        108 kB/s |  13 kB     00:00
(44/65): perl-Data-Dumper-2.174-462.el9.x86_64.rpm                                      499 kB/s |  55 kB     00:00
(45/65): perl-Errno-1.30-481.1.el9_6.x86_64.rpm                                         111 kB/s |  13 kB     00:00
(46/65): perl-File-Temp-0.231.100-4.el9.noarch.rpm                                      465 kB/s |  59 kB     00:00
(47/65): perl-Pod-Simple-3.42-4.el9.noarch.rpm                                          1.3 MB/s | 215 kB     00:00
(48/65): perl-Digest-MD5-2.58-4.el9.x86_64.rpm                                          289 kB/s |  36 kB     00:00
(49/65): perl-Term-ANSIColor-5.01-461.el9.noarch.rpm                                    394 kB/s |  48 kB     00:00
(50/65): perl-Mozilla-CA-20200520-6.el9.noarch.rpm                                      119 kB/s |  12 kB     00:00
(51/65): perl-Pod-Usage-2.01-4.el9.noarch.rpm                                           325 kB/s |  40 kB     00:00
(52/65): perl-Class-Struct-0.66-481.1.el9_6.noarch.rpm                                  122 kB/s |  21 kB     00:00
(53/65): perl-IO-Socket-SSL-2.073-2.el9.noarch.rpm                                      1.0 MB/s | 214 kB     00:00
(54/65): perl-Carp-1.50-460.el9.noarch.rpm                                              235 kB/s |  29 kB     00:00
(55/65): perl-Time-Local-1.300-7.el9.noarch.rpm                                         333 kB/s |  33 kB     00:00
(56/65): perl-IPC-Open3-1.21-481.1.el9_6.noarch.rpm                                     209 kB/s |  21 kB     00:00
(57/65): perl-libnet-3.13-4.el9.noarch.rpm                                              1.1 MB/s | 125 kB     00:00
(58/65): perl-libs-5.32.1-481.1.el9_6.x86_64.rpm                                        3.7 MB/s | 2.0 MB     00:00
(59/65): perl-overloading-0.02-481.1.el9_6.noarch.rpm                                    23 kB/s |  11 kB     00:00
(60/65): perl-Encode-3.08-462.el9.x86_64.rpm                                            2.0 MB/s | 1.7 MB     00:00
(61/65): perl-constant-1.33-461.el9.noarch.rpm                                           72 kB/s |  23 kB     00:00
(62/65): perl-Text-ParseWords-3.30-460.el9.noarch.rpm                                    53 kB/s |  16 kB     00:00
(63/65): perl-mro-1.23-481.1.el9_6.x86_64.rpm                                           236 kB/s |  27 kB     00:00
(64/65): perl-interpreter-5.32.1-481.1.el9_6.x86_64.rpm                                 517 kB/s |  69 kB     00:00
(65/65): perl-IO-Socket-IP-0.41-5.el9.noarch.rpm                                        297 kB/s |  42 kB     00:00
------------------------------------------------------------------------------------------------------------------------
Total                                                                                   5.6 MB/s |  66 MB     00:11
MySQL 8.0 Community Server                                                              3.0 MB/s | 3.1 kB     00:00
Importing GPG key 0xA8D3785C:
 Userid     : "MySQL Release Engineering <mysql-build@oss.oracle.com>"
 Fingerprint: BCA4 3417 C3B4 85DD 128E C6D4 B7B3 B788 A8D3 785C
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-mysql-2023
Key imported successfully
MySQL 8.0 Community Server                                                              3.0 MB/s | 3.1 kB     00:00
Importing GPG key 0x3A79BD29:
 Userid     : "MySQL Release Engineering <mysql-build@oss.oracle.com>"
 Fingerprint: 859B E8D7 C586 F538 430B 19C2 467B 942D 3A79 BD29
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-mysql-2022
Key imported successfully
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                1/1
  Installing       : perl-Digest-1.19-4.el9.noarch                                                                 1/65
  Installing       : perl-Digest-MD5-2.58-4.el9.x86_64                                                             2/65
  Installing       : perl-B-1.80-481.1.el9_6.x86_64                                                                3/65
  Installing       : perl-FileHandle-2.03-481.1.el9_6.noarch                                                       4/65
  Installing       : perl-Data-Dumper-2.174-462.el9.x86_64                                                         5/65
  Installing       : perl-libnet-3.13-4.el9.noarch                                                                 6/65
  Installing       : perl-base-2.27-481.1.el9_6.noarch                                                             7/65
  Installing       : perl-AutoLoader-5.74-481.1.el9_6.noarch                                                       8/65
  Installing       : perl-URI-5.09-3.el9.noarch                                                                    9/65
  Installing       : perl-if-0.60.800-481.1.el9_6.noarch                                                          10/65
  Installing       : perl-Pod-Escapes-1:1.07-460.el9.noarch                                                       11/65
  Installing       : perl-Text-Tabs+Wrap-2013.0523-460.el9.noarch                                                 12/65
  Installing       : perl-Net-SSLeay-1.94-1.el9.x86_64                                                            13/65
  Installing       : perl-File-Path-2.18-4.el9.noarch                                                             14/65
  Installing       : perl-Mozilla-CA-20200520-6.el9.noarch                                                        15/65
  Installing       : perl-Time-Local-2:1.300-7.el9.noarch                                                         16/65
  Installing       : perl-IO-Socket-SSL-2.073-2.el9.noarch                                                        17/65
  Installing       : perl-IO-Socket-IP-0.41-5.el9.noarch                                                          18/65
  Installing       : perl-subs-1.03-481.1.el9_6.noarch                                                            19/65
  Installing       : perl-Term-Cap-1.17-460.el9.noarch                                                            20/65
  Installing       : perl-Term-ANSIColor-5.01-461.el9.noarch                                                      21/65
  Installing       : perl-POSIX-1.94-481.1.el9_6.x86_64                                                           22/65
  Installing       : perl-Class-Struct-0.66-481.1.el9_6.noarch                                                    23/65
  Installing       : perl-IPC-Open3-1.21-481.1.el9_6.noarch                                                       24/65
  Installing       : perl-Pod-Simple-1:3.42-4.el9.noarch                                                          25/65
  Installing       : perl-File-Temp-1:0.231.100-4.el9.noarch                                                      26/65
  Installing       : perl-HTTP-Tiny-0.076-462.el9.noarch                                                          27/65
  Installing       : perl-Socket-4:2.031-4.el9.x86_64                                                             28/65
  Installing       : perl-Symbol-1.08-481.1.el9_6.noarch                                                          29/65
  Installing       : perl-SelectSaver-1.02-481.1.el9_6.noarch                                                     30/65
  Installing       : perl-File-stat-1.09-481.1.el9_6.noarch                                                       31/65
  Installing       : perl-podlators-1:4.14-460.el9.noarch                                                         32/65
  Installing       : perl-Pod-Perldoc-3.28.01-461.el9.noarch                                                      33/65
  Installing       : perl-Fcntl-1.13-481.1.el9_6.x86_64                                                           34/65
  Installing       : perl-overloading-0.02-481.1.el9_6.noarch                                                     35/65
  Installing       : perl-Text-ParseWords-3.30-460.el9.noarch                                                     36/65
  Installing       : perl-IO-1.43-481.1.el9_6.x86_64                                                              37/65
  Installing       : perl-mro-1.23-481.1.el9_6.x86_64                                                             38/65
  Installing       : perl-Pod-Usage-4:2.01-4.el9.noarch                                                           39/65
  Installing       : perl-parent-1:0.238-460.el9.noarch                                                           40/65
  Installing       : perl-vars-1.05-481.1.el9_6.noarch                                                            41/65
  Installing       : perl-Scalar-List-Utils-4:1.56-462.el9.x86_64                                                 42/65
  Installing       : perl-Getopt-Std-1.12-481.1.el9_6.noarch                                                      43/65
  Installing       : perl-File-Basename-2.85-481.1.el9_6.noarch                                                   44/65
  Installing       : perl-MIME-Base64-3.16-4.el9.x86_64                                                           45/65
  Installing       : perl-Errno-1.30-481.1.el9_6.x86_64                                                           46/65
  Installing       : perl-constant-1.33-461.el9.noarch                                                            47/65
  Installing       : perl-Storable-1:3.21-460.el9.x86_64                                                          48/65
  Installing       : perl-overload-1.31-481.1.el9_6.noarch                                                        49/65
  Installing       : perl-Getopt-Long-1:2.52-4.el9.noarch                                                         50/65
  Installing       : perl-NDBM_File-1.15-481.1.el9_6.x86_64                                                       51/65
  Installing       : perl-Exporter-5.74-461.el9.noarch                                                            52/65
  Installing       : perl-Carp-1.50-460.el9.noarch                                                                53/65
  Installing       : perl-PathTools-3.78-461.el9.x86_64                                                           54/65
  Installing       : perl-Encode-4:3.08-462.el9.x86_64                                                            55/65
  Installing       : perl-libs-4:5.32.1-481.1.el9_6.x86_64                                                        56/65
  Installing       : perl-interpreter-4:5.32.1-481.1.el9_6.x86_64                                                 57/65
  Installing       : mysql-community-common-8.0.43-1.el9.x86_64                                                   58/65
  Installing       : mysql-community-client-plugins-8.0.43-1.el9.x86_64                                           59/65
  Installing       : mysql-community-libs-8.0.43-1.el9.x86_64                                                     60/65
  Running scriptlet: mysql-community-libs-8.0.43-1.el9.x86_64                                                     60/65
  Installing       : mysql-community-client-8.0.43-1.el9.x86_64                                                   61/65
  Installing       : libtirpc-1.3.3-9.el9.x86_64                                                                  62/65
  Installing       : net-tools-2.0-0.64.20160912git.el9.x86_64                                                    63/65
  Running scriptlet: net-tools-2.0-0.64.20160912git.el9.x86_64                                                    63/65
  Installing       : mysql-community-icu-data-files-8.0.43-1.el9.x86_64                                           64/65
  Running scriptlet: mysql-community-server-8.0.43-1.el9.x86_64                                                   65/65
  Installing       : mysql-community-server-8.0.43-1.el9.x86_64                                                   65/65
  Running scriptlet: mysql-community-server-8.0.43-1.el9.x86_64                                                   65/65
  Verifying        : mysql-community-client-8.0.43-1.el9.x86_64                                                    1/65
  Verifying        : mysql-community-client-plugins-8.0.43-1.el9.x86_64                                            2/65
  Verifying        : mysql-community-common-8.0.43-1.el9.x86_64                                                    3/65
  Verifying        : mysql-community-icu-data-files-8.0.43-1.el9.x86_64                                            4/65
  Verifying        : mysql-community-libs-8.0.43-1.el9.x86_64                                                      5/65
  Verifying        : mysql-community-server-8.0.43-1.el9.x86_64                                                    6/65
  Verifying        : net-tools-2.0-0.64.20160912git.el9.x86_64                                                     7/65
  Verifying        : libtirpc-1.3.3-9.el9.x86_64                                                                   8/65
  Verifying        : perl-Getopt-Long-1:2.52-4.el9.noarch                                                          9/65
  Verifying        : perl-Term-Cap-1.17-460.el9.noarch                                                            10/65
  Verifying        : perl-NDBM_File-1.15-481.1.el9_6.x86_64                                                       11/65
  Verifying        : perl-Pod-Escapes-1:1.07-460.el9.noarch                                                       12/65
  Verifying        : perl-vars-1.05-481.1.el9_6.noarch                                                            13/65
  Verifying        : perl-Net-SSLeay-1.94-1.el9.x86_64                                                            14/65
  Verifying        : perl-Socket-4:2.031-4.el9.x86_64                                                             15/65
  Verifying        : perl-parent-1:0.238-460.el9.noarch                                                           16/65
  Verifying        : perl-B-1.80-481.1.el9_6.x86_64                                                               17/65
  Verifying        : perl-URI-5.09-3.el9.noarch                                                                   18/65
  Verifying        : perl-Scalar-List-Utils-4:1.56-462.el9.x86_64                                                 19/65
  Verifying        : perl-base-2.27-481.1.el9_6.noarch                                                            20/65
  Verifying        : perl-Getopt-Std-1.12-481.1.el9_6.noarch                                                      21/65
  Verifying        : perl-PathTools-3.78-461.el9.x86_64                                                           22/65
  Verifying        : perl-Pod-Perldoc-3.28.01-461.el9.noarch                                                      23/65
  Verifying        : perl-HTTP-Tiny-0.076-462.el9.noarch                                                          24/65
  Verifying        : perl-Digest-1.19-4.el9.noarch                                                                25/65
  Verifying        : perl-File-Basename-2.85-481.1.el9_6.noarch                                                   26/65
  Verifying        : perl-Exporter-5.74-461.el9.noarch                                                            27/65
  Verifying        : perl-subs-1.03-481.1.el9_6.noarch                                                            28/65
  Verifying        : perl-MIME-Base64-3.16-4.el9.x86_64                                                           29/65
  Verifying        : perl-AutoLoader-5.74-481.1.el9_6.noarch                                                      30/65
  Verifying        : perl-Fcntl-1.13-481.1.el9_6.x86_64                                                           31/65
  Verifying        : perl-Text-Tabs+Wrap-2013.0523-460.el9.noarch                                                 32/65
  Verifying        : perl-SelectSaver-1.02-481.1.el9_6.noarch                                                     33/65
  Verifying        : perl-IO-1.43-481.1.el9_6.x86_64                                                              34/65
  Verifying        : perl-overload-1.31-481.1.el9_6.noarch                                                        35/65
  Verifying        : perl-if-0.60.800-481.1.el9_6.noarch                                                          36/65
  Verifying        : perl-POSIX-1.94-481.1.el9_6.x86_64                                                           37/65
  Verifying        : perl-FileHandle-2.03-481.1.el9_6.noarch                                                      38/65
  Verifying        : perl-podlators-1:4.14-460.el9.noarch                                                         39/65
  Verifying        : perl-File-Path-2.18-4.el9.noarch                                                             40/65
  Verifying        : perl-File-stat-1.09-481.1.el9_6.noarch                                                       41/65
  Verifying        : perl-Storable-1:3.21-460.el9.x86_64                                                          42/65
  Verifying        : perl-Symbol-1.08-481.1.el9_6.noarch                                                          43/65
  Verifying        : perl-Data-Dumper-2.174-462.el9.x86_64                                                        44/65
  Verifying        : perl-Pod-Simple-1:3.42-4.el9.noarch                                                          45/65
  Verifying        : perl-File-Temp-1:0.231.100-4.el9.noarch                                                      46/65
  Verifying        : perl-Errno-1.30-481.1.el9_6.x86_64                                                           47/65
  Verifying        : perl-Digest-MD5-2.58-4.el9.x86_64                                                            48/65
  Verifying        : perl-Term-ANSIColor-5.01-461.el9.noarch                                                      49/65
  Verifying        : perl-Mozilla-CA-20200520-6.el9.noarch                                                        50/65
  Verifying        : perl-Pod-Usage-4:2.01-4.el9.noarch                                                           51/65
  Verifying        : perl-IO-Socket-SSL-2.073-2.el9.noarch                                                        52/65
  Verifying        : perl-Class-Struct-0.66-481.1.el9_6.noarch                                                    53/65
  Verifying        : perl-Carp-1.50-460.el9.noarch                                                                54/65
  Verifying        : perl-Time-Local-2:1.300-7.el9.noarch                                                         55/65
  Verifying        : perl-IPC-Open3-1.21-481.1.el9_6.noarch                                                       56/65
  Verifying        : perl-libnet-3.13-4.el9.noarch                                                                57/65
  Verifying        : perl-libs-4:5.32.1-481.1.el9_6.x86_64                                                        58/65
  Verifying        : perl-Encode-4:3.08-462.el9.x86_64                                                            59/65
  Verifying        : perl-overloading-0.02-481.1.el9_6.noarch                                                     60/65
  Verifying        : perl-constant-1.33-461.el9.noarch                                                            61/65
  Verifying        : perl-Text-ParseWords-3.30-460.el9.noarch                                                     62/65
  Verifying        : perl-mro-1.23-481.1.el9_6.x86_64                                                             63/65
  Verifying        : perl-interpreter-4:5.32.1-481.1.el9_6.x86_64                                                 64/65
  Verifying        : perl-IO-Socket-IP-0.41-5.el9.noarch                                                          65/65

Installed:
  libtirpc-1.3.3-9.el9.x86_64                                   mysql-community-client-8.0.43-1.el9.x86_64
  mysql-community-client-plugins-8.0.43-1.el9.x86_64            mysql-community-common-8.0.43-1.el9.x86_64
  mysql-community-icu-data-files-8.0.43-1.el9.x86_64            mysql-community-libs-8.0.43-1.el9.x86_64
  mysql-community-server-8.0.43-1.el9.x86_64                    net-tools-2.0-0.64.20160912git.el9.x86_64
  perl-AutoLoader-5.74-481.1.el9_6.noarch                       perl-B-1.80-481.1.el9_6.x86_64
  perl-Carp-1.50-460.el9.noarch                                 perl-Class-Struct-0.66-481.1.el9_6.noarch
  perl-Data-Dumper-2.174-462.el9.x86_64                         perl-Digest-1.19-4.el9.noarch
  perl-Digest-MD5-2.58-4.el9.x86_64                             perl-Encode-4:3.08-462.el9.x86_64
  perl-Errno-1.30-481.1.el9_6.x86_64                            perl-Exporter-5.74-461.el9.noarch
  perl-Fcntl-1.13-481.1.el9_6.x86_64                            perl-File-Basename-2.85-481.1.el9_6.noarch
  perl-File-Path-2.18-4.el9.noarch                              perl-File-Temp-1:0.231.100-4.el9.noarch
  perl-File-stat-1.09-481.1.el9_6.noarch                        perl-FileHandle-2.03-481.1.el9_6.noarch
  perl-Getopt-Long-1:2.52-4.el9.noarch                          perl-Getopt-Std-1.12-481.1.el9_6.noarch
  perl-HTTP-Tiny-0.076-462.el9.noarch                           perl-IO-1.43-481.1.el9_6.x86_64
  perl-IO-Socket-IP-0.41-5.el9.noarch                           perl-IO-Socket-SSL-2.073-2.el9.noarch
  perl-IPC-Open3-1.21-481.1.el9_6.noarch                        perl-MIME-Base64-3.16-4.el9.x86_64
  perl-Mozilla-CA-20200520-6.el9.noarch                         perl-NDBM_File-1.15-481.1.el9_6.x86_64
  perl-Net-SSLeay-1.94-1.el9.x86_64                             perl-POSIX-1.94-481.1.el9_6.x86_64
  perl-PathTools-3.78-461.el9.x86_64                            perl-Pod-Escapes-1:1.07-460.el9.noarch
  perl-Pod-Perldoc-3.28.01-461.el9.noarch                       perl-Pod-Simple-1:3.42-4.el9.noarch
  perl-Pod-Usage-4:2.01-4.el9.noarch                            perl-Scalar-List-Utils-4:1.56-462.el9.x86_64
  perl-SelectSaver-1.02-481.1.el9_6.noarch                      perl-Socket-4:2.031-4.el9.x86_64
  perl-Storable-1:3.21-460.el9.x86_64                           perl-Symbol-1.08-481.1.el9_6.noarch
  perl-Term-ANSIColor-5.01-461.el9.noarch                       perl-Term-Cap-1.17-460.el9.noarch
  perl-Text-ParseWords-3.30-460.el9.noarch                      perl-Text-Tabs+Wrap-2013.0523-460.el9.noarch
  perl-Time-Local-2:1.300-7.el9.noarch                          perl-URI-5.09-3.el9.noarch
  perl-base-2.27-481.1.el9_6.noarch                             perl-constant-1.33-461.el9.noarch
  perl-if-0.60.800-481.1.el9_6.noarch                           perl-interpreter-4:5.32.1-481.1.el9_6.x86_64
  perl-libnet-3.13-4.el9.noarch                                 perl-libs-4:5.32.1-481.1.el9_6.x86_64
  perl-mro-1.23-481.1.el9_6.x86_64                              perl-overload-1.31-481.1.el9_6.noarch
  perl-overloading-0.02-481.1.el9_6.noarch                      perl-parent-1:0.238-460.el9.noarch
  perl-podlators-1:4.14-460.el9.noarch                          perl-subs-1.03-481.1.el9_6.noarch
  perl-vars-1.05-481.1.el9_6.noarch

Complete!
```

## 3) je verifie l'installation

```
[user1@frontend ~]$ sudo dnf list installed | grep mysql
[sudo] password for user1:

mysql-community-client.x86_64         8.0.43-1.el9                  @mysql80-community
mysql-community-client-plugins.x86_64 8.0.43-1.el9                  @mysql80-community
mysql-community-common.x86_64         8.0.43-1.el9                  @mysql80-community
mysql-community-icu-data-files.x86_64 8.0.43-1.el9                  @mysql80-community
mysql-community-libs.x86_64           8.0.43-1.el9                  @mysql80-community
mysql-community-server.x86_64         8.0.43-1.el9                  @mysql80-community
mysql80-community-release.noarch      el9-5                         @System

```
## 6) je Démarre et j'active au demarrage automatique le service MySQL

```
[user1@frontend ~]$ sudo systemctl status mysqld --no-pager
● mysqld.service - MySQL Server
     Loaded: loaded (/usr/lib/systemd/system/mysqld.service; enabled; preset: disabled)
     Active: active (running) since Tue 2025-09-16 19:00:16 CEST; 77ms ago
       Docs: man:mysqld(8)
             http://dev.mysql.com/doc/refman/en/using-systemd.html
    Process: 4008 ExecStartPre=/usr/bin/mysqld_pre_systemd (code=exited, status=0/SUCCESS)
   Main PID: 4074 (mysqld)
     Status: "Server is operational"
      Tasks: 38 (limit: 11067)
     Memory: 452.8M
        CPU: 6.082s
     CGroup: /system.slice/mysqld.service
             └─4074 /usr/sbin/mysqld

Sep 16 19:00:05 frontend systemd[1]: Starting MySQL Server...
Sep 16 19:00:16 frontend systemd[1]: Started MySQL Server.

[user1@frontend ~]$ sudo systemctl enable mysqld
[user1@frontend ~]$ systemctl is-enabled mysqld
enabled
```

## verification du mot de passe temporaire
```
[user1@frontend ~]$ sudo grep 'temporary password' /var/log/mysqld.log
2025-09-16T17:00:07.866607Z 6 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: -p1;je*k*rgT

 mdp mysql temporaire :-p1;je*k*rgT
 ```

## connexion a mysql :

```
 [user1@frontend ~]$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.43

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```



## effectueons les commandes SQL suivantes 
```
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'MonMotdePasseUltraSecur1!';
Query OK, 0 rows affected (0.02 sec)

mysql> CREATE USER 'oneadmin' IDENTIFIED BY 'AnotherPassw0rd!' ;
Query OK, 0 rows affected (0.02 sec)

mysql> CREATE DATABASE opennebula;
Query OK, 1 row affected (0.00 sec)

mysql> GRANT ALL PRIVILEGES ON opennebula.* TO 'oneadmin';
Query OK, 0 rows affected (0.00 sec)

mysql> SET GLOBAL TRANSACTION ISOLATION LEVEL READ COMMITTED;
Query OK, 0 rows affected (0.01 sec)

```

# B. OpenNebula

🌞 Ajouter les dépôts Open Nebula

    ajoutez le dépôt suivant à la liste de dépôts de votre machine

🌞[opennebula]
name=OpenNebula Community Edition
baseurl=https://downloads.opennebula.io/repo/6.10/RedHat/$releasever/$basearch
enabled=1
gpgkey=https://downloads.opennebula.io/repo/repo2.key
gpgcheck=1
repo_gpgcheck=1

```
PS C:\Users\Fadhil> ssh user1@10.3.1.10
user1@10.3.1.10's password:
Last login: Tue Sep 16 19:25:30 2025 from 10.3.1.1
[user1@frontend ~]$ sudo vim /etc/yum.repos.d/opennebula.repo
```
sudo tee /etc/yum.repos.d/opennebula.repo > /dev/null <<EOF
## je Rafraîchir le cache des dépôts

```
[user1@frontend ~]$ sudo dnf makecache -y
[sudo] password for user1:
Extra Packages for Enterprise Linux 9 - x86_64                                           99 kB/s |  33 kB     00:00
Extra Packages for Enterprise Linux 9 openh264 (From Cisco) - x86_64                    4.0 kB/s | 993  B     00:00
MySQL 8.0 Community Server                                                               20 kB/s | 3.0 kB     00:00
MySQL Connectors Community                                                               22 kB/s | 3.0 kB     00:00
MySQL Tools Community                                                                    28 kB/s | 3.0 kB     00:00
OpenNebula Community Edition                                                            1.5 kB/s | 833  B     00:00
OpenNebula Community Edition                                                             15 kB/s | 3.1 kB     00:00
Importing GPG key 0x906DC27C:
 Userid     : "OpenNebula Repository <contact@opennebula.io>"
 Fingerprint: 0B2D 385C 7C93 04B1 1A03 67B9 05A0 5927 906D C27C
 From       : https://downloads.opennebula.io/repo/repo2.key
OpenNebula Community Edition                                                            755 kB/s | 690 kB     00:00
Rocky Linux 9 - BaseOS                                                                  6.5 kB/s | 4.1 kB     00:00
Rocky Linux 9 - AppStream                                                               6.3 kB/s | 4.5 kB     00:00
Rocky Linux 9 - CRB                                                                     8.2 kB/s | 4.5 kB     00:00
Rocky Linux 9 - Extras                                                                  5.8 kB/s | 2.9 kB     00:00
Metadata cache created.
```

## Installation de OpenNebula et ses composants


```
[user1@frontend ~]$ sudo dnf install -y opennebula opennebula-sunstone opennebula-fireedge
Last metadata expiration check: 0:02:35 ago on Tue Sep 16 19:47:40 2025.
Dependencies resolved.
========================================================================================================================
 Package                           Architecture   Version                                      Repository          Size
========================================================================================================================
Installing:
 opennebula                        x86_64         6.10.0.1-1.el9                               opennebula          10 M
 opennebula-fireedge               x86_64         6.10.0.1-1.el9                               opennebula          46 M
 opennebula-sunstone               noarch         6.10.0.1-1.el9                               opennebula          29 M
Installing dependencies:
 alsa-lib                          x86_64         1.2.13-2.el9                                 appstream          506 k
 augeas-libs                       x86_64         1.14.1-2.el9                                 appstream          373 k
 avahi-libs                        x86_64         0.8-22.el9_6.1                               baseos              66 k
 cairo                             x86_64         1.17.4-7.el9                                 appstream          659 k
 cups-libs                         x86_64         1:2.3.3op2-33.el9                            baseos             261 k
 dejavu-sans-fonts                 noarch         2.37-18.el9                                  baseos             1.3 M
 ed                                x86_64         1.14.2-12.el9                                baseos              74 k
 emacs-filesystem                  noarch         1:27.2-14.el9_6.2                            appstream          7.9 k
 flac-libs                         x86_64         1.3.3-10.el9_2.1                             appstream          217 k
 flexiblas                         x86_64         3.0.4-8.el9.0.1                              appstream           30 k
 flexiblas-netlib                  x86_64         3.0.4-8.el9.0.1                              appstream          3.0 M
 flexiblas-openblas-openmp         x86_64         3.0.4-8.el9.0.1                              appstream           15 k
 fontconfig                        x86_64         2.14.0-2.el9_1                               appstream          274 k
 fonts-filesystem                  noarch         1:2.0.5-7.el9.1                              baseos             9.0 k
 freerdp-libs                      x86_64         2:2.11.7-1.el9                               appstream          900 k
 freetype                          x86_64         2.10.4-10.el9_5                              baseos             386 k
 fribidi                           x86_64         1.0.10-6.el9.2                               appstream           84 k
 gd                                x86_64         2.3.2-3.el9                                  appstream          131 k
 genisoimage                       x86_64         1.1.11-48.el9                                epel               324 k
 git                               x86_64         2.47.3-1.el9_6                               appstream           50 k
 git-core                          x86_64         2.47.3-1.el9_6                               appstream          4.6 M
 git-core-doc                      noarch         2.47.3-1.el9_6                               appstream          2.8 M
 glx-utils                         x86_64         8.4.0-12.20210504git0f9e7d9.el9.0.1          appstream           40 k
 gnuplot-common                    x86_64         5.4.3-2.el9                                  epel               776 k
 graphite2                         x86_64         1.3.14-9.el9                                 baseos              94 k
 gsm                               x86_64         1.0.19-6.el9                                 appstream           33 k
 harfbuzz                          x86_64         2.7.4-10.el9                                 baseos             623 k
 info                              x86_64         6.7-15.el9                                   baseos             224 k
 jbigkit-libs                      x86_64         2.1-23.el9                                   appstream           52 k
 keyutils-libs-devel               x86_64         1.6.3-1.el9                                  appstream           54 k
 krb5-devel                        x86_64         1.21.1-8.el9_6                               appstream          132 k
 lame-libs                         x86_64         3.100-12.el9                                 appstream          332 k
 langpacks-core-font-en            noarch         3.0-16.el9                                   appstream          9.5 k
 libICE                            x86_64         1.0.10-8.el9                                 appstream           70 k
 libSM                             x86_64         1.2.3-10.el9                                 appstream           41 k
 libX11                            x86_64         1.7.0-11.el9                                 appstream          645 k
 libX11-common                     noarch         1.7.0-11.el9                                 appstream          151 k
 libX11-xcb                        x86_64         1.7.0-11.el9                                 appstream           10 k
 libXau                            x86_64         1.0.9-8.el9                                  appstream           30 k
 libXext                           x86_64         1.3.4-8.el9                                  appstream           39 k
 libXfixes                         x86_64         5.0.3-16.el9                                 appstream           19 k
 libXft                            x86_64         2.3.3-8.el9                                  appstream           61 k
 libXpm                            x86_64         3.5.13-10.el9                                appstream           58 k
 libXrender                        x86_64         0.9.10-16.el9                                appstream           27 k
 libXxf86vm                        x86_64         1.1.4-18.el9                                 appstream           18 k
 libasyncns                        x86_64         0.8-22.el9                                   appstream           29 k
 libcerf                           x86_64         1.17-2.el9                                   epel                38 k
 libcom_err-devel                  x86_64         1.46.5-7.el9                                 appstream           15 k
 libdatrie                         x86_64         0.2.13-4.el9                                 appstream           32 k
 libdrm                            x86_64         2.4.123-2.el9                                appstream          158 k
 libevdev                          x86_64         1.11.0-3.el9                                 appstream           45 k
 libgfortran                       x86_64         11.5.0-5.el9_5                               baseos             797 k
 libglvnd                          x86_64         1:1.3.4-1.el9                                appstream          133 k
 libglvnd-egl                      x86_64         1:1.3.4-1.el9                                appstream           36 k
 libglvnd-glx                      x86_64         1:1.3.4-1.el9                                appstream          140 k
 libgudev                          x86_64         237-1.el9                                    baseos              35 k
 libicu                            x86_64         67.1-10.el9_6                                baseos             9.6 M
 libinput                          x86_64         1.19.3-5.el9_6                               appstream          193 k
 libjpeg-turbo                     x86_64         2.0.90-7.el9                                 appstream          174 k
 libkadm5                          x86_64         1.21.1-8.el9_6                               baseos              75 k
 libogg                            x86_64         2:1.3.4-6.el9                                appstream           32 k
 libpciaccess                      x86_64         0.16-7.el9                                   baseos              26 k
 libpkgconf                        x86_64         1.7.3-10.el9                                 baseos              35 k
 libpng                            x86_64         2:1.6.37-12.el9                              baseos             116 k
 libproxy                          x86_64         0.4.15-35.el9                                baseos              73 k
 libquadmath                       x86_64         11.5.0-5.el9_5                               baseos             187 k
 libselinux-devel                  x86_64         3.6-3.el9                                    appstream          113 k
 libsepol-devel                    x86_64         3.6-2.el9                                    appstream           39 k
 libsndfile                        x86_64         1.0.31-9.el9                                 appstream          205 k
 libsodium                         x86_64         1.0.18-8.el9                                 epel               161 k
 libsodium-devel                   x86_64         1.0.18-8.el9                                 epel               1.0 M
 libssh2                           x86_64         1.11.0-1.el9                                 epel               132 k
 libthai                           x86_64         0.1.28-8.el9                                 appstream          208 k
 libtiff                           x86_64         4.4.0-13.el9                                 appstream          197 k
 libunwind                         x86_64         1.6.2-1.el9                                  epel                67 k
 libunwind-devel                   x86_64         1.6.2-1.el9                                  epel                80 k
 liburing                          x86_64         2.5-1.el9                                    appstream           38 k
 libusal                           x86_64         1.1.11-48.el9                                epel               137 k
 libusbx                           x86_64         1.0.26-1.el9                                 baseos              75 k
 libverto-devel                    x86_64         0.3.2-3.el9                                  appstream           14 k
 libvncserver                      x86_64         0.9.13-11.el9                                epel               296 k
 libvorbis                         x86_64         1:1.3.7-5.el9                                appstream          192 k
 libwacom                          x86_64         1.12.1-3.el9_4                               appstream           43 k
 libwacom-data                     noarch         1.12.1-3.el9_4                               appstream          105 k
 libwayland-client                 x86_64         1.21.0-1.el9                                 appstream           33 k
 libwayland-cursor                 x86_64         1.21.0-1.el9                                 appstream           18 k
 libwayland-server                 x86_64         1.21.0-1.el9                                 appstream           41 k
 libwebp                           x86_64         1.2.0-8.el9                                  appstream          276 k
 libwinpr                          x86_64         2:2.11.7-1.el9                               appstream          356 k
 libxcb                            x86_64         1.13.1-9.el9                                 appstream          224 k
 libxkbcommon                      x86_64         1.0.3-4.el9                                  appstream          132 k
 libxkbcommon-x11                  x86_64         1.0.3-4.el9                                  appstream           21 k
 libxkbfile                        x86_64         1.1.0-8.el9                                  appstream           88 k
 libxshmfence                      x86_64         1.3-10.el9                                   appstream           12 k
 libxslt                           x86_64         1.1.34-13.el9_6                              appstream          239 k
 llvm-libs                         x86_64         19.1.7-1.el9                                 appstream           57 M
 mesa-dri-drivers                  x86_64         24.2.8-2.el9_6                               appstream          9.4 M
 mesa-filesystem                   x86_64         24.2.8-2.el9_6                               appstream           11 k
 mesa-libEGL                       x86_64         24.2.8-2.el9_6                               appstream          141 k
 mesa-libGL                        x86_64         24.2.8-2.el9_6                               appstream          169 k
 mesa-libgbm                       x86_64         24.2.8-2.el9_6                               appstream           36 k
 mesa-libglapi                     x86_64         24.2.8-2.el9_6                               appstream           44 k
 mtdev                             x86_64         1.1.5-22.el9                                 appstream           21 k
 nodejs                            x86_64         1:16.20.2-8.el9_4                            appstream          111 k
 nodejs-libs                       x86_64         1:16.20.2-8.el9_4                            appstream           15 M
 openblas                          x86_64         0.3.26-2.el9                                 appstream           37 k
 openblas-openmp                   x86_64         0.3.26-2.el9                                 appstream          4.9 M
 opennebula-common                 noarch         6.10.0.1-1.el9                               opennebula          23 k
 opennebula-common-onecfg          noarch         6.10.0.1-1.el9                               opennebula         9.1 k
 opennebula-libs                   noarch         6.10.0.1-1.el9                               opennebula         202 k
 opennebula-provision-data         noarch         6.10.0.1-1.el9                               opennebula          52 k
 opennebula-rubygems               x86_64         6.10.0.1-1.el9                               opennebula          16 M
 opennebula-tools                  noarch         6.10.0.1-1.el9                               opennebula         191 k
 openpgm                           x86_64         5.2.122-28.el9                               epel               176 k
 openpgm-devel                     x86_64         5.2.122-28.el9                               epel                58 k
 opus                              x86_64         1.3.1-10.el9                                 appstream          199 k
 pango                             x86_64         1.48.7-3.el9                                 appstream          297 k
 patch                             x86_64         2.7.6-16.el9                                 appstream          127 k
 pcre2-devel                       x86_64         10.40-6.el9                                  appstream          471 k
 pcre2-utf16                       x86_64         10.40-6.el9                                  appstream          213 k
 pcre2-utf32                       x86_64         10.40-6.el9                                  appstream          202 k
 perl-DynaLoader                   x86_64         1.47-481.1.el9_6                             appstream           24 k
 perl-Error                        noarch         1:0.17029-7.el9                              appstream           41 k
 perl-File-Find                    noarch         1.37-481.1.el9_6                             appstream           24 k
 perl-Git                          noarch         2.47.3-1.el9_6                               appstream           37 k
 perl-TermReadKey                  x86_64         2.38-11.el9                                  appstream           36 k
 perl-lib                          x86_64         0.65-481.1.el9_6                             appstream           13 k
 pixman                            x86_64         0.40.0-6.el9_3                               appstream          269 k
 pkgconf                           x86_64         1.7.3-10.el9                                 baseos              40 k
 pkgconf-m4                        noarch         1.7.3-10.el9                                 baseos              14 k
 pkgconf-pkg-config                x86_64         1.7.3-10.el9                                 baseos              10 k
 pulseaudio-libs                   x86_64         15.0-3.el9                                   appstream          663 k
 python3-numpy                     x86_64         1:1.23.5-1.el9                               appstream          5.8 M
 python3-setuptools                noarch         53.0.0-13.el9_6.1                            baseos             837 k
 qemu-img                          x86_64         17:9.1.0-15.el9_6.7                          appstream          2.5 M
 qt5-qtbase                        x86_64         5.15.9-11.el9_6                              appstream          3.5 M
 qt5-qtbase-common                 noarch         5.15.9-11.el9_6                              appstream          7.6 k
 qt5-qtbase-gui                    x86_64         5.15.9-11.el9_6                              appstream          6.3 M
 qt5-qtsvg                         x86_64         5.15.9-2.el9                                 appstream          184 k
 rsync                             x86_64         3.2.5-3.el9                                  baseos             403 k
 ruby                              x86_64         3.0.7-165.el9_5                              appstream           38 k
 ruby-libs                         x86_64         3.0.7-165.el9_5                              appstream          3.2 M
 rubygem-bigdecimal                x86_64         3.0.0-165.el9_5                              appstream           52 k
 rubygem-io-console                x86_64         0.5.7-165.el9_5                              appstream           23 k
 rubygem-json                      x86_64         2.5.1-165.el9_5                              appstream           51 k
 rubygem-psych                     x86_64         3.3.2-165.el9_5                              appstream           48 k
 rubygem-rexml                     noarch         3.2.5-165.el9_5                              appstream           92 k
 rubygems                          noarch         3.2.33-165.el9_5                             appstream          253 k
 sqlite                            x86_64         3.34.1-8.el9_6                               appstream          746 k
 tar                               x86_64         2:1.34-7.el9                                 baseos             875 k
 uuid                              x86_64         1.6.2-55.el9                                 appstream           56 k
 xcb-util                          x86_64         0.4.0-19.el9                                 appstream           18 k
 xcb-util-image                    x86_64         0.4.0-19.el9.0.1                             appstream           18 k
 xcb-util-keysyms                  x86_64         0.4.0-17.el9                                 appstream           14 k
 xcb-util-renderutil               x86_64         0.3.9-20.el9.0.1                             appstream           16 k
 xcb-util-wm                       x86_64         0.4.1-22.el9                                 appstream           31 k
 xkeyboard-config                  noarch         2.33-2.el9                                   appstream          779 k
 xml-common                        noarch         0.6.3-58.el9                                 appstream           31 k
 xmlrpc-c                          x86_64         1.51.0-16.el9                                appstream          140 k
 zeromq                            x86_64         4.3.4-2.el9                                  epel               431 k
 zeromq-devel                      x86_64         4.3.4-2.el9                                  epel                16 k
Installing weak dependencies:
 bash-completion                   noarch         1:2.11-5.el9                                 baseos             291 k
 gnuplot                           x86_64         5.4.3-2.el9                                  epel               820 k
 nodejs-docs                       noarch         1:16.20.2-8.el9_4                            appstream          7.1 M
 nodejs-full-i18n                  x86_64         1:16.20.2-8.el9_4                            appstream          8.2 M
 npm                               x86_64         1:8.19.4-1.16.20.2.8.el9_4                   appstream          1.7 M
 opennebula-guacd                  x86_64         6.10.0.1-1.2.0+1.el9                         opennebula         220 k
 ruby-default-gems                 noarch         3.0.7-165.el9_5                              appstream           30 k
 rubygem-bundler                   noarch         2.2.33-165.el9_5                             appstream          370 k
 rubygem-rdoc                      noarch         6.3.4.1-165.el9_5                            appstream          398 k

Transaction Summary
========================================================================================================================
Install  173 Packages

Total download size: 271 M
Installed size: 1.4 G
Downloading Packages:
(1/173): genisoimage-1.1.11-48.el9.x86_64.rpm                                           816 kB/s | 324 kB     00:00
(2/173): libcerf-1.17-2.el9.x86_64.rpm                                                  423 kB/s |  38 kB     00:00
(3/173): gnuplot-5.4.3-2.el9.x86_64.rpm                                                 1.5 MB/s | 820 kB     00:00
(4/173): gnuplot-common-5.4.3-2.el9.x86_64.rpm                                          1.3 MB/s | 776 kB     00:00
(5/173): libsodium-1.0.18-8.el9.x86_64.rpm                                              968 kB/s | 161 kB     00:00
(6/173): libssh2-1.11.0-1.el9.x86_64.rpm                                                982 kB/s | 132 kB     00:00
(7/173): libsodium-devel-1.0.18-8.el9.x86_64.rpm                                        5.1 MB/s | 1.0 MB     00:00
(8/173): libunwind-1.6.2-1.el9.x86_64.rpm                                               509 kB/s |  67 kB     00:00
(9/173): libunwind-devel-1.6.2-1.el9.x86_64.rpm                                         814 kB/s |  80 kB     00:00
(10/173): libusal-1.1.11-48.el9.x86_64.rpm                                              1.3 MB/s | 137 kB     00:00
(11/173): openpgm-5.2.122-28.el9.x86_64.rpm                                             1.8 MB/s | 176 kB     00:00
(12/173): libvncserver-0.9.13-11.el9.x86_64.rpm                                         2.1 MB/s | 296 kB     00:00
(13/173): openpgm-devel-5.2.122-28.el9.x86_64.rpm                                       556 kB/s |  58 kB     00:00
(14/173): zeromq-devel-4.3.4-2.el9.x86_64.rpm                                           170 kB/s |  16 kB     00:00
(15/173): zeromq-4.3.4-2.el9.x86_64.rpm                                                 2.3 MB/s | 431 kB     00:00
(16/173): opennebula-common-6.10.0.1-1.el9.noarch.rpm                                    92 kB/s |  23 kB     00:00
(17/173): opennebula-common-onecfg-6.10.0.1-1.el9.noarch.rpm                             36 kB/s | 9.1 kB     00:00
(18/173): opennebula-guacd-6.10.0.1-1.2.0+1.el9.x86_64.rpm                              369 kB/s | 220 kB     00:00
(19/173): opennebula-libs-6.10.0.1-1.el9.noarch.rpm                                     207 kB/s | 202 kB     00:00
(20/173): opennebula-provision-data-6.10.0.1-1.el9.noarch.rpm                           111 kB/s |  52 kB     00:00
(21/173): opennebula-6.10.0.1-1.el9.x86_64.rpm                                          3.8 MB/s |  10 MB     00:02
(22/173): opennebula-fireedge-6.10.0.1-1.el9.x86_64.rpm                                 4.1 MB/s |  46 MB     00:11
(23/173): opennebula-rubygems-6.10.0.1-1.el9.x86_64.rpm                                 1.7 MB/s |  16 MB     00:09
(24/173): opennebula-tools-6.10.0.1-1.el9.noarch.rpm                                    472 kB/s | 191 kB     00:00
(25/173): info-6.7-15.el9.x86_64.rpm                                                    502 kB/s | 224 kB     00:00
(26/173): cups-libs-2.3.3op2-33.el9.x86_64.rpm                                          261 kB/s | 261 kB     00:01
(27/173): harfbuzz-2.7.4-10.el9.x86_64.rpm                                              640 kB/s | 623 kB     00:00
(28/173): libicu-67.1-10.el9_6.x86_64.rpm                                               3.4 MB/s | 9.6 MB     00:02
(29/173): dejavu-sans-fonts-2.37-18.el9.noarch.rpm                                      4.1 MB/s | 1.3 MB     00:00
(30/173): bash-completion-2.11-5.el9.noarch.rpm                                         2.3 MB/s | 291 kB     00:00
(31/173): libpng-1.6.37-12.el9.x86_64.rpm                                               289 kB/s | 116 kB     00:00
(32/173): ed-1.14.2-12.el9.x86_64.rpm                                                   488 kB/s |  74 kB     00:00
(33/173): pkgconf-1.7.3-10.el9.x86_64.rpm                                               266 kB/s |  40 kB     00:00
(34/173): avahi-libs-0.8-22.el9_6.1.x86_64.rpm                                          494 kB/s |  66 kB     00:00
(35/173): libpciaccess-0.16-7.el9.x86_64.rpm                                            150 kB/s |  26 kB     00:00
(36/173): libpkgconf-1.7.3-10.el9.x86_64.rpm                                            199 kB/s |  35 kB     00:00
(37/173): fonts-filesystem-2.0.5-7.el9.1.noarch.rpm                                     100 kB/s | 9.0 kB     00:00
(38/173): libquadmath-11.5.0-5.el9_5.x86_64.rpm                                         1.7 MB/s | 187 kB     00:00
(39/173): pkgconf-m4-1.7.3-10.el9.noarch.rpm                                             53 kB/s |  14 kB     00:00
(40/173): tar-1.34-7.el9.x86_64.rpm                                                     2.9 MB/s | 875 kB     00:00
(41/173): libproxy-0.4.15-35.el9.x86_64.rpm                                             720 kB/s |  73 kB     00:00
(42/173): pkgconf-pkg-config-1.7.3-10.el9.x86_64.rpm                                     73 kB/s |  10 kB     00:00
(43/173): libgudev-237-1.el9.x86_64.rpm                                                 400 kB/s |  35 kB     00:00
(44/173): freetype-2.10.4-10.el9_5.x86_64.rpm                                           1.1 MB/s | 386 kB     00:00
(45/173): graphite2-1.3.14-9.el9.x86_64.rpm                                             378 kB/s |  94 kB     00:00
(46/173): python3-setuptools-53.0.0-13.el9_6.1.noarch.rpm                               1.8 MB/s | 837 kB     00:00
(47/173): rsync-3.2.5-3.el9.x86_64.rpm                                                  2.0 MB/s | 403 kB     00:00
(48/173): libgfortran-11.5.0-5.el9_5.x86_64.rpm                                         3.8 MB/s | 797 kB     00:00
(49/173): libkadm5-1.21.1-8.el9_6.x86_64.rpm                                            648 kB/s |  75 kB     00:00
(50/173): libusbx-1.0.26-1.el9.x86_64.rpm                                               836 kB/s |  75 kB     00:00
(51/173): rubygem-json-2.5.1-165.el9_5.x86_64.rpm                                        78 kB/s |  51 kB     00:00
(52/173): flac-libs-1.3.3-10.el9_2.1.x86_64.rpm                                         287 kB/s | 217 kB     00:00
(53/173): flexiblas-openblas-openmp-3.0.4-8.el9.0.1.x86_64.rpm                           95 kB/s |  15 kB     00:00
(54/173): libwinpr-2.11.7-1.el9.x86_64.rpm                                              1.1 MB/s | 356 kB     00:00
(55/173): libXxf86vm-1.1.4-18.el9.x86_64.rpm                                             79 kB/s |  18 kB     00:00
(56/173): libXpm-3.5.13-10.el9.x86_64.rpm                                               375 kB/s |  58 kB     00:00
(57/173): libthai-0.1.28-8.el9.x86_64.rpm                                               1.1 MB/s | 208 kB     00:00
(58/173): libglvnd-1.3.4-1.el9.x86_64.rpm                                               444 kB/s | 133 kB     00:00
(59/173): libtiff-4.4.0-13.el9.x86_64.rpm                                               159 kB/s | 197 kB     00:01
(60/173): nodejs-docs-16.20.2-8.el9_4.noarch.rpm                                        3.7 MB/s | 7.1 MB     00:01
(61/173): perl-DynaLoader-1.47-481.1.el9_6.x86_64.rpm                                    87 kB/s |  24 kB     00:00
(62/173): libwayland-client-1.21.0-1.el9.x86_64.rpm                                     287 kB/s |  33 kB     00:00
(63/173): libselinux-devel-3.6-3.el9.x86_64.rpm                                         888 kB/s | 113 kB     00:00
(64/173): keyutils-libs-devel-1.6.3-1.el9.x86_64.rpm                                    381 kB/s |  54 kB     00:00
(65/173): rubygem-bundler-2.2.33-165.el9_5.noarch.rpm                                   1.8 MB/s | 370 kB     00:00
(66/173): libXrender-0.9.10-16.el9.x86_64.rpm                                           200 kB/s |  27 kB     00:00
(67/173): qt5-qtbase-common-5.15.9-11.el9_6.noarch.rpm                                   76 kB/s | 7.6 kB     00:00
(68/173): libwebp-1.2.0-8.el9.x86_64.rpm                                                883 kB/s | 276 kB     00:00
(69/173): xcb-util-wm-0.4.1-22.el9.x86_64.rpm                                            74 kB/s |  31 kB     00:00
(70/173): nodejs-libs-16.20.2-8.el9_4.x86_64.rpm                                        4.1 MB/s |  15 MB     00:03
(71/173): python3-numpy-1.23.5-1.el9.x86_64.rpm                                         2.0 MB/s | 5.8 MB     00:02
(72/173): libX11-common-1.7.0-11.el9.noarch.rpm                                         1.2 MB/s | 151 kB     00:00
(73/173): jbigkit-libs-2.1-23.el9.x86_64.rpm                                            229 kB/s |  52 kB     00:00
(74/173): pcre2-utf16-10.40-6.el9.x86_64.rpm                                            1.1 MB/s | 213 kB     00:00
(75/173): libXau-1.0.9-8.el9.x86_64.rpm                                                 332 kB/s |  30 kB     00:00
(76/173): libverto-devel-0.3.2-3.el9.x86_64.rpm                                         130 kB/s |  14 kB     00:00
(77/173): mesa-libGL-24.2.8-2.el9_6.x86_64.rpm                                          993 kB/s | 169 kB     00:00
(78/173): augeas-libs-1.14.1-2.el9.x86_64.rpm                                           1.9 MB/s | 373 kB     00:00
(79/173): xcb-util-renderutil-0.3.9-20.el9.0.1.x86_64.rpm                               130 kB/s |  16 kB     00:00
(80/173): mesa-libglapi-24.2.8-2.el9_6.x86_64.rpm                                       319 kB/s |  44 kB     00:00
(81/173): ruby-3.0.7-165.el9_5.x86_64.rpm                                               274 kB/s |  38 kB     00:00
(82/173): liburing-2.5-1.el9.x86_64.rpm                                                 342 kB/s |  38 kB     00:00
(83/173): libinput-1.19.3-5.el9_6.x86_64.rpm                                            1.1 MB/s | 193 kB     00:00
(84/173): libXext-1.3.4-8.el9.x86_64.rpm                                                189 kB/s |  39 kB     00:00
(85/173): xml-common-0.6.3-58.el9.noarch.rpm                                            261 kB/s |  31 kB     00:00
(86/173): perl-lib-0.65-481.1.el9_6.x86_64.rpm                                          108 kB/s |  13 kB     00:00
(87/173): glx-utils-8.4.0-12.20210504git0f9e7d9.el9.0.1.x86_64.rpm                      250 kB/s |  40 kB     00:00
(88/173): libxshmfence-1.3-10.el9.x86_64.rpm                                             72 kB/s |  12 kB     00:00
(89/173): rubygem-rdoc-6.3.4.1-165.el9_5.noarch.rpm                                     2.4 MB/s | 398 kB     00:00
(90/173): langpacks-core-font-en-3.0-16.el9.noarch.rpm                                   53 kB/s | 9.5 kB     00:00
(91/173): flexiblas-3.0.4-8.el9.0.1.x86_64.rpm                                           48 kB/s |  30 kB     00:00
(92/173): openblas-openmp-0.3.26-2.el9.x86_64.rpm                                       2.9 MB/s | 4.9 MB     00:01
(93/173): flexiblas-netlib-3.0.4-8.el9.0.1.x86_64.rpm                                   2.1 MB/s | 3.0 MB     00:01
(94/173): libX11-xcb-1.7.0-11.el9.x86_64.rpm                                             20 kB/s |  10 kB     00:00
(95/173): opennebula-sunstone-6.10.0.1-1.el9.noarch.rpm                                 1.1 MB/s |  29 MB     00:25
(96/173): mesa-libgbm-24.2.8-2.el9_6.x86_64.rpm                                         126 kB/s |  36 kB     00:00
(97/173): libglvnd-glx-1.3.4-1.el9.x86_64.rpm                                           499 kB/s | 140 kB     00:00
(98/173): libwayland-cursor-1.21.0-1.el9.x86_64.rpm                                     201 kB/s |  18 kB     00:00
(99/173): openblas-0.3.26-2.el9.x86_64.rpm                                              342 kB/s |  37 kB     00:00
(100/173): npm-8.19.4-1.16.20.2.8.el9_4.x86_64.rpm                                      4.6 MB/s | 1.7 MB     00:00
(101/173): xkeyboard-config-2.33-2.el9.noarch.rpm                                       1.4 MB/s | 779 kB     00:00
(102/173): krb5-devel-1.21.1-8.el9_6.x86_64.rpm                                         162 kB/s | 132 kB     00:00
(103/173): nodejs-full-i18n-16.20.2-8.el9_4.x86_64.rpm                                  4.4 MB/s | 8.2 MB     00:01
(104/173): pcre2-devel-10.40-6.el9.x86_64.rpm                                           381 kB/s | 471 kB     00:01
(105/173): libglvnd-egl-1.3.4-1.el9.x86_64.rpm                                           61 kB/s |  36 kB     00:00
(106/173): git-core-doc-2.47.3-1.el9_6.noarch.rpm                                       4.4 MB/s | 2.8 MB     00:00
(107/173): libevdev-1.11.0-3.el9.x86_64.rpm                                              73 kB/s |  45 kB     00:00
(108/173): freerdp-libs-2.11.7-1.el9.x86_64.rpm                                         1.3 MB/s | 900 kB     00:00
(109/173): emacs-filesystem-27.2-14.el9_6.2.noarch.rpm                                   87 kB/s | 7.9 kB     00:00
(110/173): libcom_err-devel-1.46.5-7.el9.x86_64.rpm                                      28 kB/s |  15 kB     00:00
(111/173): libxcb-1.13.1-9.el9.x86_64.rpm                                               153 kB/s | 224 kB     00:01
(112/173): patch-2.7.6-16.el9.x86_64.rpm                                                 37 kB/s | 127 kB     00:03
(113/173): rubygems-3.2.33-165.el9_5.noarch.rpm                                         104 kB/s | 253 kB     00:02
(114/173): git-2.47.3-1.el9_6.x86_64.rpm                                                 25 kB/s |  50 kB     00:01
(115/173): xcb-util-0.4.0-19.el9.x86_64.rpm                                             9.5 kB/s |  18 kB     00:01
(116/173): llvm-libs-19.1.7-1.el9.x86_64.rpm                                            8.1 MB/s |  57 MB     00:07
(117/173): libsepol-devel-3.6-2.el9.x86_64.rpm                                           37 kB/s |  39 kB     00:01
(118/173): pulseaudio-libs-15.0-3.el9.x86_64.rpm                                        613 kB/s | 663 kB     00:01
(119/173): uuid-1.6.2-55.el9.x86_64.rpm                                                 322 kB/s |  56 kB     00:00
(120/173): libXft-2.3.3-8.el9.x86_64.rpm                                                363 kB/s |  61 kB     00:00
(121/173): libxkbcommon-x11-1.0.3-4.el9.x86_64.rpm                                      134 kB/s |  21 kB     00:00
(122/173): libdatrie-0.2.13-4.el9.x86_64.rpm                                            261 kB/s |  32 kB     00:00
(123/173): xmlrpc-c-1.51.0-16.el9.x86_64.rpm                                            952 kB/s | 140 kB     00:00
(124/173): pcre2-utf32-10.40-6.el9.x86_64.rpm                                           1.3 MB/s | 202 kB     00:00
(125/173): libSM-1.2.3-10.el9.x86_64.rpm                                                340 kB/s |  41 kB     00:00
(126/173): libwacom-data-1.12.1-3.el9_4.noarch.rpm                                      493 kB/s | 105 kB     00:00
(127/173): qt5-qtbase-gui-5.15.9-11.el9_6.x86_64.rpm                                    8.9 MB/s | 6.3 MB     00:00
(128/173): alsa-lib-1.2.13-2.el9.x86_64.rpm                                             749 kB/s | 506 kB     00:00
(129/173): qemu-img-9.1.0-15.el9_6.7.x86_64.rpm                                         3.3 MB/s | 2.5 MB     00:00
(130/173): rubygem-bigdecimal-3.0.0-165.el9_5.x86_64.rpm                                226 kB/s |  52 kB     00:00
(131/173): perl-File-Find-1.37-481.1.el9_6.noarch.rpm                                   109 kB/s |  24 kB     00:00
(132/173): libwacom-1.12.1-3.el9_4.x86_64.rpm                                           428 kB/s |  43 kB     00:00
(133/173): pango-1.48.7-3.el9.x86_64.rpm                                                1.6 MB/s | 297 kB     00:00
(134/173): gd-2.3.2-3.el9.x86_64.rpm                                                    684 kB/s | 131 kB     00:00
(135/173): xcb-util-keysyms-0.4.0-17.el9.x86_64.rpm                                     122 kB/s |  14 kB     00:00
(136/173): libdrm-2.4.123-2.el9.x86_64.rpm                                              1.0 MB/s | 158 kB     00:00
(137/173): cairo-1.17.4-7.el9.x86_64.rpm                                                3.4 MB/s | 659 kB     00:00
(138/173): gsm-1.0.19-6.el9.x86_64.rpm                                                  198 kB/s |  33 kB     00:00
(139/173): ruby-default-gems-3.0.7-165.el9_5.noarch.rpm                                 308 kB/s |  30 kB     00:00
(140/173): opus-1.3.1-10.el9.x86_64.rpm                                                 1.5 MB/s | 199 kB     00:00
(141/173): rubygem-io-console-0.5.7-165.el9_5.x86_64.rpm                                170 kB/s |  23 kB     00:00
(142/173): rubygem-rexml-3.2.5-165.el9_5.noarch.rpm                                     522 kB/s |  92 kB     00:00
(143/173): libogg-1.3.4-6.el9.x86_64.rpm                                                112 kB/s |  32 kB     00:00
(144/173): qt5-qtbase-5.15.9-11.el9_6.x86_64.rpm                                        7.4 MB/s | 3.5 MB     00:00
(145/173): nodejs-16.20.2-8.el9_4.x86_64.rpm                                            295 kB/s | 111 kB     00:00
(146/173): rubygem-psych-3.3.2-165.el9_5.x86_64.rpm                                     249 kB/s |  48 kB     00:00
(147/173): libasyncns-0.8-22.el9.x86_64.rpm                                             205 kB/s |  29 kB     00:00
(148/173): libXfixes-5.0.3-16.el9.x86_64.rpm                                            122 kB/s |  19 kB     00:00
(149/173): mtdev-1.1.5-22.el9.x86_64.rpm                                                132 kB/s |  21 kB     00:00
(150/173): libvorbis-1.3.7-5.el9.x86_64.rpm                                             644 kB/s | 192 kB     00:00
(151/173): fontconfig-2.14.0-2.el9_1.x86_64.rpm                                         924 kB/s | 274 kB     00:00
(152/173): git-core-2.47.3-1.el9_6.x86_64.rpm                                           4.7 MB/s | 4.6 MB     00:00
(153/173): perl-Error-0.17029-7.el9.noarch.rpm                                           71 kB/s |  41 kB     00:00
(154/173): ruby-libs-3.0.7-165.el9_5.x86_64.rpm                                         5.0 MB/s | 3.2 MB     00:00
(155/173): libsndfile-1.0.31-9.el9.x86_64.rpm                                           1.4 MB/s | 205 kB     00:00
(156/173): libICE-1.0.10-8.el9.x86_64.rpm                                               451 kB/s |  70 kB     00:00
(157/173): mesa-libEGL-24.2.8-2.el9_6.x86_64.rpm                                        1.1 MB/s | 141 kB     00:00
(158/173): sqlite-3.34.1-8.el9_6.x86_64.rpm                                             3.7 MB/s | 746 kB     00:00
(159/173): mesa-filesystem-24.2.8-2.el9_6.x86_64.rpm                                     57 kB/s |  11 kB     00:00
(160/173): fribidi-1.0.10-6.el9.2.x86_64.rpm                                            499 kB/s |  84 kB     00:00
(161/173): xcb-util-image-0.4.0-19.el9.0.1.x86_64.rpm                                   132 kB/s |  18 kB     00:00
(162/173): qt5-qtsvg-5.15.9-2.el9.x86_64.rpm                                            1.3 MB/s | 184 kB     00:00
(163/173): libxkbfile-1.1.0-8.el9.x86_64.rpm                                            610 kB/s |  88 kB     00:00
(164/173): libwayland-server-1.21.0-1.el9.x86_64.rpm                                    271 kB/s |  41 kB     00:00
(165/173): libxkbcommon-1.0.3-4.el9.x86_64.rpm                                          861 kB/s | 132 kB     00:00
(166/173): perl-TermReadKey-2.38-11.el9.x86_64.rpm                                      235 kB/s |  36 kB     00:00
(167/173): perl-Git-2.47.3-1.el9_6.noarch.rpm                                           299 kB/s |  37 kB     00:00
(168/173): lame-libs-3.100-12.el9.x86_64.rpm                                            558 kB/s | 332 kB     00:00
(169/173): mesa-dri-drivers-24.2.8-2.el9_6.x86_64.rpm                                   7.6 MB/s | 9.4 MB     00:01
(170/173): pixman-0.40.0-6.el9_3.x86_64.rpm                                             242 kB/s | 269 kB     00:01
(171/173): libjpeg-turbo-2.0.90-7.el9.x86_64.rpm                                        270 kB/s | 174 kB     00:00
(172/173): libxslt-1.1.34-13.el9_6.x86_64.rpm                                           1.1 MB/s | 239 kB     00:00
(173/173): libX11-1.7.0-11.el9.x86_64.rpm                                               3.0 MB/s | 645 kB     00:00
------------------------------------------------------------------------------------------------------------------------
Total                                                                                   6.0 MB/s | 271 MB     00:45
OpenNebula Community Edition                                                             14 kB/s | 3.1 kB     00:00
Importing GPG key 0x906DC27C:
 Userid     : "OpenNebula Repository <contact@opennebula.io>"
 Fingerprint: 0B2D 385C 7C93 04B1 1A03 67B9 05A0 5927 906D C27C
 From       : https://downloads.opennebula.io/repo/repo2.key
Key imported successfully
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Running scriptlet: npm-1:8.19.4-1.16.20.2.8.el9_4.x86_64                                                          1/1
  Preparing        :                                                                                                1/1
  Installing       : ruby-libs-3.0.7-165.el9_5.x86_64                                                             1/173
  Installing       : libjpeg-turbo-2.0.90-7.el9.x86_64                                                            2/173
  Installing       : libpng-2:1.6.37-12.el9.x86_64                                                                3/173
  Running scriptlet: opennebula-common-onecfg-6.10.0.1-1.el9.noarch                                               4/173
  Installing       : opennebula-common-onecfg-6.10.0.1-1.el9.noarch                                               4/173
  Installing       : libogg-2:1.3.4-6.el9.x86_64                                                                  5/173
  Installing       : libX11-xcb-1.7.0-11.el9.x86_64                                                               6/173
  Running scriptlet: opennebula-common-6.10.0.1-1.el9.noarch                                                      7/173
  Installing       : opennebula-common-6.10.0.1-1.el9.noarch                                                      7/173
  Running scriptlet: opennebula-common-6.10.0.1-1.el9.noarch                                                      7/173
  Installing       : libxshmfence-1.3-10.el9.x86_64                                                               8/173
  Installing       : libwebp-1.2.0-8.el9.x86_64                                                                   9/173
  Installing       : libwayland-client-1.21.0-1.el9.x86_64                                                       10/173
  Installing       : libvorbis-1:1.3.7-5.el9.x86_64                                                              11/173
  Installing       : ruby-3.0.7-165.el9_5.x86_64                                                                 12/173
  Installing       : rubygem-bigdecimal-3.0.0-165.el9_5.x86_64                                                   13/173
  Installing       : rubygem-bundler-2.2.33-165.el9_5.noarch                                                     14/173
  Installing       : ruby-default-gems-3.0.7-165.el9_5.noarch                                                    15/173
  Installing       : rubygem-io-console-0.5.7-165.el9_5.x86_64                                                   16/173
  Installing       : rubygem-psych-3.3.2-165.el9_5.x86_64                                                        17/173
  Installing       : rubygems-3.2.33-165.el9_5.noarch                                                            18/173
  Installing       : rubygem-json-2.5.1-165.el9_5.x86_64                                                         19/173
  Installing       : rubygem-rdoc-6.3.4.1-165.el9_5.noarch                                                       20/173
  Installing       : libwayland-server-1.21.0-1.el9.x86_64                                                       21/173
  Installing       : libICE-1.0.10-8.el9.x86_64                                                                  22/173
  Installing       : git-core-2.47.3-1.el9_6.x86_64                                                              23/173
  Installing       : gsm-1.0.19-6.el9.x86_64                                                                     24/173
  Installing       : flexiblas-3.0.4-8.el9.0.1.x86_64                                                            25/173
  Installing       : augeas-libs-1.14.1-2.el9.x86_64                                                             26/173
  Installing       : pcre2-utf16-10.40-6.el9.x86_64                                                              27/173
  Installing       : libglvnd-1:1.3.4-1.el9.x86_64                                                               28/173
  Installing       : libquadmath-11.5.0-5.el9_5.x86_64                                                           29/173
  Installing       : libgfortran-11.5.0-5.el9_5.x86_64                                                           30/173
  Installing       : fonts-filesystem-1:2.0.5-7.el9.1.noarch                                                     31/173
  Installing       : dejavu-sans-fonts-2.37-18.el9.noarch                                                        32/173
  Installing       : libicu-67.1-10.el9_6.x86_64                                                                 33/173
  Installing       : libwinpr-2:2.11.7-1.el9.x86_64                                                              34/173
  Installing       : openpgm-5.2.122-28.el9.x86_64                                                               35/173
  Installing       : libunwind-1.6.2-1.el9.x86_64                                                                36/173
  Installing       : libsodium-1.0.18-8.el9.x86_64                                                               37/173
  Installing       : zeromq-4.3.4-2.el9.x86_64                                                                   38/173
  Installing       : langpacks-core-font-en-3.0-16.el9.noarch                                                    39/173
  Installing       : git-core-doc-2.47.3-1.el9_6.noarch                                                          40/173
  Installing       : libSM-1.2.3-10.el9.x86_64                                                                   41/173
  Installing       : rubygem-rexml-3.2.5-165.el9_5.noarch                                                        42/173
  Installing       : libwayland-cursor-1.21.0-1.el9.x86_64                                                       43/173
  Installing       : flac-libs-1.3.3-10.el9_2.1.x86_64                                                           44/173
  Installing       : libvncserver-0.9.13-11.el9.x86_64                                                           45/173
  Installing       : libxslt-1.1.34-13.el9_6.x86_64                                                              46/173
  Installing       : opennebula-rubygems-6.10.0.1-1.el9.x86_64                                                   47/173
  Running scriptlet: opennebula-rubygems-6.10.0.1-1.el9.x86_64                                                   47/173
  Installing       : pixman-0.40.0-6.el9_3.x86_64                                                                48/173
  Installing       : lame-libs-3.100-12.el9.x86_64                                                               49/173
  Installing       : fribidi-1.0.10-6.el9.2.x86_64                                                               50/173
  Installing       : mesa-filesystem-24.2.8-2.el9_6.x86_64                                                       51/173
  Installing       : sqlite-3.34.1-8.el9_6.x86_64                                                                52/173
  Installing       : perl-Error-1:0.17029-7.el9.noarch                                                           53/173
  Installing       : libasyncns-0.8-22.el9.x86_64                                                                54/173
  Installing       : mtdev-1.1.5-22.el9.x86_64                                                                   55/173
  Installing       : opus-1.3.1-10.el9.x86_64                                                                    56/173
  Installing       : libsndfile-1.0.31-9.el9.x86_64                                                              57/173
  Installing       : perl-File-Find-1.37-481.1.el9_6.noarch                                                      58/173
  Installing       : alsa-lib-1.2.13-2.el9.x86_64                                                                59/173
  Installing       : libwacom-data-1.12.1-3.el9_4.noarch                                                         60/173
  Installing       : xmlrpc-c-1.51.0-16.el9.x86_64                                                               61/173
  Installing       : pcre2-utf32-10.40-6.el9.x86_64                                                              62/173
  Installing       : libdatrie-0.2.13-4.el9.x86_64                                                               63/173
  Installing       : libthai-0.1.28-8.el9.x86_64                                                                 64/173
  Installing       : uuid-1.6.2-55.el9.x86_64                                                                    65/173
  Installing       : llvm-libs-19.1.7-1.el9.x86_64                                                               66/173
  Installing       : emacs-filesystem-1:27.2-14.el9_6.2.noarch                                                   67/173
  Installing       : libevdev-1.11.0-3.el9.x86_64                                                                68/173
  Installing       : xkeyboard-config-2.33-2.el9.noarch                                                          69/173
  Installing       : libxkbcommon-1.0.3-4.el9.x86_64                                                             70/173
  Installing       : openblas-0.3.26-2.el9.x86_64                                                                71/173
  Installing       : openblas-openmp-0.3.26-2.el9.x86_64                                                         72/173
  Installing       : flexiblas-openblas-openmp-3.0.4-8.el9.0.1.x86_64                                            73/173
  Installing       : flexiblas-netlib-3.0.4-8.el9.0.1.x86_64                                                     74/173
  Installing       : perl-lib-0.65-481.1.el9_6.x86_64                                                            75/173
  Running scriptlet: xml-common-0.6.3-58.el9.noarch                                                              76/173
  Installing       : xml-common-0.6.3-58.el9.noarch                                                              76/173
  Installing       : liburing-2.5-1.el9.x86_64                                                                   77/173
  Installing       : qemu-img-17:9.1.0-15.el9_6.7.x86_64                                                         78/173
  Installing       : libXau-1.0.9-8.el9.x86_64                                                                   79/173
  Installing       : libxcb-1.13.1-9.el9.x86_64                                                                  80/173
  Installing       : xcb-util-wm-0.4.1-22.el9.x86_64                                                             81/173
  Installing       : xcb-util-renderutil-0.3.9-20.el9.0.1.x86_64                                                 82/173
  Installing       : xcb-util-0.4.0-19.el9.x86_64                                                                83/173
  Installing       : xcb-util-image-0.4.0-19.el9.0.1.x86_64                                                      84/173
  Installing       : pulseaudio-libs-15.0-3.el9.x86_64                                                           85/173
  Installing       : libxkbcommon-x11-1.0.3-4.el9.x86_64                                                         86/173
  Installing       : xcb-util-keysyms-0.4.0-17.el9.x86_64                                                        87/173
  Installing       : jbigkit-libs-2.1-23.el9.x86_64                                                              88/173
  Installing       : libtiff-4.4.0-13.el9.x86_64                                                                 89/173
  Installing       : libX11-common-1.7.0-11.el9.noarch                                                           90/173
  Installing       : libX11-1.7.0-11.el9.x86_64                                                                  91/173
  Installing       : libXext-1.3.4-8.el9.x86_64                                                                  92/173
  Installing       : libXrender-0.9.10-16.el9.x86_64                                                             93/173
  Installing       : libXxf86vm-1.1.4-18.el9.x86_64                                                              94/173
  Installing       : gnuplot-common-5.4.3-2.el9.x86_64                                                           95/173
  Installing       : libXpm-3.5.13-10.el9.x86_64                                                                 96/173
  Installing       : libXfixes-5.0.3-16.el9.x86_64                                                               97/173
  Installing       : libxkbfile-1.1.0-8.el9.x86_64                                                               98/173
  Installing       : nodejs-libs-1:16.20.2-8.el9_4.x86_64                                                        99/173
  Installing       : perl-DynaLoader-1.47-481.1.el9_6.x86_64                                                    100/173
  Installing       : perl-TermReadKey-2.38-11.el9.x86_64                                                        101/173
  Installing       : perl-Git-2.47.3-1.el9_6.noarch                                                             102/173
  Installing       : git-2.47.3-1.el9_6.x86_64                                                                  103/173
  Installing       : nodejs-docs-1:16.20.2-8.el9_4.noarch                                                       104/173
  Installing       : nodejs-full-i18n-1:16.20.2-8.el9_4.x86_64                                                  105/173
  Installing       : nodejs-1:16.20.2-8.el9_4.x86_64                                                            106/173
  Installing       : npm-1:8.19.4-1.16.20.2.8.el9_4.x86_64                                                      107/173
  Installing       : libusbx-1.0.26-1.el9.x86_64                                                                108/173
  Installing       : libkadm5-1.21.1-8.el9_6.x86_64                                                             109/173
  Installing       : rsync-3.2.5-3.el9.x86_64                                                                   110/173
  Installing       : graphite2-1.3.14-9.el9.x86_64                                                              111/173
  Installing       : freetype-2.10.4-10.el9_5.x86_64                                                            112/173
  Installing       : harfbuzz-2.7.4-10.el9.x86_64                                                               113/173
  Installing       : fontconfig-2.14.0-2.el9_1.x86_64                                                           114/173
  Running scriptlet: fontconfig-2.14.0-2.el9_1.x86_64                                                           114/173
  Installing       : cairo-1.17.4-7.el9.x86_64                                                                  115/173
  Installing       : libXft-2.3.3-8.el9.x86_64                                                                  116/173
  Installing       : pango-1.48.7-3.el9.x86_64                                                                  117/173
  Installing       : gd-2.3.2-3.el9.x86_64                                                                      118/173
  Installing       : python3-setuptools-53.0.0-13.el9_6.1.noarch                                                119/173
  Installing       : python3-numpy-1:1.23.5-1.el9.x86_64                                                        120/173
  Installing       : libgudev-237-1.el9.x86_64                                                                  121/173
  Installing       : libwacom-1.12.1-3.el9_4.x86_64                                                             122/173
  Installing       : libinput-1.19.3-5.el9_6.x86_64                                                             123/173
  Running scriptlet: libinput-1.19.3-5.el9_6.x86_64                                                             123/173
  Installing       : libproxy-0.4.15-35.el9.x86_64                                                              124/173
  Installing       : qt5-qtbase-common-5.15.9-11.el9_6.noarch                                                   125/173
  Running scriptlet: qt5-qtbase-5.15.9-11.el9_6.x86_64                                                          126/173
  Installing       : qt5-qtbase-5.15.9-11.el9_6.x86_64                                                          126/173
  Running scriptlet: qt5-qtbase-5.15.9-11.el9_6.x86_64                                                          126/173
  Installing       : tar-2:1.34-7.el9.x86_64                                                                    127/173
  Installing       : pkgconf-m4-1.7.3-10.el9.noarch                                                             128/173
  Installing       : libpkgconf-1.7.3-10.el9.x86_64                                                             129/173
  Installing       : pkgconf-1.7.3-10.el9.x86_64                                                                130/173
  Installing       : pkgconf-pkg-config-1.7.3-10.el9.x86_64                                                     131/173
  Installing       : libsodium-devel-1.0.18-8.el9.x86_64                                                        132/173
  Installing       : libunwind-devel-1.6.2-1.el9.x86_64                                                         133/173
  Installing       : openpgm-devel-5.2.122-28.el9.x86_64                                                        134/173
  Installing       : bash-completion-1:2.11-5.el9.noarch                                                        135/173
  Installing       : keyutils-libs-devel-1.6.3-1.el9.x86_64                                                     136/173
  Installing       : libverto-devel-0.3.2-3.el9.x86_64                                                          137/173
  Installing       : pcre2-devel-10.40-6.el9.x86_64                                                             138/173
  Installing       : libcom_err-devel-1.46.5-7.el9.x86_64                                                       139/173
  Installing       : libsepol-devel-3.6-2.el9.x86_64                                                            140/173
  Installing       : libselinux-devel-3.6-3.el9.x86_64                                                          141/173
  Installing       : krb5-devel-1.21.1-8.el9_6.x86_64                                                           142/173
  Installing       : zeromq-devel-4.3.4-2.el9.x86_64                                                            143/173
  Installing       : opennebula-libs-6.10.0.1-1.el9.noarch                                                      144/173
  Running scriptlet: opennebula-libs-6.10.0.1-1.el9.noarch                                                      144/173
  Installing       : libpciaccess-0.16-7.el9.x86_64                                                             145/173
  Installing       : libdrm-2.4.123-2.el9.x86_64                                                                146/173
  Installing       : mesa-libglapi-24.2.8-2.el9_6.x86_64                                                        147/173
  Installing       : mesa-libgbm-24.2.8-2.el9_6.x86_64                                                          148/173
  Installing       : libglvnd-egl-1:1.3.4-1.el9.x86_64                                                          149/173
  Installing       : mesa-libEGL-24.2.8-2.el9_6.x86_64                                                          150/173
  Installing       : mesa-dri-drivers-24.2.8-2.el9_6.x86_64                                                     151/173
  Installing       : libglvnd-glx-1:1.3.4-1.el9.x86_64                                                          152/173
  Installing       : mesa-libGL-24.2.8-2.el9_6.x86_64                                                           153/173
  Installing       : glx-utils-8.4.0-12.20210504git0f9e7d9.el9.0.1.x86_64                                       154/173
  Installing       : avahi-libs-0.8-22.el9_6.1.x86_64                                                           155/173
  Installing       : cups-libs-1:2.3.3op2-33.el9.x86_64                                                         156/173
  Installing       : qt5-qtbase-gui-5.15.9-11.el9_6.x86_64                                                      157/173
  Installing       : qt5-qtsvg-5.15.9-2.el9.x86_64                                                              158/173
  Installing       : freerdp-libs-2:2.11.7-1.el9.x86_64                                                         159/173
  Installing       : info-6.7-15.el9.x86_64                                                                     160/173
  Installing       : ed-1.14.2-12.el9.x86_64                                                                    161/173
  Installing       : patch-2.7.6-16.el9.x86_64                                                                  162/173
  Installing       : opennebula-provision-data-6.10.0.1-1.el9.noarch                                            163/173
  Installing       : libusal-1.1.11-48.el9.x86_64                                                               164/173
  Installing       : genisoimage-1.1.11-48.el9.x86_64                                                           165/173
  Running scriptlet: genisoimage-1.1.11-48.el9.x86_64                                                           165/173
  Installing       : libssh2-1.11.0-1.el9.x86_64                                                                166/173
  Running scriptlet: opennebula-guacd-6.10.0.1-1.2.0+1.el9.x86_64                                               167/173
  Installing       : opennebula-guacd-6.10.0.1-1.2.0+1.el9.x86_64                                               167/173
  Running scriptlet: opennebula-guacd-6.10.0.1-1.2.0+1.el9.x86_64                                               167/173
  Installing       : libcerf-1.17-2.el9.x86_64                                                                  168/173
  Installing       : gnuplot-5.4.3-2.el9.x86_64                                                                 169/173
  Installing       : opennebula-tools-6.10.0.1-1.el9.noarch                                                     170/173
  Running scriptlet: opennebula-6.10.0.1-1.el9.x86_64                                                           171/173
  Installing       : opennebula-6.10.0.1-1.el9.x86_64                                                           171/173
  Running scriptlet: opennebula-6.10.0.1-1.el9.x86_64                                                           171/173
Generating public/private rsa key pair.
Your identification has been saved in /var/lib/one/.ssh/id_rsa
Your public key has been saved in /var/lib/one/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:06ubhKbhbS7sysrKOMWX4hacW0ZrTrgy0sWqjzfPa68 oneadmin@frontend
The key's randomart image is:
+---[RSA 3072]----+
|                 |
|                 |
|                 |
|    .    .       |
| o = o  S .      |
|  O @  . . .     |
| + /. o . .      |
|OoXo==.. o       |
|O%+*EB+ +.       |
+----[SHA256]-----+

  Running scriptlet: opennebula-sunstone-6.10.0.1-1.el9.noarch                                                  172/173
  Installing       : opennebula-sunstone-6.10.0.1-1.el9.noarch                                                  172/173
  Running scriptlet: opennebula-sunstone-6.10.0.1-1.el9.noarch                                                  172/173
  Running scriptlet: opennebula-fireedge-6.10.0.1-1.el9.x86_64                                                  173/173
  Installing       : opennebula-fireedge-6.10.0.1-1.el9.x86_64                                                  173/173
  Running scriptlet: opennebula-fireedge-6.10.0.1-1.el9.x86_64                                                  173/173
  Running scriptlet: fontconfig-2.14.0-2.el9_1.x86_64                                                           173/173
  Running scriptlet: gnuplot-5.4.3-2.el9.x86_64                                                                 173/173
  Running scriptlet: opennebula-fireedge-6.10.0.1-1.el9.x86_64                                                  173/173
  Verifying        : genisoimage-1.1.11-48.el9.x86_64                                                             1/173
  Verifying        : gnuplot-5.4.3-2.el9.x86_64                                                                   2/173
  Verifying        : gnuplot-common-5.4.3-2.el9.x86_64                                                            3/173
  Verifying        : libcerf-1.17-2.el9.x86_64                                                                    4/173
  Verifying        : libsodium-1.0.18-8.el9.x86_64                                                                5/173
  Verifying        : libsodium-devel-1.0.18-8.el9.x86_64                                                          6/173
  Verifying        : libssh2-1.11.0-1.el9.x86_64                                                                  7/173
  Verifying        : libunwind-1.6.2-1.el9.x86_64                                                                 8/173
  Verifying        : libunwind-devel-1.6.2-1.el9.x86_64                                                           9/173
  Verifying        : libusal-1.1.11-48.el9.x86_64                                                                10/173
  Verifying        : libvncserver-0.9.13-11.el9.x86_64                                                           11/173
  Verifying        : openpgm-5.2.122-28.el9.x86_64                                                               12/173
  Verifying        : openpgm-devel-5.2.122-28.el9.x86_64                                                         13/173
  Verifying        : zeromq-4.3.4-2.el9.x86_64                                                                   14/173
  Verifying        : zeromq-devel-4.3.4-2.el9.x86_64                                                             15/173
  Verifying        : opennebula-6.10.0.1-1.el9.x86_64                                                            16/173
  Verifying        : opennebula-common-6.10.0.1-1.el9.noarch                                                     17/173
  Verifying        : opennebula-common-onecfg-6.10.0.1-1.el9.noarch                                              18/173
  Verifying        : opennebula-fireedge-6.10.0.1-1.el9.x86_64                                                   19/173
  Verifying        : opennebula-guacd-6.10.0.1-1.2.0+1.el9.x86_64                                                20/173
  Verifying        : opennebula-libs-6.10.0.1-1.el9.noarch                                                       21/173
  Verifying        : opennebula-provision-data-6.10.0.1-1.el9.noarch                                             22/173
  Verifying        : opennebula-rubygems-6.10.0.1-1.el9.x86_64                                                   23/173
  Verifying        : opennebula-sunstone-6.10.0.1-1.el9.noarch                                                   24/173
  Verifying        : opennebula-tools-6.10.0.1-1.el9.noarch                                                      25/173
  Verifying        : libicu-67.1-10.el9_6.x86_64                                                                 26/173
  Verifying        : info-6.7-15.el9.x86_64                                                                      27/173
  Verifying        : cups-libs-1:2.3.3op2-33.el9.x86_64                                                          28/173
  Verifying        : harfbuzz-2.7.4-10.el9.x86_64                                                                29/173
  Verifying        : dejavu-sans-fonts-2.37-18.el9.noarch                                                        30/173
  Verifying        : libpng-2:1.6.37-12.el9.x86_64                                                               31/173
  Verifying        : bash-completion-1:2.11-5.el9.noarch                                                         32/173
  Verifying        : ed-1.14.2-12.el9.x86_64                                                                     33/173
  Verifying        : pkgconf-1.7.3-10.el9.x86_64                                                                 34/173
  Verifying        : avahi-libs-0.8-22.el9_6.1.x86_64                                                            35/173
  Verifying        : libpciaccess-0.16-7.el9.x86_64                                                              36/173
  Verifying        : libpkgconf-1.7.3-10.el9.x86_64                                                              37/173
  Verifying        : fonts-filesystem-1:2.0.5-7.el9.1.noarch                                                     38/173
  Verifying        : libquadmath-11.5.0-5.el9_5.x86_64                                                           39/173
  Verifying        : pkgconf-m4-1.7.3-10.el9.noarch                                                              40/173
  Verifying        : tar-2:1.34-7.el9.x86_64                                                                     41/173
  Verifying        : libproxy-0.4.15-35.el9.x86_64                                                               42/173
  Verifying        : pkgconf-pkg-config-1.7.3-10.el9.x86_64                                                      43/173
  Verifying        : freetype-2.10.4-10.el9_5.x86_64                                                             44/173
  Verifying        : libgudev-237-1.el9.x86_64                                                                   45/173
  Verifying        : python3-setuptools-53.0.0-13.el9_6.1.noarch                                                 46/173
  Verifying        : graphite2-1.3.14-9.el9.x86_64                                                               47/173
  Verifying        : rsync-3.2.5-3.el9.x86_64                                                                    48/173
  Verifying        : libgfortran-11.5.0-5.el9_5.x86_64                                                           49/173
  Verifying        : libkadm5-1.21.1-8.el9_6.x86_64                                                              50/173
  Verifying        : libusbx-1.0.26-1.el9.x86_64                                                                 51/173
  Verifying        : flac-libs-1.3.3-10.el9_2.1.x86_64                                                           52/173
  Verifying        : rubygem-json-2.5.1-165.el9_5.x86_64                                                         53/173
  Verifying        : flexiblas-openblas-openmp-3.0.4-8.el9.0.1.x86_64                                            54/173
  Verifying        : libwinpr-2:2.11.7-1.el9.x86_64                                                              55/173
  Verifying        : libXxf86vm-1.1.4-18.el9.x86_64                                                              56/173
  Verifying        : libXpm-3.5.13-10.el9.x86_64                                                                 57/173
  Verifying        : libthai-0.1.28-8.el9.x86_64                                                                 58/173
  Verifying        : nodejs-docs-1:16.20.2-8.el9_4.noarch                                                        59/173
  Verifying        : libglvnd-1:1.3.4-1.el9.x86_64                                                               60/173
  Verifying        : libtiff-4.4.0-13.el9.x86_64                                                                 61/173
  Verifying        : perl-DynaLoader-1.47-481.1.el9_6.x86_64                                                     62/173
  Verifying        : libwayland-client-1.21.0-1.el9.x86_64                                                       63/173
  Verifying        : libselinux-devel-3.6-3.el9.x86_64                                                           64/173
  Verifying        : rubygem-bundler-2.2.33-165.el9_5.noarch                                                     65/173
  Verifying        : keyutils-libs-devel-1.6.3-1.el9.x86_64                                                      66/173
  Verifying        : libXrender-0.9.10-16.el9.x86_64                                                             67/173
  Verifying        : qt5-qtbase-common-5.15.9-11.el9_6.noarch                                                    68/173
  Verifying        : nodejs-libs-1:16.20.2-8.el9_4.x86_64                                                        69/173
  Verifying        : libwebp-1.2.0-8.el9.x86_64                                                                  70/173
  Verifying        : xcb-util-wm-0.4.1-22.el9.x86_64                                                             71/173
  Verifying        : python3-numpy-1:1.23.5-1.el9.x86_64                                                         72/173
  Verifying        : libX11-common-1.7.0-11.el9.noarch                                                           73/173
  Verifying        : jbigkit-libs-2.1-23.el9.x86_64                                                              74/173
  Verifying        : pcre2-utf16-10.40-6.el9.x86_64                                                              75/173
  Verifying        : libverto-devel-0.3.2-3.el9.x86_64                                                           76/173
  Verifying        : libXau-1.0.9-8.el9.x86_64                                                                   77/173
  Verifying        : mesa-libGL-24.2.8-2.el9_6.x86_64                                                            78/173
  Verifying        : augeas-libs-1.14.1-2.el9.x86_64                                                             79/173
  Verifying        : xcb-util-renderutil-0.3.9-20.el9.0.1.x86_64                                                 80/173
  Verifying        : mesa-libglapi-24.2.8-2.el9_6.x86_64                                                         81/173
  Verifying        : ruby-3.0.7-165.el9_5.x86_64                                                                 82/173
  Verifying        : liburing-2.5-1.el9.x86_64                                                                   83/173
  Verifying        : libinput-1.19.3-5.el9_6.x86_64                                                              84/173
  Verifying        : libXext-1.3.4-8.el9.x86_64                                                                  85/173
  Verifying        : xml-common-0.6.3-58.el9.noarch                                                              86/173
  Verifying        : perl-lib-0.65-481.1.el9_6.x86_64                                                            87/173
  Verifying        : glx-utils-8.4.0-12.20210504git0f9e7d9.el9.0.1.x86_64                                        88/173
  Verifying        : libxshmfence-1.3-10.el9.x86_64                                                              89/173
  Verifying        : rubygem-rdoc-6.3.4.1-165.el9_5.noarch                                                       90/173
  Verifying        : langpacks-core-font-en-3.0-16.el9.noarch                                                    91/173
  Verifying        : openblas-openmp-0.3.26-2.el9.x86_64                                                         92/173
  Verifying        : flexiblas-3.0.4-8.el9.0.1.x86_64                                                            93/173
  Verifying        : flexiblas-netlib-3.0.4-8.el9.0.1.x86_64                                                     94/173
  Verifying        : libX11-xcb-1.7.0-11.el9.x86_64                                                              95/173
  Verifying        : mesa-libgbm-24.2.8-2.el9_6.x86_64                                                           96/173
  Verifying        : libglvnd-glx-1:1.3.4-1.el9.x86_64                                                           97/173
  Verifying        : libwayland-cursor-1.21.0-1.el9.x86_64                                                       98/173
  Verifying        : nodejs-full-i18n-1:16.20.2-8.el9_4.x86_64                                                   99/173
  Verifying        : openblas-0.3.26-2.el9.x86_64                                                               100/173
  Verifying        : npm-1:8.19.4-1.16.20.2.8.el9_4.x86_64                                                      101/173
  Verifying        : xkeyboard-config-2.33-2.el9.noarch                                                         102/173
  Verifying        : krb5-devel-1.21.1-8.el9_6.x86_64                                                           103/173
  Verifying        : pcre2-devel-10.40-6.el9.x86_64                                                             104/173
  Verifying        : libglvnd-egl-1:1.3.4-1.el9.x86_64                                                          105/173
  Verifying        : git-core-doc-2.47.3-1.el9_6.noarch                                                         106/173
  Verifying        : freerdp-libs-2:2.11.7-1.el9.x86_64                                                         107/173
  Verifying        : libevdev-1.11.0-3.el9.x86_64                                                               108/173
  Verifying        : emacs-filesystem-1:27.2-14.el9_6.2.noarch                                                  109/173
  Verifying        : llvm-libs-19.1.7-1.el9.x86_64                                                              110/173
  Verifying        : libcom_err-devel-1.46.5-7.el9.x86_64                                                       111/173
  Verifying        : libxcb-1.13.1-9.el9.x86_64                                                                 112/173
  Verifying        : patch-2.7.6-16.el9.x86_64                                                                  113/173
  Verifying        : rubygems-3.2.33-165.el9_5.noarch                                                           114/173
  Verifying        : git-2.47.3-1.el9_6.x86_64                                                                  115/173
  Verifying        : xcb-util-0.4.0-19.el9.x86_64                                                               116/173
  Verifying        : libsepol-devel-3.6-2.el9.x86_64                                                            117/173
  Verifying        : pulseaudio-libs-15.0-3.el9.x86_64                                                          118/173
  Verifying        : uuid-1.6.2-55.el9.x86_64                                                                   119/173
  Verifying        : libXft-2.3.3-8.el9.x86_64                                                                  120/173
  Verifying        : libxkbcommon-x11-1.0.3-4.el9.x86_64                                                        121/173
  Verifying        : libdatrie-0.2.13-4.el9.x86_64                                                              122/173
  Verifying        : pcre2-utf32-10.40-6.el9.x86_64                                                             123/173
  Verifying        : xmlrpc-c-1.51.0-16.el9.x86_64                                                              124/173
  Verifying        : libSM-1.2.3-10.el9.x86_64                                                                  125/173
  Verifying        : qt5-qtbase-gui-5.15.9-11.el9_6.x86_64                                                      126/173
  Verifying        : libwacom-data-1.12.1-3.el9_4.noarch                                                        127/173
  Verifying        : alsa-lib-1.2.13-2.el9.x86_64                                                               128/173
  Verifying        : qemu-img-17:9.1.0-15.el9_6.7.x86_64                                                        129/173
  Verifying        : rubygem-bigdecimal-3.0.0-165.el9_5.x86_64                                                  130/173
  Verifying        : perl-File-Find-1.37-481.1.el9_6.noarch                                                     131/173
  Verifying        : libwacom-1.12.1-3.el9_4.x86_64                                                             132/173
  Verifying        : gd-2.3.2-3.el9.x86_64                                                                      133/173
  Verifying        : pango-1.48.7-3.el9.x86_64                                                                  134/173
  Verifying        : xcb-util-keysyms-0.4.0-17.el9.x86_64                                                       135/173
  Verifying        : libdrm-2.4.123-2.el9.x86_64                                                                136/173
  Verifying        : cairo-1.17.4-7.el9.x86_64                                                                  137/173
  Verifying        : gsm-1.0.19-6.el9.x86_64                                                                    138/173
  Verifying        : ruby-default-gems-3.0.7-165.el9_5.noarch                                                   139/173
  Verifying        : rubygem-io-console-0.5.7-165.el9_5.x86_64                                                  140/173
  Verifying        : opus-1.3.1-10.el9.x86_64                                                                   141/173
  Verifying        : rubygem-rexml-3.2.5-165.el9_5.noarch                                                       142/173
  Verifying        : qt5-qtbase-5.15.9-11.el9_6.x86_64                                                          143/173
  Verifying        : libogg-2:1.3.4-6.el9.x86_64                                                                144/173
  Verifying        : nodejs-1:16.20.2-8.el9_4.x86_64                                                            145/173
  Verifying        : rubygem-psych-3.3.2-165.el9_5.x86_64                                                       146/173
  Verifying        : libXfixes-5.0.3-16.el9.x86_64                                                              147/173
  Verifying        : mtdev-1.1.5-22.el9.x86_64                                                                  148/173
  Verifying        : libasyncns-0.8-22.el9.x86_64                                                               149/173
  Verifying        : libvorbis-1:1.3.7-5.el9.x86_64                                                             150/173
  Verifying        : git-core-2.47.3-1.el9_6.x86_64                                                             151/173
  Verifying        : fontconfig-2.14.0-2.el9_1.x86_64                                                           152/173
  Verifying        : perl-Error-1:0.17029-7.el9.noarch                                                          153/173
  Verifying        : ruby-libs-3.0.7-165.el9_5.x86_64                                                           154/173
  Verifying        : libICE-1.0.10-8.el9.x86_64                                                                 155/173
  Verifying        : libsndfile-1.0.31-9.el9.x86_64                                                             156/173
  Verifying        : mesa-libEGL-24.2.8-2.el9_6.x86_64                                                          157/173
  Verifying        : sqlite-3.34.1-8.el9_6.x86_64                                                               158/173
  Verifying        : mesa-filesystem-24.2.8-2.el9_6.x86_64                                                      159/173
  Verifying        : fribidi-1.0.10-6.el9.2.x86_64                                                              160/173
  Verifying        : xcb-util-image-0.4.0-19.el9.0.1.x86_64                                                     161/173
  Verifying        : qt5-qtsvg-5.15.9-2.el9.x86_64                                                              162/173
  Verifying        : libxkbfile-1.1.0-8.el9.x86_64                                                              163/173
  Verifying        : libwayland-server-1.21.0-1.el9.x86_64                                                      164/173
  Verifying        : libxkbcommon-1.0.3-4.el9.x86_64                                                            165/173
  Verifying        : perl-TermReadKey-2.38-11.el9.x86_64                                                        166/173
  Verifying        : perl-Git-2.47.3-1.el9_6.noarch                                                             167/173
  Verifying        : lame-libs-3.100-12.el9.x86_64                                                              168/173
  Verifying        : mesa-dri-drivers-24.2.8-2.el9_6.x86_64                                                     169/173
  Verifying        : pixman-0.40.0-6.el9_3.x86_64                                                               170/173
  Verifying        : libjpeg-turbo-2.0.90-7.el9.x86_64                                                          171/173
  Verifying        : libxslt-1.1.34-13.el9_6.x86_64                                                             172/173
  Verifying        : libX11-1.7.0-11.el9.x86_64                                                                 173/173

Installed:
  alsa-lib-1.2.13-2.el9.x86_64                             augeas-libs-1.14.1-2.el9.x86_64
  avahi-libs-0.8-22.el9_6.1.x86_64                         bash-completion-1:2.11-5.el9.noarch
  cairo-1.17.4-7.el9.x86_64                                cups-libs-1:2.3.3op2-33.el9.x86_64
  dejavu-sans-fonts-2.37-18.el9.noarch                     ed-1.14.2-12.el9.x86_64
  emacs-filesystem-1:27.2-14.el9_6.2.noarch                flac-libs-1.3.3-10.el9_2.1.x86_64
  flexiblas-3.0.4-8.el9.0.1.x86_64                         flexiblas-netlib-3.0.4-8.el9.0.1.x86_64
  flexiblas-openblas-openmp-3.0.4-8.el9.0.1.x86_64         fontconfig-2.14.0-2.el9_1.x86_64
  fonts-filesystem-1:2.0.5-7.el9.1.noarch                  freerdp-libs-2:2.11.7-1.el9.x86_64
  freetype-2.10.4-10.el9_5.x86_64                          fribidi-1.0.10-6.el9.2.x86_64
  gd-2.3.2-3.el9.x86_64                                    genisoimage-1.1.11-48.el9.x86_64
  git-2.47.3-1.el9_6.x86_64                                git-core-2.47.3-1.el9_6.x86_64
  git-core-doc-2.47.3-1.el9_6.noarch                       glx-utils-8.4.0-12.20210504git0f9e7d9.el9.0.1.x86_64
  gnuplot-5.4.3-2.el9.x86_64                               gnuplot-common-5.4.3-2.el9.x86_64
  graphite2-1.3.14-9.el9.x86_64                            gsm-1.0.19-6.el9.x86_64
  harfbuzz-2.7.4-10.el9.x86_64                             info-6.7-15.el9.x86_64
  jbigkit-libs-2.1-23.el9.x86_64                           keyutils-libs-devel-1.6.3-1.el9.x86_64
  krb5-devel-1.21.1-8.el9_6.x86_64                         lame-libs-3.100-12.el9.x86_64
  langpacks-core-font-en-3.0-16.el9.noarch                 libICE-1.0.10-8.el9.x86_64
  libSM-1.2.3-10.el9.x86_64                                libX11-1.7.0-11.el9.x86_64
  libX11-common-1.7.0-11.el9.noarch                        libX11-xcb-1.7.0-11.el9.x86_64
  libXau-1.0.9-8.el9.x86_64                                libXext-1.3.4-8.el9.x86_64
  libXfixes-5.0.3-16.el9.x86_64                            libXft-2.3.3-8.el9.x86_64
  libXpm-3.5.13-10.el9.x86_64                              libXrender-0.9.10-16.el9.x86_64
  libXxf86vm-1.1.4-18.el9.x86_64                           libasyncns-0.8-22.el9.x86_64
  libcerf-1.17-2.el9.x86_64                                libcom_err-devel-1.46.5-7.el9.x86_64
  libdatrie-0.2.13-4.el9.x86_64                            libdrm-2.4.123-2.el9.x86_64
  libevdev-1.11.0-3.el9.x86_64                             libgfortran-11.5.0-5.el9_5.x86_64
  libglvnd-1:1.3.4-1.el9.x86_64                            libglvnd-egl-1:1.3.4-1.el9.x86_64
  libglvnd-glx-1:1.3.4-1.el9.x86_64                        libgudev-237-1.el9.x86_64
  libicu-67.1-10.el9_6.x86_64                              libinput-1.19.3-5.el9_6.x86_64
  libjpeg-turbo-2.0.90-7.el9.x86_64                        libkadm5-1.21.1-8.el9_6.x86_64
  libogg-2:1.3.4-6.el9.x86_64                              libpciaccess-0.16-7.el9.x86_64
  libpkgconf-1.7.3-10.el9.x86_64                           libpng-2:1.6.37-12.el9.x86_64
  libproxy-0.4.15-35.el9.x86_64                            libquadmath-11.5.0-5.el9_5.x86_64
  libselinux-devel-3.6-3.el9.x86_64                        libsepol-devel-3.6-2.el9.x86_64
  libsndfile-1.0.31-9.el9.x86_64                           libsodium-1.0.18-8.el9.x86_64
  libsodium-devel-1.0.18-8.el9.x86_64                      libssh2-1.11.0-1.el9.x86_64
  libthai-0.1.28-8.el9.x86_64                              libtiff-4.4.0-13.el9.x86_64
  libunwind-1.6.2-1.el9.x86_64                             libunwind-devel-1.6.2-1.el9.x86_64
  liburing-2.5-1.el9.x86_64                                libusal-1.1.11-48.el9.x86_64
  libusbx-1.0.26-1.el9.x86_64                              libverto-devel-0.3.2-3.el9.x86_64
  libvncserver-0.9.13-11.el9.x86_64                        libvorbis-1:1.3.7-5.el9.x86_64
  libwacom-1.12.1-3.el9_4.x86_64                           libwacom-data-1.12.1-3.el9_4.noarch
  libwayland-client-1.21.0-1.el9.x86_64                    libwayland-cursor-1.21.0-1.el9.x86_64
  libwayland-server-1.21.0-1.el9.x86_64                    libwebp-1.2.0-8.el9.x86_64
  libwinpr-2:2.11.7-1.el9.x86_64                           libxcb-1.13.1-9.el9.x86_64
  libxkbcommon-1.0.3-4.el9.x86_64                          libxkbcommon-x11-1.0.3-4.el9.x86_64
  libxkbfile-1.1.0-8.el9.x86_64                            libxshmfence-1.3-10.el9.x86_64
  libxslt-1.1.34-13.el9_6.x86_64                           llvm-libs-19.1.7-1.el9.x86_64
  mesa-dri-drivers-24.2.8-2.el9_6.x86_64                   mesa-filesystem-24.2.8-2.el9_6.x86_64
  mesa-libEGL-24.2.8-2.el9_6.x86_64                        mesa-libGL-24.2.8-2.el9_6.x86_64
  mesa-libgbm-24.2.8-2.el9_6.x86_64                        mesa-libglapi-24.2.8-2.el9_6.x86_64
  mtdev-1.1.5-22.el9.x86_64                                nodejs-1:16.20.2-8.el9_4.x86_64
  nodejs-docs-1:16.20.2-8.el9_4.noarch                     nodejs-full-i18n-1:16.20.2-8.el9_4.x86_64
  nodejs-libs-1:16.20.2-8.el9_4.x86_64                     npm-1:8.19.4-1.16.20.2.8.el9_4.x86_64
  openblas-0.3.26-2.el9.x86_64                             openblas-openmp-0.3.26-2.el9.x86_64
  opennebula-6.10.0.1-1.el9.x86_64                         opennebula-common-6.10.0.1-1.el9.noarch
  opennebula-common-onecfg-6.10.0.1-1.el9.noarch           opennebula-fireedge-6.10.0.1-1.el9.x86_64
  opennebula-guacd-6.10.0.1-1.2.0+1.el9.x86_64             opennebula-libs-6.10.0.1-1.el9.noarch
  opennebula-provision-data-6.10.0.1-1.el9.noarch          opennebula-rubygems-6.10.0.1-1.el9.x86_64
  opennebula-sunstone-6.10.0.1-1.el9.noarch                opennebula-tools-6.10.0.1-1.el9.noarch
  openpgm-5.2.122-28.el9.x86_64                            openpgm-devel-5.2.122-28.el9.x86_64
  opus-1.3.1-10.el9.x86_64                                 pango-1.48.7-3.el9.x86_64
  patch-2.7.6-16.el9.x86_64                                pcre2-devel-10.40-6.el9.x86_64
  pcre2-utf16-10.40-6.el9.x86_64                           pcre2-utf32-10.40-6.el9.x86_64
  perl-DynaLoader-1.47-481.1.el9_6.x86_64                  perl-Error-1:0.17029-7.el9.noarch
  perl-File-Find-1.37-481.1.el9_6.noarch                   perl-Git-2.47.3-1.el9_6.noarch
  perl-TermReadKey-2.38-11.el9.x86_64                      perl-lib-0.65-481.1.el9_6.x86_64
  pixman-0.40.0-6.el9_3.x86_64                             pkgconf-1.7.3-10.el9.x86_64
  pkgconf-m4-1.7.3-10.el9.noarch                           pkgconf-pkg-config-1.7.3-10.el9.x86_64
  pulseaudio-libs-15.0-3.el9.x86_64                        python3-numpy-1:1.23.5-1.el9.x86_64
  python3-setuptools-53.0.0-13.el9_6.1.noarch              qemu-img-17:9.1.0-15.el9_6.7.x86_64
  qt5-qtbase-5.15.9-11.el9_6.x86_64                        qt5-qtbase-common-5.15.9-11.el9_6.noarch
  qt5-qtbase-gui-5.15.9-11.el9_6.x86_64                    qt5-qtsvg-5.15.9-2.el9.x86_64
  rsync-3.2.5-3.el9.x86_64                                 ruby-3.0.7-165.el9_5.x86_64
  ruby-default-gems-3.0.7-165.el9_5.noarch                 ruby-libs-3.0.7-165.el9_5.x86_64
  rubygem-bigdecimal-3.0.0-165.el9_5.x86_64                rubygem-bundler-2.2.33-165.el9_5.noarch
  rubygem-io-console-0.5.7-165.el9_5.x86_64                rubygem-json-2.5.1-165.el9_5.x86_64
  rubygem-psych-3.3.2-165.el9_5.x86_64                     rubygem-rdoc-6.3.4.1-165.el9_5.noarch
  rubygem-rexml-3.2.5-165.el9_5.noarch                     rubygems-3.2.33-165.el9_5.noarch
  sqlite-3.34.1-8.el9_6.x86_64                             tar-2:1.34-7.el9.x86_64
  uuid-1.6.2-55.el9.x86_64                                 xcb-util-0.4.0-19.el9.x86_64
  xcb-util-image-0.4.0-19.el9.0.1.x86_64                   xcb-util-keysyms-0.4.0-17.el9.x86_64
  xcb-util-renderutil-0.3.9-20.el9.0.1.x86_64              xcb-util-wm-0.4.1-22.el9.x86_64
  xkeyboard-config-2.33-2.el9.noarch                       xml-common-0.6.3-58.el9.noarch
  xmlrpc-c-1.51.0-16.el9.x86_64                            zeromq-4.3.4-2.el9.x86_64
  zeromq-devel-4.3.4-2.el9.x86_64

Complete!
```


## 🌞 Créer un user pour se log sur la WebUI OpenNebula
🌞pour ça, il faut se log en tant que l'utilisateur oneadmin sur le serveur
une fois connecté en tant que oneadmin, inscrivez le user oneadmin et le password de votre choix dans le fichier /var/lib/one/.one/one_auth sous la forme user:password

```
PS C:\Users\Fadhil> ssh user1@10.3.1.10
user1@10.3.1.10's password:
Last login: Tue Sep 16 19:41:38 2025 from 10.3.1.1
[user1@frontend ~]$ sudo su - oneadmin
[sudo] password for user1:
Last login: Tue Sep 16 19:53:26 CEST 2025
[oneadmin@frontend ~]$ echo "oneadmin:monSuperMotDePasse" > /var/lib/one/.one/one_auth
[oneadmin@frontend ~]$ cat /var/lib/one/.one/one_auth
**oneadmin:monSuperMotDePasse**
[oneadmin@frontend ~]$
```


# 🌞 Démarrer les services OpenNebula
démarrez les services opennebula, opennebula-sunstone
activez-les aussi au démarrage de la machine

```
[user1@frontend ~]$ sudo systemctl start opennebula-sunstone
[user1@frontend ~]$ sudo systemctl status opennebula-sunstone
● opennebula-sunstone.service - OpenNebula Web UI Server
     Loaded: loaded (/usr/lib/systemd/system/opennebula-sunstone.service; disabled; preset: disabled)
     Active: active (running) since Tue 2025-09-16 21:01:51 CEST; 10min ago
    Process: 11189 ExecStartPre=/usr/sbin/logrotate -f /etc/logrotate.d/opennebula-sunstone -s /var/lib/one/.logrotate.status (code=exited, status=0/SUCCESS)
    Process: 11190 ExecStartPre=/bin/sh -c for file in /var/log/one/sunstone*.log; do if [ ! -f "$file.gz" ]; then gzip -9 "$file"; fi; done (code=exited, status=1/FAILURE)
   Main PID: 11192 (ruby)
      Tasks: 1 (limit: 11067)
     Memory: 110.7M
        CPU: 5.261s
     CGroup: /system.slice/opennebula-sunstone.service
             └─11192 /usr/bin/ruby /usr/lib/one/sunstone/sunstone-server.rb

Sep 16 21:01:55 frontend opennebula-sunstone[11192]:  :threshold_high=>66,
Sep 16 21:01:55 frontend opennebula-sunstone[11192]:  :support_fs=>["ext4", "ext3", "ext2", "xfs"],
Sep 16 21:01:55 frontend opennebula-sunstone[11192]:  :oneflow_server=>"http://localhost:2474/",
Sep 16 21:01:55 frontend opennebula-sunstone[11192]:  :routes=>["oneflow", "vcenter", "support", "nsx"],
Sep 16 21:01:55 frontend opennebula-sunstone[11192]:  :private_fireedge_endpoint=>"http://localhost:2616",
Sep 16 21:01:55 frontend opennebula-sunstone[11192]:  :public_fireedge_endpoint=>"http://localhost:2616",
Sep 16 21:01:55 frontend opennebula-sunstone[11192]:  :webauthn_avail=>true,
Sep 16 21:01:55 frontend opennebula-sunstone[11192]:  :session_expire_time=>3600}
Sep 16 21:01:55 frontend opennebula-sunstone[11192]: --------------------------------------
Sep 16 21:01:59 frontend opennebula-sunstone[11192]: == Sinatra (v3.2.0) has taken the stage on 9869 for production with backup from Thin
[user1@frontend ~]$ sudo systemctl enable opennebula-sunstone
Created symlink /etc/systemd/system/multi-user.target.wants/opennebula-sunstone.service → /usr/lib/systemd/system/opennebula-sunstone.service.
[user1@frontend ~]$ systemctl is-enabled opennebula-sunstone
enabled
[user1@frontend ~]$ sudo systemctl enable opennebula
pennebula-sunstone
[user1@frontend ~]$ sudo systemctl enable opennebula-sunstone
[user1@frontend ~]$ sudo systemctl enable opennebula
pennebula-sunstone
[user1@frontend ~]$ sudo systemctl enable opennebula-sunstone
[user1@frontend ~]$ sudo systemctl enable opennebula-sunstone
[user1@frontend ~]$ sudo systemctl enable opennebula
[user1@frontend ~]$ sudo systemctl status opennebula
● opennebula.service - OpenNebula Cloud Controller Daemon
     Loaded: loaded (/usr/lib/systemd/system/opennebula.service; enabled; preset: disabled)
     Active: active (running) since Tue 2025-09-16 21:01:51 CEST; 13min ago
   Main PID: 10964 (oned)
      Tasks: 74 (limit: 11067)
     Memory: 320.0M
        CPU: 12.104s
     CGroup: /system.slice/opennebula.service
             ├─10964 /usr/bin/oned -f
             ├─10965 /usr/bin/ruby /usr/lib/one/mads/one_hm.rb -p 2101 -l 2102 -b 127.0.0.1
             ├─10989 /usr/bin/ruby /usr/lib/one/mads/one_vmm_exec.rb -t 15 -r 0 kvm -p
             ├─11006 /usr/bin/ruby /usr/lib/one/mads/one_vmm_exec.rb -t 15 -r 0 lxc
             ├─11023 /usr/bin/ruby /usr/lib/one/mads/one_vmm_exec.rb -t 15 -r 0 kvm
             ├─11044 /usr/bin/ruby /usr/lib/one/mads/one_tm.rb -t 15 -d dummy,lvm,shared,fs_lvm,fs_lvm_ssh,qcow2,ssh,ceph,dev,vcenter,iscsi_libvirt
             ├─11067 /usr/bin/ruby /usr/lib/one/mads/one_auth_mad.rb --authn ssh,x509,ldap,server_cipher,server_x509
             ├─11082 /usr/bin/ruby /usr/lib/one/mads/one_datastore.rb -t 15 -d dummy,fs,lvm,ceph,dev,iscsi_libvirt,vcenter,restic,rsync -s shared,ssh,ceph,fs_lvm,fs_lvm_ssh,qcow2,vc>
             ├─11099 /usr/bin/ruby /usr/lib/one/mads/one_market.rb -t 15 -m http,s3,one,linuxcontainers
             ├─11116 /usr/bin/ruby /usr/lib/one/mads/one_ipam.rb -t 1 -i dummy,aws,equinix,vultr
             ├─11130 /usr/lib/one/mads/onemonitord "-c monitord.conf"
             ├─11131 /usr/bin/ruby /usr/lib/one/mads/one_im_exec.rb -r 3 -t 15 -w 90 kvm
             ├─11144 /usr/bin/ruby /usr/lib/one/mads/one_im_exec.rb -r 3 -t 15 -w 90 lxc
             └─11157 /usr/bin/ruby /usr/lib/one/mads/one_im_exec.rb -r 3 -t 15 -w 90 qemu

Sep 16 21:01:40 frontend systemd[1]: Starting OpenNebula Cloud Controller Daemon...
Sep 16 21:01:40 frontend opennebula[10962]: gzip: /var/log/one/vcenter_monitor*.log: No such file or directory
Sep 16 21:01:51 frontend systemd[1]: Started OpenNebula Cloud Controller Daemon.
lines 1-26/26 (END)
```

```
[user1@frontend ~]$ sudo systemctl status opennebula-sunstone
● opennebula-sunstone.service - OpenNebula Web UI Server
     Loaded: loaded (/usr/lib/systemd/system/opennebula-sunstone.service; enabled; preset: disabled)
     Active: active (running) since Tue 2025-09-16 21:01:51 CEST; 14min ago
   Main PID: 11192 (ruby)
      Tasks: 1 (limit: 11067)
     Memory: 110.4M
        CPU: 5.306s
     CGroup: /system.slice/opennebula-sunstone.service
             └─11192 /usr/bin/ruby /usr/lib/one/sunstone/sunstone-server.rb

Sep 16 21:01:55 frontend opennebula-sunstone[11192]:  :threshold_high=>66,
Sep 16 21:01:55 frontend opennebula-sunstone[11192]:  :support_fs=>["ext4", "ext3", "ext2", "xfs"],
Sep 16 21:01:55 frontend opennebula-sunstone[11192]:  :oneflow_server=>"http://localhost:2474/",
Sep 16 21:01:55 frontend opennebula-sunstone[11192]:  :routes=>["oneflow", "vcenter", "support", "nsx"],
Sep 16 21:01:55 frontend opennebula-sunstone[11192]:  :private_fireedge_endpoint=>"http://localhost:2616",
Sep 16 21:01:55 frontend opennebula-sunstone[11192]:  :public_fireedge_endpoint=>"http://localhost:2616",
Sep 16 21:01:55 frontend opennebula-sunstone[11192]:  :webauthn_avail=>true,
Sep 16 21:01:55 frontend opennebula-sunstone[11192]:  :session_expire_time=>3600}
Sep 16 21:01:55 frontend opennebula-sunstone[11192]: --------------------------------------
Sep 16 21:01:59 frontend opennebula-sunstone[11192]: == Sinatra (v3.2.0) has taken the stage on 9869 for production with backup from Thin
[user1@frontend ~]$ sudo ss -ltpn
State            Recv-Q           Send-Q                     Local Address:Port                        Peer Address:Port           Process
LISTEN           0                15                               0.0.0.0:2633                             0.0.0.0:*               users:(("oned",pid=10964,fd=4))
LISTEN           0                100                            127.0.0.1:2101                             0.0.0.0:*               users:(("one_hm.rb",pid=10965,fd=11))
LISTEN           0                100                            127.0.0.1:2102                             0.0.0.0:*               users:(("one_hm.rb",pid=10965,fd=13))
LISTEN           0                100                              0.0.0.0:9869                             0.0.0.0:*               users:(("ruby",pid=11192,fd=8))
LISTEN           0                8                                0.0.0.0:4124                             0.0.0.0:*               users:(("onemonitord",pid=11130,fd=11))
LISTEN           0                128                              0.0.0.0:22                               0.0.0.0:*               users:(("sshd",pid=723,fd=3))
LISTEN           0                100                              0.0.0.0:29876                            0.0.0.0:*               users:(("python",pid=10936,fd=0))
LISTEN           0                128                                 [::]:22                                  [::]:*               users:(("sshd",pid=723,fd=4))
LISTEN           0                151                                    *:3306                                   *:*               users:(("mysqld",pid=4074,fd=24))
LISTEN           0                70                                     *:33060                                  *:*               users:(("mysqld",pid=4074,fd=21))
```


```
[user1@frontend ~]$ sudo !!
sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3 enp0s8
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 48830/tcp
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
[user1@frontend ~]$ sudo firewall-cmd --add-port=9869/tcp --permanent
success
[user1@frontend ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3 enp0s8
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 48830/tcp
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
[user1@frontend ~]$ sudo firewall-cmd --reload
success
[user1@frontend ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3 enp0s8
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 48830/tcp 9869/tcp
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
  ```

## 🌞 Configuration OpenNebula
dans le fichier /etc/one/oned.conf, définissez correctement les paramètres de connexion à la base de données, c'est la clause DB = que vous devez remplacer par
```
[user1@frontend ~]$ sudo vim /etc/one/oned.conf
[user1@frontend ~]$ oned -v
OpenNebula 6.10.0.1 (47a5d0fe)
Copyright 2002-2024, OpenNebula Project, OpenNebula Systems

Licensed under the Apache License, Version 2.0 (the "License"); you may not
use this file except in compliance with the License. You may obtain a copy
of the License at http://www.apache.org/licenses/LICENSE-2.0
[user1@frontend ~]$
```

monSuperMotDePasse

## C. Conf système¶

🌞 Ouverture firewall

    ouvrez les ports suivants, avec des commandes firewall-cmd :

Port 	Proto 	Why ?
9869 	TCP 	WebUI (Sunstone)
22 	TCP 	SSH
2633 	TCP 	Daemon oned et API XML RPC
4124 	TPC et UDP 	Monitoring
29876 	TCP 	NoVNC proxy

```
[user1@frontend ~]$ sudo firewall-cmd --permanent --add-port=9869/tcp
Warning: ALREADY_ENABLED: 9869:tcp
success
[user1@frontend ~]$ sudo firewall-cmd --permanent --add-port=22/tcp
success
[user1@frontend ~]$ sudo firewall-cmd --permanent --add-port=2633/tcp
success
[user1@frontend ~]$ sudo firewall-cmd --permanent --add-port=4124/tcp
irewall-cmd --permanent --add-port=4124/udpsuccess
[user1@frontend ~]$ sudo firewall-cmd --permanent --add-port=4124/udp
success
[user1@frontend ~]$ sudo firewall-cmd --permanent --add-port=4124/tcp
Warning: ALREADY_ENABLED: 4124:tcp
success
[user1@frontend ~]$ sudo firewall-cmd --permanent --add-port=29876/tcp
success
[user1@frontend ~]$ sudo firewall-cmd --reload
success
[user1@frontend ~]$ sudo firewall-cmd --list-ports
22/tcp 2633/tcp 4124/tcp 9869/tcp 29876/tcp 48830/tcp 4124/udp
```


# II.2. Noeuds KVM
## 🌞 Étape A : Ajouter les dépôts
1. Dépôt OpenNebula
```
PS C:\Users\Fadhil> ssh user1@10.3.1.11
user1@10.3.1.11's password:
Last login: Tue Sep 16 17:31:21 2025 from 10.3.1.1
[user1@kvm1 ~]$ sudo vim /etc/yum.repos.d/opennebula.repo
[sudo] password for user1:
[user1@kvm1 ~]$ sudo tee /etc/yum.repos.d/opennebula.repo > /dev/null <<EOF
> [opennebula]
> name=OpenNebula Community Edition
> baseurl=https://downloads.opennebula.io/repo/6.10/RedHat/\$releasever/\$basearch
> enabled=1
> gpgkey=https://downloads.opennebula.io/repo/repo2.key
> gpgcheck=1
> repo_gpgcheck=1
> EOF
[user1@kvm1 ~]$ dnf repolist
repo id                                                                      repo name
appstream                                                                    Rocky Linux 9 - AppStream
baseos                                                                       Rocky Linux 9 - BaseOS
extras                                                                       Rocky Linux 9 - Extras
opennebula                                                                   OpenNebula Community Edition
```



### ajoutez aussi les dépôts du serveur MySQL communautaire
le RPM de la partie précédente (comme sur le frontend)

```
[user1@kvm1 ~]$ sudo dnf makecache
OpenNebula Community Edition                                                                                                                1.1 kB/s | 833  B     00:00
OpenNebula Community Edition                                                                                                                 10 kB/s | 3.1 kB     00:00
Importing GPG key 0x906DC27C:
 Userid     : "OpenNebula Repository <contact@opennebula.io>"
 Fingerprint: 0B2D 385C 7C93 04B1 1A03 67B9 05A0 5927 906D C27C
 From       : https://downloads.opennebula.io/repo/repo2.key
Is this ok [y/N]: y
OpenNebula Community Edition                                                                                                                595 kB/s | 690 kB     00:01
Rocky Linux 9 - BaseOS                                                                                                                      6.8 kB/s | 4.1 kB     00:00
Rocky Linux 9 - AppStream                                                                                                                   6.1 kB/s | 4.5 kB     00:00
Rocky Linux 9 - Extras                                                                                                                      3.7 kB/s | 2.9 kB     00:00
Metadata cache created.
[user1@kvm1 ~]$ dnf repolist | grep mysql
[user1@kvm1 ~]$ sudo dnf install -y https://dev.mysql.com/get/mysql80-community-release-el9-1.noarch.rpm
Last metadata expiration check: 0:01:37 ago on Wed Sep 17 00:40:02 2025.
mysql80-community-release-el9-1.noarch.rpm                                                                                                   14 kB/s |  10 kB     00:00
Dependencies resolved.
============================================================================================================================================================================
 Package                                               Architecture                       Version                            Repository                                Size
============================================================================================================================================================================
Installing:
 mysql80-community-release                             noarch                             el9-1                              @commandline                              10 k

Transaction Summary
============================================================================================================================================================================
Install  1 Package

Total size: 10 k
Installed size: 5.7 k
Downloading Packages:
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                    1/1
  Installing       : mysql80-community-release-el9-1.noarch                                                                                                             1/1
  Verifying        : mysql80-community-release-el9-1.noarch                                                                                                             1/1

Installed:
  mysql80-community-release-el9-1.noarch

Complete!
[user1@kvm1 ~]$ dnf repolist | grep mysql
mysql-connectors-community             MySQL Connectors Community
mysql-tools-community                  MySQL Tools Community
mysql80-community                      MySQL 8.0 Community Server
```

### ajoutez aussi les dépôts EPEL en exécutant :


````
[user1@kvm1 ~]$ sudo dnf install -y epel-release
[sudo] password for user1:
MySQL 8.0 Community Server                                                                                                                  3.0 MB/s | 2.7 MB     00:00
MySQL Connectors Community                                                                                                                  239 kB/s |  90 kB     00:00
MySQL Tools Community                                                                                                                       1.8 MB/s | 1.2 MB     00:00
Dependencies resolved.
============================================================================================================================================================================
 Package                                      Architecture                           Version                                   Repository                              Size
============================================================================================================================================================================
Installing:
 epel-release                                 noarch                                 9-7.el9                                   extras                                  19 k

Transaction Summary
============================================================================================================================================================================
Install  1 Package

Total download size: 19 k
Installed size: 26 k
Downloading Packages:
epel-release-9-7.el9.noarch.rpm                                                                                                              92 kB/s |  19 kB     00:00
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                        30 kB/s |  19 kB     00:00
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                    1/1
  Installing       : epel-release-9-7.el9.noarch                                                                                                                        1/1
  Running scriptlet: epel-release-9-7.el9.noarch                                                                                                                        1/1
Many EPEL packages require the CodeReady Builder (CRB) repository.
It is recommended that you run /usr/bin/crb enable to enable the CRB repository.

  Verifying        : epel-release-9-7.el9.noarch                                                                                                                        1/1

Installed:
  epel-release-9-7.el9.noarch

Complete!
```


🌞 Installer les libs MySQL

```
[user1@kvm1 ~]$ sudo dnf install -y mysql-community-server
Extra Packages for Enterprise Linux 9 - x86_64                                                                                              3.8 MB/s |  20 MB     00:05
Extra Packages for Enterprise Linux 9 openh264 (From Cisco) - x86_64                                                                        2.2 kB/s | 2.5 kB     00:01
Last metadata expiration check: 0:00:01 ago on Wed Sep 17 00:53:00 2025.
Dependencies resolved.
============================================================================================================================================================================
 Package                                             Architecture                Version                                       Repository                              Size
============================================================================================================================================================================
Installing:
 mysql-community-server                              x86_64                      8.0.43-1.el9                                  mysql80-community                       50 M
Installing dependencies:
 libtirpc                                            x86_64                      1.3.3-9.el9                                   baseos                                  93 k
 mysql-community-client                              x86_64                      8.0.43-1.el9                                  mysql80-community                      3.3 M
 mysql-community-client-plugins                      x86_64                      8.0.43-1.el9                                  mysql80-community                      1.4 M
 mysql-community-common                              x86_64                      8.0.43-1.el9                                  mysql80-community                      556 k
 mysql-community-icu-data-files                      x86_64                      8.0.43-1.el9                                  mysql80-community                      2.3 M
 mysql-community-libs                                x86_64                      8.0.43-1.el9                                  mysql80-community                      1.5 M
 net-tools                                           x86_64                      2.0-0.64.20160912git.el9                      baseos                                 294 k
 perl-AutoLoader                                     noarch                      5.74-481.1.el9_6                              appstream                               20 k
 perl-B                                              x86_64                      1.80-481.1.el9_6                              appstream                              178 k
 perl-Carp                                           noarch                      1.50-460.el9                                  appstream                               29 k
 perl-Class-Struct                                   noarch                      0.66-481.1.el9_6                              appstream                               21 k
 perl-Data-Dumper                                    x86_64                      2.174-462.el9                                 appstream                               55 k
 perl-Digest                                         noarch                      1.19-4.el9                                    appstream                               25 k
 perl-Digest-MD5                                     x86_64                      2.58-4.el9                                    appstream                               36 k
 perl-Encode                                         x86_64                      4:3.08-462.el9                                appstream                              1.7 M
 perl-Errno                                          x86_64                      1.30-481.1.el9_6                              appstream                               13 k
 perl-Exporter                                       noarch                      5.74-461.el9                                  appstream                               31 k
 perl-Fcntl                                          x86_64                      1.13-481.1.el9_6                              appstream                               19 k
 perl-File-Basename                                  noarch                      2.85-481.1.el9_6                              appstream                               16 k
 perl-File-Path                                      noarch                      2.18-4.el9                                    appstream                               35 k
 perl-File-Temp                                      noarch                      1:0.231.100-4.el9                             appstream                               59 k
 perl-File-stat                                      noarch                      1.09-481.1.el9_6                              appstream                               16 k
 perl-FileHandle                                     noarch                      2.03-481.1.el9_6                              appstream                               14 k
 perl-Getopt-Long                                    noarch                      1:2.52-4.el9                                  appstream                               60 k
 perl-Getopt-Std                                     noarch                      1.12-481.1.el9_6                              appstream                               14 k
 perl-HTTP-Tiny                                      noarch                      0.076-462.el9                                 appstream                               53 k
 perl-IO                                             x86_64                      1.43-481.1.el9_6                              appstream                               85 k
 perl-IO-Socket-IP                                   noarch                      0.41-5.el9                                    appstream                               42 k
 perl-IO-Socket-SSL                                  noarch                      2.073-2.el9                                   appstream                              214 k
 perl-IPC-Open3                                      noarch                      1.21-481.1.el9_6                              appstream                               21 k
 perl-MIME-Base64                                    x86_64                      3.16-4.el9                                    appstream                               30 k
 perl-Mozilla-CA                                     noarch                      20200520-6.el9                                appstream                               12 k
 perl-Net-SSLeay                                     x86_64                      1.94-1.el9                                    appstream                              391 k
 perl-POSIX                                          x86_64                      1.94-481.1.el9_6                              appstream                               95 k
 perl-PathTools                                      x86_64                      3.78-461.el9                                  appstream                               85 k
 perl-Pod-Escapes                                    noarch                      1:1.07-460.el9                                appstream                               20 k
 perl-Pod-Perldoc                                    noarch                      3.28.01-461.el9                               appstream                               83 k
 perl-Pod-Simple                                     noarch                      1:3.42-4.el9                                  appstream                              215 k
 perl-Pod-Usage                                      noarch                      4:2.01-4.el9                                  appstream                               40 k
 perl-Scalar-List-Utils                              x86_64                      4:1.56-462.el9                                appstream                               70 k
 perl-SelectSaver                                    noarch                      1.02-481.1.el9_6                              appstream                               10 k
 perl-Socket                                         x86_64                      4:2.031-4.el9                                 appstream                               54 k
 perl-Storable                                       x86_64                      1:3.21-460.el9                                appstream                               95 k
 perl-Symbol                                         noarch                      1.08-481.1.el9_6                              appstream                               13 k
 perl-Term-ANSIColor                                 noarch                      5.01-461.el9                                  appstream                               48 k
 perl-Term-Cap                                       noarch                      1.17-460.el9                                  appstream                               22 k
 perl-Text-ParseWords                                noarch                      3.30-460.el9                                  appstream                               16 k
 perl-Text-Tabs+Wrap                                 noarch                      2013.0523-460.el9                             appstream                               23 k
 perl-Time-Local                                     noarch                      2:1.300-7.el9                                 appstream                               33 k
 perl-URI                                            noarch                      5.09-3.el9                                    appstream                              108 k
 perl-base                                           noarch                      2.27-481.1.el9_6                              appstream                               15 k
 perl-constant                                       noarch                      1.33-461.el9                                  appstream                               23 k
 perl-if                                             noarch                      0.60.800-481.1.el9_6                          appstream                               13 k
 perl-interpreter                                    x86_64                      4:5.32.1-481.1.el9_6                          appstream                               69 k
 perl-libnet                                         noarch                      3.13-4.el9                                    appstream                              125 k
 perl-libs                                           x86_64                      4:5.32.1-481.1.el9_6                          appstream                              2.0 M
 perl-mro                                            x86_64                      1.23-481.1.el9_6                              appstream                               27 k
 perl-overload                                       noarch                      1.31-481.1.el9_6                              appstream                               44 k
 perl-overloading                                    noarch                      0.02-481.1.el9_6                              appstream                               11 k
 perl-parent                                         noarch                      1:0.238-460.el9                               appstream                               14 k
 perl-podlators                                      noarch                      1:4.14-460.el9                                appstream                              112 k
 perl-subs                                           noarch                      1.03-481.1.el9_6                              appstream                               10 k
 perl-vars                                           noarch                      1.05-481.1.el9_6                              appstream                               12 k
Installing weak dependencies:
 perl-NDBM_File                                      x86_64                      1.15-481.1.el9_6                              appstream                               21 k

Transaction Summary
============================================================================================================================================================================
Install  65 Packages

Total download size: 66 M
Installed size: 363 M
Downloading Packages:
(1/65): mysql-community-common-8.0.43-1.el9.x86_64.rpm                                                                                      1.4 MB/s | 556 kB     00:00
(2/65): mysql-community-client-plugins-8.0.43-1.el9.x86_64.rpm                                                                              1.5 MB/s | 1.4 MB     00:00
(3/65): mysql-community-libs-8.0.43-1.el9.x86_64.rpm                                                                                        1.2 MB/s | 1.5 MB     00:01
(4/65): mysql-community-icu-data-files-8.0.43-1.el9.x86_64.rpm                                                                              1.3 MB/s | 2.3 MB     00:01
(5/65): mysql-community-client-8.0.43-1.el9.x86_64.rpm                                                                                      1.5 MB/s | 3.3 MB     00:02
(6/65): libtirpc-1.3.3-9.el9.x86_64.rpm                                                                                                      13 kB/s |  93 kB     00:06
(7/65): mysql-community-server-8.0.43-1.el9.x86_64.rpm                                                                                      5.7 MB/s |  50 MB     00:08
(8/65): net-tools-2.0-0.64.20160912git.el9.x86_64.rpm                                                                                        34 kB/s | 294 kB     00:08
(9/65): perl-Term-Cap-1.17-460.el9.noarch.rpm                                                                                               135 kB/s |  22 kB     00:00
(10/65): perl-NDBM_File-1.15-481.1.el9_6.x86_64.rpm                                                                                         110 kB/s |  21 kB     00:00
(11/65): perl-Getopt-Long-2.52-4.el9.noarch.rpm                                                                                              30 kB/s |  60 kB     00:02
(12/65): perl-Pod-Escapes-1.07-460.el9.noarch.rpm                                                                                           276 kB/s |  20 kB     00:00
(13/65): perl-vars-1.05-481.1.el9_6.noarch.rpm                                                                                              112 kB/s |  12 kB     00:00
(14/65): perl-Net-SSLeay-1.94-1.el9.x86_64.rpm                                                                                              1.9 MB/s | 391 kB     00:00
(15/65): perl-Socket-2.031-4.el9.x86_64.rpm                                                                                                 303 kB/s |  54 kB     00:00
(16/65): perl-parent-0.238-460.el9.noarch.rpm                                                                                               124 kB/s |  14 kB     00:00
(17/65): perl-URI-5.09-3.el9.noarch.rpm                                                                                                     1.0 MB/s | 108 kB     00:00
(18/65): perl-Scalar-List-Utils-1.56-462.el9.x86_64.rpm                                                                                     631 kB/s |  70 kB     00:00
(19/65): perl-B-1.80-481.1.el9_6.x86_64.rpm                                                                                                 1.4 MB/s | 178 kB     00:00
(20/65): perl-base-2.27-481.1.el9_6.noarch.rpm                                                                                              212 kB/s |  15 kB     00:00
(21/65): perl-Getopt-Std-1.12-481.1.el9_6.noarch.rpm                                                                                        202 kB/s |  14 kB     00:00
(22/65): perl-PathTools-3.78-461.el9.x86_64.rpm                                                                                             932 kB/s |  85 kB     00:00
(23/65): perl-Pod-Perldoc-3.28.01-461.el9.noarch.rpm                                                                                        1.1 MB/s |  83 kB     00:00
(24/65): perl-HTTP-Tiny-0.076-462.el9.noarch.rpm                                                                                            513 kB/s |  53 kB     00:00
(25/65): perl-Digest-1.19-4.el9.noarch.rpm                                                                                                  310 kB/s |  25 kB     00:00
(26/65): perl-File-Basename-2.85-481.1.el9_6.noarch.rpm                                                                                     143 kB/s |  16 kB     00:00
(27/65): perl-Exporter-5.74-461.el9.noarch.rpm                                                                                              365 kB/s |  31 kB     00:00
(28/65): perl-subs-1.03-481.1.el9_6.noarch.rpm                                                                                              109 kB/s |  10 kB     00:00
(29/65): perl-MIME-Base64-3.16-4.el9.x86_64.rpm                                                                                             378 kB/s |  30 kB     00:00
(30/65): perl-Fcntl-1.13-481.1.el9_6.x86_64.rpm                                                                                             272 kB/s |  19 kB     00:00
(31/65): perl-AutoLoader-5.74-481.1.el9_6.noarch.rpm                                                                                        262 kB/s |  20 kB     00:00
(32/65): perl-Text-Tabs+Wrap-2013.0523-460.el9.noarch.rpm                                                                                   263 kB/s |  23 kB     00:00
(33/65): perl-SelectSaver-1.02-481.1.el9_6.noarch.rpm                                                                                       102 kB/s |  10 kB     00:00
(34/65): perl-IO-1.43-481.1.el9_6.x86_64.rpm                                                                                                806 kB/s |  85 kB     00:00
(35/65): perl-overload-1.31-481.1.el9_6.noarch.rpm                                                                                          514 kB/s |  44 kB     00:00
(36/65): perl-if-0.60.800-481.1.el9_6.noarch.rpm                                                                                            152 kB/s |  13 kB     00:00
(37/65): perl-POSIX-1.94-481.1.el9_6.x86_64.rpm                                                                                             797 kB/s |  95 kB     00:00
(38/65): perl-FileHandle-2.03-481.1.el9_6.noarch.rpm                                                                                        155 kB/s |  14 kB     00:00
(39/65): perl-podlators-4.14-460.el9.noarch.rpm                                                                                             1.0 MB/s | 112 kB     00:00
(40/65): perl-File-Path-2.18-4.el9.noarch.rpm                                                                                               465 kB/s |  35 kB     00:00
(41/65): perl-File-stat-1.09-481.1.el9_6.noarch.rpm                                                                                         185 kB/s |  16 kB     00:00
(42/65): perl-Storable-3.21-460.el9.x86_64.rpm                                                                                              1.0 MB/s |  95 kB     00:00
(43/65): perl-Symbol-1.08-481.1.el9_6.noarch.rpm                                                                                            132 kB/s |  13 kB     00:00
(44/65): perl-Data-Dumper-2.174-462.el9.x86_64.rpm                                                                                          830 kB/s |  55 kB     00:00
(45/65): perl-File-Temp-0.231.100-4.el9.noarch.rpm                                                                                          603 kB/s |  59 kB     00:00
(46/65): perl-Errno-1.30-481.1.el9_6.x86_64.rpm                                                                                             135 kB/s |  13 kB     00:00
(47/65): perl-Pod-Simple-3.42-4.el9.noarch.rpm                                                                                              1.7 MB/s | 215 kB     00:00
(48/65): perl-Digest-MD5-2.58-4.el9.x86_64.rpm                                                                                              356 kB/s |  36 kB     00:00
(49/65): perl-Term-ANSIColor-5.01-461.el9.noarch.rpm                                                                                        462 kB/s |  48 kB     00:00
(50/65): perl-Mozilla-CA-20200520-6.el9.noarch.rpm                                                                                          124 kB/s |  12 kB     00:00
(51/65): perl-Class-Struct-0.66-481.1.el9_6.noarch.rpm                                                                                      228 kB/s |  21 kB     00:00
(52/65): perl-Pod-Usage-2.01-4.el9.noarch.rpm                                                                                               365 kB/s |  40 kB     00:00
(53/65): perl-IO-Socket-SSL-2.073-2.el9.noarch.rpm                                                                                          1.6 MB/s | 214 kB     00:00
(54/65): perl-Carp-1.50-460.el9.noarch.rpm                                                                                                  300 kB/s |  29 kB     00:00
(55/65): perl-Time-Local-1.300-7.el9.noarch.rpm                                                                                             378 kB/s |  33 kB     00:00
(56/65): perl-IPC-Open3-1.21-481.1.el9_6.noarch.rpm                                                                                         241 kB/s |  21 kB     00:00
(57/65): perl-libnet-3.13-4.el9.noarch.rpm                                                                                                  1.0 MB/s | 125 kB     00:00
(58/65): perl-libs-5.32.1-481.1.el9_6.x86_64.rpm                                                                                            3.7 MB/s | 2.0 MB     00:00
(59/65): perl-Encode-3.08-462.el9.x86_64.rpm                                                                                                3.0 MB/s | 1.7 MB     00:00
(60/65): perl-overloading-0.02-481.1.el9_6.noarch.rpm                                                                                        24 kB/s |  11 kB     00:00
(61/65): perl-constant-1.33-461.el9.noarch.rpm                                                                                              206 kB/s |  23 kB     00:00
(62/65): perl-mro-1.23-481.1.el9_6.x86_64.rpm                                                                                               329 kB/s |  27 kB     00:00
(63/65): perl-Text-ParseWords-3.30-460.el9.noarch.rpm                                                                                       184 kB/s |  16 kB     00:00
(64/65): perl-interpreter-5.32.1-481.1.el9_6.x86_64.rpm                                                                                     766 kB/s |  69 kB     00:00
(65/65): perl-IO-Socket-IP-0.41-5.el9.noarch.rpm                                                                                            504 kB/s |  42 kB     00:00
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                       4.6 MB/s |  66 MB     00:14
MySQL 8.0 Community Server                                                                                                                  3.0 MB/s | 3.1 kB     00:00
Importing GPG key 0x3A79BD29:
 Userid     : "MySQL Release Engineering <mysql-build@oss.oracle.com>"
 Fingerprint: 859B E8D7 C586 F538 430B 19C2 467B 942D 3A79 BD29
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-mysql-2022
Key imported successfully
Import of key(s) didn't help, wrong key(s)?
Public key for mysql-community-client-8.0.43-1.el9.x86_64.rpm is not installed. Failing package is: mysql-community-client-8.0.43-1.el9.x86_64
 GPG Keys are configured as: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql-2022
Public key for mysql-community-client-plugins-8.0.43-1.el9.x86_64.rpm is not installed. Failing package is: mysql-community-client-plugins-8.0.43-1.el9.x86_64
 GPG Keys are configured as: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql-2022
Public key for mysql-community-common-8.0.43-1.el9.x86_64.rpm is not installed. Failing package is: mysql-community-common-8.0.43-1.el9.x86_64
 GPG Keys are configured as: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql-2022
Public key for mysql-community-icu-data-files-8.0.43-1.el9.x86_64.rpm is not installed. Failing package is: mysql-community-icu-data-files-8.0.43-1.el9.x86_64
 GPG Keys are configured as: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql-2022
Public key for mysql-community-libs-8.0.43-1.el9.x86_64.rpm is not installed. Failing package is: mysql-community-libs-8.0.43-1.el9.x86_64
 GPG Keys are configured as: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql-2022
Public key for mysql-community-server-8.0.43-1.el9.x86_64.rpm is not installed. Failing package is: mysql-community-server-8.0.43-1.el9.x86_64
 GPG Keys are configured as: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql-2022
The downloaded packages were saved in cache until the next successful transaction.
You can remove cached packages by executing 'dnf clean packages'.
```

🌞 Installer KVM

```
[user1@kvm1 ~]$ sudo dnf install -y opennebula-node-kvm
Last metadata expiration check: 0:05:27 ago on Wed Sep 17 00:53:00 2025.
Dependencies resolved.
============================================================================================================================================================================
 Package                                                Architecture           Version                                              Repository                         Size
============================================================================================================================================================================
Installing:
 opennebula-node-kvm                                    noarch                 6.10.0.1-1.el9                                       opennebula                         13 k
Installing dependencies:
 augeas                                                 x86_64                 1.14.1-2.el9                                         appstream                          63 k
 augeas-libs                                            x86_64                 1.14.1-2.el9                                         appstream                         373 k
 boost-iostreams                                        x86_64                 1.75.0-10.el9                                        appstream                          36 k
 boost-system                                           x86_64                 1.75.0-10.el9                                        appstream                          11 k
 boost-thread                                           x86_64                 1.75.0-10.el9                                        appstream                          53 k
 bzip2                                                  x86_64                 1.0.8-10.el9_5                                       baseos                             51 k
 capstone                                               x86_64                 4.0.2-10.el9                                         appstream                         766 k
 checkpolicy                                            x86_64                 3.6-1.el9                                            appstream                         352 k
 cyrus-sasl-gssapi                                      x86_64                 2.1.27-21.el9                                        baseos                             26 k
 daxctl-libs                                            x86_64                 78-2.el9                                             baseos                             41 k
 device-mapper-multipath-libs                           x86_64                 0.8.7-35.el9_6.1                                     baseos                            267 k
 dmidecode                                              x86_64                 1:3.6-1.el9                                          baseos                            100 k
 dnsmasq                                                x86_64                 2.85-16.el9_4                                        appstream                         326 k
 edk2-ovmf                                              noarch                 20241117-2.el9                                       appstream                         6.1 M
 flac-libs                                              x86_64                 1.3.3-10.el9_2.1                                     appstream                         217 k
 gnutls-dane                                            x86_64                 3.8.3-6.el9                                          appstream                          18 k
 gnutls-utils                                           x86_64                 3.8.3-6.el9                                          appstream                         283 k
 gsm                                                    x86_64                 1.0.19-6.el9                                         appstream                          33 k
 gssproxy                                               x86_64                 0.8.4-7.el9                                          baseos                            108 k
 ipxe-roms-qemu                                         noarch                 20200823-9.git4bd064de.el9                           appstream                         673 k
 iscsi-initiator-utils                                  x86_64                 6.2.1.9-1.gita65a472.el9                             baseos                            383 k
 iscsi-initiator-utils-iscsiuio                         x86_64                 6.2.1.9-1.gita65a472.el9                             baseos                             80 k
 isns-utils-libs                                        x86_64                 0.101-4.el9                                          baseos                            100 k
 json-glib                                              x86_64                 1.6.6-1.el9                                          baseos                            151 k
 libX11                                                 x86_64                 1.7.0-11.el9                                         appstream                         645 k
 libX11-common                                          noarch                 1.7.0-11.el9                                         appstream                         151 k
 libX11-xcb                                             x86_64                 1.7.0-11.el9                                         appstream                          10 k
 libXau                                                 x86_64                 1.0.9-8.el9                                          appstream                          30 k
 libXext                                                x86_64                 1.3.4-8.el9                                          appstream                          39 k
 libXfixes                                              x86_64                 5.0.3-16.el9                                         appstream                          19 k
 libXxf86vm                                             x86_64                 1.1.4-18.el9                                         appstream                          18 k
 libasyncns                                             x86_64                 0.8-22.el9                                           appstream                          29 k
 libblkio                                               x86_64                 1.5.0-1.el9_4                                        appstream                         1.0 M
 libbsd                                                 x86_64                 0.12.2-1.el9                                         epel                              120 k
 libdrm                                                 x86_64                 2.4.123-2.el9                                        appstream                         158 k
 libepoxy                                               x86_64                 1.5.5-4.el9                                          appstream                         244 k
 libev                                                  x86_64                 4.33-6.el9                                           baseos                             51 k
 libfdt                                                 x86_64                 1.6.0-7.el9                                          appstream                          33 k
 libglvnd                                               x86_64                 1:1.3.4-1.el9                                        appstream                         133 k
 libglvnd-egl                                           x86_64                 1:1.3.4-1.el9                                        appstream                          36 k
 libglvnd-glx                                           x86_64                 1:1.3.4-1.el9                                        appstream                         140 k
 libibverbs                                             x86_64                 54.0-1.el9                                           baseos                            434 k
 libmd                                                  x86_64                 1.1.0-1.el9                                          epel                               46 k
 libnbd                                                 x86_64                 1.20.3-1.el9                                         appstream                         168 k
 libnfsidmap                                            x86_64                 1:2.5.4-34.el9                                       baseos                             60 k
 libogg                                                 x86_64                 2:1.3.4-6.el9                                        appstream                          32 k
 libpcap                                                x86_64                 14:1.10.0-4.el9                                      baseos                            172 k
 libpciaccess                                           x86_64                 0.16-7.el9                                           baseos                             26 k
 libpmem                                                x86_64                 1.12.1-1.el9                                         appstream                         111 k
 libpng                                                 x86_64                 2:1.6.37-12.el9                                      baseos                            116 k
 librados2                                              x86_64                 2:16.2.4-5.el9                                       appstream                         3.4 M
 librbd1                                                x86_64                 2:16.2.4-5.el9                                       appstream                         3.0 M
 librdmacm                                              x86_64                 54.0-1.el9                                           baseos                             70 k
 libretls                                               x86_64                 3.8.1-1.el9                                          epel                               41 k
 libslirp                                               x86_64                 4.4.0-8.el9                                          appstream                          67 k
 libsndfile                                             x86_64                 1.0.31-9.el9                                         appstream                         205 k
 libtirpc                                               x86_64                 1.3.3-9.el9                                          baseos                             93 k
 libtpms                                                x86_64                 0.9.1-5.20211126git1ff6fe1f43.el9_6                  appstream                         182 k
 liburing                                               x86_64                 2.5-1.el9                                            appstream                          38 k
 libusbx                                                x86_64                 1.0.26-1.el9                                         baseos                             75 k
 libverto-libev                                         x86_64                 0.3.2-3.el9                                          baseos                             13 k
 libvirt                                                x86_64                 10.10.0-7.6.el9_6                                    appstream                          29 k
 libvirt-client                                         x86_64                 10.10.0-7.6.el9_6                                    appstream                         449 k
 libvirt-client-qemu                                    x86_64                 10.10.0-7.6.el9_6                                    appstream                          49 k
 libvirt-daemon                                         x86_64                 10.10.0-7.6.el9_6                                    appstream                         215 k
 libvirt-daemon-common                                  x86_64                 10.10.0-7.6.el9_6                                    appstream                         137 k
 libvirt-daemon-config-network                          x86_64                 10.10.0-7.6.el9_6                                    appstream                          31 k
 libvirt-daemon-config-nwfilter                         x86_64                 10.10.0-7.6.el9_6                                    appstream                          37 k
 libvirt-daemon-driver-interface                        x86_64                 10.10.0-7.6.el9_6                                    appstream                         221 k
 libvirt-daemon-driver-network                          x86_64                 10.10.0-7.6.el9_6                                    appstream                         270 k
 libvirt-daemon-driver-nodedev                          x86_64                 10.10.0-7.6.el9_6                                    appstream                         245 k
 libvirt-daemon-driver-nwfilter                         x86_64                 10.10.0-7.6.el9_6                                    appstream                         257 k
 libvirt-daemon-driver-qemu                             x86_64                 10.10.0-7.6.el9_6                                    appstream                         991 k
 libvirt-daemon-driver-secret                           x86_64                 10.10.0-7.6.el9_6                                    appstream                         218 k
 libvirt-daemon-driver-storage                          x86_64                 10.10.0-7.6.el9_6                                    appstream                          28 k
 libvirt-daemon-driver-storage-core                     x86_64                 10.10.0-7.6.el9_6                                    appstream                         273 k
 libvirt-daemon-driver-storage-disk                     x86_64                 10.10.0-7.6.el9_6                                    appstream                          39 k
 libvirt-daemon-driver-storage-iscsi                    x86_64                 10.10.0-7.6.el9_6                                    appstream                          37 k
 libvirt-daemon-driver-storage-logical                  x86_64                 10.10.0-7.6.el9_6                                    appstream                          41 k
 libvirt-daemon-driver-storage-mpath                    x86_64                 10.10.0-7.6.el9_6                                    appstream                          34 k
 libvirt-daemon-driver-storage-rbd                      x86_64                 10.10.0-7.6.el9_6                                    appstream                          45 k
 libvirt-daemon-driver-storage-scsi                     x86_64                 10.10.0-7.6.el9_6                                    appstream                          36 k
 libvirt-daemon-lock                                    x86_64                 10.10.0-7.6.el9_6                                    appstream                          66 k
 libvirt-daemon-log                                     x86_64                 10.10.0-7.6.el9_6                                    appstream                          70 k
 libvirt-daemon-plugin-lockd                            x86_64                 10.10.0-7.6.el9_6                                    appstream                          40 k
 libvirt-daemon-proxy                                   x86_64                 10.10.0-7.6.el9_6                                    appstream                         214 k
 libvirt-libs                                           x86_64                 10.10.0-7.6.el9_6                                    appstream                         5.0 M
 libvorbis                                              x86_64                 1:1.3.7-5.el9                                        appstream                         192 k
 libwayland-client                                      x86_64                 1.21.0-1.el9                                         appstream                          33 k
 libwayland-server                                      x86_64                 1.21.0-1.el9                                         appstream                          41 k
 libxcb                                                 x86_64                 1.13.1-9.el9                                         appstream                         224 k
 libxkbcommon                                           x86_64                 1.0.3-4.el9                                          appstream                         132 k
 libxshmfence                                           x86_64                 1.3-10.el9                                           appstream                          12 k
 libxslt                                                x86_64                 1.1.34-13.el9_6                                      appstream                         239 k
 llvm-libs                                              x86_64                 19.1.7-1.el9                                         appstream                          57 M
 lzop                                                   x86_64                 1.04-8.el9                                           baseos                             55 k
 mdevctl                                                x86_64                 1.1.0-4.el9                                          appstream                         758 k
 mesa-dri-drivers                                       x86_64                 24.2.8-2.el9_6                                       appstream                         9.4 M
 mesa-filesystem                                        x86_64                 24.2.8-2.el9_6                                       appstream                          11 k
 mesa-libEGL                                            x86_64                 24.2.8-2.el9_6                                       appstream                         141 k
 mesa-libGL                                             x86_64                 24.2.8-2.el9_6                                       appstream                         169 k
 mesa-libgbm                                            x86_64                 24.2.8-2.el9_6                                       appstream                          36 k
 mesa-libglapi                                          x86_64                 24.2.8-2.el9_6                                       appstream                          44 k
 mysql-community-client-plugins                         x86_64                 8.0.43-1.el9                                         mysql80-community                 1.4 M
 mysql-community-common                                 x86_64                 8.0.43-1.el9                                         mysql80-community                 556 k
 mysql-community-libs                                   x86_64                 8.0.43-1.el9                                         mysql80-community                 1.5 M
 nbdkit-basic-filters                                   x86_64                 1.38.5-5.el9_6                                       appstream                         308 k
 nbdkit-basic-plugins                                   x86_64                 1.38.5-5.el9_6                                       appstream                         207 k
 nbdkit-selinux                                         noarch                 1.38.5-5.el9_6                                       appstream                          23 k
 nbdkit-server                                          x86_64                 1.38.5-5.el9_6                                       appstream                         128 k
 ndctl-libs                                             x86_64                 78-2.el9                                             baseos                             89 k
 nfs-utils                                              x86_64                 1:2.5.4-34.el9                                       baseos                            430 k
 numad                                                  x86_64                 0.5-37.20150602git.el9                               baseos                             36 k
 opennebula-common                                      noarch                 6.10.0.1-1.el9                                       opennebula                         23 k
 opennebula-common-onecfg                               noarch                 6.10.0.1-1.el9                                       opennebula                        9.1 k
 opennebula-rubygems                                    x86_64                 6.10.0.1-1.el9                                       opennebula                         16 M
 opus                                                   x86_64                 1.3.1-10.el9                                         appstream                         199 k
 passt-selinux                                          noarch                 0^20250217.ga1e48a0-10.el9_6                         appstream                          27 k
 pciutils                                               x86_64                 3.7.0-7.el9                                          baseos                             92 k
 pixman                                                 x86_64                 0.40.0-6.el9_3                                       appstream                         269 k
 policycoreutils-python-utils                           noarch                 3.6-2.1.el9                                          appstream                          71 k
 polkit                                                 x86_64                 0.117-13.el9                                         baseos                            146 k
 polkit-libs                                            x86_64                 0.117-13.el9                                         baseos                            8.3 M
 protobuf-c                                             x86_64                 1.3.3-13.el9                                         baseos                             34 k
 pulseaudio-libs                                        x86_64                 15.0-3.el9                                           appstream                         663 k
 python3-audit                                          x86_64                 3.1.5-4.el9                                          appstream                          83 k
 python3-cffi                                           x86_64                 1.14.5-5.el9                                         baseos                            241 k
 python3-cryptography                                   x86_64                 36.0.1-4.el9                                         baseos                            1.2 M
 python3-distro                                         noarch                 1.5.0-7.el9                                          appstream                          36 k
 python3-libsemanage                                    x86_64                 3.6-5.el9_6                                          appstream                          78 k
 python3-libvirt                                        x86_64                 10.10.0-1.el9                                        appstream                         333 k
 python3-lxml                                           x86_64                 4.6.5-3.el9                                          appstream                         1.2 M
 python3-ply                                            noarch                 3.11-14.el9.0.1                                      baseos                            103 k
 python3-policycoreutils                                noarch                 3.6-2.1.el9                                          appstream                         2.0 M
 python3-pycparser                                      noarch                 2.20-6.el9                                           baseos                            124 k
 python3-pyyaml                                         x86_64                 5.4.1-6.el9                                          baseos                            191 k
 python3-setools                                        x86_64                 4.4.4-1.el9                                          baseos                            551 k
 python3-setuptools                                     noarch                 53.0.0-13.el9_6.1                                    baseos                            837 k
 qemu-img                                               x86_64                 17:9.1.0-15.el9_6.7                                  appstream                         2.5 M
 qemu-kvm                                               x86_64                 17:9.1.0-15.el9_6.7                                  appstream                          64 k
 qemu-kvm-audio-pa                                      x86_64                 17:9.1.0-15.el9_6.7                                  appstream                          73 k
 qemu-kvm-block-blkio                                   x86_64                 17:9.1.0-15.el9_6.7                                  appstream                          76 k
 qemu-kvm-block-rbd                                     x86_64                 17:9.1.0-15.el9_6.7                                  appstream                          78 k
 qemu-kvm-common                                        x86_64                 17:9.1.0-15.el9_6.7                                  appstream                         668 k
 qemu-kvm-core                                          x86_64                 17:9.1.0-15.el9_6.7                                  appstream                         4.9 M
 qemu-kvm-device-display-virtio-gpu                     x86_64                 17:9.1.0-15.el9_6.7                                  appstream                          85 k
 qemu-kvm-device-display-virtio-gpu-pci                 x86_64                 17:9.1.0-15.el9_6.7                                  appstream                          68 k
 qemu-kvm-device-display-virtio-vga                     x86_64                 17:9.1.0-15.el9_6.7                                  appstream                          69 k
 qemu-kvm-device-usb-host                               x86_64                 17:9.1.0-15.el9_6.7                                  appstream                          82 k
 qemu-kvm-device-usb-redirect                           x86_64                 17:9.1.0-15.el9_6.7                                  appstream                          87 k
 qemu-kvm-docs                                          x86_64                 17:9.1.0-15.el9_6.7                                  appstream                         1.2 M
 qemu-kvm-tools                                         x86_64                 17:9.1.0-15.el9_6.7                                  appstream                         571 k
 qemu-kvm-ui-egl-headless                               x86_64                 17:9.1.0-15.el9_6.7                                  appstream                          69 k
 qemu-kvm-ui-opengl                                     x86_64                 17:9.1.0-15.el9_6.7                                  appstream                          76 k
 qemu-pr-helper                                         x86_64                 17:9.1.0-15.el9_6.7                                  appstream                         492 k
 quota                                                  x86_64                 1:4.09-4.el9                                         baseos                            188 k
 quota-nls                                              noarch                 1:4.09-4.el9                                         baseos                             76 k
 rpcbind                                                x86_64                 1.2.6-7.el9                                          baseos                             56 k
 rsync                                                  x86_64                 3.2.5-3.el9                                          baseos                            403 k
 ruby                                                   x86_64                 3.0.7-165.el9_5                                      appstream                          38 k
 ruby-libs                                              x86_64                 3.0.7-165.el9_5                                      appstream                         3.2 M
 rubygem-io-console                                     x86_64                 0.5.7-165.el9_5                                      appstream                          23 k
 rubygem-json                                           x86_64                 2.5.1-165.el9_5                                      appstream                          51 k
 rubygem-psych                                          x86_64                 3.3.2-165.el9_5                                      appstream                          48 k
 rubygem-rexml                                          noarch                 3.2.5-165.el9_5                                      appstream                          92 k
 rubygem-sqlite3                                        x86_64                 1.4.2-8.el9                                          epel                               44 k
 rubygems                                               noarch                 3.2.33-165.el9_5                                     appstream                         253 k
 scrub                                                  x86_64                 2.6.1-4.el9                                          appstream                          44 k
 seabios-bin                                            noarch                 1.16.3-4.el9                                         appstream                         100 k
 seavgabios-bin                                         noarch                 1.16.3-4.el9                                         appstream                          34 k
 sssd-nfs-idmap                                         x86_64                 2.9.6-4.el9_6.2                                      baseos                             39 k
 swtpm                                                  x86_64                 0.8.0-2.el9_4                                        appstream                          42 k
 swtpm-libs                                             x86_64                 0.8.0-2.el9_4                                        appstream                          48 k
 swtpm-tools                                            x86_64                 0.8.0-2.el9_4                                        appstream                         116 k
 systemd-container                                      x86_64                 252-51.el9_6.1                                       baseos                            577 k
 tar                                                    x86_64                 2:1.34-7.el9                                         baseos                            875 k
 unbound-libs                                           x86_64                 1.16.2-19.el9_6.1                                    appstream                         550 k
 usbredir                                               x86_64                 0.13.0-2.el9                                         appstream                          50 k
 virtiofsd                                              x86_64                 1.13.2-1.el9_6                                       appstream                         990 k
 xkeyboard-config                                       noarch                 2.33-2.el9                                           appstream                         779 k
 zstd                                                   x86_64                 1.5.5-1.el9                                          baseos                            461 k
Installing weak dependencies:
 nbdkit                                                 x86_64                 1.38.5-5.el9_6                                       appstream                         8.5 k
 nbdkit-curl-plugin                                     x86_64                 1.38.5-5.el9_6                                       appstream                          39 k
 nbdkit-ssh-plugin                                      x86_64                 1.38.5-5.el9_6                                       appstream                          28 k
 netcat                                                 x86_64                 1.229-1.el9                                          epel                               34 k
 passt                                                  x86_64                 0^20250217.ga1e48a0-10.el9_6                         appstream                         259 k
 polkit-pkla-compat                                     x86_64                 0.1-21.el9                                           baseos                             44 k
 ruby-default-gems                                      noarch                 3.0.7-165.el9_5                                      appstream                          30 k
 rubygem-bigdecimal                                     x86_64                 3.0.0-165.el9_5                                      appstream                          52 k
 rubygem-bundler                                        noarch                 2.2.33-165.el9_5                                     appstream                         370 k
 rubygem-rdoc                                           noarch                 6.3.4.1-165.el9_5                                    appstream                         398 k

Transaction Summary
============================================================================================================================================================================
Install  192 Packages

Total size: 158 M
Installed size: 784 M
Downloading Packages:
[SKIPPED] libbsd-0.12.2-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] libmd-1.1.0-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] libretls-3.8.1-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] netcat-1.229-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] rubygem-sqlite3-1.4.2-8.el9.x86_64.rpm: Already downloaded
[SKIPPED] mysql-community-client-plugins-8.0.43-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] mysql-community-common-8.0.43-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] mysql-community-libs-8.0.43-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] opennebula-common-6.10.0.1-1.el9.noarch.rpm: Already downloaded
[SKIPPED] opennebula-common-onecfg-6.10.0.1-1.el9.noarch.rpm: Already downloaded
[SKIPPED] opennebula-node-kvm-6.10.0.1-1.el9.noarch.rpm: Already downloaded
[SKIPPED] opennebula-rubygems-6.10.0.1-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] python3-pycparser-2.20-6.el9.noarch.rpm: Already downloaded
[SKIPPED] isns-utils-libs-0.101-4.el9.x86_64.rpm: Already downloaded
[SKIPPED] protobuf-c-1.3.3-13.el9.x86_64.rpm: Already downloaded
[SKIPPED] sssd-nfs-idmap-2.9.6-4.el9_6.2.x86_64.rpm: Already downloaded
[SKIPPED] numad-0.5-37.20150602git.el9.x86_64.rpm: Already downloaded
[SKIPPED] python3-pyyaml-5.4.1-6.el9.x86_64.rpm: Already downloaded
[SKIPPED] polkit-pkla-compat-0.1-21.el9.x86_64.rpm: Already downloaded
[SKIPPED] iscsi-initiator-utils-6.2.1.9-1.gita65a472.el9.x86_64.rpm: Already downloaded
[SKIPPED] libpng-1.6.37-12.el9.x86_64.rpm: Already downloaded
[SKIPPED] python3-cryptography-36.0.1-4.el9.x86_64.rpm: Already downloaded
[SKIPPED] lzop-1.04-8.el9.x86_64.rpm: Already downloaded
[SKIPPED] polkit-libs-0.117-13.el9.x86_64.rpm: Already downloaded
[SKIPPED] librdmacm-54.0-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] cyrus-sasl-gssapi-2.1.27-21.el9.x86_64.rpm: Already downloaded
[SKIPPED] libtirpc-1.3.3-9.el9.x86_64.rpm: Already downloaded
[SKIPPED] device-mapper-multipath-libs-0.8.7-35.el9_6.1.x86_64.rpm: Already downloaded
[SKIPPED] quota-4.09-4.el9.x86_64.rpm: Already downloaded
[SKIPPED] python3-ply-3.11-14.el9.0.1.noarch.rpm: Already downloaded
[SKIPPED] iscsi-initiator-utils-iscsiuio-6.2.1.9-1.gita65a472.el9.x86_64.rpm: Already downloaded
[SKIPPED] libpciaccess-0.16-7.el9.x86_64.rpm: Already downloaded
[SKIPPED] quota-nls-4.09-4.el9.noarch.rpm: Already downloaded
[SKIPPED] polkit-0.117-13.el9.x86_64.rpm: Already downloaded
[SKIPPED] gssproxy-0.8.4-7.el9.x86_64.rpm: Already downloaded
[SKIPPED] dmidecode-3.6-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] json-glib-1.6.6-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] ndctl-libs-78-2.el9.x86_64.rpm: Already downloaded
[SKIPPED] libibverbs-54.0-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] libev-4.33-6.el9.x86_64.rpm: Already downloaded
[SKIPPED] libverto-libev-0.3.2-3.el9.x86_64.rpm: Already downloaded
[SKIPPED] python3-cffi-1.14.5-5.el9.x86_64.rpm: Already downloaded
[SKIPPED] libpcap-1.10.0-4.el9.x86_64.rpm: Already downloaded
[SKIPPED] nfs-utils-2.5.4-34.el9.x86_64.rpm: Already downloaded
[SKIPPED] systemd-container-252-51.el9_6.1.x86_64.rpm: Already downloaded
[SKIPPED] tar-1.34-7.el9.x86_64.rpm: Already downloaded
[SKIPPED] rpcbind-1.2.6-7.el9.x86_64.rpm: Already downloaded
[SKIPPED] pciutils-3.7.0-7.el9.x86_64.rpm: Already downloaded
[SKIPPED] python3-setools-4.4.4-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] zstd-1.5.5-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] libnfsidmap-2.5.4-34.el9.x86_64.rpm: Already downloaded
[SKIPPED] daxctl-libs-78-2.el9.x86_64.rpm: Already downloaded
[SKIPPED] python3-setuptools-53.0.0-13.el9_6.1.noarch.rpm: Already downloaded
[SKIPPED] bzip2-1.0.8-10.el9_5.x86_64.rpm: Already downloaded
[SKIPPED] rsync-3.2.5-3.el9.x86_64.rpm: Already downloaded
[SKIPPED] libusbx-1.0.26-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] libslirp-4.4.0-8.el9.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-plugin-lockd-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] dnsmasq-2.85-16.el9_4.x86_64.rpm: Already downloaded
[SKIPPED] flac-libs-1.3.3-10.el9_2.1.x86_64.rpm: Already downloaded
[SKIPPED] rubygem-json-2.5.1-165.el9_5.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-proxy-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] libXxf86vm-1.1.4-18.el9.x86_64.rpm: Already downloaded
[SKIPPED] passt-selinux-0^20250217.ga1e48a0-10.el9_6.noarch.rpm: Already downloaded
[SKIPPED] libglvnd-1.3.4-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] virtiofsd-1.13.2-1.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] libwayland-client-1.21.0-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-lock-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-libs-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] rubygem-bundler-2.2.33-165.el9_5.noarch.rpm: Already downloaded
[SKIPPED] swtpm-0.8.0-2.el9_4.x86_64.rpm: Already downloaded
[SKIPPED] swtpm-tools-0.8.0-2.el9_4.x86_64.rpm: Already downloaded
[SKIPPED] nbdkit-selinux-1.38.5-5.el9_6.noarch.rpm: Already downloaded
[SKIPPED] libvirt-daemon-driver-nodedev-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] passt-0^20250217.ga1e48a0-10.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] libX11-common-1.7.0-11.el9.noarch.rpm: Already downloaded
[SKIPPED] qemu-kvm-block-rbd-9.1.0-15.el9_6.7.x86_64.rpm: Already downloaded
[SKIPPED] python3-policycoreutils-3.6-2.1.el9.noarch.rpm: Already downloaded
[SKIPPED] libvirt-daemon-log-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] libXau-1.0.9-8.el9.x86_64.rpm: Already downloaded
[SKIPPED] mesa-libGL-24.2.8-2.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] augeas-libs-1.14.1-2.el9.x86_64.rpm: Already downloaded
[SKIPPED] mesa-libglapi-24.2.8-2.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] libnbd-1.20.3-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] ruby-3.0.7-165.el9_5.x86_64.rpm: Already downloaded
[SKIPPED] boost-thread-1.75.0-10.el9.x86_64.rpm: Already downloaded
[SKIPPED] libtpms-0.9.1-5.20211126git1ff6fe1f43.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] seavgabios-bin-1.16.3-4.el9.noarch.rpm: Already downloaded
[SKIPPED] liburing-2.5-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] nbdkit-server-1.38.5-5.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] libXext-1.3.4-8.el9.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-config-network-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] qemu-kvm-docs-9.1.0-15.el9_6.7.x86_64.rpm: Already downloaded
[SKIPPED] scrub-2.6.1-4.el9.x86_64.rpm: Already downloaded
[SKIPPED] libxshmfence-1.3-10.el9.x86_64.rpm: Already downloaded
[SKIPPED] qemu-kvm-device-display-virtio-gpu-9.1.0-15.el9_6.7.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-driver-storage-mpath-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] rubygem-rdoc-6.3.4.1-165.el9_5.noarch.rpm: Already downloaded
[SKIPPED] libvirt-daemon-driver-storage-core-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] qemu-kvm-device-usb-redirect-9.1.0-15.el9_6.7.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-driver-storage-iscsi-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-client-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] ipxe-roms-qemu-20200823-9.git4bd064de.el9.noarch.rpm: Already downloaded
[SKIPPED] libX11-xcb-1.7.0-11.el9.x86_64.rpm: Already downloaded
[SKIPPED] mesa-libgbm-24.2.8-2.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] libglvnd-glx-1.3.4-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-driver-nwfilter-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] capstone-4.0.2-10.el9.x86_64.rpm: Already downloaded
[SKIPPED] libepoxy-1.5.5-4.el9.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-driver-storage-logical-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] xkeyboard-config-2.33-2.el9.noarch.rpm: Already downloaded
[SKIPPED] nbdkit-curl-plugin-1.38.5-5.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] libglvnd-egl-1.3.4-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] qemu-kvm-ui-egl-headless-9.1.0-15.el9_6.7.x86_64.rpm: Already downloaded
[SKIPPED] python3-libsemanage-3.6-5.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] llvm-libs-19.1.7-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] qemu-kvm-core-9.1.0-15.el9_6.7.x86_64.rpm: Already downloaded
[SKIPPED] libxcb-1.13.1-9.el9.x86_64.rpm: Already downloaded
[SKIPPED] rubygems-3.2.33-165.el9_5.noarch.rpm: Already downloaded
[SKIPPED] qemu-kvm-9.1.0-15.el9_6.7.x86_64.rpm: Already downloaded
[SKIPPED] qemu-pr-helper-9.1.0-15.el9_6.7.x86_64.rpm: Already downloaded
[SKIPPED] policycoreutils-python-utils-3.6-2.1.el9.noarch.rpm: Already downloaded
[SKIPPED] checkpolicy-3.6-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] libpmem-1.12.1-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] gnutls-dane-3.8.3-6.el9.x86_64.rpm: Already downloaded
[SKIPPED] pulseaudio-libs-15.0-3.el9.x86_64.rpm: Already downloaded
[SKIPPED] augeas-1.14.1-2.el9.x86_64.rpm: Already downloaded
[SKIPPED] swtpm-libs-0.8.0-2.el9_4.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-common-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] qemu-img-9.1.0-15.el9_6.7.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-driver-storage-disk-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] rubygem-bigdecimal-3.0.0-165.el9_5.x86_64.rpm: Already downloaded
[SKIPPED] unbound-libs-1.16.2-19.el9_6.1.x86_64.rpm: Already downloaded
[SKIPPED] nbdkit-ssh-plugin-1.38.5-5.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] libdrm-2.4.123-2.el9.x86_64.rpm: Already downloaded
[SKIPPED] qemu-kvm-device-display-virtio-vga-9.1.0-15.el9_6.7.x86_64.rpm: Already downloaded
[SKIPPED] python3-audit-3.1.5-4.el9.x86_64.rpm: Already downloaded
[SKIPPED] boost-iostreams-1.75.0-10.el9.x86_64.rpm: Already downloaded
[SKIPPED] gsm-1.0.19-6.el9.x86_64.rpm: Already downloaded
[SKIPPED] ruby-default-gems-3.0.7-165.el9_5.noarch.rpm: Already downloaded
[SKIPPED] rubygem-io-console-0.5.7-165.el9_5.x86_64.rpm: Already downloaded
[SKIPPED] opus-1.3.1-10.el9.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-driver-interface-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] usbredir-0.13.0-2.el9.x86_64.rpm: Already downloaded
[SKIPPED] rubygem-rexml-3.2.5-165.el9_5.noarch.rpm: Already downloaded
[SKIPPED] libogg-1.3.4-6.el9.x86_64.rpm: Already downloaded
[SKIPPED] boost-system-1.75.0-10.el9.x86_64.rpm: Already downloaded
[SKIPPED] rubygem-psych-3.3.2-165.el9_5.x86_64.rpm: Already downloaded
[SKIPPED] libXfixes-5.0.3-16.el9.x86_64.rpm: Already downloaded
[SKIPPED] qemu-kvm-device-usb-host-9.1.0-15.el9_6.7.x86_64.rpm: Already downloaded
[SKIPPED] qemu-kvm-device-display-virtio-gpu-pci-9.1.0-15.el9_6.7.x86_64.rpm: Already downloaded
[SKIPPED] libasyncns-0.8-22.el9.x86_64.rpm: Already downloaded
[SKIPPED] libvorbis-1.3.7-5.el9.x86_64.rpm: Already downloaded
[SKIPPED] seabios-bin-1.16.3-4.el9.noarch.rpm: Already downloaded
[SKIPPED] nbdkit-basic-plugins-1.38.5-5.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] gnutls-utils-3.8.3-6.el9.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-config-nwfilter-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] ruby-libs-3.0.7-165.el9_5.x86_64.rpm: Already downloaded
[SKIPPED] python3-distro-1.5.0-7.el9.noarch.rpm: Already downloaded
[SKIPPED] qemu-kvm-block-blkio-9.1.0-15.el9_6.7.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-driver-secret-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] libblkio-1.5.0-1.el9_4.x86_64.rpm: Already downloaded
[SKIPPED] mdevctl-1.1.0-4.el9.x86_64.rpm: Already downloaded
[SKIPPED] libsndfile-1.0.31-9.el9.x86_64.rpm: Already downloaded
[SKIPPED] python3-libvirt-10.10.0-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] mesa-libEGL-24.2.8-2.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-driver-qemu-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] mesa-filesystem-24.2.8-2.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-driver-storage-scsi-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] qemu-kvm-tools-9.1.0-15.el9_6.7.x86_64.rpm: Already downloaded
[SKIPPED] edk2-ovmf-20241117-2.el9.noarch.rpm: Already downloaded
[SKIPPED] libwayland-server-1.21.0-1.el9.x86_64.rpm: Already downloaded
[SKIPPED] nbdkit-1.38.5-5.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] librados2-16.2.4-5.el9.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-driver-storage-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] libxkbcommon-1.0.3-4.el9.x86_64.rpm: Already downloaded
[SKIPPED] qemu-kvm-audio-pa-9.1.0-15.el9_6.7.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-driver-storage-rbd-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] librbd1-16.2.4-5.el9.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-daemon-driver-network-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] qemu-kvm-ui-opengl-9.1.0-15.el9_6.7.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-client-qemu-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] libfdt-1.6.0-7.el9.x86_64.rpm: Already downloaded
[SKIPPED] libvirt-10.10.0-7.6.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] mesa-dri-drivers-24.2.8-2.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] nbdkit-basic-filters-1.38.5-5.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] pixman-0.40.0-6.el9_3.x86_64.rpm: Already downloaded
[SKIPPED] python3-lxml-4.6.5-3.el9.x86_64.rpm: Already downloaded
[SKIPPED] libxslt-1.1.34-13.el9_6.x86_64.rpm: Already downloaded
[SKIPPED] qemu-kvm-common-9.1.0-15.el9_6.7.x86_64.rpm: Already downloaded
[SKIPPED] libX11-1.7.0-11.el9.x86_64.rpm: Already downloaded
MySQL 8.0 Community Server                                                                                                                  3.0 MB/s | 3.1 kB     00:00
GPG key at file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql-2022 (0x3A79BD29) is already installed
The GPG keys listed for the "MySQL 8.0 Community Server" repository are already installed but they are not correct for this package.
Check that the correct key URLs are configured for this repository.. Failing package is: mysql-community-client-plugins-8.0.43-1.el9.x86_64
 GPG Keys are configured as: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql-2022
Public key for mysql-community-common-8.0.43-1.el9.x86_64.rpm is not installed. Failing package is: mysql-community-common-8.0.43-1.el9.x86_64
 GPG Keys are configured as: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql-2022
Public key for mysql-community-libs-8.0.43-1.el9.x86_64.rpm is not installed. Failing package is: mysql-community-libs-8.0.43-1.el9.x86_64
 GPG Keys are configured as: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql-2022
The downloaded packages were saved in cache until the next successful transaction.
You can remove cached packages by executing 'dnf clean packages'.

````

🌞 Dépendances additionnelles

```
[user1@kvm1 ~]$ sudo dnf install -y genisoimage
Last metadata expiration check: 0:07:37 ago on Wed Sep 17 00:53:00 2025.
Dependencies resolved.
============================================================================================================================================================================
 Package                                    Architecture                          Version                                         Repository                           Size
============================================================================================================================================================================
Installing:
 genisoimage                                x86_64                                1.1.11-48.el9                                   epel                                324 k
Installing dependencies:
 libusal                                    x86_64                                1.1.11-48.el9                                   epel                                137 k

Transaction Summary
============================================================================================================================================================================
Install  2 Packages

Total download size: 461 k
Installed size: 1.6 M
Downloading Packages:
(1/2): libusal-1.1.11-48.el9.x86_64.rpm                                                                                                     466 kB/s | 137 kB     00:00
(2/2): genisoimage-1.1.11-48.el9.x86_64.rpm                                                                                                 809 kB/s | 324 kB     00:00
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                       426 kB/s | 461 kB     00:01
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                    1/1
  Installing       : libusal-1.1.11-48.el9.x86_64                                                                                                                       1/2
  Installing       : genisoimage-1.1.11-48.el9.x86_64                                                                                                                   2/2
  Running scriptlet: genisoimage-1.1.11-48.el9.x86_64                                                                                                                   2/2
  Verifying        : genisoimage-1.1.11-48.el9.x86_64                                                                                                                   1/2
  Verifying        : libusal-1.1.11-48.el9.x86_64                                                                                                                       2/2

Installed:
  genisoimage-1.1.11-48.el9.x86_64                                                       libusal-1.1.11-48.el9.x86_64

Complete!

```
🌞 Démarrer le service libvirtd

```
[user1@kvm1 ~]$ sudo dnf install -y libvirt libvirt-daemon-kvm qemu-kvm virt-install bridge-utils
Last metadata expiration check: 0:10:48 ago on Wed Sep 17 00:53:00 2025.
Dependencies resolved.
============================================================================================================================================================================
 Package                                                  Architecture             Version                                                Repository                   Size
============================================================================================================================================================================
Installing:
 bridge-utils                                             x86_64                   1.7.1-3.el9                                            epel                         34 k
 libvirt                                                  x86_64                   10.10.0-7.6.el9_6                                      appstream                    29 k
 libvirt-daemon-kvm                                       x86_64                   10.10.0-7.6.el9_6                                      appstream                    29 k
 qemu-kvm                                                 x86_64                   17:9.1.0-15.el9_6.7                                    appstream                    64 k
 virt-install                                             noarch                   5.0.0-1.el9                                            appstream                    41 k
Installing dependencies:
 adobe-source-code-pro-fonts                              noarch                   2.030.1.050-12.el9.1                                   baseos                      831 k
 boost-iostreams                                          x86_64                   1.75.0-10.el9                                          appstream                    36 k
 boost-system                                             x86_64                   1.75.0-10.el9                                          appstream                    11 k
 boost-thread
 .
 .
 .
 . Verifying        : python3-lxml-4.6.5-3.el9.x86_64                                                                                                                195/198
  Verifying        : libxslt-1.1.34-13.el9_6.x86_64                                                                                                                 196/198
  Verifying        : qemu-kvm-common-17:9.1.0-15.el9_6.7.x86_64                                                                                                     197/198
  Verifying        : libX11-1.7.0-11.el9.x86_64                                                                                                                     198/198

Installed:
  abattis-cantarell-fonts-0.301-4.el9.noarch                                         adobe-source-code-pro-fonts-2.030.1.050-12.el9.1.noarch
  .
  .
  .
   webkit2gtk3-jsc-2.48.5-1.el9_6.x86_64                                              xkeyboard-config-2.33-2.el9.noarch
  xorriso-1.5.4-5.el9_5.x86_64                                                       zstd-1.5.5-1.el9.x86_64

Complete!
```

```
ket
[user1@kvm1 ~]$ sudo systemctl start libvirtd.socket
[user1@kvm1 ~]$ sudo systemctl status virtqemud
bvirtd.socket
○ virtqemud.service - libvirt QEMU daemon
     Loaded: loaded (/usr/lib/systemd/system/virtqemud.service; enabled; preset: enabled)
     Active: inactive (dead) since Wed 2025-09-17 01:08:34 CEST; 16s ago
   Duration: 135ms
TriggeredBy: ○ virtqemud-ro.socket
             ○ virtqemud-admin.socket
             ○ virtqemud.socket
       Docs: man:virtqemud(8)
             https://libvirt.org/
    Process: 6085 ExecStart=/usr/sbin/virtqemud $VIRTQEMUD_ARGS (code=exited, status=0/SUCCESS)
   Main PID: 6085 (code=exited, status=0/SUCCESS)
        CPU: 73ms

Sep 17 01:08:34 kvm1 systemd[1]: Starting libvirt QEMU daemon...
Sep 17 01:08:34 kvm1 systemd[1]: Started libvirt QEMU daemon.
Sep 17 01:08:34 kvm1 virtqemud[6085]: libvirt version: 10.10.0, package: 7.6.el9_6 (Rocky Linux Build System (Peridot) <releng@rockylinux.org>, 2025-08-05-16:48:51, )
Sep 17 01:08:34 kvm1 virtqemud[6085]: hostname: kvm1
Sep 17 01:08:34 kvm1 virtqemud[6085]: Unable to open /dev/kvm: No such file or directory
Sep 17 01:08:34 kvm1 systemd[1]: Stopping libvirt QEMU daemon...
Sep 17 01:08:34 kvm1 systemd[1]: virtqemud.service: Deactivated successfully.
Sep 17 01:08:34 kvm1 systemd[1]: Stopped libvirt QEMU daemon.
[user1@kvm1 ~]$ sudo systemctl status libvirtd.socket
● libvirtd.socket - libvirt legacy monolithic daemon socket
     Loaded: loaded (/usr/lib/systemd/system/libvirtd.socket; disabled; preset: disabled)
     Active: active (listening) since Wed 2025-09-17 01:08:34 CEST; 16s ago
      Until: Wed 2025-09-17 01:08:34 CEST; 16s ago
   Triggers: ● libvirtd.service
     Listen: /run/libvirt/libvirt-sock (Stream)
     CGroup: /system.slice/libvirtd.socket

Sep 17 01:08:34 kvm1 systemd[1]: Listening on libvirt legacy monolithic daemon socket.
```

### Activer au démarrage :

```
[user1@kvm1 ~]$ sudo systemctl enable virtqemud
bvirtd.socket
[user1@kvm1 ~]$ sudo systemctl enable libvirtd.socket
Created symlink /etc/systemd/system/sockets.target.wants/libvirtd.socket → /usr/lib/systemd/system/libvirtd.socket.
Created symlink /etc/systemd/system/sockets.target.wants/libvirtd-ro.socket → /usr/lib/systemd/system/libvirtd-ro.socket.
Created symlink /etc/systemd/system/sockets.target.wants/libvirtd-admin.socket → /usr/lib/systemd/system/libvirtd-admin.socket.
```
# B. Système

### 🌞 1️⃣ Ouvrir les ports SSH (port 22 TCP) VXLAN (port 8472 UDP)

```
[user1@kvm1 ~]$ sudo firewall-cmd --permanent --add-port=22/tcp
success
[user1@kvm1 ~]$ sudo firewall-cmd --permanent --add-port=8472/udp
success

[user1@kvm1 ~]$ sudo firewall-cmd --reload
success


[user1@kvm1 ~]$ sudo firewall-cmd --list-ports
22/tcp 8472/udp
```

🌞 Handle SSH
uniquement pour ce point, repassez en SSH sur frontend.one
OpenNebula reposant sur des connexions SSH, elles doivent toutes se passer sans interaction humaine (pas de demande d'acceptation d'empreintes, ni de passwords par exemple)
        donc, en étant connecté en tant que oneadmin sur frontend.one
        les commandes doivent fonctionner sans aucun prompt (ni password, ni empreinte) :

```
sudo chmod 700[user1@frontend ~]$ sudo chown oneadmin:oneadmin /home/oneadmin
 /home/oneadmin
[user1@frontend ~]$ sudo chmod 700 /home/oneadmin
[user1@frontend ~]$ sudo -u oneadmin mkdir -p /home/oneadmin/.ssh
eadmin chmod 700 /home/oneadmin/.ssh
[user1@frontend ~]$ sudo -u oneadmin chmod 700 /home/oneadmin/.ssh
[user1@frontend ~]$ sudo -u oneadmin ssh-keygen -t ed25519 -f /home/oneadmin/.ssh/id_ed25519 -N ""
Generating public/private ed25519 key pair.
Your identification has been saved in /home/oneadmin/.ssh/id_ed25519
Your public key has been saved in /home/oneadmin/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:fPJ3X+pEn8I46kwoRjffsSat7X5NA5OVXzwiliYn+RA oneadmin@frontend
The key's randomart image is:
+--[ED25519 256]--+
|         Eo .  ..|
|         = * . +o|
|          O . + +|
|       .   . +  .|
|     . oS ..  +  |
|    . . ++o =. +.|
|     o . +.B.o=.+|
|    . . o *..+.+.|
|        .=o+..o .|
+----[SHA256]-----+

```

```
[user1@frontend ~]$ sudo -u oneadmin cat /home/oneadmin/.ssh/id_ed25519.pub
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIGq/mTjvtLQK8RP9gMM6NdUNWDlpxIVig6KT6ZbfDODl oneadmin@frontend

```




SHA256:fPJ3X+pEn8I46kwoRjffsSat7X5NA5OVXzwiliYn+RA oneadmin@frontend

```

PS C:\Users\Fadhil> ssh user1@10.3.1.10
user1@10.3.1.10's password:
Last login: Wed Sep 17 01:57:51 2025 from 10.3.1.1
[user1@frontend ~]$ sudo su - oneadmin
[sudo] password for user1:
Last login: Wed Sep 17 02:44:16 CEST 2025 from 10.3.1.10 on pts/1
[oneadmin@frontend ~]$ ssh  oneadmin@frontend.one
Last login: Sun Sep 21 20:03:09 2025
[oneadmin@frontend ~]$
```

```
[user1@frontend ~]$ sudo -u oneadmin ssh-copy-id -i /home/oneadmin/.ssh/id_ed25519 oneadmin@kvm1.one
```




# II.3. Setup réseau
## A. Intro

## B. Création du Virtual Network
### Étape A : Création du Virtual Network (WebUI)

### 🌞 Étape B : Préparer le bridge réseau
```
[user1@kvm1 ~]$ sudo ip link add name vxlan_bridge type bridge
[sudo] password for user1:
[user1@kvm1 ~]$ ip link show vxlan_bridge
4: vxlan_bridge: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN mode DEFAULT group default qlen 1000
    link/ether 8e:16:6b:b7:c3:20 brd ff:ff:ff:ff:ff:ff
```

```
[user1@kvm1 ~]$ sudo ip addr add 10.220.220.201/24 dev vxlan_bridge
[user1@kvm1 ~]$ ip addr show vxlan_bridge
4: vxlan_bridge: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UNKNOWN group default qlen 1000
    link/ether 8e:16:6b:b7:c3:20 brd ff:ff:ff:ff:ff:ff
    inet 10.220.220.201/24 scope global vxlan_bridge
       valid_lft forever preferred_lft forever
    inet6 fe80::8c16:6bff:feb7:c320/64 scope link
       valid_lft forever preferred_lft forever
[user1@kvm1 ~]$ sudo firewall-cmd --add-interface=vxlan_bridge --zone=public --permanent
success
[user1@kvm1 ~]$ sudo firewall-cmd --add-masquerade --permanent
success
[user1@kvm1 ~]$ sudo firewall-cmd --reload
success
[user1@kvm1 ~]$
```


# C. Préparer le bridge réseau¶

### ➜ Ces étapes sont à effectuer uniquement sur kvm1.one dans un premier temps
dans la partie IV du TP, quand vous mettrez en place kvm2.one, il faudra aussi refaire ça dessus

🌞 Créer et configurer le bridge Linux

```
[user1@kvm1 ~]$ sudo vim /opt/vxlan.sh
[user1@kvm1 ~]$ sudo chmod +x /opt/vxlan.sh
```

### je Créer le service systemd

```
[user1@kvm1 ~]$ sudo vim /etc/systemd/system/vxlan.service
[user1@kvm1 ~]$ sudo systemctl daemon-reload
[user1@kvm1 ~]$ sudo systemctl start vxlan
[user1@kvm1 ~]$ ip addr show vxlan_bridge
4: vxlan_bridge: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UNKNOWN group default qlen 1000
    link/ether 8e:16:6b:b7:c3:20 brd ff:ff:ff:ff:ff:ff
    inet 10.220.220.201/24 scope global vxlan_bridge
       valid_lft forever preferred_lft forever
    inet6 fe80::8c16:6bff:feb7:c320/64 scope link
       valid_lft forever preferred_lft forever
```

### j'active au boot

```
[user1@kvm1 ~]$ sudo systemctl enable vxlan
Created symlink /etc/systemd/system/multi-user.target.wants/vxlan.service → /etc/systemd/system/vxlan.service.
```


# III. Utiliser la plateforme


### ➜ Tester la connectivité à la VM
déjà est-ce qu'on peut la ping ?
depuis le noeud kvm1.one, faites un ping vers l'IP de la VM
l'IP de la VM est visible dans la WebUI

```
ping -c 3 10.220.220.100
PING 10.220.220.100 (10.220.220.100) 56(84) bytes of data.
64 bytes from 10.220.220.100: icmp_seq=1 ttl=64 time=0.879 ms
64 bytes from 10.220.220.100: icmp_seq=2 ttl=64 time=0.842 ms
64 bytes from 10.220.220.100: icmp_seq=3 ttl=64 time=0.801 ms

--- 10.220.220.100 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
```
```
sudo su - oneadmin
eval $(ssh-agent)
ssh-add ~/.ssh/id_ed25519
Identity added: /var/lib/one/.ssh/id_ed25519 (oneadmin@frontend)
ssh -J kvm1.one root@10.220.220.100
[root@localhost ~]# 
ip route add default via 10.220.220.201
ip route show
default via 10.220.220.201 dev eth0
10.220.220.0/24 dev eth0 proto kernel scope link src 10.220.220.100
ping -c 3 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=57 time=20.1 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=57 time=19.8 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=57 time=21.0 ms


```


# IV. Ajout d'un noeud et VXLAN