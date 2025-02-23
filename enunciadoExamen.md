### Parte 1: Modificación de Modelos y Base de Datos (2/2.5 puntos)

#### 1. Añadir un campo obligatorio en eventos
- Modifica el modelo `Evento` para incluir un nuevo campo `precio` (DecimalField con dos decimales).
- Asegúrate de que el campo es obligatorio.
- Añade al menos un evento hardcodeado en el panel de administración de Django. Un superusuario es `admin/admin`.

**Rúbrica (0.5 puntos):**
- 0.25 puntos: Modificación correcta del modelo y campo obligatorio.
- 0.25 puntos: Inserción de eventos en el panel de administración.

#### 2. Añadir un campo en reservas
- Modifica el modelo `Reserva` para incluir un nuevo campo `precio_total` (DecimalField con dos decimales).
- Este campo debe calcularse multiplicando el número de entradas reservadas por el precio del evento.

**Rúbrica (0.5/1 puntos):**
- 0.5 puntos: Implementación correcta del campo `precio_total`.
- + 0.5 puntos: Cálculo automático del precio total en base a la cantidad de entradas.

#### 3. Crear un nuevo modelo `Calificacion`
Este modelo debe contener los siguientes campos:
- `evento`: Evento calificado.
- `usuario`: Usuario que califica.
- `puntuacion`: Valor entre 1 y 5.
- `fecha_creacion`: Fecha en la que se realizó la calificación.

**Rúbrica (1 punto):**
- 0.5 puntos: Creación correcta del modelo con todas las relaciones necesarias.
- 0.5 puntos: Validación de la puntuación entre 1 y 5.

---

### Parte 2: Implementación de Endpoints REST con APIView (8 puntos)

#### 4. Creación de un endpoint para crear reservas con cálculo de precio total
- Implementa un nuevo endpoint `POST /reservas/crear/` que permita a un usuario realizar una reserva.
- La reserva debe incluir el número de entradas y estar asociada a un evento.
- El campo `precio_total` debe calcularse  multiplicando el número de entradas por el precio del evento.
- Valida que el número de entradas sea mayor a 0 y que el evento exista.

**Rúbrica (2.5 puntos):**
- 1 punto: Implementación del endpoint con validaciones correctas.
- 1 punto: Correcta asociación del precio total con la cantidad de entradas.
- 0.5 puntos: Manejo adecuado de posibles errores.

#### 5. Creación de un endpoint para listar reservas con detalles de eventos y organizadores
Implementa un nuevo endpoint `GET /reservas/detalladas/` que devuelva todas las reservas de un usuario autenticado.

Cada reserva debe incluir información del evento (todos los campos) y del organizador (nombre y correo en caso de que exista).

Uso obligatorio de `select_related` para optimizar el rendimiento y evitar consultas innecesarias.

**Rúbrica (2 puntos):**
- 1 punto: Implementación correcta del endpoint.
- 1 punto: Uso adecuado de `select_related` para mejorar el rendimiento.

#### 6. Crear un endpoint para que los usuarios califiquen eventos
- Implementa el endpoint `POST /eventos/{id}/calificar/` que permita a los participantes calificar un evento en el que han asistido.
- Asegúrate de que:
  - Solo los usuarios con una reserva confirmada en el evento puedan calificarlo.
  - Se valide que la puntuación esté entre 1 y 5.

**Rúbrica (3.5 puntos):**
- 1.5 puntos: Implementación correcta del endpoint con validaciones adecuadas.
- 1 punto: Restricción para que solo los usuarios con reserva confirmada puedan calificar.
- 1 punto: Validación de puntuación dentro del rango permitido.

### **ENTREGA:**
- Graba un vídeo en el que se vea todo lo que se solicita en la rúbrica. Agregaciones en el panel de administración, archivo models.py modificado, endpoints probados desde Postman.
- Añade el código de tu proyecto, el archivo conexiones_navegador y tu vídeo de captura de pantalla a un archivo comprimido. Súbelo a Google Classroom.

