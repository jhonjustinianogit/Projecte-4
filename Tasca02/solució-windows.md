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




























