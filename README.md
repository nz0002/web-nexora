# 🚀 Nexora SaaS - Guía de Despliegue en Producción

Nexora es una plataforma SaaS de gestión empresarial con arquitectura **Local-First** (frontend puro que almacena de forma segura los datos en el navegador del usuario). Esto significa que **no requiere base de datos ni backend para funcionar en producción**.

El proyecto está 100% optimizado para ser desplegado en servicios de hosting estático gratuitos y ultrarrápidos como **Vercel**, **Netlify** o **GitHub Pages**.

---

## 📂 Estructura del Proyecto

El código final es limpio, nativo y no requiere dependencias complejas de Node.js para compilar (Zero-Build).

```text
/
├── index.html       # Landing Page de Marketing (Pública)
├── app.html         # Aplicación SaaS (Privada / Multitenant)
├── vercel.json      # Configuración de despliegue y seguridad para Vercel
├── .env.example     # Plantilla de variables de entorno futuras
├── .gitignore       # Reglas para repositorios Git
└── README.md        # Documentación (este archivo)
```

---

## 🛠 Cómo Desplegar en Vercel (Recomendado)

Vercel es la plataforma ideal para este proyecto gracias a su velocidad global (CDN edge) y configuración automática.

### Método 1: Despliegue Directo vía GitHub (Recomendado)

1. Sube este proyecto a tu cuenta de GitHub:
   ```bash
   git init
   git add .
   git commit -m "Initial commit: Nexora SaaS v1.0"
   git branch -M main
   git remote add origin https://github.com/TU_USUARIO/nexora-saas.git
   git push -u origin main
   ```
2. Entra en [Vercel.com](https://vercel.com) e inicia sesión con tu cuenta de GitHub.
3. Haz clic en **"Add New..."** > **"Project"**.
4. Importa el repositorio `nexora-saas` desde tu lista de GitHub.
5. En la sección "Framework Preset", asegúrate de que esté marcado como **"Other"** (ya que es HTML puro).
6. **Importante:** Deja las configuraciones de Build ("Build Command" y "Output Directory") vacías o con su valor por defecto.
7. Haz clic en **Deploy**. En menos de 30 segundos, tu aplicación estará online y lista para usarse.

### Método 2: Despliegue Manual con Vercel CLI

Si prefieres desplegar directamente desde tu terminal sin GitHub:

1. Instala Vercel CLI globalmente (requiere Node.js instalado):
   ```bash
   npm i -g vercel
   ```
2. Inicia sesión en Vercel:
   ```bash
   vercel login
   ```
3. Ejecuta el comando de despliegue dentro de esta misma carpeta:
   ```bash
   vercel --prod
   ```
4. Sigue las instrucciones en la consola (acepta la configuración por defecto presionando Enter).
5. Obtendrás una URL de producción inmediata.

---

## ⚙️ Configuración y Seguridad (vercel.json)

El proyecto incluye un archivo `vercel.json` preconfigurado. Este archivo se encarga de:
- **Clean URLs (`"cleanUrls": true`)**: Permite que tus usuarios accedan a `tudominio.com/app` en lugar de `tudominio.com/app.html`, dándole un aspecto mucho más profesional.
- **Seguridad (Headers)**: Protege la aplicación contra ataques comunes (Clickjacking, XSS) mediante cabeceras de respuesta estrictas.
- **Caché Eficiente**: Los archivos estáticos se cachean automáticamente para que la app cargue de forma instantánea.

---

## 🔐 Modo Administrador Global

Una vez que la aplicación esté online, podrás gestionar a los clientes que se registren. Accede a la URL de tu aplicación (ej. `https://nexora-saas.vercel.app/app`), e inicia sesión con las credenciales automáticas:

- **Email**: `admin@nexora.com`
- **Contraseña**: `admin_nexora_secure`

Desde este panel podrás ver los Workspaces creados y aprobar solicitudes de subida de plan (Pro, Growth, etc.).

---

## 🔄 Integración Futura de Base de Datos (Next Steps)

Actualmente, Nexora almacena la información por usuario/empresa en el `localStorage`. Esto es ideal para una versión MVP de alta privacidad (los datos no salen del dispositivo del usuario). 

Cuando desees escalar y guardar la información en la nube para que se sincronice entre dispositivos:
1. Revisa el archivo `.env.example` para configurar un backend.
2. Puedes conectar la lógica actual de guardado (ver funciones `saveData()` y `loadWorkspaceData()` en `app.html`) directamente a bases de datos como **Supabase** o **Firebase**, reemplazando las llamadas locales por peticiones HTTP sencillas.

**¡Nexora está lista para conquistar el mercado!** 🚀
