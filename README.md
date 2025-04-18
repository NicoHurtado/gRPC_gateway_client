
# 📈 Distributed gRPC

**Distributed gRPC** muestra los principios de **microservicios**, **gRPC** y **RabbitMQ**. Implementa una calculadora distribuida donde cada operación matemática básica — suma, resta, multiplicacion y division se gestiona en un microservicio separado, garantizando modularidad, escalabilidad y facilidad de mantenimiento.

---

## 🧩 Descripción General

Esta aplicación integra:

- **FastAPI** como cliente REST.
- **RabbitMQ** como sistema de mensajería para encolar solicitudes.
- **gRPC** para la comunicación eficiente entre servicios.
- **Docker Compose** para el despliegue coordinado de todos los componentes.

Cada operación aritmética se delega a un microservicio independiente, reflejando una arquitectura desacoplada y extensible.

---

## 🏗️ Estructura del Proyecto

- **client_rest/**  
  Cliente REST desarrollado en FastAPI. Envía peticiones de operaciones matemáticas.

- **gateway/**  
  Componente intermediario que recibe solicitudes REST, las convierte en mensajes y las enruta hacia los microservicios apropiados mediante RabbitMQ.

- **sum_service/**  
  Operaciones de suma.

- **sub_service/**  
  Operaciones de resta.

- **mul_service/**  
  Operaciones de multiplicación.

- **div_service/**  
  Operaciones de división.

- **rabbitmq/**  
  Configuración y consumidor de colas

- **docker-compose.yml**  
  Archivo para levantar todos los servicios.

---

## ⚙️ Requisitos Previos

Antes de comenzar, asegúrate de tener instalados:

- **Docker** (v20 o superior recomendado)
- **Docker Compose** (v2.0+)

---

## 🛠️ Instrucciones de Instalación

1. Clona el repositorio:

   ```bash
   git clone https://github.com/NicoHurtado/gRPC_gateway_client.git
   cd gRPC_gateway_client
   ```

2. Levanta los servicios:

   ```bash
   docker-compose up --build
   ```

Esto construirá y desplegará automáticamente todos los contenedores necesarios.

---

## 🚀 Cómo Ejecutarlo

1. Una vez desplegados los contenedores, puedes interactuar con el cliente REST

2. Endpoints principales:

   - `POST /sum` — Suma
   - `POST /sub` — Resta
   - `POST /mul` — Multiplicación
   - `POST /div` — División

   Cada solicitud debe incluir un cuerpo JSON con los números a, b (float) correspondientes.

---
