---
title: "aaaFlask и хранилищем таблиц Azure в Azure с помощью средства Python 2.2 для Visual Studio"
description: "Узнайте, как toouse hello средства Python для Visual Studio toocreate термосе веб-приложения, который сохраняет данные в хранилище таблиц Azure и развернуть ее tooAzure приложения службы веб-приложений."
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
ms.openlocfilehash: 1a09d4cc78078a00492ba4fe7e2075df96fb0380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="flask-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="218a3-103">Flask и хранилище таблиц Azure с использованием инструментов Python 2.2 для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="218a3-103">Flask and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="218a3-104">В этом учебнике мы будем использовать [средства Python для Visual Studio] toocreate простой опрашивает веб-приложения с помощью одного из шаблонов образец hello PTVS.</span><span class="sxs-lookup"><span data-stu-id="218a3-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="218a3-105">Также доступна [видеоверсия](https://www.youtube.com/watch?v=qUtZWtPwbTk)этого учебника.</span><span class="sxs-lookup"><span data-stu-id="218a3-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span></span>

<span data-ttu-id="218a3-106">веб-приложения Hello опрашивает определяет абстракцию для своего репозитория легко переключаться между различными типами репозиториев (в памяти, хранилище таблиц Azure, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="218a3-106">hello polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="218a3-107">Будет рассматриваться как toocreate хранилища Azure учетной записи, как tooconfigure hello web app toouse табличного хранилища Azure и как toopublish hello веб-приложения слишком[веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="218a3-107">We'll learn how toocreate an Azure Storage account, how tooconfigure hello web app toouse Azure Table Storage, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="218a3-108">В разделе hello [центре разработчиков Python] Дополнительные статьи, посвященные разработки Azure приложение службы веб-приложений с помощью бутылка PTVS, термосе и Django веб-платформы с помощью службы MongoDB, хранилище таблиц Azure, MySQL и базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="218a3-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="218a3-109">Хотя данная статья посвящена службы приложений, hello шаги похожи, при разработке [облачных служб Azure].</span><span class="sxs-lookup"><span data-stu-id="218a3-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="218a3-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="218a3-110">Prerequisites</span></span>
* <span data-ttu-id="218a3-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="218a3-111">Visual Studio 2015</span></span>
* <span data-ttu-id="218a3-112">[Инструменты Python 2.2 для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="218a3-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="218a3-113">[средства Python 2.2 для Visual Studio образцы VSIX]</span><span class="sxs-lookup"><span data-stu-id="218a3-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="218a3-114">[Инструменты пакета SDK для Azure для Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="218a3-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="218a3-115">[Python 2.7 (32-разрядная версия)] или [Python 3.4 (32-разрядная версия)]</span><span class="sxs-lookup"><span data-stu-id="218a3-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="218a3-116">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="218a3-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="218a3-117">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="218a3-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="218a3-118">Создание проекта hello</span><span class="sxs-lookup"><span data-stu-id="218a3-118">Create hello Project</span></span>
<span data-ttu-id="218a3-119">В этом разделе мы создадим проект Visual Studio с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="218a3-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="218a3-120">Мы создадим виртуальную среду и установим необходимые пакеты.</span><span class="sxs-lookup"><span data-stu-id="218a3-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="218a3-121">Затем мы выполним приложение hello локально с помощью репозитория в памяти по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="218a3-121">Then we'll run hello application locally using hello default in-memory repository.</span></span>

1. <span data-ttu-id="218a3-122">В Visual Studio выберите последовательно **Файл** и **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="218a3-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="218a3-123">Здравствуйте, шаблоны проектов из hello [средства Python 2.2 для Visual Studio образцы VSIX] можно найти в разделе **Python**, **образцы**.</span><span class="sxs-lookup"><span data-stu-id="218a3-123">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="218a3-124">Выберите **опрашивает термосе веб-проекта** и нажмите кнопку ОК toocreate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="218a3-124">Select **Polls Flask Web Project** and click OK toocreate hello project.</span></span>
   
     ![Диалоговое окно "Новый проект"](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskNewProject.png)
3. <span data-ttu-id="218a3-126">Появится запрос tooinstall внешние пакеты.</span><span class="sxs-lookup"><span data-stu-id="218a3-126">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="218a3-127">Выберите вариант **Установить в виртуальной среде**.</span><span class="sxs-lookup"><span data-stu-id="218a3-127">Select **Install into a virtual environment**.</span></span>
   
     ![Диалоговое окно «Внешние пакеты»](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskExternalPackages.png)
4. <span data-ttu-id="218a3-129">Выберите **Python 2.7** или **Python 3.4** базовый интерпретатора hello.</span><span class="sxs-lookup"><span data-stu-id="218a3-129">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
     ![Диалоговое окно «Добавление виртуальной среды»](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="218a3-131">Убедитесь, что приложение hello работает, нажав клавишу `F5`.</span><span class="sxs-lookup"><span data-stu-id="218a3-131">Confirm that hello application works by pressing `F5`.</span></span> <span data-ttu-id="218a3-132">По умолчанию hello приложению репозитория в памяти, который не требует никакой настройки.</span><span class="sxs-lookup"><span data-stu-id="218a3-132">By default, hello application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="218a3-133">Все данные будут потеряны при остановке hello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="218a3-133">All data is lost when hello web server is stopped.</span></span>
6. <span data-ttu-id="218a3-134">Щелкните **Создать примеры опросов**, а затем выберите опросник, чтобы проголосовать.</span><span class="sxs-lookup"><span data-stu-id="218a3-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Веб-браузер](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="218a3-136">Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="218a3-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="218a3-137">операции сохранения toouse, необходима учетная запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="218a3-137">toouse storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="218a3-138">Выполнив следующие шаги, вы создадите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="218a3-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="218a3-139">Войти в hello [портала Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="218a3-139">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="218a3-140">Нажмите кнопку hello **New** значок hello сверху слева от hello портала, нажмите кнопку **данные + хранилище** > **учетной записи хранилища**.</span><span class="sxs-lookup"><span data-stu-id="218a3-140">Click hello **New** icon on hello top left of hello Portal, then click **Data + Storage** > **Storage Account**.</span></span> <span data-ttu-id="218a3-141">Щелкните **создать**, укажите уникальное имя учетной записи хранилища hello и создать новую [группы ресурсов](../azure-resource-manager/resource-group-overview.md) для него.</span><span class="sxs-lookup"><span data-stu-id="218a3-141">Click on **Create**, then give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Быстрое создание](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="218a3-143">При создании учетной записи хранилища hello hello **уведомления** кнопка будет мигать зеленым **успех** и учетной записи хранилища hello колонке открыт tooshow, что оно принадлежит новый ресурс toohello группы создать.</span><span class="sxs-lookup"><span data-stu-id="218a3-143">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="218a3-144">Нажмите кнопку hello **клавиши доступа** часть — в колонке учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="218a3-144">Click hello **Access Keys** part in hello storage account's blade.</span></span> <span data-ttu-id="218a3-145">Запишите имя учетной записи hello и hello key1.</span><span class="sxs-lookup"><span data-stu-id="218a3-145">Take note of hello account name and hello key1.</span></span>
   
      ![ключей](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="218a3-147">Нам понадобится этот tooconfigure сведения о проекте в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="218a3-147">We will need this information tooconfigure your project in hello next section.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="218a3-148">Настройка проекта hello</span><span class="sxs-lookup"><span data-stu-id="218a3-148">Configure hello Project</span></span>
<span data-ttu-id="218a3-149">В этом разделе мы настроим наши приложения toouse hello учетную запись хранилища, мы только что создали.</span><span class="sxs-lookup"><span data-stu-id="218a3-149">In this section, we'll configure our application toouse hello storage account we just created.</span></span> <span data-ttu-id="218a3-150">Мы рассмотрим, как параметры подключения tooobtain hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="218a3-150">We'll see how tooobtain connection settings from hello Azure Portal.</span></span> <span data-ttu-id="218a3-151">Затем мы выполним приложение hello локально.</span><span class="sxs-lookup"><span data-stu-id="218a3-151">Then we'll run hello application locally.</span></span>

1. <span data-ttu-id="218a3-152">В Visual Studio щелкните правой кнопкой мыши узел проекта в обозревателе решений и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="218a3-152">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="218a3-153">Щелкните hello **отладки** вкладки.</span><span class="sxs-lookup"><span data-stu-id="218a3-153">Click on hello **Debug** tab.</span></span>
   
     ![Параметры отладки проекта](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="218a3-155">Задать hello значения переменных среды, необходимые для приложения hello в **отлаживать команды Server**, **среды**.</span><span class="sxs-lookup"><span data-stu-id="218a3-155">Set hello values of environment variables required by hello application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="218a3-156">Это задаст переменные среды hello при вы **начать отладку**.</span><span class="sxs-lookup"><span data-stu-id="218a3-156">This will set hello environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="218a3-157">Переменные toobe hello задайте при вы **Запуск без отладки**, набор hello же значения в разделе **выполнение команды сервера** также.</span><span class="sxs-lookup"><span data-stu-id="218a3-157">If you want hello variables toobe set when you **Start Without Debugging**, set hello same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="218a3-158">Кроме того можно определить переменные среды, с помощью панели управления Windows hello.</span><span class="sxs-lookup"><span data-stu-id="218a3-158">Alternatively, you can define environment variables using hello Windows Control Panel.</span></span> <span data-ttu-id="218a3-159">Это является лучшим вариантом, если файл проекта tooavoid хранение учетных данных в исходном коде.</span><span class="sxs-lookup"><span data-stu-id="218a3-159">This is a better option if you want tooavoid storing credentials in source code / project file.</span></span> <span data-ttu-id="218a3-160">Обратите внимание, что вам потребуется toorestart Visual Studio для новой среды hello значения toobe toohello доступных приложений.</span><span class="sxs-lookup"><span data-stu-id="218a3-160">Note that you will need toorestart Visual Studio for hello new environment values toobe available toohello application.</span></span>
3. <span data-ttu-id="218a3-161">Hello код, который реализует репозитория hello табличного хранилища Azure находится в **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="218a3-161">hello code that implements hello Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="218a3-162">В разделе hello [документации] Дополнительные сведения о том, как toouse службы таблиц из Python.</span><span class="sxs-lookup"><span data-stu-id="218a3-162">See hello [documentation] for more information on how toouse Table Service from Python.</span></span>
4. <span data-ttu-id="218a3-163">Запустите приложение hello с `F5`.</span><span class="sxs-lookup"><span data-stu-id="218a3-163">Run hello application with `F5`.</span></span> <span data-ttu-id="218a3-164">Опросы, созданных с помощью **создать образец опрашивает** и hello данные, переданные с правом голоса сериализуются в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="218a3-164">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="218a3-165">Hello Python 2.7 виртуальной среды может привести к на разрыв исключений в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="218a3-165">hello Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="218a3-166">Нажмите клавишу `F5` toocontinue загрузке hello веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="218a3-166">Press `F5` toocontinue loading hello web project.</span></span>
   > 
   > 
5. <span data-ttu-id="218a3-167">Обзор toohello **о** tooverify страницы, hello приложение использует hello **табличного хранилища Azure** репозитория.</span><span class="sxs-lookup"><span data-stu-id="218a3-167">Browse toohello **About** page tooverify that hello application is using hello **Azure Table Storage** repository.</span></span>
   
     ![Веб-браузер](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a><span data-ttu-id="218a3-169">Просмотр hello табличного хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="218a3-169">Explore hello Azure Table Storage</span></span>
<span data-ttu-id="218a3-170">Он просто tooview и редактирование таблиц хранилища с помощью Cloud Explorer в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="218a3-170">It's easy tooview and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="218a3-171">В этом разделе мы будем использовать обозреватель серверов tooview hello содержимого таблиц приложений опрашивает hello.</span><span class="sxs-lookup"><span data-stu-id="218a3-171">In this section we'll use Server Explorer tooview hello contents of hello polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="218a3-172">Это требует toobe инструментов Microsoft Azure установлены, они доступны как часть hello [Azure SDK для .NET].</span><span class="sxs-lookup"><span data-stu-id="218a3-172">This requires Microsoft Azure Tools toobe installed, which are available as part of hello [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="218a3-173">Откройте **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="218a3-173">Open **Cloud Explorer**.</span></span> <span data-ttu-id="218a3-174">Разверните узел **Учетные записи хранения**, свою учетную запись хранения, а затем узел **Таблицы**.</span><span class="sxs-lookup"><span data-stu-id="218a3-174">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="218a3-176">Дважды щелкните hello **опрашивает** или **варианты** таблице tooview hello содержимое таблицы hello в окне документа, а также добавления, удаления и изменения сущностей.</span><span class="sxs-lookup"><span data-stu-id="218a3-176">Double-click on hello **polls** or **choices** table tooview hello contents of hello table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Результаты запросов таблицы](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="218a3-178">Публикация hello web app tooAzure службы приложений</span><span class="sxs-lookup"><span data-stu-id="218a3-178">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="218a3-179">Hello Azure .NET SDK предоставляет простой способ toodeploy вашей web app tooAzure службы приложений.</span><span class="sxs-lookup"><span data-stu-id="218a3-179">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="218a3-180">В **обозревателе решений**, правой кнопкой мыши узел проекта hello и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="218a3-180">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
     ![Диалоговое окно «Публикация веб-сайта»](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="218a3-182">Щелкните **Веб-приложения Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="218a3-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="218a3-183">Щелкните **New** toocreate новое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="218a3-183">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="218a3-184">Заполните следующие поля hello и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="218a3-184">Fill in hello following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="218a3-185">**Имя веб-приложения**</span><span class="sxs-lookup"><span data-stu-id="218a3-185">**Web App name**</span></span>
   * <span data-ttu-id="218a3-186">**План обслуживания приложения**</span><span class="sxs-lookup"><span data-stu-id="218a3-186">**App Service plan**</span></span>
   * <span data-ttu-id="218a3-187">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="218a3-187">**Resource group**</span></span>
   * <span data-ttu-id="218a3-188">**Регион**</span><span class="sxs-lookup"><span data-stu-id="218a3-188">**Region**</span></span>
   * <span data-ttu-id="218a3-189">Оставить **сервера базы данных** значение слишком**ни одной базы данных**</span><span class="sxs-lookup"><span data-stu-id="218a3-189">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="218a3-190">Примите значения по умолчанию и щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="218a3-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="218a3-191">Веб-браузере откроется автоматически toohello опубликованных веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="218a3-191">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="218a3-192">При просмотре toohello о странице вы увидите, что он использует hello **в памяти** репозитория, не hello **табличного хранилища Azure** репозитория.</span><span class="sxs-lookup"><span data-stu-id="218a3-192">If you browse toohello about page, you'll see that it uses hello **In-Memory** repository, not hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="218a3-193">Это потому, что hello переменные среды не установлены hello экземпляр веб-приложений в службе приложений Azure, поэтому он использует значения по умолчанию hello в **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="218a3-193">That's because hello environment variables are not set on hello Web Apps instance in Azure App Service, so it uses hello default values specified in **settings.py**.</span></span>

## <a name="configure-hello-web-apps-instance"></a><span data-ttu-id="218a3-194">Настройка экземпляра веб-приложения hello</span><span class="sxs-lookup"><span data-stu-id="218a3-194">Configure hello Web Apps instance</span></span>
<span data-ttu-id="218a3-195">В этом разделе мы настроим переменные среды для экземпляра веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="218a3-195">In this section, we'll configure environment variables for hello Web Apps instance.</span></span>

1. <span data-ttu-id="218a3-196">В [портала Azure](https://portal.azure.com), откройте колонку hello веб-приложение, нажав **Обзор** > **службы приложений** > имя вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="218a3-196">In [Azure Portal](https://portal.azure.com), open hello web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="218a3-197">В колонке веб-приложения щелкните **Все параметры**, а затем — **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="218a3-197">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="218a3-198">Прокрутите вниз toohello **параметры приложения** статьи и задание значений hello для **РЕПОЗИТОРИЯ\_имя**, **ХРАНЕНИЯ\_имя** и  **ХРАНИЛИЩЕ\_ключ** согласно инструкциям hello **проекта hello Настройка** выше.</span><span class="sxs-lookup"><span data-stu-id="218a3-198">Scroll down toohello **App settings** section and set hello values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in hello **Configure hello project** section above.</span></span>
   
     ![Параметры приложения](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="218a3-200">Щелкните **Save**(Сохранить).</span><span class="sxs-lookup"><span data-stu-id="218a3-200">Click on **Save**.</span></span> <span data-ttu-id="218a3-201">После получил уведомления hello применения hello изменения, выберите команду **Обзор** из колонки основного приложения Web hello.</span><span class="sxs-lookup"><span data-stu-id="218a3-201">After you've received hello notifications that hello changes were applied, click on **Browse** from hello Web app main blade.</span></span>
5. <span data-ttu-id="218a3-202">Вы увидите рабочее приложение hello web, как и ожидалось, с помощью hello **табличного хранилища Azure** репозитория.</span><span class="sxs-lookup"><span data-stu-id="218a3-202">You should see hello web app working as expected, using hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="218a3-203">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="218a3-203">Congratulations!</span></span>
   
     ![Веб-браузер](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="218a3-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="218a3-205">Next steps</span></span>
<span data-ttu-id="218a3-206">Выполните эти ссылки toolearn Дополнительные сведения о средствах Python для Visual Studio, термосе и табличного хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="218a3-206">Follow these links toolearn more about Python Tools for Visual Studio, Flask and Azure Table Storage.</span></span>

* <span data-ttu-id="218a3-207">[Документация по средствам Python для Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="218a3-207">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="218a3-208">[Веб-проекты]</span><span class="sxs-lookup"><span data-stu-id="218a3-208">[Web Projects]</span></span>
  * <span data-ttu-id="218a3-209">[Проекты для облачной службы]</span><span class="sxs-lookup"><span data-stu-id="218a3-209">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="218a3-210">[Удаленная отладка в Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="218a3-210">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="218a3-211">[Документация по Flask]</span><span class="sxs-lookup"><span data-stu-id="218a3-211">[Flask Documentation]</span></span>
* <span data-ttu-id="218a3-212">[Хранилище Azure]</span><span class="sxs-lookup"><span data-stu-id="218a3-212">[Azure Storage]</span></span>
* <span data-ttu-id="218a3-213">[Пакет SDK для Azure для Python]</span><span class="sxs-lookup"><span data-stu-id="218a3-213">[Azure SDK for Python]</span></span>
* <span data-ttu-id="218a3-214">[Как tooUse hello службы хранения таблиц из Python]</span><span class="sxs-lookup"><span data-stu-id="218a3-214">[How tooUse hello Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="218a3-215">Изменения</span><span class="sxs-lookup"><span data-stu-id="218a3-215">What's changed</span></span>
* <span data-ttu-id="218a3-216">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="218a3-216">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[центре разработчиков Python]: /develop/python/
[облачных служб Azure]: ../cloud-services/cloud-services-python-ptvs.md
[документации]:../cosmos-db/table-storage-how-to-use-python.md
[Как tooUse hello службы хранения таблиц из Python]:../cosmos-db/table-storage-how-to-use-python.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Azure SDK для .NET]: http://azure.microsoft.com/downloads/
[средства Python для Visual Studio]: http://aka.ms/ptvs
[Инструменты Python 2.2 для Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[средства Python 2.2 для Visual Studio образцы VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
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
