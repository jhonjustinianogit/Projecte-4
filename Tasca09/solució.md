# Solució: T09: Servidor fitxers Linux. NFS (tasca individual)

## Fase 1: Preparació de l'entorn

### Per preparar aquesta prova de concepte, necessitaràs dues màquines virtuals Linux: tot i que pel servidor podríem fer servir qualsevol distribució, ens decantarem per Ubuntu Server 24.04 LTS per la seva facilitat d'ús i popularitat. Per al client, utilitzarem Zorin OS 18. Els dos equips els configurarem amb dues interfícies de xarxa: una NAT per a l'accés a Internet i una adaptador de xarxa només-amb-amfitrió per a la comunicació entre ells i potencialment, treballar via terminal SSH amb el servidor.

**Ubuntu Server:**

Creamos la máquina

![foto1](img/f1.png)

Nos vamos a configuraciones y en red ponemos el primer adaptador en “NAT” para tener conexión a internet.

![foto2](img/f2.png)

Habilitamos el segundo adaptador y ponemos en “Adaptador de solo anfitrión” para que las máquinas se puedan conectar entre ellas.

![foto3](img/f3.png)

**Zorin Cliente:**

Lo mismo creamos la máquina

![foto4](img/f4.png)

Una vez creada la máquina, nos vamos a configuraciones y en red, en el adaptador 1 ponemos “NAT” para que la máquina tenga conexión a internet.

![foto5](img/f5.png)

Después habilitamos el segundo adaptador y lo ponemos en “Adaptador de solo anfitrión” para que se pueda conectar con la otra máquina del server.

![foto6](img/f6.png)

### Tots dos equips els instal·larem seguint els requisits recomanats. L'idioma triat serà espanyol (Espanya) i amb l'idioma per defecte en espanyol. En el cas d'Ubuntu Server, seleccionarem la instal·lació del servei SSH durant el procés d'instal·lació per facilitar la gestió remota.

**Ubuntu Server:**

Le damos a iniciar la máquina y ahora sí toca hacer la instalación, tal y como nos lo pide la tasca, seleccionamos el idioma que será “Español” de España.

![foto7](img/f7.png)

Nos dice que el idioma por defecto del teclado también es “Español” de España.

![foto8](img/f8.png)

Tal y como nos pide la tasca durante el proceso de instalación instalaremos el SSH.

![foto9](img/f9.png)

**Zorin Cliente:**

Hacemos lo mismo con el Zorin del cliente, iniciamos la máquina y hacemos el proceso de instalación, seleccionamos el idioma, el cuál será “Español de España” y le damos a Instalar Zorin OS.

![foto10](img/f10.png)

Lo mismo con el teclado, seleccionamos “Español” de España y continuamos.

![foto11](img/f11.png)

### Ens assegurarem que ambdues màquines tinguin accés a Internet i que es puguin comunicar entre elles a través de la xarxa només-amb-amfitrió i actualitzarem els sistemes amb les últimes actualitzacions disponibles.

**Ubuntu server:**

Para asegurarnos de que la máquina del servidor en este caso Ubuntu Server tenga conexión a internet hacemos un ping a google. 

``` bash
ping google.com
```

![foto12](img/f12.png)

Para comprobar que las dos máquinas puedan comunicarse entre ellas, desde la máquina del cliente que en este caso es la máquina Zorin hacemos ip a para ver la ip del adaptador de solo anfitrión para que después nos conectemos con esa ip desde la máquina Ubuntu del servidor.

``` bash
ip a
```

![foto13](img/f13.png)

Después de hacer ip a en la máquina Zorin del cliente, desde la máquina Ubuntu que es del servidor hacemos un ping a esa ip del adaptador de solo anfitrión de la máquina del cliente.

``` bash
ping 192.168.56.106
```

![foto14](img/f14.png)

Por último actualizamos el sistema.

``` bash
sudo apt apgrade && sudo apt update
```

![foto15](img/f15.png)

**Zorin Cliente:**

Lo mismo con el Zorin del cliente, para asegurarnos de que tenemos conexión a internet hacemos un ping a google.

``` bash
ping google.com
```

![foto16](img/f16.png)

