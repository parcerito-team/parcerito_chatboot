# Personas – ParceroGo

Este documento describe las personas (usuarios tipo) del producto **ParceroGo**, una plataforma ficticia de transporte urbano en Colombia. Estas personas fueron diseñadas para representar perfiles reales de usuarios y servir como guía para el diseño de funcionalidades, tono del chatbot y priorización del desarrollo.

---

## 👤 Persona 1: Diana Vargas – Usuaria frecuente del servicio

**Edad**: 33 años  
**Profesión**: Analista financiera  
**Ubicación**: Medellín  
**Nivel digital**: Alto  

### Contexto de uso
Usa ParceroGo todos los días para ir y volver del trabajo. Tiene buena familiaridad con apps móviles y espera respuestas claras y rápidas de los servicios que utiliza.

### Objetivos
- Ahorrar tiempo en sus desplazamientos.
- Obtener soporte eficiente cuando algo falla.

### Motivaciones
- Le molesta tener que contactar soporte por correo o esperar demasiado.
- Prefiere autoservicio siempre que sea claro y útil.

### Dolencias
- No siempre entiende por qué se le cobra una tarifa extra.
- Ha tenido problemas con métodos de pago rechazados.

### Historias asociadas
- Chat con el bot
- Simulación de RAG
- Escalación simulada

---

## 👤 Persona 2: Luis Felipe Ortega – Usuario nuevo con poca experiencia digital

**Edad**: 46 años  
**Profesión**: Técnico de refrigeración  
**Ubicación**: Bogotá  
**Nivel digital**: Medio  

### Contexto de uso
Descargó ParceroGo por recomendación de un amigo. Usa la app esporádicamente y necesita orientación clara sobre cómo usarla.

### Objetivos
- Aprender a usar la app y resolver dudas básicas.

### Motivaciones
- Quiere moverse sin depender de terceros.

### Dolencias
- No le gusta tener que registrarse en múltiples sistemas.
- No está seguro de cómo navegar entre pantallas o qué significan ciertos mensajes.

### Historias asociadas
- Registro
- Login
- Primer uso del chatbot

---

## 👤 Persona 3: Carlos Marín – Usuario técnico que prefiere SSO

**Edad**: 29 años  
**Profesión**: Desarrollador en startup  
**Ubicación**: Cali  
**Nivel digital**: Muy alto  

### Contexto de uso
Ya está autenticado en la app ParceroGo y quiere acceder al chatbot directamente desde ahí, sin repetir el login.

### Objetivos
- Usar herramientas sin duplicar autenticación.
- Acceder al chat desde interfaces integradas (ej. app móvil).

### Motivaciones
- Agilidad en los procesos, buena UX.

### Dolencias
- Repetir login en cada módulo le parece anticuado y molesto.

### Historias asociadas
- OAuth2 / SSO

---

## 👤 Persona 4: Felipe Arguello – Líder de producto (rol técnico)

**Edad**: 38 años  
**Profesión**: Líder de producto digital en ParceroGo  
**Ubicación**: Remota (Colombia)  
**Nivel digital**: Alto  

### Contexto de uso
Supervisa calidad del sistema, disponibilidad, y métricas. No usa el chatbot como usuario final, pero sí supervisa su operación.

### Objetivos
- Garantizar que el sistema esté disponible y estable.
- Detectar errores y comportamientos anómalos fácilmente.

### Motivaciones
- Quiere automatizar el monitoreo y no depender del equipo técnico constantemente.

### Dolencias
- Le frustra no tener visibilidad sobre qué está fallando cuando los usuarios se quejan.

### Historias asociadas
- Observabilidad
- Health check
- Logs
- CI/CD

---

## 🤖 Persona digital: Parcerito – Chatbot de ParceroGo

**Edad digital**: 25 años  
**Rol**: Asistente virtual de atención al cliente  
**Lenguaje**: Español colombiano, cercano pero respetuoso

### Personalidad
- Amable, empático y relajado.
- Usa expresiones locales como “parcero”, “tranqui”, o “ya te ayudo con eso 😉”.
- Evita tecnicismos y mantiene el enfoque en el usuario.

### Objetivo
- Resolver preguntas frecuentes sin necesidad de escalar a soporte humano.
- Mantener una experiencia de soporte rápida, clara y humana.

### Historias asociadas
- Interacción en `/chat`
- Simulación RAG
- Escalación simulada

