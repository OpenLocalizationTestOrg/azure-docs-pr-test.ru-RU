---
title: "Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных | Документация Майкрософт"
description: "С помощью этого учебника вы создадите конвейер фабрики данных Azure с действием копирования при помощи мастера копирования, поддерживаемого фабрикой данных."
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
ms.openlocfilehash: 5922c050cc09236ba5fdec885a70d11da20135cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a><span data-ttu-id="c75de-103">Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных</span><span class="sxs-lookup"><span data-stu-id="c75de-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c75de-104">Обзор и предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c75de-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="c75de-105">Мастер копирования</span><span class="sxs-lookup"><span data-stu-id="c75de-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="c75de-106">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="c75de-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="c75de-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c75de-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="c75de-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c75de-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="c75de-109">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c75de-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="c75de-110">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="c75de-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="c75de-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="c75de-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="c75de-112">В этом руководстве описано, как скопировать данные из хранилища BLOB-объектов Azure в базу данных Azure SQL с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="c75de-112">This tutorial shows you how to use the **Copy Wizard** to copy data from an Azure blob storage to an Azure SQL database.</span></span> 

<span data-ttu-id="c75de-113">**Мастер копирования** фабрики данных Azure позволяет быстро создать конвейер данных, копирующий данные из поддерживаемого исходного хранилища данных в поддерживаемое целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="c75de-113">The Azure Data Factory **Copy Wizard** allows you to quickly create a data pipeline that copies data from a supported source data store to a supported destination data store.</span></span> <span data-ttu-id="c75de-114">Поэтому мы рекомендуем использовать мастер в качестве первого шага при создании примера конвейера для сценария перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="c75de-114">Therefore, we recommend that you use the wizard as a first step to create a sample pipeline for your data movement scenario.</span></span> <span data-ttu-id="c75de-115">Список хранилищ данных, которые поддерживаются в качестве исходных и целевых, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c75de-115">For a list of data stores supported as sources and as destinations, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>  

