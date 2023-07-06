# <font color="yellow"><center>SQL</center></font>
1. [Conceptos y terminos de las bases de datos](#conceptos-y-términos-de-las-bases-de-datos-relacionales)
2. [Tipos de Datos](#tipos-de-datos)
3. [Sentencias](#sentencias)
4. [Lenguaje de Definición de Datos](#lenguaje-de-definición-de-datos)
5. [Lenguaje de Manipulacion de Datos](#lenguaje-de-manipulación-de-datos)
6. [Lenguaje de Consulta de Datos](#lenguaje-de-consulta-de-datos)
7. [Funciones](#funciones)

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

### <font color="orange"><ins>**ALTER TABLE**</ins></font>
Permite modificar la definición de una tabla, agregando, modificando o eliminando columnas o restricciones

```
Sintaxis: 
         ALTER TABLE nombre_tabla <accion>;
```

Las acciones que podemos usar son:
- **RENAME nuevo_nombre**: cambiar el nombre de la tabla.
- **ADD nueva_columna definicion**: agregar una columna a la tabla.
- **DROP columna**: eliminar una columna.
- **MODIFY columna definicion**: cambiar la definicion de una columna.
- **CHANGE columna nuevo_nombre definicion**: cambiar el nombre y definicion de una columna.

Por ejemplo: 

Si quisiéramos agregarle una columna más, de **año** de estreno, a la tabla peliculas, podemos usar:

```
ALTER TABLE peliculas ADD año SMALLINT;
```

> Si la tabla ya contenía registros, se insertará el valor NULL en la nueva columna creada para todos esos registros
A menos que se defina un valor por defecto con el atributo DEFAULT al momento de agregar la columna. En tal caso, se insertará el valor indicado

Por ejemplo .2:

Si quisiéramos modificar una columna existente, por ejemplo, cambiando el tipo de dato:
```
ALTER TABLE peliculas MODIFY año INT;
```
> Si la tabla ya contenía registros, se intentará castear los valores de ese campo al nuevo tipo. Si no se puede hacer la
sentencia dará un error.

>Si la columna original tenía valores CHAR solo se podrá castear a INT, por ejemplo, si contiene valores
correspondientes a números enteros dentro del rango de INT.

> Si contiene valores fuera del rango, o alfabéticos, no se podrá completar la modificación.
Finalmente, también se pueden agregar restricciones de clave foránea

### <font color="orange"><ins>**DROP TABLE**</ins></font>
Elimina la tabla indicada de la base de datos.
```
Sintaxis: 
         DROP TABLE tabla;
```
> Si existen referencias a la tabla no podremos eliminarla sin antes eliminar las restricciones de clave foránea.

### <font color="orange"><ins>**TRUNCATE**</ins></font>
Elimina todos los registros de la tabla indicada
```
Sintaxis:
         TRUNCATE tabla;
```
> Existe la misma restricción que en la sentencia anterior

### <font color="orange"><ins>**Restricción de clave foránea – FOREIGN KEY**</ins></font>
Vamos a ver que no hace falta que exista la restricción de clave foránea para referenciar o unir dos o más tablas.

Sin embargo, si queremos que el SGBD mantenga la integridad referencial de la base de datos, debemos definir restricciones de clave foránea

Usualmente se usan solo claves primarias simples (de una sola columna), por lo tanto, las claves foráneas también son simples.

También se puede definir una restricción de clave foránea usando ALTER TABLE.

Por ejemplo:

Si quisiéramos definir una restricción de clave foránea sobre nuestra tabla peliculas, que haría referencia a una hipotética tabla directores (que debe existir de antemano) podríamos haberla definido de la siguiente manera:
```
CREATE TABLE peliculas (
        id_pelicula INT NOT NULL AUTO_INCREMENT UNIQUE,
        titulo VARCHAR(150) NOT NULL,
        duracion SMALLINT UNSIGNED NOT NULL,
        director SMALLINT UNSIGNED NOT NULL,
        CONSTRAINT directores_fk FOREIGN KEY (director)
        REFERENCES directores (id_director)
);
```

Es posible definir qué debe suceder cuando se elimina un registro o actualiza el valor de una clave primaria a la cuál hace referencia un registro de otra tabla, con las subcláusulas ON DELETE y ON UPDATE.

- **ON DELETE accion**: indica que se debe tomar una acción en el momento en que se elimine un registro en la tabla padre.

- **ON UPDATE accion**: se refiere al momento en que se actualice el valor de la clave primaria de un registro de la tabla padre (no otro campo cualquiera).

> Estas acciones se establecen para que se ejecuten automáticamente en el momento en que se cumple alguno de los requisitos definidos

Ambas subcláusulas, ON DELETE y ON UPDATE, soportan las siguientes acciones:

- **CASCADE**: en caso que se actualice (ON UPDATE) o elimine (ON DELETE) una fila de la tabla padre, automáticamente actualiza o elimina las filas correspondientes en la tabla hija.

- **SET NULL**:  en caso que se actualice o elimine una fila de la tabla padre, automáticamente pone en NULL las filas correspondientes de la tabla hija. La columna que actúa como clave foránea no debe tener el atributo NOT NULL.

- **RESTRICT**: rechaza la acción que se quiere realizar en la tabla padre. Es equivalente a no incluir la cláusula ON DELETE o ON UPDATE.

- **NO ACTION**: es una palabra reservada del estándar SQL y en tablas InnoDB es equivalente a RESTRICT.

- **SET DEFAULT**: es una palabra reservada por MySQL, pero no se puede usar en tablas InnoDB. Por lo tanto, no está recomendado su uso.

Por ejemplo, si implementamos la subcláusula ON DELETE en la definición anterior:

```
CREATE TABLE peliculas (
        id_pelicula INT NOT NULL AUTO_INCREMENT UNIQUE,
        titulo VARCHAR(150) NOT NULL,
        duracion SMALLINT UNSIGNED NOT NULL,
        director SMALLINT UNSIGNED NOT NULL,
        CONSTRAINT directores_fk FOREIGN KEY (director)
        REFERENCES directores (id_director)
        ON DELETE CASCADE
);

```
En este caso elegimos la acción CASCADE, esto quiere decir que, si en algún momento se elimina el registro de un director, todas las filas correspondientes a sus películas también serán eliminadas.

Esto es un poco drástico, ya que, en este caso hipotético, perderíamos los registros de las películas.

Dicho esto, sería mucho mejor usar la acción SET NULL, de esta forma no perderíamos los registros de las películas,
solo quedarían sin referencia y es posible, posteriormente, volver a referenciar al director (si se vuelven a cargar sus datos)

### <font color="orange"><ins>**Indices**</ins></font>
Un índice es, básicamente, una tabla (independiente) ordenada de los valores de algún campo de una tabla, con un puntero a la posición real del registro de esos valores. Esta estructura permite realizar operaciones de obtención de datos mucho más rápido, sacrificando espacio de almacenamiento (ya que se copian los valores del campo) ytiempo para la gestión del índice mismo.

![Ejemplo grafico de indices](/images/indices.JPG)

Ejemplo de un índice (i_titulo) sobre el campo título de la tabla peliculas. El índice mantiene el orden alfabético de los títulos de las películas y una referencia a la fila original. Al estar ordenado, la búsqueda es más rápida

Al estar ordenado, un índice permite al SGBD usar algoritmos de búsqueda binaria para encontrar un elemento más rápido que una búsqueda secuencial, como debería hacerlo si no existiera el índice.

- Los índices son manejados por el SGBD automáticamente en segundo plano, tanto en su uso para búsquedas, como en su mantenimiento.

- Algunos se crean automáticamente por el SGBD. Como por ejemplo: claves primarias, claves foráneas, campos únicos, etc., todos tienen un índice asociado.

- Un usuario puede crear un índice manualmente, sobre un campo que considere necesario, usando la sintaxis:

```
        CREATE INDEX nombre_indice ON tabla (col1);
```

___

## **Lenguaje de Manipulación de Datos**
___

### <font color="orange"><ins>**INSERT**</ins></font>

Carga uno o varios registros nuevos en una tabla de la base de datos en una misma operación.

```
Sintaxis: 
         INSERT INTO tabla (col1, col2) VALUES (val1, val2);
```
> Donde tabla es la tabla en la cual queremos insertar los datos, col1 y col2 son las columnas en las que queremos
insertar los valores val1 y val2

- Si omitimos nombrar una columna, esta tomará un valor por defecto.

- No hace falta pasar un valor para un campo definido como AUTO_INCREMENT .

- Si se van a insertar valores para todas las columnas de la tabla no hace falta nombrarlas antes, pero es buena práctica hacerlo siempre. Por ejemplo:

INSERT INTO peliculas (titulo, duracion, año)
VALUES ('Metegol', 106, 2013);

Para insertar varios registros en una sola sentencia podemos usar la siguiente sintaxis:

```
INSERT INTO tabla (col1, col2)
VALUES (val1, val2), (val3, val4), (val5, val6);
```

```
Por ejemplo
           INSERT INTO peliculas (titulo, duracion, año)
           VALUES ('El secreto de sus ojos', 129, 2009),
           ('Nueve Reinas', 115, 2000),
           ('Esperando la carroza', 96, 1989);
```

### <font color="orange"><ins>**UPDATE**</ins></font>
Modifica los valores de los campos y registros especificados.
```
Sintaxis:
         UPDATE tabla SET campo = valor [WHERE <condicion>];
```
> Con esta sentencia indicamos, primero, el nombre de la tabla a modificar, y luego, seguido de la palabra reservada SET, los campos, asignándoles un valor con el operador de asignación =. Se puede modificar más de un campo indicando las asignaciones separadas por comas

- La sentencia UPDATE tiene la capacidad de modificar los campos indicados de todas las filas de una tabla dada.

-  Admite la cláusula opcional WHERE, la cual brinda la posibilidad de filtrar los campos que van a ser afectados.

- Si no usamos WHERE, la sentencia UPDATE afectaría los campos indicados de todos los registros de la tabla.

- El uso de WHERE implica que debemos conocer la tabla de antemano, para saber como realizar el filtro.

> Dentro de una cláusula WHERE, el símbolo = es un operador de comparación, por lo tanto, sirve para crear condiciones lógicas. Por otro lado, después de un SET de una sentencia UPDATE , = funciona como operador de asignación, y el valor se asigna al campo indicado


*Por ejemplo, digamos que queremos modificar el campo año del registro de la película ‘Esperando la carroza’ que
insertamos erróneamente como 1989 por el correcto, 1985. Podemos intentar usar la siguiente sentencia:*

```
Sentencia peligrosa:

UPDATE peliculas SET año = 1985;

Si ejecutamos esta sentencia, el campo año de todos los registros se modificaría a 1985.

Sentencia correcta:

UPDATE peliculas SET año = 1985 WHERE id_pelicula = 4;

Debemos identificar unívocamente el registro que queremos modificar. La mejor forma es usando su clave primaria:

```
> No siempre vamos a querer modificar solo un registro de una tabla. A veces es necesario modificar varios registros que cumplan cierta condición. En tal caso, debemos diseñar una condición adecuada en la cláusula WHERE. Por ejemplo:

*Digamos que queremos modificar el campo tipo de una hipotética tabla cuentas_bancarias al valor “vip” solo para las cuentas que superen los $10.000 000 de saldo. En tal caso deberíamos ejecutar una sentencia como la siguiente:*

`
UPDATE cuentas_bancarias SET tipo = “vip” WHERE saldo > 10000000;
`

### <font color="orange"><ins>**DELETE**</ins></font>

Elimina uno o más registros de una tabla. De manera similar a UPDATE, solo permite indicar de qué tabla se tienen que eliminar los registros, por tal motivo, también admite una cláusula WHERE para filtrar los registros a eliminar.

```
Sintaxis:
         DELETE FROM tabla WHERE <condicion>;
```
> Ejecutar un **DELETE** sobre una tabla X, sin cláusula **WHERE** es equivalente a ejecutar **TRUNCATE** X. En otras palabras, ambas sentencias eliminan todos los registros de la tabla.

Al igual que en el ejemplo con UPDATE, lo mejor es indicar un registro por su clave primaria.

Por ejemplo:

*Digamos que queremos eliminar el registro de la película ‘Duro de matar’ por algún motivo. La sentencia debería ser:*

`
DELETE FROM peliculas WHERE id_pelicula = 1;
`

___
## **Lenguaje de Consulta de Datos**
___
Permite consultar registros de la base de datos que satisfagan un criterio determinado.

**SELECT** es la única sentencia de este sub-lenguaje, pero por su complejidad usualmente se la separa en su propio sub-lenguaje.

- Permite distintos tipos de filtros.

- Permite ordenamientos y agrupamientos de registros.

- Permite limitar la cantidad de registros devueltos 

- Permite obtener datos de una o más tablas, uniéndolas.

> Generalmente se suele llamar a esta sentencia *consulta*

```
Su sintaxis (simplificada):
SELECT <expresion_seleccion> FROM <referencia_tabla>
        WHERE <condicion>
        GROUP BY columna
        ORDER BY columna
        LIMIT cant;
```

### **<font color="pink"><ins>Expresión de selección</ins></font>**

Lo que nombramos como <expresion_seleccion> es el espacio en donde se deben indicar qué campos queremos obtener en la consulta.

Por ejemplo:

`
SELECT * FROM tabla;
`
> El carácter * como expresión de selección, este carácter es un comodín en SQL e indica que se van a solicitar todos los campos de la tabla.

Podemos indicar una o dos columnas si lo deseamos, por ejemplo:

`
SELECT titulo, año FROM peliculas;
`

Nos devolverá una lista de todos los títulos de todas las películas y sus respectivos años de estreno. O, de la forma en que está diseñada la tabla.

También existen diferentes funciones predefinidas que podemos usar en la expresión de selección. Por ahora, solo veremos una que es muy útil:

- COUNT(col): devuelve la cantidad de registros que se encontraron en determinada 
consulta. La forma correcta de usar esta función para obtener la cantidad de 
registros es usando el comodín * como parámetro. Por ejemplo:

`
SELECT COUNT(*) FROM peliculas;
`

### **<font color="pink"><ins>**WHERE**</ins></font>**
Esta cláusula impone una condición lógica sobre los registros que se van a recuperar de la base de datos. Los registros para los que la condición evalúe a verdadero serán devueltos y los que no, serán ignorados.

#### **Operadores lógicos**
- **AND** - Devuelve uno o más registros si ambos operandos son verdaderos.

- **OR** - Devuelve uno o más registros si al menos uno de los operandos es verdadero.

- **NOT** - Devuelve uno o más registros si la condición devuelve falso.

- **campo1 BETWEEN valor1 AND valor2** - Devuelve uno o más registros si el valor del campo indicado está entre los dos valores

Por ejemplo:

`
SELECT * FROM películas
WHERE duracion > 100 AND duracion < 120;
`

o usando BETWEEN:

`
SELECT * FROM películas
WHERE duracion BETWEEN 100 AND 120;
`

#### **LIKE**
Este operador permite filtrar registros basado en la coincidencia de patrones Permite la definición de patrones textuales y devuelve los registros que cumplen con dicho patrón

`
SELECT <campos> FROM tabla WHERE campo LIKE <patron>;
`

Por ejemplo:

`
SELECT nombre FROM directores
WHERE nombre LIKE 'Juan José Campanella';
`

Esta consulta devolverá los registros de la tabla directores cuyo nombre sea la cadena ‘Juan José Campanella’. Es decir, sería lo mismo que usar el operador =, iguala el valor exacto de la cadena

Si no queremos que solo encuentre cadenas exactas, debemos usar comodines.
Existen dos comodines que se pueden usar para definir patrones con **LIKE**, ellos son:

- % representa ninguno, uno o múltiples caracteres

- _  representa solo un carácter.

Por ejemplo

`
SELECT nombre FROM directores
WHERE nombre LIKE ‘Juan Jos_ Campanella’;
`

Encontrará a directores con los nombres ‘Juan José Campanella’, y también a nombres erróneamente almacenados como ‘Juan Josr Campanella`

Por otro lado:

`
SELECT nombre FROM directores WHERE nombre LIKE 'Juan%';
`

Encontrará a directores cuyos nombres comiencen con la cadena ‘Juan’ y terminen con cualquier combinación de caracteres.

Pueden ser: ‘Juan José Campanella’, ‘Juan Perez’ o ‘Juan Martínez’, ya que todos comienzan con ‘Juan’

Inclusive podemos combinar dos búsquedas mutuamente excluyentes con el operador **AND**

Pj: 

`SELECT nombre FROM directores`

`WHERE nombre LIKE 'Juan%' AND nombre LIKE '%lla';`

> Encontrará a directores cuyo nombre comience con la cadena ‘Juan’ y termine con la cadena ‘lla’. Por lo tanto, encontrará, por ejemplo, a directores con nombre‘Juan José Campanella’, ‘Juan Padilla’, ‘Juan Mansilla’, etc.

### **<font color="pink"><ins>**GROUP BY**</ins></font>**
Esta cláusula sirve para agrupar registros que tienen el mismo valor en cierto campo (llamado campo de agrupación). Normalmente es usada con alguna función de agregación, como la antes vista COUNT() u otras como SUM() o AVG().

```
Sintaxis;
         SELECT FUNCION(), col1, ... FROM tabla GROUP BY col1;
```
Por ejemplo, podríamos hacer una consulta para obtener la cantidad de películas que fueron dirigidas por el mismo director, ya que sabemos que el director (su id) se repite en la tabla peliculas.

```
SELECT director, COUNT(*) AS cantidad FROM películas
GROUP BY director;
```
Como vemos, incluimos el campo director en la expresión de selección ya que estamos utilizando el GROUP BY sobre ese campo. Si no lo incluimos MySQL usualmente puede devolver datos, pero en general esto no es lo correcto. Además, no sabríamos a qué director corresponde qué cantidad.

En este último ejemplo usamos un alias, con la palabra reservada AS, como nombre del 
campo temporario donde se suman las cantidades de películas. El result-set tendrá 
entonces, dos campos, director y cantidad. También podemos volver a usar el alias 
dentro de la consulta en lugar de lo que representa.

### **<font color="pink"><ins>**ORDER BY**</ins></font>**
Esta cláusula sirve para ordenar el result-set de una consulta por algún campo.
- **El orden puede ser ascendente o descendente, dependiendo de los modificadores ASC o DESC respectivamente.**

- **El valor de orden por defecto es ASC (ascendente).**

- **Si el campo es de tipo cadena de texto, se ordenará según su orden alfabético.**

- **Si el campo es del tipo fecha se ordenará cronológicamente.**

- **No es necesario que la columna por la que se ordena este presente en la expresión de selección.**

```
Sintaxis: 
         SELECT col1, col2, ... FROM tabla ORDER BY col_X;
```

*Por ejemplo, con una base de datos cine, si queremos los datos de las películas ordenadas alfabéticamente ascendentemente (de menor a mayor) por título, podemos ejecutar la siguiente consulta.*

`SELECT titulo FROM peliculas ORDER BY titulo;`

*O, si queremos los datos de las películas ordenadas descendentemente (de mayor a menor) por duración.*

`SELECT titulo, duracion FROM peliculas ORDER BY duracion DESC;`

### **<font color="pink"><ins>**LIMIT**</ins></font>**

Esta cláusula simplemente limita la cantidad de registros devueltos en una consulta a un número entero. Siempre debe ir al final de una sentencia SELECT.

```
Sintaxis: 
         SELECT campos... FROM tabla LIMIT <numero entero>;
```
*Por ejemplo, si queremos obtener solo los 10 países con mayor superficie, de la base de datos world:*

`SELECT Name, SurfaceArea
FROM country
ORDER BY SurfaceArea DESC
LIMIT 10;`

*Por ejemplo, si queremos obtener un ranking de los primeros 5 países que tienen más ciudades registradas en la base de datos de clientes de sakila, podemos hacer:*

`
SELECT country_id, COUNT(*) AS cantidad FROM city
GROUP BY country_id
ORDER BY cantidad DESC
LIMIT 5;
`

### **<font color="pink"><ins>**JOIN**</ins></font>**

Esta cláusula se usa para obtener datos de dos o más tablas. Forma parte de la cláusula FROM, ya que esta indica de qué tabla o tablas queremos obtener los datos.Las tablas a unir usualmente están relacionadas por una clave foránea y la unión se hace sobre esa clave. Pero esto no es necesario, ya que se pueden ejecutar uniones sobre cualesquiera dos campos, mientras que sean del mismo tipo y rango.Cada unión, se realiza entre dos tablas. Si se quieren relacionar más tablas se deben incluir más cláusulas JOIN. Existen cuatro tipos de uniones (en MySQL)

- INNER JOIN

- RIGHT JOIN

- LEFT JOIN

- CROSSJOIN

#### **INNER JOIN**
Selecciona registros que tienen valores coincidentes en ambas tablas.
Si un valor existe solo en una de las tablas no figurará en el resultado.

```
Sintaxis:
         SELECT tabla1.campo1, tabla2.campo1, ...
         FROM tabla1
         INNER JOIN tabla2 ON tabla1.campoX = tabla2.campoY
```

![Ejemplo grafico de INNER JOIN](/images/inner.JPG)

> En este ejemplo, se seleccionan todos los registros, de ambas tablas 
(tabla1 y tabla2), en los que los campos tabla1.campoX y tabla2.campoY coincidan.

> De esos registros se mostrarán los campos indicados (tabla1.campo1
y tabla2.campo1).

- Se recomienda usar nombres de campos calificados para evitar ambigüedades, ya que, al unir dos tablas, estas pueden tener el columnas con el mismo nombre.

- Solo se obtendrán registros para los cuales los valores de sus campos coincidan.

- Los campos mostrados pueden ser cualquiera de las tablas que se están uniendo.

- Los campos que se igualan indican qué registros se deben obtener.

- La expresión de selección indica cuales campos, de los registros obtenidos, queremos mostrar como result-set.


*Por ejemplo, usando la base de datos world: Queremos obtener el nombre del país al que pertenece la ciudad ‘Amsterdam’.*

```
SELECT country.Name, city.Name
FROM city INNER JOIN country
ON city.CountryCode = country.Code
WHERE city.Name = "Amsterdam";
```

> **Uniendo tres tablas a la vez**

```
Sintaxis:
        SELECT tabla1.campo1, tabla2.campo3, ...
        FROM ((tabla1
        INNER JOIN tabla2
        ON tabla1.campoX = tabla2.campoY)
        INNER JOIN tabla3
        ON tabla1.campoZ = tabla3.campoT)
```

#### **LEFT JOIN**
Devuelve todos los registros de la tabla de la izquierda (la que se nombra primero) y solo los registros que coincidan de la tabla de la
derecha (la que se nombra segunda). Si no existe ninguna coincidencia no se obtendrá ningún registro de la tabla derecha.

```
Sintaxis: 
         SELECT tabla1.campo1, tabla2.campo1, ...
         FROM tabla1 LEFT JOIN tabla2
         ON tabla1.campoX = tabla2.campoY;
```

![Ejemplo grafico de INNER JOIN](/images/left-join.JPG)

*Usando las tablas de nuestra base de datos cine, digamos que tenemos los siguientes datos cargados:*

![Ejemplo grafico de INNER JOIN](/images/ej-left-join.JPG)

Y queremos obtener todos los directores, y las películas que dirigieron, si es que tienen registros.

Tendremos que realizar un LEFT JOIN tomando como tabla izquierda,directores, ya que queremos si o si todos los directores.

```
SELECT directores.nombre, peliculas.titulo
FROM directores LEFT JOIN peliculas
ON directores.id_director = peliculas.director;
```

![Ejemplo grafico de INNER JOIN](/images/res-left-join.JPG)

> Podemos observar dos cosas, primero, que, ya que ‘Juan José Campanella’ tenía 2 películas, figuran sus 2 registros.
Y segundo, ‘Andy Muschietti’ no tiene ninguna película registrada, sin embargo, ya que estamos usando LEFT JOIN este debe figurar, aunque tenga el valor NULL


#### **RIGHT JOIN**
Esta sentencia es equivalente a la anterior, pero le da prioridad a la tabla de la derecha. Funcionalmente es idéntica a la anterior.

En otras palabras, se puede obtener el mismo resultado que obtiene LEFT JOIN si invirtiéramos el orden en que se nombran las tablas.

```
Sintaxis: 
         SELECT tabla1.campo1, tabla2.campo1, ...
         FROM tabla1
         RIGHT JOIN tabla2
         ON tabla1.campoX = tabla2.campoY;
```

![Ejemplo grafico de INNER JOIN](/images/right-join.JPG)


#### **CROSS JOIN**
Devuelve todos los registros de ambas tablas como producto cartesiano, es decir, todos los registros de una tabla en relación con todos los registros de la otra tabla.

Esta consulta no utiliza la cláusula ON ya que siempre devuelve el producto cartesiano de los registros

```
Sintaxis:
         SELECT tabla1.campo1, tabla2.campo1, ...
         FROM tabla1
         CROSS JOIN tabla2;
```

![Ejemplo grafico de INNER JOIN](/images/cross-join.JPG)

> Esta cláusula es específica de MySQL. Y el diagrama de Venn no
representa exactamente su funcionalidad, ya que son muchos más
registros los que devuelve.

*Por ejemplo, si realizamos un CROSS JOIN entre nuestras tablas
peliculas y directores, obtendremos un result-set de 16
registros de todos las películas combinadas con todos los directores.
Lo cual no tiene mucho sentido.*

`
SELECT directores.nombre, peliculas.tituloFROM peliculas CROSS JOIN directores;
`

![Ejemplo grafico de INNER JOIN](/images/cross-join-ej.JPG)

> Sin embargo, hay veces en que se necesitan obtener todas las
combinaciones de dos elementos (representados por tablas), en las
cuales es de utilidad

___
## **Funciones**
___
Ya vimos algunas funciones de MySQL. Algunas de agregación, especialmente útiles para su uso con GROUP BY.
Algunas que devuelven valores del sistema operativo, como las de fecha y hora.

Vamos a ver algunas de ellas clasificadas en estos grupos: 

- De agregacion.

- Numéricas y matemáticas

- Operaciones con cadenas

- Fecha y hora

### **De agregacion**

| Sintaxis   | Descripcion |
| -----------| ----------- |
| COUNT(col) | devuelve la cantidad de registros encontrados.|
| MAX(col)   | devuelve el valor máximo de la columna indicada dentro de un resultado |
| MIN(col)   | devuelve el valor mínimo de la columna indicada dentro de un result-set.|
| AVG(col)   | devuelve el promedio (average) de los valores de una columna específica. La columna debe ser de algún tipo numérico para permitir el cálculo.|
| SUM(col)   |  devuelve la suma de los valores de una columna específica. La columna debe ser de algún tipo numérico para permitir el cálculo.|

### **Numéricas y matemáticas**

| Sintaxis   | Descripcion |
| -----------| ----------- |
| ABS(x)     | devuelve el valor absoluto de un valor x pasado como parámetro.|
| PI()       | devuelve el valor de pi, hasta 7 decimales. |
| ROUND(x)   | devuelve el valor de x redondeado.|
| MOD(x, y)  | devuelve el resto de la división de x con y.|
| POW(x, y)  | devuelve el valor de x elevado a la y |
| SQRT(x)    | devuelve la raíz cuadrada de x.|

### **Cadenas**

| Sintaxis   | Descripcion |
| -----------| ----------- |
|CONCAT(str1, str2, ...) |  devuelve una cadena que concatena todas las cadenas pasadas por parámetro.|
| LOWER(str) | devuelve la cadena pasada como parámetro en minúsculas. |
| UPPER(str)  | devuelve la cadena pasada como parámetro en mayúsculas.|
| REVERSE(str) | devuelve la cadena con los caracteres ordenados al revés.|

### **Fecha y Hora**

| Sintaxis   | Descripcion |
| -----------| ----------- |
| CURDATE()  | devuelve la fecha actual en el formato “YYYY-MM-DD”. |
| CURTIME()  | devuelve la hora actual en el formato: “HH-MM-SS”.|
| NOW()      | devuelve la fecha y la hora actuales en el formato “YYYY-MM-DD HH-MM-SS"|
| EXTRACT()  | extraer una parte de una fecha-hora. La parte debe ser especificada con las palabras reservadas: MICROSECOND, SECOND, MINUTE, HOUR, DAY, WEEK, MONTH, QUARTER, YEAR, entre otras. |

> Los valores que devuelven las funciones pueden ser usados para establecer valores por 
defecto para columnas de una tabla, para insertar o actualizar alguna columna de un 
registro, o para devolverlos al usuario.
Estas solo son algunas de las funciones disponibles en MySQL. Podemos encontrar el listado 
completo de funciones en la documentación oficial de MySQL.
