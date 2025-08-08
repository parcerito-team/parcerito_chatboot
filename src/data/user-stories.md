🟩 Historia de Usuario 1 -- Registro de usuario
----------------------------------------------

**Persona**: *Luis Felipe Ortega*\
**Edad**: 46 años\
**Perfil**: Técnico de refrigeración, nivel digital medio, quiere usar ParceroGo sin complicaciones.

* * * * *

### 🧾 Historia

Como nuevo usuario que no tiene experiencia con la app,\
quiero poder registrarme fácilmente con mis datos básicos,\
para comenzar a usar el chatbot de ParceroGo sin confusión ni procesos complicados.

* * * * *

### 🎯 Beneficio esperado

Ingresar al sistema sin fricción y recibir ayuda sobre cómo usar el servicio.

* * * * *

### ✅ Criterios de aceptación

1.  El sistema debe aceptar registros con nombre, correo y contraseña válidos.

2.  Si el correo ya existe, se debe mostrar el mensaje:\
    `"Ese correo ya está registrado. Intenta iniciar sesión o usar otro correo."`

3.  Si el formato del correo es inválido, debe mostrarse:\
    `"Por favor ingresa un correo válido."`

4.  Si la contraseña no cumple requisitos mínimos (mínimo 6 caracteres), debe mostrarse:\
    `"La contraseña debe tener al menos 6 caracteres."`

5.  Al registrarse exitosamente, debe mostrarse:\
    `"¡Bienvenido a ParceroGo, parcero! Ya podés iniciar sesión."`

* * * * *

### 🔐 Endpoint mapeado

`POST /users/register`

* * * * *

### 📦 Payload esperado


`{
  "name": "Luis Felipe Ortega",
  "email": "luisfelipe@email.com",
  "password": "segura123"
}`

* * * * *

### 🛠️ Alcance técnico

-   Crear el controlador para `POST /users/register` en el backend.

-   Implementar validación de campos (nombre, correo, contraseña).

-   Verificar que el correo no esté duplicado en la base de datos.

-   Encriptar la contraseña antes de guardarla.

-   Almacenar el nuevo usuario en la base de datos.

-   Enviar respuesta con mensaje de éxito o error según el caso.

-   (Opcional) Agregar prueba unitaria para los escenarios positivos y negativos.

🟩 Historia de Usuario 2 -- Inicio de sesión (login)
---------------------------------------------------

**Persona**: *Luis Felipe Ortega*\
**Edad**: 46 años\
**Perfil**: Técnico de refrigeración, nivel digital medio, quiere usar ParceroGo sin complicaciones.

* * * * *

### 🧾 Historia

Como usuario registrado,\
quiero poder iniciar sesión con mi correo y contraseña,\
para acceder al chatbot de ParceroGo de manera segura y personalizada.

* * * * *

### 🎯 Beneficio esperado

Entrar a mi cuenta y recibir asistencia sin tener que volver a registrarme.

* * * * *

### ✅ Criterios de aceptación

1.  Si el usuario ingresa un correo y contraseña válidos, debe recibir un token y un `statusCode: 200`.

2.  Si las credenciales son incorrectas, debe devolverse:


    `{
      "message": "Correo o contraseña incorrectos. Verifica tus datos e intenta de nuevo.",
      "statusCode": 401
    }`

3.  Si algún campo está vacío o mal formado:


    `{
      "message": "Por favor completa todos los campos correctamente.",
      "statusCode": 400
    }`

4.  Si el usuario no existe:


    `{
      "message": "No encontramos una cuenta con ese correo. ¿Querés registrarte?",
      "statusCode": 404
    }`

5.  Si el login es exitoso:


    `{
      "token": "<JWT_token>",
      "message": "¡Bienvenido de nuevo, parcero! Ya podés comenzar a chatear.",
      "statusCode": 200
    }`

* * * * *

### 🔐 Endpoint mapeado

`POST /users/login`

* * * * *

### 📦 Payload esperado


