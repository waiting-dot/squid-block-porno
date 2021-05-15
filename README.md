# Блокировка порно с помощью прокси squid (для порноманов)
Прокси блокирует ВСЕ картинки и видео, кроме разрешенных сайтов в конфигурации squid.
Траффик пропускается принудительно через прокси с помощью правил iptables.

Во время ломок появляется сильное желание отключить iptables или сбросить настройки squid.
Поэтому пришлось поставить неизвестный себе пароль на root.

Чтобы нельзя было записать live cd и загрузиться с него, чтобы сбросить пароль root, пришлось
закрыть доступ к флешкам и к смарт телефону андроид.

Также чтобы нельзя было сбросить пароль на root через загрузчик grub2
пришлось заблокировать его от изменений.

Само собой нужно выкинуть все live cd диски и стереть с флешек 

1. Инструкцию по установке и настройке squid можно посмотреть тут https://losst.ru/prozrachnyj-proksi-dlya-https-v-squid

Конфигурация squid и правила iptables будут другие, чем в статье, так как у нас будет не прозрачный
прокси (для блокирования браузерных плагинов vpn и proxy)

Чтобы не компилировать squid, можно скачать готовый здесь https://github.com/diladele/squid-ubuntu

Конфигурационные файлы squid
Файл /etc/squid/squid.conf
```
#можно разкомментировать две нижние строки для отключения интернета в заданное время ночью
#acl night_time time 01:00-08:00
#http_access deny all night_time

acl whitelist dstdomain "/etc/squid/policy/whitelist.txt"
http_access allow whitelist
http_reply_access allow whitelist

acl blacklist dstdomain "/etc/squid/policy/blacklist.txt"
http_access deny blacklist
http_reply_access deny blacklist

acl blackmimetypesp rep_mime_type -i ^video/x-f4f$
acl blackmimetypesp rep_mime_type -i ^video/x-flv$
acl blackmimetypesp rep_mime_type -i ^video/mp2t$
acl blackmimetypesp rep_mime_type -i ^audio/mp4$
acl blackmimetypesp rep_mime_type -i ^video/mp4$
acl blackmimetypesp rep_mime_type -i ^video/mpeg$
acl blackmimetypesp rep_mime_type -i ^video/quicktime$
acl blackmimetypesp rep_mime_type -i ^video/x-msvideo$
acl blackmimetypesp rep_mime_type -i ^video/x-sgi-movie$
acl blackmimetypesp rep_mime_type -i ^video/vnd.mpegurl$
acl blackmimetypesp rep_mime_type -i ^video/ogg$
acl blackmimetypesp rep_mime_type -i ^video/webm$
acl blackmimetypesp rep_mime_type -i ^video/web2$
acl blackmimetypesp rep_mime_type -i ^video/x-ms-wmv$
acl blackmimetypesp rep_mime_type -i ^video/3gpp$
acl blackmimetypesp rep_mime_type -i ^video/3gpp2$
acl blackmimetypesp rep_mime_type -i ^video/avi$
acl blackmimetypesp rep_mime_type -i ^video/msvideo$
acl blackmimetypesp rep_mime_type -i ^video/x-dv$
acl blackmimetypesp rep_mime_type -i ^video/dl$
acl blackmimetypesp rep_mime_type -i ^video/x-dl$
acl blackmimetypesp rep_mime_type -i ^video/vnd.rn-realvideo$
acl blackmimetypesp rep_mime_type -i ^video/x-ms-asf$
acl blackmimetypesp rep_mime_type -i ^video/mp2t$
acl blackmimetypesp rep_mime_type -i ^application/vnd.ms.wms-hdr.asfv1$
acl blackmimetypesp rep_mime_type -i ^application/x-mms-framed$
acl blackmimetypesp rep_mime_type -i ^audio/x-pn-realaudio$
acl blackmimetypesp rep_mime_type -i ^application/x-shockwave-flash$
acl blackmimetypesp rep_mime_type -i ^application/x-mpegURL$
acl blackmimetypesp rep_mime_type -i ^application/mp4$
acl blackmimetypesp rep_mime_type -i ^image/gif$
acl blackmimetypesp rep_mime_type -i ^image/ief$
acl blackmimetypesp rep_mime_type -i ^image/jpeg$
acl blackmimetypesp rep_mime_type -i ^image/bmp$
acl blackmimetypesp rep_mime_type -i ^image/tiff$
acl blackmimetypesp rep_mime_type -i ^image/x-cmu-raster$
acl blackmimetypesp rep_mime_type -i ^image/x-portable-anymap$
acl blackmimetypesp rep_mime_type -i ^image/x-portable-bitmap$
acl blackmimetypesp rep_mime_type -i ^image/x-portable-graymap$
acl blackmimetypesp rep_mime_type -i ^image/x-portable-pixmap$
acl blackmimetypesp rep_mime_type -i ^image/x-rgb$
acl blackmimetypesp rep_mime_type -i ^image/x-xbitmap$
acl blackmimetypesp rep_mime_type -i ^image/x-xpixmap$
acl blackmimetypesp rep_mime_type -i ^image/x-xwindowdump$
acl blackmimetypesp rep_mime_type -i ^image/png$
acl blackmimetypesp rep_mime_type -i ^image/vnd.djvu$
acl blackmimetypesp rep_mime_type -i ^image/vnd.wap.wbmp$
acl blackmimetypesp rep_mime_type -i ^image/webp$
acl blackmimetypesp rep_mime_type -i ^image/svg+xml$
http_reply_access deny blackmimetypesp

acl blackmimetypesq req_mime_type -i ^video/x-f4f$
acl blackmimetypesq req_mime_type -i ^video/x-flv$
acl blackmimetypesq req_mime_type -i ^video/mp2t$
acl blackmimetypesq req_mime_type -i ^audio/mp4$
acl blackmimetypesq req_mime_type -i ^video/mp4$
acl blackmimetypesq req_mime_type -i ^video/mpeg$
acl blackmimetypesq req_mime_type -i ^video/quicktime$
acl blackmimetypesq req_mime_type -i ^video/x-msvideo$
acl blackmimetypesq req_mime_type -i ^video/x-sgi-movie$
acl blackmimetypesq req_mime_type -i ^video/vnd.mpegurl$
acl blackmimetypesq req_mime_type -i ^video/ogg$
acl blackmimetypesq req_mime_type -i ^video/webm$
acl blackmimetypesq req_mime_type -i ^video/web2$
acl blackmimetypesq req_mime_type -i ^video/x-ms-wmv$
acl blackmimetypesq req_mime_type -i ^video/3gpp$
acl blackmimetypesq req_mime_type -i ^video/3gpp2$
acl blackmimetypesq req_mime_type -i ^video/avi$
acl blackmimetypesq req_mime_type -i ^video/msvideo$
acl blackmimetypesq req_mime_type -i ^video/x-dv$
acl blackmimetypesq req_mime_type -i ^video/dl$
acl blackmimetypesq req_mime_type -i ^video/x-dl$
acl blackmimetypesq req_mime_type -i ^video/vnd.rn-realvideo$
acl blackmimetypesq req_mime_type -i ^video/x-ms-asf$
acl blackmimetypesq req_mime_type -i ^video/mp2t$
acl blackmimetypesq req_mime_type -i ^application/vnd.ms.wms-hdr.asfv1$
acl blackmimetypesq req_mime_type -i ^application/x-mms-framed$
acl blackmimetypesq req_mime_type -i ^audio/x-pn-realaudio$
acl blackmimetypesq req_mime_type -i ^application/x-shockwave-flash$
acl blackmimetypesq req_mime_type -i ^application/x-mpegURL$
acl blackmimetypesq req_mime_type -i ^application/mp4$
acl blackmimetypesq req_mime_type -i ^image/gif$
acl blackmimetypesq req_mime_type -i ^image/ief$
acl blackmimetypesq req_mime_type -i ^image/jpeg$
acl blackmimetypesq req_mime_type -i ^image/bmp$
acl blackmimetypesq req_mime_type -i ^image/tiff$
acl blackmimetypesq req_mime_type -i ^image/x-cmu-raster$
acl blackmimetypesq req_mime_type -i ^image/x-portable-anymap$
acl blackmimetypesq req_mime_type -i ^image/x-portable-bitmap$
acl blackmimetypesq req_mime_type -i ^image/x-portable-graymap$
acl blackmimetypesq req_mime_type -i ^image/x-portable-pixmap$
acl blackmimetypesq req_mime_type -i ^image/x-rgb$
acl blackmimetypesq req_mime_type -i ^image/x-xbitmap$
acl blackmimetypesq req_mime_type -i ^image/x-xpixmap$
acl blackmimetypesq req_mime_type -i ^image/x-xwindowdump$
acl blackmimetypesq req_mime_type -i ^image/png$
acl blackmimetypesq req_mime_type -i ^image/vnd.djvu$
acl blackmimetypesq req_mime_type -i ^image/vnd.wap.wbmp$
acl blackmimetypesq req_mime_type -i ^image/webp$
acl blackmimetypesq req_mime_type -i ^image/svg+xml$
http_reply_access deny blackmimetypesq

acl blackrepheaders rep_header Content-Disposition -i ^(.)*filename=(\"|)(.)*\.mp4(\"|)$
acl blackrepheaders rep_header Content-Disposition -i ^attachment; filename*=(\"|)(.)*\.mp4$
http_reply_access deny blackrepheaders

acl blackextensions urlpath_regex -i \.avi(\?.*)?$
acl blackextensions urlpath_regex -i \.mpg(\?.*)?$
acl blackextensions urlpath_regex -i \.mp4(\?.*)?$
acl blackextensions urlpath_regex -i \.mpeg(\?.*)?$
acl blackextensions urlpath_regex -i \.mkv(\?.*)?$
acl blackextensions urlpath_regex -i \.ogg(\?.*)?$
acl blackextensions urlpath_regex -i \.quicktime(\?.*)?$
acl blackextensions urlpath_regex -i \.webm(\?.*)?$
acl blackextensions urlpath_regex -i \.web2(\?.*)?$
acl blackextensions urlpath_regex -i \.wmv(\?.*)?$
acl blackextensions urlpath_regex -i \.flv(\?.*)?$
acl blackextensions urlpath_regex -i \.3gp(\?.*)?$
acl blackextensions urlpath_regex -i \.3g2(\?.*)?$
acl blackextensions urlpath_regex -i \.3gpp(\?.*)?$
acl blackextensions urlpath_regex -i \.3gpp2(\?.*)?$
acl blackextensions urlpath_regex -i \.m3u(\?.*)?$
acl blackextensions urlpath_regex -i \.m3u8(\?.*)?$
acl blackextensions urlpath_regex -i \.ovpn(\?.*)?$
acl blackextensions urlpath_regex -i \.xspf(\?.*)?$
http_access deny blackextensions
http_reply_access deny blackextensions

acl SSL_ports port 443    # HTTPS (C)
acl Safe_ports port 80    # HTTP
acl CONNECT method CONNECT
http_access deny !Safe_ports !SSL_ports

# DNS Options
dns_v4_first on
dns_nameservers 8.8.8.8

http_access allow all
http_port 3128 ssl-bump generate-host-certificates=on dynamic_cert_mem_cache_size=4MB cert=/etc/squid/ssl/squid.pem key=/etc/squid/ssl/squid.key

acl step1 at_step SslBump1
acl step2 at_step SslBump2
acl step3 at_step SslBump3
acl nobumpSites ssl::server_name "/etc/squid/policy/whitelist.txt"
ssl_bump peek step1 all
ssl_bump peek step2 nobumpSites
ssl_bump splice step3 nobumpSites
ssl_bump server-first all
ssl_bump bump all
acl domainMismatchList dstdom_regex -i "/etc/squid/policy/domain_mismatch.txt"
acl certMismatch all-of domainMismatchList ssl::certDomainMismatch
sslproxy_cert_error allow certMismatch
sslproxy_cert_error deny all

sslcrtd_program /usr/lib/squid/security_file_certgen -s /var/lib/ssl_db -M 10MB

icon_directory /usr/local/squid/share/icons
access_log none
cache deny all
```
Файл /etc/squid/policy/whitelist.txt, содержащий список сайтов исключений. Это пример, можно добавить свои
```
.2gis.com
.2gis.ru
.4pda.ru
.accounts.google.com
.askubuntu.com
.asset-packagist.org
.cyberforum.ru
.disk.yandex.ru
.dl.google.com
.docs.google.com
.drive.google.com
.github.com
.github.io
.gitlab-static.net
.gitlab.com
.gitlab.com
.gitlab.net
.google.com/recaptcha
.google.com:443/recaptcha
.googleapis.com
.packagist.org
antio.ru
.sourceforge.net
```
Файл /etc/squid/policy/blacklist.txt заполняем сайтами, к которым запрещаем доступ
(можно оставить пустым)
Файл /etc/squid/policy/domain_mismatch.txt тоже можно оставить пустым

