# Parcial 3
Felipe Clement - A00320196   
Andrés Villegas - A00239620   
repositorio Github: https://github.com/avillega/so-exam3/   


### Nota: Por alguna razon los gifs no hacen loop, por tanto para verlos quiza sea necesario hacer un refresh de esta pagina.

Para instalar el Stack de sensu se siguieron las instrucciones dadas por el profesor en el respositorio https://github.com/ICESI/so-monitoring . En el cliente la instalación es más sencilla, es necesario instalar sensu, y configurar los archivos para que funcionene correctamente, el `/etc/sensu/conf.d/rabbitmq.json` y `/etc/sensu/conf.d/client.json`. En estos archivos se configura el servidor de rabbitmq y el nombre del cliente como aparecera en el dashboard.    

Para la instalación del stack en el servidor, es necesario instalar redis, rabbitmq y el dashboard uchiwa. La instalación de estos programas del stack necesitan la instalación de varias dependencias, una de las más importantes es erlang, el lenguaje ne que esta escrito rabbitmq. AL instalar estos elementos del stack de sensu, es necesario crear los archivos de configuración. Uno de lso archivos más importantes es el check_apache.json. En este archivo se defienen los checks que tomara sensu y se configura la frecuencia del checkeo.   

A continuación se muestran unos gif del funcionamiento de rabbitmq y el dashboard de uchiwa con el funcionamiento de un check

![alt text](https://raw.githubusercontent.com/avillega/so-exam3/master/A00320196-A00239620/resources/RabbitMQ.png)

![alt text](https://cdn.rawgit.com/avillega/so-exam3/597b25f8/A00320196-A00239620/resources/video_parcial3.gif)   

Para agregar nuevos checks es necesario agregar el programa que se va a usar para checkear. En nuestro caso se uso un check del repositorio de github https://github.com/sensu-plugins/sensu-plugins-cpu-checks . Una vez descargado se debe agregar a la carpeta `/etc/sensu/plugins` y se debe configurar el archivo donde se definen los checks en nuestro caso el archivo `/etc/sensu/conf.d/check_apache.json`. en este archivo se defienen cada cuento se va a ejecutar el check, quien va a ser el handler, en nuestro caso slack y la ruta del archivo que se va a ejecutar y el ambiente de ejecucion. uan vez agregado esto y reiniciado los servicios. el check aparece como parte del cliente en el dashboard de uchiwa. En el siguiente gif se muestra el check adicionado. 


![alt text](https://raw.githubusercontent.com/avillega/so-exam3/ae989515/A00320196-A00239620/resources/video_plugin_extra.gif)


