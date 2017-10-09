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
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="b54db-103">Использование Django и базы данных SQL в Azure с помощью инструментов Python 2.2 для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b54db-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="b54db-104">В этом учебнике мы будем использовать [средства Python для Visual Studio] toocreate простой опрашивает веб-приложения с помощью одного из шаблонов образец hello PTVS.</span><span class="sxs-lookup"><span data-stu-id="b54db-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="b54db-105">Также доступна [видеоверсия](https://www.youtube.com/watch?v=ZwcoGcIeHF4)этого учебника.</span><span class="sxs-lookup"><span data-stu-id="b54db-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="b54db-106">Мы рассмотрим, как toouse базы данных SQL размещена в Azure, как tooconfigure hello web app toouse базы данных SQL, а также как toopublish hello веб-приложения слишком[веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="b54db-106">We'll learn how toouse a SQL database hosted on Azure, how tooconfigure hello web app toouse a SQL database, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="b54db-107">В разделе hello [центре разработчиков Python] Дополнительные статьи, посвященные разработки Azure приложение службы веб-приложений с помощью бутылка PTVS, термосе и Django веб-платформы с помощью службы хранилища Azure таблицы, MySQL и базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="b54db-107">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="b54db-108">Хотя данная статья посвящена службы приложений, hello шаги похожи, при разработке [облачных служб Azure].</span><span class="sxs-lookup"><span data-stu-id="b54db-108">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b54db-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b54db-109">Prerequisites</span></span>
* <span data-ttu-id="b54db-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="b54db-110">Visual Studio 2015</span></span>
* <span data-ttu-id="b54db-111">[Python 2.7 (32-разрядная версия).]</span><span class="sxs-lookup"><span data-stu-id="b54db-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="b54db-112">[Инструменты Python 2.2 для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="b54db-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="b54db-113">[средства Python 2.2 для Visual Studio образцы VSIX]</span><span class="sxs-lookup"><span data-stu-id="b54db-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="b54db-114">[Инструменты пакета SDK для Azure для Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="b54db-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="b54db-115">Django 1.9 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b54db-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="b54db-116">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="b54db-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b54db-117">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="b54db-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-hello-project"></a><span data-ttu-id="b54db-118">Создание проекта hello</span><span class="sxs-lookup"><span data-stu-id="b54db-118">Create hello Project</span></span>
<span data-ttu-id="b54db-119">В этом разделе мы создадим проект Visual Studio с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="b54db-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="b54db-120">Мы создадим виртуальную среду и установим необходимые пакеты.</span><span class="sxs-lookup"><span data-stu-id="b54db-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="b54db-121">Мы создадим локальную базу данных с помощью sqlite.</span><span class="sxs-lookup"><span data-stu-id="b54db-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="b54db-122">Затем мы выполним hello веб-приложения локально.</span><span class="sxs-lookup"><span data-stu-id="b54db-122">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="b54db-123">В Visual Studio выберите последовательно **Файл** и **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="b54db-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="b54db-124">Здравствуйте, шаблоны проектов из hello [средства Python 2.2 для Visual Studio образцы VSIX] можно найти в разделе **Python**, **образцы**.</span><span class="sxs-lookup"><span data-stu-id="b54db-124">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="b54db-125">Выберите **опрашивает Django веб-проекта** и нажмите кнопку ОК toocreate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="b54db-125">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>

     ![Диалоговое окно "Новый проект"](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="b54db-127">Появится запрос tooinstall внешние пакеты.</span><span class="sxs-lookup"><span data-stu-id="b54db-127">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="b54db-128">Выберите вариант **Установить в виртуальной среде**.</span><span class="sxs-lookup"><span data-stu-id="b54db-128">Select **Install into a virtual environment**.</span></span>

     ![Диалоговое окно «Внешние пакеты»](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="b54db-130">Выберите **Python 2.7** базовый интерпретатора hello.</span><span class="sxs-lookup"><span data-stu-id="b54db-130">Select **Python 2.7** as hello base interpreter.</span></span>

     ![Диалоговое окно «Добавление виртуальной среды»](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="b54db-132">В **обозревателе решений**, правой кнопкой мыши узел проекта hello и выберите **Python**и выберите **Django перенести**.</span><span class="sxs-lookup"><span data-stu-id="b54db-132">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="b54db-133">Выберите **Django Create Superuser**(Создать суперпользователя Django).</span><span class="sxs-lookup"><span data-stu-id="b54db-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="b54db-134">Это будет открыть консоль управления Django и создать базу данных sqlite в папке проекта hello.</span><span class="sxs-lookup"><span data-stu-id="b54db-134">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="b54db-135">Выполните запросы hello toocreate пользователя.</span><span class="sxs-lookup"><span data-stu-id="b54db-135">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="b54db-136">Убедитесь, что приложение hello работает, нажав клавишу <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="b54db-136">Confirm that hello application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="b54db-137">Нажмите кнопку **входа** hello панели навигации в верхней hello.</span><span class="sxs-lookup"><span data-stu-id="b54db-137">Click **Log in** from hello navigation bar at hello top.</span></span>

     ![Веб-браузер](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="b54db-139">Введите учетные данные hello hello пользователя, созданный при синхронизации базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="b54db-139">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>

     ![Веб-браузер](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="b54db-141">Щелкните **Создать примеры опросов**.</span><span class="sxs-lookup"><span data-stu-id="b54db-141">Click **Create Sample Polls**.</span></span>

      ![Веб-браузер](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="b54db-143">Выберите опрос и проголосуйте.</span><span class="sxs-lookup"><span data-stu-id="b54db-143">Click on a poll and vote.</span></span>

      ![Веб-браузер](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="b54db-145">Создание базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="b54db-145">Create a SQL Database</span></span>
<span data-ttu-id="b54db-146">Для базы данных hello мы создадим базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="b54db-146">For hello database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="b54db-147">Выполнив следующие шаги, вы создадите базу данных.</span><span class="sxs-lookup"><span data-stu-id="b54db-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="b54db-148">Войти в hello [портала Azure].</span><span class="sxs-lookup"><span data-stu-id="b54db-148">Log into hello [Azure Portal].</span></span>
2. <span data-ttu-id="b54db-149">Hello нижней части панели навигации hello, нажмите кнопку **NEW**.</span><span class="sxs-lookup"><span data-stu-id="b54db-149">At hello bottom of hello navigation pane, click **NEW**.</span></span> <span data-ttu-id="b54db-150">Выберите **Данные+хранилище** > **База данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="b54db-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="b54db-151">Настройка hello новой базы данных SQL путем создания новой группы ресурсов и выберите hello соответствующее место для него.</span><span class="sxs-lookup"><span data-stu-id="b54db-151">Configure hello new SQL Database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="b54db-152">После создания базы данных SQL hello щелкните **в среде Visual Studio** в колонке базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="b54db-152">Once hello SQL Database is created, click **Open in Visual Studio** in hello database blade.</span></span>
5. <span data-ttu-id="b54db-153">Щелкните **Настроить брандмауэр**.</span><span class="sxs-lookup"><span data-stu-id="b54db-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="b54db-154">В hello **параметры брандмауэра** колонки, добавьте правило брандмауэра с **НАЧАЛЬНЫЙ IP-** и **конечным IP** задать toohello общедоступный IP-адрес компьютера разработчика.</span><span class="sxs-lookup"><span data-stu-id="b54db-154">In hello **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set toohello public IP address of your development machine.</span></span> <span data-ttu-id="b54db-155">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b54db-155">Click **Save**.</span></span>

   <span data-ttu-id="b54db-156">Это позволит серверу базы данных toohello соединения с компьютера разработки.</span><span class="sxs-lookup"><span data-stu-id="b54db-156">This will allow connections toohello database server from your development machine.</span></span>
7. <span data-ttu-id="b54db-157">В колонке базы данных hello, нажмите кнопку **свойства**, нажмите кнопку **Показать строки подключения базы данных**.</span><span class="sxs-lookup"><span data-stu-id="b54db-157">Back in hello database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="b54db-158">Используйте hello копирования кнопки tooput hello значение **ADO.NET** hello буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="b54db-158">Use hello copy button tooput hello value of **ADO.NET** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="b54db-159">Настройка проекта hello</span><span class="sxs-lookup"><span data-stu-id="b54db-159">Configure hello Project</span></span>
<span data-ttu-id="b54db-160">В этом разделе мы настроим наш веб-приложения toouse hello SQL база данных только что созданный.</span><span class="sxs-lookup"><span data-stu-id="b54db-160">In this section, we'll configure our web app toouse hello SQL database we just created.</span></span> <span data-ttu-id="b54db-161">Также будут установлены дополнительные Python пакетов требуется toouse баз данных SQL с Django.</span><span class="sxs-lookup"><span data-stu-id="b54db-161">We'll also install additional Python packages required toouse SQL databases with Django.</span></span> <span data-ttu-id="b54db-162">Затем мы выполним hello веб-приложения локально.</span><span class="sxs-lookup"><span data-stu-id="b54db-162">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="b54db-163">В Visual Studio откройте **settings.py**, из hello *ProjectName* папки.</span><span class="sxs-lookup"><span data-stu-id="b54db-163">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="b54db-164">Временно вставьте строку подключения hello в редакторе hello.</span><span class="sxs-lookup"><span data-stu-id="b54db-164">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="b54db-165">указана строка подключения Hello в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="b54db-165">hello connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="b54db-166">Изменить определение hello `DATABASES` toouse hello значений, приведенных выше.</span><span class="sxs-lookup"><span data-stu-id="b54db-166">Edit hello definition of `DATABASES` toouse hello values above.</span></span>

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

1. <span data-ttu-id="b54db-167">В обозревателе решений в разделе **среды Python**, щелкните правой кнопкой мыши в виртуальной среде hello и выберите **установить пакет Python**.</span><span class="sxs-lookup"><span data-stu-id="b54db-167">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="b54db-168">Установить пакет hello `pyodbc` с помощью **pip**.</span><span class="sxs-lookup"><span data-stu-id="b54db-168">Install hello package `pyodbc` using **pip**.</span></span>

     ![Диалоговое окно «Установка пакета Python»](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="b54db-170">Установить пакет hello `django-pyodbc-azure` с помощью **pip**.</span><span class="sxs-lookup"><span data-stu-id="b54db-170">Install hello package `django-pyodbc-azure` using **pip**.</span></span>

     ![Диалоговое окно «Установка пакета Python»](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="b54db-172">В **обозревателе решений**, правой кнопкой мыши узел проекта hello и выберите **Python**и выберите **Django перенести**.</span><span class="sxs-lookup"><span data-stu-id="b54db-172">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="b54db-173">Выберите **Django Create Superuser**(Создать суперпользователя Django).</span><span class="sxs-lookup"><span data-stu-id="b54db-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="b54db-174">Это создаст hello таблиц для базы данных SQL hello, созданной в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="b54db-174">This will create hello tables for hello SQL database we created in hello previous section.</span></span> <span data-ttu-id="b54db-175">Выполните запросы hello toocreate пользователя, который не имеет toomatch hello пользователя в базе данных sqlite hello, созданные в первом разделе hello.</span><span class="sxs-lookup"><span data-stu-id="b54db-175">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section.</span></span>
5. <span data-ttu-id="b54db-176">Запустите приложение hello с `F5`.</span><span class="sxs-lookup"><span data-stu-id="b54db-176">Run hello application with `F5`.</span></span> <span data-ttu-id="b54db-177">Опросы, созданных с помощью **создать образец опрашивает** и hello данные, переданные с правом голоса сериализуются в базе данных SQL hello.</span><span class="sxs-lookup"><span data-stu-id="b54db-177">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello SQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="b54db-178">Публикация hello web app tooAzure службы приложений</span><span class="sxs-lookup"><span data-stu-id="b54db-178">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="b54db-179">Hello Azure .NET SDK предоставляет легко toodeploy вашей web tooAzure приложения web веб-приложений служб приложений.</span><span class="sxs-lookup"><span data-stu-id="b54db-179">hello Azure .NET SDK provides an easy way toodeploy your web web app tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="b54db-180">В **обозревателе решений**, правой кнопкой мыши узел проекта hello и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="b54db-180">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>

     ![Диалоговое окно «Публикация веб-сайта»](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="b54db-182">Щелкните **Веб-приложения Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="b54db-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="b54db-183">Щелкните **New** toocreate новое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="b54db-183">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="b54db-184">Заполните следующие поля hello и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="b54db-184">Fill in hello following fields and click **Create**.</span></span>

   * <span data-ttu-id="b54db-185">**Имя веб-приложения**</span><span class="sxs-lookup"><span data-stu-id="b54db-185">**Web App name**</span></span>
   * <span data-ttu-id="b54db-186">**План обслуживания приложения**</span><span class="sxs-lookup"><span data-stu-id="b54db-186">**App Service plan**</span></span>
   * <span data-ttu-id="b54db-187">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="b54db-187">**Resource group**</span></span>
   * <span data-ttu-id="b54db-188">**Регион**</span><span class="sxs-lookup"><span data-stu-id="b54db-188">**Region**</span></span>
   * <span data-ttu-id="b54db-189">Оставить **сервера базы данных** значение слишком**ни одной базы данных**</span><span class="sxs-lookup"><span data-stu-id="b54db-189">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="b54db-190">Примите значения по умолчанию и щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="b54db-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="b54db-191">Веб-браузере откроется автоматически toohello опубликованных веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="b54db-191">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="b54db-192">Вы увидите рабочее приложение hello web, как и ожидалось, с помощью hello **SQL** базы данных, размещенной в Azure.</span><span class="sxs-lookup"><span data-stu-id="b54db-192">You should see hello web app working as expected, using hello **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="b54db-193">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b54db-193">Congratulations!</span></span>

     ![Веб-браузер](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="b54db-195">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b54db-195">Next steps</span></span>
<span data-ttu-id="b54db-196">Выполните эти ссылки toolearn Дополнительные сведения о средствах Python для Visual Studio, Django и базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="b54db-196">Follow these links toolearn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="b54db-197">[Документация по средствам Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="b54db-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="b54db-198">[Веб-проекты]</span><span class="sxs-lookup"><span data-stu-id="b54db-198">[Web Projects]</span></span>
  * <span data-ttu-id="b54db-199">[Проекты для облачной службы]</span><span class="sxs-lookup"><span data-stu-id="b54db-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="b54db-200">[Удаленная отладка в Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="b54db-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="b54db-201">[Документация по Django]</span><span class="sxs-lookup"><span data-stu-id="b54db-201">[Django Documentation]</span></span>
* <span data-ttu-id="b54db-202">[База данных SQL]</span><span class="sxs-lookup"><span data-stu-id="b54db-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="b54db-203">Изменения</span><span class="sxs-lookup"><span data-stu-id="b54db-203">What's changed</span></span>
* <span data-ttu-id="b54db-204">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b54db-204">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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
