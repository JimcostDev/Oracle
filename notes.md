# ORACLE

## USUARIOS

- 1. HR -> *usuario de prueba*

- 2. System -> **super usuario**

## COMANDOS 

- 1. conn o connect -> conexion a bd

- 2. show user -> visualizar usuario

- 3. alter user HR(user-name) account unlock -> desbloquear usuario (debe estar conectado con system)

## SQL (COMMAND LINE)

- 1. select * from cat -> visualizar el diccionario de datos del usuario con el que estoy conectado (catalogo)

- 2. describe o desc name-table -> visualizar estructura de la tabla

- 3. set linesize 300 -> ancho cmd sql

- 4. set pagesize 30 -> alto cmd sql

## TIPOS DE DATOS 

- NUMBER (numerico)

- VARCHAR2 (alfanumerico)

- DATE (fechas)

## CLASE 1 - EJERCICIOS:

### 1. Seleccionar los registros de la tabla empleado, donde el salario este entre 1000 y 3000.

- select *
from emp
where sal between 1000 and 3000;

- select *
from emp
where sal >= 1000
and sal <= 3000;

### -- 2. Seleccionar los registros de la tabla empleado, donde el salario no este entre 1000 y 3000.**

- select *
from emp
where sal not between 1000 and 3000;

- select *
from emp
where sal < 1000
or sal > 3000;

### 3. Seleccionar los registros de la tabla empleado, donde el cargo pueda ser analista o vendedor.

- select * 
from emp 
where job  = 'ANALYST' 
or job = 'SALESMAN';

### 4. Seleccionar el nombre del empleado, cargo y salario. para todos los registros de la tabla empleado.
    ordenados alfabeticamente por el nombre del empleado

- select ename
  ,job
  ,sal
  from emp 
  order by ename asc;


