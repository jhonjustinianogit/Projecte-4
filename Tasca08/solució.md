# Solució: T08: Auditoria de Qualitat i Estandardització de Servidors (tasca individual)
# Auditoria de Qualitat i Estandardització de Servidors (SOP)

A continuació, es detallen les tasques que heu de realitzar per preparar la vostra prova de  certificació.  

## Tasca 1: Desplegament de la Plantilla (OVA) 

Importeu la màquina virtual "Ubuntu Server Base" (el fitxer .ova proporcionat). Assegureu-vos  de marcar l’opció per generar noves adreces MAC en totes les interfícies.  

## Tasca 2: Configuració de Xarxa i Identitat  

Un cop inicieu la màquina, verifiqueu les adreces IP que us proporciona.  

![foto 1](img/foto1.png)

Canvieu a VirtualBox la interfície que està en NAT per “adaptador pont”. Editeu el Netplan amb  la següent configuració: 

![foto 2](img/foto2.png)

-  Adreça 192.168.C.X on C=2 (A) o 4 (B) i X és el vostre número de llista.
-  Porta d’enllaç 192.168.2.254 o 192.168.4.254 segons correspongui.
-  Servidor de noms: 8.8.8.8  

![foto 3](img/foto3.png)

![foto 4](img/foto4.png)

Apliqueu els canvis i verifiqueu les adreces.  

![foto 5](img/foto5.png)

A continuació canviareu el nom del servidor:  

- Canvieu el nom de la màquina a srv-baseXX (on XX és el vostre número).  

![foto 6](img/foto6.png)

![foto 7](img/foto7.png)

Apliqueu els canvis i verifiqueu que els noms es resolen correctament.  

![foto 10](img/foto10.png)

- Editeu l’arxiu de host perquè el FQDN sigui srv-baseXX.everpia.test 

![foto 8](img/foto8.png)

![foto 9](img/foto9.png)

Apliqueu els canvis i verifiqueu que els noms es resolen correctament.  

![foto 10](img/foto10.png)

Reiniciamos la máquina:

![foto 11](img/foto11.png)

![foto 12](img/foto12.png)

## Tasca 3: Cicle de Vida i Seguretat (Actualitzacions) 

Un servidor no actualitzat és un servidor vulnerable.  

1.Executeu una actualització completa del sistema (repositoris i paquets).  

![foto 13](img/foto13.png)

2.Verifiqueu que no queden actualitzacions pendents. 

![foto 14](img/foto14.png)

## Tasca 4: Gestió d'Aplicacions (Paquets)  

Sovint necessitem eines addicionals o hem d'eliminar programari innecessari.  

1.Instal·lació: Instal·leu el paquet tree (una eina útil per visualitzar directoris). 

![foto 15](img/foto15.png)

2.Verificació: Executeu tree --version per demostrar que s'ha instal·lat.  

![foto 16](img/foto16.png)

3.Eliminació: Suposem que el paquet vim no està permès per la política de seguretat d'EverPia  (només es permet nano). Desinstal·leu completament el paquet vim (incloent la seva configuració). Elimineu dependències innecessàries amb apt autoremove.  

![foto 17](img/foto17.png)

## Tasca 5: Gestió d'Usuaris i Grups  

**Grups:** Creeu dos grups: developers i designers.  

![foto 18](img/foto18.png)

**Usuaris:**

- Creeu un usuari ana_dev i afegiu-lo al grup developers.  

![foto 19](img/foto19.png)

- Creeu un usuari marc_design i afegiu-lo al grup designers.  

![foto 20](img/foto20.png)

Verificació: Mostreu el contingut de l'arxiu /etc/group (utilitzant grep) on es vegin els nous grups i  els usuaris assignats.  

![foto 21](img/foto21.png)

## Tasca 6: Gestió de Permisos i Propietat 

Aquesta és la tasca més crítica. Hem de crear l'estructura de carpetes del projecte i assignar els  permisos correctes per evitar que els departaments es molestin entre ells.  

**Creació d'Estructura:**

- Creeu un directori arrel: /srv/projectes  

![foto 22](img/foto22.png)

- Creeu dos subdirectoris: /srv/projectes/dev_area i /srv/projectes/design_area.  

![foto 23](img/foto23.png)

**Assignació de Propietat (Ownership):**

- La carpeta dev_area ha de pertànyer a root i al grup developers.  

![foto 24](img/foto24.png)

- La carpeta design_area ha de pertànyer a root i al grup designers.  

![foto 25](img/foto25.png)

**Assignació de Permisos:**

-  El propietari (root) ha de tenir control total (rwx) sobre les carpetes.  

![foto 26](img/foto26.png)

- El grup propietari de cada carpeta (developers, designers) ha de poder crear i modificar fitxers  dins la seva carpeta (rwx).  

![foto 27](img/foto27.png)

- Verificar els permisos amb la comanda ls -l 

![foto 28](img/foto28.png)

- Important: Els usuaris d'un grup NO han de poder veure el contingut ni accedir a la carpeta de  l'altre grup. (Permisos 770).

![foto 29](img/foto29.png)

## Proves: 

![foto 30](img/foto30.png)

![foto 31](img/foto31.png)

![foto 32](img/foto32.png)

![foto 33](img/foto33.png)

![foto 34](img/foto34.png)

![foto 35](img/foto35.png)

![foto 36](img/foto36.png)

![foto 37](img/foto37.png)

![foto 38](img/foto38.png)

![foto 39](img/foto39.png)


[Torna a l'enunciat](README.md)

