Acceptance Test -MiGranja

## US01 – Inicio de sesión

```gherkin
Feature: US01 - Inicio de sesión

  Como usuario registrado,
  quiero iniciar sesión con mi correo y contraseña
  para acceder de manera segura a MiGranja.

  Scenario: Happy path - credenciales válidas
    Given que el usuario tiene una cuenta activa
    When ingresa su correo y contraseña correctos
    And presiona el botón "Ingresar"
    Then el sistema permite el acceso
    And muestra el panel principal de su granja

  Scenario: Unhappy path - credenciales incorrectas
    Given que el usuario se encuentra en la pantalla de inicio de sesión
    When ingresa una contraseña incorrecta
    And presiona el botón "Ingresar"
    Then el sistema muestra el mensaje "Correo o contraseña incorrectos"
    And no permite el acceso

  Scenario: Unhappy path - bloqueo por intentos fallidos
    Given que el usuario ha ingresado credenciales incorrectas cinco veces consecutivas
    When intenta iniciar sesión nuevamente
    Then el sistema bloquea temporalmente el acceso durante 15 minutos
    And sugiere recuperar la contraseña

  Scenario: Preferencia - recordar sesión
    Given que el usuario se encuentra en la pantalla de inicio de sesión
    When ingresa sus credenciales correctas
    And selecciona la opción "Recordarme"
    Then el sistema mantiene la sesión abierta en ese dispositivo
```

## US02 – Registro de usuario

```gherkin
Feature: US02 - Registro de usuario

  Como nuevo usuario,
  quiero registrar mis datos personales
  para crear una cuenta en MiGranja.

  Scenario: Happy path - registro exitoso
    Given que el usuario se encuentra en el formulario de registro
    When completa sus datos personales correctamente
    And presiona el botón "Registrarse"
    Then el sistema crea su cuenta
    And muestra una confirmación del registro

  Scenario: Unhappy path - campos obligatorios vacíos
    Given que el usuario está en el formulario de registro
    When deja uno o más campos obligatorios vacíos
    And intenta registrarse
    Then el sistema solicita completar los campos faltantes
    And no crea la cuenta

  Scenario: Unhappy path - correo ya registrado
    Given que el correo ingresado pertenece a una cuenta existente
    When el usuario intenta registrarse
    Then el sistema informa que el correo ya está registrado
    And no crea una cuenta duplicada
```

## US03 – Selección de plan

```gherkin
Feature: US03 - Selección de plan

  Como nuevo usuario,
  quiero elegir entre los planes Básico, Pro o Premium
  para usar las funciones adecuadas al tamaño de mi granja.

  Scenario: Happy path - selección de plan
    Given que el usuario se encuentra en la sección de planes
    When selecciona uno de los planes disponibles
    Then el sistema registra el plan seleccionado
    And permite continuar con el proceso de registro

  Scenario: Unhappy path - no seleccionar un plan
    Given que el usuario se encuentra en la selección de planes
    When intenta continuar sin seleccionar un plan
    Then el sistema solicita elegir una opción

  Scenario: Alternativo - cambiar de plan
    Given que el usuario seleccionó un plan
    When decide seleccionar otro plan disponible
    Then el sistema actualiza la selección
    And muestra el nuevo plan elegido
```

## US04 – Confirmación de registro

```gherkin
Feature: US04 - Confirmación de registro

  Como nuevo usuario,
  quiero recibir una confirmación después de crear mi cuenta
  para saber que el registro se realizó correctamente.

  Scenario: Happy path - confirmación exitosa
    Given que el usuario completó correctamente su registro
    When el sistema procesa la creación de su cuenta
    Then muestra una confirmación de registro exitoso

  Scenario: Unhappy path - registro no completado
    Given que el usuario tiene datos incompletos en el registro
    When intenta finalizar el proceso
    Then el sistema no confirma la creación de la cuenta
    And solicita corregir los datos

  Scenario: Alternativo - continuar después de confirmar
    Given que el sistema confirmó el registro del usuario
    When el usuario selecciona continuar
    Then el sistema permite avanzar al siguiente paso
```

## US05 – Recuperación de contraseña

```gherkin
Feature: US05 - Recuperación de contraseña

  Como usuario registrado,
  quiero solicitar la recuperación de mi contraseña mediante mi correo
  para volver a acceder a mi cuenta.

  Scenario: Happy path - solicitud de recuperación
    Given que el usuario se encuentra en la opción de recuperar contraseña
    When ingresa el correo asociado a su cuenta
    And solicita la recuperación
    Then el sistema procesa la solicitud
    And envía las instrucciones de recuperación al correo

  Scenario: Unhappy path - correo no registrado
    Given que el usuario solicita recuperar su contraseña
    When ingresa un correo que no está asociado a una cuenta
    Then el sistema informa que no puede procesar la solicitud

  Scenario: Unhappy path - correo inválido
    Given que el usuario está en el formulario de recuperación
    When ingresa un correo con formato incorrecto
    Then el sistema solicita ingresar un correo válido
```

## US06 – Validar código de recuperación

```gherkin
Feature: US06 - Validar código de recuperación

  Como usuario,
  quiero ingresar el código enviado a mi correo
  para verificar mi identidad antes de cambiar mi contraseña.

  Scenario: Happy path - código válido
    Given que el usuario recibió un código de recuperación
    When ingresa el código correcto
    Then el sistema valida su identidad
    And permite continuar con el cambio de contraseña

  Scenario: Unhappy path - código incorrecto
    Given que el usuario se encuentra en la pantalla de validación
    When ingresa un código incorrecto
    Then el sistema informa que el código no es válido
    And no permite continuar

  Scenario: Unhappy path - código vacío
    Given que el usuario está en la pantalla de validación
    When intenta continuar sin ingresar el código
    Then el sistema solicita completar el campo
```

