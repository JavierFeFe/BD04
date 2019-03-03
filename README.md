# BD04
Tarea para BD04.
Detalles de la tarea de esta unidad.
Enunciado.
La empresa El Desván, que se dedica a la rama textil ha decidido informatizar su gestión de nóminas. Para ello BK programación desarrollará para ellos la base de datos.

El gerente le ha explicado como funciona la gestión de nóminas y Juan, que será quien se encargue de crear el modelo, las tablas y las consultas, ha recogido la siguiente información:

A cada empleado se le entrega un justificante de nómina al mes. De cada empleado registraremos su código de empleado, nombre, apellidos, número de hijos, cuenta corriente y porcentaje de retención para Hacienda.
Un empleado puede trabajar en varios Departamentos y en cada uno de ellos realizará una función.
De un Departamento mantenemos el nombre del mismo y un código de Departamento.
Los datos de un justificante de nómina son el ingreso total percibido por el empleado y el descuento total aplicado.
La distinción entre dos justificantes de nómina se hace, además de mediante el código de empleado, mediante el ejercicio fiscal y número de mes al que pertenece.
Cada justificante de nómina consta de varias líneas y cada línea se identifica por un número de línea del correspondiente justificante. Una línea puede corresponder a un ingreso o a un descuento. En ambos casos se recoge la cantidad (positiva o negativa). En el caso de los descuentos se recoge la base y el porcentaje.
Con todos estos datos ha llegado al siguiente modelo entidad-relación:

Modelo entidad-relación que describe las relaciones entre las distintas tablas que se necesitan para la tarea.
También ha creado las bases y ha insertado algunos datos para realizar pruebas de las consultas que haga.

Todo está listo para que le ayudes. Estas son las consultas que debes crear:

Código y nombre de todos los departamentos.
Mes y ejercicio de los justificantes de nómina pertenecientes al empleado cuyo código es 1.
Número de cuenta y nombre de los empleados cuya retención es mayor o igual que 10.
Código y nombre de los empleados ordenados ascendentemente por nombre.
Nombre de los empleados que tienen más de 2 hijos.
Código y número de cuenta de los empleados cuyo nombre empieze por 'A' o por 'J'.
Número de empleados que hay en la base de datos.
Nombre del primer y último empleado en términos alfabéticos.
Nombre y número de hijos de los empleados cuya retención es: 8, 10 o 12.
Número de hijos y número de empleados agrupados por hijos, mostrando sólo los grupos cuyo número de empleados sea mayor que 1.
Número de hijos, retención máxima, mínima y media de los empleados agrupados por hijos.
Nombre y función de los empleados que han trabajado en el departamento 1.
Nombre del empleado, nombre del departamento y función que han realizado de los empleados que tienen 1 hijo.
Nombre del empleado y nombre del departamento en el que han trabajado empleados que no tienen hijos.
Nombre del empleado, mes y ejercicio de sus justificantes de nómina, número de línea y cantidad de las líneas de los justificantes para el empleado cuyo código=1.
Nombre del empleado, mes y ejercicio de sus justificantes de nómina para los empleados que han trabajado en el departamento de Ventas.
Nombre del empleado e ingresos totales percibidos agrupados por nombre.
Nombre de los empleados que han ganado más de 2000 € en el año 2006.
Número de empleados cuyo número de hijos es superior a la media de hijos de los empleados.
Nombre de los empleados que más hijos tienen o que menos hijos tienen.
Nombre de los empleados que no tienen justificante de nóminas.
Nombre y fecha de nacimiento de todos los empleados.
Nombre y fecha de nacimiento con formato "1 de Enero de 2000" y etiquetada la columna como fecha, de todos los empleados.
Nombre de los empleados, nombre de los departamentos en los que ha trabajado y función en mayúsculas que ha realizado en cada departamento.
Nombre, fecha de nacimiento y nombre del día de la semana de su fecha de nacimiento de todos los empleados.
Nombre y edad de los empleados.
Nombre, edad y número de hijos de los empleados que tienen menos de 40 años y tienen hijos.
Nombre, edad de los empleados y nombre del departamento de los empleados que han trabajado en más de un departamento.
Nombre, edad y número de cuenta de aquellos empleados cuya edad es múltiplo de 3.
Nombre e ingresos percibidos empleado más joven y del más longevo.
Criterios de puntuación. Total 10 puntos.
Todos los apartados tienen la misma puntuación. Se valorará además, la presentación del documento elaborado. 0,33 puntos cada respuesta correcta, para un total de 10 puntos.
Recursos necesarios para realizar la Tarea.
Aquí tienes los archivos que necesitas para crear las tablas e insertar los datos. Con ellas, además de ver la estructura de las tablas, podrás probar las consultas para comprobar su funcionamiento.

Creación de tablas e inserción de datos (2.2 KB)

Consejos y recomendaciones.
Es aconsejable que crees en Oracle un usuario nuevo para estas tablas. Recuerda que puedes ejecutar los archivos desde Línea de Comandos SQL, para ello necesitabas acceder con un usuario y ejecutar los archivos tablas.sql y registros.sql tal y como se indica en los contenidos.

Indicaciones de entrega.
Una vez realizada la tarea elaborarás un único documento donde figuren las respuestas correspondientes. El envío se realizará a través de la plataforma de la forma establecida para ello, y el archivo se nombrará siguiendo las siguientes pautas:

apellido1_apellido2_nombre_SIGxx_Tarea

Asegúrate que el nombre no contenga la letra ñ, tildes ni caracteres especiales extraños. Así por ejemplo la alumna Begoña Sánchez Mañas para la cuarta unidad del MP de BD, debería nombrar esta tarea como...

sanchez_manas_begona_BD04_Tarea
