---
title: "Использование Django и базы данных SQL в Azure с помощью инструментов Python 2.2 для Visual Studio"
description: "Информация о том, как создать веб-приложение Django, которое хранит данные в экземпляре базы данных SQL, с помощью инструментов Python для Visual Studio и развернуть его в веб-приложениях службы приложений Azure."
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
ms.openlocfilehash: 65b59dee2b7bddca77d31c692dab713c68d67e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="a9693-103">Использование Django и базы данных SQL в Azure с помощью инструментов Python 2.2 для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a9693-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="a9693-104">В этом учебнике мы используем [Средства Python для Visual Studio] , чтобы создать простое веб-приложение опросника с помощью шаблонов PTVS.</span><span class="sxs-lookup"><span data-stu-id="a9693-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="a9693-105">Также доступна [видеоверсия](https://www.youtube.com/watch?v=ZwcoGcIeHF4)этого учебника.</span><span class="sxs-lookup"><span data-stu-id="a9693-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="a9693-106">Вы узнаете, как использовать базы данных SQL, размещенные на платформе Azure, как настроить веб-приложение для работы с базой данных SQL, а затем опубликовать его в [веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="a9693-106">We'll learn how to use a SQL database hosted on Azure, how to configure the web app to use a SQL database, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="a9693-107">В [центре разработчиков для Python] доступны материалы по разработке веб-приложений службы приложений Azure с использованием PTVS, веб-платформ Bottle, Flask и Django, хранилища таблиц Azure, а также служб базы данных SQL и MySQL.</span><span class="sxs-lookup"><span data-stu-id="a9693-107">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="a9693-108">Хотя эта статья ориентирована в первую очередь на службу приложений, при разработке для [облачных служб Azure]используются аналогичные процедуры.</span><span class="sxs-lookup"><span data-stu-id="a9693-108">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9693-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a9693-109">Prerequisites</span></span>
* <span data-ttu-id="a9693-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="a9693-110">Visual Studio 2015</span></span>
* <span data-ttu-id="a9693-111">[Python 2.7 (32-разрядная версия).]</span><span class="sxs-lookup"><span data-stu-id="a9693-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="a9693-112">[Инструменты Python 2.2 для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a9693-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="a9693-113">[примеров VSIX для инструментов Python 2.2 для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a9693-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="a9693-114">[Инструменты пакета SDK для Azure для Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="a9693-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="a9693-115">Django 1.9 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="a9693-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="a9693-116">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="a9693-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a9693-117">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="a9693-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-the-project"></a><span data-ttu-id="a9693-118">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="a9693-118">Create the Project</span></span>
<span data-ttu-id="a9693-119">В этом разделе мы создадим проект Visual Studio с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="a9693-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="a9693-120">Мы создадим виртуальную среду и установим необходимые пакеты.</span><span class="sxs-lookup"><span data-stu-id="a9693-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="a9693-121">Мы создадим локальную базу данных с помощью sqlite.</span><span class="sxs-lookup"><span data-stu-id="a9693-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="a9693-122">Затем запустим веб-приложение локально.</span><span class="sxs-lookup"><span data-stu-id="a9693-122">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="a9693-123">В Visual Studio выберите последовательно **Файл** и **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="a9693-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="a9693-124">Чтобы найти шаблоны [примеров VSIX для инструментов Python 2.2 для Visual Studio], в разделе **Python** выберите **Примеры**.</span><span class="sxs-lookup"><span data-stu-id="a9693-124">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="a9693-125">Выберите **Веб-проект опросов Django** и нажмите кнопку «ОК», чтобы создать проект.</span><span class="sxs-lookup"><span data-stu-id="a9693-125">Select **Polls Django Web Project** and click OK to create the project.</span></span>

     ![Диалоговое окно «Новый проект»](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="a9693-127">Вам будет предложено установить внешние пакеты.</span><span class="sxs-lookup"><span data-stu-id="a9693-127">You will be prompted to install external packages.</span></span> <span data-ttu-id="a9693-128">Выберите вариант **Установить в виртуальной среде**.</span><span class="sxs-lookup"><span data-stu-id="a9693-128">Select **Install into a virtual environment**.</span></span>

     ![Диалоговое окно «Внешние пакеты»](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="a9693-130">Выберите **Python 2.7** в качестве базового интерпретатора.</span><span class="sxs-lookup"><span data-stu-id="a9693-130">Select **Python 2.7** as the base interpreter.</span></span>

     ![Диалоговое окно «Добавление виртуальной среды»](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="a9693-132">В **обозревателе решений** щелкните правой кнопкой мыши узел проекта, а затем последовательно выберите **Python** и **Django Migrate** (Миграция Django).</span><span class="sxs-lookup"><span data-stu-id="a9693-132">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="a9693-133">Выберите **Django Create Superuser**(Создать суперпользователя Django).</span><span class="sxs-lookup"><span data-stu-id="a9693-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="a9693-134">Откроется консоль управления Django, а в папке проекта будет создана база данных sqlite.</span><span class="sxs-lookup"><span data-stu-id="a9693-134">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="a9693-135">Следуйте инструкциям на экране для создания пользователя.</span><span class="sxs-lookup"><span data-stu-id="a9693-135">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="a9693-136">Убедитесь в том, что приложение работает, нажав клавишу <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="a9693-136">Confirm that the application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="a9693-137">Щелкните **Войти в систему** на панели навигации сверху.</span><span class="sxs-lookup"><span data-stu-id="a9693-137">Click **Log in** from the navigation bar at the top.</span></span>

     ![Веб-браузер](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="a9693-139">Введите учетные данные пользователя, который был создан при синхронизации базы данных.</span><span class="sxs-lookup"><span data-stu-id="a9693-139">Enter the credentials for the user you created when you synchronized the database.</span></span>

     ![Веб-браузер](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="a9693-141">Щелкните **Создать примеры опросов**.</span><span class="sxs-lookup"><span data-stu-id="a9693-141">Click **Create Sample Polls**.</span></span>

      ![Веб-браузер](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="a9693-143">Выберите опрос и проголосуйте.</span><span class="sxs-lookup"><span data-stu-id="a9693-143">Click on a poll and vote.</span></span>

      ![Веб-браузер](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="a9693-145">Создание базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="a9693-145">Create a SQL Database</span></span>
<span data-ttu-id="a9693-146">В качестве базы данных мы создадим базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a9693-146">For the database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="a9693-147">Выполнив следующие шаги, вы создадите базу данных.</span><span class="sxs-lookup"><span data-stu-id="a9693-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="a9693-148">Войдите на [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="a9693-148">Log into the [Azure Portal].</span></span>
2. <span data-ttu-id="a9693-149">В нижней части области навигации щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a9693-149">At the bottom of the navigation pane, click **NEW**.</span></span> <span data-ttu-id="a9693-150">Выберите **Данные+хранилище** > **База данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="a9693-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="a9693-151">Настройте новую Базу данных SQL, создав новую группу ресурсов, и выберите соответствующее расположение для нее.</span><span class="sxs-lookup"><span data-stu-id="a9693-151">Configure the new SQL Database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="a9693-152">После создания Базы данных SQL щелкните **Открыть в Visual Studio** в колонке базы данных.</span><span class="sxs-lookup"><span data-stu-id="a9693-152">Once the SQL Database is created, click **Open in Visual Studio** in the database blade.</span></span>
5. <span data-ttu-id="a9693-153">Щелкните **Настроить брандмауэр**.</span><span class="sxs-lookup"><span data-stu-id="a9693-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="a9693-154">В колонке **Параметры брандмауэра** добавьте правило брандмауэра, указав для параметров **Начальный IP-адрес** и **Конечный IP-адрес** общедоступный IP-адрес компьютера разработки.</span><span class="sxs-lookup"><span data-stu-id="a9693-154">In the **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set to the public IP address of your development machine.</span></span> <span data-ttu-id="a9693-155">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a9693-155">Click **Save**.</span></span>

   <span data-ttu-id="a9693-156">Это позволит вам подключаться к серверу базы данных со своего компьютера разработчика.</span><span class="sxs-lookup"><span data-stu-id="a9693-156">This will allow connections to the database server from your development machine.</span></span>
7. <span data-ttu-id="a9693-157">В колонке базы данных щелкните **Свойства**, затем щелкните **Показать строки подключения к базам данных**.</span><span class="sxs-lookup"><span data-stu-id="a9693-157">Back in the database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="a9693-158">Поместите значение **ADO.NET** в буфер обмена с помощью кнопки копирования.</span><span class="sxs-lookup"><span data-stu-id="a9693-158">Use the copy button to put the value of **ADO.NET** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="a9693-159">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="a9693-159">Configure the Project</span></span>
<span data-ttu-id="a9693-160">В этом разделе мы настроим веб-приложение для использования только что созданной базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a9693-160">In this section, we'll configure our web app to use the SQL database we just created.</span></span> <span data-ttu-id="a9693-161">Мы также установим дополнительные пакеты Python, необходимые для использования баз данных SQL с Django.</span><span class="sxs-lookup"><span data-stu-id="a9693-161">We'll also install additional Python packages required to use SQL databases with Django.</span></span> <span data-ttu-id="a9693-162">Затем запустим веб-приложение локально.</span><span class="sxs-lookup"><span data-stu-id="a9693-162">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="a9693-163">Откройте в Visual Studio файл **settings.py**из папки *ProjectName* .</span><span class="sxs-lookup"><span data-stu-id="a9693-163">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="a9693-164">Временно вставьте строку подключения в редакторе.</span><span class="sxs-lookup"><span data-stu-id="a9693-164">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="a9693-165">Строка подключения имеет такой формат:</span><span class="sxs-lookup"><span data-stu-id="a9693-165">The connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="a9693-166">Измените определение `DATABASES` , чтобы использовать указанные выше значения.</span><span class="sxs-lookup"><span data-stu-id="a9693-166">Edit the definition of `DATABASES` to use the values above.</span></span>

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

1. <span data-ttu-id="a9693-167">В обозревателе решений в разделе **Python Environments** (Среды Python) щелкните правой кнопкой мыши виртуальную среду и выберите **Install Python Package** (Установить пакет Python).</span><span class="sxs-lookup"><span data-stu-id="a9693-167">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="a9693-168">Установите пакет `pyodbc` , используя **pip**.</span><span class="sxs-lookup"><span data-stu-id="a9693-168">Install the package `pyodbc` using **pip**.</span></span>

     ![Диалоговое окно «Установка пакета Python»](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="a9693-170">Установите пакет `django-pyodbc-azure` , используя **pip**.</span><span class="sxs-lookup"><span data-stu-id="a9693-170">Install the package `django-pyodbc-azure` using **pip**.</span></span>

     ![Диалоговое окно «Установка пакета Python»](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="a9693-172">В **обозревателе решений** щелкните правой кнопкой мыши узел проекта, а затем последовательно выберите **Python** и **Django Migrate** (Миграция Django).</span><span class="sxs-lookup"><span data-stu-id="a9693-172">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="a9693-173">Выберите **Django Create Superuser**(Создать суперпользователя Django).</span><span class="sxs-lookup"><span data-stu-id="a9693-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="a9693-174">В результате будут созданы таблицы для базы данных SQL, созданной в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="a9693-174">This will create the tables for the SQL database we created in the previous section.</span></span> <span data-ttu-id="a9693-175">Следуя подсказкам, создайте пользователя, отличного от пользователя базы данных sqlite, которого мы создали в первом разделе.</span><span class="sxs-lookup"><span data-stu-id="a9693-175">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section.</span></span>
5. <span data-ttu-id="a9693-176">Запустите приложение, нажав клавишу `F5`.</span><span class="sxs-lookup"><span data-stu-id="a9693-176">Run the application with `F5`.</span></span> <span data-ttu-id="a9693-177">Опросы, созданные с помощью команды **Создать примеры опросов** и отправленных данных голосования, будут сериализованы в базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a9693-177">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the SQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="a9693-178">Публикация веб-приложения в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="a9693-178">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="a9693-179">С помощью пакета SDK для Azure для .NET можно легко развернуть свое веб-приложение в веб-приложениях службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="a9693-179">The Azure .NET SDK provides an easy way to deploy your web web app to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="a9693-180">В **обозревателе решений** щелкните правой кнопкой мыши узел проекта и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="a9693-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>

     ![Диалоговое окно «Публикация веб-сайта»](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="a9693-182">Щелкните **Веб-приложения Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="a9693-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="a9693-183">Нажмите **Создать** , чтобы создать новое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="a9693-183">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="a9693-184">Заполните перечисленные ниже поля и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a9693-184">Fill in the following fields and click **Create**.</span></span>

   * <span data-ttu-id="a9693-185">**Имя веб-приложения**</span><span class="sxs-lookup"><span data-stu-id="a9693-185">**Web App name**</span></span>
   * <span data-ttu-id="a9693-186">**План обслуживания приложения**</span><span class="sxs-lookup"><span data-stu-id="a9693-186">**App Service plan**</span></span>
   * <span data-ttu-id="a9693-187">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="a9693-187">**Resource group**</span></span>
   * <span data-ttu-id="a9693-188">**Регион**</span><span class="sxs-lookup"><span data-stu-id="a9693-188">**Region**</span></span>
   * <span data-ttu-id="a9693-189">Для параметра **Сервер базы данных** оставьте значение **Нет базы данных**.</span><span class="sxs-lookup"><span data-stu-id="a9693-189">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="a9693-190">Примите значения по умолчанию и щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="a9693-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="a9693-191">Опубликованное веб-приложение автоматически откроется в вашем браузере.</span><span class="sxs-lookup"><span data-stu-id="a9693-191">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="a9693-192">Вы должны увидеть, что приложение, как и ожидалось, работает с базой данных **SQL** , размещенной в Azure.</span><span class="sxs-lookup"><span data-stu-id="a9693-192">You should see the web app working as expected, using the **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="a9693-193">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="a9693-193">Congratulations!</span></span>

     ![Веб-браузер](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="a9693-195">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a9693-195">Next steps</span></span>
<span data-ttu-id="a9693-196">Используйте следующие ссылки, чтобы узнать больше об инструментах Python для Visual Studio, Django и базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a9693-196">Follow these links to learn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="a9693-197">[Документация по средствам Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a9693-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="a9693-198">[Веб-проекты]</span><span class="sxs-lookup"><span data-stu-id="a9693-198">[Web Projects]</span></span>
  * <span data-ttu-id="a9693-199">[Проекты для облачной службы]</span><span class="sxs-lookup"><span data-stu-id="a9693-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="a9693-200">[Удаленная отладка в Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="a9693-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="a9693-201">[Документация по Django]</span><span class="sxs-lookup"><span data-stu-id="a9693-201">[Django Documentation]</span></span>
* <span data-ttu-id="a9693-202">[База данных SQL]</span><span class="sxs-lookup"><span data-stu-id="a9693-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="a9693-203">Изменения</span><span class="sxs-lookup"><span data-stu-id="a9693-203">What's changed</span></span>
* <span data-ttu-id="a9693-204">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="a9693-204">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="a9693-205">[центре разработчиков для Python]: /develop/python/</span><span class="sxs-lookup"><span data-stu-id="a9693-205">[Python Developer Center]: /develop/python/</span></span>
<span data-ttu-id="a9693-206">[облачных служб Azure]: ../cloud-services/cloud-services-python-ptvs.md</span><span class="sxs-lookup"><span data-stu-id="a9693-206">[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md</span></span>

<!--External Link references-->
<span data-ttu-id="a9693-207">[портал Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="a9693-207">[Azure Portal]: https://portal.azure.com</span></span>
<span data-ttu-id="a9693-208">[Средства Python для Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="a9693-208">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="a9693-209">[Инструменты Python 2.2 для Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="a9693-209">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="a9693-210">[примеров VSIX для инструментов Python 2.2 для Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="a9693-210">[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="a9693-211">[Инструменты пакета SDK для Azure для Visual Studio 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span><span class="sxs-lookup"><span data-stu-id="a9693-211">[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span></span>
<span data-ttu-id="a9693-212">[Python 2.7 (32-разрядная версия).]: http://go.microsoft.com/fwlink/?LinkId=517190</span><span class="sxs-lookup"><span data-stu-id="a9693-212">[Python 2.7 32-bit]: http://go.microsoft.com/fwlink/?LinkId=517190</span></span>
<span data-ttu-id="a9693-213">[Документация по средствам Python для Visual Studio]: http://aka.ms/ptvsdocs</span><span class="sxs-lookup"><span data-stu-id="a9693-213">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs</span></span>
<span data-ttu-id="a9693-214">[Удаленная отладка в Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026</span><span class="sxs-lookup"><span data-stu-id="a9693-214">[Remote Debugging on Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026</span></span>
<span data-ttu-id="a9693-215">[Веб-проекты]: http://go.microsoft.com/fwlink/?LinkId=624027</span><span class="sxs-lookup"><span data-stu-id="a9693-215">[Web Projects]: http://go.microsoft.com/fwlink/?LinkId=624027</span></span>
<span data-ttu-id="a9693-216">[Проекты для облачной службы]: http://go.microsoft.com/fwlink/?LinkId=624028</span><span class="sxs-lookup"><span data-stu-id="a9693-216">[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028</span></span>
<span data-ttu-id="a9693-217">[Документация по Django]: https://www.djangoproject.com/</span><span class="sxs-lookup"><span data-stu-id="a9693-217">[Django Documentation]: https://www.djangoproject.com/</span></span>
<span data-ttu-id="a9693-218">[База данных SQL]: /documentation/services/sql-database/</span><span class="sxs-lookup"><span data-stu-id="a9693-218">[SQL Database]: /documentation/services/sql-database/</span></span>
