# 🐘 Python + PostgreSQL: Capa de Datos con Pool de Conexiones

Proyecto de la **Sección 29 – Conexión a PostgreSQL** del curso *Universidad Python: De Cero a Experto* (Udemy).

Implementa una **capa de datos** en Python que se conecta a PostgreSQL con `psycopg2`, usando un **pool de conexiones**, el patrón **DAO** (Data Access Object) y manejo automático de **transacciones** con un *context manager*. Incluye un CRUD para dos tablas (`persona` y `usuario`) y un menú interactivo en consola.

---

## 🚀 Funcionalidades

- **Pool de conexiones** con `psycopg2.pool.SimpleConnectionPool` (mínimo 1, máximo 5 conexiones)
- **Context manager** (`with`) que obtiene una conexión del pool, hace `commit` si todo sale bien o `rollback` si ocurre un error, y la regresa al pool
- **CRUD completo** (Create, Read, Update, Delete) para las tablas `persona` y `usuario`
- **Consultas parametrizadas** (`%s`) para prevenir inyección SQL
- **Logging** centralizado a consola y al archivo `capa_datos.log`
- **Menú interactivo** en consola para administrar usuarios

---

## 🗂️ Estructura del proyecto

```
capa_datos_persona/
├── conexion.py          # Clase Conexion: crea y administra el pool de conexiones
├── cursor_del_pool.py   # Context manager: commit/rollback automático y liberación de la conexión
├── logger_base.py       # Configuración del logging (consola + archivo)
├── persona.py           # Clase de entidad Persona (encapsulamiento con @property)
├── persona_dao.py       # DAO con el CRUD de la tabla persona
├── usuario.py           # Clase de entidad Usuario
├── usuario_dao.py       # DAO con el CRUD de la tabla usuario
├── menu_app_usuario.py  # Aplicación de consola para administrar usuarios
├── .env.example        # Plantilla de variables de entorno (credenciales)
└── requirements.txt
```

---

## 🧱 Arquitectura

```
menu_app_usuario.py
        │
        ▼
  UsuarioDao / PersonaDAO     ← Lógica de acceso a datos (CRUD)
        │
        ▼
    CursorDelPool             ← with: commit / rollback automático
        │
        ▼
      Conexion                ← Pool de conexiones (psycopg2)
        │
        ▼
     PostgreSQL
```

---

## 🛠️ Tecnologías

- Python 3
- PostgreSQL
- psycopg2
- python-dotenv
- logging (biblioteca estándar)

---

## 🗄️ Base de datos

Base de datos: `test_db`

```sql
CREATE TABLE persona (
    id_persona SERIAL PRIMARY KEY,
    nombre     VARCHAR(50),
    apellido   VARCHAR(50),
    email      VARCHAR(100)
);

CREATE TABLE usuario (
    id_usuario SERIAL PRIMARY KEY,
    username   VARCHAR(50),
    password   VARCHAR(50)
);
```

---

## ▶️ Cómo ejecutarlo

1. Clonar el repositorio:
   ```bash
   git clone https://github.com/JosephCandor/python-postgresql-personas-db.git
   cd python-postgresql-personas-db
   ```
2. Crear y activar un entorno virtual:
   ```bash
   python -m venv .venv
   .venv\Scripts\activate        # Windows
   source .venv/bin/activate     # Linux / macOS
   ```
3. Instalar dependencias:
   ```bash
   pip install -r requirements.txt
   ```
4. Crear la base de datos `test_db` y las tablas en PostgreSQL (script de arriba).
5. Copiar `.env.example` como `.env` y escribir tus credenciales de PostgreSQL:
   ```bash
   copy .env.example .env        # Windows
   cp .env.example .env          # Linux / macOS
   ```
6. Ejecutar el menú:
   ```bash
   python menu_app_usuario.py
   ```

---

## 📚 Conceptos aprendidos

- Conexión a PostgreSQL con `psycopg2`
- Pool de conexiones y reutilización de conexiones
- Patrón DAO para separar la lógica de acceso a datos
- Context managers (`__enter__` / `__exit__`) para manejar transacciones
- `commit` y `rollback`
- Consultas parametrizadas contra inyección SQL
- Métodos de clase (`@classmethod`) y encapsulamiento con `@property`
- Logging a consola y archivo
- Variables de entorno con `python-dotenv` para no subir credenciales al repositorio

---

## 👤 Autor

**Joseph Candor** – [github.com/JosephCandor](https://github.com/JosephCandor)