`{
  "email": "luisfelipe@email.com",
  "password": "segura123"
}`

* * * * *

### 🛠️ Alcance técnico

-   Crear el controlador para `POST /users/login` en el backend.

-   Verificar existencia del usuario y validar la contraseña (encriptada).

-   Generar y devolver un JWT válido con el perfil del usuario.

-   Responder con `statusCode` correcto en todos los escenarios.

-   (Opcional) Incluir pruebas unitarias para login válido, inválido, campos vacíos y usuario no existente.

🟩 Historia de Usuario 3 -- Enviar mensaje al chatbot y recibir respuesta útil
-------------------------------------------------------------------------------------------

**Persona**: *Diana Vargas*\
**Edad**: 33 años\
**Perfil**: Analista financiera, usuaria frecuente y autosuficiente de ParceroGo.

* * * * *

### 🧾 Historia

Como usuaria frecuente de ParceroGo,\
quiero poder enviarle preguntas al chatbot,\
para recibir respuestas rápidas y claras sin tener que contactar al soporte humano.

* * * * *

### 🎯 Beneficio esperado

Resolver mis dudas sobre el servicio sin depender de otros canales ni esperar a un agente.

* * * * *

### ✅ Criterios de aceptación

1.  El endpoint `/chat` debe aceptar un `message` y un `conversation_id` en el cuerpo del request.

2.  Si el `conversation_id` no se envía, el backend debe generar uno automáticamente y devolverlo en la respuesta.

3.  El mensaje debe ser procesado y respondido por el modelo (OpenAI o similar).

4.  La respuesta debe tener la siguiente estructura:


    `{
      "reply": "¡Claro, parcero! Para ver tu historial de viajes solo tenés que ir a 'Mis viajes' en el menú principal.",
      "statusCode": 200,
      "conversation_id": "abc123"
    }`

5.  Si el usuario no está autenticado, debe mostrarse:


    `{
      "message": "No estás autenticado. Inicia sesión para chatear.",
      "statusCode": 401
    }`

6.  Si el campo `message` está vacío:


    `{
      "message": "El mensaje no puede estar vacío.",
      "statusCode": 400
    }`

7.  El historial de la conversación debe guardarse con:

    -   `conversation_id`

    -   `user_id` (obtenido del JWT)

    -   Lista de mensajes (user/bot)

    -   Flags como `escalated: true` si aplica (ver Historia 7)

* * * * *

### 🔐 Endpoint mapeado

`POST /chat`\
**Headers requeridos**:


`Authorization: Bearer <JWT_token>`

* * * * *

### 📦 Payload esperado

`{
  "message": "¿Cómo reviso mis viajes pasados?",
  "conversation_id": "abc123"
}`

* * * * *

### 📤 Respuesta esperada (éxito)


`{
  "reply": "¡Claro, parcero! Para ver tu historial de viajes solo tenés que ir a 'Mis viajes' en el menú principal.",
  "statusCode": 200,
  "conversation_id": "abc123"
}`

* * * * *

### 🛠️ Alcance técnico

-   Crear el endpoint `POST /chat` en el backend.

-   Validar JWT y extraer `user_id`.

-   Si no se recibe `conversation_id`, generar uno único (UUID).

-   Guardar mensaje del usuario, respuesta del bot y `conversation_id` en un log o BD.

-   Incluir lógica para detectar flujos especiales:

    -   **RAG** (Historia 5)

    -   **Escalación simulada** (Historia 7)

    -   **Rate limits / errores** (Historia 4)

-   Establecer estructura de respuesta estándar.



🟩 Historia de Usuario 4 -- Manejo de errores del modelo y límites de uso
------------------------------------------------------------------------

**Persona**: *Diana Vargas*\
**Edad**: 33 años\
**Perfil**: Analista financiera, usuaria frecuente y autosuficiente de ParceroGo.

* * * * *

### 🧾 Historia