## US07 – Crear nueva contraseña

```gherkin
Feature: US07 - Crear nueva contraseña

  Como usuario verificado,
  quiero establecer una nueva contraseña
  para recuperar el acceso a mi cuenta.

  Scenario: Happy path - contraseña actualizada
    Given que el usuario verificó correctamente su identidad
    When ingresa una nueva contraseña válida
    And confirma el cambio
    Then el sistema actualiza su contraseña
    And confirma que la operación fue exitosa

  Scenario: Unhappy path - contraseña no válida
    Given que el usuario está creando una nueva contraseña
    When ingresa una contraseña que no cumple los requisitos
    Then el sistema muestra las indicaciones correspondientes
    And no actualiza la contraseña

  Scenario: Unhappy path - contraseñas diferentes
    Given que el usuario ingresa una nueva contraseña
    When la confirmación no coincide con la contraseña ingresada
    Then el sistema informa que ambas contraseñas deben coincidir
```

## US08 – Registrar datos de la granja

```gherkin
Feature: US08 - Registrar datos de la granja

  Como nuevo usuario,
  quiero registrar los datos de mi granja
  para que MiGranja se adapte a mi unidad ganadera.

  Scenario: Happy path - registro de granja
    Given que el usuario completó su registro
    When ingresa los datos solicitados de su granja
    And guarda la información
    Then el sistema registra los datos de la granja
    And permite continuar utilizando MiGranja

  Scenario: Unhappy path - datos incompletos
    Given que el usuario está registrando su granja
    When deja campos obligatorios sin completar
    And intenta guardar
    Then el sistema solicita completar la información

  Scenario: Alternativo - modificar datos antes de guardar
    Given que el usuario está completando los datos de su granja
    When modifica la información ingresada
    And guarda los cambios
    Then el sistema registra la información actualizada
```

## US09 – Panel principal

```gherkin
Feature: US09 - Panel principal

  Como productor ganadero,
  quiero ver un resumen general de mi granja al iniciar sesión
  para conocer rápidamente el estado de mi operación.

  Scenario: Happy path - visualizar panel principal
    Given que el productor inició sesión correctamente
    When accede al panel principal
    Then el sistema muestra el resumen general de su granja
    And presenta la información disponible de su operación

  Scenario: Unhappy path - información no disponible
    Given que el productor accede al panel principal
    When el sistema no puede cargar la información de la granja
    Then muestra un mensaje indicando que no fue posible cargar los datos

  Scenario: Alternativo - actualizar información del panel
    Given que el productor se encuentra en el panel principal
    When solicita actualizar la información
    Then el sistema muestra los datos disponibles más recientes
```

## US10 – Indicadores de la granja

```gherkin
Feature: US10 - Indicadores de la granja

  Como productor ganadero,
  quiero ver indicadores de animales activos, lotes y vacunas pendientes
  para conocer el estado general del ganado.

  Scenario: Happy path - visualizar indicadores
    Given que el productor accede al panel de su granja
    When consulta la sección de indicadores
    Then el sistema muestra la cantidad de animales activos
    And muestra la cantidad de lotes
    And muestra las vacunas pendientes

  Scenario: Unhappy path - información no disponible
    Given que el productor ingresa a la sección de indicadores
    When no existen datos disponibles para mostrar
    Then el sistema informa que no hay información registrada

  Scenario: Alternativo - consultar indicadores actualizados
    Given que existen nuevos registros en la granja
    When el productor actualiza los indicadores
    Then el sistema presenta las cantidades correspondientes a los registros disponibles
```

## US11 – Recordatorios de actividades

```gherkin
Feature: US11 - Recordatorios de actividades

  Como encargado de granja,
  quiero recibir recordatorios de vacunaciones y alimentaciones programadas
  para no olvidar ninguna actividad.

  Scenario: Happy path - recibir recordatorio
    Given que existen actividades de alimentación o vacunación programadas
    When se aproxima la fecha u hora de una actividad
    Then el sistema genera un recordatorio
    And muestra la actividad correspondiente

  Scenario: Alternativo - consultar recordatorios
    Given que el encargado tiene recordatorios registrados
    When accede a la sección de recordatorios
    Then el sistema muestra las actividades programadas

  Scenario: Unhappy path - no existen actividades programadas
    Given que el encargado accede a los recordatorios
    When no existen actividades pendientes
    Then el sistema informa que no hay recordatorios disponibles
```

## US12 – Alertas prioritarias

```gherkin
Feature: US12 - Alertas prioritarias

  Como productor ganadero,
  quiero ver alertas ordenadas por prioridad
  para atender primero los casos más urgentes.

  Scenario: Happy path - visualizar alertas
    Given que existen alertas registradas en la granja
    When el productor accede a la sección de alertas
    Then el sistema muestra las alertas disponibles
    And las ordena según su prioridad

  Scenario: Alternativo - consultar alerta
    Given que el productor visualiza una alerta
    When selecciona una alerta específica
    Then el sistema muestra la información correspondiente

  Scenario: Unhappy path - no existen alertas
    Given que el productor accede a la sección de alertas
    When no existen alertas registradas
    Then el sistema informa que no hay alertas disponibles
```

## US13 – Listado de animales

