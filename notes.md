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
		from parcial1 ;
```
 
 ## PARCIAL-FINAL:
 
 ### 1. Realizar un script de sql, para seleccionar lo siguiente: Codigo del Empleado, Nombre del Empleado, Codigo del Departamento, Nombre del Departamento,Salario, Grado salarial, ingresos (salario mas comision) y un nivel de ingresos aplicado asi:
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

### 2. Crear una tabla llamada Valores, la cual almacene un valor numero de 5 posiciones, e insertar 10 valores diferentes.
``` SQL
		/*
			Seleccionar el valor en numeros y el valor en letras.
			Nota: Tener en cuenta que al insertar cualquier valor de 5 digitos, debe retornar correctamente el valor en letras.

			Ej:
			83734, el valor en letras es: Ochenta y Tres Mil Setecientos Treinta y Cuatro
		*/
		
		select numero, 
		decode(substr(numero, 1,2),10, 'DIEZ MIL',11, 'ONCE MIL',12,'DOCE MIL',13,'TRECE MIL',14,'CATORCE MIL',15,'QUINCE MIL',16,'DIECISÉIS MIL',17,'DIECISIETE MIL',18,'DIECIOCHO MIL',19,'DIECINUEVE MIL'
		,20,'VEINTE MIL',21,'VEINTE Y UN MIL',22,'VEINTE Y DOS MIL',23,'VEINTE Y TRES MIL',24,'VEINTE Y CUATRO MIL',25,'VEINTE Y CINCO MIL',26,'VEINTE Y SEIS MIL',27,'VEINTE Y SIETE MIL',28,'VEINTE Y OCHO MIL',29,'VEINTE Y NUEVE MIL'
		,30,'TREINTA MIL',31,'TREINTA Y UN MIL',32,'TREINTA Y DOS MIL',33,'TREINTA Y TRES MIL',34,'TREINTA Y CUATRO MIL',35,'TREINTA Y CINCO MIL',36,'TREINTA Y SEIS MIL',37,'TREINTA Y SIETE MIL',38,'TREINTA Y OCHO MIL',39,'TREINTA Y NUEVE MIL'
		,40,'CUARENTA MIL',41,'CUARENTA Y UN MIL',42,'CUARENTA Y DOS MIL',43,'CUARENTA Y TRES MIL',44,'CUARENTA Y CUATRO MIL',45,'CUARENTA Y CINCO MIL',46,'CUARENTA Y SEIS MIL',47,'CUARENTA Y SIETE MIL',48,'CUARENTA Y OCHO MIL',49,'CUARENTA Y NUEVE MIL'
		,50,'CINCUENTA MIL',51,'CINCUENTA Y UN MIL',52,'CINCUENTA Y DOS MIL',53,'CINCUENTA Y TRES MIL',54,'CINCUENTA Y CUATRO MIL',55,'CINCUENTA Y CINCO MIL',56,'CINCUENTA Y SEIS MIL',57,'CINCUENTA Y SIETE MIL',58,'VEINTE Y OCHO MIL',59,'VEINTE Y NUEVE MIL'
		,60,'SESENTA MIL',61,'SESENTA Y UN MIL',62,'SESENTA Y DOS MIL',63,'SESENTA Y TRES MIL',64,'SESENTA Y CUATRO MIL',65,'SESENTA Y CINCO MIL',66,'SESENTA Y SEIS MIL',67,'SESENTA Y SIETE MIL',68,'SESENTA Y OCHO MIL',69,'SESENTA Y NUEVE MIL'
		,70,'SETENTA MIL',71,'SETENTA Y UN MIL',72,'SETENTA Y DOS MIL',73,'SETENTA Y TRES MIL',74,'SETENTA Y CUATRO MIL',75,'SETENTA Y CINCO MIL',76,'SETENTA Y SEIS MIL',77,'SETENTA Y SIETE MIL',78,'SETENTA Y OCHO MIL',79,'SETENTA Y NUEVE MIL'
		,80,'OCHENTA MIL',81,'OCHENTA Y UN MIL',82,'OCHENTA Y DOS MIL',83,'OCHENTA Y TRES MIL',84,'OCHENTA Y CUATRO MIL',85,'OCHENTA Y CINCO MIL',86,'OCHENTA Y SEIS MIL',87,'OCHENTA Y SIETE MIL',88,'OCHENTA Y OCHO MIL',89,'OCHENTA Y NUEVE MIL'
		,90,'NOVENTA MIL',91,'NOVENTA Y UN MIL',92,'NOVENTA Y DOS MIL',93,'NOVENTA Y TRES MIL',94,'NOVENTA Y CUATRO MIL',95,'NOVENTA Y CINCO MIL',96,'NOVENTA Y SEIS MIL',97,'NOVENTA Y SIETE MIL',98,'NOVENTA Y OCHO MIL',99,'NOVENTA Y NUEVE MIL'
		) 
		||' '||
		decode(substr(numero, 3,3),000, '',100, 'CIEN', 
			decode(substr(numero, 3,1),1, 'CIENTO',2, 'DOSCIENTOS',3, 'TRESCIENTOS',4, 'CUATROCIENTOS',5, 'QUINIENTOS',6, 'SEISCIENTOS',7, 'SETECIENTOS',8, 'OCHOCIENTOS',9, 'NOVECIENTOS'
			)
		||' '||
		decode(substr(numero, 4,2),01, 'UNO',02, 'DOS',03, 'TRES',04, 'CUATRO',05, 'CINCO',06, 'SEIS',07, 'SIETE',08, 'OCHO',09, 'NUEVE'
			,10, 'DIEZ',11, 'ONCE',12,'DOCE',13,'TRECE',14,'CATORCE',15,'QUINCE',16,'DIECISÉIS',17,'DIECISIETE',18,'DIECIOCHO',19,'DIECINUEVE'
			,20,'VEINTE',21,'VEINTE Y UNO',22,'VEINTE Y DOS',23,'VEINTE Y TRES',24,'VEINTE Y CUATRO',25,'VEINTE Y CINCO',26,'VEINTE Y SEIS',27,'VEINTE Y SIETE',28,'VEINTE Y OCHO',29,'VEINTE Y NUEVE'
			,30,'TREINTA',31,'TREINTA Y UNO',32,'TREINTA Y DOS',33,'TREINTA Y TRES',34,'TREINTA Y CUATRO',35,'TREINTA Y CINCO',36,'TREINTA Y SEIS',37,'TREINTA Y SIETE',38,'TREINTA Y OCHO',39,'TREINTA Y NUEVE'
			,40,'CUARENTA',41,'CUARENTA Y UNO',42,'CUARENTA Y DOS',43,'CUARENTA Y TRES',44,'CUARENTA Y CUATRO',45,'CUARENTA Y CINCO',46,'CUARENTA Y SEIS',47,'CUARENTA Y SIETE',48,'CUARENTA Y OCHO',49,'CUARENTA Y NUEVE'
			,50,'CINCUENTA',51,'CINCUENTA Y UNO',52,'CINCUENTA Y DOS',53,'CINCUENTA Y TRES',54,'CINCUENTA Y CUATRO',55,'CINCUENTA Y CINCO',56,'CINCUENTA Y SEIS',57,'CINCUENTA Y SIETE',58,'VEINTE Y OCHO',59,'VEINTE Y NUEVE'
			,60,'SESENTA',61,'SESENTA Y UNO',62,'SESENTA Y DOS',63,'SESENTA Y TRES',64,'SESENTA Y CUATRO',65,'SESENTA Y CINCO',66,'SESENTA Y SEIS',67,'SESENTA Y SIETE',68,'SESENTA Y OCHO',69,'SESENTA Y NUEVE'
			,70,'SETENTA',71,'SETENTA Y UNO',72,'SETENTA Y DOS',73,'SETENTA Y TRES',74,'SETENTA Y CUATRO',75,'SETENTA Y CINCO',76,'SETENTA Y SEIS',77,'SETENTA Y SIETE',78,'SETENTA Y OCHO',79,'SETENTA Y NUEVE'
			,80,'OCHENTA',81,'OCHENTA Y UNO',82,'OCHENTA Y DOS',83,'OCHENTA Y TRES',84,'OCHENTA Y CUATRO',85,'OCHENTA Y CINCO',86,'OCHENTA Y SEIS',87,'OCHENTA Y SIETE',88,'OCHENTA Y OCHO',89,'OCHENTA Y NUEVE'
			,90,'NOVENTA',91,'NOVENTA Y UN0',92,'NOVENTA Y DOS',93,'NOVENTA Y TRES',94,'NOVENTA Y CUATRO',95,'NOVENTA Y CINCO',96,'NOVENTA Y SEIS',97,'NOVENTA Y SIETE',98,'NOVENTA Y OCHO',99,'NOVENTA Y NUEVE'
			)
		)AS DESCRIPCION
		from valores;
