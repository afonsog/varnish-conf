# Varnish-conf
Docker container basado en https://github.com/rancher/catalog-dockerfiles/tree/master/utils/containers/confd para definir un archivo de configuracion de Varnish a partir de metadatos de Rancher.

## Como funciona
Este contenedor recolecta metadatos definidos en Rancher. Para esto se tiene definido dentro de la carpeta conf.d un archivo en donde se define: que template leera confd, donde almacenara el archivo generado y un conjunto de claves.
El template mediante el cual generara el archivo de configuración en templates/default.vcl.tmpl. 

Los metadatos en Rancher deben ser definidos de la siguiente manera, ejemplo de rancher-compose.yml:

```yml
nginx:
	scale: 1
  	metadata:
    	varnish-backends:
      		backend1:
        		host: ....
			port: ....
			max-connections: ....
	      	backend2:
        		host: ....
			port: ....
			max-connections: ....
	      	backendN:
			host: ....
			port: ....
			max-connections: ....
      		options: |
```

Los campos a partir de metadata son los que nos importan.
Los campos posibles de editar son los siguientes:
* backend1..backendN: campo que indica cada uno de los backends a definir. Campo obligatorio y cada uno debe ser unico, como se encuentra definido anteriormente.
* * host: campo que indica el host del backend
* * port: puerto en el que se encuentra escuchando
* * max-connections: 
* options: campo opcional, configuraciones opcionales para varnish
