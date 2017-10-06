---
title: "aaaCreating веб-приложений с термосе в Azure"
description: "Учебник, в котором представлены toorunning Python веб-приложения в Azure."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: b7f4ca3a-0b52-4108-90a7-f7e07ac73da0
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/20/2016
ms.author: huvalo
ms.openlocfilehash: 3362047b3106b4380b5971e47cbd8042d38a792b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a>Создание веб-приложений с помощью Flask в Azure
В данном учебнике как tooget была запущена Python в [веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).  Служба веб-приложений предоставляет ограниченное бесплатное размещение приложений, а также возможности их быстрого развертывания и использования языка Python.  Здравствуйте, по мере роста приложения, можно переключить toopaid размещение и также можно интегрировать со всеми другими службами Azure.

Вы создадите приложения с помощью веб-платформа термосе hello (см. другие версии этого учебника, чтобы [Django](web-sites-python-create-deploy-django-app.md) и [Bottle](web-sites-python-create-deploy-bottle-app.md)).  Будет создать веб-сайт hello из коллекции Azure hello, Настройка развертывания Git и клонировать репозиторий hello локально.  Затем можно будет запустить приложение hello локально, внести изменения, зафиксируйте и отправьте их tooAzure.  Здравствуйте учебника показано, как toodo это в Windows или Mac и Linux.

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
Если у вас еще не установлен Python 2.7 или 3.4 (32-разрядная версия), рекомендуется сначала установить [пакет SDK для Azure для Python 2.7] или [пакет SDK для Azure для Python 3.4] с помощью установщика веб-платформы.  При этом устанавливаются hello 32-разрядной версии Python дублирует, pip, virtualenv, (32-разрядных Python —, установленных на компьютерах hello Azure узлов) и т. д.  Python также можно скачать с веб-сайта [python.org].

Для Git рекомендуется использовать [Git для Windows] или [GitHub для Windows].  При использовании Visual Studio, можно использовать поддержку hello интеграции Git.

Мы также рекомендуем установить [инструменты Python 2.2 для Visual Studio].  Это не обязательно, но если у вас [Visual Studio], включая hello освободить Visual Studio Community 2013 или Visual Studio Express 2013 для Web, а затем это даст значительные среду IDE Python.

### <a name="maclinux"></a>Mac/Linux
У вас должны быть установлены Python и Git. Убедитесь, что у вас установлена версия Python 2.7 или 3.4.