Como usuaria que usa frecuentemente el chatbot,\
quiero que el sistema me avise con claridad si hubo un error al generar la respuesta o si he enviado demasiadas preguntas,\
para que sepa qué hacer y no me frustre si no obtengo respuesta.

* * * * *

### 🎯 Beneficio esperado

Evitar frustraciones innecesarias y entender qué pasa cuando el bot no responde.

* * * * *

### ✅ Criterios de aceptación

1.  Si la llamada al modelo LLM (ej. OpenAI) falla por un error interno, debe devolverse:


    `{
      "message": "Uy, parcero... algo falló al generar la respuesta. Intentalo de nuevo en un momentico.",
      "statusCode": 500
    }`

2.  Si se alcanza el límite de mensajes por minuto (ej. 5 mensajes en 1 minuto), debe devolverse:


    `{
      "message": "Has enviado muchas preguntas en poco tiempo. Espera un momento y volvé a intentarlo.",
      "statusCode": 429
    }`

3.  Estos errores deben ser manejados de forma centralizada en el backend.

4.  El usuario debe recibir siempre un mensaje amable y claro, en el tono definido por Parcerito, sin mensajes técnicos crudos.

* * * * *

### 🔐 Endpoint mapeado

`POST /chat`\
*(Mismo endpoint de historia anterior, pero distintos flujos)*

* * * * *

### 📦 Payload esperado

`{
  "message": "¿Por qué me cobraron una tarifa extra?"
}`

* * * * *

### 🛠️ Alcance técnico

-   Implementar manejo de errores de red o fallos en la respuesta de OpenAI.

-   Capturar `rate limit errors` y aplicar lógica local o basada en headers de la API.

-   Definir umbral de peticiones por usuario (ej. 5 por minuto) y rechazar el exceso.

-   Centralizar errores con middleware de error handling.

-   En todos los casos, devolver `statusCode` apropiado y un mensaje amigable.


🟩 Historia de Usuario 5 -- Incluir contexto del Knowledge Base en las respuestas del bot (RAG simulado)
---------------------------------------------------------------------------------------------------------------------

**Persona**: *Diana Vargas*\
**Edad**: 33 años\
**Perfil**: Analista financiera, autosuficiente, prefiere respuestas precisas y útiles del primer intento.

* * * * *

### 🧾 Historia

Como usuaria del chatbot,\
quiero que las respuestas del bot incluyan información específica de ParceroGo,\
para que sean más útiles y respondan realmente a mi pregunta sin vaguedades.

* * * * *

### 🎯 Beneficio esperado

Obtener respuestas más confiables, claras y personalizadas sobre el servicio.

* * * * *

### ✅ Criterios de aceptación

1.  El sistema debe tener una base de conocimiento en formato `kb.json` o `kb.yaml` con artículos sobre funciones, políticas y preguntas frecuentes.

2.  Al recibir un mensaje del usuario, el backend debe buscar fragmentos relevantes dentro del KB en base a keywords (o embeddings simples).

3.  El fragmento encontrado debe añadirse al prompt enviado al modelo.

4.  Si no se encuentra un fragmento relevante, debe enviarse el prompt sin contexto adicional, pero informando al usuario si el modelo no puede dar una respuesta confiable.

5.  Las respuestas del modelo deben estar limitadas únicamente al dominio de ParceroGo.

6.  Si el modelo intenta responder a temas externos (ej. "¿Qué opinás de Apple vs Samsung?"), debe responder:


    `{
      "reply": "Parcero, esa pregunta se sale del alcance de este chat. Solo puedo ayudarte con temas relacionados con tu experiencia en ParceroGo.",
      "statusCode": 200
    }`

* * * * *

### 🔐 Endpoint mapeado

`POST /chat`\
*(Lógica interna del endpoint, etapa previa a la llamada al modelo)*

* * * * *

### 📦 Payload esperado

`{
  "message": "¿Qué pasa si cancelo un viaje después de que ya va en camino?"
}`

* * * * *

### 🛠️ Alcance técnico

-   Crear el archivo `kb.yaml` o `kb.json` con contenido relevante redactado en el tono de Parcerito.