2. Правила для iptables сохраняем в файл /etc/squid/policy/iptables
```
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
iptables -F
iptables -X

iptables -P INPUT ACCEPT
iptables -P FORWARD DROP
iptables -P OUTPUT DROP

iptables -A OUTPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT
iptables -A OUTPUT -m conntrack --ctstate INVALID -j DROP
iptables -A OUTPUT -p icmp --icmp-type 8 -m conntrack --ctstate NEW -j ACCEPT
iptables -A OUTPUT -p tcp -m owner --uid-owner proxy -j ACCEPT
iptables -A OUTPUT -p udp -m owner --uid-owner proxy --dport 53 -j ACCEPT

iptables -A OUTPUT -p tcp -j REJECT --reject-with tcp-reset
iptables -A OUTPUT -p udp -j REJECT --reject-with icmp-port-unreachable
iptables -A OUTPUT -j REJECT --reject-with icmp-proto-unreach
```
и добавляем в автозагрузку в /etc/rc.local, который теперь выглядит так
```
#!/bin/bash
/etc/squid/policy/iptables
exit 0
```
3. Прописываем в браузер firefox прокси по https://proxy6.net/blog/5-nastroyka-proxy-firefox

Адрес нашего прокси 127.0.0.1 порт 3128

или добавляем в конце файла ~/.profile
```
export HTTP_PROXY="http://127.0.0.1:3128"
export HTTPS_PROXY="http://127.0.0.1:3128"
export FTP_PROXY="http://127.0.0.1:3128"
export http_proxy="http://127.0.0.1:3128"
export https_proxy="http://127.0.0.1:3128"
export ftp_proxy="http://127.0.0.1:3128"
```

