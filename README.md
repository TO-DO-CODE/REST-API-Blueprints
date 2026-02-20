## Laboratorio #4 – REST API Blueprints (Java 21 / Spring Boot 3.3.x)
# Escuela Colombiana de Ingeniería – Arquitecturas de Software  

---

## 📋 Requisitos
- Java 21
- Maven 3.9+
- PostgreSQL (Instalado o vía Docker)

## ▶️ Ejecución del proyecto
Para compilar y ejecutar la aplicación:
```bash
mvn clean install
mvn spring-boot:run
```

### Probar con `curl`:
*(Nota: Hemos actualizado la API a la versión `/api/v1/`)*

**Obtener todos los planos:**
```bash
curl -s http://localhost:8080/api/v1/blueprints
```

**Obtener planos de un autor:**
```bash
curl -s http://localhost:8080/api/v1/blueprints/john
```

**Crear un nuevo plano:**
```bash
curl -i -X POST http://localhost:8080/api/v1/blueprints \
     -H 'Content-Type: application/json' \
     -d '{"author":"john","name":"kitchen","points":[{"x":1,"y":1}]}'
```

**Agregar un punto a un plano:**
```bash
curl -i -X PUT http://localhost:8080/api/v1/blueprints/john/kitchen/points \
     -H 'Content-Type: application/json' \
     -d '{"x":3,"y":3}'
```

---

## 🛠️ Documentación y Monitoreo (Swagger & Actuator)
- **Swagger UI (Interactivo):** [http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html)
- **OpenAPI JSON:** [http://localhost:8080/v3/api-docs](http://localhost:8080/v3/api-docs)
- **Actuator Health:** [http://localhost:8080/actuator/health](http://localhost:8080/actuator/health)

---

## 🗂️ Estructura de carpetas
```
src/main/java/edu/eci/arsw/blueprints
  ├── model/         # Entidades: Blueprint, Point
  ├── persistence/   # Repositorios (InMemory, Postgres)
  ├── services/      # Lógica de negocio
  ├── filters/       # Filtros (Identity, Redundancy, Undersampling)
  ├── controllers/   # REST Controllers
  └── config/        # Configuración (OpenApiConfig)
```

---

## 📊 Pruebas y Cobertura
Para ejecutar las pruebas unitarias y ver el reporte de JaCoCo (>90%):
```bash
mvn clean test
```
El reporte detallado se genera en: `target/site/jacoco/index.html`

---

## 📖 Resumen de Implementación
- **Persistencia Dual**: Soporte para memoria y PostgreSQL (activado por defecto).
- **ApiResponse**: Todas las respuestas siguen un formato JSON estandarizado.
- **Filtros por Perfiles**: 
  - Activar redundancia: `-Dspring-boot.run.profiles=redundancy`
  - Activar submuestreo: `-Dspring-boot.run.profiles=undersampling`