-   Implementar una función que reciba una pregunta y devuelva entradas relevantes del KB (por keywords o lógica simple).

-   Concatenar esos fragmentos al `system` prompt del modelo antes de hacer la llamada.

-   Incluir una validación para que el modelo solo responda usando ese contexto.

-   Si no hay información suficiente, el modelo debe devolver una respuesta de "fuera de alcance" o escalar la consulta.

-   Incluir pruebas para preguntas válidas y preguntas fuera del dominio.

-   (Opcional) Loguear los mensajes sin match en el KB para análisis posterior.

🟩 Historia de Usuario 6 -- Diseño e integración del prompt base del modelo
--------------------------------------------------------------------------

**Persona**: *Felipe Arguello*\
**Edad**: 33 años\
**Perfil**: Líder de producto técnico en ParceroGo. Supervisa calidad del sistema y coherencia del comportamiento del chatbot.

* * * * *

### 🧾 Historia

Como líder de producto técnico,\
quiero definir un prompt base coherente con la identidad del chatbot,\
para asegurar que las respuestas sean claras, útiles, alineadas al tono de Parcerito y dentro del dominio de ParceroGo.

* * * * *

### 🎯 Beneficio esperado

Garantizar que todas las respuestas del modelo reflejen los valores de la marca, sean precisas y no se salgan del ámbito del producto.

* * * * *

### ✅ Criterios de aceptación

1.  El prompt base debe incluir instrucciones claras sobre:

    -   El tono y personalidad del asistente (Parcerito).

    -   El idioma (español, estilo colombiano informal pero respetuoso).

    -   La limitación de respuestas únicamente al contexto de ParceroGo.

2.  El prompt debe instruir al modelo a **no inventar respuestas** si no tiene suficiente información.

3.  Si el usuario hace una pregunta fuera del dominio, el modelo debe devolver:


    `{
      "reply": "Parcero, esa pregunta se sale del alcance de este chat. Solo puedo ayudarte con temas relacionados con tu experiencia en ParceroGo.",
      "statusCode": 200
    }`

4.  El prompt debe permitir integrar el contexto del KB cuando esté disponible.

5.  El prompt debe estar centralizado y ser reutilizable desde el endpoint `/chat`.

* * * * *

### 🔐 Endpoint mapeado

`POST /chat`\
*(El prompt base es parte de la construcción del request a la API del modelo)*

* * * * *

### 📦 Ejemplo de estructura del prompt enviado al modelo


`{
  "messages": [
    {
      "role": "system",
      "content": "Eres Parcerito, el asistente virtual de ParceroGo, una plataforma de transporte urbano en Colombia. Solo puedes responder preguntas relacionadas con el funcionamiento de ParceroGo. Si el usuario hace preguntas fuera de ese ámbito, debes responder amablemente que no puedes ayudar con eso. Usa un lenguaje claro, respetuoso y cercano. Si no tienes suficiente información, ofrece escalar la consulta a soporte humano. Usa únicamente la información proporcionada en el contexto."
    },
    {
      "role": "user",
      "content": "¿Qué pasa si cancelo un viaje después de que el conductor ya va en camino?"
    },
    {
      "role": "system",
      "content": "[Contexto desde el KB insertado aquí, si aplica]"
    }
  ]
}`

* * * * *

### 🛠️ Alcance técnico

-   Escribir y validar el `prompt base` del chatbot alineado a Parcerito.

-   Integrarlo como plantilla o constante central en el backend.

-   Inyectar en tiempo de ejecución el mensaje del usuario y el contexto del KB.

-   Validar que el prompt limita respuestas a ParceroGo y controla el tono.

-   (Opcional) Probar variaciones del prompt para ajustar precisión o estilo.

-   Documentar el prompt en `docs/prompt.md` o en el repo para mantenimiento futuro.

🟩 Historia de Usuario 7 -- Escalación simulada a un agente humano
-----------------------------------------------------------------

