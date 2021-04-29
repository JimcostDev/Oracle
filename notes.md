# ORACLE

## USUARIOS:

- HR -> *usuario de prueba*

- System -> **super usuario**

## COMANDOS:

- conn o connect -> conexion a bd

- show user -> visualizar usuario

- alter user HR(user-name) account unlock -> desbloquear usuario (debe estar conectado con system)

## SQL (COMMAND LINE):

Comando/Sentencia SQL | Concepto/Descripcion
--|--
```select * from cat``` | Visualizar el diccionario de datos del usuario con el que estoy conectado (catalogo)
```describe o desc name-table``` | visualizar estructura de la tabla
```set linesize 300``` | ancho cmd sql
```set pagesize 30``` | alto cmd sql
```BETWEEN``` | Entre un rango de valores
```NOT BETWEEN``` | No este entre un rango de valores
```IN``` | Selecciona de una lista
```NOT IN``` | Selecciona los valores que no estan en la lista
```IS NULL``` | Retorna valores nulos
```IS NOT NULL``` | Retorna valores No nulos
```LIKE``` | Busqueda de patrones 
```NOT LIKE``` | Retorna los que no cumplan con la busqueda de patrones
```ORDER BY```  | Se utiliza para ordenar, puedo ordernar asc-Ascendente(por defecto) desc-descendente
```NVL``` | Nivelar Valores Nulos a un numero
```JOIN``` | Poder seleccionar informacion de mas de una tabla
```UPPER ``` | Convertir a mayusculas. Ej: ```select ename, upper(ename) from emp;```
```LOWER ``` | Convertir a minusculas. Ej: ```select ename, lower(ename) from emp;```
```INITCAP``` | Convierte el Primer caracter en Mayuscula, el resto en minuscula. Ej: ```select ename, initcap(ename) from emp;```
```LPAD``` | Llenar o completar a la izquierda con. Ej: ```select ename, lpad(ename,10,'*') from emp;```
```RPAD ``` | Llenar o completar a la izquierda con. Ej: ```select ename, rpad(ename,10,'-') from emp;```
```LENGTH ``` | Retorna el tamano de una Cadena. Ej: ```select ename, length(ename) from emp;```
```SUBSTR ``` | Retorna una Subcadena. Ej: ```select ename, substr(ename, 1,3) from emp;```
```INSTR  ``` | Retorna la posicion del caracter dentro de la cadena. Ej: ```select ename, instr(ename,'A') from emp;```



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
### 13. SINTAXIS COMPLETA DEL COMANDO SELECT:
  ```SQL 
		SELECT lista de campo(s)
		FROM tabla(s)
		WHERE condicion(es)
		[GROUP BY lista de campos(s)] => Agrupar por
		[HAVING condicion] => condicion de agrupamiento
		[ORDER BY lista de campo(s)] => Ordenamiento 
```		
		``````

 
 ## TALLER-1:
  
 ### 1. Seleccionar el cargo y cantidad de registros por cargo. para la tabla empleado, solo para aquellos donde la cantidad de registros por cargo es mayor o igual a 3.
 
 ```SQL 
	select job, count(*) 
	from emp group by job having count(*) >= 3;
  ```
### 2. Seleccionar el registro de la tabla empleado, con la fecha de ingreso mas reciente. 

```SQL 
	select max(hiredate) FINGRESO from emp;
```

### 3. Seleccionar los registros de la tabla empleado, donde el salario sea mayor o igual al promedio de todos los salarios de la tabla empleado.

```SQL 
	/* 
	nota: para averiguar el promedio salarial
	select avg(sal) from emp;
	*/
	select * from emp where sal >= 2073.214;
	
	select * from emp where sal >= (select avg(sal) from emp);
```

### 4. Seleccionar el codigo del empleado, cargo, ingresos (salario mas comision) codigo del departamento y nombre del departamento para todos los registros de la tabla empleado. Ordenados de forma descendente por los ingresos.

```SQL 
	select empno,job, sal+nvl(comm,0)as TOTAL,  e.deptno, dname 
	from emp e, dept d
	where e.deptno = d.deptno 
	order by TOTAL desc;
```

## TALLER-2:

### 1. Seleccionar el nombre del empleado (en minusculas), lleno tanto a la derecha, como a la izquierda con asteriscos, hasta completar 20 posiciones. Nota: utilizando 1 solo script de sql, debe quedar asi:
```SQL 
	/*
		*******smith*******
		*******allen********
		*******ward********
	*/
	select lpad(lower(ename),13, '*') ||''|| rpad('*',7, '*') from emp;
```
	

### 2. Crear una tabla llamada taller3, de la siguiente manera:
```SQL 
	create table taller3
	(
		nombres varchar2(40)
	);
```

### 3. insertar los siguientes registros en la tabla taller3, asi:
```SQL 
	insert into taller3
	values ('ana paz');

	insert into taller3
	values ('margarita sinisterra');

	insert into taller3
	values ('carlos saldarriaga');

	insert into taller3
	values ('santiago gil');

	insert into taller3
	values ('eduardo castro');
```

