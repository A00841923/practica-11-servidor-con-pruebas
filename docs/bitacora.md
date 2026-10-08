# Ejercicios

## Ejercicio O — Dos decisiones de `conftest.py`

### Pregunta 1

Cada prueba registra a sus personas con un sufijo al azar (por ejemplo, `ana.f07ea4b1`). ¿Qué pasaría si todas usaran `ana`?

### Respuesta

La segunda prueba fallaría al registrarla porque recibiría un error `409` de "ya existe". Además, la segunda corrida de `pytest` también fallaría. Con el sufijo al azar, cada prueba tiene sus propias personas y se pueden correr las veces que sea, en cualquier orden.

### Pregunta 2

Las pruebas corren contra el PostgreSQL de verdad, no contra una base falsa. ¿Qué se gana? ¿Qué se pierde?

### Respuesta

Se gana que las pruebas comprueban lo que realmente hace el servidor. Por ejemplo, una prueba de permisos contra una base de datos falsa no demostraría que la real respeta esos permisos.

Se pierde velocidad y se necesita tener Docker encendido. Las pruebas de la app de la Práctica 11 eligieron lo contrario, usando un servidor de mentira, porque ahí lo que se prueba es la app.

---

## Ejercicio B4 — La carrera

### Pregunta

Las cuatro pruebas mandan los envíos uno después del otro. ¿Qué parte de crear no ejecuta ninguna? ¿Cómo escribirías una prueba que sí la ejecute?

### Respuesta

El `except IntegrityError` solo corre si dos envíos con la misma clave pasan por `ya_publicado` al mismo tiempo. Una prueba secuencial nunca logra esa situación.

Para provocarla se necesitan dos hilos que manden la petición a la vez, usando `threading` y una barrera que los suelte juntos. Se tendría que repetir varias veces porque no siempre ocurre la colisión.

Se comprobó manualmente para esta guía que, con cuatro envíos simultáneos durante veinte repeticiones, PostgreSQL rechazó 57 filas repetidas y quedaron exactamente veinte avisos. Como se comprobó a mano y no con una prueba automática, esto debe indicarse así en la matriz del Bloque D.

---

## Ejercicio D2 — Tres filas de su reto

### Pregunta

Escojan tres requisitos de su backlog: uno de seguridad, uno funcional y uno que hoy no puedan demostrar. Escriban su fila completa, con el estado honesto.

### Respuesta

Se deben elegir:

- Un requisito de seguridad.
- Un requisito funcional.
- Un requisito que actualmente no se pueda demostrar.

El criterio debe poder comprobarse sin opinar. Por ejemplo, **"responde 403 y el aviso sigue"** en lugar de **"es seguro"**.

La prueba debe tener un nombre que pueda encontrarse en la evidencia. Además, el requisito que no se pueda demostrar debe tener el estado **Pendiente** o **Parcialmente cumplido**, indicando el motivo.