Después hacemos ip a desde la máquina Ubuntu para ver la ip del adaptador de solo anfitrión para que con esa ip hagamos un ping desde la máquina Zorin a la máquina Ubuntu.

``` bash
ip a
```

![foto17](img/f17.png)

Ahora desde la máquina Zorin del cliente hacemos un ping a esa ip del adaptador de solo anfitrión de la máquina Ubuntu.

``` bash
ping 192.168.56.105
```

![foto18](img/f18.png)

Y por último actualizamos el sistema.

``` bash
sudo apt apgrade && sudo apt update
```

![foto19](img/f19.png)

## Fase 2: Preparació del servidor

### Abans de compartir res, hem de preparar els usuaris i els directoris al Servidor.

- **1.Creació de Grups: Crear dos grups per al client: devs i admins.**

Para crear los grupos hacemos las siguientes comandas:

``` bash
sudo groupadd devs
sudo groupadd admins
```

![foto20](img/f20.png)

Después de crear los dos grupos hacemos las siguientes comandas para comprobar que se han creado bien.

``` bash
grep devs /etc/group
grep admins /etc/group
```

En lo que vemos que se han creado correctamente.

![foto21](img/f21.png)

- **2.Creació d'Usuaris: Crear un usuari dev01 (membre del grup devs).**

Hacemos la siguiente comanda para crear los usuario, que se creen con la carpeta personal y para hacerlo miembro del grupo que nos pide. 

``` bash
sudo useradd -G devs -m -s /bin/bash dev01
```

![foto22](img/f22.png)

Después hacemos la comanda que se muestra a continuación para confirmar que lo hemos hecho bien.

``` bash
grep dev01 /etc/passwd
```

![foto23](img/f23.png)

- **3.Crear un usuari admin01 (membre del grup admins).** 

Hacemos la siguiente comanda para crear los usuario, que se creen con la carpeta personal y para hacerlo miembro del grupo que nos pide. 

``` bash
sudo useradd -G admins -m -s /bin/bash admin01
```

![foto24](img/f24.png)

Después hacemos la comanda que se muestra a continuación para confirmar que lo hemos hecho bien.

``` bash
grep admin01 /etc/passwd
```

![foto25](img/f25.png)

**Creació de Directoris (al Servidor):**

- **4.Crear el directori per als projectes de desenvolupament: /srv/nfs/dev_projects**

Para crear el directorio para los proyectos hacemos la siguiente comanda.

``` bash
sudo mkdir /srv/nfs/dev_projects
```

![foto26](img/f26.png)

- **5.Crear el directori per a les eines d'administració: /srv/nfs/admin_tools**

Para crear el directorio para las herramientas de administración hacemos casi el mismo comando solo que al final cambiamos el nombre.

``` bash
sudo mkdir /srv/nfs/admin_tools
```

![foto27](img/f27.png)

Como podemos ver, hacemos la comanda ls /srv/nfs y dentro nos salen los dos directorios creados anteriormente.

``` bash
ls /srv/nfs
```

![foto28](img/f28.png)

- **6.Permisos del Servidor (El punt clau):**

**Es vol que els developers tinguin control total sobre els seus projectes.**

Hacemos la siguiente comanda para que developers tengan el control total sobre sus proyectos.

``` bash
sudo chown root:devs /srv/nfs/dev_projects
```

![foto29](img/f29.png)

**Es vol que els administradors tinguin control sobre les seves eines.**

Hacemos la siguiente comanda para que administradors tengan el control total sobre sus herramientas.

``` bash
sudo chown root:admins /srv/nfs/admin_tools
```

![foto30](img/f30.png)

**En tots dos casos, l'usuari propietari serà root.**

En las capturas anteriores se ve como root es el propietario.

También le asignamos los permisos a las carpetas:

``` bash
sudo chmod 2775 /srv/nfs/dev_projects
sudo chmod 2775 /srv/nfs/admin_tools
```

![foto31](img/f31.png)

Y hacemos la comanda ls -l para comprobar que los permisos son los correctos

``` bash
ls -l /srv/nfs
```

![foto32](img/f32.png)

Después antes de hacer el siguiente punto tenemos que crear los grupos y los usuarios que tengan el mismo ID en la máquina cliente osea en Zorin.

Instalamos la aplicación users and groups para crear los grupos y los usuarios.

