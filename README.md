# **Diagramas C4 Model test DEVSU**

Este README comenta brevemente el contenido del repositorio

### **Información del repositorio** ###

* Repositorio en el cual se registran los diagramas solicitados
* Version 1.0
* [Repo](https://bitbucket.org/dxl17042006/test)

### **Contenido** ###

* Diagrama de Contexto
* Diagrama de Contenedores
* Diagrama de Componentes
* Diagrama de despliegue

## **Diagrama de Contexto** ##

* Modelo general de la solución planteada, en el cual se observa la iteración del usuario o Customer con los sistemas Core del banco que permite obtener la información del usuario, cuentas, balances y transferencias entre sus cuentas. Es importante comentar que al realizar una transferencia, se debe notificar al usuario por lo cual se plantea dos mecanismos que son:
    * Envío de notificación por correo electrónico, el cual puede ser un servicio interno o externo .
    * Envío de mensajes de textos al dispositivos móvil, conocido como sms, se recomiendo utilizar el servicio de AWS Amazon SNS que permite implementar fácilmente este tipo de mensajería.


## **Diagrama de Contenedores** ##

* En este diagrama se puede observar la tecnología que se plantea para la implementación de este proyecto como se detalla a continuación.

    * SPA: se plantea utilizar JavaScript con React o Angular como tecnología que nos permite desarrollar un sitio web con características óptimas para que el usuario pueda utilizar la página de manera sencilla.
    * Mobile App: Se recomienda utilizar React Native o Angular que son las tecnologías más utilizadas y que nos permite tener aplicaciones multiplataforma sin tener una afectación considerable en el rendimiento de la misma. Flutter una tecnología de Google también es recomendada por su sencilles en el aprendizaje y actualmente va incrementando su adopción para aplicaciones móviles.

    **Nota:** Se debe desarrollar utilizando el concepto de microFrontEnds para facilitar su mantenimiento y rapidez en el desarrollo de software.
    
    * Como orquestador se puede utilizar MODYO que nos permite utilizar Widgets los cuales orquestan los componentes desarrollados sean en Angular o React, lo que facilita su mantenimiento y desarrollo ágil con equipos grandes.

    * Seguridad: Para evitar ser vulnerados todos los datos de entrada sensibles deben ser validados, encriptados, información como tarjetas de crédito, números de cuentas deben ser enviarse de manera encriptada al API para que en el servicio se des encripte y se envíe a buscar la cuenta o tarjeta requerida para una transferencia. 

    *  A nivel de servicios se recomienda utilizar Spring Framework lo cual nos ayuda para implementar MVC en nuestra aplicación, para la creación de las apis tipo REST igualmente podemos utilizar este framework, o si es necesario se puede utilizar Spring Boots para crear microservicios lo cual nos facilita el mantenimiento y agilidad en el desarrollo. 

## **Diagrama de Componentes** ##

* En este diagrama se puede observar como se realizaría el proceso de autenticación (SSO) y como se puede implementar en web y app (considerando el enrolamiento de un usuario y su mecanismo de autenticación que puede ser reconocimiento facial, biometría, etc)
* Adicionalmente se puede observar el modelo planteado para transferencias y consulta de información relacionada a cuentas, pagos del cliente y como interactúa con los distintos componentes.
* Finalmente se puede observar como se puede implementar la auditoría que nos permite registrar toda la información de los usuarios mediante procesos asíncronos que evitan cargar procesamiento cuando existe alta demanda. 
Se recomienda que en los archivos logs nunca se registre información en texto claro información sensible como tarjetas de crédito, números de cuenta, correo electrónico, número de celular, esta información se debe registrar enmascarada para evitar exposición innecesaria de esta información.
* Base de datos, se recomienda utilizar un motor de base robusto como Oracle para registrar la información, la misma que se debe implementar mecanismos de seguridad para no registrar en tablas información sensible en texto claro, por ejemplo los números de tarjeta de crédito deben ser tokenizadas para evitar vulnerabilidades.

## **Diagrama de Despliegue** ##
* Se adiciona este diagrama en el cual se puede observar un flujo que nos permitirá un CD/CI de la aplicación con lo cual utilizando servicios de AWS podemos tener un esquema de alta disponibilidad, escalamiento automático, tolerancia a fallos y podemos monitorear fácilmente.

* Se plantea utilizar servicios de AWS como se detalla a continuación.
    * AWS CodeBuild que nos permitirá compilar el código fuente de la aplicación y generar el war que posteriormente automáticamente se generará la imagen docker que será registrada en AWS ECR. 
    * AWS ECR nos permite registrar los contenedores Docker de manera sencilla y que se lo utilizará en el clúster de Kubernetes.
    * AWS CodePipeline nos permite determinar si se realizó algún cambio en el repositorio del código fuente y se dispara automáticamente para generar el artefacto, por seguridad se recomienda niveles de aprobación para su ejecución.
    * AWS EKS, nos permite ejecutar Kubernetes en la nube de AWS.
    * AWS CloudWatch Logs, nos permite monitorear los servicios.

    Con este esquema se pretende que la aplicación tenga alta disponibilidad ya que automáticamente al utilizar un clúster de Kubernetes se puede configurar el número de PODS mínimos y máximos que son requeridos de acuerdo a la demanda, es decir que automáticamente se crean instancias y permite que la aplicación se recupere rápidamente a fallos en alguna instancia.





