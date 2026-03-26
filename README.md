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