![foto33](img/f33.png)

Miramos que los usuarios y grupos estén todos bien “contraseña de los usuarios en zorin es usuari”

Hacemos la siguiente comanda para ver que tengamos el mismo ID y que se hayan creado bien los usuarios.

``` bash
cat /etc/group
```

![foto34](img/f34.png)

``` bash
sudo grep dev01 /etc/passwd
sudo grep admin01 /etc/passwd
```

![foto35](img/f35.png)

Y lo mismo, hacemos la siguiente comanda para ver que los grupos estén bien y hayamos asignados bien a los usuarios al grupo que corresponde.

``` bash
sudo grep devs /etc/group
sudo grep admins /etc/group
```

![foto36](img/f36.png)

- **7.Com a pas final, s'instal·laran els paquets necessaris per al servei NFS al servidor i es configurarà l'exportació dels directoris amb les opcions adequades.**

Para instalar los paquetes necesarios para el servicio NFS hacemos la siguiente comanda.

``` bash
sudo apt install nfs-kernel-server -y
```

![foto37](img/f37.png)

Comprobamos que se haya instalado bien y que esté activo.

``` bash
sudo systemctl status nfs-kernel-server
```

![foto38](img/f38.png)

Una vez vemos que está activo, tenemos que editar el archivo /etc/exports para decir que archivos queremos exportar, que en este caso vamos a exportar el archivo /srv/nfs 

``` bash
sudo nano /etc/exports
```

Añadimos la línea que está al final.

``` bash
/srv/nfs *(rw,sync,no_subtree_check)
```

![foto39](img/f39.png)

Después tenemos que reiniciar el servicio para poder aplicar los cambios.

``` bash
sudo systemctl restart nfs-kernel-server
```

![foto40](img/f40.png)

Una vez reiniciado el servicio lo que tenemos que hacer es comprobar que todo funciona bien y correctamente, para eso en la máquina Ubuntu del server hacemos la siguiente comanda para ver qué archivos son los que podemos exportar.

``` bash
sudo exportfs -u
```

Y como podemos ver nos dice que archivos son los que podemos exportar en este caso está todo bien ya que coincide con la línea añadida en el archivo /etc/exports.

![foto41](img/f41.png)

Después hacemos ip a para ver la ip del adaptador de solo anfitrión.

``` bash
ip a
```

![foto42](img/f42.png)

Para que con esa ip probemos de hacer la siguiente comanda para ver el puerto desde el cuál trabaja.

``` bash
sudo rpcinfo -p 192.168.56.105
```

![foto43](img/f43.png)

Como podemos ver, en este caso trabaja desde el puerto 2049.

![foto44](img/f44.png)

Después nos conectamos desde el cliente que es Zorin a la máquina del servidor que es Ubuntu, pero para eso primero tenemos que instalar el paquete nfs-common. 

``` bash
sudo apt install nf-common
```

![foto45](img/f45.png)

Ahora sí después nos conectamos desde el cliente que es Zorin a la máquina del servidor que es Ubuntu con la ip del adaptador de solo anfitrión de la máquina del server que es Ubuntu.

``` bash
sudo showmount -e 192.168.56.105
```

En la cuál una vez conectado vemos ,la carpeta /srv/nfs que es lo que podemos exportar.

![foto46](img/f46.png)

## Fase 3: L'Exportació d'Administració (El Dilema del root_squash)

### El client necessita que el directori /srv/nfs/admin_tools sigui accessible per l'equip d'administradors. A vegades, l'usuari root del client (que sou vosaltres, els consultors) necessitarà escriure en aquest directori per instal·lar eines. Aquí mostrarem un error típic i la seva solució.