**Persona**: *Carlos Marín*\
**Edad**: 59 años\
**Perfil**: Usuario poco digital, confía más en la atención humana. Se frustra fácilmente si no entiende cómo funciona algo.

* * * * *

### 🧾 Historia

Como usuario que no entiende una respuesta del bot,\
quiero poder pedir que me atienda un agente,\
para sentir que no me dejaron solo cuando el chatbot no resolvió mi duda.

* * * * *

### 🎯 Beneficio esperado

Recibir una respuesta empática cuando el chatbot no logra ayudarme y evitar frustración.

* * * * *

### ✅ Criterios de aceptación

1.  Si el usuario envía un mensaje como `"quiero hablar con un agente"` o `"esto no me ayuda"`, el backend debe identificar la intención de escalación.

2.  El sistema debe devolver una respuesta prediseñada en tono Parcerito, como:


    `{
      "reply": "Entiendo, parcero. Ya estoy reenviando tu consulta a uno de nuestros agentes. ¡Te van a ayudar en un ratico!",
      "statusCode": 200,
      "escalated": true,
      "conversation_id": "abc123"
    }`

3.  No debe realizarse ninguna conexión real con humanos: la respuesta debe ser 100% simulada.

4.  La detección de intención debe basarse en palabras clave o una lista configurable.

5.  Esta lógica se debe ejecutar antes de cualquier intento de llamada al modelo.

* * * * *

### 🔐 Endpoint mapeado

`POST /chat`\
*(Lógica integrada, infraestructura y estructura general definidas en Historia 3)*

* * * * *

### 📦 Payload de ejemplo

`{
  "message": "Esto no me ayudó, quiero hablar con alguien",
  "conversation_id": "abc123"
}`

* * * * *

### 🛠️ Alcance técnico

-   Implementar detección de intención de escalación (por keywords o lógica simple).

-   Interrumpir flujo normal y devolver respuesta prediseñada cuando aplique.

-   Marcar la conversación con `escalated: true` (ver Historia 3).

-   Asegurar consistencia de tono con Parcerito.


🛠️ Historia de Usuario 8 -- Preparar despliegue en Azure y configurar CI/CD
----------------------------------------------------------------------------

**Persona**: *Felipe Arguello*\
**Edad**: 33 años\
**Perfil**: PO técnico del equipo ParceroGo, enfocado en asegurar que el sistema sea entregable, automatizado y accesible en un entorno real de ejecución.

* * * * *

### 🧾 Historia

Como equipo técnico de ParceroGo,\
queremos automatizar el ciclo de construcción, prueba y despliegue del chatbot,\
para garantizar que la solución esté disponible en Azure de forma reproducible, mantenible y accesible durante el reto.

* * * * *

### 🎯 Beneficio esperado

Cumplir con los entregables obligatorios del reto de GenAI, facilitar revisiones técnicas y permitir iteraciones rápidas con mínima fricción.

* * * * *

### ✅ Criterios de aceptación

#### 🧪 CI/CD (Parte 7 del reto)

1.  Debe existir un pipeline de CI configurado (idealmente con GitHub Actions) que:

    -   Realice `checkout` del repositorio.

    -   Instale dependencias.

    -   Ejecute pruebas automáticas (si existen).

    -   Construya una imagen Docker del backend.

    -   Suba la imagen a un container registry (Azure Container Registry o DockerHub).

2.  El archivo del pipeline debe estar disponible en:

    -   `.github/workflows/ci.yml`

3.  El pipeline debe ejecutarse automáticamente en cada `push` a `main` o en `pull requests`.

#### ☁️ Despliegue en Azure (Parte 8 del reto)

1.  El backend del chatbot debe estar desplegado en **Azure**, utilizando el acceso proporcionado (usuario y contraseña).

2.  Se deben configurar variables de entorno en el entorno de Azure para:

    -   API key de OpenAI

    -   Ruta o URL de la base de conocimiento (si aplica)

3.  El endpoint `/chat` debe estar accesible públicamente (requiere autenticación).

