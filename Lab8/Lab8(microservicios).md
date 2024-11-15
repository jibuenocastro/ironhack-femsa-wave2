# API Specifications Document:

- Se comparte en el el archivo yaml la descripcion de las apis

# Reflection Report:

Uno de los desafios creo que fue el tema de seguridad, no se como se puede implementar la seguridad en la api en el swagger sin embargo, para las API's con las que he trabajado en la que se transaccionan con datos criticos, siempre hay un metodo de autenticación ya sea por x-api-key, por un Autorization con un JWT o me ha tocado trabajar con ambas. 

Otro es que no da mucho detalle la tarea como para implementar un diseño mas completo, consideré dos apis principales que son las de usuarios y las de ordenes. En estos casos documente dos endpoints del api de users uno para darlo de alta (POST) y otro con el metodo GET para recuperar los datos del usuario, tomando en consideración solo recuperar los datos necesarios, para este definí unos codigos de respuestas de acuerdo a lo platicado en el curso, 200, 201, 400,403, 404, 500

Para la documentacion de ordenes, definí 3 endpoints los primeros dos son de tipo GET, que recupera la orden por ID, y un endpoint que recupera todas las ordenes, la idea es paginarlo como se sugiere, si es que este dato crece demasiado, tambien el metodo POST para la creación de la orden.

Para la definicion del basepath se contenplo a como se sugiere, v1/{entidad}


Como dato adicional se que lo ideal es implementar los verbos que sean necesarios por entidad de acuerdo a la necesidad:

- POST
- GET
- PATCH
- DELETE
- PUT 