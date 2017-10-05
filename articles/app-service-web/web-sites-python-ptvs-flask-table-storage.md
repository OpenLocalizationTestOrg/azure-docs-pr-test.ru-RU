---
title: "Flask и хранилище таблиц Azure с использованием инструментов Python 2.2 для Visual Studio"
description: "Информация о том, как создать веб-приложение Flask, которое хранит данные в табличном хранилище Azure, с помощью инструментов Python для Visual Studio и развернуть его в веб-приложениях службы приложений Azure."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: d8e70a29-aca1-4010-95f5-cfe769e3be06
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 2e1bc8eebd0b67b965cc70ac4b5dfe03c4720ddf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="flask-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="bc182-103">Flask и хранилище таблиц Azure с использованием инструментов Python 2.2 для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bc182-103">Flask and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="bc182-104">В этом учебнике мы используем [Средства Python для Visual Studio] , чтобы создать простое веб-приложение опросника с помощью шаблонов PTVS.</span><span class="sxs-lookup"><span data-stu-id="bc182-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="bc182-105">Также доступна [видеоверсия](https://www.youtube.com/watch?v=qUtZWtPwbTk)этого учебника.</span><span class="sxs-lookup"><span data-stu-id="bc182-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span></span>

<span data-ttu-id="bc182-106">Веб-приложение опросника реализует абстракцию для своего репозитория, что позволяет легко переключаться между разными типами репозиториев (размещенный в памяти, табличном хранилище Azure или MongoDB).</span><span class="sxs-lookup"><span data-stu-id="bc182-106">The polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="bc182-107">Вы узнаете, как создать учетную запись хранения Azure и настроить веб-приложение для использования табличного хранилища Azure, а также как опубликовать приложение в [веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="bc182-107">We'll learn how to create an Azure Storage account, how to configure the web app to use Azure Table Storage, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="bc182-108">Зайдите в [Центр по разработке для Python] , где можно найти статьи о разработке веб-приложений службы приложений Azure с PTVS при помощи веб-платформ Bottle, Flask и Django, с использованием MongoDB, табличного хранилища Azure, MySQL и служб Базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="bc182-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="bc182-109">Хотя эта статья ориентирована в первую очередь на службу приложений, при разработке для [облачных служб Azure]используются аналогичные процедуры.</span><span class="sxs-lookup"><span data-stu-id="bc182-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc182-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bc182-110">Prerequisites</span></span>
* <span data-ttu-id="bc182-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="bc182-111">Visual Studio 2015</span></span>
* <span data-ttu-id="bc182-112">[Инструменты Python 2.2 для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="bc182-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="bc182-113">[Образцы VSIX средств Python 2.2 для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="bc182-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="bc182-114">[Инструменты пакета SDK для Azure для Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="bc182-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="bc182-115">[Python 2.7 (32-разрядная версия)] или [Python 3.4 (32-разрядная версия)]</span><span class="sxs-lookup"><span data-stu-id="bc182-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="bc182-116">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="bc182-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="bc182-117">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="bc182-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="bc182-118">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="bc182-118">Create the Project</span></span>
<span data-ttu-id="bc182-119">В этом разделе мы создадим проект Visual Studio с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="bc182-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="bc182-120">Мы создадим виртуальную среду и установим необходимые пакеты.</span><span class="sxs-lookup"><span data-stu-id="bc182-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="bc182-121">Затем мы запустим приложение локально в размещенном в памяти репозитории.</span><span class="sxs-lookup"><span data-stu-id="bc182-121">Then we'll run the application locally using the default in-memory repository.</span></span>

1. <span data-ttu-id="bc182-122">В Visual Studio выберите последовательно **Файл** и **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="bc182-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="bc182-123">Чтобы найти шаблоны [Образцы VSIX средств Python 2.2 для Visual Studio], в разделе **Python** выберите **Примеры**.</span><span class="sxs-lookup"><span data-stu-id="bc182-123">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="bc182-124">Выберите **Веб-проект опросов Flask** и нажмите кнопку «ОК», чтобы создать проект.</span><span class="sxs-lookup"><span data-stu-id="bc182-124">Select **Polls Flask Web Project** and click OK to create the project.</span></span>
   
     ![Диалоговое окно «Новый проект»](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskNewProject.png)
3. <span data-ttu-id="bc182-126">Вам будет предложено установить внешние пакеты.</span><span class="sxs-lookup"><span data-stu-id="bc182-126">You will be prompted to install external packages.</span></span> <span data-ttu-id="bc182-127">Выберите вариант **Установить в виртуальной среде**.</span><span class="sxs-lookup"><span data-stu-id="bc182-127">Select **Install into a virtual environment**.</span></span>
   
     ![Диалоговое окно «Внешние пакеты»](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskExternalPackages.png)
4. <span data-ttu-id="bc182-129">Выберите **Python 2.7** или **Python 3.4** в качестве базового интерпретатора.</span><span class="sxs-lookup"><span data-stu-id="bc182-129">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
     ![Диалоговое окно «Добавление виртуальной среды»](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="bc182-131">Убедитесь, что приложение работает, нажав клавишу `F5`.</span><span class="sxs-lookup"><span data-stu-id="bc182-131">Confirm that the application works by pressing `F5`.</span></span> <span data-ttu-id="bc182-132">По умолчанию приложение использует размещенный в памяти репозиторий, который не требует настройки.</span><span class="sxs-lookup"><span data-stu-id="bc182-132">By default, the application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="bc182-133">При остановке веб-сервера все данные будут утеряны.</span><span class="sxs-lookup"><span data-stu-id="bc182-133">All data is lost when the web server is stopped.</span></span>
6. <span data-ttu-id="bc182-134">Щелкните **Создать примеры опросов**, а затем выберите опросник, чтобы проголосовать.</span><span class="sxs-lookup"><span data-stu-id="bc182-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Веб-браузер](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="bc182-136">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="bc182-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="bc182-137">Для выполнения операций хранилища необходимо использовать учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="bc182-137">To use storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="bc182-138">Выполнив следующие шаги, вы создадите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="bc182-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="bc182-139">Войдите на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bc182-139">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="bc182-140">В левом нижнем углу страницы щелкните значок **Создать** и выберите **Данные + хранилище** > **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="bc182-140">Click the **New** icon on the top left of the Portal, then click **Data + Storage** > **Storage Account**.</span></span> <span data-ttu-id="bc182-141">Щелкните **Создать**, присвойте учетной записи хранения уникальное имя и создайте для нее новую [группу ресурсов](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bc182-141">Click on **Create**, then give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Быстрое создание](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="bc182-143">После создания новой учетной записи на кнопке **Уведомления** начнет мигать зеленым слово **Успешно** и откроется колонка учетной записи хранения, в которой будет видно, что учетная запись принадлежит к созданной вами группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="bc182-143">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="bc182-144">Щелкните элемент **Ключи доступа** в колонке учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="bc182-144">Click the **Access Keys** part in the storage account's blade.</span></span> <span data-ttu-id="bc182-145">Запишите имя учетной записи и значение key1.</span><span class="sxs-lookup"><span data-stu-id="bc182-145">Take note of the account name and the key1.</span></span>
   
      ![ключей](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="bc182-147">Эта информация нам понадобится для настройки проекта в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="bc182-147">We will need this information to configure your project in the next section.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="bc182-148">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="bc182-148">Configure the Project</span></span>
<span data-ttu-id="bc182-149">В этом разделе мы настроим приложение для использования только что созданной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="bc182-149">In this section, we'll configure our application to use the storage account we just created.</span></span> <span data-ttu-id="bc182-150">Мы узнаем, как получить настройки соединения при помощи портала Azure.</span><span class="sxs-lookup"><span data-stu-id="bc182-150">We'll see how to obtain connection settings from the Azure Portal.</span></span> <span data-ttu-id="bc182-151">После этого мы запустим приложение локально.</span><span class="sxs-lookup"><span data-stu-id="bc182-151">Then we'll run the application locally.</span></span>

1. <span data-ttu-id="bc182-152">В Visual Studio щелкните правой кнопкой мыши узел проекта в обозревателе решений и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="bc182-152">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="bc182-153">Откройте вкладку **Отладка** .</span><span class="sxs-lookup"><span data-stu-id="bc182-153">Click on the **Debug** tab.</span></span>
   
     ![Параметры отладки проекта](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="bc182-155">Установите значения переменных среды для своего приложения в разделе **Команда отладки сервера** > **Среда**.</span><span class="sxs-lookup"><span data-stu-id="bc182-155">Set the values of environment variables required by the application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="bc182-156">В результате переменные среды будут заданы при **запуске отладки**.</span><span class="sxs-lookup"><span data-stu-id="bc182-156">This will set the environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="bc182-157">Чтобы настроить переменные для **запуска без отладки**, также установите необходимые значения в разделе **Команда запуска сервера**.</span><span class="sxs-lookup"><span data-stu-id="bc182-157">If you want the variables to be set when you **Start Without Debugging**, set the same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="bc182-158">Также можно определить значения переменных среды с помощью панели управления Windows.</span><span class="sxs-lookup"><span data-stu-id="bc182-158">Alternatively, you can define environment variables using the Windows Control Panel.</span></span> <span data-ttu-id="bc182-159">Это будет наилучшим решением, если вы не желаете хранить учетные данные в исходном коде или файле проекта.</span><span class="sxs-lookup"><span data-stu-id="bc182-159">This is a better option if you want to avoid storing credentials in source code / project file.</span></span> <span data-ttu-id="bc182-160">Чтобы новые значения переменных стали доступными для приложения, будет необходимо перезапустить Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc182-160">Note that you will need to restart Visual Studio for the new environment values to be available to the application.</span></span>
3. <span data-ttu-id="bc182-161">Код с реализацией репозитория хранилища таблиц Azure находится в файле **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="bc182-161">The code that implements the Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="bc182-162">Дополнительные сведения о том, как использовать службу табличного хранилища в Python, см. в [документации].</span><span class="sxs-lookup"><span data-stu-id="bc182-162">See the [documentation] for more information on how to use Table Service from Python.</span></span>
4. <span data-ttu-id="bc182-163">Запустите приложение, нажав клавишу `F5`.</span><span class="sxs-lookup"><span data-stu-id="bc182-163">Run the application with `F5`.</span></span> <span data-ttu-id="bc182-164">Опросы, созданные с помощью команды **Создать примеры опросов** , и отправленные при голосовании данные будут сериализованы в табличном хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="bc182-164">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bc182-165">Виртуальная среда Python 2.7 может вызвать исключение в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc182-165">The Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="bc182-166">Нажмите клавишу `F5` , чтобы продолжить загрузку веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="bc182-166">Press `F5` to continue loading the web project.</span></span>
   > 
   > 
5. <span data-ttu-id="bc182-167">Перейдите на страницу **О программе**, чтобы убедиться в том, что приложение использует репозиторий **хранилища таблиц Azure**.</span><span class="sxs-lookup"><span data-stu-id="bc182-167">Browse to the **About** page to verify that the application is using the **Azure Table Storage** repository.</span></span>
   
     ![Веб-браузер](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageAbout.png)

## <a name="explore-the-azure-table-storage"></a><span data-ttu-id="bc182-169">Знакомство с хранилищем таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="bc182-169">Explore the Azure Table Storage</span></span>
<span data-ttu-id="bc182-170">Таблицы хранилища легко просматривать и редактировать с помощью Cloud Explorer в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc182-170">It's easy to view and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="bc182-171">В этом разделе мы будем использовать обозреватель сервера для просмотра содержимого таблиц приложения опросника.</span><span class="sxs-lookup"><span data-stu-id="bc182-171">In this section we'll use Server Explorer to view the contents of the polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="bc182-172">Для этого требуется установить инструменты Microsoft Azure, которые доступны в составе пакета [SDK для Azure для .NET].</span><span class="sxs-lookup"><span data-stu-id="bc182-172">This requires Microsoft Azure Tools to be installed, which are available as part of the [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="bc182-173">Откройте **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="bc182-173">Open **Cloud Explorer**.</span></span> <span data-ttu-id="bc182-174">Разверните узел **Учетные записи хранения**, свою учетную запись хранения, а затем узел **Таблицы**.</span><span class="sxs-lookup"><span data-stu-id="bc182-174">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="bc182-176">Дважды щелкните таблицу **опросов** или **вариантов**, чтобы просмотреть содержимое таблицы в окне документа, а также добавить, удалить или отредактировать записи.</span><span class="sxs-lookup"><span data-stu-id="bc182-176">Double-click on the **polls** or **choices** table to view the contents of the table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Результаты запросов таблицы](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="bc182-178">Публикация веб-приложения в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="bc182-178">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="bc182-179">С помощью пакета SDK для Azure для .NET можно легко развернуть веб-приложение в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="bc182-179">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="bc182-180">В **обозревателе решений** щелкните правой кнопкой мыши узел проекта и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="bc182-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
     ![Диалоговое окно «Публикация веб-сайта»](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="bc182-182">Щелкните **Веб-приложения Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="bc182-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="bc182-183">Нажмите **Создать** , чтобы создать новое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="bc182-183">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="bc182-184">Заполните перечисленные ниже поля и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="bc182-184">Fill in the following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="bc182-185">**Имя веб-приложения**</span><span class="sxs-lookup"><span data-stu-id="bc182-185">**Web App name**</span></span>
   * <span data-ttu-id="bc182-186">**План обслуживания приложения**</span><span class="sxs-lookup"><span data-stu-id="bc182-186">**App Service plan**</span></span>
   * <span data-ttu-id="bc182-187">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="bc182-187">**Resource group**</span></span>
   * <span data-ttu-id="bc182-188">**Регион**</span><span class="sxs-lookup"><span data-stu-id="bc182-188">**Region**</span></span>
   * <span data-ttu-id="bc182-189">Для параметра **Сервер базы данных** оставьте значение **Нет базы данных**.</span><span class="sxs-lookup"><span data-stu-id="bc182-189">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="bc182-190">Примите значения по умолчанию и щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="bc182-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="bc182-191">Опубликованное веб-приложение автоматически откроется в вашем браузере.</span><span class="sxs-lookup"><span data-stu-id="bc182-191">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="bc182-192">Если перейти на страницу "О программе", вы увидите, что используется размещенный **в памяти** репозиторий, а не репозиторий **хранилища таблиц Azure**.</span><span class="sxs-lookup"><span data-stu-id="bc182-192">If you browse to the about page, you'll see that it uses the **In-Memory** repository, not the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="bc182-193">Это объясняется тем, что переменные среды не устанавливаются на экземпляре веб-приложения Azure, поэтому используются значения по умолчанию, указанные в файле **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="bc182-193">That's because the environment variables are not set on the Web Apps instance in Azure App Service, so it uses the default values specified in **settings.py**.</span></span>

## <a name="configure-the-web-apps-instance"></a><span data-ttu-id="bc182-194">Настройка экземпляра веб-приложений</span><span class="sxs-lookup"><span data-stu-id="bc182-194">Configure the Web Apps instance</span></span>
<span data-ttu-id="bc182-195">В этом разделе мы настроим переменные среды для экземпляра веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="bc182-195">In this section, we'll configure environment variables for the Web Apps instance.</span></span>

1. <span data-ttu-id="bc182-196">На [портале Azure](https://portal.azure.com) откройте колонку веб-приложения, выбрав **Обзор** > **Службы приложений** > имя вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bc182-196">In [Azure Portal](https://portal.azure.com), open the web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="bc182-197">В колонке веб-приложения щелкните **Все параметры**, а затем — **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="bc182-197">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="bc182-198">Прокрутите список вниз до раздела **Параметры приложения** и присвойте переменным **REPOSITORY\_NAME**, **STORAGE\_NAME** и **STORAGE\_KEY** значения, описанные ранее в разделе **Настройка проекта**.</span><span class="sxs-lookup"><span data-stu-id="bc182-198">Scroll down to the **App settings** section and set the values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in the **Configure the project** section above.</span></span>
   
     ![Параметры приложения](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="bc182-200">Щелкните **Save**(Сохранить).</span><span class="sxs-lookup"><span data-stu-id="bc182-200">Click on **Save**.</span></span> <span data-ttu-id="bc182-201">После получения уведомлений о том, что изменения были применены, щелкните **Обзор** в главной колонке веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bc182-201">After you've received the notifications that the changes were applied, click on **Browse** from the Web app main blade.</span></span>
5. <span data-ttu-id="bc182-202">Вы должны увидеть, что веб-приложение работает корректно и использует репозиторий **табличного хранилища Azure** .</span><span class="sxs-lookup"><span data-stu-id="bc182-202">You should see the web app working as expected, using the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="bc182-203">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="bc182-203">Congratulations!</span></span>
   
     ![Веб-браузер](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="bc182-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bc182-205">Next steps</span></span>
<span data-ttu-id="bc182-206">Для получения более подробной информации о средствах Python для Visual Studio, Flask и хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="bc182-206">Follow these links to learn more about Python Tools for Visual Studio, Flask and Azure Table Storage.</span></span>

* <span data-ttu-id="bc182-207">[Документация по средствам Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="bc182-207">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="bc182-208">[Веб-проекты]</span><span class="sxs-lookup"><span data-stu-id="bc182-208">[Web Projects]</span></span>
  * <span data-ttu-id="bc182-209">[Проекты для облачной службы]</span><span class="sxs-lookup"><span data-stu-id="bc182-209">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="bc182-210">[Удаленная отладка в Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="bc182-210">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="bc182-211">[Документация по Flask]</span><span class="sxs-lookup"><span data-stu-id="bc182-211">[Flask Documentation]</span></span>
* <span data-ttu-id="bc182-212">[Хранилище Azure]</span><span class="sxs-lookup"><span data-stu-id="bc182-212">[Azure Storage]</span></span>
* <span data-ttu-id="bc182-213">[Пакет SDK для Azure для Python]</span><span class="sxs-lookup"><span data-stu-id="bc182-213">[Azure SDK for Python]</span></span>
* <span data-ttu-id="bc182-214">[Как использовать службу табличного хранилища в Python]</span><span class="sxs-lookup"><span data-stu-id="bc182-214">[How to Use the Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="bc182-215">Изменения</span><span class="sxs-lookup"><span data-stu-id="bc182-215">What's changed</span></span>
* <span data-ttu-id="bc182-216">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="bc182-216">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Центр по разработке для Python]: /develop/python/
[облачных служб Azure]: ../cloud-services/cloud-services-python-ptvs.md
[документации]:../cosmos-db/table-storage-how-to-use-python.md
[Как использовать службу табличного хранилища в Python]:../cosmos-db/table-storage-how-to-use-python.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[SDK для Azure для .NET]: http://azure.microsoft.com/downloads/
[Средства Python для Visual Studio]: http://aka.ms/ptvs
[Инструменты Python 2.2 для Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Образцы VSIX средств Python 2.2 для Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Инструменты пакета SDK для Azure для Visual Studio 2015]: http://go.microsoft.com/fwlink/?linkid=518003
[Python 2.7 (32-разрядная версия)]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 (32-разрядная версия)]: http://go.microsoft.com/fwlink/?LinkId=517191
[Документация по средствам Python для Visual Studio]: http://aka.ms/ptvsdocs
[Документация по Flask]: http://flask.pocoo.org/
[Удаленная отладка в Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Веб-проекты]: http://go.microsoft.com/fwlink/?LinkId=624027
[Проекты для облачной службы]: http://go.microsoft.com/fwlink/?LinkId=624028
[Хранилище Azure]: http://azure.microsoft.com/documentation/services/storage/
[Пакет SDK для Azure для Python]: https://github.com/Azure/azure-sdk-for-python