4. Запрещаем себе доступ к root

Если после перезагрузки копьютера прокси заработал и мимо прокси компьютер не выходит в интернет, 
то нужно заблокировать все эти настройки от себя, чтобы во время ломок не смог получить доступ к порно.

4.1 Заблокируем флешку, чтобы нельзя было установить на нее Live cd
```
chmod 750 /media
```
4.2 Закроем доступ к телефону ( получилось проверить только для андроид ) 
chmod 750 /usr/lib/gvfs/gvfsd-mtp
chmod 750 /usr/lib/gvfs/gvfsd-gphoto2
Желательно закрыть доступ к телефону андроид и в udev как описано здесь
https://sleeplessbeastie.eu/2018/06/25/how-to-disable-usb-device/

4.3 Закрываем возможность входа в root при загрузке grub
Для этого удаляем лишние записи в меню загрузки
https://itisgood.ru/2019/09/26/kak-nastroit-parametry-zagruzchika-grub2-na-linux/
и запрещаем возможность правки меню при загрузке
https://askubuntu.com/questions/631317/restricting-on-the-fly-editing-of-grub2-menuentries
или как тут
https://xakinfo.ru/network_administration/grub-password/
4.4 Если установлен virtualbox то проверяем доступ к интернету мимо прокси через сетевой мост.

Если доступ есть то выполняем
```
sudo modprobe -r vboxnetflt
```

4.5 Теперь заблокируем root
sudo passwd
и вводим любой случайный пароль, который тут же забываем


Для разблокировки root можно загрузиться с live cd ubuntu (с установочного диска)
и сбросить пароль


Конечно, эта инструкция может покажется довольно трудной, но я буду рад, если
этот способ блокировки порно кому-нибудь поможет        
