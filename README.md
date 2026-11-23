# Zetros ELS-Kaufmann v3

Instalación nueva con 70 ítems, 24 secciones numeradas y 96 fotos de referencia. La publicación usa un Worker y una base D1 nuevos. La base comienza sin avances ni comentarios.

## 1. Sube todo en un solo commit con GitHub Desktop

1. Extrae el ZIP. Abre la carpeta extraída y localiza la carpeta que contiene `wrangler.jsonc`, `package.json`, `public`, `scripts` y `src`.
2. Instala [GitHub Desktop](https://desktop.github.com/) e inicia sesión con tu cuenta de GitHub.
3. En GitHub Desktop, abre **File → New repository**. Escribe `zetros-els-kaufmann-v3` y pulsa **Create repository**.
4. Pulsa **Repository → Show in Explorer**. En la carpeta que se abre, pega todo el contenido de la carpeta del paso 1. Acepta reemplazar `.gitignore` o `README.md` si te lo pide.
5. Vuelve a GitHub Desktop. Abajo a la izquierda, en **Summary**, escribe `Tablero Zetros completo` y pulsa **Commit to main**.
6. Pulsa **Publish repository**. Mantén marcada **Keep this code private** y pulsa **Publish Repository**.

## 2. Publica en Cloudflare

En **Workers & Pages → Create application → GitHub**, selecciona el repositorio nuevo.

| Campo | Valor |
|---|---|
| Worker name | `zetros-els-kaufmann-v3` |
| Production branch | `main` |
| Root directory | Dejar vacío |
| Build command | Dejar vacío |
| Deploy command | `npm run deploy` |

Pulsa **Deploy**. El registro debe mostrar `Verificación correcta: 96 fotos de referencia y ambos logos.` y después `Success! Build completed`. Si falta una imagen, el despliegue se detiene y el registro indica su ruta. La configuración solicita una base D1 nueva llamada `zetros-ctz15-v3`.

## 3. Crea el enlace privado

Abre PowerShell y pega esta línea:

```powershell
$b = New-Object byte[] 32; $rng = [System.Security.Cryptography.RandomNumberGenerator]::Create(); $rng.GetBytes($b); $rng.Dispose(); [BitConverter]::ToString($b).Replace('-', '').ToLowerInvariant()
```

En el Worker nuevo, ve a **Settings → Runtime variables and secrets → Add variable**. Marca **Production** y **Secret**. En **Key**, escribe `ZETROS_ACCESS_KEY`. En **Value**, pega los 64 caracteres que generaste. Pulsa **Add variable and deploy**.

Abre una ventana de incógnito. Pega la URL nueva de Cloudflare, añade `/#acceso=` y pega la misma clave a continuación. Guarda el enlace completo antes de entrar. Escribe tu nombre y comprueba los 70 ítems, los dos logos y las fotos de **12.1** y **23.1**.

La sesión del navegador dura siete días. El equipo puede volver a entrar con el mismo enlace.
