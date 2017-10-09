---
title: "aaaDjango и базы данных SQL в Azure с помощью средства Python 2.2 для Visual Studio"
description: "Узнайте, как toouse hello средства Python для Visual Studio toocreate Django веб-приложения, который сохраняет данные в экземпляр базы данных SQL и развернуть ее tooAzure приложения службы веб-приложений."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a>Использование Django и базы данных SQL в Azure с помощью инструментов Python 2.2 для Visual Studio
В этом учебнике мы будем использовать [средства Python для Visual Studio] toocreate простой опрашивает веб-приложения с помощью одного из шаблонов образец hello PTVS. Также доступна [видеоверсия](https://www.youtube.com/watch?v=ZwcoGcIeHF4)этого учебника.

Мы рассмотрим, как toouse базы данных SQL размещена в Azure, как tooconfigure hello web app toouse базы данных SQL, а также как toopublish hello веб-приложения слишком[веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

В разделе hello [центре разработчиков Python] Дополнительные статьи, посвященные разработки Azure приложение службы веб-приложений с помощью бутылка PTVS, термосе и Django веб-платформы с помощью службы хранилища Azure таблицы, MySQL и базы данных SQL. Хотя данная статья посвящена службы приложений, hello шаги похожи, при разработке [облачных служб Azure].

## <a name="prerequisites"></a>Предварительные требования
* Visual Studio 2015
* [Python 2.7 (32-разрядная версия).]
* [Инструменты Python 2.2 для Visual Studio]
* [средства Python 2.2 для Visual Studio образцы VSIX]
* [Инструменты пакета SDK для Azure для Visual Studio 2015]
* Django 1.9 или более поздней версии.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
>
>

## <a name="create-hello-project"></a>Создание проекта hello
В этом разделе мы создадим проект Visual Studio с помощью шаблона. Мы создадим виртуальную среду и установим необходимые пакеты. Мы создадим локальную базу данных с помощью sqlite. Затем мы выполним hello веб-приложения локально.

1. В Visual Studio выберите последовательно **Файл** и **Создать проект**.
2. Здравствуйте, шаблоны проектов из hello [средства Python 2.2 для Visual Studio образцы VSIX] можно найти в разделе **Python**, **образцы**. Выберите **опрашивает Django веб-проекта** и нажмите кнопку ОК toocreate hello проекта.

     ![Диалоговое окно "Новый проект"](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. Появится запрос tooinstall внешние пакеты. Выберите вариант **Установить в виртуальной среде**.

     ![Диалоговое окно «Внешние пакеты»](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. Выберите **Python 2.7** базовый интерпретатора hello.

     ![Диалоговое окно «Добавление виртуальной среды»](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. В **обозревателе решений**, правой кнопкой мыши узел проекта hello и выберите **Python**и выберите **Django перенести**.  Выберите **Django Create Superuser**(Создать суперпользователя Django).
6. Это будет открыть консоль управления Django и создать базу данных sqlite в папке проекта hello. Выполните запросы hello toocreate пользователя.
7. Убедитесь, что приложение hello работает, нажав клавишу <kbd>F5</kbd>.
8. Нажмите кнопку **входа** hello панели навигации в верхней hello.

     ![Веб-браузер](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. Введите учетные данные hello hello пользователя, созданный при синхронизации базы данных hello.

     ![Веб-браузер](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. Щелкните **Создать примеры опросов**.

      ![Веб-браузер](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. Выберите опрос и проголосуйте.

      ![Веб-браузер](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a>Создание базы данных SQL
Для базы данных hello мы создадим базы данных Azure SQL.

Выполнив следующие шаги, вы создадите базу данных.

1. Войти в hello [портала Azure].
2. Hello нижней части панели навигации hello, нажмите кнопку **NEW**. Выберите **Данные+хранилище** > **База данных SQL**.
3. Настройка hello новой базы данных SQL путем создания новой группы ресурсов и выберите hello соответствующее место для него.
4. После создания базы данных SQL hello щелкните **в среде Visual Studio** в колонке базы данных hello.
5. Щелкните **Настроить брандмауэр**.
6. В hello **параметры брандмауэра** колонки, добавьте правило брандмауэра с **НАЧАЛЬНЫЙ IP-** и **конечным IP** задать toohello общедоступный IP-адрес компьютера разработчика. Щелкните **Сохранить**.

   Это позволит серверу базы данных toohello соединения с компьютера разработки.
7. В колонке базы данных hello, нажмите кнопку **свойства**, нажмите кнопку **Показать строки подключения базы данных**.
8. Используйте hello копирования кнопки tooput hello значение **ADO.NET** hello буфер обмена.

## <a name="configure-hello-project"></a>Настройка проекта hello
В этом разделе мы настроим наш веб-приложения toouse hello SQL база данных только что созданный. Также будут установлены дополнительные Python пакетов требуется toouse баз данных SQL с Django. Затем мы выполним hello веб-приложения локально.

1. В Visual Studio откройте **settings.py**, из hello *ProjectName* папки. Временно вставьте строку подключения hello в редакторе hello. указана строка подключения Hello в следующем формате:

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

Изменить определение hello `DATABASES` toouse hello значений, приведенных выше.

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. В обозревателе решений в разделе **среды Python**, щелкните правой кнопкой мыши в виртуальной среде hello и выберите **установить пакет Python**.
2. Установить пакет hello `pyodbc` с помощью **pip**.

     ![Диалоговое окно «Установка пакета Python»](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. Установить пакет hello `django-pyodbc-azure` с помощью **pip**.

     ![Диалоговое окно «Установка пакета Python»](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. В **обозревателе решений**, правой кнопкой мыши узел проекта hello и выберите **Python**и выберите **Django перенести**.  Выберите **Django Create Superuser**(Создать суперпользователя Django).

   Это создаст hello таблиц для базы данных SQL hello, созданной в предыдущем разделе hello. Выполните запросы hello toocreate пользователя, который не имеет toomatch hello пользователя в базе данных sqlite hello, созданные в первом разделе hello.
5. Запустите приложение hello с `F5`. Опросы, созданных с помощью **создать образец опрашивает** и hello данные, переданные с правом голоса сериализуются в базе данных SQL hello.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Публикация hello web app tooAzure службы приложений
Hello Azure .NET SDK предоставляет легко toodeploy вашей web tooAzure приложения web веб-приложений служб приложений.

1. В **обозревателе решений**, правой кнопкой мыши узел проекта hello и выберите **публикации**.

     ![Диалоговое окно «Публикация веб-сайта»](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. Щелкните **Веб-приложения Microsoft Azure**.
3. Щелкните **New** toocreate новое веб-приложение.
4. Заполните следующие поля hello и нажмите кнопку **создать**.

   * **Имя веб-приложения**
   * **План обслуживания приложения**
   * **Группа ресурсов**
   * **Регион**
   * Оставить **сервера базы данных** значение слишком**ни одной базы данных**
5. Примите значения по умолчанию и щелкните **Опубликовать**.
6. Веб-браузере откроется автоматически toohello опубликованных веб-приложения. Вы увидите рабочее приложение hello web, как и ожидалось, с помощью hello **SQL** базы данных, размещенной в Azure.

   Поздравляем!

     ![Веб-браузер](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a>Дальнейшие действия
Выполните эти ссылки toolearn Дополнительные сведения о средствах Python для Visual Studio, Django и базы данных SQL.

* [Документация по средствам Python для Visual Studio]
  * [Веб-проекты]
  * [Проекты для облачной службы]
  * [Удаленная отладка в Microsoft Azure]
* [Документация по Django]
* [База данных SQL]

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[центре разработчиков Python]: /develop/python/
[облачных служб Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[портала Azure]: https://portal.azure.com
[средства Python для Visual Studio]: http://aka.ms/ptvs
[Инструменты Python 2.2 для Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[средства Python 2.2 для Visual Studio образцы VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Инструменты пакета SDK для Azure для Visual Studio 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 (32-разрядная версия).]: http://go.microsoft.com/fwlink/?LinkId=517190
[Документация по средствам Python для Visual Studio]: http://aka.ms/ptvsdocs
[Удаленная отладка в Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Веб-проекты]: http://go.microsoft.com/fwlink/?LinkId=624027
[Проекты для облачной службы]: http://go.microsoft.com/fwlink/?LinkId=624028
[Документация по Django]: https://www.djangoproject.com/
[База данных SQL]: /documentation/services/sql-database/