```gherkin
Feature: US13 - Listado de animales

  Como productor ganadero,
  quiero ver el listado de mis animales con su código y lote
  para tener una vista general de mi ganado.

  Scenario: Happy path - visualizar listado
    Given que el productor tiene animales registrados
    When accede al módulo de ganado
    Then el sistema muestra el listado de animales
    And presenta el código y lote de cada animal

  Scenario: Unhappy path - listado vacío
    Given que el productor accede al módulo de ganado
    When no existen animales registrados
    Then el sistema informa que no hay animales disponibles

  Scenario: Alternativo - consultar animal del listado
    Given que el productor visualiza el listado de animales
    When selecciona un animal
    Then el sistema permite consultar su información
```

## US14 – Detalle del animal

```gherkin
Feature: US14 - Detalle del animal

  Como productor ganadero,
  quiero consultar la ficha de un animal
  para conocer sus datos y su estado actual.

  Scenario: Happy path - consultar ficha
    Given que el productor tiene animales registrados
    When selecciona un animal del listado
    Then el sistema muestra la ficha del animal
    And presenta sus datos y estado actual

  Scenario: Unhappy path - animal inexistente
    Given que el productor intenta consultar un animal
    When el registro del animal no existe
    Then el sistema informa que no se encontró el registro

  Scenario: Alternativo - regresar al listado
    Given que el productor está visualizando la ficha de un animal
    When selecciona la opción para regresar
    Then el sistema muestra nuevamente el listado de animales
```

## US15 – Registrar animal

```gherkin
Feature: US15 - Registrar animal

  Como encargado de granja,
  quiero registrar un animal con su código, raza, sexo, fecha de nacimiento y lote
  para identificarlo correctamente.

  Scenario: Happy path - registro exitoso
    Given que el encargado se encuentra en el formulario de registro
    When ingresa el código, raza, sexo, fecha de nacimiento y lote
    And guarda la información
    Then el sistema registra el nuevo animal
    And muestra una confirmación del registro

  Scenario: Unhappy path - campos obligatorios incompletos
    Given que el encargado está registrando un animal
    When deja campos obligatorios vacíos
    And intenta guardar
    Then el sistema solicita completar los datos faltantes

  Scenario: Unhappy path - código duplicado
    Given que existe un animal con el código ingresado
    When el encargado intenta registrar otro animal con el mismo código
    Then el sistema informa que el código ya está registrado
    And evita crear un registro duplicado
```

## US16 – Editar datos del animal

```gherkin
Feature: US16 - Editar datos del animal

  Como encargado de granja,
  quiero editar los datos de un animal
  para corregir errores sin crear registros duplicados.

  Scenario: Happy path - actualizar datos
    Given que el encargado selecciona un animal registrado
    When modifica sus datos
    And guarda los cambios
    Then el sistema actualiza la información del animal

  Scenario: Unhappy path - datos obligatorios incompletos
    Given que el encargado está editando un animal
    When elimina un dato obligatorio
    And intenta guardar
    Then el sistema solicita completar la información

  Scenario: Alternativo - cancelar edición
    Given que el encargado modificó los datos de un animal
    When cancela la edición
    Then el sistema conserva la información anterior
```

## US17 – Dar de baja un animal

```gherkin
Feature: US17 - Dar de baja un animal

  Como productor ganadero,
  quiero dar de baja a un animal vendido o muerto
  para mantener actualizado mi inventario de ganado.

  Scenario: Happy path - dar de baja un animal
    Given que el productor tiene un animal registrado
    When selecciona la opción para darlo de baja
    And confirma la operación
    Then el sistema actualiza el estado del animal
    And lo retira del inventario de animales activos

  Scenario: Alternativo - cancelar baja
    Given que el productor inició el proceso de baja
    When cancela la operación
    Then el sistema mantiene el animal activo

  Scenario: Unhappy path - animal inexistente
    Given que el productor intenta dar de baja un animal
    When el registro no existe
    Then el sistema informa que no se encontró el animal
```

## US18 – Foto del animal

```gherkin
Feature: US18 - Foto del animal

  Como encargado de granja,
  quiero agregar una foto al registro del animal
  para reconocerlo visualmente con mayor facilidad.

  Scenario: Happy path - agregar fotografía
    Given que el encargado selecciona un animal registrado
    When carga una fotografía válida
    And guarda los cambios
    Then el sistema asocia la fotografía al animal

  Scenario: Unhappy path - formato no permitido
    Given que el encargado intenta agregar una fotografía
    When selecciona un archivo con formato no permitido
    Then el sistema informa que el archivo no es válido

  Scenario: Alternativo - reemplazar fotografía
    Given que el animal ya tiene una fotografía registrada
    When el encargado carga una nueva fotografía
    And guarda los cambios
    Then el sistema actualiza la imagen del animal
```

## US19 – Buscar animal por código

```gherkin
Feature: US19 - Buscar animal por código

  Como encargado de granja,
  quiero buscar un animal escribiendo su código
  para encontrarlo en segundos.

  Scenario: Happy path - búsqueda exitosa
    Given que existen animales registrados
    When el encargado ingresa un código existente en el buscador
    And realiza la búsqueda
    Then el sistema muestra el animal correspondiente

  Scenario: Unhappy path - código inexistente
    Given que el encargado se encuentra en el buscador de animales
    When ingresa un código que no está registrado
    Then el sistema informa que no se encontraron resultados

  Scenario: Unhappy path - búsqueda vacía
    Given que el encargado se encuentra en el buscador
    When intenta buscar sin ingresar un código
    Then el sistema solicita ingresar un código válido
```

