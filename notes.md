# ORACLE

## USUARIOS

- HR -> *usuario de prueba*

- System -> **super usuario**

## COMANDOS 

- conn o connect -> conexion a bd

- show user -> visualizar usuario

- alter user HR(user-name) account unlock -> desbloquear usuario (debe estar conectado con system)

## SQL (COMMAND LINE)

- select * from cat -> visualizar el diccionario de datos del usuario con el que estoy conectado (catalogo)

- describe o desc name-table -> visualizar estructura de la tabla

- set linesize 300 -> ancho cmd sql

- set pagesize 30 -> alto cmd sql

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

### 2. Seleccionar los registros de la tabla empleado, donde el salario no este entre 1000 y 3000.

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

### 4. Seleccionar el nombre del empleado, cargo y salario. para todos los registros de la tabla empleado, ordenados alfabeticamente por el nombre del empleado

```SQL 
	select ename ,job ,sal from emp order by ename asc; 
  ```


