# Monte - Prueba Técnica (Sección 2)

Este repositorio corresponde a la sección 2 de la prueba técnica de Monte.  
Aquí se documenta cómo preparar el entorno, los requerimientos previos y la configuración de un Job en Jenkins para despliegues automatizados.

## Requerimientos previos

El servidor que se usará para los despliegues debe tener instalado lo siguiente:

- [Docker](https://docs.docker.com/get-docker/)
- [Kubernetes](https://kubernetes.io/docs/setup/)
- [Git](https://git-scm.com/)
- [Jenkins](https://www.jenkins.io/)
- [Python](https://www.python.org/)
- [pip](https://pip.pypa.io/)
- [pytest (opcional)](https://docs.pytest.org/)
- [AWS CLI](https://docs.aws.amazon.com/cli/)

⚠️ **Nota importante:**  
Todo software que requiera autenticación (ejemplo: Jenkins, DockerHub, AWS) debe configurarse previamente en el entorno local y/o en sus respectivas páginas web antes de ejecutar el pipeline.

## Configuración de Jenkins

### 1. Crear credenciales
1. En Jenkins, ir a:  
   Administrar Jenkins > Credentials > Global
2. Hacer clic en Add Credentials.
3. Ingresar el usuario y contraseña de DockerHub.  
   - **ID**: dockercreds  
   - **Descripción**: opcional

### 2. Crear un nuevo Job
1. Crear un nuevo Elemento en la ubicación deseada.  
2. Asignarle el nombre que prefiera.  
3. Marcar la casilla Esta ejecución debe parametrizarse.  
4. Agregar parámetros de cadena:
   - **url** → https://github.com/RMC-15/monte.git
   - **rama** → main

### 3. Configurar el Pipeline
Tienes dos opciones:

#### Opción A: Usar Pipeline Script
1. Selecciona Pipeline script.  
2. Copia el contenido del Jenkinsfile del repositorio.

#### Opción B: Usar SCM
1. Selecciona Pipeline script from SCM.  
2. En SCM, elige Git.  
3. En Repository URL, coloca:  
https://github.com/RMC-15/monte.git
4. En Branch Specifier, coloca:  
main

### 4. Ejecutar
1. Guarda la configuración.  
2. Haz clic en Build Now para ejecutar el pipeline.  