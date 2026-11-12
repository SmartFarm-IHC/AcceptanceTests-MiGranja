# Pruebas de aceptación – MiGranja

```gherkin
# language: es
@EP01 @US01
Característica: Inicio de sesión
  Como usuario registrado, quiero iniciar sesión con mi correo y contraseña para acceder de manera segura a MiGranja.

  Escenario: Happy path - credenciales válidas
    Dado que el usuario tiene una cuenta activa
    Cuando ingresa su correo y contraseña correctos y presiona “Ingresar”
    Entonces el sistema le da acceso y muestra el panel principal de su granja.

  Escenario: Unhappy - credenciales incorrectas
    Dado que el usuario ingresa una contraseña incorrecta
    Cuando presiona “Ingresar”
    Entonces el sistema muestra el mensaje “Correo o contraseña incorrectos” y no permite el acceso.

  Escenario: Unhappy - bloqueo por intentos
    Dado que el usuario falló cinco intentos seguidos
    Cuando intenta ingresar nuevamente
    Entonces el sistema bloquea el acceso por 15 minutos y le sugiere recuperar su contraseña.

  Escenario: Preferencia - recordar sesión
    Dado que el usuario usa siempre el mismo dispositivo
    Cuando marca “Recordarme” al iniciar sesión
    Entonces el sistema mantiene su sesión abierta en ese dispositivo.
```

```gherkin
# language: es
@EP01 @US02
Característica: Registro de usuario
  Como nuevo usuario, quiero registrar mis datos personales para crear una cuenta en MiGranja.

  Escenario: Happy path - registro válido
    Dado que el usuario es nuevo
    Cuando completa su nombre, correo, teléfono y contraseña con datos válidos y presiona “Siguiente”
    Entonces el sistema guarda sus datos y continúa con el registro de la granja.

  Escenario: Unhappy - correo ya registrado
    Dado que el correo ingresado ya existe en el sistema
    Cuando el usuario intenta continuar
    Entonces el sistema muestra el mensaje “Este correo ya está en uso” y no crea la cuenta.

  Escenario: Unhappy - contraseña débil
    Dado que la contraseña no cumple los requisitos de seguridad
    Cuando el usuario envía el formulario
    Entonces el sistema indica los requisitos faltantes y no permite continuar.
```

```gherkin
# language: es
@EP01 @US03
Característica: Selección de plan
  Como nuevo usuario, quiero elegir entre los planes Básico, Pro o Premium para usar las funciones adecuadas al tamaño de mi granja.

  Escenario: Happy path - plan seleccionado
    Dado que el usuario está en la pantalla “Nuestros planes”
    Cuando elige un plan y presiona “Continuar”
    Entonces el sistema asocia el plan a su cuenta y finaliza el registro.

  Escenario: Alt - plan gratuito por defecto
    Dado que el usuario no desea pagar por ahora
    Cuando elige el plan Básico
    Entonces el sistema activa la cuenta sin solicitar datos de pago.

  Escenario: Unhappy - sin plan seleccionado
    Dado que el usuario no eligió ningún plan
    Cuando presiona “Continuar”
    Entonces el sistema le indica que debe seleccionar un plan para terminar el registro.
```

```gherkin
# language: es
@EP01 @US04
Característica: Confirmación de registro
  Como nuevo usuario, quiero recibir una confirmación después de crear mi cuenta para saber que el registro se realizó correctamente.

  Escenario: Happy path - cuenta creada
    Dado que el usuario completó todos los pasos del registro
    Cuando el sistema crea la cuenta
    Entonces muestra la pantalla “Cuenta creada correctamente” con el botón “Continuar”.

  Escenario: Happy path - correo de bienvenida
    Dado que la cuenta fue creada
    Cuando finaliza el registro
    Entonces el sistema envía un correo de bienvenida al usuario.

  Escenario: Unhappy - error al crear la cuenta
    Dado que ocurre un error en el servidor
    Cuando el sistema intenta crear la cuenta
    Entonces muestra un mensaje de error y conserva los datos ingresados para reintentar.
```

```gherkin
# language: es
@EP01 @US05
Característica: Recuperación de contraseña
  Como usuario registrado, quiero solicitar la recuperación de mi contraseña mediante mi correo para volver a acceder a MiGranja.

  Escenario: Happy path - envío de código
    Dado que el usuario ingresa su correo registrado
    Cuando selecciona “¿Olvidaste tu contraseña?” y presiona “Enviar”
    Entonces el sistema envía un código de verificación a ese correo.

  Escenario: Unhappy - correo no registrado
    Dado que el correo ingresado no está registrado
    Cuando el usuario solicita la recuperación
    Entonces el sistema le indica que no existe una cuenta con ese correo.

  Escenario: Alt - reenviar código
    Dado que el usuario no recibió el código
    Cuando presiona “Reenviar código” después de un minuto
    Entonces el sistema envía un nuevo código.
```

```gherkin
# language: es
@EP01 @US06
Característica: Validar código de recuperación
  Como usuario, quiero ingresar el código enviado a mi correo para verificar mi identidad antes de cambiar mi contraseña.

  Escenario: Happy path - código correcto
    Dado que el usuario recibió el código
    Cuando lo ingresa correctamente
    Entonces el sistema valida su identidad y muestra la pantalla para crear una nueva contraseña.

  Escenario: Unhappy - código incorrecto
    Dado que el usuario ingresa un código erróneo
    Cuando presiona “Validar”
    Entonces el sistema muestra “Código incorrecto” y permite intentarlo de nuevo.

  Escenario: Unhappy - código vencido
    Dado que pasaron más de 15 minutos desde el envío
    Cuando el usuario ingresa el código
    Entonces el sistema indica que el código caducó y ofrece enviar uno nuevo.
```