## US20 – Filtrar animales

```gherkin
Feature: US20 - Filtrar animales

  Como productor ganadero,
  quiero filtrar mis animales por lote, sexo o raza
  para encontrar grupos específicos.

  Scenario: Happy path - filtrar por lote
    Given que existen animales registrados en diferentes lotes
    When el productor selecciona un lote como filtro
    Then el sistema muestra los animales pertenecientes a ese lote

  Scenario: Alternativo - filtrar por sexo o raza
    Given que el productor se encuentra en el listado de animales
    When selecciona un filtro por sexo o raza
    Then el sistema muestra los animales que cumplen el criterio seleccionado

  Scenario: Unhappy path - sin coincidencias
    Given que el productor aplica un filtro
    When ningún animal cumple el criterio seleccionado
    Then el sistema informa que no existen resultados

  Scenario: Alternativo - limpiar filtros
```

## US21 – Crear lote

```gherkin
Feature: US21 - Crear lote

  Como productor ganadero,
  quiero crear lotes para agrupar a mis animales según su etapa o propósito.

  Scenario: Happy path - crear lote
    Given que el productor se encuentra en el módulo de lotes
    When ingresa los datos requeridos del lote
    And guarda la información
    Then el sistema registra el nuevo lote
    And muestra una confirmación de creación

  Scenario: Unhappy path - datos incompletos
    Given que el productor está creando un lote
    When deja campos obligatorios vacíos
    And intenta guardar
    Then el sistema solicita completar los datos faltantes

  Scenario: Alternativo - cancelar creación
    Given que el productor está completando el formulario de un lote
    When cancela la operación
    Then el sistema no registra el nuevo lote
```

## US22 – Listado de lotes

```gherkin
Feature: US22 - Listado de lotes

  Como productor ganadero,
  quiero ver mis lotes con su cantidad de animales y ubicación
  para organizar mejor el ganado.

  Scenario: Happy path - visualizar lotes
    Given que existen lotes registrados en la granja
    When el productor accede al módulo de lotes
    Then el sistema muestra el listado de lotes
    And presenta la cantidad de animales y ubicación de cada lote

  Scenario: Unhappy path - no existen lotes
    Given que el productor accede al módulo de lotes
    When no existen lotes registrados
    Then el sistema informa que no hay lotes disponibles

  Scenario: Alternativo - consultar lote
    Given que el productor visualiza el listado de lotes
    When selecciona un lote
    Then el sistema permite consultar su información
```

## US23 – Asignar animales a un lote

```gherkin
Feature: US23 - Asignar animales a un lote

  Como encargado de granja,
  quiero asignar o cambiar de lote a varios animales a la vez
  para ahorrar tiempo.

  Scenario: Happy path - asignar animales
    Given que existen animales y lotes registrados
    When el encargado selecciona varios animales
    And elige el lote de destino
    And confirma la operación
    Then el sistema asigna los animales al lote seleccionado

  Scenario: Unhappy path - no seleccionar animales
    Given que el encargado se encuentra en la asignación de lotes
    When intenta continuar sin seleccionar animales
    Then el sistema solicita seleccionar al menos un animal

  Scenario: Unhappy path - lote inexistente
    Given que el encargado intenta asignar animales a un lote
    When el lote seleccionado no está disponible
    Then el sistema informa que no se puede realizar la asignación

  Scenario: Alternativo - cambiar animales de lote
    Given que existen animales asignados a un lote
    When el encargado selecciona otro lote de destino
    And confirma el cambio
    Then el sistema actualiza la asignación de los animales
```

## US24 – Editar o cerrar lote

```gherkin
Feature: US24 - Editar o cerrar lote

  Como productor ganadero,
  quiero editar o cerrar un lote
  para mantener ordenada la organización de mi granja.

  Scenario: Happy path - editar lote
    Given que el productor tiene un lote registrado
    When modifica los datos del lote
    And guarda los cambios
    Then el sistema actualiza la información del lote

  Scenario: Alternativo - cerrar lote
    Given que el productor selecciona un lote registrado
    When solicita cerrar el lote
    And confirma la operación
    Then el sistema actualiza el estado del lote

  Scenario: Unhappy path - datos incompletos
    Given que el productor está editando un lote
    When elimina un dato obligatorio
    And intenta guardar
    Then el sistema solicita completar la información

  Scenario: Alternativo - cancelar cierre
    Given que el productor inició el cierre de un lote
    When cancela la operación
    Then el sistema mantiene el lote sin cambios
```

## US25 – Registrar alimentación de un animal

```gherkin
Feature: US25 - Registrar alimentación de un animal

  Como encargado de granja,
  quiero registrar el alimento y la cantidad que recibe un animal
  para llevar el control de su alimentación.

  Scenario: Happy path - registrar alimentación
    Given que el encargado selecciona un animal registrado
    When ingresa el tipo de alimento y la cantidad suministrada
    And guarda el registro
    Then el sistema registra la alimentación del animal

  Scenario: Unhappy path - cantidad inválida
    Given que el encargado está registrando una alimentación
    When ingresa una cantidad igual o menor a cero
    Then el sistema solicita ingresar una cantidad válida

  Scenario: Unhappy path - datos incompletos
    Given que el encargado está completando el registro
    When omite información obligatoria
    And intenta guardar
    Then el sistema solicita completar los datos faltantes
```

## US26 – Registrar alimentación por lote

