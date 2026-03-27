
API REST para la gestión de franquicias, sucursales y productos, desarrollada con Spring Boot WebFlux y MongoDB.

## 📋 Tabla de Contenidos

- [Características](#-características)
- [Tecnologías](#-tecnologías)
- [Requisitos Previos](#-requisitos-previos)
- [Instalación y Ejecución](#-instalación-y-ejecución)
  - [Opción 1: Ejecución con Docker Compose (Recomendado)](#opción-1-ejecución-con-docker-compose-recomendado)
  - [Opción 2: Ejecución Local con Gradle](#opción-2-ejecución-local-con-gradle)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [API Endpoints](#-api-endpoints)
- [Ejemplos de Uso](#-ejemplos-de-uso)
- [Colección de Postman](#-colección-de-postman)
- [Documentación API (Swagger)](#-documentación-api-swagger)


## 🚀 Características

- ✅ **Criterios de Aceptación Implementados:**
  - Desarrollado en Spring Boot 3.4.1
  - Endpoint para agregar nueva franquicia
  - Endpoint para agregar nueva sucursal a franquicia
  - Endpoint para agregar nuevo producto a sucursal
  - Endpoint para eliminar producto de sucursal
  - Endpoint para modificar stock de producto
  - Endpoint para obtener productos con mayor stock por sucursal

- 🎯 **Puntos Extra Implementados:**
  - ✅ Aplicación empaquetada con Docker
  - ✅ Programación funcional y reactiva (Spring WebFlux)
  - ✅ Endpoint para actualizar nombre de franquicia
  - ✅ Endpoint para actualizar nombre de sucursal
  - ✅ Endpoint para actualizar nombre de producto

## 🛠 Tecnologías

- **Java 17**
- **Spring Boot 3.2.1**
- **Spring WebFlux** (Programación Reactiva)
- **MongoDB** (Base de datos NoSQL)
- **Gradle 8.5** (Sistema de build)
- **Docker & Docker Compose**
- **Springdoc OpenAPI** (Documentación Swagger)
- **Lombok**

## 📦 Requisitos Previos

### Para ejecución local:
- Java 17 o superior
- Gradle 8.0 o superior (o usar el wrapper incluido `./gradlew`)
- MongoDB 7.0 o superior (o usar Docker Compose)

### Para Docker:
- Docker 20.10 o superior
- Docker Compose 2.0 o superior

## 🔧 Instalación y Ejecución

### Opción 1: Ejecución con Docker Compose (Recomendado)

Esta es la forma más sencilla de ejecutar la aplicación con todas sus dependencias.

#### 1. Clonar el repositorio
```bash
git clone https://github.com/BugyMan1/franchise-api.git
cd franchise-api
```

#### 2. Iniciar los contenedores
```bash
docker-compose up --build
```

Este comando:
- Construye la imagen Docker de la aplicación con Gradle
- Levanta un contenedor de MongoDB
- Levanta la aplicación en el puerto 8080
- Configura la red entre los contenedores

#### 3. Verificar que todo está funcionando
```bash
# Ver los logs
docker-compose logs -f

# Verificar que los contenedores están corriendo
docker-compose ps
```

#### 4. Detener los contenedores
```bash
docker-compose down

# Para eliminar también los volúmenes (datos de MongoDB)
docker-compose down -v
```

La API estará disponible en: `http://localhost:8080`

### Opción 2: Ejecución Local con Gradle

#### 1. Clonar el repositorio
```bash
git clone https://github.com/BugyMan1/franchise-api.git
cd franchise-api
```

#### 2. Instalar MongoDB localmente (si no lo tienes)
```bash
# En macOS con Homebrew
brew install mongodb-community@7.0
brew services start mongodb-community@7.0

# En Ubuntu/Debian
sudo apt-get install -y mongodb-org
sudo systemctl start mongod

# En Windows, descarga e instala desde:
# https://www.mongodb.com/try/download/community
```

#### 3. Compilar el proyecto
```bash
# Usando Gradle Wrapper (recomendado - no requiere instalación de Gradle)
./gradlew build

# O si tienes Gradle instalado globalmente
gradle build
```

#### 4. Ejecutar la aplicación
```bash
# Con Gradle Wrapper
./gradlew bootRun

# O con Gradle instalado
gradle bootRun
```

La API estará disponible en: `http://localhost:8080`

## 📁 Estructura del Proyecto

```
franchise-api/
├── src/
│   ├── main/
│   │   ├── java/com/franchise/api/
│   │   │   ├── config/           # Configuraciones (OpenAPI)
│   │   │   ├── controller/       # Controladores REST
│   │   │   ├── dto/              # DTOs para requests/responses
│   │   │   ├── exception/        # Manejo de excepciones
│   │   │   ├── model/            # Modelos de dominio
│   │   │   ├── repository/       # Repositorios reactivos
│   │   │   ├── service/          # Lógica de negocio
│   │   │   └── FranchiseApiApplication.java
│   │   └── resources/
│   │       └── application.yml   # Configuración de la aplicación
│   └── test/                     # Tests unitarios
├── build.gradle                  # Configuración de Gradle
├── settings.gradle               # Configuración del proyecto Gradle
├── gradle.properties             # Propiedades de Gradle
├── gradlew                       # Gradle Wrapper (Unix/Mac)
├── gradlew.bat                   # Gradle Wrapper (Windows)
├── Dockerfile                    # Imagen Docker de la aplicación
├── docker-compose.yml            # Orquestación de contenedores
└── README.md                     # Este archivo
```

## 🌐 API Endpoints

### Franquicias

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/api/franchises` | Crear nueva franquicia |
| GET | `/api/franchises` | Obtener todas las franquicias |
| GET | `/api/franchises/{franchiseId}` | Obtener franquicia por ID |
| PUT | `/api/franchises/{franchiseId}/name` | Actualizar nombre de franquicia |

### Sucursales

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/api/franchises/{franchiseId}/branches` | Agregar sucursal a franquicia |
| PUT | `/api/franchises/{franchiseId}/branches/{branchId}/name` | Actualizar nombre de sucursal |

### Productos

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/api/franchises/{franchiseId}/branches/{branchId}/products` | Agregar producto a sucursal |
| DELETE | `/api/franchises/{franchiseId}/branches/{branchId}/products/{productId}` | Eliminar producto |
| PUT | `/api/franchises/{franchiseId}/branches/{branchId}/products/{productId}/stock` | Actualizar stock |
| PUT | `/api/franchises/{franchiseId}/branches/{branchId}/products/{productId}/name` | Actualizar nombre |

### Reportes

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| GET | `/api/franchises/{franchiseId}/top-products` | Productos con mayor stock por sucursal |

## 📝 Ejemplos de Uso

### 1. Crear una franquicia
```bash
curl -X POST http://localhost:8080/api/franchises \
  -H "Content-Type: application/json" \
  -d '{"name": "McDonald'\''s"}'
```

Respuesta:
```json
{
  "id": "65a1b2c3d4e5f6g7h8i9j0k1",
  "name": "McDonald's",
  "branches": []
}
```

### 2. Agregar una sucursal
```bash
curl -X POST http://localhost:8080/api/franchises/65a1b2c3d4e5f6g7h8i9j0k1/branches \
  -H "Content-Type: application/json" \
  -d '{"name": "Sucursal Centro"}'
```

### 3. Obtener productos con mayor stock por sucursal
```bash
curl -X GET http://localhost:8080/api/franchises/65a1b2c3d4e5f6g7h8i9j0k1/top-products
```

## 📚 Colección de Postman

El proyecto incluye una **colección de Postman** (`postman-collection.json`) con todos los endpoints configurados para facilitar el testing de la API.

#### Cómo usar la colección:

1. **Importar en Postman**
- Abre Postman
- Click en "Import"
- Selecciona el archivo `postman-collection.json`

2. **Configurar variables**
- La colección incluye variables predefinidas:
  - `baseUrl`: http://localhost:8080 (por defecto)
  - `franchiseId`: Se actualiza automáticamente al crear una franquicia
  - `branchId`: Se actualiza al crear una sucursal
  - `productId`: Se actualiza al crear un producto

3. **Ejecutar requests**
- Los requests están organizados por categoría:
  - **Franchises**: Crear, obtener, actualizar franquicias
  - **Branches**: Agregar y actualizar sucursales
  - **Products**: Agregar, actualizar, eliminar productos
  - **Reports**: Consultar productos con mayor stock

4. **Flujo de testing recomendado**
   ```
   1. Create Franchise → Copiar el ID de la respuesta
   2. Add Branch to Franchise → Copiar el ID de la sucursal
   3. Add Product to Branch → Crear varios productos
   4. Get Top Products by Branch → Ver productos con mayor stock
   ```

## 📖 Documentación API (Swagger)

Una vez que la aplicación esté corriendo, accede a la documentación interactiva de Swagger UI:

```
http://localhost:8080/swagger-ui.html
```

También puedes acceder a la especificación OpenAPI en formato JSON:

```
http://localhost:8080/api-docs
```

---




Este comando:
- Construye la imagen Docker de la aplicación con Gradle
- Levanta un contenedor de MongoDB
- Levanta la aplicación en el puerto 8080
- Configura la red entre los contenedores

#### 3. Verificar que todo está funcionando
```bash
# Ver los logs
docker-compose logs -f

# Verificar que los contenedores están corriendo
docker-compose ps
```

#### 4. Detener los contenedores
```bash
docker-compose down

# Para eliminar también los volúmenes (datos de MongoDB)
docker-compose down -v
```

La API estará disponible en: `http://localhost:8080`

### Opción 2: Ejecución Local con Gradle

#### 1. Clonar el repositorio
```bash
git clone https://github.com/BugyMan1/franchise-api.git
cd franchise-api
```

#### 2. Instalar MongoDB localmente (si no lo tienes)
```bash
# En macOS con Homebrew
brew install mongodb-community@7.0
brew services start mongodb-community@7.0

# En Ubuntu/Debian
sudo apt-get install -y mongodb-org
sudo systemctl start mongod

# En Windows, descarga e instala desde:
# https://www.mongodb.com/try/download/community
```

#### 3. Compilar el proyecto
```bash
# Usando Gradle Wrapper (recomendado - no requiere instalación de Gradle)
./gradlew build

# O si tienes Gradle instalado globalmente
gradle build
```

#### 4. Ejecutar la aplicación
```bash
# Con Gradle Wrapper
./gradlew bootRun

# O con Gradle instalado
gradle bootRun
```

La API estará disponible en: `http://localhost:8080`

## 📁 Estructura del Proyecto

```
franchise-api/
├── src/
│   ├── main/
│   │   ├── java/com/franchise/api/
│   │   │   ├── config/           # Configuraciones (OpenAPI)
│   │   │   ├── controller/       # Controladores REST
│   │   │   ├── dto/              # DTOs para requests/responses
│   │   │   ├── exception/        # Manejo de excepciones
│   │   │   ├── model/            # Modelos de dominio
│   │   │   ├── repository/       # Repositorios reactivos
│   │   │   ├── service/          # Lógica de negocio
│   │   │   └── FranchiseApiApplication.java
│   │   └── resources/
│   │       └── application.yml   # Configuración de la aplicación
│   └── test/                     # Tests unitarios
├── build.gradle                  # Configuración de Gradle
├── settings.gradle               # Configuración del proyecto Gradle
├── gradle.properties             # Propiedades de Gradle
├── gradlew                       # Gradle Wrapper (Unix/Mac)
├── gradlew.bat                   # Gradle Wrapper (Windows)
├── Dockerfile                    # Imagen Docker de la aplicación
├── docker-compose.yml            # Orquestación de contenedores
└── README.md                     # Este archivo
```

## 🌐 API Endpoints

### Franquicias

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/api/franchises` | Crear nueva franquicia |
| GET | `/api/franchises` | Obtener todas las franquicias |
| GET | `/api/franchises/{franchiseId}` | Obtener franquicia por ID |
| PUT | `/api/franchises/{franchiseId}/name` | Actualizar nombre de franquicia |

### Sucursales

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/api/franchises/{franchiseId}/branches` | Agregar sucursal a franquicia |
| PUT | `/api/franchises/{franchiseId}/branches/{branchId}/name` | Actualizar nombre de sucursal |

### Productos

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/api/franchises/{franchiseId}/branches/{branchId}/products` | Agregar producto a sucursal |
| DELETE | `/api/franchises/{franchiseId}/branches/{branchId}/products/{productId}` | Eliminar producto |
| PUT | `/api/franchises/{franchiseId}/branches/{branchId}/products/{productId}/stock` | Actualizar stock |
| PUT | `/api/franchises/{franchiseId}/branches/{branchId}/products/{productId}/name` | Actualizar nombre |

### Reportes

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| GET | `/api/franchises/{franchiseId}/top-products` | Productos con mayor stock por sucursal |

## 📝 Ejemplos de Uso

### 1. Crear una franquicia
```bash
curl -X POST http://localhost:8080/api/franchises \
  -H "Content-Type: application/json" \
  -d '{"name": "McDonald'\''s"}'
```

Respuesta:
```json
{
  "id": "65a1b2c3d4e5f6g7h8i9j0k1",
  "name": "McDonald's",
  "branches": []
}
```

### 2. Agregar una sucursal
```bash
curl -X POST http://localhost:8080/api/franchises/65a1b2c3d4e5f6g7h8i9j0k1/branches \
  -H "Content-Type: application/json" \
  -d '{"name": "Sucursal Centro"}'
```

### 3. Obtener productos con mayor stock por sucursal
```bash
curl -X GET http://localhost:8080/api/franchises/65a1b2c3d4e5f6g7h8i9j0k1/top-products
```

## 📚 Colección de Postman

El proyecto incluye una **colección de Postman** (`postman-collection.json`) con todos los endpoints configurados para facilitar el testing de la API.

#### Cómo usar la colección:

1. **Importar en Postman**
- Abre Postman
- Click en "Import"
- Selecciona el archivo `postman-collection.json`

2. **Configurar variables**
- La colección incluye variables predefinidas:
  - `baseUrl`: http://localhost:8080 (por defecto)
  - `franchiseId`: Se actualiza automáticamente al crear una franquicia
  - `branchId`: Se actualiza al crear una sucursal
  - `productId`: Se actualiza al crear un producto

3. **Ejecutar requests**
- Los requests están organizados por categoría:
  - **Franchises**: Crear, obtener, actualizar franquicias
  - **Branches**: Agregar y actualizar sucursales
  - **Products**: Agregar, actualizar, eliminar productos
  - **Reports**: Consultar productos con mayor stock

4. **Flujo de testing recomendado**
   ```
   1. Create Franchise → Copiar el ID de la respuesta
   2. Add Branch to Franchise → Copiar el ID de la sucursal
   3. Add Product to Branch → Crear varios productos
   4. Get Top Products by Branch → Ver productos con mayor stock
   ```

## 📖 Documentación API (Swagger)

Una vez que la aplicación esté corriendo, accede a la documentación interactiva de Swagger UI:

```
http://localhost:8080/swagger-ui.html
```

También puedes acceder a la especificación OpenAPI en formato JSON:

```
http://localhost:8080/api-docs
```

---

**  proyecto para el cargo de desarrollador back**
