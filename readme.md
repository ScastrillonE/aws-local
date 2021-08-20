## Requisitos
 - Docker
 - Docker compose
 -  Python
 -  Pip

### Instalar Docker

Para realizar la instalación de docker entre en el link que le corresponda según su SO 

Windows: [https://docs.docker.com/desktop/windows/install/](https://docs.docker.com/desktop/windows/install/)

MacOs: [https://docs.docker.com/desktop/mac/install/](https://docs.docker.com/desktop/mac/install/)

Ubuntu: [https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)

### Correr servidor LocalStack

Para levantar el servicio usando docker-compose nos ubicamos la carpeta "aws-local" renombramos el archivo ".example-env" por ".env" y ejecutamos el siguiente codigo: 
```
> docker-compose -f localstack build

> docker-compose -f localstack up
```
y listo.
## Configuración inicial (aws cli)

En una consola/terminal diferente de la que tiene en ejecución el localstack hace lo siguiente:

Si aun no tiene instalado **aws cli** ejecute:
```
pip install awscli
```

aws requiere que se establezcan la región y las credenciales para ejecutar los comandos de aws, para configurar esto use el siguiente comando:

```
> aws configure --profile default

#Rellenamos los datos de la siguiente manera
> AWS Access Key ID [None]: test
> AWS Secret Access Key [None]: test
> Default region name [None]: us-east-1        
> Default output format [None]: json
```

## Inicio rápido (probando localstack con aws cli)

La dirección por defecto en la que se ejecuta los servicios de localstack es: http://localhost:4566  por lo que usaremos esta dirección para realizar nuestras pruebas, a continuación crearemos una cola(sqs) para esto usamos el siguiente comando:
```
aws --endpoint-url=http://localhost:4566 sqs create-queue --queue-name  scastrillone
```
Como vemos estamos usando el parámetro ```--endpoint-url``` para indicar  la url en la que se esta ejecutando el servicio localstack(aws)  luego indicamos el servicio que se usara en este caso **sqs** y le indicamos que queremos crear una nueva cola  y también se le pasa el nombre en este caso "scastrillone" 

al ejecutar el comando nos regresa en formato json la url de la cola que acabamos de crear

```
{
    "QueueUrl": "http://localhost:4566/000000000000/scastrillone"
}
```
Y como pueden ver se conecta correctamente a nuestro servicio localstack.

Tambien se puede usar librerias como **boto3** e incluso el **Cloud Development Kit (CDK)** de AWS.
