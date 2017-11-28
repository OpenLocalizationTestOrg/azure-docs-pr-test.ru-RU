---
title: "Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных | Документация Майкрософт"
description: "В этом учебнике используемого при создании конвейера фабрики данных Azure с помощью операции копирования приветствия мастера копирования, поддерживаемые фабрикой данных"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 567b89e7a54c245c134cd0674690e6f3499b46d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a><span data-ttu-id="de6a4-103">Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных</span><span class="sxs-lookup"><span data-stu-id="de6a4-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="de6a4-104">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="de6a4-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="de6a4-105">Мастер копирования</span><span class="sxs-lookup"><span data-stu-id="de6a4-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="de6a4-106">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="de6a4-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="de6a4-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="de6a4-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="de6a4-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="de6a4-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="de6a4-109">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="de6a4-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="de6a4-110">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="de6a4-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="de6a4-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="de6a4-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="de6a4-112">В этом учебнике показано как toouse hello **мастер копирования** toocopy данных из базы данных Azure SQL tooan хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="de6a4-112">This tutorial shows you how toouse hello **Copy Wizard** toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 

<span data-ttu-id="de6a4-113">Hello фабрики данных Azure **мастер копирования** позволяет tooquickly создания данных конвейера, который копирует данные из поддерживаемого источника данных хранилища поддерживается tooa целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="de6a4-113">hello Azure Data Factory **Copy Wizard** allows you tooquickly create a data pipeline that copies data from a supported source data store tooa supported destination data store.</span></span> <span data-ttu-id="de6a4-114">Таким образом рекомендуется использовать мастер hello как первый шаг-toocreate пример конвейера для вашего сценария перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="de6a4-114">Therefore, we recommend that you use hello wizard as a first step toocreate a sample pipeline for your data movement scenario.</span></span> <span data-ttu-id="de6a4-115">Список хранилищ данных, которые поддерживаются в качестве исходных и целевых, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="de6a4-115">For a list of data stores supported as sources and as destinations, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>  

