# Desplegar un API rest con python y Flask desde Elastic Beanstalk

## Hola a todos!

Soy Carlos Cortez y aprenderemos elastic beanstalk desde cero. Espero lo disfruten!


## Clonando el repositorio base

Antes de todo, instalemos este repositorio en nuestra máquina local:

git clone git@github.com:ccortezb/eb-awsroadshow-flask-demo.git

> total 24
> -rw-r--r--  1 carlos  staff   2.9K Jun 30 22:42 README.md
> -rw-r--r--  1 carlos  staff   1.1K Jun 30 22:15 application.py
> -rw-r--r--  1 carlos  staff    95B Jun 30 22:14 requirements.txt
> drwxr-xr-x  6 carlos  staff   192B Jun 30 22:13 virt

Ahora a aprender!

## primero instalemos las dependencias

### si estamos en Mac:

> brew install Xcode openssl zlib readline

y luego con brew en MacOS:

> brew install awsebcli

### si deseamos instalarlo manualmente (usuarios avanzados)

> git clone https://github.com/aws/aws-elastic-beanstalk-cli-setup.git

> ./aws-elastic-beanstalk-cli-setup/scripts/bundled_installer

### si somos práctico y usamos pip (nosotros!)

> pip install awsebcli --upgrade --user

> eb --version


## Instalamos virtualenv

> pip3 install virtualenv

> source virt/bin/activate


## instalamos flask framework
> pip install flask==1.0.2

### listamos las dependencias

> pip freeze

### las guardamos en un txt

> pip freeze > requirements.txt

> ll
> total 8
> -rw-r--r--  1 carlos  staff    95B Jun 30 22:14 requirements.txt
> drwxr-xr-x  6 carlos  staff   192B Jun 30 22:13 virt


## creamos una api simple que nos salude con /hello

(usemos el archivo en el repositorio)
y luego corremos en local para probar:

>  python application.py

>  * Serving Flask app "application" (lazy loading)
>  * Environment: production
>    WARNING: Do not use the development server in a production environment.
>    Use a production WSGI server instead.
>  * Debug mode: on
>  * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
>  * Restarting with stat
>  * Debugger is active!
>  * Debugger PIN: 154-924-317


## probamos desde el browser

> http://127.0.0.1:5000/hello


## Creamos un archivo para evitar subir las dependencias

> vim .ebignore
> virt

## Creamos una nueva app en Elastic beanstalk 

> eb init -p python-3.7 flask-roadshow --region us-east-1
> Application flask-roadshow has been created.

##  creamos un acceso para poder entrar por ssh 
> eb init
> Cannot setup CodeCommit because there is no Source Control setup, continuing with initialization
> Do you want to set up SSH for your instances?
> (Y/n): Y

Select a keypair.
1) arduino
2) awsperuerp
3) clase-elb-virginia
4) communitydaylima
5) devartucx
6) ECS-Workshop
7) elearning
8) karma
9) mlflow
10) ofbiz
11) pentaho
12) wiener
13) wiener2017
14) [ Create new KeyPair ]
(default is 13): 3

## desplegamos la app a Elastic Beanstalk

> eb create flask-env

> Creating application version archive "app-200630_222146".
> Uploading flask-roadshow/app-200630_222146.zip to S3. This may take a while.
> Upload Complete.
> Environment details for: flask-env
>   Application name: flask-roadshow
>   Region: us-east-1
>   Deployed Version: app-200630_222146
>   Environment ID: e-sbzi93wy52
>   Platform: arn:aws:elasticbeanstalk:us-east-1::platform/Python 3.7 running on 64bit Amazon Linux 2/3.0.3
>   Tier: WebServer-Standard-1.0
>   CNAME: UNKNOWN
>   Updated: 2020-07-01 03:21:52.814000+00:00

## podemos visitar nuestro nuevo sitio

> eb open

http://flask-env.eba-i5ckdi5n.us-east-1.elasticbeanstalk.com/