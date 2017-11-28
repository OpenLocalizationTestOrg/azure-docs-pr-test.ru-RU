---
title: "Использование Bottle и табличного хранилища Azure в Azure с помощью инструментов Python 2.2 для Visual Studio"
description: "Информация о том, как создать приложение Bottle, которое хранит данные в табличном хранилище Azure, с помощью инструментов Python для Visual Studio и развернуть его в веб-приложениях службы приложений Azure."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: f075124b-db79-4e51-b394-09187dd6c634
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: fb25f03607ac6e9af46b47f54e830e0283dd1b0a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="27c85-103">Использование Bottle и табличного хранилища Azure в Azure с помощью инструментов Python 2.2 для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="27c85-103">Bottle and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="27c85-104">В этом учебнике мы используем [Средства Python для Visual Studio] , чтобы создать простое веб-приложение опросника с помощью шаблонов PTVS.</span><span class="sxs-lookup"><span data-stu-id="27c85-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="27c85-105">Также доступна [видеоверсия](https://www.youtube.com/watch?v=GJXDGaEPy94)этого учебника.</span><span class="sxs-lookup"><span data-stu-id="27c85-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span></span>

<span data-ttu-id="27c85-106">Веб-приложение опросника реализует абстракцию для своего репозитория, что позволяет легко переключаться между разными типами репозиториев (размещенный в памяти, табличном хранилище Azure или MongoDB).</span><span class="sxs-lookup"><span data-stu-id="27c85-106">The polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="27c85-107">Вы узнаете, как создать учетную запись хранения Azure и настроить веб-приложение для использования табличного хранилища Azure, а также как опубликовать приложение в [веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="27c85-107">We'll learn how to create an Azure Storage account, how to configure the web app to use Azure Table Storage, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="27c85-108">Зайдите в [Центр по разработке для Python] , где можно найти статьи о разработке веб-приложений службы приложений Azure с PTVS при помощи веб-платформ Bottle, Flask и Django, с использованием MongoDB, табличного хранилища Azure, MySQL и служб Базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="27c85-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="27c85-109">Хотя эта статья ориентирована в первую очередь на службу приложений, при разработке для [облачных служб Azure]используются аналогичные процедуры.</span><span class="sxs-lookup"><span data-stu-id="27c85-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27c85-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="27c85-110">Prerequisites</span></span>
* <span data-ttu-id="27c85-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="27c85-111">Visual Studio 2015</span></span>
* <span data-ttu-id="27c85-112">[Инструменты Python 2.2 для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="27c85-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="27c85-113">[Образцы VSIX средств Python 2.2 для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="27c85-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="27c85-114">[Инструменты пакета SDK для Azure для Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="27c85-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="27c85-115">[Python 2.7 (32-разрядная версия)] или [Python 3.4 (32-разрядная версия)]</span><span class="sxs-lookup"><span data-stu-id="27c85-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="27c85-116">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="27c85-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="27c85-117">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="27c85-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="27c85-118">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="27c85-118">Create the Project</span></span>
<span data-ttu-id="27c85-119">В этом разделе мы создадим проект Visual Studio с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="27c85-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="27c85-120">Мы создадим виртуальную среду и установим необходимые пакеты.</span><span class="sxs-lookup"><span data-stu-id="27c85-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="27c85-121">Затем мы запустим приложение локально в размещенном в памяти репозитории.</span><span class="sxs-lookup"><span data-stu-id="27c85-121">Then we'll run the application locally using the default in-memory repository.</span></span>

1. <span data-ttu-id="27c85-122">В Visual Studio выберите последовательно **Файл** и **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="27c85-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="27c85-123">Чтобы найти шаблоны [Образцы VSIX средств Python 2.2 для Visual Studio], в разделе **Python** выберите **Примеры**.</span><span class="sxs-lookup"><span data-stu-id="27c85-123">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="27c85-124">Выберите **Веб-проект опросов Bottle** и нажмите кнопку «ОК», чтобы создать проект.</span><span class="sxs-lookup"><span data-stu-id="27c85-124">Select **Polls Bottle Web Project** and click OK to create the project.</span></span>
   
     ![Диалоговое окно «Новый проект»](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. <span data-ttu-id="27c85-126">Вам будет предложено установить внешние пакеты.</span><span class="sxs-lookup"><span data-stu-id="27c85-126">You will be prompted to install external packages.</span></span> <span data-ttu-id="27c85-127">Выберите вариант **Установить в виртуальной среде**.</span><span class="sxs-lookup"><span data-stu-id="27c85-127">Select **Install into a virtual environment**.</span></span>
   
     ![Диалоговое окно «Внешние пакеты»](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. <span data-ttu-id="27c85-129">Выберите **Python 2.7** или **Python 3.4** в качестве базового интерпретатора.</span><span class="sxs-lookup"><span data-stu-id="27c85-129">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
     ![Диалоговое окно «Добавление виртуальной среды»](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="27c85-131">Убедитесь, что приложение работает, нажав клавишу `F5`.</span><span class="sxs-lookup"><span data-stu-id="27c85-131">Confirm that the application works by pressing `F5`.</span></span> <span data-ttu-id="27c85-132">По умолчанию приложение использует размещенный в памяти репозиторий, который не требует настройки.</span><span class="sxs-lookup"><span data-stu-id="27c85-132">By default, the application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="27c85-133">При остановке веб-сервера все данные будут утеряны.</span><span class="sxs-lookup"><span data-stu-id="27c85-133">All data is lost when the web server is stopped.</span></span>
6. <span data-ttu-id="27c85-134">Щелкните **Создать примеры опросов**, а затем выберите опросник, чтобы проголосовать.</span><span class="sxs-lookup"><span data-stu-id="27c85-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Веб-браузер](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="27c85-136">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="27c85-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="27c85-137">Для выполнения операций хранилища необходимо использовать учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="27c85-137">To use storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="27c85-138">Выполнив следующие шаги, вы создадите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="27c85-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="27c85-139">Войдите на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="27c85-139">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="27c85-140">В левом нижнем углу страницы щелкните значок **Создать** и выберите **Данные + хранилище** > **Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="27c85-140">Click the **New** icon on the top left of the Portal, then click **Data + Storage** > **Storage Account**.</span></span>  <span data-ttu-id="27c85-141">Нажмите кнопку **Создать**, присвойте учетной записи хранения уникальное имя и создайте для нее новую [группу ресурсов](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="27c85-141">Click the **Create** button, then give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Быстрое создание](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="27c85-143">После создания новой учетной записи на кнопке **Уведомления** начнет мигать зеленым слово **Успешно** и откроется колонка учетной записи хранения, в которой будет видно, что учетная запись принадлежит к созданной вами группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="27c85-143">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="27c85-144">Щелкните элемент **Ключи доступа** в колонке учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="27c85-144">Click the **Access keys** part in the storage account's blade.</span></span> <span data-ttu-id="27c85-145">Запишите имя учетной записи и значение key1.</span><span class="sxs-lookup"><span data-stu-id="27c85-145">Take note of the account name and key1.</span></span>
   
      ![ключей](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="27c85-147">Эта информация нам понадобится для настройки проекта в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="27c85-147">We will need this information to configure your project in the next section.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="27c85-148">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="27c85-148">Configure the Project</span></span>
<span data-ttu-id="27c85-149">В этом разделе мы настроим приложение для использования только что созданной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="27c85-149">In this section, we'll configure our application to use the storage account we just created.</span></span> <span data-ttu-id="27c85-150">После этого мы запустим приложение локально.</span><span class="sxs-lookup"><span data-stu-id="27c85-150">Then we'll run the application locally.</span></span>

1. <span data-ttu-id="27c85-151">В Visual Studio щелкните правой кнопкой мыши узел проекта в обозревателе решений и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="27c85-151">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="27c85-152">Откройте вкладку **Отладка** .</span><span class="sxs-lookup"><span data-stu-id="27c85-152">Click on the **Debug** tab.</span></span>
   
     ![Параметры отладки проекта](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="27c85-154">Установите значения переменных среды для своего приложения в разделе **Команда отладки сервера** > **Среда**.</span><span class="sxs-lookup"><span data-stu-id="27c85-154">Set the values of environment variables required by the application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="27c85-155">В результате переменные среды будут заданы при **запуске отладки**.</span><span class="sxs-lookup"><span data-stu-id="27c85-155">This will set the environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="27c85-156">Чтобы настроить переменные для **запуска без отладки**, также установите необходимые значения в разделе **Команда запуска сервера**.</span><span class="sxs-lookup"><span data-stu-id="27c85-156">If you want the variables to be set when you **Start Without Debugging**, set the same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="27c85-157">Также можно определить значения переменных среды с помощью панели управления Windows.</span><span class="sxs-lookup"><span data-stu-id="27c85-157">Alternatively, you can define environment variables using the Windows Control Panel.</span></span> <span data-ttu-id="27c85-158">Это будет наилучшим решением, если вы не желаете хранить учетные данные в исходном коде или файле проекта.</span><span class="sxs-lookup"><span data-stu-id="27c85-158">This is a better option if you want to avoid storing credentials in source code / project file.</span></span> <span data-ttu-id="27c85-159">Чтобы новые значения переменных стали доступными для приложения, будет необходимо перезапустить Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="27c85-159">Note that you will need to restart Visual Studio for the new environment values to be available to the application.</span></span>
3. <span data-ttu-id="27c85-160">Код с реализацией репозитория хранилища таблиц Azure находится в файле **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="27c85-160">The code that implements the Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="27c85-161">Дополнительные сведения о том, как использовать службу табличного хранилища в Python, см. в [документации].</span><span class="sxs-lookup"><span data-stu-id="27c85-161">See the [documentation] for more information on how to use Table Service from Python.</span></span>
4. <span data-ttu-id="27c85-162">Запустите приложение, нажав клавишу `F5`.</span><span class="sxs-lookup"><span data-stu-id="27c85-162">Run the application with `F5`.</span></span> <span data-ttu-id="27c85-163">Опросы, созданные с помощью команды **Создать примеры опросов** , и отправленные при голосовании данные будут сериализованы в табличном хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="27c85-163">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="27c85-164">Виртуальная среда Python 2.7 может вызвать исключение в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="27c85-164">The Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="27c85-165">Нажмите клавишу `F5` , чтобы продолжить загрузку веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="27c85-165">Press `F5` to continue loading the web project.</span></span>
   > 
   > 
5. <span data-ttu-id="27c85-166">Перейдите на страницу **О программе**, чтобы убедиться в том, что приложение использует репозиторий **хранилища таблиц Azure**.</span><span class="sxs-lookup"><span data-stu-id="27c85-166">Browse to the **About** page to verify that the application is using the **Azure Table Storage** repository.</span></span>
   
     ![Веб-браузер](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-the-azure-table-storage"></a><span data-ttu-id="27c85-168">Знакомство с хранилищем таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="27c85-168">Explore the Azure Table Storage</span></span>
<span data-ttu-id="27c85-169">Таблицы хранилища легко просматривать и редактировать с помощью Cloud Explorer в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="27c85-169">It's easy to view and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="27c85-170">В этом разделе мы будем использовать обозреватель сервера для просмотра содержимого таблиц приложения опросника.</span><span class="sxs-lookup"><span data-stu-id="27c85-170">In this section we'll use Server Explorer to view the contents of the polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="27c85-171">Для этого требуется установить инструменты Microsoft Azure, которые доступны в составе пакета [SDK для Azure для .NET].</span><span class="sxs-lookup"><span data-stu-id="27c85-171">This requires Microsoft Azure Tools to be installed, which are available as part of the [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="27c85-172">Откройте **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="27c85-172">Open **Cloud Explorer**.</span></span> <span data-ttu-id="27c85-173">Разверните узел **Учетные записи хранения**, свою учетную запись хранения, а затем узел **Таблицы**.</span><span class="sxs-lookup"><span data-stu-id="27c85-173">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="27c85-175">Дважды щелкните таблицу **опросов** или **вариантов**, чтобы просмотреть содержимое таблицы в окне документа, а также добавить, удалить или отредактировать записи.</span><span class="sxs-lookup"><span data-stu-id="27c85-175">Double-click on the **polls** or **choices** table to view the contents of the table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Результаты запросов таблицы](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="27c85-177">Публикация веб-приложения в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="27c85-177">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="27c85-178">С помощью пакета SDK для Azure для .NET можно легко развернуть веб-приложение в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="27c85-178">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="27c85-179">В **обозревателе решений** щелкните правой кнопкой мыши узел проекта и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="27c85-179">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
     ![Диалоговое окно «Публикация веб-сайта»](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="27c85-181">Щелкните **Веб-приложения Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="27c85-181">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="27c85-182">Нажмите **Создать** , чтобы создать новое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="27c85-182">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="27c85-183">Заполните перечисленные ниже поля и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="27c85-183">Fill in the following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="27c85-184">**Имя веб-приложения**</span><span class="sxs-lookup"><span data-stu-id="27c85-184">**Web App name**</span></span>
   * <span data-ttu-id="27c85-185">**План обслуживания приложения**</span><span class="sxs-lookup"><span data-stu-id="27c85-185">**App Service plan**</span></span>
   * <span data-ttu-id="27c85-186">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="27c85-186">**Resource group**</span></span>
   * <span data-ttu-id="27c85-187">**Регион**</span><span class="sxs-lookup"><span data-stu-id="27c85-187">**Region**</span></span>
   * <span data-ttu-id="27c85-188">Для параметра **Сервер базы данных** оставьте значение **Нет базы данных**.</span><span class="sxs-lookup"><span data-stu-id="27c85-188">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="27c85-189">Примите значения по умолчанию и щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="27c85-189">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="27c85-190">Опубликованное веб-приложение автоматически откроется в вашем браузере.</span><span class="sxs-lookup"><span data-stu-id="27c85-190">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="27c85-191">Если перейти на страницу "О программе", вы увидите, что используется размещенный **в памяти** репозиторий, а не репозиторий **хранилища таблиц Azure**.</span><span class="sxs-lookup"><span data-stu-id="27c85-191">If you browse to the about page, you'll see that it uses the **In-Memory** repository, not the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="27c85-192">Это объясняется тем, что переменные среды не устанавливаются на экземпляре веб-приложения Azure, поэтому используются значения по умолчанию, указанные в файле **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="27c85-192">That's because the environment variables are not set on the Web Apps instance in Azure App Service, so it uses the default values specified in **settings.py**.</span></span>

## <a name="configure-the-web-apps-instance"></a><span data-ttu-id="27c85-193">Настройка экземпляра веб-приложений</span><span class="sxs-lookup"><span data-stu-id="27c85-193">Configure the Web Apps instance</span></span>
<span data-ttu-id="27c85-194">В этом разделе мы настроим переменные среды для экземпляра веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="27c85-194">In this section, we'll configure environment variables for the Web Apps instance.</span></span>

1. <span data-ttu-id="27c85-195">На [портале Azure] откройте колонку веб-приложения, выбрав **Обзор** > **Службы приложений** > имя вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="27c85-195">In [Azure Portal], open the web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="27c85-196">В колонке веб-приложения щелкните **Все параметры**, а затем — **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="27c85-196">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="27c85-197">Прокрутите список вниз до раздела **Параметры приложения** и присвойте переменным **REPOSITORY\_NAME**, **STORAGE\_NAME** и **STORAGE\_KEY** значения, описанные ранее в разделе **Настройка проекта**.</span><span class="sxs-lookup"><span data-stu-id="27c85-197">Scroll down to the **App settings** section and set the values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in the **Configure the project** section above.</span></span>
   
     ![Параметры приложения](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="27c85-199">Щелкните **Save**(Сохранить).</span><span class="sxs-lookup"><span data-stu-id="27c85-199">Click on **Save**.</span></span> <span data-ttu-id="27c85-200">После получения уведомлений о том, что изменения были применены, щелкните **Обзор** в главной колонке веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="27c85-200">After you've received the notifications that the changes were applied, click on **Browse** from the Web app main blade.</span></span>
5. <span data-ttu-id="27c85-201">Вы должны увидеть, что веб-приложение работает корректно и использует репозиторий **табличного хранилища Azure** .</span><span class="sxs-lookup"><span data-stu-id="27c85-201">You should see the web app working as expected, using the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="27c85-202">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="27c85-202">Congratulations!</span></span>
   
     ![Веб-браузер](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="27c85-204">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="27c85-204">Next steps</span></span>
<span data-ttu-id="27c85-205">Используйте следующие ссылки, чтобы узнать больше об инструментах Python для Visual Studio, Bottle и табличном хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="27c85-205">Follow these links to learn more about Python Tools for Visual Studio, Bottle and Azure Table Storage.</span></span>

* <span data-ttu-id="27c85-206">[Документация по средствам Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="27c85-206">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="27c85-207">[Веб-проекты]</span><span class="sxs-lookup"><span data-stu-id="27c85-207">[Web Projects]</span></span>
  * <span data-ttu-id="27c85-208">[Проекты для облачной службы]</span><span class="sxs-lookup"><span data-stu-id="27c85-208">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="27c85-209">[Удаленная отладка в Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="27c85-209">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="27c85-210">[Документация по работе с Bottle]</span><span class="sxs-lookup"><span data-stu-id="27c85-210">[Bottle Documentation]</span></span>
* <span data-ttu-id="27c85-211">[Хранилище Azure]</span><span class="sxs-lookup"><span data-stu-id="27c85-211">[Azure Storage]</span></span>
* <span data-ttu-id="27c85-212">[Пакет SDK для Azure для Python]</span><span class="sxs-lookup"><span data-stu-id="27c85-212">[Azure SDK for Python]</span></span>
* <span data-ttu-id="27c85-213">[Как использовать службу табличного хранилища в Python]</span><span class="sxs-lookup"><span data-stu-id="27c85-213">[How to Use the Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="27c85-214">Изменения</span><span class="sxs-lookup"><span data-stu-id="27c85-214">What's changed</span></span>
* <span data-ttu-id="27c85-215">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="27c85-215">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Центр по разработке для Python]: /develop/python/
[облачных служб Azure]: ../cloud-services/cloud-services-python-ptvs.md
[документации]:../cosmos-db/table-storage-how-to-use-python.md
[Как использовать службу табличного хранилища в Python]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[портале Azure]: https://portal.azure.com
[SDK для Azure для .NET]: http://azure.microsoft.com/downloads/
[Средства Python для Visual Studio]: http://aka.ms/ptvs
[Инструменты Python 2.2 для Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[Образцы VSIX средств Python 2.2 для Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[Инструменты пакета SDK для Azure для Visual Studio 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 (32-разрядная версия)]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 (32-разрядная версия)]: http://go.microsoft.com/fwlink/?LinkId=517191
[Документация по средствам Python для Visual Studio]: http://aka.ms/ptvsdocs
[Документация по работе с Bottle]: http://bottlepy.org/docs/dev/index.html
[Удаленная отладка в Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Веб-проекты]: http://go.microsoft.com/fwlink/?LinkId=624027
[Проекты для облачной службы]: http://go.microsoft.com/fwlink/?LinkId=624028
[Хранилище Azure]: http://azure.microsoft.com/documentation/services/storage/
[Пакет SDK для Azure для Python]: https://github.com/Azure/azure-sdk-for-python
