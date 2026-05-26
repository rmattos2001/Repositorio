## Creacion Agente de Ventas

### Introduccion
**Interlocutor**: Director General de NovaBank

**Asunto**: Solicitud de implementación

**Fase 1 - "Cimientos y Seguridad"**


Hola equipo, bienvenidos a NovaBank.
Les cuento nuestra situación: Somos una financiera joven dedicada a otorgar préstamos personales y microcréditos a emprendedores. Hasta hoy, hemos manejado todo (y cuando digo todo, es todo) en hojas de cálculo de Excel compartidas por correo. Esto se ha vuelto insostenible. Tenemos duplicidad de datos, asesores que borran filas por error y, lo más grave, miedo a que nuestra base de datos de clientes se filtre porque cualquiera tiene acceso a todo.

### Alcance / Objetivos

Hemos contratado su consultora para que nos migren a Salesforce. Necesitamos profesionalizarnos. Para esta primera etapa (sus próximas 4 semanas), necesito que resuelvan lo siguiente:
1. Nuestra Identidad y Espacio de Trabajo
    No quiero entrar a Salesforce y ver cosas de "ventas" genéricas que no entiendo.
    Necesito una Aplicación propia dentro del sistema que se llame "NovaBank Core".
    Quiero que pongan nuestro logotipo y que los colores reflejen nuestra marca (azul oscuro y blanco).
    Es fundamental que configuren el Dominio de mi empresa (novabank-dev-ed o similar) para que mis empleados sepan que están en el sitio correcto al loguearse.
2. El Corazón del Negocio (Los Datos)
    Necesito dejar de usar Excel. En el sistema, necesito poder registrar y ver claramente la siguiente información. Ustedes son los expertos, díganme cómo estructurarlo, pero esto es lo que necesito ver:
   - **Los Clientes**: Necesito una ficha para guardar a las personas (Nombre, DNI, Email, Teléfono, Salario Mensual).
   - **Los Productos Financieros**: Ofrecemos distintos tipos de préstamos (ej. "Préstamo Personal", "Préstamo Emprendedor", "Hipotecario"). Necesito un lugar donde estén listados estos productos con sus características (Tasa de interés, Monto máximo permitido).
   - **Las Solicitudes de Crédito**: Esto es lo más importante. Un Cliente debe poder tener varias Solicitudes de Crédito a lo largo del tiempo (una relación de uno a muchos, ¿verdad?).
   En la solicitud necesito saber: 
   ¿Qué cliente es? 
   ¿Qué producto financiero está pidiendo? 
   ¿Cuál es el monto solicitado? 
   ¿Cuál es el estado de la solicitud (Borrador, En revisión, Aprobado, Rechazado)?
   Seguro de Desempleo: A veces vendemos un seguro opcional asociado a la solicitud. Necesito que esa información esté vinculada a la solicitud.

3. Calidad y Reglas de Negocio (¡Basta de errores!)
    En los Excels actuales mis empleados escriben cualquier cosa. Necesito que el sistema sea estricto:
   - **Montos reales**: Nadie puede ingresar una solicitud de crédito con un monto negativo o cero. Eso no existe.
   - **Validación de Identidad**: El campo de DNI/Identificación del cliente es sagrado. Debe tener un formato específico (numérico) y no puede quedar vacío.
   - **Fechas coherentes**: La "Fecha de cierre estimada" de una solicitud no puede ser una fecha en el pasado.
  
4. Seguridad y Accesos (Esto es CRÍTICO)
Este es mi mayor dolor de cabeza. Tengo dos tipos de empleados y no pueden ver lo mismo. Necesito que configuren los usuarios y permisos para estos dos roles:
- A. El Asesor Comercial (Ejecutivo de Cuentas)
    Son los que venden.
    **Permiso**: Solo deben poder ver y editar los Clientes y Solicitudes que ellos mismos crearon. No quiero que un vendedor le robe la cartera de clientes a otro. (Modelo de seguridad Privado).
    **Restricción**: No pueden borrar nada. Si se equivocan, tienen que pedir permiso.
