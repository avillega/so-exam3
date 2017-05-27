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


## Instalacion Stack ELK

El stack ELK consiste en Elasticsearch, Logstash, Kibana y Filebeat, a continuacion se indica el proceso de instalacion de estos servicios.

#### ElasticSearch

El primer paso es instalar un jdk de java de version 1.6 en adelante, lo cuel se puede lograr a traves del siguiente comando:
>yum install java-1.8.0-openjdk.x86_64

Despues, se debe descargar e instalar la llave publica para el repositorio de Elasticsearch:
>rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch

Se procede a crear el repositorio de Elasticsearch de la siguiente manera:

>[elasticsearch-5.x]
>name=Elasticsearch repository for 5.x packages
>baseurl=https://artifacts.elastic.co/packages/5.x/yum
>gpgcheck=1
>gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
>enabled=1
>autorefresh=1
>type=rpm-md

Habiendo hecho esto, solo se debe instalar mediante el siguiente comando:
>yum install elasticsearch

#### Logstash

Se debe a crear el repositorio de Logstash de la siguiente manera:

>[logstash-5.x]
>name=Elastic repository for 5.x packages
>baseurl=https://artifacts.elastic.co/packages/5.x/yum
>gpgcheck=1
>gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
>enabled=1
>autorefresh=1
>type=rpm-md

Habiendo hecho esto, solo se debe instalar mediante el siguiente comando:
>yum install logstash

#### Kibana

Se debe a crear el repositorio de Kibana de la siguiente manera:

>[kibana-5.x]
>name=Kibana repository for 5.x packages
>baseurl=https://artifacts.elastic.co/packages/5.x/yum
>gpgcheck=1
>gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
>enabled=1
>autorefresh=1
>type=rpm-md

Habiendo hecho esto, solo se debe instalar mediante el siguiente comando:
>yum install kibana

#### Filebeat

Se debe descargar e instalar la llave publica para el repositorio de Filebeat:
>rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch

Se procede a crear el repositorio de Filebeat de la siguiente manera:

>[elastic-5.x]
>name=Elastic repository for 5.x packages
>baseurl=https://artifacts.elastic.co/packages/5.x/yum
>gpgcheck=1
>gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
>enabled=1
>autorefresh=1
>type=rpm-md

Habiendo hecho esto, solo se debe instalar mediante el siguiente comando:
>yum install filebeat

Posteriormente, se desea iniciar Filebeat en el arranque, lo cual se hace a traves del comando:
>sudo chkconfig --add filebeat

### Ejemplo

La configuracion de ElasticSearch puede ser modificada en el siguiente archivo: /etc/elasticsearch/elasticsearch.yml

Donde se puede cambiar la ip y puerto del servidor segun lo sea necesario; en caso de cambiar el puerto a uno que no este abierto, se debera usar (ejemplo con puerto 9200):

>firewall-cmd --zone=public --add-port=9200/tcp --permanent
>firewall-cmd --reload

Prueba de instalacion correcta de kibana y elasticsearch

![alt text](https://github.com/ClementFelipe/so-exam3/blob/master/A00320196-A00239620/resources/Instalacion%20ELK.png)
