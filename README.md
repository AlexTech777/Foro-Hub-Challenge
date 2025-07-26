🧠 ForoHub API

API RESTful desarrollada con Spring Boot 3 para la gestión segura y documentada de tópicos de foro técnico. Incluye autenticación JWT, control granular de acceso por roles y documentación interactiva con Swagger UI. Ideal para entornos empresariales y educativos donde la seguridad y claridad son prioridad.

🔐 Autenticación y Seguridad con JWT

El sistema implementa un flujo completo de autenticación basado en JSON Web Tokens (JWT), garantizando el acceso controlado a los recursos del backend:

🔄 Flujo de Autenticación

1. **Login de usuario** (`POST /auth/login`): El usuario envía credenciales válidas (email y contraseña).
2. **Generación de Token JWT**: Si las credenciales son correctas, se devuelve un token firmado.
3. **Acceso a recursos protegidos**: El token debe incluirse en cada solicitud como header `Authorization: Bearer <token>`.
4. **Control por rol**: Algunos endpoints requieren roles específicos para operar (admin, usuario).

🔍 Validaciones automáticas

- Tokens expirados o malformados generan error `401 Unauthorized`.
- Acceso sin permisos suficientes responde con `403 Forbidden`.
- Tokens válidos permiten acceso a operaciones como crear, listar y responder tópicos.


📘 Documentación Interactiva con Swagger UI
Se incluyó Swagger/OpenAPI v3 para generar documentación técnica y habilitar pruebas interactivas desde navegador:

1 - Acceso: /swagger-ui/index.html
2 - Soporta login directo desde Swagger
3 - Permite probar recursos protegidos usando el token JWT
4 - Muestra modelos de datos, parámetros requeridos y ejemplos de respuesta

La seguridad está definida a nivel global en Swagger, lo que permite usar Authorize una sola vez para todos los endpoints protegidos.

🧩 Endpoints disponibles
Endpoint	Método	Seguridad	Descripción
* - /auth/login	POST	Público	Autenticación del usuario
* - /topicos	GET	Protegido	Listado de tópicos del foro
* - /topicos	POST	Protegido	Crear nuevo tópico
* - /respuestas/{id}	POST	Protegido	Responder a un tópico específico

Todos los endpoints protegidos requieren JWT válido y perfil autorizado.

🧪 Pruebas recomendadas
Para garantizar la seguridad y robustez, se recomienda realizar las siguientes pruebas:

* - ✅ Login exitoso con credenciales válidas
* - 🚫 Acceso denegado sin token o con token inválido
* - 🔄 Token expirado y comportamiento frente al refresh
* - 🧾 Validación de roles accediendo a recursos restringidos
* - 🐞 Pruebas desde Swagger UI simulando usuarios reales

📦 Tecnologías utilizadas
* - Java 17 + Spring Boot 3
* - Spring Security + JWT
* - JPA + Hibernate
* - Flyway para control de migraciones SQL
* - Swagger/OpenAPI para documentación técnica
* - Maven como gestor de dependencias

🗄️ Base de Datos
La API utiliza MySQL como sistema de almacenamiento relacional. Se eligió por su robustez, compatibilidad con JPA/Hibernate y facilidad de integración con Spring Boot.

Características clave:
* -✅ Motor: MySQL Server
* -🗂️ Persistencia gestionada con JPA/Hibernate
* -🚀 Migraciones controladas con Flyway (src/main/resources/db/migration)
* -🔐 Integridad referencial y validación por esquema SQL
* -⚙️ Conexión configurada vía application.properties

Ejemplo de conexión:

properties
<img width="535" height="119" alt="image" src="https://github.com/user-attachments/assets/fbadf9ea-30e8-4438-86a1-89e9322ad080" />




📸 Capturas Interfaz Insomnia con token insertado y pruebas

Flujo de login y respuesta JWT
<img width="921" height="495" alt="image" src="https://github.com/user-attachments/assets/0a173a92-3282-4aa3-875e-66f576b050a8" />
 
Endpoint protegido accedido con autorización exitosa  
<img width="921" height="494" alt="image" src="https://github.com/user-attachments/assets/fc74ff87-f07d-4c6f-b982-e5186b419f71" />


Respuesta clara ante error 401 y 403 
<img width="921" height="498" alt="image" src="https://github.com/user-attachments/assets/a3003405-f9db-4813-89d9-cf90e0d61b38" />


📸 Capturas Interfaz Swagger con token insertado y pruebas

Flujo de login y respuesta JWT
<img width="921" height="435" alt="image" src="https://github.com/user-attachments/assets/d5d72805-45a0-4052-b7e2-2ed801b82db7" />

Endpoint protegido accedido con autorización exitosa  
<img width="921" height="736" alt="image" src="https://github.com/user-attachments/assets/d6805d50-c261-4818-953c-a41b5ddc2256" />


Respuesta clara ante error 401 y 403  
<img width="921" height="700" alt="image" src="https://github.com/user-attachments/assets/2325bedf-185d-4005-8fb5-92dc0e1f3ff6" />


🎯 Lecciones aprendidas
Durante la implementación se enfrentaron y resolvieron desafíos clave:

⚙️ Conflictos de dependencias entre Swagger y Spring Boot 3

🧩 Configuración granular de rutas públicas/protegidas

📚 Integración de seguridad en la documentación sin comprometer usabilidad

🔍 Debugging de filtros personalizados para autenticar y validar roles

🗂️ Estructura del Proyecto

<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/5b636319-5b61-45ce-85df-e7c0a6d30fdc" />

 

Detalles clave por carpeta

1 - controller/: Contiene clases como TopicoController, AuthController, etc., que exponen los endpoints.

2 - dto/: Modelos como LoginRequest, TopicoResponse, usados para definir payloads limpios.

3 - model/: Define entidades JPA como Topico, Usuario, Respuesta, incluyendo relaciones.

4 - repository/: Interfaces como TopicoRepository, usan Spring Data JPA.

5 - service/: Lógica como AuthService, TopicoService, encapsula reglas de negocio.

6 - security/: JWTFilter, configuración de SecurityConfig, manejo de roles y autenticación.

7 - config/: SwaggerConfig, CorsConfig, entre otros para personalización del comportamiento.

🧠 Conclusión
Este proyecto representa más que una API funcional: es un ejercicio riguroso de arquitectura segura, documentación profesional y autenticación robusta con JWT. 
A lo largo del desarrollo, se aplicaron buenas prácticas REST, se integró Swagger/OpenAPI para pruebas interactivas, y se consolidó un modelo de datos sólido con migraciones Flyway controladas.
La experiencia ha sido una oportunidad de aprendizaje activo en Spring Boot 3.x, debugging avanzado y diseño backend orientado a la excelencia técnica. 
Este foro no solo valida usuarios: valida un enfoque resiliente, metódico y comprometido con la seguridad y la calidad.

🔒 El objetivo está cumplido. Y el siguiente desafío ya está en marcha.
Realizado por Alexander Gonzalez