<span data-ttu-id="de6a4-116">Этот учебник показывает, как toocreate фабрикой данных Azure hello запуска мастера копирования пройти несколько шагов tooprovide особенности сценария приема и перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="de6a4-116">This tutorial shows you how toocreate an Azure data factory, launch hello Copy Wizard, go through a series of steps tooprovide details about your data ingestion/movement scenario.</span></span> <span data-ttu-id="de6a4-117">После завершения мастера hello hello автоматическое создание конвейера с toocopy действие копирования данных из базы данных Azure SQL tooan хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="de6a4-117">When you finish steps in hello wizard, hello wizard automatically creates a pipeline with a Copy Activity toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="de6a4-118">Дополнительные сведения о действии копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="de6a4-118">For more information about Copy Activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de6a4-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="de6a4-119">Prerequisites</span></span>
<span data-ttu-id="de6a4-120">Выполните предварительные требования, перечисленные в hello [Обзор учебника](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) статьи перед выполнением этого учебника.</span><span class="sxs-lookup"><span data-stu-id="de6a4-120">Complete prerequisites listed in hello [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="de6a4-121">Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="de6a4-121">Create data factory</span></span>
<span data-ttu-id="de6a4-122">На этом шаге используется hello Azure портала toocreate фабрикой данных Azure с именем **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-122">In this step, you use hello Azure portal toocreate an Azure data factory named **ADFTutorialDataFactory**.</span></span>

1. <span data-ttu-id="de6a4-123">Войдите в слишком[портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="de6a4-123">Log in too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="de6a4-124">Нажмите кнопку **+ создать** в левом верхнем углу hello, выберите **данные + аналитика**и нажмите кнопку **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-124">Click **+ NEW** from hello top-left corner, click **Data + analytics**, and click **Data Factory**.</span></span> 
   
   ![Создать -> Фабрика данных](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. <span data-ttu-id="de6a4-126">В hello **новую фабрику данных** колонки:</span><span class="sxs-lookup"><span data-stu-id="de6a4-126">In hello **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="de6a4-127">Введите **ADFTutorialDataFactory** для hello **имя**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-127">Enter **ADFTutorialDataFactory** for hello **name**.</span></span>
       <span data-ttu-id="de6a4-128">Имя фабрики данных Azure hello Hello должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="de6a4-128">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="de6a4-129">Если ошибка hello: `Data factory name “ADFTutorialDataFactory” is not available`, измените имя hello hello фабрики данных (например, yournameADFTutorialDataFactoryYYYYMMDD) и повторите попытку создания.</span><span class="sxs-lookup"><span data-stu-id="de6a4-129">If you receive hello error: `Data factory name “ADFTutorialDataFactory” is not available`, change hello name of hello data factory (for example, yournameADFTutorialDataFactoryYYYYMMDD) and try creating again.</span></span> <span data-ttu-id="de6a4-130">Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="de6a4-130">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
      
       ![Имя фабрики данных недоступно](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. <span data-ttu-id="de6a4-132">Выберите свою **подписку Azure**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-132">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="de6a4-133">Для группы ресурсов выполните одно из действий hello.</span><span class="sxs-lookup"><span data-stu-id="de6a4-133">For Resource Group, do one of hello following steps:</span></span> 
      
      - <span data-ttu-id="de6a4-134">Выберите **использовать существующие** tooselect существующую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="de6a4-134">Select **Use existing** tooselect an existing resource group.</span></span>
      - <span data-ttu-id="de6a4-135">Выберите **создать новый** tooenter имя для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="de6a4-135">Select **Create new** tooenter a name for a resource group.</span></span>
          
        <span data-ttu-id="de6a4-136">Некоторые шаги hello в этом учебнике предполагается использовать имя hello: **ADFTutorialResourceGroup** для группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="de6a4-136">Some of hello steps in this tutorial assume that you use hello name: **ADFTutorialResourceGroup** for hello resource group.</span></span> <span data-ttu-id="de6a4-137">toolearn о группах ресурсов. в разделе [с помощью ресурса группы toomanage ресурсам Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="de6a4-137">toolearn about resource groups, see [Using resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>
   4. <span data-ttu-id="de6a4-138">Выберите **расположение** для фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="de6a4-138">Select a **location** for hello data factory.</span></span>
   5. <span data-ttu-id="de6a4-139">Выберите **toodashboard ПИН-код** флажок hello нижней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="de6a4-139">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>  
   6. <span data-ttu-id="de6a4-140">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-140">Click **Create**.</span></span>
      
       ![Создать колонку "Фабрика данных"](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. <span data-ttu-id="de6a4-142">После завершения создания hello, вы видите hello **фабрики данных** колонки, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="de6a4-142">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image:</span></span>
   
   ![Домашняя страница фабрики данных](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a><span data-ttu-id="de6a4-144">Запуск мастера копирования</span><span class="sxs-lookup"><span data-stu-id="de6a4-144">Launch Copy Wizard</span></span>
1. <span data-ttu-id="de6a4-145">В колонке hello фабрики данных, нажмите кнопку **копирование данных [Предварительная версия]** toolaunch hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-145">On hello Data Factory blade, click **Copy data [PREVIEW]** toolaunch hello **Copy Wizard**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="de6a4-146">При появлении этого веб-браузер hello застряла в «Авторизации...», отключить или снимите **блокировать сторонние файлы cookie и данным сайта** в параметры браузера hello (или) оставьте она включена и создание исключения для  **Login.microsoftonline.com** , затем попытайтесь еще раз запустить мастер hello.</span><span class="sxs-lookup"><span data-stu-id="de6a4-146">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting in hello browser settings (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
2. <span data-ttu-id="de6a4-147">В hello **свойства** страницы:</span><span class="sxs-lookup"><span data-stu-id="de6a4-147">In hello **Properties** page:</span></span>
   
   1. <span data-ttu-id="de6a4-148">В качестве **имени задачи** введите **CopyFromBlobToAzureSql**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-148">Enter **CopyFromBlobToAzureSql** for **Task name**</span></span>
   2. <span data-ttu-id="de6a4-149">Введите **описание** (необязательно).</span><span class="sxs-lookup"><span data-stu-id="de6a4-149">Enter **description** (optional).</span></span>
   3. <span data-ttu-id="de6a4-150">Изменение hello **Дата-время начала** и hello **время Дата окончания** так, чтобы дата окончания hello tootoday установите и запустите даты ранее toofive дней.</span><span class="sxs-lookup"><span data-stu-id="de6a4-150">Change hello **Start date time** and hello **End date time** so that hello end date is set tootoday and start date toofive days earlier.</span></span>  
   4. <span data-ttu-id="de6a4-151">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-151">Click **Next**.</span></span>  
      
      ![Средство копирования — страница "Свойства"](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. <span data-ttu-id="de6a4-153">На hello **хранилище данных источника** щелкните **хранилища больших двоичных объектов** плитки.</span><span class="sxs-lookup"><span data-stu-id="de6a4-153">On hello **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="de6a4-154">Использовать хранилище страницы toospecify hello источника данных для копирования задачу hello.</span><span class="sxs-lookup"><span data-stu-id="de6a4-154">You use this page toospecify hello source data store for hello copy task.</span></span> 
   
    ![Средство копирования — страница "Хранилище данных источников"](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. <span data-ttu-id="de6a4-156">На hello **укажите учетную запись хранилища больших двоичных объектов Azure hello** страницы:</span><span class="sxs-lookup"><span data-stu-id="de6a4-156">On hello **Specify hello Azure Blob storage account** page:</span></span>
   
   1. <span data-ttu-id="de6a4-157">В качестве **имени связанной службы** введите **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-157">Enter **AzureStorageLinkedService** for **Linked service name**.</span></span>
   2. <span data-ttu-id="de6a4-158">Убедитесь, что в качестве **метода выбора учетной записи** выбран вариант **From Azure subscriptions** (Из подписок Azure).</span><span class="sxs-lookup"><span data-stu-id="de6a4-158">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="de6a4-159">Выберите свою **подписку Azure**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-159">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="de6a4-160">Выберите **учетной записи хранилища Azure** из hello список хранилища Azure учетные записи, доступные в hello выбранной подписки.</span><span class="sxs-lookup"><span data-stu-id="de6a4-160">Select an **Azure storage account** from hello list of Azure storage accounts available in hello selected subscription.</span></span> <span data-ttu-id="de6a4-161">Можно также выбрать tooenter параметры учетной записи хранилища вручную, выбрав **вручную ввести** параметр для hello **учетной записи метод выбора**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-161">You can also choose tooenter storage account settings manually by selecting **Enter manually** option for hello **Account selection method**, and then click **Next**.</span></span> 
      
      ![Средство копирования — указать учетную запись хранилища больших двоичных объектов Azure hello](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. <span data-ttu-id="de6a4-163">На **выбрать hello входной файл или папку** страницы:</span><span class="sxs-lookup"><span data-stu-id="de6a4-163">On **Choose hello input file or folder** page:</span></span>
   
   1. <span data-ttu-id="de6a4-164">Дважды щелкните папку **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-164">Double-click **adftutorial** (folder).</span></span>
   2. <span data-ttu-id="de6a4-165">Выберите **emp.txt** и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-165">Select **emp.txt**, and click **Choose**</span></span>
      
      ![Средство копирования: Выбор hello входного файла или папки](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. <span data-ttu-id="de6a4-167">На hello **выбрать hello входной файл или папку** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-167">On hello **Choose hello input file or folder** page, click **Next**.</span></span> <span data-ttu-id="de6a4-168">Не устанавливайте флажок **Binary copy**(Двоичное копирование).</span><span class="sxs-lookup"><span data-stu-id="de6a4-168">Do not select **Binary copy**.</span></span> 
   
    ![Средство копирования: Выбор hello входного файла или папки](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. <span data-ttu-id="de6a4-170">На hello **настроек формата файла** страницы, появятся разделители hello и hello схему, которая определяется автоматически мастером hello путем синтаксического анализа файла hello.</span><span class="sxs-lookup"><span data-stu-id="de6a4-170">On hello **File format settings** page, you see hello delimiters and hello schema that is auto-detected by hello wizard by parsing hello file.</span></span> <span data-ttu-id="de6a4-171">Можно также ввести разделители hello вручную для hello копирования мастера toostop автоматическое определение или toooverride.</span><span class="sxs-lookup"><span data-stu-id="de6a4-171">You can also enter hello delimiters manually for hello copy wizard toostop auto-detecting or toooverride.</span></span> <span data-ttu-id="de6a4-172">Нажмите кнопку **Далее** после проверки разделители hello и предварительного просмотра данных.</span><span class="sxs-lookup"><span data-stu-id="de6a4-172">Click **Next** after you review hello delimiters and preview data.</span></span> 
   
    ![Средство копирования — параметры формата файла](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. <span data-ttu-id="de6a4-174">В данных назначения hello хранения страницы, выберите **базы данных SQL Azure**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-174">On hello Destination data store page, select **Azure SQL Database**, and click **Next**.</span></span>
   
    ![Средство копирования — выбор целевого хранилища](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. <span data-ttu-id="de6a4-176">На **базы данных Azure SQL укажите hello** страницы:</span><span class="sxs-lookup"><span data-stu-id="de6a4-176">On **Specify hello Azure SQL database** page:</span></span>
   
   1. <span data-ttu-id="de6a4-177">Введите **AzureSqlLinkedService** для hello **имя подключения** поля.</span><span class="sxs-lookup"><span data-stu-id="de6a4-177">Enter **AzureSqlLinkedService** for hello **Connection name** field.</span></span>
   2. <span data-ttu-id="de6a4-178">В качестве **метода выбора базы данных или сервера** должен быть выбран вариант **From Azure subscriptions** (Из подписок Azure).</span><span class="sxs-lookup"><span data-stu-id="de6a4-178">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span></span>
   3. <span data-ttu-id="de6a4-179">Выберите свою **подписку Azure**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-179">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="de6a4-180">Выберите **имя сервера** и **базу данных**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-180">Select **Server name** and **Database**.</span></span>
   5. <span data-ttu-id="de6a4-181">Введите **имя пользователя** и **пароль**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-181">Enter **User name** and **Password**.</span></span>
   6. <span data-ttu-id="de6a4-182">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-182">Click **Next**.</span></span>  
      
      ![Средство копирования — указание базы данных SQL Azure](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. <span data-ttu-id="de6a4-184">На hello **сопоставление таблицы** выберите **emp** для hello **назначения** из раскрывающегося списка hello, щелкните **стрелка вниз** (необязательно) toosee hello схемы и toopreview hello данные.</span><span class="sxs-lookup"><span data-stu-id="de6a4-184">On hello **Table mapping** page, select **emp** for hello **Destination** field from hello drop-down list, click **down arrow** (optional) toosee hello schema and toopreview hello data.</span></span>
    
     ![Средство копирования — сопоставление таблиц](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. <span data-ttu-id="de6a4-186">На hello **сопоставление схемы** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-186">On hello **Schema mapping** page, click **Next**.</span></span>
    
    ![Средство копирования — сопоставление схем](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. <span data-ttu-id="de6a4-188">На hello **параметры производительности** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-188">On hello **Performance settings** page, click **Next**.</span></span> 
    
    ![Средство копирования — параметры производительности](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. <span data-ttu-id="de6a4-190">Просмотрите сведения в hello **Сводка** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="de6a4-190">Review information in hello **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="de6a4-191">Hello мастер создает две связанные службы, два набора данных (ввода и вывода) и один конвейер в фабрике данных hello (из которой запущено приветствия мастера копирования).</span><span class="sxs-lookup"><span data-stu-id="de6a4-191">hello wizard creates two linked services, two datasets (input and output), and one pipeline in hello data factory (from where you launched hello Copy Wizard).</span></span> 
    
    ![Средство копирования — параметры производительности](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a><span data-ttu-id="de6a4-193">Запуск приложения для отслеживания и управления</span><span class="sxs-lookup"><span data-stu-id="de6a4-193">Launch Monitor and Manage application</span></span>
1. <span data-ttu-id="de6a4-194">На hello **развертывания** щелкните ссылку hello: `Click here toomonitor copy pipeline`.</span><span class="sxs-lookup"><span data-stu-id="de6a4-194">On hello **Deployment** page, click hello link: `Click here toomonitor copy pipeline`.</span></span>
   
   ![Средство копирования — развертывание выполнено](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. <span data-ttu-id="de6a4-196">мониторинг приложения Hello запускается на отдельной вкладке в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="de6a4-196">hello monitoring application is launched in a separate tab in your web browser.</span></span>   
   
   ![Приложение мониторинга](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. <span data-ttu-id="de6a4-198">Последнее состояние toosee hello почасовой секторов, нажмите кнопку **обновление** кнопку в hello **действия WINDOWS** списке нижней hello.</span><span class="sxs-lookup"><span data-stu-id="de6a4-198">toosee hello latest status of hourly slices, click **Refresh** button in hello **ACTIVITY WINDOWS** list at hello bottom.</span></span> <span data-ttu-id="de6a4-199">Вы увидите пять действий windows пять дней между значениями времени начала и окончания для конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="de6a4-199">You see five activity windows for five days between start and end times for hello pipeline.</span></span> <span data-ttu-id="de6a4-200">Hello списка не обновляется автоматически, поэтому вы можете требуется tooclick обновления несколько раз, чтобы увидеть все windows hello действия в состоянии готовности hello.</span><span class="sxs-lookup"><span data-stu-id="de6a4-200">hello list is not automatically refreshed, so you may need tooclick Refresh a couple of times before you see all hello activity windows in hello Ready state.</span></span> 
4. <span data-ttu-id="de6a4-201">Выберите окно действия в списке hello.</span><span class="sxs-lookup"><span data-stu-id="de6a4-201">Select an activity window in hello list.</span></span> <span data-ttu-id="de6a4-202">. В разделе hello сведения о ней в hello **действия окно обозревателя** на hello справа.</span><span class="sxs-lookup"><span data-stu-id="de6a4-202">See hello details about it in hello **Activity Window Explorer** on hello right.</span></span>

    ![Сведения об окне действия](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    <span data-ttu-id="de6a4-204">Обратите внимание, что даты hello 11, 12, 13, 14 и 15 зеленым цветом, это означает, что hello ежедневного срезы выходных данных для этих дат уже было произведено.</span><span class="sxs-lookup"><span data-stu-id="de6a4-204">Notice that hello dates 11, 12, 13, 14, and 15 are in green color, which means that hello daily output slices for these dates have already been produced.</span></span> <span data-ttu-id="de6a4-205">Также см. это выделение цветом в конвейер hello и hello выходной набор данных в представлении диаграммы hello.</span><span class="sxs-lookup"><span data-stu-id="de6a4-205">You also see this color coding on hello pipeline and hello output dataset in hello diagram view.</span></span> <span data-ttu-id="de6a4-206">В предыдущем шаге hello Обратите внимание, что двух фрагментов уже создан, один срез обрабатывается в данный момент, hello других двух, ожидающих обработки toobe (с учетом hello цветовое кодирование).</span><span class="sxs-lookup"><span data-stu-id="de6a4-206">In hello previous step, notice that two slices have already been produced, one slice is currently being processed, and hello other two are waiting toobe processed (based on hello color coding).</span></span> 

    <span data-ttu-id="de6a4-207">Дополнительные сведения об использовании этого приложения см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью приложения для мониторинга и управления](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="de6a4-207">For more information on using this application, see [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de6a4-208">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="de6a4-208">Next steps</span></span>
<span data-ttu-id="de6a4-209">В этом руководстве в ходе операции копирования вы использовали хранилище BLOB-объектов Azure как исходное хранилище данных, а базу данных SQL Azure — как целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="de6a4-209">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="de6a4-210">Hello следующей таблице приведен список хранилищ данных, поддерживаемые действием копирования hello как источники и назначения:</span><span class="sxs-lookup"><span data-stu-id="de6a4-210">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="de6a4-211">Дополнительные сведения о полей и свойств, которые можно увидеть в мастер копирования hello для хранилища данных щелкните ссылку hello hello хранилища данных в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="de6a4-211">For details about fields/properties that you see in hello copy wizard for a data store, click hello link for hello data store in hello table.</span></span> 
