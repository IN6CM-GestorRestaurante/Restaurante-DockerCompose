# Restaurante - Entorno Docker (Docker Compose)

Este repositorio contiene la configuración centralizada de **Docker Compose** necesaria para orquestar y levantar todo el ecosistema del proyecto "Gestor de Restaurante" de manera simultánea y conectada.

## 🚀 ¿Qué hace este archivo?
El archivo `docker-compose.yml` se encarga de:
- Inicializar las bases de datos requeridas (MongoDB para los datos principales y PostgreSQL para el servicio de autenticación).
- Construir y levantar los microservicios backend (`ServerUser`, `ServerAdmin`, `auth-node` o `AuthService`).
- Construir y servir los clientes web (`Client-User-Web` y `Client-Admin`).
- Manejar redes internas (Networks) para que los contenedores se comuniquen entre sí de forma segura sin exponer puertos innecesarios.

## 🛠 Requisitos Previos
Para levantar todo el entorno con un solo comando, asegúrate de tener instalado:
- [Docker Engine](https://docs.docker.com/engine/install/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## ⚙️ Instrucciones de Ejecución

1. **Clonar el repositorio:**
   ```bash
   git clone https://github.com/IN6CM-GestorRestaurante/Restaurante-DockerCompose.git
   cd Restaurante-DockerCompose
   ```

2. **Estructura de Carpetas:**
   Asegúrate de que este repositorio se encuentre al mismo nivel (en la misma carpeta raíz) que el resto de los repositorios del proyecto, ya que Docker Compose buscará las carpetas de los otros repositorios para construir sus imágenes.
   Ejemplo de estructura esperada:
   ```
   /Proyectos/Restaurante/
   ├── Restaurante-ServerUser/
   ├── Restaurante-ServerAdmin/
   ├── Restaurante-auth-node/
   ├── Restaurante-Client-User-Web/
   ├── Restaurante-Client-Admin/
   └── Restaurante-DockerCompose/
   ```

3. **Variables de Entorno:**
   Revisa que cada repositorio individual tenga su respectivo archivo `.env` configurado según sus propios READMEs, ya que los contenedores pueden leer estas variables durante el despliegue.

4. **Levantar el Ecosistema Completo:**
   Ejecuta el siguiente comando en la terminal desde la carpeta `Restaurante-DockerCompose`:
   ```bash
   docker-compose up --build
   ```
   *(Añade la bandera `-d` al final si deseas ejecutarlo en segundo plano / modo "detached").*

5. **Detener el Entorno:**
   Para detener y eliminar los contenedores (preservando los volúmenes de datos si fueron configurados):
   ```bash
   docker-compose down
   ```

## 📋 Arquitectura de Puertos por Defecto
Una vez levantado, los servicios suelen estar disponibles en los siguientes puertos (verificar el `docker-compose.yml` para mapeos exactos):
- **Base de Datos MongoDB:** `27017`
- **Base de Datos PostgreSQL:** `5432`
- **ServerAdmin API:** `4000`
- **ServerUser API:** `3000`
- **Auth Node API:** `5000`
- **Client Admin (Web):** `5173` (o el mapeado en el host)
- **Client User (Web):** `5174` (o el mapeado en el host)
