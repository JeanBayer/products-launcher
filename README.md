### Pasos para ejecutar el proyecto

1. Ejecutar `npm install` para instalar las dependencias
2. Si es la primera vez que clonas el proyecto ejecuta `npm run init` el cual va a traer los submodulos al proyecto e instala las dependencias en cada proyecto y copia el .env.example
3. Para poner en funcionamiento el proyecto ejecuta `npm run dev` el cual ejecuta docker-compose para que las apps funcionen.

### Pasos para crear los Git Submodules

1. Crear un nuevo repositorio en GitHub
2. Clonar el repositorio en la máquina local
3. Añadir el submodule, donde `repository_url` es la url del repositorio y `directory_name` es el nombre de la carpeta donde quieres que se guarde el sub-módulo (no debe de existir en el proyecto)

```
git submodule add <repository_url> <directory_name>
```

4. Añadir los cambios al repositorio (git add, git commit, git push)
   Ej:

```
git add .
git commit -m "Add submodule"
git push
```

5. Inicializar y actualizar Sub-módulos, cuando alguien clona el repositorio por primera vez, debe de ejecutar el siguiente comando para inicializar y actualizar los sub-módulos

```
git submodule update --init --recursive
```

6. Para actualizar las referencias de los sub-módulos

```
git submodule update --remote
```

## Importante

Si se trabaja en el repositorio que tiene los sub-módulos, **primero actualizar y hacer push** en el sub-módulo y **después** en el repositorio principal.

Si se hace al revés, se perderán las referencias de los sub-módulos en el repositorio principal y tendremos que resolver conflictos.

## Para prod

1. comando para construir la imagen:

```
docker compose -f docker-compose.prod.yml build
```

2. comando para ejecutar las imagenes

```
docker compose -f docker-compose.prod.yml up
```

## Pasos para desplegar en docker hub

1. Crear repositorio en Docker Hub
2. Iniciar sesión en Docker Hub desde la terminal:

```
docker login
```

3. Construir la imagen:

```
docker build -f dockerfile.prod -t <your_dockerhub_username>/<your_dockerhub_repository>:<tag> .
```

4. Subir la imagen al repositorio de Docker Hub:

```
docker push <your_dockerhub_username>/<your_dockerhub_repository>:<tag>
```

## Pasos para desplegar en google cloud

1. Construir la imagen:

```
docker build -f dockerfile.prod -t southamerica-west1-docker.pkg.dev/secret-drake-463714-u5/image-registry/auth-ms .
```

2. Subir la imagen:

```
docker push southamerica-west1-docker.pkg.dev/secret-drake-463714-u5/image-registry/auth-ms
```
