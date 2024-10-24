# Práctica 2.3 - Proxy inverso con Nginx

## Clonación de MV

Para crear un servir de proxy inverso, en primer lugar necesitaremos una nueva MV que 
cumpla con este rol. Para ello, clonamos la máquina virtual en la que ya teníamos 
configurado Nginx, de manera que tendremos dos máquinas virtuales idénticas:

![Clonar MV](./images/00clonacion_mv.png)

## Cambios en la MV con rol de Server Web

Los cambios de este apartado se realizan sobre la MV que vaya a funcionar como servidor web, 
es decir, la que se enfoca a alojar los datos de nuestra página.

Para ello cambiaremos el nombre de nuestra página a 'webserver', tanto del directorio 
en /var/www que contiene los archivos de la página como en el archivo de configuración en 
/etc/nginx/sites-available y el enlace simbólico a /etc/nginx/sites-enabled.

En primer lugar, ejecutamos:
```console
cd /var/www
sudo mv despliegue1/ webserver/
```

A continuación, para listar los enlaces simbólicos y comprobar sus nombres podemos ejecutar:
```console
cd /etc/nginx/sites-enabled
ls -l
```

![Listar symlinks](./images/01listar_enlaces.png)

A continuación eliminamos el symlink (en mi caso se llama despliegue1 porque es el nombre 
que le di a mi página) con el comando:
```console
sudo unlink despliegue1
```

Ahora cambiamos el nombre del sitio a 'webserver' en el archivo de configuración de 
la página. Con: 
```console
cd /etc/nginx/sites-available
mv despliegue1 webserver
```
cambiamos el nombre del archivo en sí. Realizamos el mismo cambio dentro del archivo de la siguiente manera:

![Archivo configuración webserver](./images/02conf_webserver.png)

> [!NOTE]
> También sería adecuado realizar un cambio similar en /etc/hosts pero no es 
> estrictamente necesario para el funcionamiento del servidor.

## Cambios en la MV con rol de Servidor de Proxy Inverso
