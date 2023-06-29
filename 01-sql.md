# <font color="yellow"><center>SQL</center></font>
1. [Conceptos y terminos de las bases de datos](#conceptos-y-términos-de-las-bases-de-datos-relacionales)
2. [Tipos de Datos](#tipos-de-datos)
3. [Sentencias](#sentencias)
4. [Lenguaje de Definición de Datos](#lenguaje-de-definición-de-datos)

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
___
## **Sentencias**
___
SQL se divide en varios componentes o sub-lenguajes. Nos centraremos en los tres primeros 
de los siguientes:

1. Lenguaje de Definición de Datos (DDL): permite crear, definir, modificar y eliminar 
nuevas bases de datos, tablas, campos e índices (y otros elementos).

2. Lenguaje de Manipulación de Datos (DML): son las sentencias que permiten insertar 
datos en las tablas, consultarlos, modificarlos y borrarlos.

3. Lenguaje de Consulta de Datos (DQL): permiten generar consultas para ordenar, 
filtrar y extraer datos de la base de datos.

4. Lenguaje de Control de Datos (DCL): permite controlar el acceso a los datos 
mediante un sistema de permisos sobre los usuarios. En MySQL, estas y otras 
sentencias se clasifican como Sentencias de Administración de Cuentas.

5. Lenguaje de Control de Transacciones (TCL): permite manejar conjuntos de 
sentencias en una sola unidad de ejecución, llamada transacción.

### **Sintaxis de SQL**

Debemos señalar que SQL no distingue entre mayúsculas y minúsculas, por lo tanto, las 
palabras reservadas pueden escribirse de cualquier forma. Los nombres de las bases de 
datos, como los de tablas es recomendable escribirlos de la misma forma en que se crearon

Dicho esto, en esta teoría vamos a usar mayúsculas para las palabras reservadas de SQL, 
como **CREATE, SELECT, DELETE,** etc. y minúsculas para nombres de bases de datos, tablas, 
campos, etc.

Los espacios en blanco no son significantes en la sintaxis, incluyendo los saltos de línea, por 
lo que podemos organizar y separar sentencias largas en varias líneas para mejorar la 
escritura y lectura de las mismas, las cuales pueden llegar a ser muy complejas.

Las cadenas de caracteres literales se pueden escribir encerradas entre comillas simples (') 
o dobles (").

También se pueden escribir comentarios en SQL, y hay varias formas de hacerlo. Un 
comentario de una línea se interpreta desde los caracteres -- hasta el final de la línea, 
siempre dejando un espacio después de los guiones. MySQL lo soporta y también 
implementa sus propios comentarios de una línea, comenzando con el símbolo #.
Por otro lado, también se soportan cometarios multilínea con los pares de caracteres de 
inicio y fin /* y */

```
# este es un comentario unicamente en MySQL

-- este es un comentario en una linea de SQL estándar

/* este es un
Comentario
multilinea estandar*/
```

MySQL soporta distintos operadores: 

- De asignación: **=**
- Aritméticos: **+, -, *, /, %.**
- De comparación: **=, >, <, >=, <=, <>**
- Lógicos: **AND, OR, ALL, ANY, BETWEEN, EXISTS, IN, LIKE, NOT, SOME.**

___
## **Lenguaje de Definición de Datos**
___

Dentro de este sub-lenguaje se clasifican las sentencias que nos permitirán crear y definir nuevas bases de datos, tablas, campos e índices. Vamos a ver los más importantes y su sintaxis.


### <font color="orange"><ins>**CREATE DATABASE**</ins></font>
Crea una nueva base de datos o esquema vacío con el nombre indicado. Es posible también 
indicar opciones adicionales que incluyen: colación y conjunto de caracteres, y 
encriptación. Se puede usar la palabra reservada SCHEMA en lugar de DATABASE. 

```
Sintaxis: 
         CREATE DATABASE nombre_bd;

Ejemplo:
        CREATE DATABASE cine;
```

### <font color="orange"><ins>**CREATE TABLE**</ins></font>
Crea una tabla en la base de datos que está en uso en ese momento. Donde definiciones debe ser la definición de
al menos un campo.
Cada definición de la tabla debe escribirse separada por una coma (,). Estas definiciones pueden ser capos, índices,
restricciones de clave primaria y foránea, etc. Por ejemplo, siguiendo con el ejemplo de la base de datos cine:

```
Sintaxis: 
         CREATE TABLE nombre_tabla (definiciones);

Ejemplo:
        CREATE TABLE peliculas (
            id_pelicula INT NOT NULL AUTO_INCREMENT UNIQUE PRIMARY KEY,
            titulo VARCHAR(150) NOT NULL,
            duracion SMALLINT UNSIGNED NOT NULL
        )

Ejemplo 2: 
        CREATE TABLE peliculas (
            id_pelicula INT NOT NULL AUTO_INCREMENT UNIQUE,
            titulo VARCHAR(150) NOT NULL,
            duracion SMALLINT UNSIGNED NOT NULL
            PRIMARY KEY (id_pelicula)
        ) 
```

En esta simple definición, creamos una nueva tabla con el nombre películas y los campos:

- **id_pelicula**: como entero, clave primaria, no nulo, único y auto incrementable.
-  **titulo**: como una cadena de hasta 150 caracteres que no puede ser nulo.
- **duracion**: como un entero pequeño, sin signo y no nulo, ya que vamos a indicar los minutos de la película con un
entero.

Los modificadores que agregamos a cada tipo de dato se conocen como atributos. Para el primer campo incluimos
los siguientes: **NOT NULL AUTO_INCREMENT UNIQUE PRIMARY KEY.**

- **NOT NULL**: indica que el campo no puede ser nulo nunca.
- **AUTO_INCREMENT**: indica que sus valores se van a insertar automáticamente por el SGBD aumentando en 1 cada
vez.
- **UNIQUE**: indica que el campo debe ser único para todos los registros.
- **PRIMARY KEY**: indica que definimos como clave primaria al campo.

