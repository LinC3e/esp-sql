# SQL
1. [Conceptos y terminos de las bases de datos](#conceptos-y-términos-de-las-bases-de-datos-relacionales)
2. [Tipos de Datos](#tipos-de-datos)

## **Conceptos y términos de las Bases de Datos Relacionales.**

___

Las bases de datos relacionales intentan cumplir con todos los conceptos del Modelo Relacional, aunque no es
posible implementarlos todos
 
- Las tablas tienen nombre único dentro de un esquema.
- Los campos tienen un nombre único dentro de una tabla.
- Los valores de cada campo están restringidos por un tipo de dato.
- El valor nulo, se representa en SQL por el valor NULL.
- La integridad de la tabla y cada registro está garantizada por el SGBD
- La integridad referencial también está garantizada por el SGBD cuando se haya definido.

___
## **Tipos de Datos**
___
Los tipos de datos de una base de datos son similares a los de un lenguaje de programación. Su elección
dependerá de qué se quiere almacenar y para qué fin.

Una base de datos debe ser eficiente con el uso de la memoria de almacenamiento, por esto existen varios tipos
de datos diferentes para el mismo tipo general.

El tipo de dato de un campo deben definirse en el momento que se definen el campo. Esto puede ser cuando se
crea una tabla o cuando se la modifica

### **Numéricos:**
#### **1) Numericos Exactos**
___
> **INTEGER**: 
>>Sirven para almacenar números enteros exactos. La mayoría de las claves primarias usan alguno de estos
tipos. Pueden tener signo (signed) o no (unsigned), en tal caso los valores negativos se hacen positivos.

- **TINYINT**: *un entero muy pequeño, de rango -128 a 128. Sin signo, el rango es 0 a 255.*
-  **SMALLINT**: *un entero pequeño, de rango -32768 a 32767. Sin signo, el rango es 0 a 65535.*
-  **MEDIUMINT**: *un entero de tamaño mediano, de rango -8388608 a 8388607. Sin signo, el rango es 0 a 16777215.*
-  **INT o INTEGER**: *un entero normal, de rango -2147483648 a 2147483647. Sin signo, el rango es 0 a
4294967295.*
-  **BIGINT**: *Un entero grande, de rango -9223372036854775808 a 9223372036854775807. Sin signo, el rango es
0 a 18446744073709551615.*

> Un campo sin signo se marca con el atributo **UNSIGNED**.

> **DECIMAL y NUMERIC:** 
>>*Estos tipos de datos sirven para almacenar datos 
numéricos exactos con dígitos decimales, por ejemplo, para datos 
monetarios. Al declarar una columna de este tipo se deben indicar la 
cantidad total de dígitos almacenados, como así también la cantidad 
de dígitos almacenados después del punto decimal, por ejemplo: 
saldo DECIMAL(5, 2)*

#### **2) Aproximados:**
___
> **FLOAT y DOUBLE:** 
>>*Son usados para almacenar datos numéricos con 
decimales de una precisión de 4 bytes para precisión simple (FLOAT) 
y 8 bytes para precisión doble (DOUBLE). Estos tipos de datos sirven 
para almacenar datos siempre y cuando nos interese una precisión fija 
y resultados con cierto grado de tolerancia. Por ejemplo, simulaciones 
científicas, juegos, estadísticas, etc. Si necesitamos almacenar datos 
monetarios debemos usar DECIMAL.*

___

### **Cadenas:**
___
> **CHAR y VARCHAR:** 
>> - Son tipos similares y se declaran indicando, entre 
paréntesis, el tamaño en cantidad de caracteres que se quieren almacenar. 
Por ejemplo, definiendo el tipo CHAR(30), se pueden almacenar hasta 30 
caracteres. Los caracteres que sobrepasen el tamaño serán truncados 
silenciosamente. El tamaño declarado para un tipo CHAR es fijo, ya sea que se 
use todo o no. Si no se ocupa todo el espacio, se completará con espacios a 
la derecha. Por ejemplo, un campo declarado como CHAR(4) puede 
almacenar datos como: ‘hola’, ‘si’ y ‘1’. El tamaño máximo de un tipo CHAR
es de 255 caracteres. 
>>- Los campos declarados como VARCHAR son de tamaño variable, si almaceno 
la cadena ‘X’ en un campo declarado como VARCHAR(30), solo se 
almacenará ‘X’. Si la cadena es más larga, se truncará hasta el tamaño 
declarado. El tamaño máximo de un tipo VARCHAR está limitado solo por el 
máximo tamaño de un registro (65535 bytes, por defecto)

> **TEXT**: 
>> Contiene a los tipos TINYTEXT, TEXT, MEDIUMTEXT y LONGTEXT. Son 
tipos de datos para almacenar cadenas de caracteres grandes. Cada tipo varía 
en el tamaño máximo de caracteres que pueden almacenar

___
### **Fecha y hora:**
___
>**DATE**: 
>> Este tipo de dato se utiliza para almacenar datos de fecha. No incluyen 
datos de hora. MySQL recupera y muestra estos datos con el formato: **‘YYYY-MM-DD’**. El rango de valores es: desde ‘1000-01-01’ hasta ‘9999-12-31

> **DATETIME**: 
>> Se utiliza para datos que incluyen ambos fecha y hora. Estos datos 
se recuperan y muestran con el formato: **‘YYYY-MM-DD hh:mm:ss’** y el rango 
de valores posibles es: ‘1000-01-01 00:00:00’ hasta ‘9999-12-31 
23:59:59’.

> **TIMESTAMP**: 
>> También se usa para almacenar datos que incluyen fecha y hora. 
Su rango de valores posibles es desde ‘1970-01-01 00:00:01’ UTC a ‘2038-
01-19 03:14:07’ UTC. La diferencia con DATETIME es que la fecha y hora se 
almacena como UTC aunque el dato original esté en la zona horaria actual 
del sistema y, a su vez, cuando recuperan y muestran los datos, vuelve a 
convertir de UTC a la zona horaria del sistema.

Existen otros tipos de datos, como los tipos Espaciales, los cuales sirven para la generación, 
almacenamiento y análisis de características geográficas, o el tipo de dato JSON, pero no vamos a expandir a esos tipos de datos.