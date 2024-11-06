Scenario 1: Pseudo-Code for Authentication System 
    FUNCTION authenticateUser(username, password):
        QUERY database WITH username AND password
        IF found RETURN True
        ELSE RETURN False

El codigo es vulnerable 
-Ya que puede sufrir un ataque de inyeccion de codigo sql
-Los datos como el usuario y password no están encryptados
-La consulta se hace de forma directa a la base de datos

Como medida de seguridad:
-Se puede utilizar un procedimiento almacenado para la implementación de validación en base de datos para el usuario y password 
-Encriptar los datos de usuario y contraseña antes de almacenarlos en la base de datos utilizando un metodo salt.
-Ademas se puede implementar un sistema de autenticación de dos factores para mejorar la seguridad del sistema.
-Escaneao cde tipo SAST para la validación de vulnerabilidades en el código.

-------------------------------------------------------------------------------------------------------

Scenario 2: JWT Authentication Schema
    DEFINE FUNCTION generateJWT(userCredentials):
    IF validateCredentials(userCredentials):
        SET tokenExpiration = currentTime + 3600 // Token expires in one hour
        RETURN encrypt(userCredentials + tokenExpiration, secretKey)
    ELSE:
        RETURN error


El codigo es vulnerable:
   
    El JWT generado no se ve que cumpla con los 3 estandares de la estructura de uso, como son le header, el payload, y la firma.
    El objeto userCredential esta concatenado con el token expiration, lo cual genera un riesgo de que los datos del usuario pueden ser visibles despues de que se decifre el JWT.
    

Como medida de seguridad:
    Implementar en la generación del JWT lo siguiente
        Header: Definir tipo de algoritmo HS256 de typo JWT 
        Payload: No agregar datos sensibles relacionados con el usuario 
        Firma: Utilizar una firma HS256 con los datos del pyalod, header y el tiempo de expiración


-------------------------------------------------------------------------------------------------------


Scenario 3: Secure Data Communication Plan

PLAN secureDataCommunication:
  IMPLEMENT SSL/TLS for all data in transit
  USE encrypted storage solutions for data at rest
  ENSURE all data exchanges comply with HTTPS protocols

Implementacioón del plan:

    En la configuración de la infraestructura implementar un un SSL/TLS por medio de alguna herramienta( EJ: OPENSSL) para la implementación de certificados SSL lo cual permite una comunicacion segura entre el servidor y el cliente por ejemplo en las API's.

    De lo comentado en el curso, también se puede implementar una estrategia de coss origin que permite la comunicación solo de los servers autorizados. 

    Para el envio de datos la recomendación es utilizar un metodo de cifrado  con el uso de algoritmos que permitan tener una comunicación segura con una clave, donde solo los dos extremos conozcan para poder decifrar el contenido original, por ejemplo utilizar algún hash para la mensajeria.

