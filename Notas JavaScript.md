**Javascript**
===============

- **ECMAScript**:  European Computer Manufacturers Association. Se encarga de la estandarización del lenguaje.
- **DOM**: Document Object Model.
- **BOM**: Browser Object Model.


< script >
---------

- Attributes
	1. Async 
		- Es opcional.
		- Sólo aplica para archivos externos de scripting.
		- Indica que se debe iniciar con el script de inmediato, pero se puede continuar con las demás acciones (no es necesario esperar a que termine el script para continuar).
	2. Charset
		- Es opcional
		- Indica el conjunto de caracteres que se usarán en el script file.
		- Valores comunes: "ISO-8859-1", "UTF-8".
		- Generalmente se usa cuando se utilizan diferentes encodings en el HTML y en el script file.
	3. Defer
		- Es opcional
		- Indica que la ejecución del script puede ser descargado, pero esperará para ser ejecutado hasta que el contenido del documento (HTML) haya sido completamente parseado y desplegado.
		- Se parece a Async pero NO es lo mismo.
		- Sólo aplica para archivos externos de scripting.
		- NO todos los exploradores lo implementan de la misma manera.
	4. Language
		- Deprecated
	5. Src
		- Es opcional.
		- Indica el archivo externo que contiene el código a ser ejecutado.
	6. Type
		- Es opcional
		- Reemplaza el atributo Language; indica el tipo de contenido del lenguaje de scripting que está siendo usado.
		- Generalmente se usa "text/javascript" por compatibilidad con la mayoría de los exploradores.
		- Es seguro omitirlo pues toma como valor por default "text/javascript".


JavaScript inside HTML
----------------------

- Ponerlo dentro de la página HTML dentro de las etiquetas < script >
	- EL código se interpreta de arriba hacia abajo.
	- El resto de la página no se carga o despliega hasta que se termine de ejecutar el código JS.

- Incluirlo desde un archivo externo.
	- Es más fácil hacer modificaciones.
	- Para hacer esto se usa el atributo src que debe tener una URL del archivo que contiene el código JS.
	```
	
	<script type="text/javascript" src="example.js"></script>
	
	```
	- El archivo externo sólo contendrá código JS.
	- Cuando se usa un archivo externo no debe ponerse nada entre las etiquetas de script porque será ignorado.
	- Pueden usarse archivos de internet (con cuidado).


¿En dónde poner las etiquetas de script?
----------------------------------------
- **Dentro del head**
	Si se ponen dentro de las etiquetas de head y el código JS es mucho entonces el usuario no verá el contenido de la página durante un buen tiempo, hasta que el código JS se termine de ejecutar.
- **Al final del body**
	Si se pone dentro de esta etiqueta, primero se cargará el contenido de la página y después se ejecutará el código JS. Esta se considera una mejor experiencia para el usuario porque no lo hará esperar para ver la página.

Defer
-----
- Indica que la ejecución del script puede ser descargado, pero esperará para ser ejecutado hasta que el contenido del documento (HTML) haya sido completamente parseado y desplegado.
- Este atributo indica que el script no modificará la estructura de la página cuando sea ejecutado.
- Sólo aplica para archivos externos de scripting.
- Con Browser que soportan HTML5 este atributo se ignorará cuando se use en un inline script.
- NO todos los exploradores lo implementan de la misma manera.
- En XHTML se debe escribir defer="defer" en HTML sólo defer.
- El primer script se ejecutará primero, después el segundo y los dos se ejecutarán después del evento DOMContentLoaded.
- Se empezó a implementar en los navegadores en sus versiones:
	- IE 4
	- Firefox 3.5
	- Safari 5
	- Chrome 7
- Para navegadores anteriores el atributo será ignorado y se ejecutará normalmente. Por lo que se recomienda poner siempre los scripts al final de la página.


Eventos: DOMContentLoaded vs onLoad
------------------------------------
- **DOMContentLoaded**: Se dispara cuando se terminó de interpretar la página.
- **onLoad**: Se dispara cuando todos los archivos se han terminado de descargar de todos los recursos, incluyendo imagenes.
