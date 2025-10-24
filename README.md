# Normalización de base de datos


---

##  **Contexto**
La universidad registra información sobre cursos, profesores y estudiantes en una sola tabla llamada `Registro_Cursos`.  
El formato actual es el siguiente:

| ID_Registro | Curso             | Profesor      | Email_Profesor     | Estudiantes              | Emails_Estudiantes                       | Créditos | Facultad     |
|--------------|-------------------|----------------|--------------------|--------------------------|------------------------------------------|-----------|---------------|
| 1 | Bases de Datos | Ana Torres | ana@uni.edu | Luis, María, Jorge | luis@uni.edu, maria@uni.edu, jorge@uni.edu | 4 | Ingeniería |
| 2 | Programación Web | Carlos López | carlos@uni.edu | Pedro, Ana, Lucía | pedro@uni.edu, ana@uni.edu, lucia@uni.edu | 5 | Ingeniería |


##  **Primera forma normal (1NF)**


###  Estructura (1NF)

| ID_Registro | Curso | Profesor | Email_Profesor | Estudiante | Email_Estudiante | Créditos | Facultad |
|--------------|--------|-----------|----------------|-------------|------------------|-----------|-----------|
| 1 | Bases de Datos | Ana Torres | ana@uni.edu | Luis | luis@uni.edu | 4 | Ingeniería |
| 1 | Bases de Datos | Ana Torres | ana@uni.edu | María | maria@uni.edu | 4 | Ingeniería |
| 1 | Bases de Datos | Ana Torres | ana@uni.edu | Jorge | jorge@uni.edu | 4 | Ingeniería |
| 2 | Programación Web | Carlos López | carlos@uni.edu | Pedro | pedro@uni.edu | 5 | Ingeniería |
| 2 | Programación Web | Carlos López | carlos@uni.edu | Ana | ana@uni.edu | 5 | Ingeniería |
| 2 | Programación Web | Carlos López | carlos@uni.edu | Lucía | lucia@uni.edu | 5 | Ingeniería |

### Aplicación:
Se separan los valores múltiples de estudiantes y correos en registros individuales.
---

## **Segunda forma normal (2NF)**

### Estructura (2NF)

**Tabla: Profesor**
| ID_Profesor | Nombre_Profesor | Email_Profesor |
|--------------|----------------|----------------|
| 1 | Ana Torres | ana@uni.edu |
| 2 | Carlos López | carlos@uni.edu |

**Tabla: Curso**
| ID_Curso | Nombre_Curso | Créditos | Facultad | ID_Profesor |
|-----------|----------------|-----------|-----------|--------------|
| 1 | Bases de Datos | 4 | Ingeniería | 1 |
| 2 | Programación Web | 5 | Ingeniería | 2 |

**Tabla: Registro_Estudiante**
| ID_Curso | Estudiante | Email_Estudiante |
|-----------|-------------|------------------|
| 1 | Luis | luis@uni.edu |
| 1 | María | maria@uni.edu |
| 1 | Jorge | jorge@uni.edu |
| 2 | Pedro | pedro@uni.edu |
| 2 | Ana | ana@uni.edu |
| 2 | Lucía | lucia@uni.edu |

### Aplicación:
Se eliminan las dependencias parciales separando las entidades `Profesor`, `Curso` y `Registro_Estudiante`.
---

##  **Tercera forma normal (3NF)**

### Estructura (3NF)

**Tabla: Facultad**
| ID_Facultad | Nombre_Facultad |
|--------------|----------------|
| 1 | Ingeniería |

**Tabla: Profesor**
| ID_Profesor | Nombre_Profesor | Email_Profesor |
|--------------|----------------|----------------|
| 1 | Ana Torres | ana@uni.edu |
| 2 | Carlos López | carlos@uni.edu |

**Tabla: Curso**
| ID_Curso | Nombre_Curso | Créditos | ID_Profesor | ID_Facultad |
|-----------|----------------|-----------|--------------|--------------|
| 1 | Bases de Datos | 4 | 1 | 1 |
| 2 | Programación Web | 5 | 2 | 1 |

**Tabla: Estudiante**
| ID_Estudiante | Nombre_Estudiante | Email_Estudiante |
|----------------|------------------|------------------|
| 1 | Luis | luis@uni.edu |
| 2 | María | maria@uni.edu |
| 3 | Jorge | jorge@uni.edu |
| 4 | Pedro | pedro@uni.edu |
| 5 | Ana | ana@uni.edu |
| 6 | Lucía | lucia@uni.edu |

**Tabla: Registro_Estudiante**
| ID_Curso | ID_Estudiante |
|-----------|----------------|
| 1 | 1 |
| 1 | 2 |
| 1 | 3 |
| 2 | 4 |
| 2 | 5 |
| 2 | 6 |

### Aplicación:
Se crea una tabla adicional `Facultad` para eliminar dependencias transitivas.
---

## **Conclusión**
El modelo se transformó en un conjunto de tablas normalizadas que representan las entidades `Facultad`, `Profesor`, `Curso` y `Estudiante`.  
Gracias a la normalización:
- Se eliminaron duplicaciones y dependencias innecesarias.  
- Se mejoró la integridad de los datos.  