```gherkin
Feature: US26 - Registrar alimentación por lote

  Como encargado de granja,
  quiero registrar la alimentación de un lote completo en un solo paso
  para no repetir el registro animal por animal.

  Scenario: Happy path - registrar alimentación del lote
    Given que existe un lote con animales registrados
    When el encargado selecciona el lote
    And ingresa el alimento y la cantidad correspondiente
    And guarda el registro
    Then el sistema registra la alimentación para el lote seleccionado

  Scenario: Unhappy path - lote sin animales
    Given que el encargado selecciona un lote sin animales
    When intenta registrar la alimentación
    Then el sistema informa que no existen animales asignados al lote

  Scenario: Unhappy path - cantidad inválida
    Given que el encargado está registrando la alimentación del lote
    When ingresa una cantidad no válida
    Then el sistema solicita corregir la cantidad

  Scenario: Alternativo - cancelar registro
    Given que el encargado está completando el registro de alimentación
    When cancela la operación
    Then el sistema no guarda el registro
```

## US27 – Historial de alimentación

```gherkin
Feature: US27 - Historial de alimentación

  Como productor ganadero,
  quiero consultar el historial de alimentación de un animal o lote
  para verificar que reciba la ración adecuada.

  Scenario: Happy path - consultar historial
    Given que existen registros de alimentación
    When el productor selecciona un animal o lote
    And accede a su historial de alimentación
    Then el sistema muestra los registros correspondientes

  Scenario: Unhappy path - historial vacío
    Given que el productor consulta el historial de alimentación
    When no existen registros disponibles
    Then el sistema informa que no hay información registrada

  Scenario: Alternativo - consultar registros anteriores
    Given que el productor visualiza el historial de alimentación
    When revisa los registros anteriores
    Then el sistema muestra la información histórica disponible
```

## US28 – Programar alimentación

```gherkin
Feature: US28 - Programar alimentación

  Como encargado de granja,
  quiero programar alimentaciones recurrentes para un lote
  para recibir un recordatorio en cada horario.

  Scenario: Happy path - programar alimentación
    Given que existe un lote registrado
    When el encargado selecciona el lote
    And establece los horarios de alimentación
    And guarda la programación
    Then el sistema registra las alimentaciones recurrentes

  Scenario: Unhappy path - horario no válido
    Given que el encargado está programando una alimentación
    When ingresa un horario no válido
    Then el sistema solicita corregir la programación

  Scenario: Alternativo - consultar programación
    Given que el encargado tiene una alimentación programada
    When accede a la programación del lote
    Then el sistema muestra los horarios registrados
```

## US29 – Registrar vacunación

```gherkin
Feature: US29 - Registrar vacunación

  Como encargado de granja,
  quiero registrar la vacuna, la dosis y la fecha aplicada a un animal
  para mantener su control sanitario.

  Scenario: Happy path - registrar vacunación
    Given que el encargado selecciona un animal registrado
    When ingresa la vacuna, dosis y fecha de aplicación
    And guarda el registro
    Then el sistema registra la vacunación del animal

  Scenario: Unhappy path - datos incompletos
    Given que el encargado está registrando una vacunación
    When omite información obligatoria
    And intenta guardar
    Then el sistema solicita completar los datos faltantes

  Scenario: Unhappy path - dosis inválida
    Given que el encargado está completando el registro sanitario
    When ingresa una dosis no válida
    Then el sistema solicita corregir la información
```

## US30 – Vacunación por lote

```gherkin
Feature: US30 - Vacunación por lote

  Como encargado de granja,
  quiero registrar una vacunación para todo un lote
  para ahorrar tiempo en campañas sanitarias.

  Scenario: Happy path - registrar vacunación por lote
    Given que existe un lote con animales registrados
    When el encargado selecciona el lote
    And ingresa la vacuna, dosis y fecha de aplicación
    And confirma el registro
    Then el sistema registra la vacunación para los animales del lote

  Scenario: Unhappy path - lote sin animales
    Given que el encargado selecciona un lote sin animales
    When intenta registrar una vacunación
    Then el sistema informa que no existen animales asignados al lote

  Scenario: Unhappy path - datos incompletos
    Given que el encargado está registrando la vacunación del lote
    When omite información obligatoria
```

## US31 – Vacunas pendientes

```gherkin
Feature: US31 - Vacunas pendientes

  Como productor ganadero,
  quiero ver las vacunas pendientes y vencidas de mi ganado
  para cumplir el calendario sanitario.

  Scenario: Happy path - visualizar vacunas pendientes
    Given que existen vacunaciones programadas para el ganado
    When el productor accede a la sección de vacunas pendientes
    Then el sistema muestra las vacunas pendientes
    And presenta la información de cada animal correspondiente

  Scenario: Alternativo - consultar vacunas vencidas
    Given que existen vacunas cuya fecha programada ya pasó
    When el productor consulta las vacunas pendientes
    Then el sistema identifica las vacunas vencidas

  Scenario: Unhappy path - no existen vacunas pendientes
    Given que el productor accede a la sección sanitaria
    When no existen vacunas pendientes ni vencidas
    Then el sistema informa que no hay vacunas por atender
```

## US32 – Registrar tratamiento sanitario

```gherkin
Feature: US32 - Registrar tratamiento sanitario

  Como encargado de granja,
  quiero registrar tratamientos y medicamentos aplicados a un animal
  para tener su historial de salud completo.

  Scenario: Happy path - registrar tratamiento
    Given que el encargado selecciona un animal registrado
    When ingresa los datos del tratamiento y medicamento aplicado
    And guarda la información
    Then el sistema registra el tratamiento sanitario del animal

  Scenario: Unhappy path - datos incompletos
    Given que el encargado está registrando un tratamiento
    When omite información obligatoria
    And intenta guardar
    Then el sistema solicita completar los datos faltantes

  Scenario: Alternativo - consultar tratamiento registrado
    Given que el animal tiene tratamientos registrados
    When el encargado consulta su información sanitaria
    Then el sistema muestra los tratamientos disponibles
```

