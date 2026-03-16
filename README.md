# university-site-django
Проект, выполненный по техническому заданию в стеке django

## Подготовка проекта (Win VSCode)
Установка виртуального окружения
```
py -3.14 -m venv venv
source venv/Scripts/activate
```

В виртуальном окружении установка django, его расширений и debug-панели
```
pip install django django-extensions django-debug-toolbar
pip freeze > requirements.txt
```

Активация отслеживания git (мой репозиторий находится на внешнем диске)
```
git config --global --add safe.directory E:/repositories/django/university-site-django/university-site-django
```

Создание проекта django
```
django-admin startproject universitysite .
```

Подготовка settings.py
```
# установка хостов по умолчанию
sed -i "s/ALLOWED_HOSTS = \[\]/ALLOWED_HOSTS = [\n    'temp',\n]/" universitysite/settings.py
sed -i "s/'temp'/'127.0.0.1', 'localhost'/" universitysite/settings.py
```
```
# добавление приложения для дебаггинга
sed -i "s/INSTALLED_APPS = \[/INSTALLED_APPS = [\n    'debug_toolbar',/" universitysite/settings.py
sed -i "s/MIDDLEWARE = \[/MIDDLEWARE = [\n    'debug_toolbar.middleware.DebugToolbarMiddleware',/" universitysite/settings.py
sed -i "/context_processors.*\[/,/\]/ s/]/    'django.template.context_processors.debug',\n        ]/" universitysite/settings.py
echo -e "\n# Django Debug Toolbar\nINTERNAL_IPS = ['127.0.0.1']" >> universitysite/settings.py
```
```
# Template DIRS
sed -i "s/'DIRS': \[\]/'DIRS': \[\n            BASE_DIR \/ 'templates',\n        ]/" universitysite/settings.py
```
```
# Директории для статики и медиа
cat >> universitysite/settings.py << 'EOF'

# Static files
STATICFILES_DIRS = [
    BASE_DIR / 'static',
]

# Media files
MEDIA_ROOT = BASE_DIR / 'media'
MEDIA_URL = 'media/'
EOF
```

Создание приложений (шаблон)
```
python manage.py startapp MyApp
```