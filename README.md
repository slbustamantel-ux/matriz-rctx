# Matriz de visita áulica RCTX · Eight Academy

Aplicación web del Departamento de Planificación para registrar visitas áulicas con la matriz optimizada de 18 indicadores (100 puntos). Funciona en computadora y celular, y la usan personas **sin cuenta de Claude**: solo necesitan una cuenta de Google autorizada.

Los datos se guardan en Firebase (Firestore). Las fotografías (máximo 2 por visita) se comprimen y se guardan en Firestore, así que **no hace falta el plan de pago ni Cloud Storage**.

## Estructura

```
matriz-rctx-eight-academy/
├── docs/                  ← la página (GitHub Pages y Firebase Hosting la publican desde aquí)
│   ├── index.html
│   ├── firebase-config.js ← completar
│   ├── logo.png
│   └── .nojekyll
├── firestore.rules        ← completar el correo de administración
├── firestore.indexes.json
├── firebase.json
├── .firebaserc            ← completar el ID del proyecto (solo para la terminal)
├── .gitignore
└── README.md
```

## 1. Preparar Firebase (desde el navegador)

1. En <https://console.firebase.google.com> abre tu proyecto (puede ser el mismo de la bitácora).
2. **Authentication › Método de acceso**: habilita **Google**.
3. **Firestore Database**: créala si aún no existe (modo producción).
4. **Configuración del proyecto › Tus apps**: si no hay una app web, crea una (ícono `</>`). Copia el bloque `firebaseConfig`.

## 2. Completar dos archivos

- `docs/firebase-config.js`: pega los valores de `firebaseConfig` y escribe el correo de administración en `ADMIN_EMAILS`.
- `firestore.rules`: reemplaza `reemplaza_correo_admin@eightacademy.edu.ec` por el mismo correo, **en minúsculas**.

## 3. Publicar las reglas de seguridad

Firestore › **Reglas**: pega el contenido de `firestore.rules` y pulsa **Publicar**.

> **Si el proyecto es el mismo de la bitácora:** no borres sus reglas. Copia solo el bloque entre `MATRIZ RCTX (inicio)` y `MATRIZ RCTX (fin)` y pégalo dentro de las reglas existentes, antes de la última llave de cierre. Las colecciones de la matriz empiezan con `rctx_`, así que no se mezclan con las de la bitácora.

## 4. Publicar la página

### Opción A: GitHub Pages (sin terminal)
1. Sube todos los archivos al repositorio (Add file › Upload files), incluida la carpeta `docs`.
2. **Settings › Pages**: Source = *Deploy from a branch*, Branch = `main`, carpeta = **/docs**. Guarda.
3. La dirección será `https://TU_USUARIO.github.io/NOMBRE_DEL_REPOSITORIO/`.
4. Firebase › **Authentication › Configuración › Dominios autorizados**: agrega `TU_USUARIO.github.io`.

Para GitHub Pages gratuito el repositorio debe ser público. Esto no expone datos: la página solo contiene el formulario; los registros están protegidos por el inicio de sesión y las reglas de Firestore.

### Opción B: Firebase Hosting (terminal)
```
npm install -g firebase-tools
firebase login
firebase deploy --only hosting,firestore
```
(Completa antes `.firebaserc` con el ID del proyecto.) La dirección será `https://ID_DEL_PROYECTO.web.app`.

## 5. Dar acceso al equipo

Ingresa con el correo de administración › **Ajustes › Acceso del equipo** y agrega cada correo de Google:

| Rol | Puede |
|---|---|
| Administración | Todo: registrar, editar, eliminar, gestionar accesos, listas y logo |
| Editor | Registrar y editar visitas, subir fotografías |
| Lector | Consultar registros, docentes y tablero |

Luego comparte la dirección de la página. Quien no tenga acceso verá el aviso «Sin acceso».

## Escala de calificación

Puntaje del indicador = puntaje máximo × factor (Cumple 100 %, En proceso 50 %, No cumple 0 %).
Satisfactorio ≥ 90 · Conforme 70–89.99 · Insatisfactorio < 70.
