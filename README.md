# Proyecto de hoy

### Primero para iniciar el proyecto Django
hay que crear una carpeta en dentro del proyecto que veniamos trabajando.
```bash
mkdir cv
```
### Despues hay que ingresar a la carpeta y crear el entorno virtual

```bash
python -m venv cv-env
```

### Una vez creador debemos activar el entorno virtual.

```bash
source cv-env/scripts/activate
```

### Una vez activo el entorno virtual debemos instalar la dependencia a trabajar, en este caso Django 4.1

```bash
pip install django==4.1
```

### Creamos un proyecto en Django con el siguiente comando

```bash
django-admin startproject mycv
```
### Esperamos inicie el proyecto y despues probamos que todo este correctamente funcionando

```bash
python manage.py runserver
```

### Despues instalamos la aplicacion que va a correr nuestro sistema

```bash
python manage.py startapp base
```

**base** en este caso seria la aplicación principal de nuestro proyecto que va a hacer que el poryecto funcione.

### Despues vamos a incorporar **base** a nuestro proyecto dirigiendonos a mycv/settings.py

```bash #settings.py
# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'base', # Esta es la aplicacion que creamos y la incorporamos a nuestro proyecto
]
```

Despues debemos agregar una definicion al final para que nuestra aplicacion pueda servir imagenes y el css de nuestro proyecto.

```bash #setting.py
import os
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, "static"),  
]

MEDIA_URL = "/img/"
```

Ahora bien vamos a crear una carpeta **templates** en la aplicacion llamada **base** de nuestro proyecto y dentro creamos el **home.html**.
```bash 
base/templates/home.html
```

Bien vamos a ir a este repositorio y vamos a copiar el templates/home.html para que tengamos el mismo el funcionamiento.

Con la ultima definicion declarada en **setting.py** debemos crear una carpeta llamada **static** que esta sirve como ancla de las imágenes y archivos css que tengamos para nuestro proyecto.
**static/**.

Dentro de **static** debemos crear dos carpetas.
- La primera se llamara **css**
- La segunda será **img**

Ahora bien debemos acomodar nuestos archivos del proyecto para que funcionen correctamente.

- Primero hay que modificar el archivo views.py

```bash #base/views.py
from django.shortcuts import render

# Create your views here.
def home(request):
    return render(request, 'base/home.html')

```
- Segundo hay que crear el archivo urls.py en el mismo directorio **base**

```bash #base/urls.py

from django.urls import path

from . import views

urlpatterns = [
    path('', views.home, name='home'),
    
    ]

```

- Tercero debemos ir al proyecto **mycv** al arhivo urls.py e incluir estas nuevas vistas.

```bash #mycv/urls.py

from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('base.urls'))
]


```

Ahora para finalizar debemos volver al servidor.

```bash
python manage.py runserver

```

Y eso seria todo.