```

### 3. Seleccionar el nombre del empleado, grado salarial, salario, ingresos (salario mas comision)  y una bonificacion aplicada asi:
``` SQL
	/*
	-si el grado es 5, entonces la bonificacion sera el salario, mas el 50% de los ingresos.
	-si el grado es 4, entonces la bonificacion sera el salario, mas el 40% de los ingresos.
	-si el grado es 3, entonces la bonificacion sera el salario, mas el 30% de los ingresos.
	-Para el resto de grados, la bonificacion sera el salario, mas el 20% de los ingresos.
	*/
	select ename, grade, sal, sal+nvl(comm,0) as "INGRESOS TOTALES",
	decode(
		grade,5,sal+(sal+nvl(comm,0))*0.5,
		4,sal+(sal+nvl(comm,0))*0.4,
		3,sal+(sal+nvl(comm,0))*0.3,
		sal+(sal+nvl(comm,0))*0.2
	) as BONIFICACION
	from emp, salgrade ; 
```

### 4. Crear la(s) tabla(s) y registros necesarios, para que a partir de los datos de la Altura, Peso y Sexo. Realizar un script de sql para calcular el IMC (Indice de Masa Corporal) de cada persona.
``` SQL
	--
	create table IMC(
        usuario varchar(45),
        peso float,
        altura float,
        sexo char(1)
    );

	-- 
	insert into IMC (usuario, peso, altura, sexo)
		values('Silvia',60,1.56,'F')
	-- 
	insert into IMC (usuario, peso, altura, sexo)
		values('Ronaldo',60,1.85,'M')
	-- 
	insert into IMC (usuario, peso, altura, sexo)
		values('Oswaldo',75,1.82,'M')
	-- 
	insert into IMC (usuario, peso, altura, sexo)
		values('Marco',95,1.82,'M')
	--
	insert into IMC (usuario, peso, altura, sexo)
		values('Lorena',102,1.62,'F')

	-- 
	 select usuario,peso,altura, sexo,
		decode(greatest(
			decode(greatest(peso/(altura*altura), 0), least(peso/(altura*altura),  18.5), 1, 0),
			decode(greatest(peso/(altura*altura), 18.6), least(peso/(altura*altura),  24.99), 2, 0),
			decode(greatest(peso/(altura*altura), 25), least(peso/(altura*altura),  29.99), 3, 0)),
				1,'INFRAPESO',
				2,'NORMAL',
				3,'SOBREPESO',
				'OBESO') AS IMC_ESTADO
		from IMC;
