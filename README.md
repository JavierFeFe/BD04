# Tarea para BD04.
## Detalles de la tarea de esta unidad.
La empresa El Desván, que se dedica a la rama textil ha decidido informatizar su gestión de nóminas. Para ello BK programación desarrollará para ellos la base de datos.

El gerente le ha explicado como funciona la gestión de nóminas y Juan, que será quien se encargue de crear el modelo, las tablas y las consultas, ha recogido la siguiente información:

* A cada empleado se le entrega un justificante de nómina al mes. De cada empleado registraremos su código de empleado, nombre, apellidos, número de hijos, cuenta corriente y porcentaje de retención para Hacienda.
* Un empleado puede trabajar en varios Departamentos y en cada uno de ellos realizará una función.
* De un Departamento mantenemos el nombre del mismo y un código de Departamento.
* Los datos de un justificante de nómina son el ingreso total percibido por el empleado y el descuento total aplicado.
* La distinción entre dos justificantes de nómina se hace, además de mediante el código de empleado, mediante el ejercicio fiscal y número de mes al que pertenece.
* Cada justificante de nómina consta de varias líneas y cada línea se identifica por un número de línea del correspondiente justificante. Una línea puede corresponder a un ingreso o a un descuento. En ambos casos se recoge la cantidad (positiva o negativa). En el caso de los descuentos se recoge la base y el porcentaje. 

Con todos estos datos ha llegado al siguiente modelo entidad-relación: 
  
