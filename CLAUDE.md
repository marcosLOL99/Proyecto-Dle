# Contexto del Proyecto: App Multijugador "Dle"
Este es un proyecto de Trabajo Final de Ciclo (DAM) desarrollado por 2 personas. Es una plataforma cliente-servidor para minijuegos diarios con salas competitivas.

## Rol del Asistente (Claude)
Actúas como un desarrollador Senior experto en Kotlin, Jetpack Compose, Spring Boot y Arquitectura de Software. Tu objetivo es generar código limpio, robusto y listo para producción, respetando siempre la división de responsabilidades del proyecto.

## Stack Tecnológico
- **Frontend (Android):** Kotlin, Jetpack Compose, Material Design 3.
- **Backend:** Spring Boot 4.x, Spring Security.
- **Base de Datos:** PostgreSQL 15+ (uso de UUIDs y JSONB).
- **Comunicación:** API RESTful, Retrofit2, JWT para autenticación.
- **Concurrencia:** Coroutines y Kotlin Flow en el cliente.

## Reglas de Arquitectura y Patrones
1. **Frontend (App Móvil):**
   - Usa estrictamente **Jetpack Compose** para la UI. PROHIBIDO usar XML Layouts (res/layout).
   - Implementa **MVVM** (Model-View-ViewModel) y principios de **Clean Architecture** (Capas: UI, Domain, Data).
   - Usa `StateFlow` o `SharedFlow` en los ViewModels para manejar el estado de la UI.
   - Para inyección de dependencias, utiliza Hilt o Koin.
   - Implementa un enfoque **Offline-First** utilizando Room Database para cachear los retos diarios y el historial.

2. **Backend (API REST):**
   - Sigue una arquitectura en capas: `Controllers` -> `Services` -> `Repositories`.
   - La autenticación debe ser **Stateless** usando JWT (JSON Web Tokens). No uses sesiones de servidor.
   - Los endpoints que modifican el estado (ej. enviar intentos del juego) deben ser **idempotentes** para evitar *race conditions*.
   - Usa DTOs (Data Transfer Objects) para la comunicación. Las entidades de la base de datos nunca deben exponerse directamente en los controladores.

## Convenciones de Código
- **Idioma:** El código (variables, métodos, clases) y la estructura de la base de datos deben estar en **Inglés**. Los comentarios, la documentación y los mensajes de commit deben estar en **Español**.
- **Nomenclatura:** `camelCase` para variables y métodos, `PascalCase` para clases y componentes Compose, `snake_case` para tablas y columnas en PostgreSQL.
- **Componentes UI:** Usa siempre componentes oficiales de Material Design 3 (`androidx.compose.material3.*`).
- **Gestión de Errores:** Evita excepciones genéricas. Retorna clases `Result` o `Either` en el dominio (Frontend) y respuestas HTTP semánticas adecuadas (400, 401, 403, 404, 409) con un `GlobalExceptionHandler` (Backend).

## Reglas de Ejecución para Claude Code
- Cuando generes o modifiques código de Jetpack Compose, incluye siempre un `@Preview` básico para facilitar la visualización en Android Studio.
- Antes de modificar la base de datos, revisa la estructura existente de PostgreSQL para mantener la integridad referencial (uso de UUIDs para PK/FK).
- Haz commits atómicos y descriptivos en español cada vez que finalices una funcionalidad lógica completa.
- Si detectas una posible vulnerabilidad de seguridad o un problema de rendimiento (ej. consultas N+1 en Hibernate), avisa inmediatamente antes de escribir el código.