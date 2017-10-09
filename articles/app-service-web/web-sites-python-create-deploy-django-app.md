---
title: "aaaCreating веб-приложений с Django в Azure"
description: "Учебник, в котором представлены toorunning Python веб-приложения в веб-приложениях службы приложений Azure."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 9be1a05a-9460-49ae-94fb-9798f82c11cf
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 26a131da358748bd6fe4ee5c114d0a8f91b83cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a>Создание веб-приложений с помощью Django в Azure
В данном учебнике как tooget к выполнению Python на [веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714). Служба веб-приложений предоставляет ограниченное бесплатное размещение приложений, а также возможности их быстрого развертывания и использования языка Python. Здравствуйте, по мере роста приложения, можно переключить toopaid размещение и также можно интегрировать со всеми другими службами Azure.

Вы создадите приложения с помощью веб-платформа Django hello (см. другие версии этого учебника, чтобы [термосе](web-sites-python-create-deploy-flask-app.md) и [Bottle](web-sites-python-create-deploy-bottle-app.md)). Будет создать веб-приложение hello из hello Azure Marketplace, Настройка развертывания Git и клонировать репозиторий hello локально. Затем можно будет запустить приложение hello локально, внести изменения, зафиксируйте и отправьте их tooAzure. Здравствуйте учебника показано, как toodo это в Windows или Mac и Linux.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

## <a name="prerequisites"></a>Предварительные требования
* Windows, Mac или Linux
* Python 2.7 или 3.4
* setuptools, pip, virtualenv (только для Python 2.7)
* Git
* [средствами Python для Visual Studio][средствами Python для Visual Studio] (PTVS) (необязательно).

**Примечание.** Публикация TFS в настоящее время для проектов Python не поддерживается.

### <a name="windows"></a>Windows
Если у вас еще не установлен Python 2.7 или 3.4 (32-разрядная версия), рекомендуется сначала установить [пакет SDK для Azure для Python 2.7] или [пакет SDK для Azure для Python 3.4] с помощью установщика веб-платформы. При этом устанавливаются hello 32-разрядной версии Python дублирует, pip, virtualenv, (32-разрядных Python —, установленных на компьютерах hello Azure узлов) и т. д. Python также можно скачать с веб-сайта [python.org].

Для Git рекомендуется использовать [Git для Windows] или [GitHub для Windows]. При использовании Visual Studio, можно использовать поддержку hello интеграции Git.

Мы также рекомендуем установить [инструменты Python 2.2 для Visual Studio]. Это не обязательно, но если у вас [Visual Studio], включая hello освободить Visual Studio Community 2013 или Visual Studio Express 2013 для Web, а затем это даст значительные среду IDE Python.

### <a name="maclinux"></a>Mac/Linux
У вас должны быть установлены Python и Git. Убедитесь, что у вас установлена версия Python 2.7 или 3.4.

