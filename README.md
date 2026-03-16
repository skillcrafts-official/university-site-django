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
sed -i "s/ALLOWED_HOSTS = \[\]/ALLOWED_HOSTS = [\n    'temp',\n]/" universitysite/settings.py
sed -i "s/'temp'/'127.0.0.1', 'localhost'/" universitysite/settings.py
```

Создание приложений (шаблон)
```
python manage.py startapp MyApp
```