```gherkin
# language: es
@EP01 @US07
Característica: Crear nueva contraseña
  Como usuario verificado, quiero establecer una nueva contraseña para recuperar el acceso a mi cuenta.

  Escenario: Happy path - contraseña actualizada
    Dado que el usuario validó su código
    Cuando ingresa y confirma una nueva contraseña válida
    Entonces el sistema la actualiza y lo redirige al inicio de sesión.

  Escenario: Unhappy - contraseñas no coinciden
    Dado que la confirmación no coincide con la nueva contraseña
    Cuando el usuario presiona “Guardar”
    Entonces el sistema muestra que las contraseñas no coinciden.

  Escenario: Unhappy - contraseña anterior
    Dado que el usuario ingresa la misma contraseña que tenía
    Cuando intenta guardar
    Entonces el sistema le pide elegir una contraseña diferente.
```

```gherkin
# language: es
@EP01 @US08
Característica: Registrar datos de la granja
  Como nuevo usuario, quiero registrar los datos de mi granja para que MiGranja se adapte a mi unidad ganadera.

  Escenario: Happy path - datos completos
    Dado que el usuario completó sus datos personales
    Cuando ingresa el nombre de la granja, departamento, tipo de ganado y cantidad aproximada de animales y presiona “Siguiente”
    Entonces el sistema guarda la granja y muestra los planes.

  Escenario: Unhappy - campos obligatorios vacíos
    Dado que el usuario dejó vacío el nombre de la granja
    Cuando intenta continuar
    Entonces el sistema resalta el campo y no permite avanzar.

  Escenario: Alt - completar después
    Dado que el usuario no conoce la cantidad exacta de animales
    Cuando deja ese campo vacío
    Entonces el sistema le permite continuar y completarlo más adelante desde su cuenta.
```

```gherkin
# language: es
@EP02 @US09
Característica: Panel principal
  Como productor ganadero, quiero ver un resumen general de mi granja al iniciar sesión para conocer rápidamente el estado de mi operación.

  Escenario: Happy path - resumen cargado
    Dado que el usuario tiene animales y lotes registrados
    Cuando ingresa a MiGranja
    Entonces el sistema muestra el panel con el total de animales, lotes, registros recientes y alertas.

  Escenario: Unhappy - granja sin datos
    Dado que el usuario aún no registra animales
    Cuando ingresa al panel
    Entonces el sistema muestra un mensaje de bienvenida y el botón “Registrar mi primer animal”.

  Escenario: Unhappy - error de conexión
    Dado que no hay conexión a internet
    Cuando el usuario abre el panel
    Entonces el sistema muestra los últimos datos cargados e indica la fecha de la última actualización.
```

```gherkin
# language: es
@EP02 @US10
Característica: Indicadores de la granja
  Como productor ganadero, quiero ver indicadores de animales activos, lotes y vacunas pendientes para conocer el estado general del ganado.

  Escenario: Happy path - indicadores actualizados
    Dado que existen registros en la granja
    Cuando el usuario abre el panel
    Entonces el sistema muestra los indicadores de animales activos, lotes activos y vacunas pendientes.

  Escenario: Alt - ver detalle del indicador
    Dado que el usuario quiere más información
    Cuando toca un indicador
    Entonces el sistema abre el listado correspondiente.

  Escenario: Unhappy - datos incompletos
    Dado que algunos animales no tienen lote asignado
    Cuando se calculan los indicadores
    Entonces el sistema los muestra como “Sin lote” para que el usuario los regularice.
```

```gherkin
# language: es
@EP02 @US11
Característica: Recordatorios de actividades
  Como encargado de granja, quiero recibir recordatorios de vacunaciones y alimentaciones programadas para no olvidar ninguna actividad.

  Escenario: Happy path - recordatorio enviado
    Dado que existe una vacunación programada para mañana
    Cuando llega la hora configurada
    Entonces el sistema envía una notificación al encargado.

  Escenario: Preferencia - horario del recordatorio
    Dado que el encargado empieza su jornada a las 6:00 a. m.
    Cuando configura la hora de los recordatorios
    Entonces el sistema envía las notificaciones a esa hora.

  Escenario: Unhappy - notificaciones desactivadas
    Dado que el usuario desactivó las notificaciones del dispositivo
    Cuando hay una actividad pendiente
    Entonces el sistema la muestra igualmente en el panel principal.
```

```gherkin
# language: es
@EP02 @US12
Característica: Alertas prioritarias
  Como productor ganadero, quiero ver alertas ordenadas por prioridad para atender primero los casos más urgentes.

  Escenario: Happy path - alertas ordenadas
    Dado que existen vacunas vencidas y animales sin registros recientes
    Cuando el usuario abre las alertas
    Entonces el sistema las muestra ordenadas de mayor a menor prioridad.

  Escenario: Alt - marcar como atendida
    Dado que el usuario resolvió una alerta
    Cuando la marca como “Atendida”
    Entonces el sistema la quita de la lista de pendientes.

  Escenario: Unhappy - sin alertas
    Dado que no hay actividades pendientes
    Cuando el usuario abre las alertas
    Entonces el sistema muestra el mensaje “Todo al día”.
```

