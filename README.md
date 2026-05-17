# Sistema de Gestión de Pedidos — Integración de Patrones y Arquitecturas

## Ingeniería de Sistemas — Patrones de Diseño de Software
### Unidad 12 — Integración de Patrones y Arquitecturas
### Post-Contenido 1

---

# 📌 Descripción del Proyecto

Este proyecto consiste en el desarrollo de un sistema de gestión de pedidos utilizando Spring Boot y aplicando múltiples patrones de diseño para desacoplar responsabilidades y mejorar la mantenibilidad del sistema.

El sistema permite:

- Crear pedidos REST
- Procesar diferentes tipos de pedidos
- Publicar eventos de dominio
- Ejecutar notificaciones desacopladas
- Verificar calidad de código con SonarQube
- Validar arquitectura y pruebas mediante Spring Boot Testing

---

# 🚀 Tecnologías Utilizadas

- Java 17
- Spring Boot 3
- Maven
- Spring Web
- Spring Data JPA
- H2 Database
- Spring Events
- SonarQube
- JUnit 5

---

# 🏗️ Arquitectura del Proyecto

El proyecto utiliza una estructura feature-first basada en separación de responsabilidades y arquitectura desacoplada.

```text
src/main/java/com/empresa/pedidos/
├── dominio/
├── aplicacion/
├── infraestructura/
├── adaptadores/
```

---

# 🎯 Patrones de Diseño Implementados

## 1️⃣ Strategy Pattern

### Problema resuelto
El sistema necesitaba diferentes algoritmos para procesar pedidos según su tipo.

### Solución
Se implementó la interfaz `ProcesadorPedido` y tres estrategias concretas:

- `ProcesadorPedidoEstandar`
- `ProcesadorPedidoExpress`
- `ProcesadorPedidoInternacional`

### Beneficio
Se eliminó el uso de múltiples condicionales `if/else`, mejorando extensibilidad y mantenibilidad.

---

## 2️⃣ Factory Pattern

### Problema resuelto
La selección de la estrategia de procesamiento estaba acoplada al servicio principal.

### Solución
Se creó `ProcesadorPedidoFactory`, que selecciona dinámicamente el procesador adecuado según el tipo de pedido.

### Beneficio
La lógica de selección quedó centralizada y desacoplada.

---

## 3️⃣ Observer Pattern

### Problema resuelto
Las notificaciones estaban acopladas directamente al procesamiento de pedidos.

### Solución
Se implementaron eventos con Spring Events utilizando:

- `PedidoProcesadoEvent`
- `NotificacionEmail`
- `NotificacionLog`

### Beneficio
Las notificaciones quedaron desacopladas y extensibles.

---

## 4️⃣ Facade Pattern

### Problema resuelto
El controlador REST tenía demasiada lógica y dependencias internas.

### Solución
Se creó `FachadaPedidos` para encapsular el flujo completo de procesamiento.

### Beneficio
El controlador quedó simplificado y desacoplado de la lógica interna.

---

# 🔄 Flujo del Sistema

1. El cliente realiza un POST a `/api/pedidos`
2. El controlador llama a `FachadaPedidos`
3. La fachada solicita el procesador correcto mediante Factory
4. Strategy procesa el pedido
5. El pedido se guarda en base de datos
6. Se publica `PedidoProcesadoEvent`
7. Los listeners responden automáticamente

---

# 🌐 Endpoint REST

## Crear Pedido

```http
POST /api/pedidos
```

## Ejemplo JSON

```json
{
  "subtotal": 100,
  "tipo": "EXPRESS"
}
```

---

# 🧪 Pruebas Implementadas

El proyecto incluye:

- ✅ Prueba de Factory
- ✅ Prueba de eventos Observer
- ✅ Pruebas de estrategias
- ✅ Prueba de integración con `@SpringBootTest`

---

# 📊 Métricas de Calidad

## Antes de la Refactorización

- Cyclomatic Complexity: 4
- Cognitive Complexity: 6
- Acoplamiento directo a correo y repositorio

## Después de la Refactorización

- Cyclomatic Complexity reducida
- Eliminación de condicionales principales
- Bajo acoplamiento
- Arquitectura desacoplada
- Quality Gate Passed en SonarQube

---

# 📸 Capturas del Proyecto

## ✅ Quality Gate Passed

![Quality Gate](docs/quality_gate_passed.PNG)

---

## 📈 Métricas de Complejidad

![Metricas Complejidad](docs/metricas-complejidad.PNG)

---

## 📬 Prueba REST en Postman

![Postman](docs/postman-express.PNG)

---

# ⚙️ Comandos Utilizados

## Compilar proyecto

```bash
mvn clean package
```

## Ejecutar aplicación

```bash
mvn spring-boot:run
```

## Ejecutar pruebas

```bash
mvn test
```

## Ejecutar SonarQube

```bash
mvn clean verify sonar:sonar ^
-Dsonar.projectKey=pedidos-integrado ^
-Dsonar.host.url=http://localhost:9000 ^
-Dsonar.login=TOKEN
```

---

# ✅ Resultado Final

El sistema cumple correctamente con:

- ✅ Integración de 4 patrones de diseño
- ✅ Arquitectura desacoplada
- ✅ Publicación de eventos
- ✅ Uso de Spring Boot
- ✅ Verificación de calidad con SonarQube
- ✅ Cobertura de pruebas
- ✅ Controlador desacoplado mediante Facade

---

# 👨‍💻 Autor

**Diego Armando Bautista**  
Ingeniería de Sistemas — 2026