## US33 – Detalle de ubicación

```gherkin
Feature: US33 - Detalle de ubicación

  Como productor ganadero,
  quiero consultar un corral o potrero y los animales que contiene
  para saber cómo está distribuido mi ganado.

  Scenario: Happy path - consultar ubicación
    Given que existen corrales o potreros registrados
    When el productor selecciona una ubicación
    Then el sistema muestra los datos de la ubicación
    And presenta los animales que contiene

  Scenario: Unhappy path - ubicación inexistente
    Given que el productor busca consultar una ubicación
    When la ubicación no se encuentra registrada
    Then el sistema informa que no se encontró la ubicación

  Scenario: Unhappy path - ubicación sin animales
    Given que el productor selecciona un corral o potrero registrado
    When no existen animales asignados
    Then el sistema informa que la ubicación no contiene animales
```

## US34 – Historial de movimientos

```gherkin
Feature: US34 - Historial de movimientos

  Como productor ganadero,
  quiero ver los movimientos recientes de mis animales y lotes
  para saber cuándo y hacia dónde se trasladaron.

  Scenario: Happy path - visualizar movimientos
    Given que existen movimientos registrados
    When el productor accede al historial de movimientos
    Then el sistema muestra los movimientos recientes
    And presenta las fechas y destinos correspondientes

  Scenario: Unhappy path - historial vacío
    Given que el productor consulta el historial de movimientos
    When no existen movimientos registrados
    Then el sistema informa que no hay movimientos disponibles

  Scenario: Alternativo - consultar movimiento
    Given que el productor visualiza el historial de movimientos
    When selecciona un movimiento específico
    Then el sistema muestra la información correspondiente
```

## US35 – Registrar movimiento

```gherkin
Feature: US35 - Registrar movimiento

  Como encargado de granja,
  quiero registrar el traslado de un animal o lote indicando origen, destino, fecha y hora
  para mantener actualizada su ubicación.

  Scenario: Happy path - registrar traslado
    Given que el encargado selecciona un animal o lote registrado
    When ingresa el origen, destino, fecha y hora del traslado
    And guarda el registro
    Then el sistema registra el movimiento
    And actualiza la ubicación correspondiente

  Scenario: Unhappy path - datos incompletos
    Given que el encargado está registrando un movimiento
    When omite el origen o destino
    And intenta guardar
    Then el sistema solicita completar los datos obligatorios

  Scenario: Unhappy path - origen y destino iguales
    Given que el encargado está registrando un traslado
    When selecciona el mismo lugar como origen y destino
    Then el sistema solicita seleccionar ubicaciones diferentes

  Scenario: Alternativo - cancelar movimiento
    Given que el encargado está completando los datos del traslado
    When cancela la operación
    Then el sistema no registra el movimiento
```

## US36 – Detalle de movimiento

```gherkin
Feature: US36 - Detalle de movimiento

  Como productor ganadero,
  quiero ver el detalle de un movimiento con su responsable
  para verificar quién y cuándo trasladó al animal.

  Scenario: Happy path - consultar detalle
    Given que existen movimientos registrados
    When el productor selecciona un movimiento
    Then el sistema muestra el detalle del traslado
    And presenta el responsable y la fecha correspondiente

  Scenario: Unhappy path - movimiento inexistente
    Given que el productor intenta consultar un movimiento
    When el registro seleccionado no existe
    Then el sistema informa que no se encontró el movimiento

  Scenario: Alternativo - regresar al historial
    Given que el productor está visualizando el detalle de un movimiento
    When selecciona regresar
    Then el sistema muestra nuevamente el historial de movimientos
```

## US37 – Buscar historial

```gherkin
Feature: US37 - Buscar historial

  Como productor ganadero,
  quiero buscar el historial de un animal por su código o seleccionar un lote
  para consultar su información rápidamente.

  Scenario: Happy path - buscar historial por código
    Given que existen animales con registros históricos
    When el productor ingresa el código de un animal
    And realiza la búsqueda
    Then el sistema muestra el historial correspondiente

  Scenario: Happy path - consultar historial por lote
    Given que existen lotes registrados
    When el productor selecciona un lote
    Then el sistema muestra la información histórica del lote

  Scenario: Unhappy path - código inexistente
    Given que el productor busca un historial por código
    When ingresa un código que no está registrado
    Then el sistema informa que no se encontraron resultados

  Scenario: Unhappy path - lote sin registros
    Given que el productor selecciona un lote
    When el lote no tiene información histórica
    Then el sistema informa que no existen registros disponibles
```

## US38 – Historial integral del animal

```gherkin
Feature: US38 - Historial integral del animal

  Como productor ganadero,
  quiero ver en una línea de tiempo la alimentación, vacunación y movimientos de un animal
  para conocer toda su trazabilidad.

  Scenario: Happy path - visualizar historial integral
    Given que el animal tiene registros de actividades
    When el productor accede a su historial integral
    Then el sistema muestra una línea de tiempo
    And presenta los registros de alimentación, vacunación y movimientos

  Scenario: Unhappy path - animal sin historial
    Given que el productor consulta el historial de un animal
    When el animal no tiene actividades registradas
    Then el sistema informa que no existen registros históricos

  Scenario: Alternativo - consultar actividad
    Given que el productor visualiza la línea de tiempo
    When selecciona una actividad registrada
    Then el sistema muestra los detalles correspondientes
```