```gherkin
# language: es
@EP03 @US13
Característica: Listado de animales
  Como productor ganadero, quiero ver el listado de mis animales con su código y lote para tener una vista general de mi ganado.

  Escenario: Happy path - listado cargado
    Dado que existen animales registrados
    Cuando el usuario ingresa a “Mis animales”
    Entonces el sistema muestra el listado con código, raza, sexo y lote de cada animal.

  Escenario: Unhappy - sin animales
    Dado que la granja no tiene animales registrados
    Cuando el usuario abre el listado
    Entonces el sistema muestra el botón “Registrar animal”.

  Escenario: Alt - ordenar listado
    Dado que el usuario quiere ver primero los más recientes
    Cuando elige “Ordenar por fecha de registro”
    Entonces el sistema reordena el listado.
```

```gherkin
# language: es
@EP03 @US14
Característica: Detalle del animal
  Como productor ganadero, quiero consultar la ficha de un animal para conocer sus datos y su estado actual.

  Escenario: Happy path - ficha completa
    Dado que el animal existe
    Cuando el usuario lo selecciona
    Entonces el sistema muestra su código, raza, sexo, edad, lote, ubicación actual y últimos registros.

  Escenario: Alt - acceso desde otra pantalla
    Dado que el usuario está viendo el detalle de un corral o de un movimiento
    Cuando toca el código del animal
    Entonces el sistema abre su ficha.

  Escenario: Unhappy - animal dado de baja
    Dado que el animal fue dado de baja
    Cuando el usuario abre su ficha
    Entonces el sistema la muestra en modo de solo lectura con el motivo de la baja.
```

```gherkin
# language: es
@EP03 @US15
Característica: Registrar animal
  Como encargado de granja, quiero registrar un animal con su código, raza, sexo, fecha de nacimiento y lote para identificarlo correctamente.

  Escenario: Happy path - registro exitoso
    Dado que el encargado completa los datos obligatorios
    Cuando presiona “Registrar”
    Entonces el sistema guarda el animal y lo muestra en el listado.

  Escenario: Unhappy - código duplicado
    Dado que el código ingresado ya pertenece a otro animal
    Cuando el encargado intenta guardar
    Entonces el sistema muestra “Este código ya está registrado” y no crea el animal.

  Escenario: Unhappy - campos obligatorios vacíos
    Dado que falta el código o el sexo del animal
    Cuando el encargado intenta guardar
    Entonces el sistema resalta los campos faltantes.

  Escenario: Alt - código automático
    Dado que la granja no usa códigos propios
    Cuando el encargado elige “Generar código”
    Entonces el sistema asigna un código correlativo, por ejemplo BOV-043.
```

```gherkin
# language: es
@EP03 @US16
Característica: Editar datos del animal
  Como encargado de granja, quiero editar los datos de un animal para corregir errores sin crear registros duplicados.

  Escenario: Happy path - edición guardada
    Dado que el encargado abre la ficha del animal
    Cuando modifica un dato y presiona “Guardar”
    Entonces el sistema actualiza la información y registra quién y cuándo hizo el cambio.

  Escenario: Unhappy - código en uso
    Dado que el encargado cambia el código por uno que ya existe
    Cuando intenta guardar
    Entonces el sistema rechaza el cambio.

  Escenario: Alt - cancelar edición
    Dado que el encargado cambió de opinión
    Cuando presiona “Cancelar”
    Entonces el sistema descarta los cambios.
```

```gherkin
# language: es
@EP03 @US17
Característica: Dar de baja un animal
  Como productor ganadero, quiero dar de baja a un animal vendido o muerto para mantener actualizado mi inventario de ganado.

  Escenario: Happy path - baja registrada
    Dado que el animal fue vendido
    Cuando el usuario selecciona “Dar de baja”, elige el motivo “Venta” y confirma
    Entonces el sistema lo retira de los animales activos y conserva su historial.

  Escenario: Unhappy - motivo sin seleccionar
    Dado que el usuario no eligió un motivo
    Cuando intenta confirmar la baja
    Entonces el sistema le pide seleccionar uno.

  Escenario: Alt - reactivar animal
    Dado que la baja fue un error
    Cuando el usuario elige “Reactivar”
    Entonces el sistema devuelve el animal a la lista de activos.
```

```gherkin
# language: es
@EP03 @US18
Característica: Foto del animal
  Como encargado de granja, quiero agregar una foto al registro del animal para reconocerlo visualmente con mayor facilidad.

  Escenario: Happy path - foto agregada
    Dado que el encargado está en la ficha del animal
    Cuando toma o sube una foto
    Entonces el sistema la guarda y la muestra en la ficha.

  Escenario: Unhappy - archivo no válido
    Dado que el archivo no es una imagen o supera los 5 MB
    Cuando el encargado intenta subirlo
    Entonces el sistema muestra un mensaje de error.

  Escenario: Alt - cambiar foto
    Dado que el animal ya tiene una foto
    Cuando el encargado sube una nueva
    Entonces el sistema reemplaza la anterior.
```

