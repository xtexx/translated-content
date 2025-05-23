---
title: "Руководство по Django часть 2: создание скелета"
slug: Learn_web_development/Extensions/Server-side/Django/skeleton_website
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/Server-side/Django/Tutorial_local_library_website", "Learn/Server-side/Django/Models", "Learn/Server-side/Django")}}

Это вторая статья из нашего [руководства по Django](/ru/docs/Learn_web_development/Extensions/Server-side/Django/Tutorial_local_library_website), которая показывает, как можно создать "скелет" сайта, как фундамент, на котором можно строить всё остальное: настройки, ссылки, модели, контроллеры и представления.

| Необходимо: | [Настройка окружения](/ru/docs/Learn_web_development/Extensions/Server-side/Django/development_environment). Прочитать первую статью [руководства по Django](/ru/docs/Learn_web_development/Extensions/Server-side/Django/Tutorial_local_library_website). |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Цель:       | Научиться использовать инструменты Django для создания новых веб-сайтов.                                                                                                                                                                                   |

## Обзор

Эта статья показывает, как можно создать "скелет"(прототип) сайта, который затем можно расширить при помощи различных настроек, url адресов, моделей, представлений, и шаблонов (эти темы будут объясняться в последующих статьях).

Алгоритм следующий:

1. Использовать `django-admin` для создания папки проекта, шаблонов остальных файлов, и скрипта для управления проектом (**manage.py**).
2. Использовать **manage.py** _для создания одного или нескольких_ приложений.

   > [!NOTE]
   > Сайт может состоять из одной или нескольких различных частей, например: основная часть, блог, вики, раздел загрузок, и так далее. Философия Django подталкивает разработчиков создавать эти части, как разные **приложения**, которые, если понадобится, могут быть использованы повторно в других проектах.

3. Зарегистрировать в настройках эти приложения, чтобы использовать их в проекте.
4. Настроить маршруты url адресов для каждого из приложений.

Для [Сайта местной библиотеки](/ru/docs/Learn_web_development/Extensions/Server-side/Django/Tutorial_local_library_website) папка сайта и проекта будет называться _locallibrary_, и у нас будет одно приложение с названием _catalog_. Верхняя структура проекта будет следующей:

```bash
locallibrary/         # Папка сайта
    manage.py         # Скрипт для управления проектов (создан manage.py)
    locallibrary/     # Папка сайта/проекта (создана manage.py)
    catalog/          # Папка приложения (также создана manage.py)
```

Следующие разделы статьи разложат по полочкам этапы создания "скелета", и покажут вам, как можно проверить сделанные изменения. В конце статьи мы обсудим некоторые другие настройки сайта, которые можно назначить на этом этапе.

## Создание проекта

Для начала откройте командную строку/терминал, перейдите в ту папку, куда вы хотите поместить проект Django(лучше в папке профиля пользователя `C:\Users\user_name`, при запуске командной строки используется именно эта директория), и создайте папку для вашего нового сайта (в данном случае: _locallibrary_). Затем войдите в эту папку, используя команду cd:

```bash
mkdir locallibrary
cd locallibrary
```

Создайте новую папку, используя команду `django-admin startproject` как в примере ниже, и затем зайдите в созданную папку.

```bash
  django-admin startproject locallibrary .
cd locallibrary
```

Команда `django-admin` создаст файловую структуру, как в примере ниже:

```bash
locallibrary/
    manage.py
    locallibrary/
        settings.py
        urls.py
        wsgi.py
```

Подпапка проекта _locallibrary_ это ключевая директория нашего проекта:

- **settings.py** содержит в себе все настройки проекта. Здесь мы регистрируем приложения, задаём размещение _статичных_ файлов, настройки базы данных и так далее.
- **urls.py** задаёт ассоциации url адресов с представлениями. Несмотря на то, что этот файл может содержать _все_ настройки url, обычно его делят на части, по одной на приложение, как будет показано далее.
- **wsgi.py** используется для налаживания связи между вашим Django приложением и веб-сервером. Вы можете воспринимать его, как утилиту.

Скрипт **manage.py** используется для создания приложений, работы с базами данных и для запуска отладочного сервера.

## Создание приложения Каталог

Выполнив предыдущие шаги, запустите следующую команду для создания приложения _catalog_, который будет размещён внутри папки locallibrary (команду необходимо выполнять из папки, в которой находится **manage.py**):

```bash
python3 manage.py startapp catalog
```

> [!NOTE]
> Приведённая выше команда справедлива для GNU Linux/Mac OS. На Windows команда должна иметь вид: `py -3 manage.py startapp catalog`
>
> Если вы работаете под Windows, заменяйте команду `python3` на `py -3` в этой и следующих статьях.

