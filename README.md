# ciberseguridad_lab4

1.	Instalar VirtualBox (Si ya lo tienes instalado saltar este paso)

https://www.oracle.com/latam/virtualization/technologies/vm/downloads/virtualbox-downloads.html?source=:ow:o:p:nav:mmddyyVirtualBoxHero\_latam\&intcmp=:ow:o:p:nav:mmddyyVirtualBoxHero\_latam

2.	Instalar vagrant de acuerdo a la versión de SO que se tenga
https://developer.hashicorp.com/vagrant/install

3.	Descargar las máquinas virtuales utilizando los repositorios de vagrant 

https://github.com/rapid7/metasploitable3

Windows

#mkdir metasploitable3-workspace

#cd metasploitable3-workspace

#Invoke-WebRequest -Uri "https://raw.githubusercontent.com/rapid7/metasploitable3/master/Vagrantfile" -OutFile "Vagrantfile"

#vagrant up

Linux

#mkdir metasploitable3-workspace

#cd metasploitable3-workspace

#curl -O https://raw.githubusercontent.com/rapid7/metasploitable3/master/Vagrantfile \&\& vagrant up

Una vez que termine de hacer el deploy de las máquinas virtuales ubuntu1404 y win2k8 usted ya las veras creadas en virtualbox

4. Configuración de interfaces de red de las maquinas virtuales

* Maquina Kali Linux: Red Adacter 1 modo NAT
* Maquina Kali Linux: Red Adacter 2 modo host only (Adacter name: este debe ser la misma en todas las maquinas virtuales)
* Maquina Ubuntu1404: Red Adacter 1 modo host only
* Maquina Ubuntu1404: Red Adacter 2 modo red interna
* Maquina Win2k8: Red Adacter 1 modo host only

5. En Kali Linux validar direccionamiento asignado a las interfaces

ifconfig eth0 (interface 1: esta es para navegación)
ifconfig eth1 (interface 2: segmento para pruebas de laboratorio)

6. utilizando nmap para identificar los equipos activos en la red

namp -sn 192.168.8.0/24 (o la red que te asigne en la interface eth1)

\\home\\kali> ifconfig

