# Solució: T06: Accés remot. Escriptori remot (RDP) (tasca individual)

## Máquina Windows:

Lo primero que tenemos que hacer es poner la máquina Windows en el adaptador de “Red NAT” para que se puedan ver y al mismo tiempo tengan conexión a internet .

![foto 1](img/foto1.png)

## Máquina Zorin:

Lo mismo ponemos la máquina Zorin en adaptador de “Red NAT” para que se pueda ver con la máquina de Windows y que al mismo tiempo tenga conexión a internet.

![foto 2](img/foto2.png)

## Configuración de la Máquina Windows:

Una vez iniciada la máquina, nos vamos a la configuración y entramos a sistemas y a escritorio remoto, y obviamente activamos la opción de escritorio remoto. Esto es para que otra máquina en este caso en Zorin se pueda conectar remotamente.

![foto 3](img/foto3.png)

Ahora entramos a “Usuarios de Escritorio Remoto” para decirle a la máquina que usuario tendrá el permiso para conectarse remotamente.

![foto 4](img/foto4.png)

Una vez dentro le damos a agregar.

![foto 5](img/foto5.png)

Aquí tenemos que poner lo mismo que sale en el apartado: Desde esta ubicación. Ponemos eso donde dice “Escriba los nombres de objeto que desea seleccionar”, ponemos eso y una barra y el nombre del usuario de la máquina Windows. En mi caso será /usuari y por último le damos a aceptar.

![foto 6](img/foto6.png)

Cómo podemos ver ya estaría, le damos a aceptar.

![foto 7](img/foto7.png)

Y ya nos sale en los usuarios de escritorio remoto, vemos que es el mismo y le damos a aceptar.

![foto 8](img/foto8.png)

Después también desactivamos el firewall. Nos vamos a la configuración del sistema y entramos a “Privacidad y seguridad” y entramos a “Firewall y protección de red”.

![foto 9](img/foto9.png)

Y desactivamos todo.

![foto 10](img/foto10.png)

![foto 11](img/foto11.png)

## Configuración de la máquina Zorin:

Una vez iniciada la máquina, nos vamos a la configuración de la máquina y entramos a sistemas y a escritorio remoto.

![foto 12](img/foto12.png)

Y activamos las dos opciones, compartición de escritorio y control remoto.
Como podemos ver nos sale el nombre del equipo, el puerto, el nombre del usuario y la contraseña.

![foto 13](img/foto13.png)

## Conexión desde Zorin a Windows:

Desde la máquina de Windows abrimos la terminal y hacemos ipconfig para ver la ip y poder conectarnos desde la máquina Zorin.

``` bash
ipconfig
```

![foto 14](img/foto14.png)

Después entramos a la aplicación Remmina para conectarnos.

![foto 15](img/foto15.png)

Una vez dentro ponemos la ip que nos dio la máquina Windows.

![foto 16](img/foto16.png)

Nos pedirá certificación a lo cuál le damos que si queremos aceptar el certificado.

![foto 17](img/foto17.png)

Nos pedirá que pongamos el nombre de usuario y contraseña de la máquina Windows y le damos a aceptar.

![foto 18](img/foto18.png)

Después de hacer la validación y eso ya nos hemos conectado y como podemos ver nos aparece la pantalla de la máquina Windows dentro de la máquina Zorin.

![foto 19](img/foto19.png)

## Conexión desde Windows a Zorin:

Lo mismo desde la máquina Zorin hacemos ip a para ver la ip de la máquina y poder conectarnos desde la máquina Windows.

``` bash
ip a
```

![foto 20](img/foto20.png)

Ahora abrimos la aplicación de “Conexión a Escritorio remoto”

![foto 21](img/foto21.png)

Una vez dentro de la aplicación, ponemos la ip de la máquina Zorin y le damos a aceptar.

![foto 22](img/foto22.png)

Seguidamente nos pedirá el nombre de usuario y la contraseña, en este caso no es el usuario de la máquina ni la contraseña del usuario. En este caso para poner el usuario y la contraseña no vamos a configuraciones y a sistemas y dentro entramos a escritorio remoto.

![foto 23](img/foto23.png)

Y el usuario que tenemos que poner y la contraseña es la siguiente:

![foto 24](img/foto24.png)

Ahora si ponemos el nombre de usuario y la contraseña que he indicado antes.

![foto 25](img/foto25.png)

Igualmente nos sale la certificación y le damos que si.

![foto 26](img/foto26.png)

Y como podemos ver ya nos hemos conectado desde la máquina Windows a la máquina Zorin.

![foto 27](img/foto27.png)


[Torna a l'enunciat](README.md)