<span data-ttu-id="c75de-116">В этом руководстве показано, как создать фабрику данных Azure, запустить мастер копирования и выполнить шаги, чтобы предоставить сведения о сценарии приема и перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="c75de-116">This tutorial shows you how to create an Azure data factory, launch the Copy Wizard, go through a series of steps to provide details about your data ingestion/movement scenario.</span></span> <span data-ttu-id="c75de-117">После завершения работы в мастере он автоматически создаст конвейер с действием копирования, позволяющим перенести данные из хранилища BLOB-объектов Azure в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c75de-117">When you finish steps in the wizard, the wizard automatically creates a pipeline with a Copy Activity to copy data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="c75de-118">Дополнительные сведения о действии копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c75de-118">For more information about Copy Activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c75de-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c75de-119">Prerequisites</span></span>
<span data-ttu-id="c75de-120">Прежде чем начать работу с этим руководством, выполните необходимые действия, перечисленные в [этой обзорной статье](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .</span><span class="sxs-lookup"><span data-stu-id="c75de-120">Complete prerequisites listed in the [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="c75de-121">Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="c75de-121">Create data factory</span></span>
<span data-ttu-id="c75de-122">На этом шаге с помощью портала Azure создается фабрика данных с именем **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="c75de-122">In this step, you use the Azure portal to create an Azure data factory named **ADFTutorialDataFactory**.</span></span>

1. <span data-ttu-id="c75de-123">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c75de-123">Log in to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c75de-124">В верхнем левом углу нажмите кнопку **+ Создать**, выберите **Данные+аналитика** и щелкните **Фабрика данных**.</span><span class="sxs-lookup"><span data-stu-id="c75de-124">Click **+ NEW** from the top-left corner, click **Data + analytics**, and click **Data Factory**.</span></span> 
   
   ![Создать -> Фабрика данных](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. <span data-ttu-id="c75de-126">В колонке **Создать фабрику данных** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c75de-126">In the **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="c75de-127">Введите **ADFTutorialDataFactory** в поле **Имя**.</span><span class="sxs-lookup"><span data-stu-id="c75de-127">Enter **ADFTutorialDataFactory** for the **name**.</span></span>
       <span data-ttu-id="c75de-128">Имя фабрики данных Azure должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="c75de-128">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="c75de-129">При возникновении ошибки `Data factory name “ADFTutorialDataFactory” is not available` измените имя фабрики данных (например, на ваше_имя_ADFTutorialDataFactoryYYYYMMDD) и попробуйте создать фабрику данных снова.</span><span class="sxs-lookup"><span data-stu-id="c75de-129">If you receive the error: `Data factory name “ADFTutorialDataFactory” is not available`, change the name of the data factory (for example, yournameADFTutorialDataFactoryYYYYMMDD) and try creating again.</span></span> <span data-ttu-id="c75de-130">Ознакомьтесь с разделом [Фабрика данных — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="c75de-130">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
      
       ![Имя фабрики данных недоступно](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. <span data-ttu-id="c75de-132">Выберите свою **подписку Azure**.</span><span class="sxs-lookup"><span data-stu-id="c75de-132">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="c75de-133">Для группы ресурсов выполните одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="c75de-133">For Resource Group, do one of the following steps:</span></span> 
      
      - <span data-ttu-id="c75de-134">а) выберите **Использовать существующую** и укажите имеющуюся группу ресурсов;</span><span class="sxs-lookup"><span data-stu-id="c75de-134">Select **Use existing** to select an existing resource group.</span></span>
      - <span data-ttu-id="c75de-135">выберите **Создать** и введите имя для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c75de-135">Select **Create new** to enter a name for a resource group.</span></span>
          
        <span data-ttu-id="c75de-136">Некоторые действия, описанные в этом руководстве, предполагают, что для группы ресурсов используется имя **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="c75de-136">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span></span> <span data-ttu-id="c75de-137">Сведения о группах ресурсов см. в статье, где описывается [использование групп ресурсов для управления ресурсами Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c75de-137">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>
   4. <span data-ttu-id="c75de-138">Укажите **расположение** фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="c75de-138">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="c75de-139">Установите флажок **Закрепить на панели мониторинга** в нижней части колонки.</span><span class="sxs-lookup"><span data-stu-id="c75de-139">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="c75de-140">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c75de-140">Click **Create**.</span></span>
      
       ![Создать колонку "Фабрика данных"](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. <span data-ttu-id="c75de-142">После создания вы увидите колонку **Фабрика данных**, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="c75de-142">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>
   
   ![Домашняя страница фабрики данных](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a><span data-ttu-id="c75de-144">Запуск мастера копирования</span><span class="sxs-lookup"><span data-stu-id="c75de-144">Launch Copy Wizard</span></span>
1. <span data-ttu-id="c75de-145">Чтобы запустить **мастер копирования**, на вкладке фабрики данных щелкните **Копирование данных [предварительная версия]**.</span><span class="sxs-lookup"><span data-stu-id="c75de-145">On the Data Factory blade, click **Copy data [PREVIEW]** to launch the **Copy Wizard**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="c75de-146">Если веб-браузер завис на действии "Авторизация...", отключите параметр или снимите флажок **Block third party cookies and site data** (Блокировать сторонние файлы cookie и данные сайта) в параметрах браузера. Либо оставьте флажок и создайте исключение для адреса **login.microsoftonline.com**, а затем попробуйте запустить мастер еще раз.</span><span class="sxs-lookup"><span data-stu-id="c75de-146">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting in the browser settings (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
2. <span data-ttu-id="c75de-147">Вот что нужно сделать на странице **Свойства** :</span><span class="sxs-lookup"><span data-stu-id="c75de-147">In the **Properties** page:</span></span>
   
   1. <span data-ttu-id="c75de-148">В качестве **имени задачи** введите **CopyFromBlobToAzureSql**.</span><span class="sxs-lookup"><span data-stu-id="c75de-148">Enter **CopyFromBlobToAzureSql** for **Task name**</span></span>
   2. <span data-ttu-id="c75de-149">Введите **описание** (необязательно).</span><span class="sxs-lookup"><span data-stu-id="c75de-149">Enter **description** (optional).</span></span>
   3. <span data-ttu-id="c75de-150">Измените **дату и время начала** и **дату и время завершения** таким образом, чтобы датой завершения был сегодняшний день, а дата начала была на пять дней раньше.</span><span class="sxs-lookup"><span data-stu-id="c75de-150">Change the **Start date time** and the **End date time** so that the end date is set to today and start date to five days earlier.</span></span>  
   4. <span data-ttu-id="c75de-151">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c75de-151">Click **Next**.</span></span>  
      
      ![Средство копирования — страница "Свойства"](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. <span data-ttu-id="c75de-153">На странице **Source data store** (Хранилище данных источников) щелкните плитку **Хранилище BLOB-объектов Azure**.</span><span class="sxs-lookup"><span data-stu-id="c75de-153">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="c75de-154">На этой странице можно указать хранилище данных источников для задачи копирования.</span><span class="sxs-lookup"><span data-stu-id="c75de-154">You use this page to specify the source data store for the copy task.</span></span> 
   
    ![Средство копирования — страница "Хранилище данных источников"](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. <span data-ttu-id="c75de-156">Вот что нужно сделать на странице **Specify the Azure Blob storage account** (Указание учетной записи хранилища BLOB-объектов Azure).</span><span class="sxs-lookup"><span data-stu-id="c75de-156">On the **Specify the Azure Blob storage account** page:</span></span>
   
   1. <span data-ttu-id="c75de-157">В качестве **имени связанной службы** введите **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="c75de-157">Enter **AzureStorageLinkedService** for **Linked service name**.</span></span>
   2. <span data-ttu-id="c75de-158">Убедитесь, что в качестве **метода выбора учетной записи** выбран вариант **From Azure subscriptions** (Из подписок Azure).</span><span class="sxs-lookup"><span data-stu-id="c75de-158">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="c75de-159">Выберите свою **подписку Azure**.</span><span class="sxs-lookup"><span data-stu-id="c75de-159">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="c75de-160">Выберите **учетную запись хранения Azure** из списка учетных записей хранения Azure, доступных в выбранной вами подписке.</span><span class="sxs-lookup"><span data-stu-id="c75de-160">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="c75de-161">Кроме того, вы можете вручную настроить параметры учетной записи хранения. Для этого в качестве **метода выбора учетной записи** выберите вариант **Ввести вручную** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c75de-161">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**, and then click **Next**.</span></span> 
      
      ![Средство копирования — указание учетной записи хранилища BLOB-объектов Azure](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. <span data-ttu-id="c75de-163">Вот что нужно сделать на странице **Choose the input file or folder** (Выбор входного файла или папки).</span><span class="sxs-lookup"><span data-stu-id="c75de-163">On **Choose the input file or folder** page:</span></span>
   
   1. <span data-ttu-id="c75de-164">Дважды щелкните папку **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="c75de-164">Double-click **adftutorial** (folder).</span></span>
   2. <span data-ttu-id="c75de-165">Выберите **emp.txt** и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c75de-165">Select **emp.txt**, and click **Choose**</span></span>
      
      ![Средство копирования — выбор входного файла или папки](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. <span data-ttu-id="c75de-167">На странице **Choose the input file or folder** (Выбор входного файла или папки) нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c75de-167">On the **Choose the input file or folder** page, click **Next**.</span></span> <span data-ttu-id="c75de-168">Не устанавливайте флажок **Binary copy**(Двоичное копирование).</span><span class="sxs-lookup"><span data-stu-id="c75de-168">Do not select **Binary copy**.</span></span> 
   
    ![Средство копирования — выбор входного файла или папки](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. <span data-ttu-id="c75de-170">На странице **File format settings** (Параметры формата файла) отображаются разделители и схема, которые мастер определяет автоматически при анализе файла.</span><span class="sxs-lookup"><span data-stu-id="c75de-170">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> <span data-ttu-id="c75de-171">Можно также ввести разделители вручную, чтобы остановить автоопределение с помощью мастера копирования или переопределить.</span><span class="sxs-lookup"><span data-stu-id="c75de-171">You can also enter the delimiters manually for the copy wizard to stop auto-detecting or to override.</span></span> <span data-ttu-id="c75de-172">Проверив разделители и просмотрев предварительные данные, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c75de-172">Click **Next** after you review the delimiters and preview data.</span></span> 
   
    ![Средство копирования — параметры формата файла](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. <span data-ttu-id="c75de-174">На странице целевого хранилища данных выберите **База данных SQL Azure** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c75de-174">On the Destination data store page, select **Azure SQL Database**, and click **Next**.</span></span>
   
    ![Средство копирования — выбор целевого хранилища](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. <span data-ttu-id="c75de-176">Вот что нужно сделать на странице **Specify the Azure SQL database** (Указание базы данных SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="c75de-176">On **Specify the Azure SQL database** page:</span></span>
   
   1. <span data-ttu-id="c75de-177">В поле **Имя подключения** введите **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="c75de-177">Enter **AzureSqlLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="c75de-178">В качестве **метода выбора базы данных или сервера** должен быть выбран вариант **From Azure subscriptions** (Из подписок Azure).</span><span class="sxs-lookup"><span data-stu-id="c75de-178">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span></span>
   3. <span data-ttu-id="c75de-179">Выберите свою **подписку Azure**.</span><span class="sxs-lookup"><span data-stu-id="c75de-179">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="c75de-180">Выберите **имя сервера** и **базу данных**.</span><span class="sxs-lookup"><span data-stu-id="c75de-180">Select **Server name** and **Database**.</span></span>
   5. <span data-ttu-id="c75de-181">Введите **имя пользователя** и **пароль**.</span><span class="sxs-lookup"><span data-stu-id="c75de-181">Enter **User name** and **Password**.</span></span>
   6. <span data-ttu-id="c75de-182">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c75de-182">Click **Next**.</span></span>  
      
      ![Средство копирования — указание базы данных SQL Azure](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. <span data-ttu-id="c75de-184">На странице **Сопоставление таблицы** выберите **emp** в поле **Назначение** раскрывающегося списка, щелкните **стрелку вниз** (необязательно), чтобы отобразить схему и просмотреть данные.</span><span class="sxs-lookup"><span data-stu-id="c75de-184">On the **Table mapping** page, select **emp** for the **Destination** field from the drop-down list, click **down arrow** (optional) to see the schema and to preview the data.</span></span>
    
     ![Средство копирования — сопоставление таблиц](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. <span data-ttu-id="c75de-186">На странице **Сопоставление схемы** нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c75de-186">On the **Schema mapping** page, click **Next**.</span></span>
    
    ![Средство копирования — сопоставление схем](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. <span data-ttu-id="c75de-188">На странице **Performance settings** (Параметры производительности) нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c75de-188">On the **Performance settings** page, click **Next**.</span></span> 
    
    ![Средство копирования — параметры производительности](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. <span data-ttu-id="c75de-190">Просмотрите сведения на странице **Сводка** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c75de-190">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="c75de-191">Мастер создаст две связанные службы, два набора данных (входной и выходной) и один конвейер в фабрике данных (из которой вы запустили мастер копирования).</span><span class="sxs-lookup"><span data-stu-id="c75de-191">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span> 
    
    ![Средство копирования — параметры производительности](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a><span data-ttu-id="c75de-193">Запуск приложения для отслеживания и управления</span><span class="sxs-lookup"><span data-stu-id="c75de-193">Launch Monitor and Manage application</span></span>
1. <span data-ttu-id="c75de-194">На странице **развертывания** щелкните ссылку: `Click here to monitor copy pipeline`.</span><span class="sxs-lookup"><span data-stu-id="c75de-194">On the **Deployment** page, click the link: `Click here to monitor copy pipeline`.</span></span>
   
   ![Средство копирования — развертывание выполнено](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. <span data-ttu-id="c75de-196">Приложение мониторинга запускается в отдельной вкладке веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="c75de-196">The monitoring application is launched in a separate tab in your web browser.</span></span>   
   
   ![Приложение мониторинга](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. <span data-ttu-id="c75de-198">Щелкните кнопку **Обновить** внизу списка **Activity Windows** (Окна действий), чтобы увидеть последнее состояние почасовых срезов.</span><span class="sxs-lookup"><span data-stu-id="c75de-198">To see the latest status of hourly slices, click **Refresh** button in the **ACTIVITY WINDOWS** list at the bottom.</span></span> <span data-ttu-id="c75de-199">Отобразится пять действий Windows за пять дней между временем начала и окончания конвейера.</span><span class="sxs-lookup"><span data-stu-id="c75de-199">You see five activity windows for five days between start and end times for the pipeline.</span></span> <span data-ttu-id="c75de-200">Список не обновляется автоматически, поэтому может потребоваться нажать кнопку "Обновить" несколько раз, прежде чем все действия Windows будут в состоянии "Готово".</span><span class="sxs-lookup"><span data-stu-id="c75de-200">The list is not automatically refreshed, so you may need to click Refresh a couple of times before you see all the activity windows in the Ready state.</span></span> 
4. <span data-ttu-id="c75de-201">Выберите окно действия в списке.</span><span class="sxs-lookup"><span data-stu-id="c75de-201">Select an activity window in the list.</span></span> <span data-ttu-id="c75de-202">Просмотрите сведения о нем в окне **Activity Window Explorer** справа.</span><span class="sxs-lookup"><span data-stu-id="c75de-202">See the details about it in the **Activity Window Explorer** on the right.</span></span>

    ![Сведения об окне действия](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    <span data-ttu-id="c75de-204">Обратите внимание, что 11, 12, 13, 14 и 15 число выделены зеленым цветом. Это означает, что ежедневные временные срезы для них уже созданы.</span><span class="sxs-lookup"><span data-stu-id="c75de-204">Notice that the dates 11, 12, 13, 14, and 15 are in green color, which means that the daily output slices for these dates have already been produced.</span></span> <span data-ttu-id="c75de-205">Также эту цветовую кодировку вы увидите в конвейере и в выходном наборе данных в представлении схемы.</span><span class="sxs-lookup"><span data-stu-id="c75de-205">You also see this color coding on the pipeline and the output dataset in the diagram view.</span></span> <span data-ttu-id="c75de-206">На предыдущем шаге обратите внимание, что два среза уже созданы. Один срез обрабатывается сейчас, а два остальных ожидают обработки (с учетом выделения цветом).</span><span class="sxs-lookup"><span data-stu-id="c75de-206">In the previous step, notice that two slices have already been produced, one slice is currently being processed, and the other two are waiting to be processed (based on the color coding).</span></span> 

    <span data-ttu-id="c75de-207">Дополнительные сведения об использовании этого приложения см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью приложения для мониторинга и управления](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="c75de-207">For more information on using this application, see [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c75de-208">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c75de-208">Next steps</span></span>
<span data-ttu-id="c75de-209">В этом руководстве в ходе операции копирования вы использовали хранилище BLOB-объектов Azure как исходное хранилище данных, а базу данных SQL Azure — как целевое хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="c75de-209">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="c75de-210">В следующей таблице приведен список хранилищ данных, которые поддерживаются в качестве источников и целевых расположений для действия копирования.</span><span class="sxs-lookup"><span data-stu-id="c75de-210">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="c75de-211">Чтобы получить дополнительные сведения о полях и свойствах в мастере копирования для хранилища данных, щелкните ссылку для хранилища данных в таблице.</span><span class="sxs-lookup"><span data-stu-id="c75de-211">For details about fields/properties that you see in the copy wizard for a data store, click the link for the data store in the table.</span></span> 