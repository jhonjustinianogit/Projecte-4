# Solució Windows: T02: DPR: còpies de seguretat. Cas pràctic

# Part 1: Còpia seguretat dels equips clients Windows

## Configuracions inicials

Primer que tot creguem la màquina Windows i li afegim el segon disc de 10 GB que ens demana la taverna.

![foto 1](img/foto1.png)

Ens anem a emmagatzematge i afegir un disc, dins li donem a crear i posem que sigui de 10GB.

![foto 2](img/foto2.png)

![foto 3](img/foto3.png)

Com podem veure en la següent imatge ja tenim creat el segon disc ara el seleccionem i li donem a “choose”

![foto 4](img/foto4.png)

I aquí en la imatge següent veiem com ja tenim posat el segon disc. Seguidament iniciem la màquina.

![foto 5](img/foto5.png)

Una vegada iniciada la màquina iniciem sessió amb un correu que no sigui de l'escola per a fer la simulació, en el meu cas jo em creu un nou.

![foto 6](img/foto6.png)

Després segueix configurar el segon disc, per a això ens administrarem espai d'emmagatzematge, creem el grup i creem l'espai d'emmagatzematge.

![foto 7](img/foto7.png)

![foto 8](img/foto8.png)

Seguidament, instal·lem el Duplicati i ho iniciem i seguim tots els passos d'instal·lació que ens demana, “només és donar-li següent-següent, instal·lar i posar una contrasenya”. La meva contrasenya és: usuario1234

![foto 9](img/foto9.png)

![foto 10](img/foto10.png)

## Creació de còpia de seguretat “LOCAL”

Una vegada dins de l'aplicació per a crear la còpia de seguretat local li donem a Backups i add.

![foto 11](img/foto11.png)

Seguidament li donem a add a new backup.

![foto 12](img/foto12.png)

Després posem el nom de la còpia, la descripció que en el meu cas jo li vaig posar el mateix en el nom i en la descripció, i posem la contrasenya de la còpia que en el meu cas li vaig posar de contrasenya usuari.

![foto 13](img/foto13.png)

Cliquem en file system - Choose.

![foto 14](img/foto14.png)

Després hem de posar el destí de la còpia que en el meu cas va ser en el disc secundari de 10 GB que van crear al principi.

![foto 15](img/foto15.png)

Seguidament seleccionem la carpeta que volem copiar que en el meu cas jo vaig posar documents.

![foto 16](img/foto16.png)

Seguidament hem de programar la còpia que en aquest cas és el que demana la tasca, a partir de les sis de la tarda del dia 9/12 es faran còpies de seguretat cada hora. després li donem a continuar.

![foto 17](img/foto17.png)

Després finalment posem que es guardin totes les versions.

![foto 18](img/foto18.png)

Podem veure com ja està completada i configurada la còpia.

![foto 19](img/foto19.png)

## Prova de la còpia “LOCAL”

Ens anem a documents i creem un arxiu o document i jo per exemple li vaig posar de nom “Prova t2”

![foto 20](img/foto20.png)

Una vegada creat l'arxiu o document tornem al Duplicati i en la còpia de seguretat del local li donem a start perquè es faci la còpia.

![foto 21](img/foto21.png)

Ara si una vegada feta la còpia, esborrem l'arxiu o document de la carpeta de documents per a fer la prova de restauració.

![foto 22](img/foto22.png)

## Restauració de la còpia de seguretat “LOCAL”

Tornem novament al Duplicati i en “Restores” li donem a start.

![foto 23](img/foto23.png)

Després seleccionem la còpia que volem restaurar, ho seleccionem clicant sobre “Restore”

![foto 24](img/foto24.png)

Després seleccionem el que volem recuperar, en el meu cas és el document Prova t2.

![foto 25](img/foto25.png)

Li diem que ho volem restaurar a la ubicació original.

![foto 26](img/foto26.png)

I finalment li donem a Submit.

![foto 27](img/foto27.png)

Ens diu que la restauració està completada.

![foto 28](img/foto28.png)