```

### 5. Crear las tablas e insertar los registros que uds. consideren necesarios para el manejo de una tabla de posiciones de equipos de futbol.
``` SQL
	/*
	En Futbol los puntos son asi:
	Partido Ganado.......3 pts
	Partido Empatado.....1 pt
	Partido Perdido......0 pt

	PJ-Partidos Jugados
	PG-Partidos Ganados
	PE-Partidos Empatados
	PP-Partidos Perdidos
	GF-Goles a Favor
	GC-Goles en Contra
	GD-Gol diferencia
	
	Ejemplo:
	Posicion	Nombre del Equipo	Puntos	PJ 	PG	PE	PP	GF	GC	GD
	1			America				15		5	5	0	0	10	3	+7
	2			Cali				11		5	3	2	0	12	10	+2
	3			Nacional			10		5	3	1	1	15	9	+6
	4			Junior				8		5	2	2	1	11	12	-1
	5			Santafe				7		5	2	1	2	5	5	0
	6			Medellin			5		5	1	2	2	15	13	+2
	7			Millonarios			5		5	1	2	2	12	20	-8
	*/
	
	/*******************************CREATES*****************************************/

	------------------------EQUIPO--------------------------------------
	create table equipo(
	   eq_codigo char(10),
	   eq_nombre varchar(40),   
	   constraint equipo_pk primary key(eq_codigo)
	);
	-------------------------VISITANTE-LOCAL------------------------------
	create table vis_loc(
		vis_loc_codigo char(10),
		vis_loc_nombre varchar(40),
		constraint vis_loc_pk primary key(vis_loc_codigo)  
	);
	------------------------JUGADOR-----------------------------------
	create table jugador(
		ju_codigo char(10),
		eq_codigo char(10),
		ju_nombres varchar(40),
		ju_apellidos varchar(40),
	   constraint jugador_pk primary key(ju_codigo),
	   constraint ju_eq_fk foreign key (eq_codigo) references equipo (eq_codigo)
	);
	-------------------------PARTIDO------------------------------------
	create table partido(
	   par_codigo char(10),
	   fecha date,
	   eq_codigo char(10),
	   vis_loc_codigo char(10),
	   n_partido char(2),
	   constraint partido_pk primary key(par_codigo),
	   constraint  vi_lo_par_fk foreign key (vis_loc_codigo) references vis_loc (vis_loc_codigo),
	   constraint  eq_par_fk foreign key (eq_codigo) references equipo (eq_codigo)
	);
	-------------------------PUNTOS-------------------------------------
	create table puntos(
	   pun_codigo char(10),
	   descripcion varchar(40),
	   puntos number (1),   
	   constraint puntos_pk primary key(pun_codigo)
	); 
	-------------------------RESULTADO----------------------------------
	CREATE TABLE resultado(
	   res_codigo char(10),
	   par_codigo char(10),
	   eq_codigo char(10),
	   pun_codigo char(10),   
	   constraint resultados_pk primary key(res_codigo),
	   constraint re_eq_fk foreign key (eq_codigo) references equipo (eq_codigo),
	   constraint re_pun_fk foreign key (pun_codigo) references puntos (pun_codigo),
	   constraint par_pun_fk foreign key (par_codigo) references partido (par_codigo)
	);
	-------------------------GOLES--------------------------------------
	create table goles(
	   gol_codigo char(10),
	   par_codigo char(10),
	   ju_codigo char(10), 
	   gol_cant char(2),
	   constraint gol_pk primary key(gol_codigo),
	   constraint ju_gol_fk foreign key (ju_codigo) references jugador (ju_codigo),
	   constraint par_gol_fk foreign key (par_codigo) references partido (par_codigo)
	);


	/*******************************INSERTS*****************************************/

	--------------------------EQUIPO------------------------------------------------
	insert  into equipo (eq_codigo,eq_nombre)
	values(1,'Cali');
	insert  into equipo (eq_codigo,eq_nombre)
	values(2,'America');
	insert  into equipo (eq_codigo,eq_nombre)
	values(3,'Nacional');

	select * from equipo;

	--------------------------VISITANTE-LOCAL---------------------------------------
	insert  into vis_loc (vis_loc_codigo,vis_loc_nombre)
	values(1,'Local');
	insert  into vis_loc (vis_loc_codigo,vis_loc_nombre)
	values(2,'Visitante');

	select * from vis_loc;

	--------------------------PARTIDO-----------------------------------------------
	insert  into partido (par_codigo,fecha,eq_codigo,vis_loc_codigo,n_partido)
	values(1,'21/04/2021',1,1,1);
	insert  into partido (par_codigo,fecha,eq_codigo,vis_loc_codigo,n_partido)
	values(2,'21/04/2021',2,2,1);
	insert  into partido (par_codigo,fecha,eq_codigo,vis_loc_codigo,n_partido)
	values(3,'26/04/2021',1,2,2);
	insert  into partido (par_codigo,fecha,eq_codigo,vis_loc_codigo,n_partido)
	values(4,'26/04/2021',3,1,1);
	insert  into partido (par_codigo,fecha,eq_codigo,vis_loc_codigo,n_partido)
	values(5,'29/04/2021',2,2,2);
	insert  into partido (par_codigo,fecha,eq_codigo,vis_loc_codigo,n_partido)
	values(6,'29/04/2021',1,1,2);


	select * from partido;

	--------------------------JUGADOR-----------------------------------------------
	insert  into jugador (ju_codigo,eq_codigo,ju_nombres,ju_apellidos)
	values(1,1,'Gaston','Rodriguez');
	insert  into jugador (ju_codigo,eq_codigo,ju_nombres,ju_apellidos)
	values(2,2,'Adrian','Ramos');
	insert  into jugador (ju_codigo,eq_codigo,ju_nombres,ju_apellidos)
	values(3,3,'Jefferson','Duque');

	select * from jugador;

	--------------------------------PUNTOS------------------------------------------
	insert  into puntos (pun_codigo,descripcion,puntos)
	values(1,'ganado',3);
	insert  into puntos (pun_codigo,descripcion,puntos)
	values(2,'empatado',1);
	insert  into puntos (pun_codigo,descripcion,puntos)
	values(3,'perdido',0);

	select * from puntos;

	--------------------------------RESULTADO---------------------------------------
	insert  into resultado (res_codigo,par_codigo,eq_codigo,pun_codigo)
	values(1,1,1,1);
	insert  into resultado (res_codigo,par_codigo,eq_codigo,pun_codigo)
	values(2,1,1,2);
	insert  into resultado (res_codigo,par_codigo,eq_codigo,pun_codigo)
	values(3,2,2,3);
	insert  into resultado (res_codigo,par_codigo,eq_codigo,pun_codigo)
	values(4,2,2,2);
	insert  into resultado (res_codigo,par_codigo,eq_codigo,pun_codigo)
	values(5,3,3,1);
	insert  into resultado (res_codigo,par_codigo,eq_codigo,pun_codigo)
	values(6,3,3,2);


	select * from resultado;

	--------------------------------GOLES-------------------------------------------
	insert  into goles (gol_codigo,ju_codigo,par_codigo,gol_cant)
	values(1,1,1,3);
	insert  into goles (gol_codigo,ju_codigo,par_codigo,gol_cant)
	values(2,2,2,2);
	insert  into goles (gol_codigo,ju_codigo,par_codigo,gol_cant)
	values(3,3,3,1);
	insert  into goles (gol_codigo,ju_codigo,par_codigo,gol_cant)
	values(4,1,1,1);
	insert  into goles (gol_codigo,ju_codigo,par_codigo,gol_cant)
	values(5,2,2,4);
	insert  into goles (gol_codigo,ju_codigo,par_codigo,gol_cant)
	values(6,2,2,1);


	select * from goles;

	/*******************************TABLA*****************************************/
	SELECT SUM(P.PUNTOS) PUNTOS,EQ.EQ_NOMBRE, COUNT(DECODE(P.PUNTOS,3,PUNTOS )) PG,
	COUNT(DECODE(P.PUNTOS,1,PUNTOS )) PE,COUNT(DECODE(P.PUNTOS,0,PUNTOS )) PP,COUNT(PUNTOS ) PJ,
	COUNT(G.GOL_CANT) GF
	FROM RESULTADO R
	INNER JOIN PUNTOS P ON R.PUN_CODIGO = P.PUN_CODIGO 
	INNER JOIN PARTIDO PAR ON PAR.PAR_CODIGO = PAR.PAR_CODIGO 
	INNER JOIN EQUIPO EQ ON R.EQ_CODIGO = EQ.EQ_CODIGO 
	INNER JOIN JUGADOR JU ON JU.EQ_CODIGO = EQ.EQ_CODIGO 
	INNER JOIN GOLES G ON G.ju_codigo = JU.ju_codigo
	WHERE PAR.PAR_CODIGO = R.PAR_CODIGO
	GROUP BY PAR.N_PARTIDO,EQ.EQ_NOMBRE
	ORDER BY PUNTOS DESC
```