# Sistema de Gestión AIR — TEC

Aplicación web para digitalizar los procesos de la **Asamblea Institucional Representativa (AIR)** del Instituto Tecnológico de Costa Rica: registro de asambleístas y nombramientos, normativa, sesiones y asistencia, votaciones, comisiones, certificaciones y reportes.

![Node.js](https://img.shields.io/badge/Node.js-Express-339933?logo=nodedotjs&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?logo=postgresql&logoColor=white)
![JWT](https://img.shields.io/badge/Auth-JWT-000000?logo=jsonwebtokens&logoColor=white)
![Metodología](https://img.shields.io/badge/metodolog%C3%ADa-sprints-1f4e79)

---

## Tabla de contenido

1. [Funcionalidades](#funcionalidades)
2. [Arquitectura](#arquitectura)
3. [Tecnologías](#tecnologías)
4. [Estructura del repositorio](#estructura-del-repositorio)
5. [Instalación y ejecución](#instalación-y-ejecución)
6. [Metodología de trabajo](#metodología-de-trabajo)
7. [Equipo](#equipo)

---

## Funcionalidades

| Módulo | Qué permite |
|--------|-------------|
| **Seguridad** | Inicio de sesión con JWT, contraseñas cifradas con bcrypt y permisos por rol (por ejemplo, `GESTIONAR_ASAMBLEISTAS`). |
| **Asambleístas y nombramientos** | Registro, edición y búsqueda de asambleístas por sector, con historial de nombramientos. |
| **Normativa** | Gestión de propuestas y elementos normativos, con notas legales condicionales según el origen de la propuesta. |
| **Sesiones** | Control de asistencia por sesión. |
| **Votaciones** | Tablero de votación para las propuestas. |
| **Comisiones** | Conformación y consulta de comisiones. |
| **Certificaciones** | Generación de certificaciones en PDF con hash SHA-256 para verificar que no fueron alteradas después de emitirse. |
| **Reportes** | Consultas y reportes de la actividad de la Asamblea. |

## Arquitectura

El proyecto sigue el patrón **MVC**:

- **Modelos** (`src/models`): consultas SQL a PostgreSQL.
- **Controladores** (`src/controllers`): lógica de negocio y rutas de la API.
- **Vistas** (`src/views`): páginas HTML de la interfaz.
- **Servicios** (`src/services`): generación de PDF, plantillas, hash criptográfico y reglas condicionales.

```
Navegador ──► Express (app.js) ──► Controladores ──► Modelos ──► PostgreSQL
                    │                     │
                    │                     └──► Servicios (PDF, SHA-256, plantillas)
                    └──► Vistas HTML
```

## Tecnologías

- **Backend:** Node.js, Express
- **Base de datos:** PostgreSQL (scripts organizados por sprint)
- **Seguridad:** JSON Web Tokens, bcryptjs, dotenv
- **Documentos:** PDFKit y Puppeteer para certificaciones en PDF
- **Herramientas:** Git, GitHub Projects, Nodemon
- **Desarrollo asistido por IA:** Claude Code y Codex

## Estructura del repositorio

```
Project-AIR/
├── app.js                  Punto de entrada y definición de rutas
├── project-air.sql         Script completo de la base de datos
├── database/
│   ├── schema.sql
│   ├── sprint2/            Catálogos, seguridad, asambleístas, normativa,
│   │                       nombramientos, permisos y comisiones
│   └── sprint3/            Reportes
├── docs/
│   └── diccionario-datos.md
├── src/
│   ├── config/             Conexión a la BD y configuración de seguridad
│   ├── controllers/        Auth, asambleístas, normativa, sesiones,
│   │                       votaciones, comisiones, certificaciones, reportes
│   ├── models/
│   ├── services/           PDFService, CryptoService, TemplateService,
│   │                       NotaCondicionalService
│   └── views/              Login, buscador, propuestas, asistencia,
│                           votaciones, comisiones, reportes, certificaciones
├── test/
└── REGLAS_GIT.md           Reglas de ramas, commits y Pull Requests
```

## Instalación y ejecución

**Requisitos:** Node.js 18 o superior, PostgreSQL y Git.

```bash
# 1. Clonar e instalar dependencias
git clone https://github.com/Ju4nj0s3MM/Project-AIR.git
cd Project-AIR
npm install

# 2. Crear la base de datos y cargar el esquema
psql -U postgres -c "CREATE DATABASE air;"
psql -U postgres -d air -f project-air.sql

# 3. Configurar variables de entorno
cp .env.example .env
# Completar DB_HOST, DB_PORT, DB_NAME, DB_USER, DB_PASSWORD,
# JWT_SECRET, JWT_EXPIRES_IN y PORT

# 4. Iniciar el servidor
npm run dev      # con recarga automática
# o
npm start
```

Abrir <http://localhost:3000> (o el puerto configurado) e iniciar sesión.

## Metodología de trabajo

El equipo trabajó por **sprints** con un tablero en **GitHub Projects** (Backlog → Ready for Sprint → In Progress → In Review → Done):

- **Ramas:** `main` (versión final), `develop` (integración del sprint) y `feature/issue-N-descripcion` por cada issue.
- **Commits** con [Conventional Commits](https://www.conventionalcommits.org/es/): `feat`, `fix`, `db` y `docs`, indicando el módulo.
- **Pull Requests** revisados por el líder, con `Closes #N` para cerrar el issue automáticamente.
- **Límite de trabajo en curso:** máximo 2 issues por persona en *In Progress*.

El detalle completo está en [`REGLAS_GIT.md`](REGLAS_GIT.md).

## Equipo

| Integrante |
|------------|
| Juan José Morales Montero |
| Jimena Fernández Castillo |
| Mauricio Membreño Artavia |

---

Proyecto académico · Instituto Tecnológico de Costa Rica