Per a comprovar que realment la restauració estigui completa i ben feta verifiquem en la carpeta de documents que estigui novament el document de “Prova t2” i efectivament si està.

![foto 29](img/foto29.png)

## Còpia de seguretat en “Google Drive”

Fem el mateix que abans, li donem a Backups i a add.

![foto 30](img/foto30.png)

Li donem a Add new backup.

![foto 31](img/foto31.png)

Li posem nom i descripció que en el meu cas he posat el mateix de nom que de descripció, també posem contrasenya de la còpia, en el meu cas de contrasenya vaig posar usuari1.

![foto 32](img/foto32.png)

Ara si comencem a configurar la còpia, de destí li posem Google Drive i li donem a Choose.

![foto 33](img/foto33.png)

Després posem la ruta de documents i hem de clicar sobre AuthID, això és per a vincular el nostre compte de Google.

![foto 34](img/foto34.png)

Quan fem clic sobre AuthID se'ns obrirà una finestra perquè vinculem el nostre compte de google on volem fer la còpia.

![foto 35](img/foto35.png)

![foto 36](img/foto36.png)

Una vegada que ja hem vinculat el nostre compte, de nou fem clic en AuthID per a obtenir el codi d'autorització per a poder continuar.

![foto 37](img/foto37.png)

Si no tenim la carpeta documents Duplicati ens la crea.

![foto 38](img/foto38.png)

Després seleccionem que volem copiar, posem documents.

![foto 39](img/foto39.png)

Ara programem l'hora i tot, ho fem d'acord amb el que ens demana la tasca, que serà que es faci la còpia de seguretat cada dia a les 18.00 de la tarda.

![foto 40](img/foto40.png)

Li diem que mantingui totes les còpies, osigui deixem tot com està per defecte i li donem a continuar.

![foto 41](img/foto41.png)

## Prova de la còpia “Google Drive”

Una vegada ja està creada i configurada la còpia li donem a start perquè faci la còpia de seguretat.

![foto 42](img/foto42.png)

Com podem veure no em deixa fer la còpia de seguretat perquè crec que no hem vinculat bé el compte. Tranquils ara ho fem. Cliquem sobre la campaneta que ens surt a baix a la dreta i copiem el link que ens surt en el navegador de google.

![foto 43](img/foto43.png)

Una vegada que copiem el link en un navegador google ens sortirà el següent a la qual cosa cliquem sobre el que posa Google Drive i triem el compte.

![foto 44](img/foto44.png)

![foto 45](img/foto45.png)

Després ens sortirà un codi el qual l'hem de copiar.

![foto 46](img/foto46.png)

Una vegada tinguem el codi copiat tornem al Duplicati, li donem a editar la còpia de seguretat de Google Drive, i entrem a Destinació i on posa AuthID peguem el codi que havíem copiat abans i guardem.

![foto 47](img/foto47.png)

Una vegada ho hem guardat li donem a start a la còpia de seguretat de Google Drive.

![foto 48](img/foto48.png)

Com podem veure ara si que se'ns ha fet la còpia correctament perquè es va crear la carpeta documents en Google Drive amb tots els arxius de còpia.

![foto 49](img/foto49.png)

Ara abans de fer la prova de restauració esborrem el document de Prova t2 de la carpeta de documents.

![foto 50](img/foto50.png)

## Restauració de còpia de seguretat de “Google Drive”

Li donem a restore i start

![foto 51](img/foto51.png)

Després seleccionem la còpia de seguretat de Google Drive i li donem a restore.

![foto 52](img/foto52.png)

Després seleccionem el document de Prova t2 per a restaurar-lo i li donem a continuar.

![foto 53](img/foto53.png)

Li diem que volem que es restauri en la ubicació original.

![foto 54](img/foto54.png)

Li donem a submit i ja estaria.

![foto 55](img/foto55.png)

Com podem veure ens diu que la restauració s'ha realitzat correctament.

![foto 56](img/foto56.png)

Per a comprovar-ho ens anem a la carpeta documento i hauria d'estar en document de Prova t2 i efectivament sí que hi hes.

![foto 57](img/foto57.png)


[Torna a l'enunciat](README.md)

