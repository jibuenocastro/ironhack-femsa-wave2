
# Esquema de Arquitectura de Microservicios:

Nota: Para poder responder a todas las preguntas del lab creo que es necesario que se haya presentado una arquitectura del monolito que se miragrará para saber la relación que existe entre los modulos y modelos actuales y poder definir la arquitectura de la nueva infraestructura basada en microservicios, tomando en consideración esto, mi definición sería la siguiente:

## Un diagrama de la arquitectura propuesta.

![ Alt Text](URL)

## Explicación de cómo interactúan los servicios y el flujo de comunicación entre ellos.

- Gestion de usuarios.- La idea es usar un formulario de registro similar al que debe de tener el monolito, donde se soliciten los datos del usuario, y asignarle un perfil. Adicional a eso se habilitan un endpoint para realizar la autenticación  del usuario esta autenticacion 
    generará un JWT con los datos del usuario para realizar la autorización del consumo de los demas servicios como el procesamiento de pedidos y la atencion del cliente, la idea es generar el JWT de acuerdo a lo platicado en el tema de seguridad, el tiempo de caducidad del token, etc. y sobre el password asignarle un salt a la contraseña por ejemplo.
    Para la gestión de los usuarios existentes de ser necesario restaurar las contraseñas y se puedan loguear con la nueva definición.
    

- En el modulo de catalogos de productos, se definieron unas apis para poder obtener los datos de los productos y los productos por categoria, el llamado CRUD, esto implica lo que se menciona en la definicion de la entidad como puede ser el inventario del producto, precio. La imagen creo que puede quedar bien, subir la imagen a un repositorio de imagenes en un servidor puede funcionar un S3 y obtener la ruta para la visualización de estos productos aunque si son muchos productos puede ser un poco costoso. 
    
- En el procesamiento de pedidos.- La idea es habilitar un servicio con los endpoints para agregar los productos al carrito, los pedidos, los pagos del usuario, para obtener las ordenes, etc.

- Atención al cliente: Agregar un microservicio para la gestión de la atención al cliente por ticket, la idea es crear un ticket por necesidad, se habilitará un endpoint tipo POST con la estructura para identificar la necesidad del usuario a reportar, ya sea una devulución, queja, sugerencia, etc.


# El flujo de comunicación de los microservicios: 

En primera instancia el autenticación y la autorización de los usuarios para poder realizar un pedido convive principalmente con todo el entorno de las transacciones del ecoommerce, (tomando en cuenta que para poder realizar un pedido se requiere estar autenticado). Con la API de login, se obtiene un Jwt el cual se va a validar en cada uno de los servicios en el backend en cada petición para la identificación del usuario. El usario en el frontend seleccionara los productos y se ejecutaran las apis dependiendo la necesitad, es decir, agregar un producto al carrito, procesar un pago, agregar alguna devolución, sugerencia o queja, filtrar los productos, visualizar sus pedidos, etc. El modulo de productos categorizados y el de procesamientos de pedidos conviven de forma activa, el modulo de atención a clientes es un modulo tambien que puede considerearse que convive y depende de las ordenes realizadas por el usuario, es decir depende del modulo de ordenes. 

Otro punto importante para la definicion de microservicios es generar un x-api-key para poder consumir todas las API's adicional a esto es contemplar la caché en algunas peticiones como por ejemplo el catalogo de productos, si el tema del inventario esta desacoplado. 


# Plan de Migración Detallado:
- Prioridades de migración de servicios.
como prioridades modulo de datos-Negocio-presentación 
- Estrategia para manejar dependencias de datos.
Considero que una migración por modulos puede ser mas optimo en un sentido de migración gradual, podría ser el modulo de catalogos, valorar que datos son los que tocan esa entidad, e ir valorando los datos que se van a ir migrando a la nueva arquitectura, ir desacoplando los modulos menos criticos, como el de la gestión de atención a clientes y finalmente ir desacoplando por funcionalidad las partes mas criticas. otro punto a considerar es el tema de devops y las pruebas unitarias que se desarrolllen para los nuevos microservicios esto ayudara a lo que se vaya migrando no sufra alguna afectación y tener que retrabajar o tener deudas tecnicas que sean mas complicados de mantener a largo plazo.

En la parte del front se puede ir diseñando las UI mientras se desarrollan los microservicios despues de que se tenga la definición proporcionar una documentación sobre las API's que se habilitarán con los posibles codigos de error mapeados dependiendo las reglas de negocio que ya existan en el monolito y las nuevas que se definan en la migración.

- Descripción del proceso de migración de la base de datos monolítica a un entorno de microservicios.
        
Esta parte depende sobre la definición, es probable que mucho de lo que esta en cuando a las reglas de negocio del monolito en base de datos se pueda reutilizar, todo depende que tan bien se haya definido el esquema de base de datos, si es un tipo refactory a la infraestructura de base de datos, es lo primero que se tendría que realizar para luego realizar los diseños de los microservicios.
        
# Informe de Reflexión:

## Discusión sobre los desafíos enfrentados en el diseño y las decisiones de migración.

Una parte importante sobre la migración creo que es evaluar si el modelado de base de datos, lo que ya está digamos en producción nos sirve para la migración a microservicios o tegamos que hacer una nueva definición  de esquemas de base de datos desde cero. El principal desafio de la migración considero que es por los datos que ya existen, que deben de convivir con la nueva arquitectura. Creo que puede ser complejo dependiendo que tan robusto sea el aplicativo y los cambios que se vayan metiendo a la aplicación mientras se hace esa migración.