Эта команда создаст новую папку и наполнит её файлами различных частей приложения (выделенные **полужирным** ниже). Большинство файлов названы, исходя из их назначения (например контроллеры(views) должны находится во **views.py**, модели в **models.py**, тесты в **tests.py**, настройки административной части в **admin.py**, регистрация приложения в **apps.py**) и уже содержат некоторый шаблонный код для работы с вышеназванными объектами.

Обновлённая директория должна выглядеть следующим образом:

```bash
locallibrary/
    manage.py
    locallibrary/
    catalog/
        admin.py
        apps.py
        models.py
        tests.py
        views.py
        __init__.py
        migrations/
```

Кроме перечисленных выше файлов были созданы:

- Папка _migrations_ используется, чтобы хранить"миграции" — файлы, которые позволяют вам автоматически обновлять базу данных по мере изменения моделей.
- **\_\_init\_\_.py** — пустой файл для того, чтобы Django и Python распознавали папку как [Python модуль](https://docs.python.org/3/tutorial/modules.html#packages) и позволяет нам использовать его объекты внутри других частей проекта.

> [!NOTE]
> Заметили, что некоторых файлов не хватает? В то время, как там нашли себе место файлы для контроллеров(views) и моделей(models), файлов для настройки url соотносителя, шаблонов, и статичных файлов создано не было. Далее мы покажем, как их создать (они не обязательны для каждого сайта, но нужны в данном примере).

## Регистрация папки с приложением

После создания приложения, нам нужно зарегистрировать его в проекте, чтобы различные утилиты затрагивали его своим действием (например при добавлении моделей в базу данных). Приложения регистрируются добавлением их названий в список `INSTALLED_APPS` в настройках проекта(который, как мы помним, называется **settings.py**).

Откройте файл **locallibrary/locallibrary/settings.py** и найдите в нём список `INSTALLED_APPS` . Затем добавьте новую строку в конец списка, как показано **полужирным** ниже.

```bash
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'catalog.apps.CatalogConfig',
]
```

Новая строка указывает на файл конфигурации приложения (`CatalogConfig`), который был создан в **/locallibrary/catalog/apps.py** , когда вы создали приложение.

> [!NOTE]
> Легко заметить, что в `INSTALLED_APPS` уже подключено большое количество приложений (и объектов `MIDDLEWARE`, ниже в файле конфигурации). Они добавляют поддержку [админ-панели Django](/ru/docs/Learn_web_development/Extensions/Server-side/Django/Admin_site) и, как следствие, огромное количество функциональности (включая сессии, аутентификацию и прочее).

## Настройка базы данных

На этом шаге обычно указывают базу данных для будущего проекта — имеет смысл использовать для разработки и размещённого в Сети одну и ту же базу данных, по возможности, чтобы исключить различия в поведении. Про различные варианты вы можете прочитать в документации Django в разделе [Базы данных](https://docs.djangoproject.com/en/1.10/ref/settings/#databases).

Мы будем использовать базу данных SQLite для этого проекта, потому что не предполагаем большое количество одновременных запросов на неё, а ещё потому, что для её настройки совсем не надо ничего делать! Вы можете видеть, что база данных уже настроена в **settings.py** (подробная информация указана ниже):

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```

Так как мы используем SQLite, то нам не нужно ничего делать.

Давайте продолжим!

## Другие настройки проекта

Файл **settings.py** так же применяется и для некоторых других настроек, но на данном шаге имеет смысл поменять разве что [TIME_ZONE](https://docs.djangoproject.com/en/1.10/ref/settings/#std:setting-TIME_ZONE) — это значение должно быть представлено строкой, указанной в [списке часовых поясов tz](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (колонка TZ в таблице, в строке временной зоны, которая вам нужна). Измените `TIME_ZONE` на одну из строк из таблицы, которая отвечает вашему часовому поясу. Например:

```python
TIME_ZONE = 'Europe/Moscow'
```

В файле присутствует две настройки, которые не нужно менять сейчас, но о назначении которых следует знать:

- `SECRET_KEY`. Это секретный ключ, который используется Django для поддержки безопасности сайта. Если вы раскроете этот ключ в процессе разработки кому-либо, то необходимо будет его сменить (возможно считать его с какого-либо файла на сервере или переменной окружения) когда будете размещать проект на сервер.
- `DEBUG`. Включает подробные сообщения об ошибках, вместо стандартных HTTP статусов ответов. Должно быть изменено на `False` на сервере, так как эта информация очень много расскажет взломщикам.

## Подключение URL-адреса

При создании сайта, был создан файл сопоставления URL (**urls.py**) в корне проекта. Хотя можно использовать его для обработки всех URL адресов, более целесообразно подключать отдельные файлы сопоставлений для каждого приложения.

Откройте **locallibrary/locallibrary/urls.py** и обратите внимание на закомментированный текст, который объясняет суть происходящего.

```python
"""
locallibrary URL Configuration

The `urlpatterns` list routes URLs to views. For more information please see:
    https://docs.djangoproject.com/en/1.10/topics/http/urls/
Examples:
Function views
    1. Add an import:  from my_app import views
    2. Add a URL to urlpatterns:  url(r'^$', views.home, name='home')
Class-based views
    1. Add an import:  from other_app.views import Home
    2. Add a URL to urlpatterns:  url(r'^$', Home.as_view(), name='home')
Including another URLconf
    1. Import the include() function: from django.conf.urls import url, include
    2. Add a URL to urlpatterns:  url(r'^blog/', include('blog.urls'))
"""
from django.urls import path
from django.contrib import admin


urlpatterns = [
    path('admin/', admin.site.urls),
]
```

URL соотношения хранятся в переменной `urlpatterns`, которая является списком функций `path()`. Каждая `path()` функция или ассоциирует шаблон URL\_ _с контроллером(views) или же его с другим таким списком (во втором случае, первый URL становится "базовым" для других, которые определяются в дочернем списке). Список `urlpatterns` инициализирует список функции, которая, например, соотносит \_admin/_ с модулем `admin.site.urls` , который содержит собственный файл-соотноситель.

Добавьте строчки, приведённые ниже в низ файла **urls.py** , чтобы добавить новый элемент в список `urlpatterns`. Этот элемент содержит `url()` который направляет запросы с URL `catalog/` к модулю `catalog.urls` (файл с относительным путём **/catalog/urls.py**).

```python
# Используйте include() чтобы добавлять URL из каталога приложения
from django.urls import include
from django.urls import path
urlpatterns += [
     path('catalog/', include('catalog.urls')),
]
```

Теперь давайте перенаправим корневой URL нашего сайта (например `127.0.0.1:8000`) на URL `127.0.0.1:8000/catalog/`; это единственное приложение, которое мы собираемся использовать, поэтому это вполне разумно. Чтобы это использовать, нам понадобится специальная функция (`RedirectView`), которая принимает первым параметром новый относительный URL на который следует перенаправлять (`/catalog/`) когда указанный в функции `url()` адрес соотносится с адресом запроса (корневой URL, в данном случае).

Добавьте следующие строчки, тоже в конец файла:

```python
# Добавьте URL соотношения, чтобы перенаправить запросы с корневого URL, на URL приложения
from django.views.generic import RedirectView
urlpatterns += [
    path('', RedirectView.as_view(url='/catalog/', permanent=True)),
]
```

Django не размещает _статические_ файлы(CSS, JavaScript, и изображения) по умолчанию, но это было бы крайне полезно на этапе разработки нашего сайта. В самом конце нашего URL соотносителя, можно включить размещение статических файлов.

Добавьте последнюю часть в конец файла:

```
# Используйте static() чтобы добавить соотношения для статических файлов
# Только на период разработки
from django.conf import settings
from django.conf.urls.static import static

urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```

> [!NOTE]
> Существуют различные способы дополнения списка `urlpatterns` (в примере мы просто добавляли объект, используя оператор `+=` чтобы чётко разделить изначальный и дописанный код). Вместо этого, мы могли бы добавить соотношения внутрь определения переменной:
>
> ```
> urlpatterns = [   path('admin/', admin.site.urls),
> path('catalog/', include('catalog.urls')),path('',
> RedirectView.as_view(url='/catalog/', permanent=True)), ] +
> static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
> ```
>
> Кроме того, мы добавили import вниз файла (`from django.urls import include`) ,чтобы видеть, что мы добавили, но обычно все инструкции import добавляются в верхнюю часть файла.

Напоследок, создайте файл **urls.py** внутри папки **catalog**, и добавьте следующий код, чтобы определить (пустой) `urlpatterns`. Сюда мы будем добавлять наши URL соотношения, по мере разработки сайта.

```python
from django.urls import path
from . import views


urlpatterns = [

]
```

## Тестирование работы скелета

На этом, мы создали прототип сайта. Пока сайт ничего не умеет делать, но стоит запустить его, чтобы убедиться, что мы ничего не сломали.

До этого, нам предстоит впервые запустить _миграцию базы данных_. Это обновит нашу базу данных и добавит туда необходимые модели (и уберёт некоторые предупреждения, которые были бы показаны при попытке запуска).

### Запуск миграций базы данных

Django использует Объектный Соотноситель Связей (ORM) чтобы соотносить определения моделей в Django приложении со структурами данных, которые используются базой данных. Когда мы меняем наши модели, Django отслеживает изменения и может создать файлы миграций (в папке **/locallibrary/catalog/migrations/**) чтобы применить соответствующие структуры данных к базе, чтобы та соответствовала модели.

При создании сайта, Django автоматически добавил несколько моделей, чтобы мы могли их использовать в админ-панели (о которой мы поговорим позже). Выполните следующие команды, чтобы создать нужные таблицы в базе данных, соответствующие этим моделям (убедитесь, что вы находитесь в папке с **manage.py**):

```bash
python3 manage.py makemigrations
python3 manage.py migrate
```

> [!WARNING]
> Необходимо выполнять команды выше каждый раз, когда вы меняете модели таким образом, что структура таблицы изменится(включая добавления и удаления как отдельных полей, так и целых моделей).

`Команда makemigrations` _создаёт_ (но не применяет) миграции для всех приложений, которые установлены в ваш проект (вы так же можете указать в конце имя конкретного приложения, чтобы создать миграции только для него). Это даёт вам возможность проверить код перед тем, как их применить — когда вы станете хорошо разбираться в Django, то сможете даже менять их!

Команда `migrate` применяет созданные миграции к базе (Django отслеживает, какие миграции были созданы для данной базы).

> [!NOTE]
> Посмотрите раздел [Миграции](https://docs.djangoproject.com/en/2.2/topics/migrations/) в документации Django чтобы получить информацию о менее распространённых командах для управления миграциями.

### Запуск сайта

Во время разработки, вы можете проверить свой сайт, разместив его на _встроенном отладочном сервере_, и просмотрев его в своём браузере.

> [!NOTE]
> Отладочный веб-сервер не настолько функционален и производителен, для постоянного размещения , но это самый простой способ запустить свой сайт на Django и проверить его на наличие ошибок. По умолчанию, он разместит сайт на вашем компьютере (`http://127.0.0.1:8000/)`, но вы так же можете указать различные компьютеры в вашей сети для этой цели. Для получения большего количества информации загляните в раздел [django-admin и manage.py: отладочный сервер](https://docs.djangoproject.com/en/2.2/ref/django-admin/) документации Django.

Запустите веб-сервер, используя команду _runserver_ (в той же папке, что и **manage.py**):

```bash
python3 manage.py runserver

 Performing system checks...

 System check identified no issues (0 silenced).
 September 22, 2016 - 16:11:26
 Django version 1.10, using settings 'locallibrary.settings'
 Starting development server at http://127.0.0.1:8000/
 Quit the server with CTRL-BREAK.
```

Когда сервер запустится, вы сможете посетить сайт по адресу `http://127.0.0.1:8000/` в вашем веб-браузере. Вы должны увидеть страницу с ошибкой, навроде этой:

![Django debug page for a 404 not found error](django_404_debug_page.png)

Не волнуйтесь! Эта страница должна появиться и сообщить нам, что мы ещё не настроили ни одной страницы в модуле `catalogs.urls` (на который мы были перенаправлены запросили корневой URL сайта).

> [!NOTE]
> Показанная выше страница открывает нам одно из замечательных свойств Django — автоматические отчёты об ошибках. На экране с ошибкой отображается множество полезной информации, когда страница не найдена, или ошибка была вызвана кодом. В данном случае, мы видим, что запрошенный URL не соответствует ни одному шаблону (из указанных). Подобные отчёты будут выключены при DEBUG=False (когда мы разместим приложение в Сеть), в этом случае будет показана менее информативная, но более дружелюбная к пользователю страница(которую вам надо будет создать - прим. переводчика).

На данном этапе, мы поняли, что Django работает должным образом!

> [!NOTE]
> Вам следует перезапускать миграцию и заново тестировать сайт, после того как вы делаете важные изменения. Поверьте, это не займёт много времени!

## Домашнее задание

Папка **catalog/** содержит файлы контроллеров(views), моделей(models), и других частей приложения. Просмотрите эти файлы.

Как было написано выше, URL соотноситель для админ-панели был подключён в файле **urls.py**. Войдите в административную часть и посмотрите, что произойдёт (вы можете найти URL из соотношения выше).

## Подводя итоги

Теперь вы создали полноценный скелет веб-приложения, который теперь вы можете расширить url соотносителями, контроллерами(views) и моделями(models).

Теперь скелет [Сайта местной библиотеки](/ru/docs/Learn_web_development/Extensions/Server-side/Django/Tutorial_local_library_website) сделан и запущен, теперь самое время начать писать код, который научит сайт делать то, что он должен делать.

## Смотрите также

- [Пишем своё первое приложение на Django - часть 1](https://docs.djangoproject.com/en/2.2/intro/tutorial01/) (документация Django)
- [Приложения](https://docs.djangoproject.com/en/2.2/ref/applications/) (документация Django). содержит информацию о настройке приложений.

{{PreviousMenuNext("Learn/Server-side/Django/Tutorial_local_library_website", "Learn/Server-side/Django/Models", "Learn/Server-side/Django")}}
