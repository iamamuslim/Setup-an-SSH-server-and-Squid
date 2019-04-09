# Setup-an-SSH-server-and-Squid
Setup an SSH server and Squid on ubuntu , debain

Requirements:
```
1 VPS Server
2 WinSCP or PuTTY
```
#Steps 1 
Commands:
```
sudo su
apt-get update
apt-get install apache2
apt-get install squid3
```
#Step 2
Access root via PuTTY or WinSCP then go to etc > ssh > sshd_config
Open and edit the file with nano and add
```
Port 443
```

#Step 3
Open squid folder and delete file squid.conf
```
rm -f /etc/squid/squid.conf
```

#Step 4
Create file squid.conf in squid folder
```
nano /etc/squid/squid.conf
```

add:
```
acl url1 url_regex -i 127.0.0.1
acl url2 url_regex -i localhost
acl url3 url_regex -i (IP server)
acl payload url_regex -i "/etc/squid/payload.txt"
http_access allow url1
http_access allow url2
http_access allow url3
http_access allow payload
http_access allow all
http_port 8080
http_port 80
http_port 3128
visible_hostname (Name server)
forwarded_for off
via off
```
Step #5
Restart ssh and squid
```
service ssh restart
service squid restart
reboot
```

Step #6
You can add a new user or exit