![image](https://user-images.githubusercontent.com/44543081/53692994-8c9e8380-3d99-11e9-8ecb-c61af768a92c.png)
  
Modelo entidad-relación que describe las relaciones entre las distintas tablas que se necesitan para la tarea.
También ha creado las bases y ha insertado algunos datos para realizar pruebas de las consultas que haga.

Todo está listo para que le ayudes. Estas son las consultas que debes crear:

* Código y nombre de todos los departamentos.

```SQL
select CODIGO, NOMBRE from DEPARTAMENTOS
```
* Mes y ejercicio de los justificantes de nómina pertenecientes al empleado cuyo código es 1.
```SQL
select MES, EJERCICIO from JUST_NOMINAS where COD_EMP=1
```
* Número de cuenta y nombre de los empleados cuya retención es mayor o igual que 10.
```SQL
select CUENTA, NOMBRE from EMPLEADOS where RETENCION >= 10
```
* Código y nombre de los empleados ordenados ascendentemente por nombre.
```SQL
select CODIGO, NOMBRE from EMPLEADOS order by NOMBRE asc
```
* Nombre de los empleados que tienen más de 2 hijos.
```SQL
select NOMBRE from EMPLEADOS where HIJOS > 2
```
* Código y número de cuenta de los empleados cuyo nombre empieze por 'A' o por 'J'.
```SQL
select CODIGO, CUENTA from EMPLEADOS where NOMBRE like 'A%' or NOMBRE like 'J%'
```
* Número de empleados que hay en la base de datos.
```SQL
select count(CODIGO) FROM EMPLEADOS
```
* Nombre del primer y último empleado en términos alfabéticos.
```SQL
select NOMBRE from (select NOMBRE FROM EMPLEADOS order by NOMBRE asc) where ROWNUM = 1
union
select NOMBRE from (select NOMBRE FROM EMPLEADOS order by NOMBRE desc) where ROWNUM = 1;
```
* Nombre y número de hijos de los empleados cuya retención es: 8, 10 o 12.
```SQL
select NOMBRE, HIJOS from EMPLEADOS where RETENCION=8 or RETENCION=10 or RETENCION=12
```
* Número de hijos y número de empleados agrupados por hijos, mostrando sólo los grupos cuyo número de empleados sea mayor que 1.
```SQL
select * from (select sum(HIJOS)as numero_hijos , count(CODIGO) as numero_empleados from EMPLEADOS group by HIJOS) where numero_empleados > 1;
```
* Número de hijos, retención máxima, mínima y media de los empleados agrupados por hijos.
```SQL
select sum(HIJOS), max(RETENCION), min(RETENCION), avg(RETENCION) from EMPLEADOS group by HIJOS;
```
* Nombre y función de los empleados que han trabajado en el departamento 1.
```SQL
select NOMBRE, FUNCION from EMPLEADOS inner join TRABAJAN on EMPLEADOS.CODIGO=TRABAJAN.COD_EMP where COD_DEP = 1;
```
* Nombre del empleado, nombre del departamento y función que han realizado de los empleados que tienen 1 hijo.
```SQL
select EMPLEADOS.NOMBRE as EMPLEADO, DEPARTAMENTOS.NOMBRE as DEPARTAMENTO, TRABAJAN.FUNCION from EMPLEADOS inner join TRABAJAN on EMPLEADOS.CODIGO=TRABAJAN.COD_EMP inner join DEPARTAMENTOS on TRABAJAN.COD_DEP=DEPARTAMENTOS.CODIGO where EMPLEADOS.HIJOS=1
```
* Nombre del empleado y nombre del departamento en el que han trabajado empleados que no tienen hijos.
```SQL
select EMPLEADOS.NOMBRE as EMPLEADO, DEPARTAMENTOS.NOMBRE as DEPARTAMENTO from EMPLEADOS inner join TRABAJAN on EMPLEADOS.CODIGO=TRABAJAN.COD_EMP inner join DEPARTAMENTOS on TRABAJAN.COD_DEP=DEPARTAMENTOS.CODIGO where EMPLEADOS.HIJOS=0
```
* Nombre del empleado, mes y ejercicio de sus justificantes de nómina, número de línea y cantidad de las líneas de los justificantes para el empleado cuyo código=1.
```SQL
select EMPLEADOS.NOMBRE, JUST_NOMINAS.MES, JUST_NOMINAS.EJERCICIO, LINEAS.NUMERO, LINEAS.CANTIDAD from EMPLEADOS 
inner join JUST_NOMINAS on JUST_NOMINAS.COD_EMP=EMPLEADOS.CODIGO inner join LINEAS on LINEAS.COD_EMP=EMPLEADOS.CODIGO where EMPLEADOS.CODIGO = 1 
```
* Nombre del empleado, mes y ejercicio de sus justificantes de nómina para los empleados que han trabajado en el departamento de Ventas.
```SQL
select EMPLEADOS.NOMBRE, JUST_NOMINAS.MES, JUST_NOMINAS.EJERCICIO from EMPLEADOS 
inner join JUST_NOMINAS on JUST_NOMINAS.COD_EMP=EMPLEADOS.CODIGO 
inner join TRABAJAN on EMPLEADOS.CODIGO=TRABAJAN.COD_EMP
inner join DEPARTAMENTOS on TRABAJAN.COD_DEP=DEPARTAMENTOS.CODIGO
where DEPARTAMENTOS.NOMBRE='Ventas'
```
* Nombre del empleado e ingresos totales percibidos agrupados por nombre.
```SQL
select EMPLEADOS.NOMBRE, sum(JUST_NOMINAS.INGRESO) from EMPLEADOS 
inner join JUST_NOMINAS on JUST_NOMINAS.COD_EMP=EMPLEADOS.CODIGO 
group by EMPLEADOS.NOMBRE 
```
* Nombre de los empleados que han ganado más de 2000 € en el año 2006.
```SQL
select NOMBRE, EJERCICIO from (select EMPLEADOS.NOMBRE, JUST_NOMINAS.EJERCICIO, sum(JUST_NOMINAS.INGRESO) AS TOTAL from EMPLEADOS 
inner join JUST_NOMINAS on JUST_NOMINAS.COD_EMP=EMPLEADOS.CODIGO 
group by EMPLEADOS.NOMBRE, JUST_NOMINAS.EJERCICIO ) where TOTAL>2000
```
* Número de empleados cuyo número de hijos es superior a la media de hijos de los empleados.
```SQL
select count(NOMBRE) from (select NOMBRE, HIJOS, (select avg(HIJOS) from EMPLEADOS) as MEDIA from EMPLEADOS) where HIJOS>MEDIA;
```
* Nombre de los empleados que más hijos tienen o que menos hijos tienen.
```SQL
select NOMBRE from (select NOMBRE, HIJOS, (select max(HIJOS) from EMPLEADOS) as MAXIMO, (select min(HIJOS) from EMPLEADOS) as MINIMO from EMPLEADOS) where HIJOS=MAXIMO OR HIJOS=MINIMO;
```
* Nombre de los empleados que no tienen justificante de nóminas.
```SQL
select NOMBRE from EMPLEADOS left join JUST_NOMINAS ON EMPLEADOS.CODIGO=JUST_NOMINAS.COD_EMP where JUST_NOMINAS.COD_EMP is null
```
* Nombre y fecha de nacimiento de todos los empleados.
```SQL
select NOMBRE, FNACIMIENTO from EMPLEADOS
```
* Nombre y fecha de nacimiento con formato "1 de Enero de 2000" y etiquetada la columna como fecha, de todos los empleados.
```SQL
select NOMBRE, to_char(FNACIMIENTO, 'DD "de" Month "de" YYYY') as FECHA from EMPLEADOS
```
* Nombre de los empleados, nombre de los departamentos en los que ha trabajado y función en mayúsculas que ha realizado en cada departamento.
```SQL
select EMPLEADOS.NOMBRE, DEPARTAMENTOS.NOMBRE, UPPER(TRABAJAN.FUNCION) from EMPLEADOS 
inner join TRABAJAN on EMPLEADOS.CODIGO=TRABAJAN.COD_EMP 
inner join DEPARTAMENTOS on TRABAJAN.COD_DEP=DEPARTAMENTOS.CODIGO
```
* Nombre, fecha de nacimiento y nombre del día de la semana de su fecha de nacimiento de todos los empleados.
```SQL
select EMPLEADOS.NOMBRE, FNACIMIENTO, to_Char(FNACIMIENTO, 'DAY') from EMPLEADOS 
```
* Nombre y edad de los empleados.
```SQL
select EMPLEADOS.NOMBRE, trunc(months_between(CURRENT_DATE, FNACIMIENTO)/12) from EMPLEADOS 
```
* Nombre, edad y número de hijos de los empleados que tienen menos de 40 años y tienen hijos.
```SQL
select NOMBRE, EDAD, HIJOS from(select EMPLEADOS.NOMBRE, HIJOS, trunc(months_between(CURRENT_DATE, FNACIMIENTO)/12)  as EDAD from EMPLEADOS) where EDAD >0 and HIJOS > 0
```
* Nombre, edad de los empleados y nombre del departamento de los empleados que han trabajado en más de un departamento.
```SQL
select NOMBRE, EDAD, HIJOS, DEPARTAMENTOS from(
select EMPLEADOS.NOMBRE, HIJOS, trunc(months_between(CURRENT_DATE, FNACIMIENTO)/12) as EDAD, count(COD_DEP) as DEPARTAMENTOS from EMPLEADOS
left join TRABAJAN on TRABAJAN.COD_EMP=EMPLEADOS.CODIGO group by EMPLEADOS.NOMBRE, HIJOS, trunc(months_between(CURRENT_DATE, FNACIMIENTO)/12)
)
where DEPARTAMENTOS > 0
```
* Nombre, edad y número de cuenta de aquellos empleados cuya edad es múltiplo de 3.
```SQL
select NOMBRE, EDAD, CUENTA from(
select EMPLEADOS.NOMBRE, CUENTA, trunc(months_between(CURRENT_DATE, FNACIMIENTO)/12) as EDAD from EMPLEADOS
) where mod(edad,3) = 0;
```
* Nombre e ingresos percibidos empleado más joven y del más longevo.
```SQL
select DISTINCT(NOMBRE), INGRESO from (select EMPLEADOS.NOMBRE, trunc(months_between(CURRENT_DATE, FNACIMIENTO)/12) as EDAD_ACTUAL , JUST_NOMINAS.INGRESO from EMPLEADOS inner join JUST_NOMINAS on EMPLEADOS.CODIGO=JUST_NOMINAS.COD_EMP)
where EDAD_ACTUAL = (select MAX(EDAD) from(
select EMPLEADOS.NOMBRE, trunc(months_between(CURRENT_DATE, FNACIMIENTO)/12) as EDAD from EMPLEADOS
)) or EDAD_ACTUAL = (select MIN(EDAD) from(
select EMPLEADOS.NOMBRE, trunc(months_between(CURRENT_DATE, FNACIMIENTO)/12) as EDAD from EMPLEADOS
))
```