```gherkin
# language: es
@EP03 @US19
Característica: Buscar animal por código
  Como encargado de granja, quiero buscar un animal escribiendo su código para encontrarlo en segundos.

  Escenario: Happy path - animal encontrado
    Dado que el animal existe
    Cuando el encargado escribe su código en el buscador
    Entonces el sistema muestra el resultado y permite abrir su ficha.

  Escenario: Unhappy - código inexistente
    Dado que el código no existe
    Cuando el encargado realiza la búsqueda
    Entonces el sistema muestra “No se encontró ningún animal con ese código”.

  Escenario: Alt - búsqueda parcial
    Dado que el encargado solo recuerda parte del código
    Cuando escribe “BOV-00”
    Entonces el sistema muestra todas las coincidencias.
```

```gherkin
# language: es
@EP03 @US20
Característica: Filtrar animales
  Como productor ganadero, quiero filtrar mis animales por lote, sexo o raza para encontrar grupos específicos.

  Escenario: Happy path - filtro aplicado
    Dado que existen animales de distintos lotes
    Cuando el usuario filtra por “Lote Norte”
    Entonces el sistema muestra solo los animales de ese lote.

  Escenario: Alt - combinar filtros
    Dado que el usuario quiere ver hembras Holstein
    Cuando combina los filtros de sexo y raza
    Entonces el sistema muestra solo los animales que cumplen ambas condiciones.

  Escenario: Unhappy - sin resultados
    Dado que ningún animal cumple los filtros
    Cuando el usuario los aplica
    Entonces el sistema muestra “Sin resultados” y el botón “Limpiar filtros”.
```

```gherkin
# language: es
@EP04 @US21
Característica: Crear lote
  Como productor ganadero, quiero crear lotes para agrupar a mis animales según su etapa o propósito.

  Escenario: Happy path - lote creado
    Dado que el usuario ingresa el nombre del lote y su ubicación
    Cuando presiona “Guardar”
    Entonces el sistema crea el lote y lo muestra en el listado.

  Escenario: Unhappy - nombre repetido
    Dado que ya existe un lote con el mismo nombre
    Cuando el usuario intenta guardar
    Entonces el sistema le pide usar otro nombre.

  Escenario: Unhappy - nombre vacío
    Dado que el usuario no escribió un nombre
    Cuando intenta guardar
    Entonces el sistema resalta el campo obligatorio.
```

```gherkin
# language: es
@EP04 @US22
Característica: Listado de lotes
  Como productor ganadero, quiero ver mis lotes con su cantidad de animales y ubicación para organizar mejor el ganado.

  Escenario: Happy path - listado de lotes
    Dado que existen lotes registrados
    Cuando el usuario ingresa a “Lotes”
    Entonces el sistema muestra cada lote con su número de animales y su ubicación actual.

  Escenario: Alt - abrir historial del lote
    Dado que el usuario quiere más información
    Cuando selecciona un lote
    Entonces el sistema abre el historial de ese lote.

  Escenario: Unhappy - sin lotes
    Dado que la granja no tiene lotes
    Cuando el usuario abre el listado
    Entonces el sistema muestra el botón “Crear lote”.
```

```gherkin
# language: es
@EP04 @US23
Característica: Asignar animales a un lote
  Como encargado de granja, quiero asignar o cambiar de lote a varios animales a la vez para ahorrar tiempo.

  Escenario: Happy path - asignación múltiple
    Dado que el encargado selecciona varios animales
    Cuando elige “Asignar a lote” y escoge el destino
    Entonces el sistema actualiza el lote de todos los animales seleccionados.

  Escenario: Unhappy - sin animales seleccionados
    Dado que el encargado no seleccionó ningún animal
    Cuando intenta asignar
    Entonces el sistema le indica que debe seleccionar al menos uno.

  Escenario: Alt - registro en el historial
    Dado que se cambió el lote de un animal
    Cuando se guarda la asignación
    Entonces el sistema registra el cambio en el historial del animal.
```

```gherkin
# language: es
@EP04 @US24
Característica: Editar o cerrar lote
  Como productor ganadero, quiero editar o cerrar un lote para mantener ordenada la organización de mi granja.

  Escenario: Happy path - lote editado
    Dado que el usuario abre un lote
    Cuando cambia su nombre o descripción y guarda
    Entonces el sistema actualiza la información.

  Escenario: Unhappy - lote con animales
    Dado que el lote todavía tiene animales
    Cuando el usuario intenta cerrarlo
    Entonces el sistema le pide reasignarlos antes de continuar.

  Escenario: Alt - lote cerrado
    Dado que el lote quedó vacío
    Cuando el usuario lo cierra
    Entonces el sistema lo oculta del listado activo y conserva su historial.
```

```gherkin
# language: es
@EP05 @US25
Característica: Registrar alimentación de un animal
  Como encargado de granja, quiero registrar el alimento y la cantidad que recibe un animal para llevar el control de su alimentación.

  Escenario: Happy path - registro guardado
    Dado que el encargado selecciona un animal
    Cuando ingresa el tipo de alimento, la cantidad y la fecha y presiona “Registrar”
    Entonces el sistema guarda el registro en el historial del animal.

  Escenario: Unhappy - cantidad inválida
    Dado que el encargado ingresa una cantidad igual a cero o negativa
    Cuando intenta guardar
    Entonces el sistema muestra un error en ese campo.

  Escenario: Alt - fecha y hora automáticas
    Dado que el encargado registra la alimentación en el momento
    Cuando abre el formulario
    Entonces el sistema completa automáticamente la fecha y la hora actuales.
```

