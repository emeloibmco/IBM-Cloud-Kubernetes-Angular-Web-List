# IBM Cloud ☁ - Despliegue de aplicación Angular-Web-List en Kubernetes <img width="30" src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/kubernetes.png">

## Índice  📰
1. [Pre-Requisitos](#Pre-Requisitos-pencil)
2. [Crear clúster Kubernetes](#Crear-clúster-Kubernetes-cloud)
3. [Instalar herramientas y comandos necesarios](#Instalar-herramientas-y-comandos-necesarios-gear)
    * [Instalación de git](#Instalación-de-git)
    * [Instalación de Docker](#Instalación-de-Docker)
    * [Instalación de IBM Cloud CLI y plug-ins](#Instalación-de-IBM-Cloud-CLI-y-plug-ins)
       * [Instalación de IBM Cloud CLI](#Instalación-de-IBM-Cloud-CLI)
       * [Instalación de plug-in kubectl](#Instalación-de-plug-in-kubectl)
       * [Instalación de plug-in IBM Cloud Container Registry](#Instalación-de-plug-in-IBM-Cloud-Container-Registry)
4. [Clonar repositorio](#Clonar-repositorio-round_pushpin)
5. [Crear imagen docker local de la aplicación](#Crear-imagen-docker-local-de-la-aplicación-computer)
6. [Subir imagen de la aplicación a IBM Cloud Container Registry](#Subir-imagen-de-la-aplicación-a-IBM-Cloud-Container-Registry-outbox_tray)
7. [Desplegar imagen de la aplicación en Kubernetes](#Desplegar-imagen-de-la-aplicación-en-Kubernetes-rocket)
8. [Verificar el funcionamiento de la aplicación](#Verificar-el-funcionamiento-de-la-aplicación-heavy_check_mark)
9. [Referencias](#Referencias-mag)
10. [Autores](#Autores-black_nib)
<br />

## Pre-Requisitos :pencil:
* Tener una cuenta en <a href="https://cloud.ibm.com/"> IBM Cloud</a> <img width="25" src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/ibm-cloud-logo.png">.
<br />

## Crear clúster Kubernetes :cloud:
Para crear un clúster de Kubernetes y desplegar la aplicación propuesta en el presente repositorio, complete los siguientes pasos:
<br />

1. Inicie sesión con su usuario y contraseña en el portal de <a href="https://cloud.ibm.com/"> IBM Cloud</a>.

2. Una vez se encuentre en el dashboard del portal, de click en el menú de navegación o hamburguesa que se encuentra en la parte superior izquierda (lo puede identificar mediante 4 líneas blancas) y allí seleccione la pestaña ```Kubernetes```.

3. Espere unos segundos mientras carga la ventana y luego de click en el botón ```Create cluster +/Crear cluster +```.

4. Complete los detalles del plan de la siguiente manera:

   * ```Princing plan/Plan de precios```: seleccione la opción **Free**.
   * ```Cluster name/Nombre del clúster```: indique un nombre exclusivo para su clúster.
   * ```Resource group/Grupo de recursos```: seleccione el grupo de recursos **Default** que aparece por defecto.

5. Para finalizar la creación de su clúster de click en el botón ```Create/Crear```. Cuando el clúster tengo como estado ```normal```, podrá utilizarlo.

   <p align="center"><img src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/CrearCluster.gif"></p>

   <br />

> NOTA: Después de dar click en el botón crear, el proceso de despliegue del clúster puede tomar entre 20 y 30 minutos. Por lo tanto, se recomiendo continuar con la siguiente sección sobre como [Instalar herramientas y comandos necesarios](#Instalar-herramientas-y-comandos-necesarios-gear), mientras se completa la creación del clúster.

<br />

## Instalar herramientas y comandos necesarios :gear:
Para desplegar la aplicación propuesta en un clúster de Kubernetes en IBM Cloud, deberá contar con una serie de comandos y herramientas que le permitirán completar el proceso con éxito. A continuación, se indican los pasos para realizar la instalación en Windows. En caso de que trabaje con un sistema operativo diferente, se indican los enlaces para que revise el proceso.
<br />

## Instalación de git
Teniendo en cuenta que debe clonar el presente repositorio para usar la aplicación, es necesario contar con el comando git. Complete los siguientes pasos para realizar realizar la instalación:
<br />

1. Verifique si tiene instalado el comando. Para ello, abra una ventana de ```Windows PowerShell``` y allí coloque:

   ```PowerShell
   git --version   
   ```
   
   Si obtiene como respuesta la versión de git, puede pasar a la siguiente sección sobre la [Instalación de Docker](#Instalación-de-Docker). De lo contrario, continúe con el paso 2.

2. Para instalar git en su computador, vaya a la página de <a href="https://git-scm.com/book/es/v2/Inicio---Sobre-el-Control-de-Versiones-Instalaci%C3%B3n-de-Git"> Instalación de Git</a>. Identifique el sistema operativo en el que desea realizar la instalación y complete el proceso indicado. Para el caso de Windows, de click sobre el enlace <a href="http://git-scm.com/download/win"> http://git-scm.com/download/win</a>, y allí seleccione la opción ```Click here to download manually```. 

3. Espere mientras se completa la descarga y posteriormente, de click en el instalador. Complete la instalación, dejando todos los campos como aparecen por defecto y al final de click en el botón ```Install```.

4. Para verificar que la instalación de git se ha completado con éxito, en una ventana de ```Windows PowerShell``` coloque:

   ```PowerShell
   git --version   
   ```
   
   Como respuesta debe obtener la versión de git.
   
   <p align="center"><img src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/Instalar%20Git.gif"></p>

   <br />

## Instalación de Docker
Para crear la imágen docker local de la aplicación y probarla, es necesario que instale *Docker Desktop*. Para ello, complete los siguientes pasos:
<br />

1. Vaya a la página <a href="https://docs.docker.com/desktop/"> Docker Desktop overview</a> y seleccione las pestaña segpun su sistema operativo. Para el caso de Windows, de click en la sección ```Install Docker Desktop on Windows``` y luego presione el botón ```Docker Desktop for Windows```.

2. Espere unos minutos mientras se completa la descarga, y luego de click sobre el instalador.

3. Habilite la 2 casillas que aparecen y de click en el botón ```Ok```. Espere unos minutos mientras se completa la instalación.

4. Una vez finalice la instalación, en la barra de búsqueda coloque ```Docker Desktop``` y abra la aplicación. Espere unos minutos mientras esta inicia.

5. Si no tiene una cuenta en <a href="https://hub.docker.com/"> DockerHub</a>, cree una y luego coloque las credenciales de inicio de sesión presionando ```Sign in``` en la parte superior derecha de la ventana de ```Docker Desktop```.

   <p align="center"><img src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/Instalar%20Docker.gif"></p>
  
   <br />
   
   > NOTA: En caso de presentar problema en Windows sobre *Enable Hyper-V Windows Features*, revise la guía <a href="https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v"> Enable Hyper-V using PowerShell</a>
  
6. Una vez complete la instalación, en un ventana de ```Windows PowerShell``` coloque:

   ```PowerShell
   docker --version   
   ```
   
   Como respuesta debe obtener la versión de docker.
   
   <p align="center"><img src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/Prueba%20Docker.gif"></p>

   <br />
   
## Instalación de IBM Cloud CLI y plug-ins
Para desplegar la aplicación en el clúster de Kubernetes en IBM Cloud, deberá instalar en su computador la CLI de IBM Cloud junto con algunos plug-ins. Para completar estas instalaciones realice lo siguiente:
<br />

### Instalación de IBM Cloud CLI
1. Vaya a la página <a href="https://cloud.ibm.com/docs/cli?topic=cli-install-ibmcloud-cli"> Installing the stand-alone IBM Cloud CLI</a> y visualice la sección ```Installing with an installer```. De click sobre el enlace <a href="https://github.com/IBM-Cloud/ibm-cloud-cli-release/releases/"> ibm-cloud-cli-releases</a>, identifique el sistema operativo en el que va a instalar la CLI de IBM Cloud y descargue el instalador. 

2. Una vez se complete la descarga, de click sobre el instalador y complete el proceso.

3. Cuando se termine la instalación, debe reiniciar el equipo para que se conserven los cambios.

   <p align="center"><img src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/InstalarCLI_IBM.gif"></p>

   <br />

4. Luego de reiniciar el equipo, abra una ventana de ```Windows PowerShell``` y coloque el comando:

   ```PowerShell
   ibmcloud --version
   ```
   Como respuesta debe obtener la versión de ibmcloud.


   <p align="center"><img src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/PruebaIBM_CLI.gif"></p>

   <br />


### Instalación de plug-in kubectl
1. En la página <a href="https://cloud.ibm.com/docs/cli?topic=cli-install-devtools-manually"> Installing the tools and plug-ins manually</a> visualice la sección ```Installing the Kubernetes command line tool```. Identifique el sistema operativo y use el comando respectivo para instalar el plug-in ```kubectl```. Para el caso de Windows, abra una venatna del ```Símbolo del sistema (cmd)``` y allí coloque:

   ```PowerShell
   curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.7.0/bin/windows/amd64/kubectl.exe
   ```
   
   <p align="center"><img src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/Instalar%20kubectl.gif"></p>

   <br />

2. Espere unos minutos mientras se completa la instalación y luego coloque el comando:

   ```PowerShell
   kubectl version 
   ```
   
   Como respuesta debe obtener la versión de kubectl.
   
   <p align="center"><img src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/PruebaVersionKubectl.gif"></p>

   <br />

### Instalación de plug-in IBM Cloud Container Registry
1. En la página <a href="https://cloud.ibm.com/docs/cli?topic=cli-install-devtools-manually"> Installing the tools and plug-ins manually</a> visualice la sección ```Installing IBM Cloud Container Registry CLI plug-in```. Para el caso de Windows, en una venatna de ```Windows PowerShell``` coloque:

   ```PowerShell
   ibmcloud plugin install container-registry
   ```
   
   <p align="center"><img src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/Instalar%20kubectl.gif"></p>

   <br />


## Clonar repositorio :round_pushpin:
1. En la página <a href="https://cloud.ibm.com/docs/cli?topic=cli-install-devtools-manually"> Installing the tools and plug-ins manually</a> visualice la sección ```Installing IBM Cloud Container Registry CLI plug-in```. Para el caso de Windows, en una ventana de ```Windows PowerShell``` coloque:

   ```PowerShell
   ibmcloud plugin install container-registry
   ```
   
   <p align="center"><img src="https://github.com/emeloibmco/IBM-Cloud-Kubernetes-Angular-Web-List/blob/main/Images/Instalar%20kubectl.gif"></p>

   <br />

## Crear imagen docker local de la aplicación :computer:
Al clonar este repositorio puede encontrar dentro de los archivos el *Dockerfile* utilizado para crear la imagen de la aplicación. Realice los siguientes pasos:
<br />

1. En la ventaja de ```Windows PowerShell``` y asegurándose que se encuentra dentro de la carpeta que contiene los archivos de la aplicación y el Dockerfile, coloque el siguiente comando para crear la imagen de su aplicación:

   ```PowerShell
   docker build -t <nombre_imagen:tag> .
   ```

2. Una vez finalice el proceso, verifique en *Docker Desktop* que la imagen que acaba de crear aparece en la lista de imágenes.

3. Si desea probar el funcionamiento de la imagen de forma local, ejecute el siguiente comando (cambie los valores de port, port_dockerfile y nombre_imagen:tag):
  
   ```PowerShell
   docker run --publish port:port_dockerfile <nombre_imagen:tag>
   ```
   
   y coloque en el navegador:
 
   ```PowerShell
   localhost:port
   ```

> Nota: En la variable port puede colocar cualquier valor, por ejemplo 8085. En la variable port_dockerfile por defecto coloque 8080, ya que es el puerto establecido para este ejercicio.

<br />

## Subir imagen de la aplicación a IBM Cloud Container Registry :outbox_tray:
Para subir la imagen creada a *IBM Cloud Container Registry* realice lo siguiente:
<br />

1. En la ventana de *Windows PowerShell* y sin salir en ningún momento de la carpeta que contiene los archivos, inicie sesión en su cuenta de *IBM Cloud* con el siguiente comando:

   ```PowerShell
   ibmcloud login --sso
   ```

2. Seleccione la cuenta en donde se encuentra su clúster de Kubernetes.

3. Una vez ha iniciado sesión, configure el grupo de recursos y la región que está utilizando su clúster de Kubernetes. Para ello utilice el siguiente comando:

   ```PowerShell
   ibmcloud target -r <REGION> -g <GRUPO_RECURSOS>
   ```
   >**Nota**: Reemplace \<REGION> y <GRUPO_RECURSOS> con su información.

4. Registre el daemon de Docker local en *IBM Cloud Container Registry* con el comando:

   ```PowerShell
   ibmcloud cr login
   ```

5. Cree un espacio de nombres (*namespace*) dentro de *IBM Cloud Container Registry* para su imagen. Para ello ejecute el siguiente comando:

   ```PowerShell
   ibmcloud cr namespace-add <namespace>
   ```
   
   >**Nota**: Reemplace \<namespace> con un nombre fácil de recordar y que esté relacionado con la imagen de la aplicación. 

6. Elija un repositorio y una etiqueta con la que pueda identificar su imagen. En este caso, debe colocar la información de la imagen que creó en *Docker* y el espacio de nombres (*namespace*) creado en el ítem anterior. Coloque el siguiente comando:

   ```PowerShell
   docker tag <nombre_imagen:tag> us.icr.io/<namespace>/<nombre_imagen:tag>
   ```
   
   >**Nota**: En el nombre de dominio **us.icr.io**, debe tener en cuenta colocar el dato correcto en base a la región en donde se encuentra su clúster y grupo de recursos. Para mayor información puede consultar <a href="https://cloud.ibm.com/docs/Registry?topic=Registry-registry_overview#registry_regions"> regiones </a>.

7. Envíe la imagen a *IBM Cloud Container Registry* mediante el comando:

   ```PowerShell
   docker push us.icr.io/<namespace>/<nombre_imagen:tag>
   ```

8. Verifique en *IBM Cloud Container Registry* que aparece el espacio de nombres (namespace), el repositorio y la imagen. Tenga en cuenta los nombres que asignó en cada paso.
<br />

## Desplegar imagen de la aplicación en Kubernetes :rocket:
Para desplegar la imagen del frontend de la aplicación en Kubernetes, realice lo siguiente:
<br />

1. En la ventana de *Windows PowerShell* en la que ha trabajado, coloque el siguiente comando para ver la lista de clústers de Kubernetes que hay en su cuenta:

   ```PowerShell
   ibmcloud cs clusters
   ```

2. Verifique el nombre de clúster en el que va a desplegar la imagen y habilite el comando kubectl de la siguiente manera:

   ```PowerShell
   ibmcloud ks cluster config --cluster <cluster_name>
   ```

3. Cree el servicio de despliegue en Kubernetes, para esto, ejecute los comandos que se muestran a continuación (recuerde cambiar \<deployment> con un nombre para su servicio de despliegue):  

   ```PowerShell
   kubectl create deployment <deployment> --image=us.icr.io/<namespace>/<nombre_imagen:tag>
   ```
  
4. A continuación, debe exponer su servicio en Kubernetes, para ello utilice el siguiente comando:

   ```PowerShell
   kubectl expose deployment/<deployment> --type=NodePort --port=8080
   ```
   
5. Por último verifique que el deployment y el service creados aparecen de forma exitosa en el panel de control de su clúster.

<br />

## Verificar el funcionamiento de la aplicación :heavy_check_mark:
Para verificar el correcto funcionamiento de su aplicación en Kubernetes realice lo siguiente:

1. Su aplicación funcionará si coloca en el navegador **IP_Publica:port**. Para obtener la IP Pública coloque el comando:

   ```PowerShell
   ibmcloud ks workers --cluster <ID_Cluster>
   ```

   Para obtener el puerto use el comando:

   ```PowerShell
   kubectl get service <deployment>
   ```

<br />

## Referencias :mag:
<br />

## Autores :black_nib:
Equipo *IBM Cloud Tech Sales Colombia*.
