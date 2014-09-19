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

Async
------
- Fue introducido con HTML5
- Es similar a defer porque cambia la manera en que se procesa el script.
- Sólo aplica para archivos externos de scripting.
- Le dice al navegador que empiece a descargar el archivo inmediatamente.
- En XHTML se debe escribir async="async" en HTML sólo async.
- El parseo de HTML continuará y el script será ejecutado tan pronto como esté listo.
- NO se garantiza que los scripts se ejecuten en el orden en que está especificado; por lo tanto no debe haber dependencias entre los scripts.
- El propósito de este atributo es indicar que la página NO necesita esperar a que el script se descargue y ejecute para continuar cargándose.
- NO se recomienda que los scripts Async modifiquen el DOM cuando se están cargando.
- Se garantiza la ejecución de estos scripts ANTES del evento onLoad y PODRIAN ejecutarse antes del evento DOMContentLoaded.
- Es soportado por las versiones:
	- Firefox 3.6+
	- Safari 5+
	- Chrome 7+

**Tanto defer como async NO son soportados por todas las versiones de navegadores.**


External vs Inline Scripts
----------------------------
- External
	- Es lo recomendado.
	- Mejor mantenibilidad.
	- Tener el código JS separado del HTML permite que se pueda trabajar mejor en equipo.
	- Si un archivo JS es usado por 2 o más páginas HTML, dicho archivo se descarga SÓLO una vez por lo que se reduce el tiempo de cargado de las páginas.
	- Funciona tanto con HTML como con XHTML.
- Inline
	- Si se utilizan caracteres cómo el "<" en el código JS, (dentro del HTML) puede ocasionar problemas, pues el parser lo puede considerar como parte de una etiqueta HTML y no como código de JS ejecutable.
		- SOLUCIONES	
			1. Reemplazar el caracter con sú HTML entity (&lt;)
			2. Envolver el código JS en una sección CDATA. Este tipo de secciones indican que el texto contenido dentro de ellas NO debe ser parseado como parte del documento, por lo que pueden usarse cualquier tipo de caracteres. El problema es que NO todos los navegadores lo entienden, para solucionar esto a veces es necesario comeentar esas etiquetas (//).
			```
				<![CDATA[
					//Código JS
				]]>

				//<![CDATA[
					//Código JS
				//]]>

			```

JS Syntax
---------
- Case-sensitivity
- Identifiers
	- Primer caracter debe ser una letra, un guion bajo o el signo de dolar ($)
	- Los demás caracteres pueden ser letras, guion bajo, signo de dola o números.
	- Se recomienda que la primera palabra sea en minusculas y las demás empiecen con mayúscula (camel case)
		- counter
		- myFirst
		- yourSecond
		- hisThirdCar
- Comments
```
	// Comentario de línea
	/* 
		Comentario de bloque
	*/ 
```
- Statements
	- Deben terminar en punto y coma (;)
	- Omitir el punto y coma puede ser válido pero NO recomendado pues le pone trabajo extra al parser, ya que el debe de "adivinar" en dónde debería ir el final de la sentencia.
	- Los bloques van dentro de corchetes { }

< noscript >
------------
- Se creo omo una alternativa para los navegadores que NO soportaban JS.
- Hoy en día se usa para cuando el usuario deshabilita JS en el navegador.
- Esta etiqueta puede contener cualquier etiqueta HTML dentro MENOS la etiqueta < script >
- El contenido de la etiqueta < noscript > se mostrará cuando:
	- El navegador NO soporte scripting
	- El navegador tenga el scripting desactivado.
- Si no se cumple alguna de las condiciones anteriores => no se rederiza el contenido del < noscript >

Variables
---------
- Inicialización
	- Cuando se quiere declarar una variable sin asignarle ningún valor se debe inicialiar = null.

		```
			//En este caso el valor null se comporta como un 0.
			var number1 = null;
			var number2 = number1*5; //number2 = 0
		```

	- Si no se le asigna ningún valor se declarará como undefined.

		```
			var number1;
			var number2 = number1*5; //number2 = NaN
		```

	- Si se comparan null y undefined los valores son iguales.
	- NO se puede usar una variable que NO ha sido declarada.

- Las variables en JS puede contener cualquier tipo de dato.

	```
		//Esta inicialización NO convierte la variable a un tipo string,
		// sólo le asigna un valor de tipo string
		var mensaje = "hola";
	```

- Es posible cambiar el valor almacenado en una variable pero TAMBIÉN EL TIPO DE DATO.

	```
		//La variable prueba primero contiene un strig y después
		//su valor se sobrescribe con un número
		var prueba = "hola";
		prueba = 100; //Es una asignación válida, pero NO RECOMENDADA
	```

- Alcance
	- Es la parte del programa dónde una variable puede ser accedida.
	- Se recomienda maneter el alcance las variables mínimo
	- Variables Globales
		- Declarada afuera de cualquier función o bloque.
		- Esta disponible para cualuier código en el documento donde fue declarada.
	- Variables locales
		- Cuando se define una variable (var) dentro de una función o bloque, ésta es destruida en cuanto la función termina.
- Se pueden definir varias variables en una sóla sentencia separándolas con comas (,). Esto aplica aún cuando las variables sean de diferente tipo.

Data Types
----------
- Existen 5 tipos simples en JS
	- Undefined
	- Null
	- Boolean
	- Number
	- String
- 1 tipo complejo de dato
	- Object: Una colección de otros tipos simples


Typeof Operator
---------------
- Provee información sobre el tipo de dato de una variable o valor.
- Este operador puede regresar alguno de los siguientes valores
	- "undefined": valor indfinido
	- "boolean": valor boleano
	- "number": valor numérico
	- "object": si el valor es un Objeto (no función) o Null
	- "function": si el valor es una función
- Al usar **typeof null** lo que se obtiene es "object" debido a que null es considerado un valor vacío para objetos.

Undefined Type
--------------
- Este tipo sólo tiene un valor, ese valor es "undefined"
- Este valor es asignado cuando se declara una variable utilizando la palabra reservada "var" pero no se le asigna algún valor a la nueva variable.

	```
	var test;
	alert(test==undefined); //true
	```

- Aunque por default las variables NO inicializadas = undefined, NUNCA se debe asignar directamente ese valor, ya que el propósito de undefined es diferenciar entre un valor vacío y una variable NO inicializada.
- Con una variable undefined sólo funciona el operador typeof.
- El operador typeof también regresará undefined cuando se use con una variable NO declarada.

	```
	var message;
	//var age is undeclared
	alert(typeof message); //"undefined"
	alert(typeof age); //"undefined"
	```

- Se recomienda SIEMPRE asignar valores cuando se declaran variables, de esta manera, si obtenemos un undefined sabremos que es porque se trata de una variable NO declarada.


Null Type
---------
- Este tipo sólo tiene un valor, ese valor es "null"
- Lógicamente, un valor null es el apuntador a un objeto vacío, es por eso que "typeof null" regresa "object";
	```
	var person = null;
	alert(typeof person); //"object"
	```
- Se puede usar este tipo de dato cuando estamos declarando una variable que más adelante contendrá un objeto, es preferible inicializarla como null a no inicializarla.
- Si inicializamos los objetos = null, entonces después podemos checar si el objeto ya fue llenado verificando si su valor es diferente de null.
- El valor undefined es un derivado de null.

**Nunca inicializar variables = undefined. Inicializar variables = null si esa variable contendrá un objeto**