## <a name="web-app-creation-on-portal"></a>Создание веб-приложения на портале
Hello первым шагом при создании приложения является toocreate hello веб-приложения через hello [портала Azure](https://portal.azure.com).

1. Войдите на портал Azure hello и щелкните hello **NEW** кнопки в левом нижнем углу hello.
2. В поле поиска hello введите «python».
3. В результатах поиска hello, выберите **Django** (опубликованное PTVS), затем нажмите кнопку **создать**.
4. Настройте hello новый Django приложение, таких как создание нового плана служб приложений и новую группу ресурсов для него. Затем щелкните **Создать**.
5. Настроить публикацию Git для только что созданный веб-приложения в соответствии с инструкциями hello в [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).

## <a name="application-overview"></a>Обзор приложений
### <a name="git-repository-contents"></a>Содержимое репозитория Git
Ниже приведен обзор hello файлов, которые можно найти в hello исходный репозиторий Git, который мы будем клонировать в следующем разделе hello.

    \app\__init__.py
    \app\forms.py
    \app\models.py
    \app\tests.py
    \app\views.py
    \app\static\content\
    \app\static\fonts\
    \app\static\scripts\
    \app\templates\about.html
    \app\templates\contact.html
    \app\templates\index.html
    \app\templates\layout.html
    \app\templates\login.html
    \app\templates\loginpartial.html
    \DjangoWebProject\__init__.py
    \DjangoWebProject\settings.py
    \DjangoWebProject\urls.py
    \DjangoWebProject\wsgi.py

Основными источниками для приложения hello. Состоит из 3 страниц (index, about, contact) с макетом главной страницы. Использует такое статическое содержимое и сценарии, как bootstrap, jquery, modernizr и respond.

    \manage.py

Поддержка локального сервера управления и разработки. Используйте это приложение hello toorun локально, синхронизацию базы данных hello и т. д.

    \db.sqlite3

База данных по умолчанию. Включает необходимые таблицы hello для toorun приложения hello, но не содержит всех пользователей (синхронизации toocreate hello базы данных пользователя).

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

Файлы проекта для использования со [средствами Python для Visual Studio].

    \ptvs_virtualenv_proxy.py

Прокси-сервер IIS для виртуальных сред и поддержки удаленной отладки PTVS.

    \requirements.txt

Внешние пакеты, необходимые для этого приложения. скрипт развертывания Hello будет pip hello пакетов установки, перечисленные в этом файле.

    \web.2.7.config
    \web.3.4.config

Файлы конфигурации IIS. скрипт развертывания Hello будет использовать соответствующий web.x.y.config hello и скопируйте его в файле web.config.

### <a name="optional-files---customizing-deployment"></a>Дополнительные файлы — настройка развертывания
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>Дополнительные файлы — среда выполнения Python
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>Дополнительные файлы на сервере
Некоторые файлы на сервере hello существует, но не добавляются toohello репозитории. Эти отчеты создаются с hello сценария развертывания.

    \web.config

Файл конфигурации IIS. Создается из файла web.x.y.config при каждом развертывании.

    \env\

Виртуальная среда Python. Создан во время развертывания, если совместимый виртуальной среды не существует на веб-приложения hello. Пакеты, перечисленные в requirements.txt являются pip установлен, но pip пропустит установки, если hello пакеты уже установлены.

Hello следующие 3 рассматриваются как tooproceed с hello веб-разработки приложений в разделе 3 различных сред:

* Windows, со средствами Python для Visual Studio
* Windows с командной строкой;
* Mac и Linux с командной строкой.

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Развертывание веб-приложений — Windows — средства Python для Visual Studio
### <a name="clone-hello-repository"></a>Клон hello репозитория
Во-первых клонирование репозитория hello, с помощью hello URL-адрес, указанный на портале Azure hello. Дополнительные сведения см. в разделе [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).

Привет открыть файл решения (SLN-файл), включенный в корне репозитория hello hello.

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a>Создание виртуальной среды
Теперь мы создадим виртуальную среду для локальной разработки веб-сайта. Щелкните правой кнопкой мыши **Python Environments** (Среды Python) и выберите **Add Virtual Environment...** (Добавить виртуальную среду...).

* Убедитесь, что имя hello среды hello `env`.
* Выберите базовый интерпретатор hello. Убедитесь, что toouse hello ту же версию Python, выбранный для веб-приложения (в runtime.txt или hello **параметры приложения** колонки веб-приложения в hello портал Azure).
* Убедитесь, что параметр hello toodownload и установки пакетов.

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

Щелкните **Создать**. Это создание виртуальной среды hello и установка зависимостей, перечисленных в requirements.txt.

### <a name="create-a-superuser"></a>Создание суперпользователя
Hello базы данных, входящий в состав приложения hello не поддерживает любой суперпользователя определен. Порядок toouse hello вход функциональных возможностей приложения hello или интерфейса администратора Django hello (Если вы решите tooenable его), вам потребуется toocreate привилегированного пользователя.

Выполните это из hello командной строки из вашей папки проекта.

    env\scripts\python manage.py createsuperuser

Выполните запросы tooset hello hello-имя пользователя, пароль и т. д.

### <a name="run-using-development-server"></a>Запуск приложения на сервере разработки
Нажмите клавишу F5 toostart отладки и веб-браузере откроется автоматически toohello страница выполняется локально.

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

Можно установить точки останова в hello источников, окна контрольных значений используйте hello и т. д. . В разделе hello [средства Python для Visual Studio документации] Дополнительные сведения о hello различных функций.

### <a name="make-changes"></a>Внесение изменений
Теперь вы можете поэкспериментировать, делая источники приложения toohello изменений и/или шаблонов.

После тестирования изменений, их можно сохранить toohello репозитории:

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a>Установка дополнительных пакетов
Зависимости приложений могут не ограничиваться Python и Django.

С помощью pip можно установить дополнительные пакеты. tooinstall пакета, щелкните правой кнопкой мыши виртуальную среду hello и выберите пункт **установить пакет Python**.

Например, пакет Azure SDK для Python, который предоставляет вам доступ tooAzure хранилище, service bus и другим службам Azure ввести hello tooinstall `azure`:

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

Щелкните правой кнопкой мыши в виртуальной среде hello и выберите **создания requirements.txt** tooupdate requirements.txt.

Зафиксируйте hello изменения toorequirements.txt toohello репозитории.

### <a name="deploy-tooazure"></a>Развертывание tooAzure
Щелкните tootrigger развертывания **синхронизации** или **Push**. При синхронизации выполняется как принудительная отправка, так и применение по запросу.

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

Hello первого развертывания может потребоваться некоторое время, как он создаст в виртуальной среде, пакетов установки, и т. д.

Visual Studio не показывает ход выполнения развертывания hello hello. При желании вывода hello tooreview разделе hello на [Устранение неполадок - развертывания](#troubleshooting-deployment).

Обзор изменения tooview toohello URL-адрес Azure.

## <a name="web-app-development---windows---command-line"></a>Разработка веб-приложения — Windows — командная строка
### <a name="clone-hello-repository"></a>Клон hello репозитория
Во-первых клонирование репозитория hello, с помощью hello URL-адрес, указанный на портале Azure hello и добавьте hello Azure репозитория как удаленный. Дополнительные сведения см. в разделе [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a>Создание виртуальной среды
Мы создадим новую виртуальную среду для разработки (не добавляйте его toohello репозитория). Виртуальных сред в Python не перемещаемые, поэтому каждый разработчик приложения hello будет создавать свои собственные локально.

Убедитесь, что toouse hello ту же версию Python, выбранный для веб-приложения (в runtime.txt или hello колонку параметров приложения из веб-приложения hello портал Azure).

Для Python 2.7:

    c:\python27\python.exe -m virtualenv env

Для Python 3.4:

    c:\python34\python.exe -m venv env

Установите все внешние пакеты, необходимые для этого приложения. Можно использовать файл requirements.txt hello в корне hello tooinstall hello hello репозитория пакетов в виртуальной среде:

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a>Создание суперпользователя
Hello базы данных, входящий в состав приложения hello не поддерживает любой суперпользователя определен. Порядок toouse hello вход функциональных возможностей приложения hello или интерфейса администратора Django hello (Если вы решите tooenable его), вам потребуется toocreate привилегированного пользователя.

Выполните это из hello командной строки из вашей папки проекта.

    env\scripts\python manage.py createsuperuser

Выполните запросы tooset hello hello-имя пользователя, пароль и т. д.

### <a name="run-using-development-server"></a>Запуск приложения на сервере разработки
Приложение hello под сервером разработки можно запустить с hello следующую команду:

    env\scripts\python manage.py runserver

Hello консоли появится URL-адрес hello и прослушивает порт hello server:

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

Откройте браузер toothat URL-адрес.

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a>Внесение изменений
Теперь вы можете поэкспериментировать, делая источники приложения toohello изменений и/или шаблонов.

После тестирования изменений, их можно сохранить toohello репозитории:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Установка дополнительных пакетов
Зависимости приложений могут не ограничиваться Python и Django.

С помощью pip можно установить дополнительные пакеты. Например tooinstall hello Azure SDK для Python, которое дает вам доступ к tooAzure хранилище, service bus и другими службами Azure, тип:

    env\scripts\pip install azure

Убедитесь, что requirements.txt tooupdate:

    env\scripts\pip freeze > requirements.txt

Применить изменения hello:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>Развертывание tooAzure
tootrigger развертывание принудительной hello изменяет tooAzure:

    git push azure master

Вы увидите выходные данные hello hello скрипт развертывания, включая создание виртуальной среды, установки пакетов, создания файла конфигурации Web.config.

Обзор изменения tooview toohello URL-адрес Azure.

## <a name="web-app-development---maclinux---command-line"></a>Разработка веб-приложения — Mac/Linux — командная строка
### <a name="clone-hello-repository"></a>Клон hello репозитория
Во-первых клонирование репозитория hello, с помощью hello URL-адрес, указанный на портале Azure hello и добавьте hello Azure репозитория как удаленный. Дополнительные сведения см. в разделе [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a>Создание виртуальной среды
Мы создадим новую виртуальную среду для разработки (не добавляйте его toohello репозитория). Виртуальных сред в Python не перемещаемые, поэтому каждый разработчик приложения hello будет создавать свои собственные локально.

Убедитесь, что toouse hello ту же версию Python, выбранный для веб-приложения (в runtime.txt или hello колонку параметров приложения из веб-приложения hello портал Azure).

Для Python 2.7:

    python -m virtualenv env

Для Python 3.4:

    python -m venv env

или

    pyvenv env

Установите все внешние пакеты, необходимые для этого приложения. Можно использовать файл requirements.txt hello в корне hello tooinstall hello hello репозитория пакетов в виртуальной среде:

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a>Создание суперпользователя
Hello базы данных, входящий в состав приложения hello не поддерживает любой суперпользователя определен. Порядок toouse hello вход функциональных возможностей приложения hello или интерфейса администратора Django hello (Если вы решите tooenable его), вам потребуется toocreate привилегированного пользователя.

Выполните это из hello командной строки из вашей папки проекта.

    env/bin/python manage.py createsuperuser

Выполните запросы tooset hello hello-имя пользователя, пароль и т. д.

### <a name="run-using-development-server"></a>Запуск приложения на сервере разработки
Приложение hello под сервером разработки можно запустить с hello следующую команду:

    env/bin/python manage.py runserver

Hello консоли появится URL-адрес hello и прослушивает порт hello server:

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

Откройте браузер toothat URL-адрес.

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a>Внесение изменений
Теперь вы можете поэкспериментировать, делая источники приложения toohello изменений и/или шаблонов.

После тестирования изменений, их можно сохранить toohello репозитории:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Установка дополнительных пакетов
Зависимости приложений могут не ограничиваться Python и Django.

С помощью pip можно установить дополнительные пакеты. Например tooinstall hello Azure SDK для Python, которое дает вам доступ к tooAzure хранилище, service bus и другими службами Azure, тип:

    env/bin/pip install azure

Убедитесь, что requirements.txt tooupdate:

    env/bin/pip freeze > requirements.txt

Применить изменения hello:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>Развертывание tooAzure
tootrigger развертывание принудительной hello изменяет tooAzure:

    git push azure master

Вы увидите выходные данные hello hello скрипт развертывания, включая создание виртуальной среды, установки пакетов, создания файла конфигурации Web.config.

Обзор изменения tooview toohello URL-адрес Azure.

## <a name="troubleshooting---package-installation"></a>Устранение неполадок — установка пакета
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Устранение неполадок — виртуальная среда
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a>Устранение неполадок — статические файлы
Django имеет концепции hello сбора статических файлов. Это занимает все статические файлы hello из своих исходных расположений и копирует их в одну папку tooa. Для этого приложения, они копируются слишком`/static`.

Это делается потому, что статические файлы могут поступать из различных приложений Django. Например hello статические файлы из интерфейсов admin Django hello расположены во вложенной папке библиотеки Django в виртуальной среде hello. Статические файлы, определенные в этом приложении, находятся в папке `/app/static`. При использовании нескольких приложений Django статические файлы будут расположены в нескольких местах.

При запуске приложения hello в режиме отладки, приложение hello служит hello статические файлы из своих исходных расположений.

При запуске приложения hello в режиме выпуска, приложение hello выполняет **не** обрабатывать hello статические файлы. Он несет hello hello tooserve файлов для hello веб-сервера. Для этого приложения IIS будет обслуживать hello статические файлы из `/static`.

Коллекция Hello статических файлов выполняется как часть скрипта развертывания hello, сняв ранее собранные файлы автоматически. Это означает, что hello сборка выполняется для всех развертываний, замедляя развертывания немного, но гарантирует, что устаревшие файлы не будут доступны, как избежать является потенциальной угрозой безопасности.

Если нужно tooskip коллекцию статических файлов для приложения Django:

    \.skipDjango

Затем вам потребуется коллекции hello toodo вручную на локальном компьютере.

    env\scripts\python manage.py collectstatic

Затем удалите hello `\static` папку из `.gitignore` и добавьте его toohello репозитории.

## <a name="troubleshooting---settings"></a>Устранение неполадок — настройки
Можно изменить различные параметры для приложения hello в `DjangoWebProject/settings.py`.

Для удобства разработчиков включен режим отладки. Хорошо побочным эффектом того, является будете иметь может toosee изображения и другие статическое содержимое, если выполняется локально, без необходимости toocollect статические файлы.

режим отладки toodisable:

    DEBUG = False

При отключении отладки hello значение `ALLOWED_HOSTS` toobe потребностей обновить имя Azure узла tooinclude hello. Например:

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

или tooenable любой:

    ALLOWED_HOSTS = (
        '*',
    )

На практике можно toodo что-нибудь более сложные toodeal с переключением между, отладки и выпуска режим и получение имени узла hello.

Можно задать переменные среды через портал Azure hello **Настройка** страницы в hello **параметры приложения** раздела.  Это может быть полезно для задания значений, что может потребоваться не tooappear в источниках hello (строки подключения, пароли, и т. д.), или что tooset по-разному между Azure и локальном компьютере. В `settings.py`, можно запросить с помощью переменных среды hello `os.getenv`.

## <a name="using-a-database"></a>Использование базы данных
Hello базы данных, которая входит в состав приложения hello является базой данных sqlite. Это toouse базы данных по умолчанию удобный и полезно для разработки, поскольку оно требует практически никакой дополнительной настройки. Hello база данных хранится в файле db.sqlite3 hello в папке проекта hello.

Azure предоставляет базы данных служб, которые являются просто toouse из Django приложения. Учебники по использованию [базы данных SQL] и [MySQL] из приложения Django Показать шаги hello необходимые toocreate hello базы данных службы, измените параметры базы данных hello в `DjangoWebProject/settings.py`и hello tooinstall необходимые библиотеки.

Конечно Если вы предпочитаете toomanage серверах баз данных, можно сделать с помощью Windows или Linux виртуальных машин, работающих в Azure.

## <a name="django-admin-interface"></a>Интерфейс администрирования Django
После начала построения моделей, будет необходимо toopopulate hello базы данных некоторые данными. Простой способ toodo Добавление и изменение содержимого в интерактивном режиме — toouse hello Django администрирования интерфейс.

Код Hello для интерфейса администрирования hello закомментированы в источниках приложения hello, но он помечается, его можно легко включить (поиск «admin»).

После включения синхронизации базы данных hello, запустите приложение hello и перехода слишком`/admin`.

## <a name="next-steps"></a>Дальнейшие действия
Выполните эти ссылки toolearn Дополнительные сведения о Django и инструменты Python для Visual Studio.

* [Документация по Django]
* [средства Python для Visual Studio документации]

Дополнительную информацию об использовании базы данных SQL и MySQL см. в статьях:

* [Использование Django и MySQL в Azure с помощью инструментов Python для Visual Studio]
* [Использование Django и базы данных SQL в Azure с помощью инструментов Python для Visual Studio]

Дополнительные сведения см. в разделе hello [центре разработчиков Python](/develop/python/).

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Использование Django и MySQL в Azure с помощью инструментов Python для Visual Studio]: web-sites-python-ptvs-django-mysql.md
[Использование Django и базы данных SQL в Azure с помощью инструментов Python для Visual Studio]: web-sites-python-ptvs-django-sql.md
[базы данных SQL]: web-sites-python-ptvs-django-sql.md
[MySQL]: web-sites-python-ptvs-django-mysql.md

<!--External Link references-->
[пакет SDK для Azure для Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[пакет SDK для Azure для Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git для Windows]: http://msysgit.github.io/
[GitHub для Windows]: https://windows.github.com/
[средствами Python для Visual Studio]: http://aka.ms/ptvs
[инструменты Python 2.2 для Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[средства Python для Visual Studio документации]: http://aka.ms/ptvsdocs
[Документация по Django]: https://www.djangoproject.com/