- **Prova 1 (L'error comú)**

**Exportar el directori /srv/nfs/admin_tools amb les opcions 'rw,sync'.**

Como hemos visto anteriormente ya exportamos el archivo /srv/ns/ en el archivo exports

![foto47](img/f47.png)

**Des del client, muntar aquest recurs compartit a /mnt/admin_tools. Com a root del client, intentar crear un fitxer dins d'aquest directori muntat.**

Primeramente creamos la carpeta ya que seguramente no exista.

``` bash
sudo mkdir /mnt/admin_tools
```

![foto48](img/f48.png)

Después de crear la carpeta lo que tenemos que hacer es montar los recursos para eso utilizaremos la siguiente comanda.

``` bash
sudo mount -t nfs 192.168.56.105:/srv/nfs/admin_tools /mnt/admin_tools
```

![foto49](img/f49.png)

Una vez montado intentaremos crear un archivo dentro de esta carpeta, yo lo haré desde los archivos de la máquina para eso nos vamos a archivos y localizamos la carpeta de “mnt” y entramos.

![foto50](img/f50.png)

Una vez dentro de la carpeta, intentamos entrar a la carpeta “admin_tools” y vemos que nos pide autenticación, ponemos la contraseña del usuario de la máquina.

![foto51](img/f51.png)

![foto52](img/f52.png)

Una vez dentro si intentamos crear un archivo vemos que no nos deja, ya que no tenemos los permisos.

![foto53](img/f53.png)

**Verificar quin és el propietari del fitxer creat. Per què? Justificar la resposta amb l'explicació tècnica de 'root_squash'.**

No nos deja entrar a la carpeta ya que no tenemos los permisos, eso nos pasa por que no tenemos el root_squash, lo cuál causa que el usuario de la máquina cliente no es el mismo root que el de la máquina server que es Ubuntu. “Pero veremos como en la siguiente actividad “Prueba 2 (La Solución)”lo solucionamos”

Mientras que vemos que si con el usuario admin si podemos crear, eso pasa ya que el usuario admin si tiene los permisos necesarios en esta carpeta. Para eso hacemos lo siguiente:

``` bash
sudo login admin01
```

Nos ponemos con usuario admin e intentamos crear un archivo y vemos que sí que podemos, además también hacemos un ls + la ruta de carpeta para ver que se ha creado.

``` bash
touch /mnt/admin_tools/file01
ls /mnt/admin_tools
```

![foto54](img/f54.png)

Como podemos ver el propietario es el usuario admin01.

``` bash
cd /home/cliente
ls -l /mnt/admin_tools
```

![foto55](img/f55.png)

Y vemos como ahora en la siguiente prueba vemos como podemos solucionar para que ahora sí el usuario root pueda crear archivos.

- **Prova 2 (La Solució)**

**Modificar l'exportació del directori /srv/nfs/admin_tools per incloure l'opció 'no_root_squash'.**

Para comenzar tenemos que editar el archivo /etc/exports.

``` bash
sudo nano /etc/exports
```

En el que editamos la linea anterior para incluir la opción de “no_root_squash” y además añadimos la segunda línea 

``` bash
/srv/nfs/admin_tools *(rw,sync,no_subtree_check,no_root_squash)
/srv/nfs/dev_projects *(rw,sync,no_subtree_check)
```

![foto56](img/f56.png)

Como podemos ver en la imágen anterior, la segunda línea, me he equivocado y he puesto “rm” en cuenta de “rw” y también he puesto “syn” en cuenta de “sunc”. (ERROR MÍO) pero lo correcto sería como se muestra en el comando de antes de la imágen, pero que también lo pongo a continuación. LO CORRECTO SERÍA:

``` bash
/srv/nfs/admin_tools *(rw,sync,no_subtree_check,no_root_squash)
/srv/nfs/dev_projects *(rw,sync,no_subtree_check)
```

Una vez hecho eso, lo que tenemos que hacer es reiniciar el servicio para que se apliquen los cambios. 

``` bash
sudo systemctl restart nfs-kernel-server
```

![foto57](img/f57.png)

**Al client, desmuntar i tornar a muntar el recurs compartit.**

Ahora nos dice que tenemos que desmontar y volver a montar nuevamente los recursos compartidos, para eso hacemos las siguientes comandas.

Para desmontar:

``` bash
sudo umount /mnt/admin_tools
```

![foto58](img/f58.png)

Para montar la ip que ponemos es la ip del adaptador de solo anfitrión de la máquina del Ubuntu que es el servidor.

``` bash
sudo mount 192.168.56.105:/srv/nfs/admin_tools /mnt/admin_tools
```

![foto59](img/f59.png)

Aquí vemos las dos comandas juntas, la primera es para desmontar y la segunda para montar.

![foto60](img/f60.png)

**Com a root del client, intentar crear un fitxer dins d'aquest directori muntat. Observeu quin és el propietari del fitxer creat aquesta vegada. Ha canviat alguna cosa? Justificar la resposta amb l'explicació tècnica de 'no_root_squash'.**

Ahora si intentamos crear un archivo como root, como el anterior archivo era file01 ahora en este caso será file02. Para eso entramos a root y creamos como root el file02


``` bash
sudo su root
touch /mnt/admin_tools/file02
```

![foto61](img/f61.png)

Ahora hacemos ls + la ruta de la carpeta para ver que se haya creado bien.

``` bash
ls /mnt/admin_tools
```

![foto62](img/f62.png)

Por último hacemos la comanda ls -l + la ruta de la carpeta y vemos que el propietario del archivo “file02” es root.

``` bash
ls -l /mnt/admin_tools
```

![foto63](img/f63.png)

Ahor si que podemos crear un archivo con root, ha cambiado ya que como pueden ver hemos editado el archivo /etc/exports, lo que hemos editado es que el root de las dos máquinas sea el mismo, tanto en la del server que es Ubuntu y la del cliente que es Zorin.

## Fase 4: L'Exportació de Desenvolupament (Permisos rw vs ro)

**Editar /etc/exports per afegir dues exportacions per al mateix directori. El client vol que la xarxa d'administració (p.ex., 192.168.56.0/24) hi pugui escriure, però que la xarxa de consultors (simularem que és una altra IP, p.ex., 192.168.56.100) només pugui llegir.**

Nos pide que la red de administración pueda escribir pero que la red de consultores solo tiene que poder leer.

Para eso nuevamente tenemos que editar el archivo /etc/exports 

``` bash
sudo nano /etc/exports
```

Borramos la segunda línea que había antes y ponemos otras dos, al final como tiene que quedar el archivo /etc/exports es con las tres líneas que se muestran a continuación. Eso lo hacemos para que le asignemos los permisos depende de la ip que tenga el usuario.

``` bash
/srv/nfs/admin_tools *(rw,sync,no_subtree_check,no_root_squash)
/srv/nfs/dev_projects 192.168.56.0/24(rw,sync,no_subtree_check)
/srv/nfs/dev_projects 192.168.56.140(ro,sync,no_subtree_check)
```

![foto64](img/f64.png)

Después como ya sabemos para que se apliquen los cambios reiniciamos el servicio.

``` bash
sudo systemctl restart nfs-kernel-server
```

![foto65](img/f65.png)

**Des del client, muntar el recurs compartit a /mnt/dev_projects i provar d'escriure-hi com a usuari dev01. Hauria de funcionar.**

Ahora lo que tenemos que hacer es montar el disco de dev_projects para comprobar que el funcionamiento es el adecuado.

Para eso primeramente creamos la carpeta.

``` bash
sudo mkdir /mnt/dev_projects
```

![foto66](img/f66.png)

Ahora modificamos la ip, para eso nos vamos a la configuración, entramos a red y editamos el Ethernet (enp0s8)

![foto67](img/f67.png)

Por ejemplo podemos probar con la siguiente ip y la siguiente máscara que se muestra en la imágen.

![foto68](img/f68.png)

Aplicamos y guardamos los cambios, después montamos los recursos, ojo lo montamos con la carpeta /mnt/dev_projects.

``` bash
sudo mount 192.168.56.105:/srv/nfs/dev_projects /mnt/dev_projects
```

![foto69](img/f69.png)

Después de montarlo, entramos como dev01 osea hacemos login y como le hemos puesto la ip del mismo rango, en teoría tiene que dejarnos crear archivos.

``` bash
sudo login dev01
```

Nos metemos en la carpeta con cd

``` bash
cd /mnt/dev_projects
```

![foto70](img/f70.png)

Y como podemos ver a continuación creamos el archivo de ejemplo que se llama “file04” y después hacemos ls y si que nos sale por tanto está bien.

``` bash
touch file04
ls
```

![foto71](img/f71.png)

**Desmuntar el recurs i canviar manualment la IP del client a 192.168.56.100. Tornar a provar d'escriure al directori muntat com a usuari dev01 i comprovar que només funciona la lectura.**

Para eso otra vez nos vamos a la configuración, entramos en red y en Ethernet enp0s8 y editamos la ip y la máscara y ponemos una dentro del rango que nos pide el enunciado.

![foto72](img/f72.png)

Aplicamos y guardamos los cambios, entramos como root. 

``` bash
sudo su root
```

![foto73](img/f73.png)

Entramos a la carpeta y vemos que sí que nos deja entrar a la carpeta y ver el contenido que hay dentro.

``` bash
cd /mnt/dev_projects
ls
```

![foto74](img/f74.png)

Intentamos crear un archivo que en este caso será el file05 y vemos que nos dice que solo tenemos permisos de lectura por tanto está bien.

``` bash
touch file05
```

![foto75](img/f75.png)

Aquí vemos todo el procedimiento junto en una sola captura.

![foto76](img/f76.png)

**Canvieu d'usuari al client a admin01 i torneu a provar d'escriure al directori muntat. Comproveu que no es pot escriure, ja que admin01 no és membre del grup devs (permisos locals del sistema de fitxers).**

Hacemos login con admin01 e intentamos crear un archivo dentro de la carpeta y nos dice que no podemos escribir, por tanto está bien.

``` bash
touch /mnt/dev_projects/file06
```

![foto77](img/f77.png)

## Fase 5: Muntatge Automàtic amb /etc/fstab

### És evident que els usuaris no poden estar muntant manualment els recursos compartits cada vegada que reinicien el sistema. Per això, es configurarà el muntatge automàtic mitjançant el fitxer /etc/fstab al client.

**Editar el fitxer /etc/fstab al client per afegir les entrades necessàries per muntar automàticament els recursos compartits NFS al directori /mnt/admin_tools i /mnt/dev_projects durant l'inici del sistema.**

Primero tenemos que entrar al archivo /etc/fstab

``` bash
sudo nano /etc/fstab
```

Una vez dentro, abajo del todo añadimos las dos últimas líneas que muestro a continuación.

``` bash
192.168.56.105:/srv/nfs/admin_tools /mnt/admin_tools nfs defaults 0 0
192.168.56.105:/srv/nfs/dev_projects /mnt/dev_projects nfs defaults 0 0
```

![foto78](img/f78.png)

**Executar la comanda mount -a per provar les entrades sense reiniciar.**

Después seguidamente hacemos la comanda mount -a para que se apliquen los cambios y se vuelva a montar todo, o si no también podemos reiniciar la máquina y ya.

``` bash
mount -a
"O reinciar la máquina"
```

**Reiniciar el client i verificar que els recursos compartits s'han muntat correctament.**

Como ya hemos reiniciado la máquina en el punto anterior, ahora lo que tenemos que hacer es comprobar que los recursos compartidos se han montado correctamente.

Para eso entramos como root.

``` bash
sudo su root
```

![foto79](img/f79.png)

Hacemos cd para entrar a “media”

![foto80](img/f80.png)

Una vez dentro de media, hacemos la comanda ls -l + ruta, que en este caso será ls -l /mnt/ y nos tendría que salir los dos recursos montados que son admin_tools y dev_projects y como podemos ver esta bien.

``` bash
ls -l /mnt/
```

![foto81](img/f81.png)

En la siguiente imágen vemos todo el procedimiento junto para que lo entiendan mejor.

![foto82](img/f82.png)

## Conclusió

Como hemos visto hemos realizado esta práctica con el NFS y hemos visto que el NFS va bien para compartir los recursos que es su principal función, hemos visto que hemos compartido recursos desde el servidor que en este caso fue Ubuntu hacia el cliente que en este caso fue Zorin, como hemos visto permite hacer una gestión de acuerdo a los usuarios, a los grupos y hasta incluso de acuerdo a la red. Pero no todo es como lo dicen también puede llegar a tener algunos problemas por ejemplo tenemos que crear los mismos usuarios y los mimos grupos en las dos màquinas, en el servidor y en el cliente y que tengan los mismo UID u todo, esto en un entorno real de una empresa física no es muy escalable ya que si tiene muchos equipos o ordenadores tendríamos que hacer lo mismo en todos imaginate si tiene 50 o 100 ordenadores,m tenemos que hacer lo mismo en todos los ordenadores y también el el servidor. 

[Torna a l'enunciat](README.md)