## <a name="web-app-create-on-hello-azure-portal"></a>Создание веб-приложения на портале Azure hello
Hello первым шагом при создании приложения является toocreate hello веб-приложения через hello [портала Azure](https://portal.azure.com). 

1. Войдите на портал Azure hello и щелкните hello **NEW** кнопки в левом нижнем углу hello. 
2. Щелкните **Интернет + мобильные устройства**.
3. В поле поиска hello введите «python».
4. В результатах поиска hello, выберите **термосе**, нажмите кнопку **создать**.
5. Настройте приложение новый термосе hello, таких как создание нового плана служб приложений и новую группу ресурсов для него. Затем щелкните **Создать**.
6. Настроить публикацию Git для только что созданный веб-приложения в соответствии с инструкциями hello в [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).

## <a name="application-overview"></a>Обзор приложений
### <a name="git-repository-contents"></a>Содержимое репозитория Git
Ниже приведен обзор hello файлов, которые можно найти в hello исходный репозиторий Git, который мы будем клонировать в следующем разделе hello.

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

Основными источниками для приложения hello.  Состоит из 3 страниц (index, about, contact) с макетом главной страницы.  Использует такое статическое содержимое и сценарии, как bootstrap, jquery, modernizr и respond.

    \runserver.py

Поддержка локального сервера разработки. Используйте это приложение hello toorun локально.

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

Файлы проекта для использования со [средствами Python для Visual Studio].

    \ptvs_virtualenv_proxy.py

Прокси-сервер IIS для виртуальных сред и поддержки удаленной отладки PTVS.

    \requirements.txt

Внешние пакеты, необходимые для этого приложения. скрипт развертывания Hello будет pip hello пакетов установки, перечисленные в этом файле.

    \web.2.7.config
    \web.3.4.config

Файлы конфигурации IIS.  скрипт развертывания Hello будет использовать соответствующий web.x.y.config hello и скопируйте его в файле web.config.

### <a name="optional-files---customizing-deployment"></a>Дополнительные файлы — настройка развертывания
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>Дополнительные файлы — среда выполнения Python
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>Дополнительные файлы на сервере
Некоторые файлы на сервере hello существует, но не добавляются toohello репозитории.  Эти отчеты создаются с hello сценария развертывания.

    \web.config

Файл конфигурации IIS.  Создается из файла web.x.y.config при каждом развертывании.

    \env\

Виртуальная среда Python.  Если совместимые виртуальная среда уже не существует в приложение hello, созданные во время развертывания.  Пакеты, перечисленные в requirements.txt являются pip установлен, но pip пропустит установки, если hello пакеты уже установлены.

Hello следующие 3 рассматриваются как tooproceed с hello веб-разработки приложений в разделе 3 различных сред:

* Windows, со средствами Python для Visual Studio
* Windows с командной строкой;
* Mac и Linux с командной строкой.

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Развертывание веб-приложений — Windows — средства Python для Visual Studio
### <a name="clone-hello-repository"></a>Клон hello репозитория
Во-первых клонирование репозитория hello, с помощью hello URL-адрес, указанный на портале Azure hello. Дополнительные сведения см. в разделе [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).

Привет открыть файл решения (SLN-файл), включенный в корне репозитория hello hello.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a>Создание виртуальной среды
Теперь мы создадим виртуальную среду для локальной разработки веб-сайта.  Щелкните правой кнопкой мыши **Python Environments** (Среды Python) и выберите **Add Virtual Environment...** (Добавить виртуальную среду...).

* Убедитесь, что имя hello среды hello `env`.
* Выберите базовый интерпретатор hello.  Убедитесь, что toouse hello ту же версию Python, выбранный для веб-приложения (в runtime.txt или hello **параметры приложения** колонки веб-приложения в hello портал Azure).
* Убедитесь, что параметр hello toodownload и установки пакетов.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

Щелкните **Создать**.  Это создание виртуальной среды hello и установка зависимостей, перечисленных в requirements.txt.

### <a name="run-using-development-server"></a>Запуск приложения на сервере разработки
Нажмите клавишу F5 toostart отладки и веб-браузере откроется автоматически toohello страница выполняется локально.

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

Можно установить точки останова в hello источников, окна контрольных значений используйте hello и т. д.  . В разделе hello [средства Python для Visual Studio документации] Дополнительные сведения о hello различных функций.

### <a name="make-changes"></a>Внесение изменений
Теперь вы можете поэкспериментировать, делая источники приложения toohello изменений и/или шаблонов.

После тестирования изменений, их можно сохранить toohello репозитории:

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a>Установка дополнительных пакетов
Зависимости приложений могут не ограничиваться Python и Flask.

С помощью pip можно установить дополнительные пакеты.  tooinstall пакета, щелкните правой кнопкой мыши виртуальную среду hello и выберите пункт **установить пакет Python**.

Например, пакет Azure SDK для Python, который предоставляет вам доступ tooAzure хранилище, service bus и другим службам Azure ввести hello tooinstall `azure`:

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

Щелкните правой кнопкой мыши в виртуальной среде hello и выберите **создания requirements.txt** tooupdate requirements.txt.

Зафиксируйте hello изменения toorequirements.txt toohello репозитории.

### <a name="deploy-tooazure"></a>Развертывание tooAzure
Щелкните tootrigger развертывания **синхронизации** или **Push**.  При синхронизации выполняется как принудительная отправка, так и применение по запросу.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

Hello первого развертывания может потребоваться некоторое время, как он создаст в виртуальной среде, пакетов установки, и т. д.

Visual Studio не показывает ход выполнения развертывания hello hello.  При желании вывода hello tooreview разделе hello на [Устранение неполадок - развертывания](#troubleshooting-deployment).

Обзор изменения tooview toohello URL-адрес Azure.

## <a name="web-app-development---windows---command-line"></a>Разработка веб-приложения — Windows — командная строка
### <a name="clone-hello-repository"></a>Клон hello репозитория
Во-первых клонирование репозитория hello, с помощью hello URL-адрес, указанный на портале Azure hello и добавьте hello Azure репозитория как удаленный. Дополнительные сведения см. в разделе [tooAzure локальное развертывание Git службы приложений](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Создание виртуальной среды
Мы создадим новую виртуальную среду для разработки (не добавляйте его toohello репозитория).  Виртуальных сред в Python не перемещаемые, поэтому каждый разработчик приложения hello будет создавать свои собственные локально.

Убедитесь, что toouse hello ту же версию Python, выбранный для веб-приложения (в runtime.txt или hello **параметры приложения** колонки веб-приложения в hello портал Azure).

Для Python 2.7:

    c:\python27\python.exe -m virtualenv env

Для Python 3.4:

    c:\python34\python.exe -m venv env

Установите все внешние пакеты, необходимые для этого приложения. Можно использовать файл requirements.txt hello в корне hello tooinstall hello hello репозитория пакетов в виртуальной среде:

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a>Запуск приложения на сервере разработки
Приложение hello под сервером разработки можно запустить с hello следующую команду:

    env\scripts\python runserver.py

Hello консоли появится URL-адрес hello и прослушивает порт hello server:

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

Откройте браузер toothat URL-адрес.

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a>Внесение изменений
Теперь вы можете поэкспериментировать, делая источники приложения toohello изменений и/или шаблонов.

После тестирования изменений, их можно сохранить toohello репозитории:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Установка дополнительных пакетов
Зависимости приложений могут не ограничиваться Python и Flask.

С помощью pip можно установить дополнительные пакеты.  Например tooinstall hello Azure SDK для Python, которое дает вам доступ к tooAzure хранилище, service bus и другими службами Azure, тип:

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
Мы создадим новую виртуальную среду для разработки (не добавляйте его toohello репозитория).  Виртуальных сред в Python не перемещаемые, поэтому каждый разработчик приложения hello будет создавать свои собственные локально.

Убедитесь, что toouse hello ту же версию Python, выбранный для веб-приложения (в runtime.txt или hello **параметры приложения** колонки веб-приложения в hello портал Azure).

Для Python 2.7:

    python -m virtualenv env

Для Python 3.4:

    python -m venv env
или pyvenv env

Установите все внешние пакеты, необходимые для этого приложения. Можно использовать файл requirements.txt hello в корне hello tooinstall hello hello репозитория пакетов в виртуальной среде:

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a>Запуск приложения на сервере разработки
Приложение hello под сервером разработки можно запустить с hello следующую команду:

    env/bin/python runserver.py

Hello консоли появится URL-адрес hello и прослушивает порт hello server:

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

Откройте браузер toothat URL-адрес.

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a>Внесение изменений
Теперь вы можете поэкспериментировать, делая источники приложения toohello изменений и/или шаблонов.

После тестирования изменений, их можно сохранить toohello репозитории:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Установка дополнительных пакетов
Зависимости приложений могут не ограничиваться Python и Flask.

С помощью pip можно установить дополнительные пакеты.  Например tooinstall hello Azure SDK для Python, которое дает вам доступ к tooAzure хранилище, service bus и другими службами Azure, тип:

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

## <a name="next-steps"></a>Дальнейшие действия
Выполните эти ссылки toolearn Дополнительные сведения о термосе и инструменты Python для Visual Studio. 

* [Документация по Flask]
* [средства Python для Visual Studio документации]

Дополнительную информацию об использовании табличного хранилища Azure и MongoDB см. в следующих статьях:

* [Использование Flask и MongoDB в Azure с помощью инструментов Python для Visual Studio]
* [Flask и хранилище таблиц Azure с использованием инструментов Python Tools для Visual Studio]

Дополнительные сведения см. также: hello [центре разработчиков Python](/develop/python/).

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Использование Flask и MongoDB в Azure с помощью инструментов Python для Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure
[Flask и хранилище таблиц Azure с использованием инструментов Python Tools для Visual Studio]: web-sites-python-ptvs-flask-table-storage.md

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
[Документация по Flask]: http://flask.pocoo.org/ 

