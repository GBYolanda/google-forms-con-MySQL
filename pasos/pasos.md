
# 🌟 Cómo Crear un Formulario en Google Forms y Conectarlo a MySQL 🚀  

Este documento te guiará paso a paso para crear un formulario en Google Forms y conectarlo a una base de datos MySQL para almacenar las respuestas.  

---

## 📋 Pasos para Crear el Formulario  

1. **Accede a Google Forms** 📋:  
   - Ve a [Google Forms](https://forms.google.com).  
   - Inicia sesión con tu cuenta de Google.  

2. **Crea un nuevo formulario**:  
   - Haz clic en el botón de `+` para crear un formulario en blanco.  
   - Añade preguntas relevantes (texto, opciones múltiples, listas, etc.).  
   - Asigna un nombre y descripción al formulario.  

3. **Configura las opciones del formulario**:  
   - Ve a `Configuración` (ícono de engranaje):  
     - Activa la opción "Recolectar direcciones de correo electrónico" si es necesario.  
     - Decide si las respuestas serán anónimas o requerirán cuenta de Google.  
   - Guarda los cambios.  

---

## 🚀 Conectar Google Forms a MySQL  

1. **Configura un script de Google Apps** 📜:  
   - En tu formulario, ve a `Más > Editar script` (Google Apps Script).  
   - Copia y pega el siguiente código en el editor:  
     ```javascript
     function onFormSubmit(e) {
       const conn = Jdbc.getConnection("jdbc:mysql://<HOST>:<PUERTO>/<BASE_DATOS>", "<USUARIO>", "<CONTRASEÑA>");
       const stmt = conn.prepareStatement("INSERT INTO respuestas (campo1, campo2) VALUES (?, ?)");
       stmt.setString(1, e.values[0]);  // Primer campo
       stmt.setString(2, e.values[1]);  // Segundo campo
       stmt.execute();
       stmt.close();
       conn.close();
     }
     ```  
   - Configura los valores `<HOST>`, `<PUERTO>`, `<BASE_DATOS>`, `<USUARIO>` y `<CONTRASEÑA>`.  
   - Guarda el proyecto y autoriza los permisos necesarios.  

2. **Crea una base de datos en MySQL** 🗃️:  
   - Abre tu cliente MySQL y ejecuta:  
     ```sql
     CREATE DATABASE google_forms;
     USE google_forms;
     CREATE TABLE respuestas (
       id INT AUTO_INCREMENT PRIMARY KEY,
       campo1 VARCHAR(255),
       campo2 VARCHAR(255)
     );
     ```  

3. **Prueba la conexión**:  
   - Completa el formulario.  
   - Verifica que los datos aparezcan en la tabla `respuestas`.  

---

## 🧩 Consejos Útiles  

- Asegúrate de que tu base de datos sea accesible desde el script de Google Apps. Configura reglas de acceso en tu servidor MySQL.  
- Usa una VPN o IP pública para conectar Google Forms a servidores locales.  
- Considera usar conexiones cifradas con SSL.  

---

## 🛠️ Solución de Problemas  

- Si ves errores de conexión: Verifica las credenciales y la IP permitida.  
- Si los datos no se envían: Asegúrate de haber vinculado el script al evento `onFormSubmit`.  

---

✨ _Creado con pasión para simplificar procesos digitales._ ✨  
