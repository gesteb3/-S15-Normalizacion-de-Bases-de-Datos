# Normalización de la Tabla `Registro_Cursos`

## 🎯 **Objetivo**
Aplicar los principios de normalización de bases de datos relacionales hasta la Tercera Forma Normal (3NF), estructurando la información de manera que los datos sean consistentes, no redundantes y fáciles de mantener.

---

## 📘 **Contexto**
La universidad registra información sobre cursos, profesores y estudiantes en una sola tabla llamada `Registro_Cursos`.  
El formato actual es el siguiente:

| ID_Registro | Curso             | Profesor      | Email_Profesor     | Estudiantes              | Emails_Estudiantes                       | Créditos | Facultad     |
|--------------|-------------------|----------------|--------------------|--------------------------|------------------------------------------|-----------|---------------|
| 1 | Bases de Datos | Ana Torres | ana@uni.edu | Luis, María, Jorge | luis@uni.edu, maria@uni.edu, jorge@uni.edu | 4 | Ingeniería |
| 2 | Programación Web | Carlos López | carlos@uni.edu | Pedro, Ana, Lucía | pedro@uni.edu, ana@uni.edu, lucia@uni.edu | 5 | Ingeniería |

---

## 🔍 **Análisis Inicial (0NF)**
En su estado actual, la tabla **no está normalizada (0NF)**.

**Problemas identificados:**
- Los campos `Estudiantes` y `Emails_Estudiantes` contienen **valores múltiples**.
- Existe **redundancia de datos** (la facultad se repite).
- Hay **dependencias múltiples** entre curso, profesor y estudiante.

> La estructura no cumple con las condiciones de una base de datos bien estructurada.

---

## 🧩 **Primera Forma Normal (1NF)**

### 📖 Reglas:
1. Cada campo debe contener **solo un valor atómico**.  
2. Cada registro debe ser **único** e identificable por una clave primaria.

### 🔧 Aplicación:
Se separan los valores múltiples de estudiantes y correos en registros individuales.

### 📋 Estructura (1NF)

| ID_Registro | Curso | Profesor | Email_Profesor | Estudiante | Email_Estudiante | Créditos | Facultad |
|--------------|--------|-----------|----------------|-------------|------------------|-----------|-----------|
| 1 | Bases de Datos | Ana Torres | ana@uni.edu | Luis | luis@uni.edu | 4 | Ingeniería |
| 1 | Bases de Datos | Ana Torres | ana@uni.edu | María | maria@uni.edu | 4 | Ingeniería |
| 1 | Bases de Datos | Ana Torres | ana@uni.edu | Jorge | jorge@uni.edu | 4 | Ingeniería |
| 2 | Programación Web | Carlos López | carlos@uni.edu | Pedro | pedro@uni.edu | 5 | Ingeniería |
| 2 | Programación Web | Carlos López | carlos@uni.edu | Ana | ana@uni.edu | 5 | Ingeniería |
| 2 | Programación Web | Carlos López | carlos@uni.edu | Lucía | lucia@uni.edu | 5 | Ingeniería |

---

## 🧱 **Segunda Forma Normal (2NF)**

### 📖 Reglas:
1. Debe estar en **1NF**.  
2. Todos los atributos **no clave** deben depender **completamente** de la clave primaria.

### 🔧 Aplicación:
Se eliminan las dependencias parciales separando las entidades `Profesor`, `Curso` y `Registro_Estudiante`.

### 📋 Estructura (2NF)

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

---

## 🧮 **Tercera Forma Normal (3NF)**

### 📖 Reglas:
1. Debe estar en **2NF**.  
2. No deben existir **dependencias transitivas**.

### 🔧 Aplicación:
Se crea una tabla adicional `Facultad` para eliminar dependencias transitivas.

### 📋 Estructura (3NF)

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

---

## 🧾 **Conclusión**
El modelo evolucionó desde una tabla única y redundante a un conjunto de tablas normalizadas que representan las entidades `Facultad`, `Profesor`, `Curso` y `Estudiante`.  
Gracias a la normalización:
- Se eliminaron duplicaciones y dependencias innecesarias.  
- Se mejoró la integridad de los datos.  
- Se facilita la actualización y mantenimiento del sistema.  

La normalización permite una base de datos **más limpia, eficiente y coherente**.
