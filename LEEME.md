# PrecioVecino v4 con Gemini: cómo publicar en Netlify

Contenido de la carpeta:
- `index.html`: la app
- `formulario.html`: formulario oculto para la encuesta de Netlify
- `netlify.toml`: le dice a Netlify dónde está la función
- `netlify/functions/analizar.mjs`: llama a Gemini. La clave nunca va en la página.

## Pasos
1. Sube esta carpeta a un repositorio de GitHub. Otra opción es la terminal: `npm i -g netlify-cli`, luego `netlify deploy --prod`. Si solo arrastras la carpeta en la web de Netlify, la función no se publica.
2. En Netlify, entra a Add new site → Import from Git y elige el repositorio.
3. En Site configuration → Environment variables, agrega:
   - `GEMINI_API_KEY` = tu clave de Google AI Studio (márcala como secreta: "Contains secret values")
   - `GEMINI_MODEL` (opcional) = el modelo que quieras. Si no la pones, se usa `gemini-2.5-flash`.
4. Ve a Deploys → Trigger deploy para que tome las variables.
5. Prueba desde el celular: toma foto de 2 productos y toca "Reconocer productos".

## Seguridad incluida
- La clave vive solo en Netlify. No está en la página ni en GitHub.
- La función solo acepta peticiones desde tu propio sitio.
- Límite de 20 consultas por hora por persona (IP).
- Se aceptan máximo 4 fotos, de máximo 1.5 MB cada una y solo en JPEG, PNG o WebP.
- El perfil de salud nunca se envía. Se queda en el teléfono.

## Recomendado en Google
- En Google AI Studio / Cloud Console, pon un tope de gasto o usa la cuota gratuita.
- No subas la clave a GitHub ni la pegues en chats. Si se filtra, bórrala y crea otra.
- La cuota gratuita de Gemini puede usar tus datos para mejorar sus modelos. Para datos reales de usuarios, usa un plan de pago.