4.  Se debe entregar:

    -   Evidencia del despliegue (pantallazo de configuración o `README` con instrucciones).

    -   URL funcional del endpoint en producción.

* * * * *

### 🧩 Alcance técnico

-   Crear y probar `Dockerfile` funcional para el backend.

-   Configurar secrets en GitHub (si se usa GitHub Actions) para credenciales de despliegue.

-   Usar el acceso directo a Azure para desplegar contenedores (ej. Azure Web App for Containers).

-   Validar que el endpoint `/chat` esté expuesto correctamente y autenticado.


🟩 Historia de Usuario 9 -- Interfaz de usuario (UI) web para acceder al chatbot
--------------------------------------------------------------------------------

**Persona**: *Diana Vargas*\
**Edad**: 33 años\
**Perfil**: Usuaria autosuficiente, espera soluciones rápidas y una experiencia fluida desde su navegador o app.

* * * * *

### 🧾 Historia

Como usuaria frecuente de ParceroGo,\
quiero acceder al chatbot desde una interfaz amigable,\
para poder interactuar visualmente con el asistente sin necesidad de instalar o configurar nada adicional.

* * * * *

### 🎯 Beneficio esperado

Mejorar la experiencia de uso general del chatbot al hacerlo más accesible y fácil de entender para personas no técnicas o con baja afinidad a interfaces de línea de comandos.

* * * * *

### ✅ Criterios de aceptación

1.  La UI debe permitir ingresar al chatbot mediante navegador web.

2.  El usuario debe poder enviar y ver mensajes en una conversación tipo "chat".

3.  Si se implementa SSO (ver Historia 8), la UI debe integrar el inicio de sesión federado y manejar el token.

4.  La UI debe mostrar claramente las respuestas del bot, incluyendo mensajes de error si los hay.

5.  Se debe respetar el diseño de tono del personaje "Parcerito" en la forma y estilo del chat.

6.  Debe haber una indicación de carga o "escribiendo..." mientras se espera respuesta del bot.

7.  Si el servidor responde con un mensaje de escalación (ver Historia 7), debe mostrarse como tal con un estilo diferenciado.

8.  El `conversation_id` debe mantenerse durante la sesión del navegador y enviarse con cada mensaje.

* * * * *

### 🧩 Alcance técnico

-   Crear una aplicación web mínima (HTML/CSS/JS o framework como React).

-   Diseñar una pantalla simple de chat que:

    -   Reciba input del usuario.

    -   Muestre respuestas del bot.

    -   Haga llamadas `POST /chat` con `Authorization` y `conversation_id`.

-   Manejar estado local del `conversation_id` y token OAuth2 si se usa SSO.

-   Mostrar mensajes con formato diferenciado entre usuario y bot.


🟩 Historia de Usuario 10 -- Inicio de sesión federado con OAuth2 (SSO) + Registro/Login desde UI
-----------------------------------------------------------------------------------------------

**Persona**: *Laura Suárez*\
**Edad**: 27 años\
**Perfil**: Ingeniera de software que espera autenticaciones modernas y una experiencia sin fricción.

* * * * *

### 🧾 Historia

Como usuaria de ParceroGo,\
quiero poder iniciar sesión en el sistema desde la interfaz web,\
para acceder al chatbot de forma segura y personalizada sin autenticaciones repetidas.

* * * * *

### 🎯 Beneficio esperado

Mantener la experiencia fluida al integrar el acceso al chatbot directamente desde la interfaz principal, sin pedir credenciales múltiples.

* * * * *

### ✅ Criterios de aceptación

1.  La UI debe incluir pantallas de:

    -   **Registro**: formulario con `nombre`, `correo`, `contraseña`

    -   **Login**: ingreso de correo y contraseña, validación y obtención de token

2.  Si se utiliza un proveedor OAuth2 (ej. Auth0 o Google), la UI debe integrar ese flujo con botón de inicio de sesión.

3.  El token (JWT o Bearer) debe guardarse en la sesión del navegador (`sessionStorage` o `localStorage`) tras el login.