- B. El Analista de Riesgos (Supervisor)
    Son los que aprueban los créditos.
    **Permiso**: Ellos necesitan ver TODAS las solicitudes y todos los clientes de la empresa, sin importar quién sea el dueño del registro.
    **Poder**: Ellos sí pueden borrar registros si es necesario (aunque preferimos que no lo hagan).
- C. Auditoría
    Necesito que ciertos campos sensibles (como el "Salario Mensual" del cliente) estén ocultos para todos, excepto para los Analistas de Riesgos y el Administrador del sistema. Los vendedores no tienen por qué ver cuánto gana el cliente, solo necesitan saber si aplica o no.

**Entregable Fecha**
    Para fin de mes, quiero ver mi sistema NovaBank funcionando. Quiero poder entrar, crear un cliente, crearle una solicitud, intentar poner un monto negativo y que el sistema me frene, y loguearme como un "Vendedor" para verificar que no veo los datos de mi compañero 


### Modelo de Datos

[Modelo de Datos 1](../Imagenes/Modelo_BBDD_1.png)

[Modelo de Datos 2](../Imagenes/Modelo_BBDD_2.png)

**Para**: Equipo de Implementación 1
**Asunto**: APROBADO - Luz verde para construcción de Fase 1
Estimado equipo,
¡Excelente trabajo de ajuste!

✅ El Dinero apareció: Veo claramente que han agregado el campo "Monto Solicitado" en la tabla de Solicitudes. Fundamental. Ahora sé exactamente cuánto dinero pide el cliente, independientemente del tope máximo del producto.

✅ Estructura Limpia: Mantuvieron la decisión correcta de usar Contactos (Clientes reales) y de integrar el Seguro dentro de la solicitud para agilizar la carga.

✅ Historial de Tasas: Veo que mantuvieron la "Tasa Interés" en la Solicitud. Reitero que esto es vital para "congelar" la tasa pactada con el cliente en el momento de la venta, aunque la tasa del producto cambie en el futuro.

**VEREDICTO: MODELO APROBADO 🟢**

No tengo más correcciones de estructura. El plano de los cimientos está listo. Por favor, procedan de inmediato a crear los Objetos, Campos y Relaciones en el entorno de Salesforce.
¡Quiero ver esto funcionando en la próxima demo!
Saludos,
Alejandro Vance CEO, NovaBank

### Roles y Requerimientos de los Sprint
    **SPRINT 1 - Colocar nombre y apellido**

    Product Owner: Robert Mattos.
    Business Analyst: Angel / Nicole
    Salesforce consultant:
    Tester QA: Lady / Robert
    DevOps Specialist:  Andrea / Nicole / Angel

