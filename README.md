# 📋 Form - Sistema en Django

Este proyecto es un sistema desarrollado con **Django** que incluye configuración de base de datos MySQL, seguridad SSL/TLS, manejo de usuarios personalizados y despliegue en producción.

---

## 🚀 Requisitos

* Python 3.9+
* MySQL 5.7+ o MariaDB
* Virtualenv (recomendado)

---

## 📦 Instalación

1. Clonar el repositorio:

   git clone [https://github.com/tuusuario/form.git](https://github.com/tuusuario/form.git)
   cd form

2. Crear y activar un entorno virtual:

   python -m venv venv
   source venv/bin/activate   # Linux/Mac
   venv\Scripts\activate      # Windows

3. Instalar dependencias:

   pip install -r requirements.txt

---

## ⚙️ Configuración

El archivo de configuración principal está en:

form/settings.py

### Base de datos

Actualmente configurado para **MySQL**:

DATABASES = {
'default': {
'ENGINE': 'django.db.backends.mysql',
'NAME': 'sistema',
'USER': 'root',
'PASSWORD': '1234',
'HOST': 'localhost',
'PORT': '3306',
}
}

⚠️ Se recomienda usar variables de entorno para mayor seguridad.

### Seguridad SSL/TLS

El proyecto está preparado para trabajar con HTTPS y certificados:

SECURE_SSL_REDIRECT = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True

Certificados deben ubicarse en la carpeta **ssl/**.

---

## 🛠 Migraciones y Superusuario

1. Crear la base de datos en MySQL:

   CREATE DATABASE sistema;

2. Aplicar migraciones:

   python manage.py migrate

3. Crear superusuario:

   python manage.py createsuperuser

---

## ▶️ Uso en Desarrollo

Con servidor SSL local:

python manage.py runsslserver

Con servidor estándar:

python manage.py runserver

---

## 🚢 Despliegue en Producción

Con **Gunicorn**:

gunicorn form.wsgi:application --bind 0.0.0.0:8000

Se recomienda usar **Nginx** como proxy inverso y manejar certificados con **Certbot**.

---

## 📚 Dependencias

Incluidas en **requirements.txt**:

* asgiref==3.5.1
* dj-database-url==0.5.0
* Django==4.0.2
* gunicorn==20.1.0
* psycopg2==2.9.3
* pytz==2022.1
* sqlparse==0.4.2
* whitenoise==6.2.0
* django-sslserver

---

## 🐳 Ejemplo de Dockerfile

FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

ENV DJANGO_SETTINGS_MODULE=form.settings

CMD ["gunicorn", "form.wsgi:application", "--bind", "0.0.0.0:8000"]

---

## 👤 Autor

Desarrollado por **Ricardo Alcantar**
📧 Contacto: *(agregar tu correo o enlace si deseas)*

---

¿Quieres que también te lo prepare en un **archivo .txt listo para descargar**, además del texto plano que ya puedes copiar?