4.  El token debe enviarse en cada request al endpoint `/chat` como:

    `Authorization: Bearer <token>`

5.  Si el token es inválido o está ausente, el usuario debe ser redirigido al login o mostrar un mensaje como:


    `{
      "message": "No estás autenticado. Inicia sesión para chatear.",
      "statusCode": 401
    }`

6.  El `user_id` contenido en el token debe usarse en el backend para vincular conversaciones (ver Historia 3).

7.  La interfaz debe evitar accesos al chat si el usuario no ha iniciado sesión correctamente.

* * * * *

### 🔐 Endpoint afectado

-   `POST /chat`

-   (Si no se usa proveedor externo) deben implementarse:

    -   `POST /auth/register`

    -   `POST /auth/login`

* * * * *

### 🧩 Alcance técnico

-   Si se usa **OAuth2**:

    -   Integrar botón de proveedor (ej. Google/Auth0).

    -   Manejar flujo de redirección y captura del token.

-   Si se usa **JWT local**:

    -   Crear formulario de registro y login.

    -   Validar y obtener token desde backend.

    -   Agregar endpoints `/auth/register` y `/auth/login` en el backend.

-   En ambos casos:

    -   Guardar el token en el navegador.

    -   Usarlo para autenticar llamadas al backend `/chat`.

    -   Mostrar errores de sesión expirada o inválida.

-   Documentar en `docs/auth.md` cómo funciona el flujo implementado.

* * * * *

### 🔍 Nota aclaratoria

> Esta historia depende directamente de la Historia 8 (UI). Solo se implementará si se desarrolla la interfaz. El equipo puede elegir entre usar un proveedor OAuth2 real o crear un flujo básico con JWTs emitidos por el propio backend.

🟩 Historia de Usuario 11 -- Observabilidad: Logs, métricas y health check
------------------------------------------------------------------------

**Persona**: *Felipe Arguello*\
**Edad**: 33 años\
**Perfil**: PO técnico del equipo ParceroGo. Le interesa monitorear el comportamiento del sistema para garantizar calidad, trazabilidad y estabilidad operativa.

* * * * *

### 🧾 Historia

Como responsable técnico del sistema,\
quiero tener visibilidad sobre su estado y comportamiento,\
para anticipar errores, analizar su uso y asegurar que esté funcionando correctamente.

* * * * *

### 🎯 Beneficio esperado

Obtener trazabilidad técnica y analítica sobre el uso del chatbot, facilitando la detección de problemas y la evaluación de desempeño.

* * * * *

### ✅ Criterios de aceptación

1.  El sistema debe generar logs estructurados en cada request a `/chat`, incluyendo:

    -   `timestamp`

    -   `conversation_id`

    -   `user_id` (si aplica)

    -   tipo de respuesta (`normal`, `escalated`, `error`)

    -   duración de la respuesta (ms)

2.  Debe haber un endpoint público para verificar el estado del servicio:

    -   `GET /healthz`

    -   Debe responder:


        `{
          "status": "ok",
          "timestamp": "2025-07-27T16:40:00Z"
        }`

        con `statusCode`: `200`

3.  Debe haber un endpoint protegido que devuelva métricas básicas:

    -   `GET /metrics`

    -   Requiere token admin (o auth básica)

    -   Devuelve (ejemplo):


        `{
          "total_requests": 125,
          "avg_response_time_ms": 456,
          "total_escalations": 14,
          "active_conversations": 7
        }`

* * * * *

### 🔐 Endpoints nuevos

-   `GET /healthz` (público)

-   `GET /metrics` (protegido)

* * * * *

### 🛠️ Alcance técnico

-   Instrumentar los endpoints existentes con logs estructurados.

-   Contar e incrementar métricas (uso de variables globales o solución ligera).

-   Exponer el endpoint `/metrics` con autenticación.

-   Documentar en `docs/observability.md` los criterios monitoreados y cómo visualizar resultados.