### 4. Seleccionar solo el nombre (en mayusculas), para todos los registros de la tabla taller3.
```SQL 
	select substr(upper(nombres),1, instr(nombres,' ')) from taller3;
```


### 5. Seleccionar solo el apellido (en mayusculas), para todos los registros de la tabla taller3.
```SQL 
	select substr(upper(nombres),instr(nombres,' ',-1)) from taller3;
```

## PARCIAL-1:

### 1. Seleccionar el codigo de empleado, nombre del empleado, codigo del jefe y nombre del jefe, para todos los registros de la tabla empleado.
```SQL 
	select emp.empno, emp.ename EMPLEADO, emp.mgr COD_JEFE, e.ename JEFE
	from emp emp
	inner join emp e ON e.empno = emp.mgr order by empno;
```
 
### 2. Seleccionar los registros de la tabla empleado, con las 2 fechas de ingreso mas reciente. (no utilizar el rownum)
```SQL 
	select  * from emp 
	where hiredate >=(select max(hiredate) 
	from emp 
	where hiredate<>(select max(hiredate) from emp)) 
	order by hiredate desc;
```	

### 3. Seleccionar el codigo del empleado, nombre del empleado, cargo, salario y grado salarial.para todos los registro de la tabla empleado. 
```SQL
	select empno, ename, sal, grade
	from emp,  salgrade 
	where sal between losal and hisal
	order by grade desc
```	

### 4. Seleccionar los registros de la tabla empleado, para aquellos registros donde el salario esta entre el promedio de salarios de todos los analistas y el promedio de salarios de todos los vendedores.

```SQL
	select * from emp 
	where sal between (select avg(sal)
	from emp 
	where job = 'SALESMAN') 
	and (select avg(sal) 
	from emp where  job = 'ANALYST');

	select * from emp 
	where sal between 1400 AND 3000 ;
```

### 5. Seleccionar Nombre1, Nombre2, Apellido1 y Apellido2 en Mayusculas, para los registros de la tabla parcial1
``` SQL
		select substr(upper(nombre_completo),1, instr(nombre_completo,' ')) NOMBRE1, 
		substr(upper(nombre_completo),instr(nombre_completo,' ',-1)) APELLIDO2 
		from parcial1;

		
		select 
		upper(substr(nombre_completo, 1, instr(nombre_completo,' ')-1)) NOMBRE1,

		upper(decode(length(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)))-length
		(replace(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)), ' ', '')),1, '  ',
		2,substr(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)) ,
		1, instr(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)),' ')-1))) NOMBRE2,

		upper(decode(length(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)))-length
		(replace(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)), ' ', '')),1, 
		substr(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)) ,
		1, instr(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)),' ')-1),
		2,substr(substr(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)),
		instr(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)),' ')+1,
		length(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)))),1,
		instr(substr(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)),
		instr(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)),' ')+1,
		length(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)))),' ')-1))) APELLIDO1,

		upper(substr(
		substr(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)),
		instr(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)),' ')+1,
		length(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)))),
		instr(substr(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)),
		instr(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)),' ')+1,
		length(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)))),' ')+1,
		length(substr(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)),
		instr(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)),' ')+1,
		length(substr(nombre_completo, instr(nombre_completo,' ')+1, length(nombre_completo)))))
		))APELLIDO2
		from parcial1 
```
 
 ## PARCIAL-FINAL:
 
 ### Realizar un script de sql, para seleccionar lo siguiente: Codigo del Empleado, Nombre del Empleado, Codigo del Departamento, Nombre del Departamento,Salario, Grado salarial, ingresos (salario mas comision) y un nivel de ingresos aplicado asi:
	``` SQL
		/*
		-Si ingresos son menores que 1000, ingresos bajos,
		-Si ingresos estan entre 1000 y 1600, ingresos medios,
		-Si ingresos estan entre 1601 y 2500, ingresos altos,
		-Si ingresos estan entre 2501 y 2999, ingresos superiores,
		-si ingresos son mayores o iguales que 3000, ingresos muy superiores.
		*/
		select empno,ename,e.deptno, dname ,sal, s.grade, sal+nvl(comm,0)as INGRESOS, 
		decode(greatest(
			decode(greatest(sal+nvl(comm,0),    0), least(sal+nvl(comm,0),  999), 1, 0),
			decode(greatest(sal+nvl(comm,0), 1000), least(sal+nvl(comm,0), 1600), 2, 0),
			decode(greatest(sal+nvl(comm,0), 1601), least(sal+nvl(comm,0), 2500), 3, 0),
			decode(greatest(sal+nvl(comm,0), 2501), least(sal+nvl(comm,0), 2999), 4, 0)), 
				1,'INGRESOS BAJOS',
				2,'INGRESOS MEDIOS',
				3,'INGRESOS ALTOS',
				4,'INGRESOS SUPERIORES',
				'INGRESOS MUY SUPERIORES') AS NIVEL_SALARIAL
	from emp e, dept d, salgrade s
	where e.deptno = d.deptno
	order by INGRESOS desc;
	```