```gherkin
# language: es
@EP05 @US26
Característica: Registrar alimentación por lote
  Como encargado de granja, quiero registrar la alimentación de un lote completo en un solo paso para no repetir el registro animal por animal.

  Escenario: Happy path - registro por lote
    Dado que el encargado selecciona un lote
    Cuando ingresa el alimento y la cantidad total y confirma
    Entonces el sistema registra la alimentación en el historial del lote y de cada uno de sus animales.

  Escenario: Unhappy - lote vacío
    Dado que el lote no tiene animales
    Cuando el encargado intenta registrar la alimentación
    Entonces el sistema le avisa que el lote está vacío.

  Escenario: Preferencia - alimento frecuente
    Dado que el encargado usa siempre el mismo concentrado
    Cuando abre el formulario
    Entonces el sistema le sugiere el último alimento registrado.
```

```gherkin
# language: es
@EP05 @US27
Característica: Historial de alimentación
  Como productor ganadero, quiero consultar el historial de alimentación de un animal o lote para verificar que reciba la ración adecuada.

  Escenario: Happy path - historial mostrado
    Dado que existen registros de alimentación
    Cuando el usuario abre la pestaña “Alimentación” del animal
    Entonces el sistema muestra los registros ordenados por fecha.

  Escenario: Alt - filtrar por fechas
    Dado que el usuario quiere revisar un mes en específico
    Cuando selecciona el rango de fechas
    Entonces el sistema muestra solo los registros de ese periodo.

  Escenario: Unhappy - sin registros
    Dado que el animal no tiene registros de alimentación
    Cuando el usuario abre la pestaña
    Entonces el sistema muestra “Aún no hay registros de alimentación”.
```

```gherkin
# language: es
@EP05 @US28
Característica: Programar alimentación
  Como encargado de granja, quiero programar alimentaciones recurrentes para un lote para recibir un recordatorio en cada horario.

  Escenario: Happy path - programación creada
    Dado que el encargado selecciona un lote
    Cuando define el alimento, la cantidad, los días y la hora
    Entonces el sistema crea la programación y genera los recordatorios.

  Escenario: Alt - marcar como realizada
    Dado que llegó la hora programada
    Cuando el encargado confirma desde el recordatorio
    Entonces el sistema registra la alimentación automáticamente.

  Escenario: Unhappy - horario repetido
    Dado que ya existe una programación en el mismo horario para ese lote
    Cuando el encargado intenta guardar
    Entonces el sistema le avisa del conflicto.
```

```gherkin
# language: es
@EP06 @US29
Característica: Registrar vacunación
  Como encargado de granja, quiero registrar la vacuna, la dosis y la fecha aplicada a un animal para mantener su control sanitario.

  Escenario: Happy path - vacuna registrada
    Dado que el encargado selecciona un animal
    Cuando ingresa la vacuna, la dosis y la fecha y presiona “Registrar”
    Entonces el sistema guarda la vacunación en el historial del animal.

  Escenario: Alt - próxima dosis
    Dado que la vacuna requiere refuerzo
    Cuando el encargado indica la fecha de la próxima dosis
    Entonces el sistema crea un recordatorio para esa fecha.

  Escenario: Unhappy - fecha futura
    Dado que el encargado ingresa una fecha de aplicación posterior a hoy
    Cuando intenta guardar
    Entonces el sistema le indica que la fecha no es válida.
```

```gherkin
# language: es
@EP06 @US30
Característica: Vacunación por lote
  Como encargado de granja, quiero registrar una vacunación para todo un lote para ahorrar tiempo en campañas sanitarias.

  Escenario: Happy path - lote vacunado
    Dado que el encargado selecciona un lote
    Cuando registra la vacuna y confirma
    Entonces el sistema la registra en el historial de cada animal del lote.

  Escenario: Alt - excluir animales
    Dado que algunos animales no fueron vacunados
    Cuando el encargado los desmarca antes de confirmar
    Entonces el sistema registra la vacuna solo en los animales marcados.

  Escenario: Unhappy - pérdida de conexión
    Dado que se pierde la conexión durante el guardado
    Cuando el sistema no logra registrar la vacunación
    Entonces informa el error y conserva los datos para reintentar.
```

```gherkin
# language: es
@EP06 @US31
Característica: Vacunas pendientes
  Como productor ganadero, quiero ver las vacunas pendientes y vencidas de mi ganado para cumplir el calendario sanitario.

  Escenario: Happy path - listado de pendientes
    Dado que existen próximas dosis programadas
    Cuando el usuario abre “Vacunas pendientes”
    Entonces el sistema muestra cada animal o lote con la vacuna y la fecha programada.

  Escenario: Unhappy - vacuna vencida
    Dado que la fecha de una dosis ya pasó sin registrarse
    Cuando el usuario revisa el listado
    Entonces el sistema la marca como “Vencida” y la envía a las alertas prioritarias.

  Escenario: Unhappy - sin pendientes
    Dado que todas las vacunas están al día
    Cuando el usuario abre el listado
    Entonces el sistema muestra “No hay vacunas pendientes”.
```

