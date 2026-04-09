# 🚀 Entorno de Desarrollo Profesional: Web IA 2026

Este entorno está configurado para el desarrollo de aplicaciones de alto rendimiento con **Laravel 12** y herramientas de **Inteligencia Artificial** integradas. Funciona mediante **Dev Containers** para garantizar que el entorno sea idéntico en cualquier máquina.

---

## 🛠️ Stack Tecnológico
* [cite_start]**Lenguaje:** PHP 8.3 [cite: 1]
* **Framework:** Laravel 12 (Soporte completo)
* [cite_start]**Base de Datos:** MySQL 8.4, PostgreSQL 16 [cite: 1]
* [cite_start]**Runtime JS:** Node.js 20 LTS [cite: 1, 2]
* [cite_start]**Caché/Queues:** Redis 7 [cite: 1]
* [cite_start]**Gestores:** Composer & NPM [cite: 1, 2]

---

## 🤖 Configuración de Herramientas de IA
Este contenedor permite usar IAs de primer nivel sin necesidad de gestionar manualmente API Keys, utilizando **autenticación por sesión**.

### 1. Activar Gemini (Google Cloud CLI)
Para habilitar el uso de modelos de Google:
1.  Abre la terminal en VS Code (`Ctrl + ñ`).
2.  Ejecuta: `gcloud auth application-default login`
3.  Sigue el enlace en tu navegador, inicia sesión y pega el código resultante en la terminal.

### 2. Activar Codex/Copilot (GitHub CLI)
Para habilitar las herramientas de GitHub:
1.  Ejecuta: `gh auth login`
2.  Selecciona: `GitHub.com` > `HTTPS` > `Login with a web browser`.
3.  Copia el código de 8 dígitos y pégalo en la ventana del navegador que se abrirá.

### 3. Uso de Aider (Asistente de Programación)
**Aider** es el asistente principal de este entorno. Puede crear archivos y refactorizar código automáticamente.
* Para iniciar con Gemini: `aider --model gemini/gemini-1.5-pro`
* Para iniciar con Qwen (vía LiteLLM): `aider --model openai/qwen-2.5-coder`

---

## 📂 Gestión del Proyecto "marcado"

### Crear el proyecto desde cero
Si aún no has creado el proyecto, ejecuta dentro de la terminal del contenedor:
```bash
composer create-project laravel/laravel marcado
cd marcado
npm install
php artisan migrate
```
---

Persistencia de Datos
Todo el trabajo se guarda automáticamente en tu ruta local:
/home/emercado/emercado_data/Cursos/2026/web-IA

Los datos de MySQL, PostgreSQL y tus sesiones de IA persistirán aunque el contenedor se detenga o se reconstruya.

🔌 Acceso a Bases de Datos
Puedes gestionar las bases de datos directamente desde la barra lateral de VS Code con la extensión SQLTools ya preconfigurada:

MySQL: Host: mysql | User: root | Pass: root

Postgres: Host: postgres | User: root | Pass: root

📝 Comandos de Mantenimiento
Reinstalar dependencias: composer install o npm install.

Compilar assets (Vite): npm run dev.

Actualizar modelos locales: ollama pull qwen2.5-coder.

---

💾 Persistencia de Datos
Gracias a la configuración de volúmenes, los siguientes datos no se perderán si borras el contenedor:

Código Fuente: Localizado en tu carpeta /home/emercado/.../web-IA.

Bases de Datos: Los datos de MySQL y Postgres se guardan en volúmenes internos de Docker.

Sesiones de IA: Tus logins de gcloud y gh se mantienen activos.

Nota Pro: Si necesitas formatear o limpiar las bases de datos totalmente, usa:
docker-compose down -v (Cuidado: esto borrará todos los registros de las tablas).

📂 Estructura de Rutas configurada
El contenedor está vinculado estrictamente a:
/home/emercado/emercado_data/Cursos/2026/web-IA

Cualquier archivo fuera de esa ruta no será visible dentro del Dev Container.

---
