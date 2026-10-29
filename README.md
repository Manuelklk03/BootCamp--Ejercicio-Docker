# Docker — Dockeriza tu proyecto Web Minimalista

## Introducción

En esta práctica vas a utilizar el proyecto **Web Minimalista** que ya tienes desarrollado.

La web es estática: contiene páginas HTML, estilos CSS e imágenes u otros recursos. No necesitas crear una web nueva ni programar funcionalidades adicionales.

El objetivo es conseguir que tu web funcione dentro de un contenedor Docker.

**Tiempo orientativo:** 25–40 minutos.

## Objetivos

- Crear una imagen Docker para una web estática.
- Utilizar Nginx para servir los archivos.
- Configurar el servicio con Docker Compose.
- Comprobar que funcionan las distintas páginas, los estilos y las imágenes.
- Arrancar y detener el contenedor.

## 1. Prepara el proyecto

Localiza la carpeta de tu proyecto **Web Minimalista**.

Debería contener el archivo `index.html`, uno o varios archivos CSS, otras páginas HTML y una carpeta de recursos, por ejemplo `assets/`.

No cambies la estructura de carpetas si no es necesario. Es importante conservar las rutas que utiliza tu web para cargar los estilos, las imágenes y las demás páginas.

Añade estos dos archivos en la carpeta principal del proyecto:

```text
Web-Minimalista/
├── index.html
├── ... otras páginas HTML ...
├── css/
├── assets/
├── Dockerfile
└── compose.yaml
```

La estructura es orientativa: conserva los nombres y las carpetas reales de tu proyecto.

## 2. Crea el Dockerfile

En la carpeta principal, crea un archivo llamado exactamente `Dockerfile` y añade:

```dockerfile
FROM nginx:alpine
COPY . /usr/share/nginx/html
```

¿Qué hace cada instrucción?

- `FROM nginx:alpine`: utiliza una imagen de Nginx como punto de partida.
- `COPY . /usr/share/nginx/html`: copia los archivos del proyecto a la carpeta desde la que Nginx sirve la web.

No necesitas instalar Node.js ni ejecutar `npm install`, porque la web es estática.

## 3. Crea el archivo de Docker Compose

En la misma carpeta, crea `compose.yaml`:

```yaml
services:
  web:
    build: .
    ports:
      - "8080:80"
```

Recuerda:

- `build: .` indica que Docker debe construir la imagen usando el `Dockerfile` de la carpeta actual.
- `8080:80` conecta el puerto `8080` de tu ordenador con el puerto `80` del contenedor.

## 4. Construye y arranca la web

Abre una terminal en la carpeta donde están `Dockerfile` y `compose.yaml`.

Ejecuta:

```bash
docker compose up --build
```

Espera a que finalice la construcción y arranque el servicio.

Abre el navegador en:

http://localhost:8080

### Comprueba tu web

- [ ] Se muestra la página principal.
- [ ] El CSS se carga correctamente.
- [ ] Las imágenes se muestran.
- [ ] Puedo navegar a otras páginas HTML mediante los enlaces de la web.
- [ ] No he tenido que abrir los archivos HTML directamente desde el explorador de archivos.

## 5. Comprueba el contenedor

Abre una segunda terminal en la misma carpeta y ejecuta:

```bash
docker compose ps
```

Este comando permite comprobar el estado del servicio.

Después, ejecuta:

```bash
docker compose logs
```

Este comando muestra los registros del servicio. No necesitas interpretar todas las líneas.

- [ ] He ejecutado `docker compose ps`.
- [ ] He ejecutado `docker compose logs`.

## 6. Detén el servicio

Vuelve a la terminal donde ejecutaste `docker compose up --build` y pulsa `Ctrl + C`.

Después ejecuta:

```bash
docker compose down
```

Vuelve a cargar `http://localhost:8080` en el navegador.

- [ ] He detenido el servicio.
- [ ] He comprobado que la web ya no se sirve desde ese contenedor.

## 7. Preguntas breves

Responde con una o dos frases por pregunta:

1. ¿Qué diferencia hay entre una imagen Docker y un contenedor?
2. ¿Para qué sirve el `Dockerfile`?
3. ¿Para qué sirve `compose.yaml`?
4. ¿Qué significa `"8080:80"`?
5. ¿Qué problemas has tenido, si los ha habido, al comprobar las páginas, los estilos o las imágenes?

## Entrega

No necesitas crear un repositorio nuevo ni subir el proyecto a GitHub para esta práctica.

Entrega en Moodle:

- [ ] **Captura 1:** la página principal funcionando en `http://localhost:8080`.
- [ ] **Captura 2:** otra página de tu web funcionando, con sus estilos e imágenes.
- [ ] **Captura 3:** la terminal mostrando `docker compose ps` con el servicio arrancado.
- [ ] Las respuestas a las cinco preguntas.

Puedes adjuntar las capturas y las respuestas en un único PDF, o entregarlas por separado si Moodle lo permite.

Las capturas deben mostrar tu propia ejecución.

## Si algo falla

- Comprueba que Docker está arrancado.
- Ejecuta los comandos desde la carpeta que contiene `compose.yaml`.
- Comprueba que el archivo se llama exactamente `Dockerfile`.
- Si el puerto `8080` está ocupado, cambia `"8080:80"` por `"8081:80"` y entra en `http://localhost:8081`.
- Si el HTML carga pero faltan estilos o imágenes, revisa las rutas utilizadas en los atributos `href` y `src`.
- Si una página secundaria no se encuentra, comprueba que se ha copiado al contenedor y que el enlace apunta a su ruta correcta.

## Reto opcional

Modifica un texto de una de las páginas HTML y vuelve a construir la imagen:

```bash
docker compose up --build
```

Recarga la web y comprueba el cambio.

No es necesario hacer este reto para completar la práctica.
