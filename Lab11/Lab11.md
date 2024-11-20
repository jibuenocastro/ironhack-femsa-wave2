

# Part 1: Designing Cloud Infrastructure

Crear una instancia EC2 nos permite tener la escalabilidad en automatico bajo demanda un VCP nos permitira crear un diseño de conexión hacia la instacía que se crea para la aplicación web, definir las zonas de diponibilidad, y los rangos de IP's de accesos y un S3 que permita el almacenamiento de archivos que necesite la aplicación.

# Part 2: IAM Configuration

- Con el IM se se permite confirgurar el acceso a la aplicación para eso es necesario definir los roles de usuario que interactuan con la aplicación, como el equipo de desarrollo, el admin y las aplicaciones.

- Crear un grupo de desarrollo, administrador que no sea root (a como tengo entendido no es recomendable usar el usuario root) pero que tenga los permisos para acceder al menu de admin. 

- Implementar en las politicas solo los permisos especificos que el rol requiere. 

- Como medida de seguridad se puede implementar el MFA para la autenticación de los usuarios

# Part 3: Resource Management Strategy

Implementar un conjunto de instancias para balancear la carga en la aplicación por medio de un ELB y no saturar ninguna instancia EC2, esto permite un unico punto de acceso para la aplicación, además de tener alta disponibilidad entre AZ. Para poder administrar los costos utilizar la implementación de un AWS Budgets, con una alerta con algun porcentaje definido del prosupuesto, e ir deteminando si es necesario utilizar mas recursos o hacer algun ajuste en la configuración.

# Part 4: Theoretical Implementation

![ Alt Text](https://github.com/jibuenocastro/ironhack-femsa-wave2/blob/main/Lab11/DiagramaAWS-Lab11.png)


# Part 5: Discussion and Evaluation

En el ejemplo del diagrama, la intención era usar algunos elementos que se vieron en el curso, la idea es que haya instancias de EC2 y eque estas instancias hagan la comuninicacion con la base de datos de DinamoDB, a su vez la implementacion de un event bridge cuando se crea un archivo en un S3 y este a su vez genere un registro en DinamoDB, se implemto un load balancer para distibuir la carga y una VPC que permite conectarse desde una red publica. La implementación de los usuarios IAM de debe implementar por roles, estos dependiendo la necesidad se dan el minimo acceso para realizar la actividad que se requieran, supongamos para los devs asignar todos los permisos sobre los buckets en ambiente de desarrollo, permisos de lectura solo para QA y para prod en los S3. 
