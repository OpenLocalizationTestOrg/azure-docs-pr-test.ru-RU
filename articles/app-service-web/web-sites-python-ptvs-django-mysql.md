---
title: "aaaDjango и MySQL в Azure с помощью средства Python 2.2 для Visual Studio"
description: "Узнайте, как toouse hello средства Python для Visual Studio toocreate Django веб-приложения, который хранит данные в экземпляре базы данных MySQL и развернуть ее tooAzure приложения службы веб-приложений."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a>Использование Django и MySQL в Azure с помощью инструментов Python 2.2 для Visual Studio
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

В этом учебнике мы используем [средства Python для Visual Studio](https://www.visualstudio.com/vs/python) toocreate простой опрашивает веб-приложения с помощью одного из шаблонов образец hello PTVS. Вы узнаете, как toouse MySQL служба размещена в Azure, как tooconfigure hello web app toouse MySQL и как toopublish hello веб-приложения слишком[веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

> [!NOTE]
> Hello сведения, содержащиеся в этом учебнике также доступен в hello следующие видео:
> 
> [PTVS 2.1: Django app with MySQL][video] (PTVS 2.1: приложение Django с использованием MySQL).
> 
> 

В разделе hello [центре разработчиков Python] Дополнительные статьи, посвященные разработки Azure приложение службы веб-приложений с помощью бутылка PTVS, термосе и Django веб-платформы с помощью службы хранилища Azure таблицы, MySQL и базы данных SQL. Хотя данная статья посвящена службы приложений, hello шаги похожи, при разработке [облачных служб Azure].

## <a name="prerequisites"></a>Предварительные требования
* Visual Studio 2015
* [Python 2.7 (32-разрядная версия)] или [Python 3.4 (32-разрядная версия)]
* [Инструменты Python 2.2 для Visual Studio]
* [средства Python 2.2 для Visual Studio образцы VSIX]
* [Инструменты пакета SDK для Azure для Visual Studio 2015]
* Django 1.9 или более поздней версии.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Не требуется никаких кредитных карт и обязательств.
> 
> 

## <a name="create-hello-project"></a>Создание проекта hello
В этом разделе мы создадим проект Visual Studio с помощью шаблона. Мы создадим виртуальную среду и установим необходимые пакеты. Мы создадим также локальную базу данных с помощью sqlite. Затем вы будете запускать приложение hello локально.

1. В Visual Studio выберите последовательно **Файл** и **Создать проект**.
2. Здравствуйте, шаблоны проектов из hello [средства Python 2.2 для Visual Studio образцы VSIX] можно найти в разделе **Python**, **образцы**. Выберите **опрашивает Django веб-проекта** и нажмите кнопку ОК toocreate hello проекта.
   
    ![Диалоговое окно "Новый проект"](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. Появится запрос tooinstall внешние пакеты. Выберите вариант **Установить в виртуальной среде**.
   
    ![Диалоговое окно «Внешние пакеты»](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. Выберите **Python 2.7** или **Python 3.4** базовый интерпретатора hello.
   
    ![Диалоговое окно «Добавление виртуальной среды»](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. В **обозревателе решений**, правой кнопкой мыши узел проекта hello и выберите **Python**и выберите **Django перенести**.  Выберите **Django Create Superuser**(Создать суперпользователя Django).
6. Это будет открыть консоль управления Django и создать базу данных sqlite в папке проекта hello. Выполните запросы hello toocreate пользователя.
7. Убедитесь, что приложение hello работает, нажав клавишу `F5`.
8. Нажмите кнопку **входа** hello панели навигации в верхней hello.
   
    ![Панель навигации Django](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. Введите учетные данные hello hello пользователя, созданный при синхронизации базы данных hello.
   
    ![Форма входа](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. Щелкните **Создать примеры опросов**.
    
     ![Создать примеры опросов](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. Выберите опрос и проголосуйте.
    
     ![Голосование в примерах опросов](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a>Создание базы данных MySQL
Для базы данных hello вы создадите базы данных ClearDB MySQL размещенной в Azure.

В качестве альтернативного решения вы можете создать свою собственную виртуальную машину в Azure, а затем установить и настроить MySQL самостоятельно.

Выполнив следующие шаги, вы сможете создать бесплатную базу данных.

1. Войдите в toohello [портала Azure].
2. Hello верхней части панели навигации hello, нажмите кнопку **NEW**, нажмите кнопку **данные + хранилище**, а затем нажмите кнопку **базы данных MySQL**.
3. Настройте новую базу данных MySQL hello, создав новую группу ресурсов и выберите hello соответствующее место для него.
4. После создания базы данных MySQL hello щелкните **свойства** в колонке базы данных hello.
5. Используйте hello копирования кнопки tooput hello значение **строка подключения** hello буфер обмена.

## <a name="configure-hello-project"></a>Настройка проекта hello
В этом разделе вы настроите наш веб-приложения toouse hello MySQL база данных только что созданный. Вы также установите дополнительные Python пакетов требуется toouse базы данных MySQL с Django. Затем вы будете запускать веб-приложения hello локально.

1. В Visual Studio откройте **settings.py**, из hello *ProjectName* папки. Временно вставьте строку подключения hello в редакторе hello. указана строка подключения Hello в следующем формате:
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    Изменить базу данных по умолчанию hello **ЯДРА** toouse MySQL, а также установите hello значения для **имя**, **пользователя**, **пароль** и  **УЗЕЛ** из hello **CONNECTIONSTRING**.
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. В обозревателе решений в разделе **среды Python**, щелкните правой кнопкой мыши в виртуальной среде hello и выберите **установить пакет Python**.
3. Установить пакет hello `mysqlclient` с помощью **pip**.
   
    ![Диалоговое окно «Установка пакета»](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. В **обозревателе решений**, правой кнопкой мыши узел проекта hello и выберите **Python**и выберите **Django перенести**.  Выберите **Django Create Superuser**(Создать суперпользователя Django).
   
    Это создаст hello таблиц для базы данных MySQL hello, созданный в предыдущем разделе hello. Выполните toocreate hello запросы пользователя, который не имеет toomatch hello пользователя в базе данных sqlite hello, созданные в hello первом разделе этой статьи.
5. Запустите приложение hello с `F5`. Опросы, созданных с помощью **создать образец опрашивает** и hello данные, переданные с правом голоса сериализуются в базе данных MySQL hello.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Публикация hello web app tooAzure службы приложений
Hello Azure .NET SDK предоставляет простой способ toodeploy вашей web app tooAzure службы приложений.

1. В **обозревателе решений**, правой кнопкой мыши узел проекта hello и выберите **публикации**.
   
    ![Диалоговое окно «Публикация веб-сайта»](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. Щелкните **Служба приложений Microsoft Azure**.
3. Щелкните **New** toocreate новое веб-приложение.
4. Заполните следующие поля hello и нажмите кнопку **создать**:
   
   * **Имя веб-приложения**
   * **План обслуживания приложения**
   * **Группа ресурсов**
   * **Регион**
   * Оставить **сервера базы данных** значение слишком**ни одной базы данных**
5. Примите значения по умолчанию и щелкните **Опубликовать**.
6. Веб-браузере откроется автоматически toohello опубликованных веб-приложения. Вы увидите рабочее приложение hello web, как и ожидалось, с помощью hello **MySQL** базы данных, размещенной в Azure.
   
    ![Веб-браузер](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    Поздравляем! Вы успешно опубликовали вашей tooAzure MySQL веб-приложения.

## <a name="next-steps"></a>Дальнейшие действия
Выполните эти ссылки toolearn Дополнительные сведения о средствах Python для Visual Studio, Django и MySQL.

* [Документация по средствам Python для Visual Studio]
  * [Веб-проекты]
  * [Проекты для облачной службы]
  * [Удаленная отладка в Microsoft Azure]
* [Документация по Django]
* [MySQL]

Дополнительные сведения см. в разделе hello [центре разработчиков Python](/develop/python/).

<!--Link references-->

[центре разработчиков Python]: /develop/python/
[облачных служб Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[портала Azure]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Инструменты Python 2.2 для Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[средства Python 2.2 для Visual Studio образцы VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Инструменты пакета SDK для Azure для Visual Studio 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 (32-разрядная версия)]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 (32-разрядная версия)]: http://go.microsoft.com/fwlink/?LinkId=517191
[Документация по средствам Python для Visual Studio]: http://aka.ms/ptvsdocs
[Удаленная отладка в Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Веб-проекты]: http://go.microsoft.com/fwlink/?LinkId=624027
[Проекты для облачной службы]: http://go.microsoft.com/fwlink/?LinkId=624028
[Документация по Django]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