## US39 – Filtrar historial

```gherkin
Feature: US39 - Filtrar historial

  Como productor ganadero,
  quiero filtrar el historial por tipo de registro y rango de fechas
  para revisar solo la información que necesito.

  Scenario: Happy path - filtrar por tipo de registro
    Given que el productor visualiza el historial de un animal
    When selecciona un tipo de registro
    Then el sistema muestra únicamente las actividades correspondientes

  Scenario: Happy path - filtrar por rango de fechas
    Given que existen registros históricos en diferentes fechas
    When el productor establece un rango de fechas
    Then el sistema muestra los registros comprendidos en ese periodo

  Scenario: Unhappy path - rango de fechas inválido
    Given que el productor está configurando un filtro por fechas
    When establece una fecha inicial posterior a la fecha final
    Then el sistema solicita corregir el rango seleccionado

  Scenario: Unhappy path - sin coincidencias
    Given que el productor aplica filtros al historial
    When no existen registros que cumplan los criterios
    Then el sistema informa que no se encontraron resultados
```

## US40 – Historial del lote

```gherkin
Feature: US40 - Historial del lote

  Como productor ganadero,
  quiero ver el historial de un lote completo
  para conocer las actividades realizadas a todo el grupo.

  Scenario: Happy path - consultar historial del lote
    Given que existe un lote con actividades registradas
    When el productor selecciona el lote
    And accede a su historial
    Then el sistema muestra las actividades realizadas al grupo

  Scenario: Unhappy path - lote sin historial
    Given que el productor selecciona un lote registrado
    When el lote no tiene actividades registradas
    Then el sistema informa que no existen registros históricos

  Scenario: Alternativo - consultar actividad del lote
    Given que el productor visualiza el historial del lote
    When selecciona una actividad específica
    Then el sistema muestra sus detalles correspondientes
```

## US41 – Resumen operativo

```gherkin
Feature: US41 - Resumen operativo

  Como productor ganadero,
  quiero ver un resumen semanal de animales activos, lotes, registros y alertas
  para evaluar cómo se está gestionando mi granja.

  Scenario: Happy path - visualizar resumen semanal
    Given que existen registros de actividad en la granja
    When el productor accede al resumen operativo
    Then el sistema muestra los indicadores semanales
    And presenta animales activos, lotes, registros y alertas

  Scenario: Unhappy path - información no disponible
    Given que el productor accede al resumen operativo
    When no existen datos registrados durante la semana
    Then el sistema informa que no hay información disponible

  Scenario: Alternativo - consultar resumen actualizado
    Given que existen nuevos registros en la granja
    When el productor actualiza el resumen operativo
    Then el sistema muestra la información semanal actualizada
```

## US42 – Gestionar ubicaciones

```gherkin
Feature: US42 - Gestionar ubicaciones

  Como productor ganadero,
  quiero registrar los corrales y potreros de mi granja
  para poder asignar y mover animales entre ellos.

  Scenario: Happy path - registrar ubicación
    Given que el productor accede al módulo de ubicaciones
    When ingresa los datos de un corral o potrero
    And guarda la información
    Then el sistema registra la nueva ubicación

  Scenario: Unhappy path - datos incompletos
    Given que el productor está registrando una ubicación
    When omite información obligatoria
    And intenta guardar
    Then el sistema solicita completar los datos faltantes

  Scenario: Alternativo - consultar ubicaciones
    Given que existen ubicaciones registradas
    When el productor accede al listado
    Then el sistema muestra los corrales y potreros disponibles
```

## US43 – Reporte de vacunación

```gherkin
Feature: US43 - Reporte de vacunación

  Como productor ganadero,
  quiero generar un reporte de las vacunas aplicadas en un periodo
  para presentarlo ante una inspección sanitaria.

  Scenario: Happy path - generar reporte
    Given que existen registros de vacunación
    When el productor selecciona un periodo
    And solicita generar el reporte
    Then el sistema muestra las vacunas aplicadas durante ese periodo

  Scenario: Unhappy path - periodo inválido
    Given que el productor está configurando el reporte
    When selecciona un rango de fechas inválido
    Then el sistema solicita corregir el periodo

  Scenario: Unhappy path - sin registros de vacunación
    Given que el productor selecciona un periodo válido
    When no existen vacunaciones registradas en ese periodo
    Then el sistema informa que no hay datos para generar el reporte
```

## US44 – Reporte de alimentación

```gherkin
Feature: US44 - Reporte de alimentación

  Como productor ganadero,
  quiero ver un reporte del alimento consumido por lote
  para controlar el gasto en alimentación.

  Scenario: Happy path - consultar reporte
    Given que existen registros de alimentación por lote
    When el productor accede al reporte de alimentación
    Then el sistema muestra el alimento consumido por cada lote

  Scenario: Unhappy path - sin registros
    Given que el productor solicita un reporte de alimentación
    When no existen registros disponibles
    Then el sistema informa que no hay información para mostrar

  Scenario: Alternativo - consultar periodo específico
    Given que existen registros de alimentación en diferentes fechas
    When el productor selecciona un periodo
    Then el sistema muestra la información correspondiente al periodo seleccionado
```

## US45 – Exportar historial del animal

