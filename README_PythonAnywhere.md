# Despliegue rápido en PythonAnywhere (plan gratis)

1) Entrá a https://www.pythonanywhere.com/ y creá tu cuenta.
2) En la pestaña **Files**, subí el ZIP `cinear_blog.zip` y descomprimilo.
3) Abrí una **Consola Bash** y ejecutá:
```
cd ~/cinear_blog
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser  # (usuario admin)
python manage.py collectstatic    # y responde 'yes'
```
4) En **Web** > **Add a new web app** > **Manual configuration** > **Python 3.x**.
5) En **Source code** poné: `/home/tuusuario/cinear_blog`
6) En **WSGI configuration file** reemplazá el contenido por:
```
import os, sys
path = '/home/tuusuario/cinear_blog'
if path not in sys.path:
    sys.path.append(path)
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'cinear_blog.settings')
from django.core.wsgi import get_wsgi_application
application = get_wsgi_application()
```
7) En **Static files**, agregá:
- URL: `/static/` — Directory: `/home/tuusuario/cinear_blog/staticfiles`
8) **Reload**. Listo. Podés entrar a tu subdominio.
