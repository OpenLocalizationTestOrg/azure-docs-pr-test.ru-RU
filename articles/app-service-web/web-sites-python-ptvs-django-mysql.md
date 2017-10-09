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
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="e9685-103">Использование Django и MySQL в Azure с помощью инструментов Python 2.2 для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e9685-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="e9685-104">В этом учебнике мы используем [средства Python для Visual Studio](https://www.visualstudio.com/vs/python) toocreate простой опрашивает веб-приложения с помощью одного из шаблонов образец hello PTVS.</span><span class="sxs-lookup"><span data-stu-id="e9685-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="e9685-105">Вы узнаете, как toouse MySQL служба размещена в Azure, как tooconfigure hello web app toouse MySQL и как toopublish hello веб-приложения слишком[веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="e9685-105">You'll learn how toouse a MySQL service hosted on Azure, how tooconfigure hello web app toouse MySQL, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

> [!NOTE]
> <span data-ttu-id="e9685-106">Hello сведения, содержащиеся в этом учебнике также доступен в hello следующие видео:</span><span class="sxs-lookup"><span data-stu-id="e9685-106">hello information contained in this tutorial is also available in hello following video:</span></span>
> 
> <span data-ttu-id="e9685-107">[PTVS 2.1: Django app with MySQL][video] (PTVS 2.1: приложение Django с использованием MySQL).</span><span class="sxs-lookup"><span data-stu-id="e9685-107">[PTVS 2.1: Django app with MySQL][video]</span></span>
> 
> 

<span data-ttu-id="e9685-108">В разделе hello [центре разработчиков Python] Дополнительные статьи, посвященные разработки Azure приложение службы веб-приложений с помощью бутылка PTVS, термосе и Django веб-платформы с помощью службы хранилища Azure таблицы, MySQL и базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="e9685-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span></span> <span data-ttu-id="e9685-109">Хотя данная статья посвящена службы приложений, hello шаги похожи, при разработке [облачных служб Azure].</span><span class="sxs-lookup"><span data-stu-id="e9685-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9685-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e9685-110">Prerequisites</span></span>
* <span data-ttu-id="e9685-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="e9685-111">Visual Studio 2015</span></span>
* <span data-ttu-id="e9685-112">[Python 2.7 (32-разрядная версия)] или [Python 3.4 (32-разрядная версия)]</span><span class="sxs-lookup"><span data-stu-id="e9685-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>
* <span data-ttu-id="e9685-113">[Инструменты Python 2.2 для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e9685-113">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="e9685-114">[средства Python 2.2 для Visual Studio образцы VSIX]</span><span class="sxs-lookup"><span data-stu-id="e9685-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="e9685-115">[Инструменты пакета SDK для Azure для Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="e9685-115">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="e9685-116">Django 1.9 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e9685-116">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> <span data-ttu-id="e9685-117">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="e9685-117">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e9685-118">Не требуется никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="e9685-118">No credit card is required, and no commitments are necessary.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="e9685-119">Создание проекта hello</span><span class="sxs-lookup"><span data-stu-id="e9685-119">Create hello Project</span></span>
<span data-ttu-id="e9685-120">В этом разделе мы создадим проект Visual Studio с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="e9685-120">In this section, you'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="e9685-121">Мы создадим виртуальную среду и установим необходимые пакеты.</span><span class="sxs-lookup"><span data-stu-id="e9685-121">You'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="e9685-122">Мы создадим также локальную базу данных с помощью sqlite.</span><span class="sxs-lookup"><span data-stu-id="e9685-122">You'll create a local database using sqlite.</span></span> <span data-ttu-id="e9685-123">Затем вы будете запускать приложение hello локально.</span><span class="sxs-lookup"><span data-stu-id="e9685-123">Then you'll run hello application locally.</span></span>

1. <span data-ttu-id="e9685-124">В Visual Studio выберите последовательно **Файл** и **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="e9685-124">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="e9685-125">Здравствуйте, шаблоны проектов из hello [средства Python 2.2 для Visual Studio образцы VSIX] можно найти в разделе **Python**, **образцы**.</span><span class="sxs-lookup"><span data-stu-id="e9685-125">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="e9685-126">Выберите **опрашивает Django веб-проекта** и нажмите кнопку ОК toocreate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="e9685-126">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>
   
    ![Диалоговое окно "Новый проект"](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. <span data-ttu-id="e9685-128">Появится запрос tooinstall внешние пакеты.</span><span class="sxs-lookup"><span data-stu-id="e9685-128">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="e9685-129">Выберите вариант **Установить в виртуальной среде**.</span><span class="sxs-lookup"><span data-stu-id="e9685-129">Select **Install into a virtual environment**.</span></span>
   
    ![Диалоговое окно «Внешние пакеты»](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="e9685-131">Выберите **Python 2.7** или **Python 3.4** базовый интерпретатора hello.</span><span class="sxs-lookup"><span data-stu-id="e9685-131">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
    ![Диалоговое окно «Добавление виртуальной среды»](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="e9685-133">В **обозревателе решений**, правой кнопкой мыши узел проекта hello и выберите **Python**и выберите **Django перенести**.</span><span class="sxs-lookup"><span data-stu-id="e9685-133">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="e9685-134">Выберите **Django Create Superuser**(Создать суперпользователя Django).</span><span class="sxs-lookup"><span data-stu-id="e9685-134">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="e9685-135">Это будет открыть консоль управления Django и создать базу данных sqlite в папке проекта hello.</span><span class="sxs-lookup"><span data-stu-id="e9685-135">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="e9685-136">Выполните запросы hello toocreate пользователя.</span><span class="sxs-lookup"><span data-stu-id="e9685-136">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="e9685-137">Убедитесь, что приложение hello работает, нажав клавишу `F5`.</span><span class="sxs-lookup"><span data-stu-id="e9685-137">Confirm that hello application works by pressing `F5`.</span></span>
8. <span data-ttu-id="e9685-138">Нажмите кнопку **входа** hello панели навигации в верхней hello.</span><span class="sxs-lookup"><span data-stu-id="e9685-138">Click **Log in** from hello navigation bar at hello top.</span></span>
   
    ![Панель навигации Django](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="e9685-140">Введите учетные данные hello hello пользователя, созданный при синхронизации базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="e9685-140">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>
   
    ![Форма входа](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="e9685-142">Щелкните **Создать примеры опросов**.</span><span class="sxs-lookup"><span data-stu-id="e9685-142">Click **Create Sample Polls**.</span></span>
    
     ![Создать примеры опросов](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="e9685-144">Выберите опрос и проголосуйте.</span><span class="sxs-lookup"><span data-stu-id="e9685-144">Click on a poll and vote.</span></span>
    
     ![Голосование в примерах опросов](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a><span data-ttu-id="e9685-146">Создание базы данных MySQL</span><span class="sxs-lookup"><span data-stu-id="e9685-146">Create a MySQL Database</span></span>
<span data-ttu-id="e9685-147">Для базы данных hello вы создадите базы данных ClearDB MySQL размещенной в Azure.</span><span class="sxs-lookup"><span data-stu-id="e9685-147">For hello database, you'll create a ClearDB MySQL hosted database on Azure.</span></span>

<span data-ttu-id="e9685-148">В качестве альтернативного решения вы можете создать свою собственную виртуальную машину в Azure, а затем установить и настроить MySQL самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="e9685-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span></span>

<span data-ttu-id="e9685-149">Выполнив следующие шаги, вы сможете создать бесплатную базу данных.</span><span class="sxs-lookup"><span data-stu-id="e9685-149">You can create a database with a free plan by following these steps.</span></span>

1. <span data-ttu-id="e9685-150">Войдите в toohello [портала Azure].</span><span class="sxs-lookup"><span data-stu-id="e9685-150">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="e9685-151">Hello верхней части панели навигации hello, нажмите кнопку **NEW**, нажмите кнопку **данные + хранилище**, а затем нажмите кнопку **базы данных MySQL**.</span><span class="sxs-lookup"><span data-stu-id="e9685-151">At hello Top of hello navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span></span>
3. <span data-ttu-id="e9685-152">Настройте новую базу данных MySQL hello, создав новую группу ресурсов и выберите hello соответствующее место для него.</span><span class="sxs-lookup"><span data-stu-id="e9685-152">Configure hello new MySQL database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="e9685-153">После создания базы данных MySQL hello щелкните **свойства** в колонке базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="e9685-153">Once hello MySQL database is created, click **Properties** in hello database blade.</span></span>
5. <span data-ttu-id="e9685-154">Используйте hello копирования кнопки tooput hello значение **строка подключения** hello буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="e9685-154">Use hello copy button tooput hello value of **CONNECTION STRING** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="e9685-155">Настройка проекта hello</span><span class="sxs-lookup"><span data-stu-id="e9685-155">Configure hello Project</span></span>
<span data-ttu-id="e9685-156">В этом разделе вы настроите наш веб-приложения toouse hello MySQL база данных только что созданный.</span><span class="sxs-lookup"><span data-stu-id="e9685-156">In this section, you'll configure our web app toouse hello MySQL database you just created.</span></span> <span data-ttu-id="e9685-157">Вы также установите дополнительные Python пакетов требуется toouse базы данных MySQL с Django.</span><span class="sxs-lookup"><span data-stu-id="e9685-157">You'll also install additional Python packages required toouse MySQL databases with Django.</span></span> <span data-ttu-id="e9685-158">Затем вы будете запускать веб-приложения hello локально.</span><span class="sxs-lookup"><span data-stu-id="e9685-158">Then you'll run hello web app locally.</span></span>

1. <span data-ttu-id="e9685-159">В Visual Studio откройте **settings.py**, из hello *ProjectName* папки.</span><span class="sxs-lookup"><span data-stu-id="e9685-159">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="e9685-160">Временно вставьте строку подключения hello в редакторе hello.</span><span class="sxs-lookup"><span data-stu-id="e9685-160">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="e9685-161">указана строка подключения Hello в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="e9685-161">hello connection string is in this format:</span></span>
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    <span data-ttu-id="e9685-162">Изменить базу данных по умолчанию hello **ЯДРА** toouse MySQL, а также установите hello значения для **имя**, **пользователя**, **пароль** и  **УЗЕЛ** из hello **CONNECTIONSTRING**.</span><span class="sxs-lookup"><span data-stu-id="e9685-162">Change hello default database **ENGINE** toouse MySQL, and set hello values for **NAME**, **USER**, **PASSWORD** and **HOST** from hello **CONNECTIONSTRING**.</span></span>
   
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
2. <span data-ttu-id="e9685-163">В обозревателе решений в разделе **среды Python**, щелкните правой кнопкой мыши в виртуальной среде hello и выберите **установить пакет Python**.</span><span class="sxs-lookup"><span data-stu-id="e9685-163">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
3. <span data-ttu-id="e9685-164">Установить пакет hello `mysqlclient` с помощью **pip**.</span><span class="sxs-lookup"><span data-stu-id="e9685-164">Install hello package `mysqlclient` using **pip**.</span></span>
   
    ![Диалоговое окно «Установка пакета»](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. <span data-ttu-id="e9685-166">В **обозревателе решений**, правой кнопкой мыши узел проекта hello и выберите **Python**и выберите **Django перенести**.</span><span class="sxs-lookup"><span data-stu-id="e9685-166">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="e9685-167">Выберите **Django Create Superuser**(Создать суперпользователя Django).</span><span class="sxs-lookup"><span data-stu-id="e9685-167">Then select **Django Create Superuser**.</span></span>
   
    <span data-ttu-id="e9685-168">Это создаст hello таблиц для базы данных MySQL hello, созданный в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="e9685-168">This will create hello tables for hello MySQL database you created in hello previous section.</span></span> <span data-ttu-id="e9685-169">Выполните toocreate hello запросы пользователя, который не имеет toomatch hello пользователя в базе данных sqlite hello, созданные в hello первом разделе этой статьи.</span><span class="sxs-lookup"><span data-stu-id="e9685-169">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section of this article.</span></span>
5. <span data-ttu-id="e9685-170">Запустите приложение hello с `F5`.</span><span class="sxs-lookup"><span data-stu-id="e9685-170">Run hello application with `F5`.</span></span> <span data-ttu-id="e9685-171">Опросы, созданных с помощью **создать образец опрашивает** и hello данные, переданные с правом голоса сериализуются в базе данных MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="e9685-171">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello MySQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="e9685-172">Публикация hello web app tooAzure службы приложений</span><span class="sxs-lookup"><span data-stu-id="e9685-172">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="e9685-173">Hello Azure .NET SDK предоставляет простой способ toodeploy вашей web app tooAzure службы приложений.</span><span class="sxs-lookup"><span data-stu-id="e9685-173">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="e9685-174">В **обозревателе решений**, правой кнопкой мыши узел проекта hello и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="e9685-174">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
    ![Диалоговое окно «Публикация веб-сайта»](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="e9685-176">Щелкните **Служба приложений Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="e9685-176">Click on **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="e9685-177">Щелкните **New** toocreate новое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="e9685-177">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="e9685-178">Заполните следующие поля hello и нажмите кнопку **создать**:</span><span class="sxs-lookup"><span data-stu-id="e9685-178">Fill in hello following fields and click **Create**:</span></span>
   
   * <span data-ttu-id="e9685-179">**Имя веб-приложения**</span><span class="sxs-lookup"><span data-stu-id="e9685-179">**Web App name**</span></span>
   * <span data-ttu-id="e9685-180">**План обслуживания приложения**</span><span class="sxs-lookup"><span data-stu-id="e9685-180">**App Service plan**</span></span>
   * <span data-ttu-id="e9685-181">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="e9685-181">**Resource group**</span></span>
   * <span data-ttu-id="e9685-182">**Регион**</span><span class="sxs-lookup"><span data-stu-id="e9685-182">**Region**</span></span>
   * <span data-ttu-id="e9685-183">Оставить **сервера базы данных** значение слишком**ни одной базы данных**</span><span class="sxs-lookup"><span data-stu-id="e9685-183">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="e9685-184">Примите значения по умолчанию и щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="e9685-184">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="e9685-185">Веб-браузере откроется автоматически toohello опубликованных веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e9685-185">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="e9685-186">Вы увидите рабочее приложение hello web, как и ожидалось, с помощью hello **MySQL** базы данных, размещенной в Azure.</span><span class="sxs-lookup"><span data-stu-id="e9685-186">You should see hello web app working as expected, using hello **MySQL** database hosted on Azure.</span></span>
   
    ![Веб-браузер](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    <span data-ttu-id="e9685-188">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="e9685-188">Congratulations!</span></span> <span data-ttu-id="e9685-189">Вы успешно опубликовали вашей tooAzure MySQL веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e9685-189">You have successfully published your MySQL-based web app tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9685-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e9685-190">Next steps</span></span>
<span data-ttu-id="e9685-191">Выполните эти ссылки toolearn Дополнительные сведения о средствах Python для Visual Studio, Django и MySQL.</span><span class="sxs-lookup"><span data-stu-id="e9685-191">Follow these links toolearn more about Python Tools for Visual Studio, Django and MySQL.</span></span>

* <span data-ttu-id="e9685-192">[Документация по средствам Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e9685-192">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="e9685-193">[Веб-проекты]</span><span class="sxs-lookup"><span data-stu-id="e9685-193">[Web Projects]</span></span>
  * <span data-ttu-id="e9685-194">[Проекты для облачной службы]</span><span class="sxs-lookup"><span data-stu-id="e9685-194">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="e9685-195">[Удаленная отладка в Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="e9685-195">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="e9685-196">[Документация по Django]</span><span class="sxs-lookup"><span data-stu-id="e9685-196">[Django Documentation]</span></span>
* <span data-ttu-id="e9685-197">[MySQL]</span><span class="sxs-lookup"><span data-stu-id="e9685-197">[MySQL]</span></span>

<span data-ttu-id="e9685-198">Дополнительные сведения см. в разделе hello [центре разработчиков Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="e9685-198">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

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
