# ACTIVIDAD NUMERO 3
```sql
CREATE DATABASE Universidad;
USE Universidad;

-- Tabla de Estudiantes
CREATE TABLE datos (
    cedula INT PRIMARY KEY,
    p_nom VARCHAR(50) NOT NULL,
    s_nom VARCHAR(50),
    p_ape VARCHAR(50) NOT NULL,
    s_ape VARCHAR(50),
    f_nac DATE NOT NULL,
    correo VARCHAR(100) UNIQUE,
    tlf VARCHAR(20),
    direc TEXT,
    cod_carrera INT,
    f_ing DATE NOT NULL,
    FOREIGN KEY (cod_carrera) REFERENCES carreras(cod_carrera)
);

-- Tabla de Materias
CREATE TABLE materias (
    cod_materia INT PRIMARY KEY,
    materia VARCHAR(100) NOT NULL,
    uni_cred INT NOT NULL
);

-- Tabla de Carreras
CREATE TABLE carreras (
    cod_carrera INT PRIMARY KEY,
    carrera VARCHAR(100) NOT NULL
);

-- Tabla de Notas
CREATE TABLE notas (
    cedula INT,
    cod_materia INT,
    nota DECIMAL(4,2) NOT NULL,
    periodo_acad VARCHAR(10) NOT NULL,
    PRIMARY KEY (cedula, cod_materia, periodo_acad),
    FOREIGN KEY (cedula) REFERENCES datos(cedula),
    FOREIGN KEY (cod_materia) REFERENCES materias(cod_materia)
);

```

# ACTIVIDAD NUMERO 4


### **1. Insertar tres registros en las tablas `carreras`, `materias`, `datos` y `notas`**  

```sql
-- Insertar en la tabla carreras
INSERT INTO carreras (cod_carrera, carrera) VALUES (1, 'Ingeniería en Sistemas');
INSERT INTO carreras (cod_carrera, carrera) VALUES (2, 'Administración');
INSERT INTO carreras (cod_carrera, carrera) VALUES (3, 'Contaduría');

-- Insertar en la tabla materias
INSERT INTO materias (cod_materia, materia, uni_cred) VALUES (101, 'Matemáticas', 3);
INSERT INTO materias (cod_materia, materia, uni_cred) VALUES (102, 'Física', 4);
INSERT INTO materias (cod_materia, materia, uni_cred) VALUES (103, 'Química', 3);

-- Insertar en la tabla datos (estudiantes)
INSERT INTO datos (cedula, p_nom, s_nom, p_ape, s_ape, f_nac, correo, tlf, direc, cod_carrera, f_ing)
VALUES 
(12345678, 'Carlos', 'Andrés', 'Gómez', 'Pérez', '2000-05-15', 'carlos@gmail.com', '04141234567', 'Calle A, Caracas', 1, '2018-09-01'),
(87654321, 'María', 'José', 'Pérez', 'Rojas', '1999-08-22', 'maria@gmail.com', '04141239876', 'Calle B, Maracay', 2, '2017-09-01'),
(11223344, 'Luis', 'Fernando', 'Fernández', 'Díaz', '2001-02-10', 'luis@gmail.com', '04141233456', 'Calle C, Valencia', 3, '2019-09-01');

-- Insertar en la tabla notas
INSERT INTO notas (cedula, cod_materia, nota, periodo_acad)
VALUES 
(12345678, 101, 15.50, '2024-1'),
(87654321, 102, 18.75, '2024-1'),
(11223344, 103, 10.00, '2024-1');
```

---

### **2. Modificar una de las notas cargadas y cambiar el `p_nom` de un alumno específico**  

```sql
-- Modificar la nota del estudiante con cédula 12345678 en la materia 101
UPDATE notas SET nota = 17.80 WHERE cedula = 12345678 AND cod_materia = 101 AND periodo_acad = '2024-1';

-- Modificar el primer nombre de un alumno específico (ejemplo, cambiar "Carlos" por "Juan")
UPDATE datos SET p_nom = 'Juan' WHERE cedula = 12345678;
```

---

### **3. Eliminar un registro específico de las tablas `datos` y `notas`**  

```sql
-- Eliminar un registro específico de la tabla datos (ejemplo, eliminar al alumno con cédula 11223344)
DELETE FROM datos WHERE cedula = 11223344;

-- Eliminar un registro específico de la tabla notas (ejemplo, eliminar la nota del alumno 11223344)
DELETE FROM notas WHERE cedula = 11223344;
```

---

### **4. Consultar los registros de cada una de las tablas**  

```sql
-- Consultar todos los registros de la tabla carreras
SELECT * FROM carreras;

-- Consultar todos los registros de la tabla materias
SELECT * FROM materias;

-- Consultar todos los registros de la tabla datos (estudiantes)
SELECT * FROM datos;

-- Consultar todos los registros de la tabla notas
SELECT * FROM notas;
```

---

### **5. Buscar todas las notas mayores a 12**  

```sql
SELECT * FROM notas WHERE nota > 12;
```

---

### **6. Buscar un alumno en específico (ejemplo, por cédula)**  

```sql
SELECT * FROM datos WHERE cedula = 12345678;
```

# ACTIVIDAD NUMERO 5

```sql
SELECT 
    d.cedula, 
    d.p_nom, 
    d.p_ape, 
    c.carrera, 
    m.materia, 
    n.nota, 
    n.periodo_acad
FROM datos d
JOIN carreras c ON d.cod_carrera = c.cod_carrera
JOIN notas n ON d.cedula = n.cedula
JOIN materias m ON n.cod_materia = m.cod_materia;
```

Esta consulta:  
- Une la tabla `datos` con `carreras` para obtener la carrera del estudiante.  
- Une la tabla `datos` con `notas` para obtener las notas del estudiante.  
- Une la tabla `notas` con `materias` para obtener la materia correspondiente.  
- Retorna solo los campos requeridos: `cedula`, `p_nom`, `p_ape`, `carrera`, `materia`, `nota` y `periodo_acad`.  

---

### **2. Pregunta personal**  

* Personalmente, me pareció excelente el contenido para introducirse en el mundo de las bases de datos relacionales. Considero que la información está bien organizada, es clara y fácil de comprender, lo que facilita el aprendizaje incluso para quienes no tienen experiencia previa en el tema. Me pareció muy práctico, con ejemplos bien planteados que permiten aplicar los conceptos de manera efectiva.

En mi caso, ya tengo varios años de experiencia en el mundo laboral de la programación y estoy familiarizado con este tipo de bases de datos, por lo que no me resultó complicado realizar las prácticas propuestas. Sin embargo, me pareció interesante la manera en que se abordaron los temas y la metodología utilizada para transmitir los conocimientos.

## participantes:

- Relly Garcia, C.I: 27561321
- Mauricio Freites, C.I: 19202051
- Cleismer Guerra, C.I: 29697213