```gherkin
# language: es
@EP06 @US32
Característica: Registrar tratamiento sanitario
  Como encargado de granja, quiero registrar tratamientos y medicamentos aplicados a un animal para tener su historial de salud completo.

  Escenario: Happy path - tratamiento registrado
    Dado que un animal está enfermo
    Cuando el encargado registra el diagnóstico, el medicamento, la dosis y la duración
    Entonces el sistema guarda el tratamiento en su historial.

  Escenario: Alt - tratamiento en curso
    Dado que el tratamiento dura varios días
    Cuando el encargado lo registra
    Entonces el sistema muestra al animal con la etiqueta “En tratamiento” hasta la fecha de fin.

  Escenario: Unhappy - datos incompletos
    Dado que falta el medicamento o la dosis
    Cuando el encargado intenta guardar
    Entonces el sistema resalta los campos obligatorios.
```

```gherkin
# language: es
@EP07 @US33
Característica: Detalle de ubicación
  Como productor ganadero, quiero consultar un corral o potrero y los animales que contiene para saber cómo está distribuido mi ganado.

  Escenario: Happy path - ubicación con animales
    Dado que el corral tiene animales asignados
    Cuando el usuario abre su detalle
    Entonces el sistema muestra el nombre de la ubicación, la cantidad de animales y la lista de sus códigos.

  Escenario: Alt - ir al animal
    Dado que el usuario necesita información de un animal del corral
    Cuando lo selecciona
    Entonces el sistema abre la ficha del animal.

  Escenario: Alt - registrar movimiento
    Dado que el usuario quiere mover animales del corral
    Cuando presiona “Registrar movimiento”
    Entonces el sistema abre el formulario con el origen completado.

  Escenario: Unhappy - ubicación vacía
    Dado que el corral no tiene animales
    Cuando el usuario abre su detalle
    Entonces el sistema muestra “No hay animales en esta ubicación”.
```

```gherkin
# language: es
@EP07 @US34
Característica: Historial de movimientos
  Como productor ganadero, quiero ver los movimientos recientes de mis animales y lotes para saber cuándo y hacia dónde se trasladaron. 88

  Escenario: Happy path - movimientos agrupados
    Dado que existen movimientos registrados
    Cuando el usuario ingresa a “Movimientos”
    Entonces el sistema los muestra agrupados por día (Hoy, Ayer) con origen, destino y hora.

  Escenario: Alt - filtrar por animal, lote o fecha
    Dado que el usuario busca un movimiento específico
    Cuando usa los filtros Animal, Lote o Fecha
    Entonces el sistema muestra solo los movimientos que coinciden.

  Escenario: Unhappy - sin movimientos
    Dado que no se han registrado movimientos
    Cuando el usuario abre la pantalla
    Entonces el sistema muestra el botón “Nuevo movimiento”.
```

```gherkin
# language: es
@EP07 @US35
Característica: Registrar movimiento
  Como encargado de granja, quiero registrar el traslado de un animal o lote indicando origen, destino, fecha y hora para mantener actualizada su ubicación.

  Escenario: Happy path - movimiento registrado
    Dado que el encargado elige “Animal”, selecciona BOV-001, origen Corral 1 y destino Corral 2
    Cuando presiona “Registrar”
    Entonces el sistema guarda el movimiento y actualiza la ubicación del animal.

  Escenario: Alt - mover un lote
    Dado que el encargado elige “Lote”
    Cuando registra el movimiento
    Entonces el sistema actualiza la ubicación de todos los animales del lote.

  Escenario: Unhappy - origen y destino iguales
    Dado que el destino es igual al origen
    Cuando el encargado intenta registrar
    Entonces el sistema indica que el destino debe ser diferente.

  Escenario: Unhappy - campos vacíos
    Dado que falta seleccionar el animal o el destino
    Cuando el encargado presiona “Registrar”
    Entonces el sistema resalta los campos obligatorios.
```

```gherkin
# language: es
@EP07 @US36
Característica: Detalle de movimiento
  Como productor ganadero, quiero ver el detalle de un movimiento con su responsable para verificar quién y cuándo trasladó al animal.

  Escenario: Happy path - detalle completo
    Dado que el usuario selecciona un movimiento
    Cuando se abre el detalle
    Entonces el sistema muestra el animal, el origen, el destino, la fecha, la hora y el responsable.

  Escenario: Alt - ver animal
    Dado que el usuario quiere revisar al animal trasladado
    Cuando presiona “Ver animal”
    Entonces el sistema abre su ficha.

  Escenario: Alt - corregir movimiento
    Dado que el movimiento tiene un error
    Cuando el encargado lo edita
    Entonces el sistema guarda la corrección y conserva el registro del cambio.
```

```gherkin
# language: es
@EP08 @US37
Característica: Buscar historial
  Como productor ganadero, quiero buscar el historial de un animal por su código o seleccionar un lote para consultar su información rápidamente.

  Escenario: Happy path - búsqueda por código
    Dado que el animal existe
    Cuando el usuario escribe su código y presiona buscar
    Entonces el sistema abre el historial integral del animal.

  Escenario: Alt - búsqueda por lote
    Dado que el usuario quiere ver un grupo
    Cuando selecciona un lote en “Buscar por lote”
    Entonces el sistema abre el historial del lote.

  Escenario: Alt - búsquedas recientes
    Dado que el usuario consultó animales antes
    Cuando abre la pantalla
    Entonces el sistema muestra sus búsquedas recientes para acceder con un toque.

  Escenario: Unhappy - código no encontrado
    Dado que el código no existe
    Cuando el usuario busca
    Entonces el sistema muestra “No se encontró el animal”.
```

```gherkin
# language: es
@EP08 @US38
Característica: Historial integral del animal
  Como productor ganadero, quiero ver en una línea de tiempo la alimentación, vacunación y movimientos de un animal para conocer toda su trazabilidad.

  Escenario: Happy path - línea de tiempo
    Dado que el animal tiene registros
    Cuando el usuario abre su historial
    Entonces el sistema muestra todos los eventos ordenados del más reciente al más antiguo.

  Escenario: Alt - pestañas por tipo
    Dado que el usuario solo quiere ver vacunas
    Cuando selecciona la pestaña “Vacunas”
    Entonces el sistema muestra solo los eventos de vacunación.

  Escenario: Unhappy - sin registros
    Dado que el animal fue registrado recientemente
    Cuando el usuario abre su historial
    Entonces el sistema indica que aún no tiene eventos.
```

```gherkin
# language: es
@EP08 @US39
Característica: Filtrar historial
  Como productor ganadero, quiero filtrar el historial por tipo de registro y rango de fechas para revisar solo la información que necesito.

  Escenario: Happy path - filtro aplicado
    Dado que el usuario está en un historial
    Cuando marca los tipos de registro, define las fechas “Desde” y “Hasta” y presiona “Aplicar”
    Entonces el sistema muestra solo los eventos que cumplen esos criterios.

  Escenario: Alt - limpiar filtros
    Dado que hay filtros aplicados
    Cuando el usuario presiona “Limpiar”
    Entonces el sistema vuelve a mostrar todo el historial.

  Escenario: Unhappy - fechas inválidas
    Dado que la fecha “Desde” es posterior a la fecha “Hasta”
    Cuando el usuario presiona “Aplicar”
    Entonces el sistema muestra un error y no aplica el filtro.
```

```gherkin
# language: es
@EP08 @US40
Característica: Historial del lote
  Como productor ganadero, quiero ver el historial de un lote completo para conocer las actividades realizadas a todo el grupo.

  Escenario: Happy path - historial del lote
    Dado que el lote tiene registros
    Cuando el usuario lo abre
    Entonces el sistema muestra la cantidad de animales y las alimentaciones, vacunaciones y movimientos del lote agrupados por día.

  Escenario: Alt - filtrar historial del lote
    Dado que el usuario quiere ver solo movimientos
    Cuando presiona “Filtrar” y elige ese tipo
    Entonces el sistema muestra solo los movimientos del lote.

  Escenario: Unhappy - lote sin actividad
    Dado que el lote no tiene registros
    Cuando el usuario abre su historial
    Entonces el sistema muestra “Este lote aún no tiene actividades registradas”.
```

```gherkin
# language: es
@EP09 @US41
Característica: Resumen operativo
  Como productor ganadero, quiero ver un resumen semanal de animales activos, lotes, registros y alertas para evaluar cómo se está gestionando mi granja.

  Escenario: Happy path - resumen semanal
    Dado que existen registros en la semana
    Cuando el usuario abre “Resumen de granja”
    Entonces el sistema muestra los animales y lotes activos, la cantidad de registros por tipo y las alertas pendientes.

  Escenario: Alt - generar reporte
    Dado que el usuario necesita compartir el resumen
    Cuando presiona “Generar reporte”
    Entonces el sistema crea un reporte descargable del periodo.

  Escenario: Unhappy - semana sin registros
    Dado que no hubo registros en la semana
    Cuando el usuario abre el resumen
    Entonces el sistema muestra los contadores en cero y sugiere registrar actividades.
```

```gherkin
# language: es
@EP07 @US42
Característica: Gestionar ubicaciones
  Como productor ganadero, quiero registrar los corrales y potreros de mi granja para poder asignar y mover animales entre ellos.

  Escenario: Happy path - ubicación creada
    Dado que el usuario ingresa el nombre y el tipo de ubicación (corral o potrero)
    Cuando presiona “Guardar”
    Entonces el sistema la crea y la habilita como origen o destino de movimientos.

  Escenario: Unhappy - nombre repetido
    Dado que ya existe una ubicación con ese nombre
    Cuando el usuario intenta guardar
    Entonces el sistema le pide otro nombre.

  Escenario: Unhappy - eliminar ubicación con animales
    Dado que la ubicación tiene animales
    Cuando el usuario intenta eliminarla
    Entonces el sistema le pide moverlos antes.
```

```gherkin
# language: es
@EP09 @US43
Característica: Reporte de vacunación
  Como productor ganadero, quiero generar un reporte de las vacunas aplicadas en un periodo para presentarlo ante una inspección sanitaria.

  Escenario: Happy path - reporte generado
    Dado que existen vacunaciones en el periodo
    Cuando el usuario elige las fechas y presiona “Generar”
    Entonces el sistema muestra el reporte con animal, vacuna, dosis y fecha.

  Escenario: Alt - filtrar por lote
    Dado que el usuario solo necesita un lote
    Cuando lo selecciona antes de generar
    Entonces el sistema incluye solo los animales de ese lote.

  Escenario: Unhappy - periodo sin datos
    Dado que no hay vacunaciones en el periodo
    Cuando el usuario genera el reporte
    Entonces el sistema indica que no hay datos para mostrar.
```

```gherkin
# language: es
@EP09 @US44
Característica: Reporte de alimentación
  Como productor ganadero, quiero ver un reporte del alimento consumido por lote para controlar el gasto en alimentación.

  Escenario: Happy path - consumo por lote
    Dado que existen registros de alimentación
    Cuando el usuario genera el reporte del mes
    Entonces el sistema muestra la cantidad total de alimento por lote y por tipo.

  Escenario: Alt - gráfico de consumo
    Dado que el usuario prefiere ver la información de forma visual
    Cuando elige la vista de gráfico
    Entonces el sistema muestra un gráfico de barras por lote.

  Escenario: Unhappy - periodo sin datos
    Dado que no hay registros en el periodo
    Cuando el usuario genera el reporte
    Entonces el sistema indica que no hay datos.
```

```gherkin
# language: es
@EP09 @US45
Característica: Exportar historial del animal
  Como productor ganadero, quiero exportar el historial de un animal en PDF para compartirlo con un veterinario o comprador.

  Escenario: Happy path - PDF descargado
    Dado que el usuario está en el historial del animal
    Cuando presiona “Exportar PDF”
    Entonces el sistema genera un documento con la ficha y todos los eventos del animal.

  Escenario: Unhappy - historial vacío
    Dado que el animal no tiene registros
    Cuando el usuario intenta exportar
    Entonces el sistema indica que no hay información para exportar.

  Escenario: Unhappy - error al generar
    Dado que ocurre un error en el servidor
    Cuando el usuario intenta descargar
    Entonces el sistema lo notifica y ofrece reintentar.
```

```gherkin
# language: es
@EP09 @US46
Característica: Exportar reportes a Excel
  Como productor ganadero, quiero exportar mis reportes a Excel para trabajarlos o guardarlos fuera de la plataforma.

  Escenario: Happy path - Excel descargado
    Dado que el usuario generó un reporte
    Cuando presiona “Exportar a Excel”
    Entonces el sistema descarga un archivo con las mismas columnas del reporte.

  Escenario: Unhappy - plan sin permiso
    Dado que el usuario tiene el plan Básico
    Cuando intenta exportar a Excel
    Entonces el sistema le indica que la función está disponible en los planes Pro y Premium.

  Escenario: Unhappy - reporte vacío
    Dado que el reporte no tiene datos
    Cuando el usuario intenta exportar
    Entonces el sistema bloquea la acción.
```

```gherkin
# language: es
@EP09 @US47
Característica: Invitar encargado de granja
  Como productor ganadero, quiero invitar a mis encargados a MiGranja para que registren las actividades diarias del ganado.

  Escenario: Happy path - invitación enviada
    Dado que el productor ingresa el correo del encargado
    Cuando presiona “Invitar”
    Entonces el sistema envía una invitación para unirse a la granja.

  Escenario: Unhappy - límite del plan
    Dado que el plan contratado alcanzó su número máximo de usuarios
    Cuando el productor intenta invitar a otro
    Entonces el sistema le sugiere mejorar su plan.

  Escenario: Alt - invitación aceptada
    Dado que el encargado acepta la invitación
    Cuando crea su contraseña
    Entonces el sistema lo agrega a la granja con el rol de encargado.
```

```gherkin
# language: es
@EP09 @US48
Característica: Roles y permisos
  Como productor ganadero, quiero definir qué puede hacer cada usuario de mi granja para proteger la información y evitar cambios no autorizados.

  Escenario: Happy path - rol asignado
    Dado que el encargado pertenece a la granja
    Cuando el productor le asigna el rol “Encargado”
    Entonces el sistema le permite registrar y consultar información, pero no eliminar animales ni ver reportes.

  Escenario: Alt - quitar acceso
    Dado que un encargado dejó de trabajar en la granja
    Cuando el productor le retira el acceso
    Entonces el sistema cierra su sesión y conserva los registros que hizo.

  Escenario: Unhappy - acción no permitida
    Dado que un encargado intenta dar de baja un animal
    Cuando presiona la opción
    Entonces el sistema le indica que no tiene permisos para esa acción.
```

```gherkin
# language: es
@EP01 @US49
Característica: Mi cuenta y plan
  Como usuario, quiero ver y modificar mis datos personales y consultar mi plan actual para administrar mi cuenta de MiGranja.

  Escenario: Happy path - datos actualizados
    Dado que el usuario ingresa a “Mi cuenta”
    Cuando modifica su teléfono y presiona “Guardar”
    Entonces el sistema actualiza sus datos.

  Escenario: Alt - cambiar de plan
    Dado que el usuario necesita más funciones
    Cuando elige “Cambiar plan” y selecciona Pro o Premium
    Entonces el sistema actualiza su plan y habilita las nuevas funciones.

  Escenario: Unhappy - correo en uso
    Dado que el usuario cambia su correo por uno que ya está registrado
    Cuando intenta guardar
    Entonces el sistema rechaza el cambio.
```

```gherkin
# language: es
@EP01 @US50
Característica: Cerrar sesión
  Como usuario, quiero cerrar sesión de manera segura para proteger la información de mi granja.

  Escenario: Happy path - sesión cerrada
    Dado que el usuario tiene una sesión activa
    Cuando presiona “Cerrar sesión” y confirma
    Entonces el sistema cierra la sesión y muestra la pantalla de inicio de sesión.

  Escenario: Alt - cierre por inactividad
    Dado que el usuario no usa la aplicación durante 30 minutos
    Cuando intenta realizar una acción
    Entonces el sistema le pide iniciar sesión nuevamente.

  Escenario: Unhappy - registros sin guardar
    Dado que el usuario tiene un formulario sin guardar
    Cuando intenta cerrar sesión
    Entonces el sistema le advierte que perderá los cambios.
```