<pre><font color="#5EBDAB">┌──(</font><font color="#277FFF"><b>kali㉿kali</b></font><font color="#5EBDAB">)-[</font><b>~/Desktop</b><font color="#5EBDAB">]</font>
<font color="#5EBDAB">└─</font><font color="#277FFF"><b>$</b></font> <font color="#49AEE6">ifconfig</font>
eth0: flags=4163&lt;UP,BROADCAST,RUNNING,MULTICAST&gt;  mtu 1500
        inet 10.0.2.15  netmask 255.255.255.0  broadcast 10.0.2.255
        inet6 fd17:625c:f037:2:6f10:2624:87d0:e70a  prefixlen 64  scopeid 0x0&lt;global&gt;
        inet6 fe80::9a99:9017:555a:c49c  prefixlen 64  scopeid 0x20&lt;link&gt;
        ether 08:00:27:ce:cc:92  txqueuelen 1000  (Ethernet)
        RX packets 7  bytes 2896 (2.8 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 27  bytes 4113 (4.0 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth1: flags=4163&lt;UP,BROADCAST,RUNNING,MULTICAST&gt;  mtu 1500
        inet 192.168.115.4  netmask 255.255.255.0  broadcast 192.168.115.255
        inet6 fe80::4c3:600a:1793:ec36  prefixlen 64  scopeid 0x20&lt;link&gt;
        ether 08:00:27:f5:be:bf  txqueuelen 1000  (Ethernet)
        RX packets 34  bytes 13674 (13.3 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 36  bytes 10980 (10.7 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73&lt;UP,LOOPBACK,RUNNING&gt;  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10&lt;host&gt;
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 8  bytes 480 (480.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 8  bytes 480 (480.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

                                                                                
<font color="#5EBDAB">┌──(</font><font color="#277FFF"><b>kali㉿kali</b></font><font color="#5EBDAB">)-[</font><b>~/Desktop</b><font color="#5EBDAB">]</font>
</pre>

7. ahora vamos a identificar los equipos activos en la red

<pre><font color="#5EBDAB">┌──(</font><font color="#277FFF"><b>kali㉿kali</b></font><font color="#5EBDAB">)-[</font><b>~/Desktop</b><font color="#5EBDAB">]</font>
<font color="#5EBDAB">└─</font><font color="#277FFF"><b>$</b></font> <font color="#49AEE6">nmap</font> <font color="#5EBDAB">-sn</font> 192.168.115.0/24
Starting Nmap 7.95 ( https://nmap.org ) at 2026-03-26 18:46 EDT
Nmap scan report for 192.168.115.1
Host is up (0.00062s latency).
MAC Address: 0A:00:27:00:00:51 (Unknown)
Nmap scan report for 192.168.115.2
Host is up (0.00100s latency).
MAC Address: 08:00:27:20:C0:1F (PCS Systemtechnik/Oracle VirtualBox virtual NIC)
Nmap scan report for 192.168.115.3
Host is up (0.0022s latency).
MAC Address: 08:00:27:F4:67:50 (PCS Systemtechnik/Oracle VirtualBox virtual NIC)
Nmap scan report for 192.168.115.7
Host is up (0.00061s latency).
MAC Address: 08:00:27:BA:CA:C9 (PCS Systemtechnik/Oracle VirtualBox virtual NIC)
Nmap scan report for 192.168.115.8
Host is up (0.0012s latency).
MAC Address: 08:00:27:B2:A5:30 (PCS Systemtechnik/Oracle VirtualBox virtual NIC)
Nmap scan report for 192.168.115.4
Host is up.
Nmap done: 256 IP addresses (6 hosts up) scanned in 4.57 seconds
</pre>

De los 4 equipos identificados el 192.168.115 es nuestro equipo por lo tanto tenemos 3 posibles disponibles mas en la red

9. Vamos a ver que servicios tienen cada uno de ellos

<pre>                                                                                                                                                                                                                                           
<font color="#5EBDAB">┌──(</font><font color="#277FFF"><b>kali㉿kali</b></font><font color="#5EBDAB">)-[</font><b>~/Desktop</b><font color="#5EBDAB">]</font>
<font color="#5EBDAB">└─</font><font color="#277FFF"><b>$</b></font> <font color="#49AEE6">nmap</font> <font color="#5EBDAB">-sV</font> 192.168.115.3   
Starting Nmap 7.95 ( https://nmap.org ) at 2026-03-26 18:52 EDT
Nmap scan report for 192.168.115.3
Host is up (0.00042s latency).
Not shown: 990 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         ProFTPD 1.3.5
22/tcp   open  ssh         OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http        Apache httpd 2.4.7
111/tcp  open  rpcbind     2-4 (RPC #100000)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
631/tcp  open  ipp         CUPS 1.7
3306/tcp open  mysql       MySQL (unauthorized)
6667/tcp open  irc         UnrealIRCd
8080/tcp open  http        Jetty 8.1.7.v20120910
MAC Address: 08:00:27:F4:67:50 (PCS Systemtechnik/Oracle VirtualBox virtual NIC)
Service Info: Hosts: 127.0.0.1, METASPLOITABLE3-UB1404, irc.TestIRC.net; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.71 seconds
                                                                                                                                                                                                                                            
<font color="#5EBDAB">┌──(</font><font color="#277FFF"><b>kali㉿kali</b></font><font color="#5EBDAB">)-[</font><b>~/Desktop</b><font color="#5EBDAB">]</font>
<font color="#5EBDAB">└─</font><font color="#277FFF"><b>$</b></font> <font color="#49AEE6">nmap</font> <font color="#5EBDAB">-sV</font> 192.168.115.7
Starting Nmap 7.95 ( https://nmap.org ) at 2026-03-26 18:52 EDT
Nmap scan report for 192.168.115.7
Host is up (0.00074s latency).
Not shown: 991 filtered tcp ports (no-response)
PORT      STATE SERVICE  VERSION
21/tcp    open  ftp      Microsoft ftpd
80/tcp    open  http     Microsoft IIS httpd 7.5
4848/tcp  open  ssl/http Oracle Glassfish Application Server
5985/tcp  open  http     Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
8080/tcp  open  http     Sun GlassFish Open Source Edition  4.0
8383/tcp  open  http     Apache httpd
9200/tcp  open  http     Elasticsearch REST API 1.1.1 (name: Adaptoid; Lucene 4.7)
49153/tcp open  msrpc    Microsoft Windows RPC
49154/tcp open  msrpc    Microsoft Windows RPC
MAC Address: 08:00:27:BA:CA:C9 (PCS Systemtechnik/Oracle VirtualBox virtual NIC)
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 66.29 seconds
                                                                                                                                                                                                                                            
<font color="#5EBDAB">┌──(</font><font color="#277FFF"><b>kali㉿kali</b></font><font color="#5EBDAB">)-[</font><b>~/Desktop</b><font color="#5EBDAB">]</font>
<font color="#5EBDAB">└─</font><font color="#277FFF"><b>$</b></font> <font color="#49AEE6">nmap</font> <font color="#5EBDAB">-sV</font> 192.168.115.8
Starting Nmap 7.95 ( https://nmap.org ) at 2026-03-26 18:54 EDT
Nmap scan report for 192.168.115.8
Host is up (0.0079s latency).
Not shown: 977 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
23/tcp   open  telnet      Linux telnetd
25/tcp   open  smtp        Postfix smtpd
53/tcp   open  domain      ISC BIND 9.4.2
80/tcp   open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
111/tcp  open  rpcbind     2 (RPC #100000)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
512/tcp  open  exec        netkit-rsh rexecd
513/tcp  open  login
514/tcp  open  shell       Netkit rshd
1099/tcp open  java-rmi    GNU Classpath grmiregistry
1524/tcp open  bindshell   Metasploitable root shell
2049/tcp open  nfs         2-4 (RPC #100003)
2121/tcp open  ftp         ProFTPD 1.3.1
3306/tcp open  mysql       MySQL 5.0.51a-3ubuntu5
5432/tcp open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
5900/tcp open  vnc         VNC (protocol 3.3)
6000/tcp open  X11         (access denied)
6667/tcp open  irc         UnrealIRCd
8009/tcp open  ajp13       Apache Jserv (Protocol v1.3)
8180/tcp open  http        Apache Tomcat/Coyote JSP engine 1.1
MAC Address: 08:00:27:B2:A5:30 (PCS Systemtechnik/Oracle VirtualBox virtual NIC)
Service Info: Hosts:  metasploitable.localdomain, irc.Metasploitable.LAN; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.95 seconds
                                                                                                                                                                                                                              
10. Ahora de nuestro primer equipo vamos a ver si el servicio de ftp tiene algun xploit disponible
  
<font color="#5EBDAB">┌──(</font><font color="#277FFF"><b>kali㉿kali</b></font><font color="#5EBDAB">)-[</font><b>~/Desktop</b><font color="#5EBDAB">]</font>
<font color="#5EBDAB">└─</font><font color="#277FFF"><b>$</b></font> <font color="#49AEE6">searchsploit</font> <font color="#5EBDAB">-w</font> ProFTPD 1.3.5
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- --------------------------------------------
 Exploit Title                                                                                                                                                                                 |  URL
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- --------------------------------------------
<font color="#EC0101"><b>ProFTPd</b></font> <font color="#EC0101"><b>1.3.5</b></font> - &apos;mod_copy&apos; Command Execution (Metasploit)                                                                                                                                      | https://www.exploit-db.com/exploits/37262
<font color="#EC0101"><b>ProFTPd</b></font> <font color="#EC0101"><b>1.3.5</b></font> - &apos;mod_copy&apos; Remote Command Execution                                                                                                                                            | https://www.exploit-db.com/exploits/36803
<font color="#EC0101"><b>ProFTPd</b></font> <font color="#EC0101"><b>1.3.5</b></font> - &apos;mod_copy&apos; Remote Command Execution (2)                                                                                                                                        | https://www.exploit-db.com/exploits/49908
<font color="#EC0101"><b>ProFTPd</b></font> <font color="#EC0101"><b>1.3.5</b></font> - File Copy                                                                                                                                                                      | https://www.exploit-db.com/exploits/36742
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- --------------------------------------------
Shellcodes: No Results
                                                                                                                                                                                                                                            
<font color="#5EBDAB">┌──(</font><font color="#277FFF"><b>kali㉿kali</b></font><font color="#5EBDAB">)-[</font><b>~/Desktop</b><font color="#5EBDAB">]</font>
<font color="#5EBDAB">└─</font><font color="#277FFF"><b>$</b></font> 

</pre>

<b> Utilizando MetaSploit Framework  </b>

1. Primero necesitamos levantar la db de postgresql

<pre>                                                                                                                                                                                                                                            
<font color="#5EBDAB">┌──(</font><font color="#277FFF"><b>kali㉿kali</b></font><font color="#5EBDAB">)-[</font><b>~/Desktop</b><font color="#5EBDAB">]</font>
<font color="#5EBDAB">└─</font><font color="#277FFF"><b>$</b></font> <font color="#5EBDAB"><u style="text-decoration-style:solid">sudo</u></font> <font color="#49AEE6">systemctl</font> status postgresql
○ postgresql.service - PostgreSQL RDBMS
     Loaded: loaded (/usr/lib/systemd/system/postgresql.service; <font color="#D7D75F"><b>disabled</b></font>; preset: <font color="#D7D75F"><b>disabled</b></font>)
     Active: inactive (dead)

Mar 26 19:26:58 kali systemd[1]: Starting postgresql.service - PostgreSQL RDBMS...
Mar 26 19:26:58 kali systemd[1]: Finished postgresql.service - PostgreSQL RDBMS.
Mar 26 19:27:28 kali systemd[1]: postgresql.service: Deactivated successfully.
Mar 26 19:27:28 kali systemd[1]: Stopped postgresql.service - PostgreSQL RDBMS.
                                                                                                                                                                                                                                            
<font color="#5EBDAB">┌──(</font><font color="#277FFF"><b>kali㉿kali</b></font><font color="#5EBDAB">)-[</font><b>~/Desktop</b><font color="#5EBDAB">]</font>
<font color="#5EBDAB">└─</font><font color="#277FFF"><b>$</b></font> <font color="#5EBDAB"><u style="text-decoration-style:solid">sudo</u></font> <font color="#49AEE6">systemctl</font> start postgresql
                                                                                                                                                                                                                                            
<font color="#5EBDAB">┌──(</font><font color="#277FFF"><b>kali㉿kali</b></font><font color="#5EBDAB">)-[</font><b>~/Desktop</b><font color="#5EBDAB">]</font>
<font color="#5EBDAB">└─</font><font color="#277FFF"><b>$</b></font> <font color="#5EBDAB"><u style="text-decoration-style:solid">sudo</u></font> <font color="#49AEE6">systemctl</font> status postgresql
<font color="#47D4B9"><b>●</b></font> postgresql.service - PostgreSQL RDBMS
     Loaded: loaded (/usr/lib/systemd/system/postgresql.service; <font color="#D7D75F"><b>disabled</b></font>; preset: <font color="#D7D75F"><b>disabled</b></font>)
     Active: <font color="#47D4B9"><b>active (exited)</b></font> since Thu 2026-03-26 19:27:45 EDT; 2s ago
 Invocation: 9f2dae5eec8942108d0663dd8a39b3ba
    Process: 22361 ExecStart=/bin/true (code=exited, status=0/SUCCESS)
   Main PID: 22361 (code=exited, status=0/SUCCESS)
   Mem peak: 1.7M
        CPU: 7ms

Mar 26 19:27:45 kali systemd[1]: Starting postgresql.service - PostgreSQL RDBMS...
Mar 26 19:27:45 kali systemd[1]: Finished postgresql.service - PostgreSQL RDBMS.
</pre>

 2. Ahora configuramos la DB de MetaSploit

<pre>                                                                                                                                                                                                                                           
<font color="#5EBDAB">┌──(</font><font color="#277FFF"><b>kali㉿kali</b></font><font color="#5EBDAB">)-[</font><b>~/Desktop</b><font color="#5EBDAB">]</font>
<font color="#5EBDAB">└─</font><font color="#277FFF"><b>$</b></font> <font color="#5EBDAB"><u style="text-decoration-style:solid">sudo</u></font> <font color="#49AEE6">msfdb</font> init                 
<font color="#FF8A18"><b>[i]</b></font> Database already started
<font color="#FF8A18"><b>[i]</b></font> The database appears to be already configured, skipping initialization
                                                                                                                                                                                                                                            
<font color="#5EBDAB">┌──(</font><font color="#277FFF"><b>kali㉿kali</b></font><font color="#5EBDAB">)-[</font><b>~/Desktop</b><font color="#5EBDAB">]</font>
</pre>

3. Abrimos msfconsole para tratar de ejecutar el xploit

Validamos que se conecte la DB

<pre><font color="#5EBDAB">┌──(</font><font color="#277FFF"><b>kali㉿kali</b></font><font color="#5EBDAB">)-[</font><b>~/Desktop</b><font color="#5EBDAB">]</font>
<font color="#5EBDAB">└─</font><font color="#277FFF"><b>$</b></font> <font color="#5EBDAB"><u style="text-decoration-style:solid">sudo</u></font> <font color="#49AEE6">msfdb</font> init                 
<font color="#FF8A18"><b>[i]</b></font> Database already started
<font color="#FF8A18"><b>[i]</b></font> The database appears to be already configured, skipping initialization

  Abrimos MetaSploit
                                                                                                                                                                                                                              
<font color="#5EBDAB">┌──(</font><font color="#277FFF"><b>kali㉿kali</b></font><font color="#5EBDAB">)-[</font><b>~/Desktop</b><font color="#5EBDAB">]</font>
<font color="#5EBDAB">└─</font><font color="#277FFF"><b>$</b></font> <font color="#49AEE6">msfconsole</font>
Metasploit tip: You can upgrade a shell to a Meterpreter session on many 
platforms using sessions -u &lt;session_id&gt;
                                                  
<font color="#49AEE6"> ______________________________________</font>
<font color="#49AEE6">/ it looks like you&apos;re trying to run a \</font>
<font color="#49AEE6">\ module                               /</font>
<font color="#49AEE6"> --------------------------------------</font>
<font color="#49AEE6"> \</font>
<font color="#49AEE6">  \</font>
<font color="#49AEE6">     __</font>
<font color="#49AEE6">    /  \</font>
<font color="#49AEE6">    |  |</font>
<font color="#49AEE6">    @  @</font>
<font color="#49AEE6">    |  |</font>
<font color="#49AEE6">    || |/</font>
<font color="#49AEE6">    || ||</font>
<font color="#49AEE6">    |\_/|</font>
<font color="#49AEE6">    \___/</font>


       =[ <font color="#FEA44C">metasploit v6.4.96-dev</font>                                ]
+ -- --=[ 2,568 exploits - 1,316 auxiliary - 1,683 payloads     ]
+ -- --=[ 433 post - 49 encoders - 13 nops - 9 evasion          ]

Metasploit Documentation: https://docs.metasploit.com/
The Metasploit Framework is a Rapid7 Open Source Project

<u style="text-decoration-style:solid">msf</u> &gt; db_status
<font color="#277FFF"><b>[*]</b></font> Connected to msf. Connection type: postgresql.
<u style="text-decoration-style:solid">msf</u> &gt; 
<u style="text-decoration-style:solid">msf</u> &gt; 

</pre>

