# ORACLE

## USUARIOS:

- HR -> *usuario de prueba*

- System -> **super usuario**

## COMANDOS:

- conn o connect -> conexion a bd

- show user -> visualizar usuario

- alter user HR(user-name) account unlock -> desbloquear usuario (debe estar conectado con system)

## SQL (COMMAND LINE):

- **SINTAXIS COMPLETA DEL COMANDO SELECT**
```SQL 
		SELECT lista de campo(s)
		FROM tabla(s)
		[WHERE condicion(es)]
		[GROUP BY lista de campos(s)] => Agrupar por
		[HAVING condicion] => condicion de agrupamiento
		[ORDER BY lista de campo(s)] => Ordenamiento
	```

- select * from cat -> visualizar el diccionario de datos del usuario con el que estoy conectado (catalogo)
- describe o desc name-table -> visualizar estructura de la tabla
- set linesize 300 -> ancho cmd sql
- set pagesize 30 -> alto cmd sql
- BETWEEN (Entre un rango de valores)
- NOT BETWEEN (No este entre un rango de valores)
- IN (Selecciona de una lista)
- NOT IN (Selecciona los valores que no estan en la lista)
- IS NULL (Retorna valores nulos)
- IS NOT NULL (Retorna valores No nulos)
- LIKE (Busqueda de patrones)
- NOT LIKE (Retorna los que no cumplan con la busqueda de patrones)
- ORDER BY  (Se utiliza para ordenar, puedo ordernar asc-Ascendente(por defecto) desc-descendente)
- NVL (Nivelar Valores Nulos a un numero)
- JOIN (Poder seleccionar informacion de mas de una tabla)


## TIPOS DE DATOS:

- NUMBER (numerico)

- VARCHAR2 (alfanumerico)

- DATE (fechas)

## EJERCICIOS EN CLASE:

### 1. Seleccionar los registros de la tabla empleado, donde el salario este entre 1000 y 3000.

```SQL 
	select * from emp where sal between 1000 and 3000;

	select * from emp where sal >= 1000 and sal <= 3000;
```

### 2. Seleccionar los registros de la tabla empleado, donde el salario no este entre 1000 y 3000.

```SQL 
	select * from emp where sal not between 1000 and 3000;

	select * from emp where sal < 1000 or sal > 3000;
```

### 3. Seleccionar los registros de la tabla empleado, donde el cargo pueda ser analista o vendedor.

```SQL 
	select * from emp where job  = 'ANALYST' or job = 'SALESMAN'; 

	select * from emp where job IN ('ANALYST','SALESMAN');	
 ```

### 4. Seleccionar el nombre del empleado, cargo y salario. para todos los registros de la tabla empleado, ordenados alfabeticamente por el nombre del empleado 

```SQL 
	select ename ,job ,sal from emp order by ename asc;
	select ename ,job ,sal from emp order by ename desc;
	select ename, job, sal from emp order by 1; => posicion relativa
  ```
  
### 5. Seleccionar los registros de la tabla empleado, donde el cargo no sea analista y vendedor.

```SQL 
	select * from emp where job  != 'ANALYST' and job != 'SALESMAN'; 
	select * from emp where job NOT IN ('ANALYST','SALESMAN');	
 ```

### 6. seleccionar los registros de la tabla empleado donde la comision es nula.

```SQL 
	select * from emp where comm is null; 
 ```

### 7. seleccionar los registros de la tabla empleado donde el nombre inicie con la letra A

```SQL 
	select * from emp where ename like 'A%'; 
 ```
 
 ### 8. seleccionar los registros de la tabla empleado donde el nombre no inicie con la letra A

```SQL 
	select * from emp where ename not like 'A%'; 
 ```

### 9. seleccionar los campos nombre, cargo, salario, comision de la tabla empleado y guardar la suma del salario y la comision en un campo llamado total.

```SQL 
	select ename, job, sal, comm, sal+nvl(comm,0) as TOTAL from emp;
 ```
 
### 10. Seleccionar el nombre del empleado, cargo, salario, codigo del departamento y nombre del departamento para todos los registros de la tabla empleado
```SQL 
	-- JOIN --
	select ename, job, sal, emp.deptno, dname 
	from emp, dept
	where emp.deptno = dept.deptno; 
	
	-- JOIN CON ALIAS --
	select ename, job, sal, e.deptno, dname 
	from emp e, dept d
	where e.deptno = d.deptno; 
 ```
 
### 11. Seleccionar el cargo y la cantidad de registros por cargo. para todos los registros de la tabla empleado
```SQL 
	select job, count(*) from emp group by job;
  ```
  
### 12. Seleccionar el cargo y el promedio salarial por cada cargo. para todos los registros de la tabla empleado

```SQL 
	select job, avg(sal) from emp group by job;
  ```
 
 ## TALLER: