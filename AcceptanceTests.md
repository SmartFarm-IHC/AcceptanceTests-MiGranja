# AcceptanceTests-MiGranja
# Acceptance Tests – MiGranja

## US01 – Inicio de sesión

**Épica:** EP01

**Historia:** Como usuario registrado, quiero iniciar sesión con mi correo y contraseña para acceder de manera segura a MiGranja.

### Escenario 1: Happy path - credenciales válidas
Dado que el usuario tiene una cuenta activa, cuando ingresa su correo y contraseña correctos y presiona “Ingresar”, entonces el sistema le da acceso y muestra el panel principal de su granja.

### Escenario 2: Unhappy - credenciales incorrectas
Dado que el usuario ingresa una contraseña incorrecta, cuando presiona “Ingresar”, entonces el sistema muestra el mensaje “Correo o contraseña incorrectos” y no permite el acceso.

### Escenario 3: Unhappy - bloqueo por intentos
Dado que el usuario falló cinco intentos seguidos, cuando intenta ingresar nuevamente, entonces el sistema bloquea el acceso por 15 minutos y le sugiere recuperar su contraseña.

### Escenario 4: Preferencia - recordar sesión
Dado que el usuario usa siempre el mismo dispositivo, cuando marca “Recordarme” al iniciar sesión, entonces el sistema mantiene su sesión abierta en ese dispositivo.

## US02 – Registro de usuario

**Épica:** EP01

**Historia:** Como nuevo usuario, quiero registrar mis datos personales para crear una cuenta en MiGranja.

### Escenario 1: Happy path - registro válido
Dado que el usuario es nuevo, cuando completa su nombre, correo, teléfono y contraseña con datos válidos y presiona “Siguiente”, entonces el sistema guarda sus datos y continúa con el registro de la granja.

### Escenario 2: Unhappy - correo ya registrado
Dado que el correo ingresado ya existe en el sistema, cuando el usuario intenta continuar, entonces el sistema muestra el mensaje “Este correo ya está en uso” y no crea la cuenta.

### Escenario 3: Unhappy - contraseña débil
Dado que la contraseña no cumple los requisitos de seguridad, cuando el usuario envía el formulario, entonces el sistema indica los requisitos faltantes y no permite continuar.

## US03 – Selección de plan

**Épica:** EP01

**Historia:** Como nuevo usuario, quiero elegir entre los planes Básico, Pro o Premium para usar las funciones adecuadas al tamaño de mi granja.

### 74

### Escenario 1: Happy path - plan seleccionado
Dado que el usuario está en la pantalla “Nuestros planes”, cuando elige un plan y presiona “Continuar”, entonces el sistema asocia el plan a su cuenta y finaliza el registro.

### Escenario 2: Alt - plan gratuito por defecto
Dado que el usuario no desea pagar por ahora, cuando elige el plan Básico, entonces el sistema activa la cuenta sin solicitar datos de pago.

### Escenario 3: Unhappy - sin plan seleccionado
Dado que el usuario no eligió ningún plan, cuando presiona “Continuar”, entonces el sistema le indica que debe seleccionar un plan para terminar el registro.

## US04 – Confirmación de registro

**Épica:** EP01

**Historia:** Como nuevo usuario, quiero recibir una confirmación después de crear mi cuenta para saber que el registro se realizó correctamente.

### Escenario 1: Happy path - cuenta creada
Dado que el usuario completó todos los pasos del registro, cuando el sistema crea la cuenta, entonces muestra la pantalla “Cuenta creada correctamente” con el botón “Continuar”.

### Escenario 2: Happy path - correo de bienvenida
Dado que la cuenta fue creada, cuando finaliza el registro, entonces el sistema envía un correo de bienvenida al usuario.

### Escenario 3: Unhappy - error al crear la cuenta
Dado que ocurre un error en el servidor, cuando el sistema intenta crear la cuenta, entonces muestra un mensaje de error y conserva los datos ingresados para reintentar.

## US05 – Recuperación de contraseña

**Épica:** EP01

**Historia:** Como usuario registrado, quiero solicitar la recuperación de mi contraseña mediante mi correo para volver a acceder a MiGranja.

### Escenario 1: Happy path - envío de código
Dado que el usuario ingresa su correo registrado, cuando selecciona “¿Olvidaste tu contraseña?” y presiona “Enviar”, entonces el sistema envía un código de verificación a ese correo. 75

### Escenario 2: Unhappy - correo no registrado
Dado que el correo ingresado no está registrado, cuando el usuario solicita la recuperación, entonces el sistema le indica que no existe una cuenta con ese correo.

### Escenario 3: Alt - reenviar código
Dado que el usuario no recibió el código, cuando presiona “Reenviar código” después de un minuto, entonces el sistema envía un nuevo código.

## US06 – Validar código de recuperación

**Épica:** EP01

**Historia:** Como usuario, quiero ingresar el código enviado a mi correo para verificar mi identidad antes de cambiar mi contraseña.

### Escenario 1: Happy path - código correcto
Dado que el usuario recibió el código, cuando lo ingresa correctamente, entonces el sistema valida su identidad y muestra la pantalla para crear una nueva contraseña.

### Escenario 2: Unhappy - código incorrecto
Dado que el usuario ingresa un código erróneo, cuando presiona “Validar”, entonces el sistema muestra “Código incorrecto” y permite intentarlo de nuevo.

### Escenario 3: Unhappy - código vencido
Dado que pasaron más de 15 minutos desde el envío, cuando el usuario ingresa el código, entonces el sistema indica que el código caducó y ofrece enviar uno nuevo.

## US07 – Crear nueva contraseña

**Épica:** EP01

**Historia:** Como usuario verificado, quiero establecer una nueva contraseña para recuperar el acceso a mi cuenta.

### Escenario 1: Happy path - contraseña actualizada
Dado que el usuario validó su código, cuando ingresa y confirma una nueva contraseña válida, entonces el sistema la actualiza y lo redirige al inicio de sesión.

### Escenario 2: Unhappy - contraseñas no coinciden
Dado que la confirmación no coincide con la nueva contraseña, cuando el usuario presiona “Guardar”, entonces el sistema muestra que las contraseñas no coinciden. 76

### Escenario 3: Unhappy - contraseña anterior
Dado que el usuario ingresa la misma contraseña que tenía, cuando intenta guardar, entonces el sistema le pide elegir una contraseña diferente.

## US08 – Registrar datos de la granja

**Épica:** EP01

**Historia:** Como nuevo usuario, quiero registrar los datos de mi granja para que MiGranja se adapte a mi unidad ganadera.

### Escenario 1: Happy path - datos completos
Dado que el usuario completó sus datos personales, cuando ingresa el nombre de la granja, departamento, tipo de ganado y cantidad aproximada de animales y presiona “Siguiente”, entonces el sistema guarda la granja y muestra los planes.

### Escenario 2: Unhappy - campos obligatorios vacíos
Dado que el usuario dejó vacío el nombre de la granja, cuando intenta continuar, entonces el sistema resalta el campo y no permite avanzar.

### Escenario 3: Alt - completar después
Dado que el usuario no conoce la cantidad exacta de animales, cuando deja ese campo vacío, entonces el sistema le permite continuar y completarlo más adelante desde su cuenta.

## US09 – Panel principal

**Épica:** EP02

**Historia:** Como productor ganadero, quiero ver un resumen general de mi granja al iniciar sesión para conocer rápidamente el estado de mi operación.

### Escenario 1: Happy path - resumen cargado
Dado que el usuario tiene animales y lotes registrados, cuando ingresa a MiGranja, entonces el sistema muestra el panel con el total de animales, lotes, registros recientes y alertas.

### Escenario 2: Unhappy - granja sin datos
Dado que el usuario aún no registra animales, cuando ingresa al panel, entonces el sistema muestra un mensaje de bienvenida y el botón “Registrar mi primer animal”.

### Escenario 3: Unhappy - error de conexión
Dado que no hay conexión a internet, cuando el usuario abre el panel, entonces el sistema muestra los últimos datos cargados e indica la fecha de la última actualización. 77

## US10 – Indicadores de la granja

**Épica:** EP02

**Historia:** Como productor ganadero, quiero ver indicadores de animales activos, lotes y vacunas pendientes para conocer el estado general del ganado.

### Escenario 1: Happy path - indicadores actualizados
Dado que existen registros en la granja, cuando el usuario abre el panel, entonces el sistema muestra los indicadores de animales activos, lotes activos y vacunas pendientes.

### Escenario 2: Alt - ver detalle del indicador
Dado que el usuario quiere más información, cuando toca un indicador, entonces el sistema abre el listado correspondiente.

### Escenario 3: Unhappy - datos incompletos
Dado que algunos animales no tienen lote asignado, cuando se calculan los indicadores, entonces el sistema los muestra como “Sin lote” para que el usuario los regularice.

## US11 – Recordatorios de actividades

**Épica:** EP02

**Historia:** Como encargado de granja, quiero recibir recordatorios de vacunaciones y alimentaciones programadas para no olvidar ninguna actividad.

### Escenario 1: Happy path - recordatorio enviado
Dado que existe una vacunación programada para mañana, cuando llega la hora configurada, entonces el sistema envía una notificación al encargado.

### Escenario 2: Preferencia - horario del recordatorio
Dado que el encargado empieza su jornada a las 6:00 a. m., cuando configura la hora de los recordatorios, entonces el sistema envía las notificaciones a esa hora.

### Escenario 3: Unhappy - notificaciones desactivadas
Dado que el usuario desactivó las notificaciones del dispositivo, cuando hay una actividad pendiente, entonces el sistema la muestra igualmente en el panel principal.

## US12 – Alertas prioritarias 78

**Épica:** EP02

**Historia:** Como productor ganadero, quiero ver alertas ordenadas por prioridad para atender primero los casos más urgentes.

### Escenario 1: Happy path - alertas ordenadas
Dado que existen vacunas vencidas y animales sin registros recientes, cuando el usuario abre las alertas, entonces el sistema las muestra ordenadas de mayor a menor prioridad.

### Escenario 2: Alt - marcar como atendida
Dado que el usuario resolvió una alerta, cuando la marca como “Atendida”, entonces el sistema la quita de la lista de pendientes.

### Escenario 3: Unhappy - sin alertas
Dado que no hay actividades pendientes, cuando el usuario abre las alertas, entonces el sistema muestra el mensaje “Todo al día”.

## US13 – Listado de animales

**Épica:** EP03

**Historia:** Como productor ganadero, quiero ver el listado de mis animales con su código y lote para tener una vista general de mi ganado.

### Escenario 1: Happy path - listado cargado
Dado que existen animales registrados, cuando el usuario ingresa a “Mis animales”, entonces el sistema muestra el listado con código, raza, sexo y lote de cada animal.

### Escenario 2: Unhappy - sin animales
Dado que la granja no tiene animales registrados, cuando el usuario abre el listado, entonces el sistema muestra el botón “Registrar animal”.

### Escenario 3: Alt - ordenar listado
Dado que el usuario quiere ver primero los más recientes, cuando elige “Ordenar por fecha de registro”, entonces el sistema reordena el listado.

## US14 – Detalle del animal

**Épica:** EP03

**Historia:** Como productor ganadero, quiero consultar la ficha de un animal para conocer sus datos y su estado actual.

### 79

### Escenario 1: Happy path - ficha completa
Dado que el animal existe, cuando el usuario lo selecciona, entonces el sistema muestra su código, raza, sexo, edad, lote, ubicación actual y últimos registros.

### Escenario 2: Alt - acceso desde otra pantalla
Dado que el usuario está viendo el detalle de un corral o de un movimiento, cuando toca el código del animal, entonces el sistema abre su ficha.

### Escenario 3: Unhappy - animal dado de baja
Dado que el animal fue dado de baja, cuando el usuario abre su ficha, entonces el sistema la muestra en modo de solo lectura con el motivo de la baja.

## US15 – Registrar animal

**Épica:** EP03

**Historia:** Como encargado de granja, quiero registrar un animal con su código, raza, sexo, fecha de nacimiento y lote para identificarlo correctamente.

### Escenario 1: Happy path - registro exitoso
Dado que el encargado completa los datos obligatorios, cuando presiona “Registrar”, entonces el sistema guarda el animal y lo muestra en el listado.

### Escenario 2: Unhappy - código duplicado
Dado que el código ingresado ya pertenece a otro animal, cuando el encargado intenta guardar, entonces el sistema muestra “Este código ya está registrado” y no crea el animal.

### Escenario 3: Unhappy - campos obligatorios vacíos
Dado que falta el código o el sexo del animal, cuando el encargado intenta guardar, entonces el sistema resalta los campos faltantes.

### Escenario 4: Alt - código automático
Dado que la granja no usa códigos propios, cuando el encargado elige “Generar código”, entonces el sistema asigna un código correlativo, por ejemplo BOV-043.

## US16 – Editar datos del animal

**Épica:** EP03

**Historia:** Como encargado de granja, quiero editar los datos de un animal para corregir errores sin crear registros duplicados.

### 80

### Escenario 1: Happy path - edición guardada
Dado que el encargado abre la ficha del animal, cuando modifica un dato y presiona “Guardar”, entonces el sistema actualiza la información y registra quién y cuándo hizo el cambio.

### Escenario 2: Unhappy - código en uso
Dado que el encargado cambia el código por uno que ya existe, cuando intenta guardar, entonces el sistema rechaza el cambio.

### Escenario 3: Alt - cancelar edición
Dado que el encargado cambió de opinión, cuando presiona “Cancelar”, entonces el sistema descarta los cambios.

## US17 – Dar de baja un animal

**Épica:** EP03

**Historia:** Como productor ganadero, quiero dar de baja a un animal vendido o muerto para mantener actualizado mi inventario de ganado.

### Escenario 1: Happy path - baja registrada
Dado que el animal fue vendido, cuando el usuario selecciona “Dar de baja”, elige el motivo “Venta” y confirma, entonces el sistema lo retira de los animales activos y conserva su historial.

### Escenario 2: Unhappy - motivo sin seleccionar
Dado que el usuario no eligió un motivo, cuando intenta confirmar la baja, entonces el sistema le pide seleccionar uno.

### Escenario 3: Alt - reactivar animal
Dado que la baja fue un error, cuando el usuario elige “Reactivar”, entonces el sistema devuelve el animal a la lista de activos.

## US18 – Foto del animal

**Épica:** EP03

**Historia:** Como encargado de granja, quiero agregar una foto al registro del animal para reconocerlo visualmente con mayor facilidad.

### Escenario 1: Happy path - foto agregada
Dado que el encargado está en la ficha del animal, cuando toma o sube una foto, entonces el sistema la guarda y la muestra en la ficha.

### Escenario 2: Unhappy - archivo no válido
Dado que el archivo no es una imagen o supera los 5 MB, cuando el encargado intenta subirlo, entonces el sistema muestra un mensaje de error.

### Escenario 3: Alt - cambiar foto
Dado que el animal ya tiene una foto, cuando el encargado sube una nueva, entonces el sistema reemplaza la anterior.

## US19 – Buscar animal por código

**Épica:** EP03

**Historia:** Como encargado de granja, quiero buscar un animal escribiendo su código para encontrarlo en segundos.

### Escenario 1: Happy path - animal encontrado
Dado que el animal existe, cuando el encargado escribe su código en el buscador, entonces el sistema muestra el resultado y permite abrir su ficha.

### Escenario 2: Unhappy - código inexistente
Dado que el código no existe, cuando el encargado realiza la búsqueda, entonces el sistema muestra “No se encontró ningún animal con ese código”.

### Escenario 3: Alt - búsqueda parcial
Dado que el encargado solo recuerda parte del código, cuando escribe “BOV-00”, entonces el sistema muestra todas las coincidencias.

## US20 – Filtrar animales

**Épica:** EP03

**Historia:** Como productor ganadero, quiero filtrar mis animales por lote, sexo o raza para encontrar grupos específicos.

### Escenario 1: Happy path - filtro aplicado
Dado que existen animales de distintos lotes, cuando el usuario filtra por “Lote Norte”, entonces el sistema muestra solo los animales de ese lote. 82

### Escenario 2: Alt - combinar filtros
Dado que el usuario quiere ver hembras Holstein, cuando combina los filtros de sexo y raza, entonces el sistema muestra solo los animales que cumplen ambas condiciones.

### Escenario 3: Unhappy - sin resultados
Dado que ningún animal cumple los filtros, cuando el usuario los aplica, entonces el sistema muestra “Sin resultados” y el botón “Limpiar filtros”.

## US21 – Crear lote

**Épica:** EP04

**Historia:** Como productor ganadero, quiero crear lotes para agrupar a mis animales según su etapa o propósito.

### Escenario 1: Happy path - lote creado
Dado que el usuario ingresa el nombre del lote y su ubicación, cuando presiona “Guardar”, entonces el sistema crea el lote y lo muestra en el listado.

### Escenario 2: Unhappy - nombre repetido
Dado que ya existe un lote con el mismo nombre, cuando el usuario intenta guardar, entonces el sistema le pide usar otro nombre.

### Escenario 3: Unhappy - nombre vacío
Dado que el usuario no escribió un nombre, cuando intenta guardar, entonces el sistema resalta el campo obligatorio.

## US22 – Listado de lotes

**Épica:** EP04

**Historia:** Como productor ganadero, quiero ver mis lotes con su cantidad de animales y ubicación para organizar mejor el ganado.

### Escenario 1: Happy path - listado de lotes
Dado que existen lotes registrados, cuando el usuario ingresa a “Lotes”, entonces el sistema muestra cada lote con su número de animales y su ubicación actual.

### Escenario 2: Alt - abrir historial del lote
Dado que el usuario quiere más información, cuando selecciona un lote, entonces el sistema abre el historial de ese lote.

### Escenario 3: Unhappy - sin lotes
Dado que la granja no tiene lotes, cuando el usuario abre el listado, entonces el sistema muestra el botón “Crear lote”.

## US23 – Asignar animales a un lote

**Épica:** EP04

**Historia:** Como encargado de granja, quiero asignar o cambiar de lote a varios animales a la vez para ahorrar tiempo.

### Escenario 1: Happy path - asignación múltiple
Dado que el encargado selecciona varios animales, cuando elige “Asignar a lote” y escoge el destino, entonces el sistema actualiza el lote de todos los animales seleccionados.

### Escenario 2: Unhappy - sin animales seleccionados
Dado que el encargado no seleccionó ningún animal, cuando intenta asignar, entonces el sistema le indica que debe seleccionar al menos uno.

### Escenario 3: Alt - registro en el historial
Dado que se cambió el lote de un animal, cuando se guarda la asignación, entonces el sistema registra el cambio en el historial del animal.

## US24 – Editar o cerrar lote

**Épica:** EP04

**Historia:** Como productor ganadero, quiero editar o cerrar un lote para mantener ordenada la organización de mi granja.

### Escenario 1: Happy path - lote editado
Dado que el usuario abre un lote, cuando cambia su nombre o descripción y guarda, entonces el sistema actualiza la información.

### Escenario 2: Unhappy - lote con animales
Dado que el lote todavía tiene animales, cuando el usuario intenta cerrarlo, entonces el sistema le pide reasignarlos antes de continuar.

### Escenario 3: Alt - lote cerrado
Dado que el lote quedó vacío, cuando el usuario lo cierra, entonces el sistema lo oculta del listado activo y conserva su historial.

## US25 – Registrar alimentación de un animal

**Épica:** EP05

**Historia:** Como encargado de granja, quiero registrar el alimento y la cantidad que recibe un animal para llevar el control de su alimentación.

### Escenario 1: Happy path - registro guardado
Dado que el encargado selecciona un animal, cuando ingresa el tipo de alimento, la cantidad y la fecha y presiona “Registrar”, entonces el sistema guarda el registro en el historial del animal.

### Escenario 2: Unhappy - cantidad inválida
Dado que el encargado ingresa una cantidad igual a cero o negativa, cuando intenta guardar, entonces el sistema muestra un error en ese campo.

### Escenario 3: Alt - fecha y hora automáticas
Dado que el encargado registra la alimentación en el momento, cuando abre el formulario, entonces el sistema completa automáticamente la fecha y la hora actuales.

## US26 – Registrar alimentación por lote

**Épica:** EP05

**Historia:** Como encargado de granja, quiero registrar la alimentación de un lote completo en un solo paso para no repetir el registro animal por animal.

### Escenario 1: Happy path - registro por lote
Dado que el encargado selecciona un lote, cuando ingresa el alimento y la cantidad total y confirma, entonces el sistema registra la alimentación en el historial del lote y de cada uno de sus animales.

### Escenario 2: Unhappy - lote vacío
Dado que el lote no tiene animales, cuando el encargado intenta registrar la alimentación, entonces el sistema le avisa que el lote está vacío.

### Escenario 3: Preferencia - alimento frecuente
Dado que el encargado usa siempre el mismo concentrado, cuando abre el formulario, entonces el sistema le sugiere el último alimento registrado.

## US27 – Historial de alimentación

**Épica:** EP05

**Historia:** Como productor ganadero, quiero consultar el historial de alimentación de un animal o lote para verificar que reciba la ración adecuada.

### Escenario 1: Happy path - historial mostrado
Dado que existen registros de alimentación, cuando el usuario abre la pestaña “Alimentación” del animal, entonces el sistema muestra los registros ordenados por fecha.

### Escenario 2: Alt - filtrar por fechas
Dado que el usuario quiere revisar un mes en específico, cuando selecciona el rango de fechas, entonces el sistema muestra solo los registros de ese periodo.

### Escenario 3: Unhappy - sin registros
Dado que el animal no tiene registros de alimentación, cuando el usuario abre la pestaña, entonces el sistema muestra “Aún no hay registros de alimentación”.

## US28 – Programar alimentación

**Épica:** EP05

**Historia:** Como encargado de granja, quiero programar alimentaciones recurrentes para un lote para recibir un recordatorio en cada horario.

### Escenario 1: Happy path - programación creada
Dado que el encargado selecciona un lote, cuando define el alimento, la cantidad, los días y la hora, entonces el sistema crea la programación y genera los recordatorios.

### Escenario 2: Alt - marcar como realizada
Dado que llegó la hora programada, cuando el encargado confirma desde el recordatorio, entonces el sistema registra la alimentación automáticamente.

### Escenario 3: Unhappy - horario repetido
Dado que ya existe una programación en el mismo horario para ese lote, cuando el encargado intenta guardar, entonces el sistema le avisa del conflicto.

## US29 – Registrar vacunación

**Épica:** EP06

**Historia:** Como encargado de granja, quiero registrar la vacuna, la dosis y la fecha aplicada a un animal para mantener su control sanitario.

### Escenario 1: Happy path - vacuna registrada
Dado que el encargado selecciona un animal, cuando ingresa la vacuna, la dosis y la fecha y presiona “Registrar”, entonces el sistema guarda la vacunación en el historial del animal.

### Escenario 2: Alt - próxima dosis
Dado que la vacuna requiere refuerzo, cuando el encargado indica la fecha de la próxima dosis, entonces el sistema crea un recordatorio para esa fecha. 86

### Escenario 3: Unhappy - fecha futura
Dado que el encargado ingresa una fecha de aplicación posterior a hoy, cuando intenta guardar, entonces el sistema le indica que la fecha no es válida.

## US30 – Vacunación por lote

**Épica:** EP06

**Historia:** Como encargado de granja, quiero registrar una vacunación para todo un lote para ahorrar tiempo en campañas sanitarias.

### Escenario 1: Happy path - lote vacunado
Dado que el encargado selecciona un lote, cuando registra la vacuna y confirma, entonces el sistema la registra en el historial de cada animal del lote.

### Escenario 2: Alt - excluir animales
Dado que algunos animales no fueron vacunados, cuando el encargado los desmarca antes de confirmar, entonces el sistema registra la vacuna solo en los animales marcados.

### Escenario 3: Unhappy - pérdida de conexión
Dado que se pierde la conexión durante el guardado, cuando el sistema no logra registrar la vacunación, entonces informa el error y conserva los datos para reintentar.

## US31 – Vacunas pendientes

**Épica:** EP06

**Historia:** Como productor ganadero, quiero ver las vacunas pendientes y vencidas de mi ganado para cumplir el calendario sanitario.

### Escenario 1: Happy path - listado de pendientes
Dado que existen próximas dosis programadas, cuando el usuario abre “Vacunas pendientes”, entonces el sistema muestra cada animal o lote con la vacuna y la fecha programada.

### Escenario 2: Unhappy - vacuna vencida
Dado que la fecha de una dosis ya pasó sin registrarse, cuando el usuario revisa el listado, entonces el sistema la marca como “Vencida” y la envía a las alertas prioritarias.

### Escenario 3: Unhappy - sin pendientes
Dado que todas las vacunas están al día, cuando el usuario abre el listado, entonces el sistema muestra “No hay vacunas pendientes”.

## US32 – Registrar tratamiento sanitario

**Épica:** EP06

**Historia:** Como encargado de granja, quiero registrar tratamientos y medicamentos aplicados a un animal para tener su historial de salud completo.

### Escenario 1: Happy path - tratamiento registrado
Dado que un animal está enfermo, cuando el encargado registra el diagnóstico, el medicamento, la dosis y la duración, entonces el sistema guarda el tratamiento en su historial.

### Escenario 2: Alt - tratamiento en curso
Dado que el tratamiento dura varios días, cuando el encargado lo registra, entonces el sistema muestra al animal con la etiqueta “En tratamiento” hasta la fecha de fin.

### Escenario 3: Unhappy - datos incompletos
Dado que falta el medicamento o la dosis, cuando el encargado intenta guardar, entonces el sistema resalta los campos obligatorios.

## US33 – Detalle de ubicación

**Épica:** EP07

**Historia:** Como productor ganadero, quiero consultar un corral o potrero y los animales que contiene para saber cómo está distribuido mi ganado.

### Escenario 1: Happy path - ubicación con animales
Dado que el corral tiene animales asignados, cuando el usuario abre su detalle, entonces el sistema muestra el nombre de la ubicación, la cantidad de animales y la lista de sus códigos.

### Escenario 2: Alt - ir al animal
Dado que el usuario necesita información de un animal del corral, cuando lo selecciona, entonces el sistema abre la ficha del animal.

### Escenario 3: Alt - registrar movimiento
Dado que el usuario quiere mover animales del corral, cuando presiona “Registrar movimiento”, entonces el sistema abre el formulario con el origen completado.

### Escenario 4: Unhappy - ubicación vacía
Dado que el corral no tiene animales, cuando el usuario abre su detalle, entonces el sistema muestra “No hay animales en esta ubicación”.

## US34 – Historial de movimientos

**Épica:** EP07

**Historia:** Como productor ganadero, quiero ver los movimientos recientes de mis animales y lotes para saber cuándo y hacia dónde se trasladaron. 88

### Escenario 1: Happy path - movimientos agrupados
Dado que existen movimientos registrados, cuando el usuario ingresa a “Movimientos”, entonces el sistema los muestra agrupados por día (Hoy, Ayer) con origen, destino y hora.

### Escenario 2: Alt - filtrar por animal, lote o fecha
Dado que el usuario busca un movimiento específico, cuando usa los filtros Animal, Lote o Fecha, entonces el sistema muestra solo los movimientos que coinciden.

### Escenario 3: Unhappy - sin movimientos
Dado que no se han registrado movimientos, cuando el usuario abre la pantalla, entonces el sistema muestra el botón “Nuevo movimiento”.

## US35 – Registrar movimiento

**Épica:** EP07

**Historia:** Como encargado de granja, quiero registrar el traslado de un animal o lote indicando origen, destino, fecha y hora para mantener actualizada su ubicación.

### Escenario 1: Happy path - movimiento registrado
Dado que el encargado elige “Animal”, selecciona BOV-001, origen Corral 1 y destino Corral 2, cuando presiona “Registrar”, entonces el sistema guarda el movimiento y actualiza la ubicación del animal.

### Escenario 2: Alt - mover un lote
Dado que el encargado elige “Lote”, cuando registra el movimiento, entonces el sistema actualiza la ubicación de todos los animales del lote.

### Escenario 3: Unhappy - origen y destino iguales
Dado que el destino es igual al origen, cuando el encargado intenta registrar, entonces el sistema indica que el destino debe ser diferente.

### Escenario 4: Unhappy - campos vacíos
Dado que falta seleccionar el animal o el destino, cuando el encargado presiona “Registrar”, entonces el sistema resalta los campos obligatorios.

## US36 – Detalle de movimiento

**Épica:** EP07

**Historia:** Como productor ganadero, quiero ver el detalle de un movimiento con su responsable para verificar quién y cuándo trasladó al animal.

### Escenario 1: Happy path - detalle completo
Dado que el usuario selecciona un movimiento, cuando se abre el detalle, entonces el sistema muestra el animal, el origen, el destino, la fecha, la hora y el responsable.

### Escenario 2: Alt - ver animal
Dado que el usuario quiere revisar al animal trasladado, cuando presiona “Ver animal”, entonces el sistema abre su ficha.

### Escenario 3: Alt - corregir movimiento
Dado que el movimiento tiene un error, cuando el encargado lo edita, entonces el sistema guarda la corrección y conserva el registro del cambio.

## US37 – Buscar historial

**Épica:** EP08

**Historia:** Como productor ganadero, quiero buscar el historial de un animal por su código o seleccionar un lote para consultar su información rápidamente.

### Escenario 1: Happy path - búsqueda por código
Dado que el animal existe, cuando el usuario escribe su código y presiona buscar, entonces el sistema abre el historial integral del animal.

### Escenario 2: Alt - búsqueda por lote
Dado que el usuario quiere ver un grupo, cuando selecciona un lote en “Buscar por lote”, entonces el sistema abre el historial del lote.

### Escenario 3: Alt - búsquedas recientes
Dado que el usuario consultó animales antes, cuando abre la pantalla, entonces el sistema muestra sus búsquedas recientes para acceder con un toque.

### Escenario 4: Unhappy - código no encontrado
Dado que el código no existe, cuando el usuario busca, entonces el sistema muestra “No se encontró el animal”.

## US38 – Historial integral del animal

**Épica:** EP08

**Historia:** Como productor ganadero, quiero ver en una línea de tiempo la alimentación, vacunación y movimientos de un animal para conocer toda su trazabilidad.

### Escenario 1: Happy path - línea de tiempo
Dado que el animal tiene registros, cuando el usuario abre su historial, entonces el sistema muestra todos los eventos ordenados del más reciente al más antiguo. 90

### Escenario 2: Alt - pestañas por tipo
Dado que el usuario solo quiere ver vacunas, cuando selecciona la pestaña “Vacunas”, entonces el sistema muestra solo los eventos de vacunación.

### Escenario 3: Unhappy - sin registros
Dado que el animal fue registrado recientemente, cuando el usuario abre su historial, entonces el sistema indica que aún no tiene eventos.

## US39 – Filtrar historial

**Épica:** EP08

**Historia:** Como productor ganadero, quiero filtrar el historial por tipo de registro y rango de fechas para revisar solo la información que necesito.

### Escenario 1: Happy path - filtro aplicado
Dado que el usuario está en un historial, cuando marca los tipos de registro, define las fechas “Desde” y “Hasta” y presiona “Aplicar”, entonces el sistema muestra solo los eventos que cumplen esos criterios.

### Escenario 2: Alt - limpiar filtros
Dado que hay filtros aplicados, cuando el usuario presiona “Limpiar”, entonces el sistema vuelve a mostrar todo el historial.

### Escenario 3: Unhappy - fechas inválidas
Dado que la fecha “Desde” es posterior a la fecha “Hasta”, cuando el usuario presiona “Aplicar”, entonces el sistema muestra un error y no aplica el filtro.

## US40 – Historial del lote

**Épica:** EP08

**Historia:** Como productor ganadero, quiero ver el historial de un lote completo para conocer las actividades realizadas a todo el grupo.

### Escenario 1: Happy path - historial del lote
Dado que el lote tiene registros, cuando el usuario lo abre, entonces el sistema muestra la cantidad de animales y las alimentaciones, vacunaciones y movimientos del lote agrupados por día.

### Escenario 2: Alt - filtrar historial del lote
Dado que el usuario quiere ver solo movimientos, cuando presiona “Filtrar” y elige ese tipo, entonces el sistema muestra solo los movimientos del lote.

### Escenario 3: Unhappy - lote sin actividad
Dado que el lote no tiene registros, cuando el usuario abre su historial, entonces el sistema muestra “Este lote aún no tiene actividades registradas”.

## US41 – Resumen operativo

**Épica:** EP09

**Historia:** Como productor ganadero, quiero ver un resumen semanal de animales activos, lotes, registros y alertas para evaluar cómo se está gestionando mi granja.

### Escenario 1: Happy path - resumen semanal
Dado que existen registros en la semana, cuando el usuario abre “Resumen de granja”, entonces el sistema muestra los animales y lotes activos, la cantidad de registros por tipo y las alertas pendientes.

### Escenario 2: Alt - generar reporte
Dado que el usuario necesita compartir el resumen, cuando presiona “Generar reporte”, entonces el sistema crea un reporte descargable del periodo.

### Escenario 3: Unhappy - semana sin registros
Dado que no hubo registros en la semana, cuando el usuario abre el resumen, entonces el sistema muestra los contadores en cero y sugiere registrar actividades.

## US42 – Gestionar ubicaciones

**Épica:** EP07

**Historia:** Como productor ganadero, quiero registrar los corrales y potreros de mi granja para poder asignar y mover animales entre ellos.

### Escenario 1: Happy path - ubicación creada
Dado que el usuario ingresa el nombre y el tipo de ubicación (corral o potrero), cuando presiona “Guardar”, entonces el sistema la crea y la habilita como origen o destino de movimientos.

### Escenario 2: Unhappy - nombre repetido
Dado que ya existe una ubicación con ese nombre, cuando el usuario intenta guardar, entonces el sistema le pide otro nombre.

### Escenario 3: Unhappy - eliminar ubicación con animales
Dado que la ubicación tiene animales, cuando el usuario intenta eliminarla, entonces el sistema le pide moverlos antes.

## US43 – Reporte de vacunación

**Épica:** EP09

**Historia:** Como productor ganadero, quiero generar un reporte de las vacunas aplicadas en un periodo para presentarlo ante una inspección sanitaria.

### Escenario 1: Happy path - reporte generado
Dado que existen vacunaciones en el periodo, cuando el usuario elige las fechas y presiona “Generar”, entonces el sistema muestra el reporte con animal, vacuna, dosis y fecha.

### Escenario 2: Alt - filtrar por lote
Dado que el usuario solo necesita un lote, cuando lo selecciona antes de generar, entonces el sistema incluye solo los animales de ese lote.

### Escenario 3: Unhappy - periodo sin datos
Dado que no hay vacunaciones en el periodo, cuando el usuario genera el reporte, entonces el sistema indica que no hay datos para mostrar.

## US44 – Reporte de alimentación

**Épica:** EP09

**Historia:** Como productor ganadero, quiero ver un reporte del alimento consumido por lote para controlar el gasto en alimentación.

### Escenario 1: Happy path - consumo por lote
Dado que existen registros de alimentación, cuando el usuario genera el reporte del mes, entonces el sistema muestra la cantidad total de alimento por lote y por tipo.

### Escenario 2: Alt - gráfico de consumo
Dado que el usuario prefiere ver la información de forma visual, cuando elige la vista de gráfico, entonces el sistema muestra un gráfico de barras por lote.

### Escenario 3: Unhappy - periodo sin datos
Dado que no hay registros en el periodo, cuando el usuario genera el reporte, entonces el sistema indica que no hay datos.

## US45 – Exportar historial del animal

**Épica:** EP09

**Historia:** Como productor ganadero, quiero exportar el historial de un animal en PDF para compartirlo con un veterinario o comprador.

### Escenario 1: Happy path - PDF descargado
Dado que el usuario está en el historial del animal, cuando presiona “Exportar PDF”, entonces el sistema genera un documento con la ficha y todos los eventos del animal.

### Escenario 2: Unhappy - historial vacío
Dado que el animal no tiene registros, cuando el usuario intenta exportar, entonces el sistema indica que no hay información para exportar.

### Escenario 3: Unhappy - error al generar
Dado que ocurre un error en el servidor, cuando el usuario intenta descargar, entonces el sistema lo notifica y ofrece reintentar.

## US46 – Exportar reportes a Excel

**Épica:** EP09

**Historia:** Como productor ganadero, quiero exportar mis reportes a Excel para trabajarlos o guardarlos fuera de la plataforma.

### Escenario 1: Happy path - Excel descargado
Dado que el usuario generó un reporte, cuando presiona “Exportar a Excel”, entonces el sistema descarga un archivo con las mismas columnas del reporte.

### Escenario 2: Unhappy - plan sin permiso
Dado que el usuario tiene el plan Básico, cuando intenta exportar a Excel, entonces el sistema le indica que la función está disponible en los planes Pro y Premium.

### Escenario 3: Unhappy - reporte vacío
Dado que el reporte no tiene datos, cuando el usuario intenta exportar, entonces el sistema bloquea la acción.

## US47 – Invitar encargado de granja

**Épica:** EP09

**Historia:** Como productor ganadero, quiero invitar a mis encargados a MiGranja para que registren las actividades diarias del ganado.

### Escenario 1: Happy path - invitación enviada
Dado que el productor ingresa el correo del encargado, cuando presiona “Invitar”, entonces el sistema envía una invitación para unirse a la granja.

### Escenario 2: Unhappy - límite del plan
Dado que el plan contratado alcanzó su número máximo de usuarios, cuando el productor intenta invitar a otro, entonces el sistema le sugiere mejorar su plan. 94

### Escenario 3: Alt - invitación aceptada
Dado que el encargado acepta la invitación, cuando crea su contraseña, entonces el sistema lo agrega a la granja con el rol de encargado.

## US48 – Roles y permisos

**Épica:** EP09

**Historia:** Como productor ganadero, quiero definir qué puede hacer cada usuario de mi granja para proteger la información y evitar cambios no autorizados.

### Escenario 1: Happy path - rol asignado
Dado que el encargado pertenece a la granja, cuando el productor le asigna el rol “Encargado”, entonces el sistema le permite registrar y consultar información, pero no eliminar animales ni ver reportes.

### Escenario 2: Alt - quitar acceso
Dado que un encargado dejó de trabajar en la granja, cuando el productor le retira el acceso, entonces el sistema cierra su sesión y conserva los registros que hizo.

### Escenario 3: Unhappy - acción no permitida
Dado que un encargado intenta dar de baja un animal, cuando presiona la opción, entonces el sistema le indica que no tiene permisos para esa acción.

## US49 – Mi cuenta y plan

**Épica:** EP01

**Historia:** Como usuario, quiero ver y modificar mis datos personales y consultar mi plan actual para administrar mi cuenta de MiGranja.

### Escenario 1: Happy path - datos actualizados
Dado que el usuario ingresa a “Mi cuenta”, cuando modifica su teléfono y presiona “Guardar”, entonces el sistema actualiza sus datos.

### Escenario 2: Alt - cambiar de plan
Dado que el usuario necesita más funciones, cuando elige “Cambiar plan” y selecciona Pro o Premium, entonces el sistema actualiza su plan y habilita las nuevas funciones.

### Escenario 3: Unhappy - correo en uso
Dado que el usuario cambia su correo por uno que ya está registrado, cuando intenta guardar, entonces el sistema rechaza el cambio.

## US50 – Cerrar sesión

**Épica:** EP01

**Historia:** Como usuario, quiero cerrar sesión de manera segura para proteger la información de mi granja.

### Escenario 1: Happy path - sesión cerrada
Dado que el usuario tiene una sesión activa, cuando presiona “Cerrar sesión” y confirma, entonces el sistema cierra la sesión y muestra la pantalla de inicio de sesión.

### Escenario 2: Alt - cierre por inactividad
Dado que el usuario no usa la aplicación durante 30 minutos, cuando intenta realizar una acción, entonces el sistema le pide iniciar sesión nuevamente.

### Escenario 3: Unhappy - registros sin guardar
Dado que el usuario tiene un formulario sin guardar, cuando intenta cerrar sesión, entonces el sistema le advierte que perderá los cambios.
