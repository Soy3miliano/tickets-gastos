# Bitácora de Registro de Tickets

Una aplicación web ligera (de un solo archivo HTML) diseñada para digitalizar, organizar y respaldar tus tickets de gastos. Utiliza la Inteligencia Artificial de Google (Gemini) para extraer los datos de la imagen automáticamente y guarda una copia de la foto directamente en tu Google Drive. Al final, puedes exportar todos tus registros a Excel.

Todo se procesa de manera segura y local en tu navegador; no requiere instalación de bases de datos ni servidores backend.

## Características
- OCR con Inteligencia Artificial: Extrae fecha, monto, concepto y ciudad usando `gemini-3.5-flash-lite`.
- Sincronización con Google Drive: Crea automáticamente una carpeta llamada `TicketsGastos` en tu Drive y sube las fotos allí.
- Exportación a Excel: Descarga tu tabla de gastos en formato `.xlsx` con enlaces directos a las fotos en Drive.
- Privacidad Total: Tus claves de API y Client IDs se guardan exclusivamente en el `localStorage` de tu navegador.

---

## Cómo usar este proyecto de manera local

Como la aplicación interactúa con las APIs de Google (Drive y Gemini), necesitas servir el archivo desde un servidor local para evitar problemas de permisos cruzados (CORS) y restricciones del protocolo `file://`.

1. Clona este repositorio o descarga el archivo `.html`.
2. Abre la carpeta del proyecto en tu editor de código (ej. Visual Studio Code).
3. Inicia un servidor local. Si usas VS Code, la forma más fácil es instalar la extensión Live Server y hacer clic en Go Live.
4. Abre la dirección de tu servidor local en el navegador (usualmente `http://127.0.0.1:5500`).

---

## Configuración de las APIs

Para que la aplicación funcione, el usuario final debe configurar sus propias credenciales directamente en la interfaz de la página web (Paso 1). Las credenciales se quedan guardadas en el navegador de forma segura.

### 1. API Key de Google Gemini (Para leer los tickets)
1. Entra a Google AI Studio (https://aistudio.google.com/app/apikey).
2. Inicia sesión con una cuenta de Google y haz clic en Create API key.
3. Copia la clave generada y pégala en el campo de Configurar Inteligencia Artificial en la aplicación.

### 2. Client ID de Google Drive (Para guardar las fotos)
1. Entra a Google Cloud Console (https://console.cloud.google.com/).
2. Crea un proyecto nuevo.
3. Ve a APIs y servicios > Biblioteca y activa la Google Drive API.
4. Ve a Pantalla de consentimiento OAuth, elige "Externo" y añade tu correo electrónico en la sección de "Usuarios de prueba".
5. Ve a Credenciales > Crear credenciales > ID de cliente de OAuth. Elige "Aplicación web".
6. En Orígenes de JavaScript autorizados, añade la URL desde donde estás corriendo el archivo (ej. `http://localhost`, `http://127.0.0.1:5500` o la URL de tu GitHub Pages si lo publicas).
7. Copia el Client ID (termina en `.apps.googleusercontent.com`) y pégalo en la aplicación web.

---

## Personalización del Código

### Cambiar el formato del nombre de archivo (Matrícula/Identificador)
Por defecto, la aplicación renombra las fotos de los tickets antes de subirlas a Google Drive usando un formato específico que incluye la matrícula A07106914, el mes, el año y un identificador único (ej. A07106914_Agosto2026_167234901.jpg).

Si quieres usar este proyecto y cambiar ese identificador por tu propia matrícula, tu nombre o un código de empleado, sigue estos pasos:

1. Abre el archivo `.html` en tu editor de texto.
2. Presiona Ctrl + F (o Cmd + F en Mac) y busca la siguiente línea de código:
   ```javascript
   const fileName = `A07106914_${mesActual}${anioActual}_${Date.now()}.jpg`;
