# Proyecto: Microservicios gRPC con Recuperación de Fallas

---

## Información de la materia:
- **Materia:** Tópicos Especiales en Telemática - C2561-ST0263-7290
- **Profesor:** Edwin Nelson Montoya Múñera, [emontoya@eafit.brightspace.com](mailto:emontoya@eafit.brightspace.com)
- **Estudiantes:**
  - Nicolás Hurtado Amezquita - nhurtadoa@eafit.edu.co
  - Jacobo Restrepo Muñoz - jrestrep32@eafit.edu.co

---

## 1. Breve descripción de la actividad

Se desarrolló un sistema distribuido basado en microservicios con comunicación gRPC, coordinado mediante un cliente REST y un API Gateway, utilizando **RabbitMQ** como intermediario de mensajes.  
El sistema implementa **recuperación ante fallas**: en caso de que un microservicio esté caído, las solicitudes se encolan automáticamente en RabbitMQ, y son procesadas cuando el servicio vuelve a estar disponible.  
Todo el ecosistema se orquestó con **Docker y Docker Compose**, y se desplegó tanto **en ambiente local** como **en AWS EC2**.

---

### 1.1 Aspectos que se cumplieron o desarrollaron (requerimientos funcionales y no funcionales)

- Implementación completa de los componentes: **Cliente REST**, **API Gateway**, **Microservicios gRPC**, **RabbitMQ**.
- Creación de múltiples microservicios
- Comunicación mediante **gRPC**.
- Configuración de **RabbitMQ**.
- Manejo de fallas: **Callbacks** al recuperar la disponibilidad de microservicios caídos.
- Contenerización de todos los componentes usando **Docker**.
- Despliegue y prueba del ecosistema tanto en **local** como en **AWS EC2**.

---

### 1.2 Aspectos que no se desarrollaron

- No se implementó sistema de **autenticaciones** para usuarios o servicios.
- No se creó una **interfaz gráfica** para el cliente (solo API REST/Swagger).
- No se aplicó **particionamiento** de microservicios o colas.
- No se implementó **replicación** (no hay alta disponibilidad entre brokers ni servicios).

---

## 2. Información general de diseño de alto nivel, arquitectura, patrones y mejores prácticas utilizadas

- **Arquitectura de Microservicios:** Cada operación matemática es un microservicio independiente.
- **Patrón Gateway:** API Gateway centraliza las comunicaciones de los clientes hacia los microservicios.
- **Contenerización:** Cada componente es desplegado en un contenedor Docker.
- **Buenas prácticas de comunicación:** Uso de gRPC para eficiencia en llamadas entre servicios.
- **Separación de responsabilidades:** Cada servicio cumple una única función específica.

---

## 3. Descripción del ambiente de desarrollo y técnico

| Herramienta | Versión |
|:---|:---|
| Lenguaje principal | Python 3.12 |
| Framework APIs | FastAPI 0.110.0 |
| RabbitMQ Broker | rabbitmq:3.9-management |
| Docker | Docker version 24.0.2 |
| Docker Compose | Docker Compose version 1.29.2 |
| gRPC | grpcio 1.64.0, grpcio-tools 1.64.0 |
| pika (RabbitMQ cliente) | pika 1.3.2 |
| Uvicorn (servidor ASGI) | uvicorn 0.30.1 |

---

### ¿Cómo se compila y ejecuta?

1. Clonar el repositorio.
2. Instalar Docker y Docker Compose.
3. En la carpeta raíz del proyecto ejecutar:

```bash
docker-compose up --build -d
```

4. Acceder a las interfaces Swagger para probar los servicios.

---

### Detalles de desarrollo
- Desarrollo modularizado por servicios.
- Uso de protobuf para definir contratos de gRPC.
- Configuración completa vía `docker-compose.yml`.

---

### Descripción y configuración de parámetros del proyecto

| Parámetro | Valor |
|:---|:---|
| RabbitMQ user/pass | `admin` / `admin` |
| Puertos expuestos EC2 | 22, 15672, 5672, 8000, 9000, 50051-50054 |
| Variables de ambiente | Definidas en `docker-compose.yml` para cada servicio. |

---

### Estructura de carpetas del proyecto

```
gRPC_gateway_client/
├── client_rest/
├── div_service/
├── gateway/
├── mul_service/
├── rabbitmq/
├── sub_service/
├── sum_service/
├── docker-compose.yml
├── README.md
```

---

## 4. Descripción del ambiente de ejecución en producción (AWS)

- **Servidor:** Amazon EC2 t2.micro (Ubuntu Server 22.04 LTS).
- **IP pública:** 54.89.216.52 (Esta cambia o a la hora de probarla podria la instancia estas apagada o detenida)
- **Acceso a servicios:**
  - RabbitMQ UI: `http://54.89.216.52:15672`
  - Client REST API: `http://54.89.216.52:9000/docs`
- **Docker y Docker Compose preinstalados.**

---

### ¿Cómo se lanza el servidor en AWS?

1. Conectarse vía SSH o Instance Connect.
2. Clonar el proyecto.
3. Ejecutar:

```bash
docker-compose up --build -d
```

4. Acceder a los servicios usando la IP pública.

---

### Mini guía de uso de la aplicación

1. Acceder al Client REST (`http://54.89.216.52:9000/docs`) o Gateway (`http://54.89.216.52:8000/docs`).
2. Probar operaciones como suma, resta, multiplicación, división.
3. Si un microservicio cae, enviar solicitudes y verificar recuperación automática vía RabbitMQ.
4. Visualizar el estado de las colas en `http://54.89.216.52:15672` (login: admin/admin).

---

## Referencias:

- Correcciones de errores, generación de código y mejores prácticas: **IA** (ChatGPT, GitHub Copilot).
- Tutoriales de referencia en **YouTube** sobre RabbitMQ, gRPC y Docker Compose.
- **Material de clase y guías del profesor**.
- **Sugerencias de compañeros** Implementación, manejo de fallos y opciones.

---