```gherkin
Feature: US45 - Exportar historial del animal

  Como productor ganadero,
  quiero exportar el historial de un animal en PDF
  para compartirlo con un veterinario o comprador.

  Scenario: Happy path - exportar historial
    Given que el productor consulta el historial de un animal
    When selecciona la opción "Exportar PDF"
    Then el sistema genera un archivo PDF
    And incluye la información histórica del animal

  Scenario: Unhappy path - historial sin información
    Given que el productor selecciona un animal sin registros históricos
    When solicita exportar su historial
    Then el sistema informa que no existen datos disponibles para exportar

  Scenario: Alternativo - descargar archivo PDF
    Given que el sistema generó correctamente el archivo PDF
    When el productor selecciona descargar
    Then el sistema permite guardar el documento
```

## US46 – Exportar reportes a Excel

```gherkin
Feature: US46 - Exportar reportes a Excel

  Como productor ganadero,
  quiero exportar mis reportes a Excel
  para trabajarlos o guardarlos fuera de la plataforma.

  Scenario: Happy path - exportar reporte
    Given que el productor tiene un reporte disponible
    When selecciona la opción "Exportar a Excel"
    Then el sistema genera un archivo Excel
    And incluye los datos del reporte seleccionado

  Scenario: Unhappy path - no existen datos para exportar
    Given que el productor consulta un reporte sin información
    When solicita exportarlo a Excel
    Then el sistema informa que no existen datos disponibles

  Scenario: Alternativo - descargar archivo Excel
    Given que el sistema generó correctamente el archivo Excel
    When el productor selecciona descargar
    Then el sistema permite guardar el archivo
```

## US47 – Invitar encargado de granja

```gherkin
Feature: US47 - Invitar encargado de granja

  Como productor ganadero,
  quiero invitar a mis encargados a MiGranja
  para que registren las actividades diarias del ganado.

  Scenario: Happy path - enviar invitación
    Given que el productor accede a la gestión de usuarios
    When ingresa los datos del encargado
    And envía la invitación
    Then el sistema registra la solicitud de invitación
    And confirma que fue enviada

  Scenario: Unhappy path - datos incompletos
    Given que el productor está invitando a un encargado
    When omite los datos obligatorios
    And intenta enviar la invitación
    Then el sistema solicita completar la información

  Scenario: Unhappy path - correo inválido
    Given que el productor ingresa los datos del encargado
    When proporciona un correo con formato incorrecto
    Then el sistema solicita ingresar un correo válido

  Scenario: Alternativo - consultar invitaciones
    Given que el productor ha enviado invitaciones
    When accede a la gestión de usuarios
    Then el sistema muestra las invitaciones registradas
```

## US48 – Roles y permisos

```gherkin
Feature: US48 - Roles y permisos

  Como productor ganadero,
  quiero definir qué puede hacer cada usuario de mi granja
  para proteger la información y evitar cambios no autorizados.

  Scenario: Happy path - asignar permisos
    Given que el productor tiene usuarios registrados en su granja
    When selecciona un usuario y configura sus permisos
    And guarda los cambios
    Then el sistema actualiza los permisos del usuario

  Scenario: Unhappy path - usuario inexistente
    Given que el productor intenta modificar los permisos de un usuario
    When el usuario seleccionado no está registrado
    Then el sistema informa que no se encontró el usuario

  Scenario: Unhappy path - acción no autorizada
    Given que un usuario tiene permisos limitados
    When intenta realizar una acción que no tiene autorizada
    Then el sistema impide la operación
    And informa que no cuenta con los permisos necesarios

  Scenario: Alternativo - modificar permisos existentes
    Given que un usuario tiene permisos asignados
    When el productor modifica sus permisos
    And guarda los cambios
    Then el sistema actualiza las autorizaciones correspondientes
```

## US49 – Mi cuenta y plan

```gherkin
Feature: US49 - Mi cuenta y plan

  Como usuario,
  quiero ver y modificar mis datos personales y consultar mi plan actual
  para administrar mi cuenta de MiGranja.

  Scenario: Happy path - actualizar datos personales
    Given que el usuario accede a la sección "Mi cuenta"
    When modifica sus datos personales
    And guarda los cambios
    Then el sistema actualiza su información

  Scenario: Alternativo - consultar plan actual
    Given que el usuario accede a la sección "Mi cuenta"
    When consulta la información de su suscripción
    Then el sistema muestra su plan actual

  Scenario: Alternativo - cambiar de plan
    Given que el usuario desea modificar su suscripción
    When selecciona otro plan disponible
    Then el sistema procesa la solicitud de cambio de plan

  Scenario: Unhappy path - datos inválidos
    Given que el usuario modifica sus datos personales
    When ingresa información con formato incorrecto
    And intenta guardar
    Then el sistema solicita corregir los datos
```

## US50 – Cerrar sesión

```gherkin
Feature: US50 - Cerrar sesión

  Como usuario,
  quiero cerrar sesión de manera segura
  para proteger la información de mi granja.

  Scenario: Happy path - cerrar sesión
    Given que el usuario tiene una sesión activa
    When presiona el botón "Cerrar sesión"
    And confirma la operación
    Then el sistema cierra la sesión
    And muestra la pantalla de inicio de sesión

  Scenario: Alternativo - cierre por inactividad
    Given que el usuario mantiene una sesión activa
    When permanece inactivo durante el tiempo establecido
    Then el sistema solicita iniciar sesión nuevamente

  Scenario: Unhappy path - cancelar cierre de sesión
    Given que el usuario seleccionó cerrar sesión
    When cancela la operación
    Then el sistema mantiene la sesión activa
```