[Link a Trello Sprint 1 :](https://trello.com/b/vlgFLyFQ/equipo-1)


    **SPRINT 2 - Colocar nombre y apellido**

    Business Analyst    : Angel,Robert Mattos
    Product Owner       : 
    Salesforce admin    : Andrea, Nicole, Karla, Stefanny
					      Backup : Robert Mattos
    Tester QA           : Lady, Stefanny, Elvis
    
[Link a Trello Sprint 2 :](https://trello.com/b/ezlsnOk3/oneforce-sprint2)

#### Requerimientos
**De**: Alejandro Vance (CEO)

**Para**: Equipos de Implementación (1 y 4) 

**Asunto**: Sprint 2 - Masividad, Inteligencia y Automatización

Estimados equipos,
El sistema base funciona, podemos guardar datos. Bien. Pero mi negocio no es "guardar datos", mi negocio es procesar créditos rápido y con inteligencia.
Para este segundo ciclo de trabajo, necesito que transformen este "repositorio de datos" en una verdadera máquina de operaciones. Tengo 3 dolores de cabeza principales que necesito que resuelvan:

1. La Migración Masiva (¡No voy a cargar a mano!)
El equipo de Marketing acaba de comprar una base de datos de posibles clientes interesados en préstamos. Son 1,000 registros.
Mis asesores se niegan a cargarlos uno por uno, y tienen razón; tardarían semanas.

    **Requerimiento**: Necesito que tomen este archivo masivo y lo inyecten en el sistema de una sola vez. Quiero entrar el lunes y ver esos 1,000 contactos listos para ser llamados.

    **Ojo**: Tengan cuidado con la calidad. No quiero duplicados si alguno ya existe.

2. El Tablero de Control (Estoy volando a ciegas)
    Hoy, para saber cómo vamos, tengo que entrar a cada solicitud y sumar con calculadora. Eso es inaceptable para un CEO. Necesito entrar a NovaBank y ver un Panel de Control (Panel de control Inicio o una sección específica) 

    1-Quieren que cada usuario vea específicamente ciertos paneles en Inicio o separamos en secciones o ambos? (resumen visibilidad y seguridad)

    (Dashboard) con gráficos claros que me respondan estas preguntas de negocio en tiempo real:
    **Volumen de Dinero**: ¿Cuánto dinero total tenemos "En Revisión" hoy? (Para saber cuánto cash necesito tener listo).

    **Ranking de Productos**: ¿Cuál es el producto más vendido? (¿El Personal o el Prendario?).

    **Desempeño del Equipo**: ¿Quién es el vendedor que más solicitudes ha cerrado este mes?

    **Tasa de Rechazo**: ¿Qué porcentaje de solicitudes estamos rechazando? (Si es muy alto, algo anda mal).

    **Clientes VIP**: Un listado simple de los clientes que han pedido más de $50,000. (Dolares)

    **El "Cuello de Botella"**: ¿Cuántas solicitudes hay estancadas en cada Estado (Borrador, Revisión, Aprobado)?

    **Quiero ver gráficos de barras, tortas y números grandes. Nada de tablas aburridas de Excel**.

3. Automatización (Quiero que el sistema trabaje por mí)
    Para evitar errores humanos y lentitud. Necesito que automaticen los siguientes procesos:

    A. El "Asistente Rápido" para Ventas Telefónicas Cuando llaman por teléfono, el vendedor tiene que ser veloz. No puede estar navegando por menús complicados.
    **Necesidad**: Quiero un botón o una pantalla simple estilo "Paso a paso" (un Wizard) que guíe al vendedor:
    Primero que le pida el DNI y Nombre. 
    **Siguiente paso**: Que elija el producto y el monto. (crear solicitud)
    **Finalizar**: Y que el sistema guarde todo automáticamente.(Mensaje de exito!)
    y donde va el botón? en qué página? 

    B. Alerta de "Pez Gordo" No quiero enterarme tarde cuando entra un negocio grande.
    **Necesidad**: Si ingresa una Solicitud de Crédito por un monto superior a $100,000, quiero que el sistema automáticamente:
    Marque esa solicitud como "Prioridad Alta" (o similar).
    Me mande un correo electrónico a mí (CEO) avisándome para que yo mismo la supervise.

    C. Limpieza Nocturna Automática Los vendedores dejan muchas solicitudes "Borrador" tiradas que nunca avanzan y ensucian mis reportes.
    **Necesidad**: Quiero un proceso automático que corra todas las noches. Si el sistema encuentra una solicitud en estado "Borrador" que no se ha modificado en los últimos 30 días, quiero que automáticamente la cambie a estado "Cerrada/Perdida" o "Descartada".

    Espero ver estas mejoras implementadas para la próxima demo.
    Saludos,
    Alejandro Vance CEO, NovaBank


#### Entornos de Desarrollo 

[Ambiente Developer: ](https://novabank-dev-ed.trailblaze.lightning.force.com/lightning/o/Contact/pipelineInspection?filterName=00Baj00000vM8vlEAC)

[Ambiente Testing QA: ](https://curious-badger-mfejk6-dev-ed.trailblaze.lightning.force.com/lightning/n/trlhdtips__Welcome)

[Ambiente Produccion: ](https://resilient-narwhal-gy4khe-dev-ed.trailblaze.my.salesforce-setup.com/lightning/setup/SetupOneHome/home)

[Portal Web Salesforce ](https://novabank-pro-dev-ed.trailblaze.my.site.com/novabankclient/s/)

[Imagen del Portal Web Novabank](../Imagenes/Web%20Novabank.PNG)

[App Plataforma Salesforce ](https://novabank-pro-dev-ed.trailblaze.lightning.force.com/lightning/page/home)

[Imagen del App Novabank](../Imagenes/App%20Novabank.PNG)




    **SPRINT 3 - Colocar nombre y apellido**

    Sprint 3 - Nombres
    Salesforce Consultant/ BA/PO    : Robert Mattos
    Salesforce QA                   : Lady Espinoza, Elvis Huamani
    Salesforce DevOps               : Karla , Robert 

[Link a Trello Sprint 3 :](https://trello.com/b/DUovMimX/oneforce-spring3)
    

#### Requerimientos

**DE**: Alejandro Vance, CEO

**PARA**: Equipo de Desarrollo e Implementación ASUNTO: Lanzamiento de la Sucursal Virtual (Portal de Clientes)


Estimado equipo,
Los tableros de control del mes pasado quedaron fantásticos. El equipo interno ya trabaja de forma eficiente. Sin embargo, tengo un nuevo problema: nuestros teléfonos no paran de sonar.

Los clientes llaman para preguntar cosas básicas como "¿En qué estado está mi préstamo?" o "¿Cómo evito caer en una estafa?". Esto satura a mis asesores y les quita tiempo para vender.

Para este Sprint 3, el objetivo es dejar de ser un banco tradicional y convertirnos en una plataforma digital de autoservicio. Necesito que construyan nuestro Portal Web para Clientes.

Estos son los 4 pilares que deben entregar:
1. La Identidad de la **"Sucursal Virtual"**
    No quiero que los clientes sientan que están entrando a un sistema genérico de bases de datos.

    Requerimiento: Quiero una página web real. Debe tener el logotipo de NovaBank, nuestros colores corporativos (Azul y Celeste) y verse profesional y confiable. El cliente debe sentir que entró a la sucursal del banco desde su computadora o celular.
2. Biblioteca de Prevención y Ayuda **(Autoservicio)**
    Quiero reducir las llamadas al centro de atención al cliente en un 40%.
    Requerimiento: Necesito una sección en el portal que funcione como un "Centro de Ayuda" o biblioteca de artículos.
    Tienen que redactar y publicar al menos 3 artículos que los clientes puedan buscar y leer por su cuenta. Ejemplos que quiero ver:

    "Guía de Prevención de Fraudes y Phishing".

    "¿Qué hacer si no puedo pagar mi cuota este mes?".

    "Requisitos para solicitar un crédito hipotecario".

3. **Atención de Emergencia en Tiempo Real**
    Si el cliente leyó los artículos y sigue con un problema urgente (ej. le robaron la tarjeta o sospecha de un fraude), necesita hablar con un humano ¡ya!.
    Requerimiento: Instalen un botón de Chat en vivo en la esquina del portal. Cuando el cliente escriba por ahí, quiero que le suene una alerta a un asesor en nuestras oficinas para que le responda al instante por escrito.

4. Formularios Inteligentes **(El motor de ventas online)**
    El portal no solo es para clientes actuales; también debe atraer nuevos negocios desde internet. Necesito que construyan un sistema de captación en la página principal:
    **Requerimiento**: Quiero un formulario interactivo estilo "Paso a paso" llamado "Solicitá tu Préstamo Hoy".

    **La regla de Seguridad**: Este formulario debe ser público. Cualquier visitante anónimo de internet debe poder entrar, dejar sus datos de contacto y cuánto dinero necesita.
    
    **La magia**: Cuando el visitante presione "Enviar", el sistema debe crear su ficha en nuestra base de datos automáticamente. Pero atención con la seguridad: Ese visitante anónimo de internet NO debe poder ver la lista de nuestros otros clientes ni acceder a los datos internos del banco bajo ninguna circunstancia. Solo puede "depositar" su información.

    Equipo, este es el sprint que nos pone en las grandes ligas financieras. Es el que le da la cara de NovaBank al mundo.
    Confío en ustedes.
    Alejandro Vance CEO, NovaBank


