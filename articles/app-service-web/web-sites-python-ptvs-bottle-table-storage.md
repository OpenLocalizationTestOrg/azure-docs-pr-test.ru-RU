---
title: "aaaBottle и хранилищем таблиц Azure в Azure с помощью средства Python 2.2 для Visual Studio"
description: "Узнайте, как toouse hello средства Python для Visual Studio toocreate Фляга для приложения, которое хранит данные в хранилище таблиц Azure и развернуть tooAzure приложения hello web App службы веб-приложений."
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
ms.openlocfilehash: 25b9eb002b8748483d5b9458b7b5860a958b4bb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="4552e-103">Использование Bottle и табличного хранилища Azure в Azure с помощью инструментов Python 2.2 для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4552e-103">Bottle and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="4552e-104">В этом учебнике мы будем использовать [средства Python для Visual Studio] toocreate простой опрашивает веб-приложения с помощью одного из шаблонов образец hello PTVS.</span><span class="sxs-lookup"><span data-stu-id="4552e-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="4552e-105">Также доступна [видеоверсия](https://www.youtube.com/watch?v=GJXDGaEPy94)этого учебника.</span><span class="sxs-lookup"><span data-stu-id="4552e-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span></span>

<span data-ttu-id="4552e-106">веб-приложения Hello опрашивает определяет абстракцию для своего репозитория легко переключаться между различными типами репозиториев (в памяти, хранилище таблиц Azure, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="4552e-106">hello polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="4552e-107">Будет рассматриваться как toocreate хранилища Azure учетной записи, как tooconfigure hello web app toouse табличного хранилища Azure и как toopublish hello веб-приложения слишком[веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="4552e-107">We'll learn how toocreate an Azure Storage account, how tooconfigure hello web app toouse Azure Table Storage, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="4552e-108">В разделе hello [центре разработчиков Python] Дополнительные статьи, посвященные разработки Azure приложение службы веб-приложений с помощью бутылка PTVS, термосе и Django веб-платформы с помощью службы MongoDB, хранилище таблиц Azure, MySQL и базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="4552e-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="4552e-109">Хотя данная статья посвящена службы приложений, hello шаги похожи, при разработке [облачных служб Azure].</span><span class="sxs-lookup"><span data-stu-id="4552e-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4552e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4552e-110">Prerequisites</span></span>
* <span data-ttu-id="4552e-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="4552e-111">Visual Studio 2015</span></span>
* <span data-ttu-id="4552e-112">[Инструменты Python 2.2 для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="4552e-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="4552e-113">[средства Python 2.2 для Visual Studio образцы VSIX]</span><span class="sxs-lookup"><span data-stu-id="4552e-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="4552e-114">[Инструменты пакета SDK для Azure для Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="4552e-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="4552e-115">[Python 2.7 (32-разрядная версия)] или [Python 3.4 (32-разрядная версия)]</span><span class="sxs-lookup"><span data-stu-id="4552e-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="4552e-116">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="4552e-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="4552e-117">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="4552e-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="4552e-118">Создание проекта hello</span><span class="sxs-lookup"><span data-stu-id="4552e-118">Create hello Project</span></span>
<span data-ttu-id="4552e-119">В этом разделе мы создадим проект Visual Studio с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="4552e-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="4552e-120">Мы создадим виртуальную среду и установим необходимые пакеты.</span><span class="sxs-lookup"><span data-stu-id="4552e-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="4552e-121">Затем мы выполним приложение hello локально с помощью репозитория в памяти по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="4552e-121">Then we'll run hello application locally using hello default in-memory repository.</span></span>

1. <span data-ttu-id="4552e-122">В Visual Studio выберите последовательно **Файл** и **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="4552e-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="4552e-123">Здравствуйте, шаблоны проектов из hello [средства Python 2.2 для Visual Studio образцы VSIX] можно найти в разделе **Python**, **образцы**.</span><span class="sxs-lookup"><span data-stu-id="4552e-123">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="4552e-124">Выберите **веб-проект Bottle опрашивает** и нажмите кнопку ОК toocreate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="4552e-124">Select **Polls Bottle Web Project** and click OK toocreate hello project.</span></span>
   
     ![Диалоговое окно "Новый проект"](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. <span data-ttu-id="4552e-126">Появится запрос tooinstall внешние пакеты.</span><span class="sxs-lookup"><span data-stu-id="4552e-126">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="4552e-127">Выберите вариант **Установить в виртуальной среде**.</span><span class="sxs-lookup"><span data-stu-id="4552e-127">Select **Install into a virtual environment**.</span></span>
   
     ![Диалоговое окно «Внешние пакеты»](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. <span data-ttu-id="4552e-129">Выберите **Python 2.7** или **Python 3.4** базовый интерпретатора hello.</span><span class="sxs-lookup"><span data-stu-id="4552e-129">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
     ![Диалоговое окно «Добавление виртуальной среды»](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="4552e-131">Убедитесь, что приложение hello работает, нажав клавишу `F5`.</span><span class="sxs-lookup"><span data-stu-id="4552e-131">Confirm that hello application works by pressing `F5`.</span></span> <span data-ttu-id="4552e-132">По умолчанию hello приложению репозитория в памяти, который не требует никакой настройки.</span><span class="sxs-lookup"><span data-stu-id="4552e-132">By default, hello application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="4552e-133">Все данные будут потеряны при остановке hello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="4552e-133">All data is lost when hello web server is stopped.</span></span>
6. <span data-ttu-id="4552e-134">Щелкните **Создать примеры опросов**, а затем выберите опросник, чтобы проголосовать.</span><span class="sxs-lookup"><span data-stu-id="4552e-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Веб-браузер](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="4552e-136">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="4552e-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="4552e-137">операции сохранения toouse, необходима учетная запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="4552e-137">toouse storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="4552e-138">Выполнив следующие шаги, вы создадите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="4552e-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="4552e-139">Войти в hello [портала Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4552e-139">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4552e-140">Нажмите кнопку hello **New** значок hello сверху слева от hello портала, нажмите кнопку **данные + хранилище** > **учетной записи хранилища**.</span><span class="sxs-lookup"><span data-stu-id="4552e-140">Click hello **New** icon on hello top left of hello Portal, then click **Data + Storage** > **Storage Account**.</span></span>  <span data-ttu-id="4552e-141">Нажмите кнопку hello **создать** кнопку, а затем укажите уникальное имя учетной записи хранилища hello и создайте новый [группы ресурсов](../azure-resource-manager/resource-group-overview.md) для него.</span><span class="sxs-lookup"><span data-stu-id="4552e-141">Click hello **Create** button, then give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Быстрое создание](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="4552e-143">При создании учетной записи хранилища hello hello **уведомления** кнопка будет мигать зеленым **успех** и учетной записи хранилища hello колонке открыт tooshow, что оно принадлежит новый ресурс toohello группы создать.</span><span class="sxs-lookup"><span data-stu-id="4552e-143">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="4552e-144">Нажмите кнопку hello **ключи доступа** часть — в колонке учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="4552e-144">Click hello **Access keys** part in hello storage account's blade.</span></span> <span data-ttu-id="4552e-145">Запишите имя учетной записи hello и key1.</span><span class="sxs-lookup"><span data-stu-id="4552e-145">Take note of hello account name and key1.</span></span>
   
      ![ключей](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="4552e-147">Нам понадобится этот tooconfigure сведения о проекте в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="4552e-147">We will need this information tooconfigure your project in hello next section.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="4552e-148">Настройка проекта hello</span><span class="sxs-lookup"><span data-stu-id="4552e-148">Configure hello Project</span></span>
<span data-ttu-id="4552e-149">В этом разделе мы настроим наши приложения toouse hello учетную запись хранилища, мы только что создали.</span><span class="sxs-lookup"><span data-stu-id="4552e-149">In this section, we'll configure our application toouse hello storage account we just created.</span></span> <span data-ttu-id="4552e-150">Затем мы выполним приложение hello локально.</span><span class="sxs-lookup"><span data-stu-id="4552e-150">Then we'll run hello application locally.</span></span>

1. <span data-ttu-id="4552e-151">В Visual Studio щелкните правой кнопкой мыши узел проекта в обозревателе решений и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="4552e-151">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="4552e-152">Щелкните hello **отладки** вкладки.</span><span class="sxs-lookup"><span data-stu-id="4552e-152">Click on hello **Debug** tab.</span></span>
   
     ![Параметры отладки проекта](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="4552e-154">Задать hello значения переменных среды, необходимые для приложения hello в **отлаживать команды Server**, **среды**.</span><span class="sxs-lookup"><span data-stu-id="4552e-154">Set hello values of environment variables required by hello application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="4552e-155">Это задаст переменные среды hello при вы **начать отладку**.</span><span class="sxs-lookup"><span data-stu-id="4552e-155">This will set hello environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="4552e-156">Переменные toobe hello задайте при вы **Запуск без отладки**, набор hello же значения в разделе **выполнение команды сервера** также.</span><span class="sxs-lookup"><span data-stu-id="4552e-156">If you want hello variables toobe set when you **Start Without Debugging**, set hello same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="4552e-157">Кроме того можно определить переменные среды, с помощью панели управления Windows hello.</span><span class="sxs-lookup"><span data-stu-id="4552e-157">Alternatively, you can define environment variables using hello Windows Control Panel.</span></span> <span data-ttu-id="4552e-158">Это является лучшим вариантом, если файл проекта tooavoid хранение учетных данных в исходном коде.</span><span class="sxs-lookup"><span data-stu-id="4552e-158">This is a better option if you want tooavoid storing credentials in source code / project file.</span></span> <span data-ttu-id="4552e-159">Обратите внимание, что вам потребуется toorestart Visual Studio для новой среды hello значения toobe toohello доступных приложений.</span><span class="sxs-lookup"><span data-stu-id="4552e-159">Note that you will need toorestart Visual Studio for hello new environment values toobe available toohello application.</span></span>
3. <span data-ttu-id="4552e-160">Hello код, который реализует репозитория hello табличного хранилища Azure находится в **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="4552e-160">hello code that implements hello Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="4552e-161">В разделе hello [документации] Дополнительные сведения о том, как toouse службы таблиц из Python.</span><span class="sxs-lookup"><span data-stu-id="4552e-161">See hello [documentation] for more information on how toouse Table Service from Python.</span></span>
4. <span data-ttu-id="4552e-162">Запустите приложение hello с `F5`.</span><span class="sxs-lookup"><span data-stu-id="4552e-162">Run hello application with `F5`.</span></span> <span data-ttu-id="4552e-163">Опросы, созданных с помощью **создать образец опрашивает** и hello данные, переданные с правом голоса сериализуются в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="4552e-163">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4552e-164">Hello Python 2.7 виртуальной среды может привести к на разрыв исключений в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4552e-164">hello Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="4552e-165">Нажмите клавишу `F5` toocontinue загрузке hello веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="4552e-165">Press `F5` toocontinue loading hello web project.</span></span>
   > 
   > 
5. <span data-ttu-id="4552e-166">Обзор toohello **о** tooverify страницы, hello приложение использует hello **табличного хранилища Azure** репозитория.</span><span class="sxs-lookup"><span data-stu-id="4552e-166">Browse toohello **About** page tooverify that hello application is using hello **Azure Table Storage** repository.</span></span>
   
     ![Веб-браузер](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a><span data-ttu-id="4552e-168">Просмотр hello табличного хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="4552e-168">Explore hello Azure Table Storage</span></span>
<span data-ttu-id="4552e-169">Он просто tooview и редактирование таблиц хранилища с помощью Cloud Explorer в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4552e-169">It's easy tooview and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="4552e-170">В этом разделе мы будем использовать обозреватель серверов tooview hello содержимого таблиц приложений опрашивает hello.</span><span class="sxs-lookup"><span data-stu-id="4552e-170">In this section we'll use Server Explorer tooview hello contents of hello polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="4552e-171">Это требует toobe инструментов Microsoft Azure установлены, они доступны как часть hello [Azure SDK для .NET].</span><span class="sxs-lookup"><span data-stu-id="4552e-171">This requires Microsoft Azure Tools toobe installed, which are available as part of hello [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="4552e-172">Откройте **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="4552e-172">Open **Cloud Explorer**.</span></span> <span data-ttu-id="4552e-173">Разверните узел **Учетные записи хранения**, свою учетную запись хранения, а затем узел **Таблицы**.</span><span class="sxs-lookup"><span data-stu-id="4552e-173">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="4552e-175">Дважды щелкните hello **опрашивает** или **варианты** таблице tooview hello содержимое таблицы hello в окне документа, а также добавления, удаления и изменения сущностей.</span><span class="sxs-lookup"><span data-stu-id="4552e-175">Double-click on hello **polls** or **choices** table tooview hello contents of hello table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Результаты запросов таблицы](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="4552e-177">Публикация hello web app tooAzure службы приложений</span><span class="sxs-lookup"><span data-stu-id="4552e-177">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="4552e-178">Hello Azure .NET SDK предоставляет простой способ toodeploy вашей web app tooAzure службы приложений.</span><span class="sxs-lookup"><span data-stu-id="4552e-178">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="4552e-179">В **обозревателе решений**, правой кнопкой мыши узел проекта hello и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="4552e-179">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
     ![Диалоговое окно «Публикация веб-сайта»](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="4552e-181">Щелкните **Веб-приложения Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="4552e-181">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="4552e-182">Щелкните **New** toocreate новое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="4552e-182">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="4552e-183">Заполните следующие поля hello и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="4552e-183">Fill in hello following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="4552e-184">**Имя веб-приложения**</span><span class="sxs-lookup"><span data-stu-id="4552e-184">**Web App name**</span></span>
   * <span data-ttu-id="4552e-185">**План обслуживания приложения**</span><span class="sxs-lookup"><span data-stu-id="4552e-185">**App Service plan**</span></span>
   * <span data-ttu-id="4552e-186">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="4552e-186">**Resource group**</span></span>
   * <span data-ttu-id="4552e-187">**Регион**</span><span class="sxs-lookup"><span data-stu-id="4552e-187">**Region**</span></span>
   * <span data-ttu-id="4552e-188">Оставить **сервера базы данных** значение слишком**ни одной базы данных**</span><span class="sxs-lookup"><span data-stu-id="4552e-188">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="4552e-189">Примите значения по умолчанию и щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="4552e-189">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="4552e-190">Веб-браузере откроется автоматически toohello опубликованных веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4552e-190">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="4552e-191">При просмотре toohello о странице вы увидите, что он использует hello **в памяти** репозитория, не hello **табличного хранилища Azure** репозитория.</span><span class="sxs-lookup"><span data-stu-id="4552e-191">If you browse toohello about page, you'll see that it uses hello **In-Memory** repository, not hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="4552e-192">Это потому, что hello переменные среды не установлены hello экземпляр веб-приложений в службе приложений Azure, поэтому он использует значения по умолчанию hello в **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="4552e-192">That's because hello environment variables are not set on hello Web Apps instance in Azure App Service, so it uses hello default values specified in **settings.py**.</span></span>

## <a name="configure-hello-web-apps-instance"></a><span data-ttu-id="4552e-193">Настройка экземпляра веб-приложения hello</span><span class="sxs-lookup"><span data-stu-id="4552e-193">Configure hello Web Apps instance</span></span>
<span data-ttu-id="4552e-194">В этом разделе мы настроим переменные среды для экземпляра веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4552e-194">In this section, we'll configure environment variables for hello Web Apps instance.</span></span>

1. <span data-ttu-id="4552e-195">В [портала Azure], откройте колонку hello веб-приложение, нажав **Обзор** > **службы приложений** > имя вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4552e-195">In [Azure Portal], open hello web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="4552e-196">В колонке веб-приложения щелкните **Все параметры**, а затем — **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="4552e-196">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="4552e-197">Прокрутите вниз toohello **параметры приложения** статьи и задание значений hello для **РЕПОЗИТОРИЯ\_имя**, **ХРАНЕНИЯ\_имя** и  **ХРАНИЛИЩЕ\_ключ** согласно инструкциям hello **проекта hello Настройка** выше.</span><span class="sxs-lookup"><span data-stu-id="4552e-197">Scroll down toohello **App settings** section and set hello values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in hello **Configure hello project** section above.</span></span>
   
     ![Параметры приложения](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="4552e-199">Щелкните **Save**(Сохранить).</span><span class="sxs-lookup"><span data-stu-id="4552e-199">Click on **Save**.</span></span> <span data-ttu-id="4552e-200">После получил уведомления hello применения hello изменения, выберите команду **Обзор** из колонки основного приложения Web hello.</span><span class="sxs-lookup"><span data-stu-id="4552e-200">After you've received hello notifications that hello changes were applied, click on **Browse** from hello Web app main blade.</span></span>
5. <span data-ttu-id="4552e-201">Вы увидите рабочее приложение hello web, как и ожидалось, с помощью hello **табличного хранилища Azure** репозитория.</span><span class="sxs-lookup"><span data-stu-id="4552e-201">You should see hello web app working as expected, using hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="4552e-202">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="4552e-202">Congratulations!</span></span>
   
     ![Веб-браузер](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="4552e-204">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4552e-204">Next steps</span></span>
<span data-ttu-id="4552e-205">Выполните эти ссылки toolearn Дополнительные сведения о средствах Python для Visual Studio, бутылка и табличного хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="4552e-205">Follow these links toolearn more about Python Tools for Visual Studio, Bottle and Azure Table Storage.</span></span>

* <span data-ttu-id="4552e-206">[Документация по средствам Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="4552e-206">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="4552e-207">[Веб-проекты]</span><span class="sxs-lookup"><span data-stu-id="4552e-207">[Web Projects]</span></span>
  * <span data-ttu-id="4552e-208">[Проекты для облачной службы]</span><span class="sxs-lookup"><span data-stu-id="4552e-208">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="4552e-209">[Удаленная отладка в Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="4552e-209">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="4552e-210">[Документация по работе с Bottle]</span><span class="sxs-lookup"><span data-stu-id="4552e-210">[Bottle Documentation]</span></span>
* <span data-ttu-id="4552e-211">[Хранилище Azure]</span><span class="sxs-lookup"><span data-stu-id="4552e-211">[Azure Storage]</span></span>
* <span data-ttu-id="4552e-212">[Пакет SDK для Azure для Python]</span><span class="sxs-lookup"><span data-stu-id="4552e-212">[Azure SDK for Python]</span></span>
* <span data-ttu-id="4552e-213">[Как tooUse hello службы хранения таблиц из Python]</span><span class="sxs-lookup"><span data-stu-id="4552e-213">[How tooUse hello Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="4552e-214">Изменения</span><span class="sxs-lookup"><span data-stu-id="4552e-214">What's changed</span></span>
* <span data-ttu-id="4552e-215">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="4552e-215">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[центре разработчиков Python]: /develop/python/
[облачных служб Azure]: ../cloud-services/cloud-services-python-ptvs.md
[документации]:../cosmos-db/table-storage-how-to-use-python.md
[Как tooUse hello службы хранения таблиц из Python]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[портала Azure]: https://portal.azure.com
[Azure SDK для .NET]: http://azure.microsoft.com/downloads/
[средства Python для Visual Studio]: http://aka.ms/ptvs
[Инструменты Python 2.2 для Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[средства Python 2.2 для Visual Studio образцы VSIX]: http://go.microsoft.com/fwlink/?LinkId=624025
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
