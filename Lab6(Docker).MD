# LAB6

## 1.- Review Simulated CI/CD Pipeline Configuration:
#### Build Stage:

### Code Commit: 
- Ayuda a la integración de codigo de forma rápida y eficiente, además de mantener un historial de cambios.

### Test Stage:

Permite tener pruebas automatizadas para garantizar la funcionalidad de la aplicación y si hay algun impacto en alguna parte del flujo del codigo 

### Deployment Stage:

Para la parte del desarrollo se puede utilizar herramientas como kubernetes para la administración de imagenes para los ambientes de desarrollo, pruebas y producción.


Un ejemplo de un archivo de configuración en yaml para la implementación de un CD/CI seria de la siguiente manera:

```bash

  # Archivo .gitlab-ci.yml

  # Definimos las etapas del pipeline
  stages:
    - build
    - test
    - push
    - deploy

  # Variables globales
  variables:
    DOCKER_IMAGE:  <Ruta del registro de Docker>
    DOCKER_TAG: < Usar el hash del commit como tag de la imagen>

  # Etapa de construcción
  build:
    stage: build
    image: docker:latest
    services:
      - docker:dind
    script:
      - docker build -t $DOCKER_IMAGE:$DOCKER_TAG .
    only:
      - main  # Ejecutar solo en la rama principal

  # Etapa de pruebas
  test:
    stage: test
    image: $DOCKER_IMAGE:$DOCKER_TAG
    script:
      - npm install
      - npm test  # Asume que hay un script 'test' en package.json para correr las pruebas
    only:
      - main

  # Etapa de publicación (push al registro de Docker)
  push:
    stage: push
    image: docker:latest
    services:
      - docker:dind
    script:
      - docker login -u $DOCKER_USER -p $DOCKER_PASSWORD registry.gitlab.com
      - docker push $DOCKER_IMAGE:$DOCKER_TAG
    only:
      - main
    dependencies:
      - build  # Asegura que la imagen construida en 'build' esté disponible

  # Etapa de despliegue (simulación de despliegue en Kubernetes)
  deploy:
    stage: deploy
    image: bitnami/kubectl:latest
    script:
      - kubectl config set-cluster k8s-cluster --server=$K8S_SERVER
      - kubectl set image deployment/node-api node-api=$DOCKER_IMAGE:$DOCKER_TAG  # Actualizar la imagen en el despliegue
    only:
      - main
    environment:
      name: production
    dependencies:
      - push  

```

## 2. Analyze Enhancements and Potential Issues:


  El uso de Docker en el proyecto puede ser una ventaja ya que mejora los flujos de trabajo de desarrollo y 
  la facilitación de prácticas de contenedorización consistentes, escalables y eficientes.

  Hay algunas consideraciones mejorar el rendimiento de la implementacion de docker en el proyecto:

- Etiquetar versiones de imágenes de Docker
- Las credenciales deben de estar fuera de los entornos de CI/CD
- Limpieza de imágenes activas 
- Limitar la distribucion de capas de imagenes


  Docker también puede presentar desafíos, como el tema de seguridad, ya que si no se tiene un control de acceso a los contenedores, se puede tener un acceso no autorizado a la información de la aplicación, por eso es necesario realizar una definicion y configuración de acceso de usuarios es decir hacer una delimitación de accesos y no usar el usuario root.


## 3. Write an Analysis Report:

De acuerdo a lo platicado en el curso, el uso de Docker en un proyecto de desarrollo de software puede ser una ventaja, ya que permite la ejecución de aplicaciones en cualquier entorno, facilita la administración de aplicaciones,  la creación de imágenes de Docker es un proceso automatizado, y permite la portabilidad y la escalabilidad.

La implementación de un archivo docker compose en el proyecto puede ser otra ventaja también ya que permite la definición de servicios que ya crean un entorno de desarrollo completo, y se pueden definir los servicios que se necesitan para la aplicación lo cual simplifica el proceso de deploy de contenedores.

Sin embargo, el uso de Docker también puede presentar desafíos, como la seguridad de los contenedores, la creación de imágenes de Docker puede ser un proceso lento y costoso, dependiendo de la  complejidad de la aplicación ademas, pueden contener vulnerabilidades de seguridad, 
especialmente si incluyen versiones obsoletas de librerias.



