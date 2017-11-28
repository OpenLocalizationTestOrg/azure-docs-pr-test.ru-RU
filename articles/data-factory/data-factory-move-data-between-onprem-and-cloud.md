---
title: "Перемещение данных: шлюз управления данными | Документация Майкрософт"
description: "Настройка шлюза данных для перемещения данных между локальными узлами и облаком. Используйте шлюз управления данными в фабрике данных Azure для перемещения данных."
keywords: "шлюз данных, интеграции данных, перемещение данных, учетные данные шлюза"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 565091e24a8c0009793e2e2365fb95013cad5028
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-between-on-premises-sources-and-the-cloud-with-data-management-gateway"></a><span data-ttu-id="491a1-105">Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными</span><span class="sxs-lookup"><span data-stu-id="491a1-105">Move data between on-premises sources and the cloud with Data Management Gateway</span></span>
<span data-ttu-id="491a1-106">Эта статья содержит общие сведения об интеграции данных, хранящихся в локальных и облачных хранилищах данных, с помощью фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="491a1-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="491a1-107">В статье используются понятия, описанные в статье [Действия по перемещению данных](data-factory-data-movement-activities.md) и других основополагающих статьях о фабрике данных: [наборы данных](data-factory-create-datasets.md) и [конвейеры](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="491a1-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="491a1-108">Шлюз управления данными</span><span class="sxs-lookup"><span data-stu-id="491a1-108">Data Management Gateway</span></span>
<span data-ttu-id="491a1-109">Шлюз управления данными необходимо установить на локальный компьютер, чтобы обеспечить перемещение данных из локального хранилища данных и в него.</span><span class="sxs-lookup"><span data-stu-id="491a1-109">You must install Data Management Gateway on your on-premises machine to enable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="491a1-110">Шлюз можно установить на том же компьютере, на котором размещается хранилище, или на другом компьютере. Важно, чтобы шлюз мог подключиться к хранилищу данных.</span><span class="sxs-lookup"><span data-stu-id="491a1-110">The gateway can be installed on the same machine as the data store or on a different machine as long as the gateway can connect to the data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="491a1-111">Дополнительные сведения о шлюзе управления данными см. в статье [Шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="491a1-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="491a1-112">Приведенное ниже пошаговое руководство поможет вам создать фабрику данных с конвейером, перемещающим данные из локальной базы данных **SQL Server** в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="491a1-112">The following walkthrough shows you how to create a data factory with a pipeline that moves data from an on-premises **SQL Server** database to an Azure blob storage.</span></span> <span data-ttu-id="491a1-113">В рамках этого пошагового руководства вы установите и настроите шлюз управления данными на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="491a1-113">As part of the walkthrough, you install and configure the Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-to-cloud"></a><span data-ttu-id="491a1-114">Пошаговое руководство: копирование локальных данных в облако</span><span class="sxs-lookup"><span data-stu-id="491a1-114">Walkthrough: copy on-premises data to cloud</span></span>
<span data-ttu-id="491a1-115">В этом пошаговом руководстве вы сделаете следующее:</span><span class="sxs-lookup"><span data-stu-id="491a1-115">In this walkthrough you do the following steps:</span></span> 

1. <span data-ttu-id="491a1-116">Создадите фабрику данных.</span><span class="sxs-lookup"><span data-stu-id="491a1-116">Create a data factory.</span></span>
2. <span data-ttu-id="491a1-117">Создадите шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="491a1-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="491a1-118">Создадите связанные службы для хранилища данных-источника и приемника.</span><span class="sxs-lookup"><span data-stu-id="491a1-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="491a1-119">Создадите наборы данных, которые представляют входные и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="491a1-119">Create datasets to represent input and output data.</span></span>
5. <span data-ttu-id="491a1-120">Создадите конвейер с действием копирования для перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="491a1-120">Create a pipeline with a copy activity to move the data.</span></span>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="491a1-121">Предварительные требования для прохождения этого учебника</span><span class="sxs-lookup"><span data-stu-id="491a1-121">Prerequisites for the tutorial</span></span>
<span data-ttu-id="491a1-122">Для работы с этим пошаговым руководством необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="491a1-122">Before you begin this walkthrough, you must have the following prerequisites:</span></span>

* <span data-ttu-id="491a1-123">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="491a1-123">**Azure subscription**.</span></span>  <span data-ttu-id="491a1-124">Если у вас нет подписки, вы можете создать бесплатную пробную версию учетной записи всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="491a1-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="491a1-125">Дополнительные сведения см. в статье [Бесплатная пробная версия](http://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="491a1-125">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="491a1-126">**исходного**хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="491a1-126">**Azure Storage Account**.</span></span> <span data-ttu-id="491a1-127">В этом руководстве в качестве **назначения и приемника** будет использоваться хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="491a1-127">You use the blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="491a1-128">в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) .</span><span class="sxs-lookup"><span data-stu-id="491a1-128">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="491a1-129">**SQL Server.**</span><span class="sxs-lookup"><span data-stu-id="491a1-129">**SQL Server**.</span></span> <span data-ttu-id="491a1-130">В этом руководстве используйте локальную базу данных SQL Server в качестве **исходного** хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="491a1-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="491a1-131">Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="491a1-131">Create data factory</span></span>
<span data-ttu-id="491a1-132">На этом этапе вы с помощью портала Azure создадите экземпляр фабрики данных Azure с именем **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="491a1-132">In this step, you use the Azure portal to create an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="491a1-133">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="491a1-133">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="491a1-134">Щелкните **+ New** (+ Создать), **Аналитика**, а затем — **Фабрика данных**.</span><span class="sxs-lookup"><span data-stu-id="491a1-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![Создать -> Фабрика данных](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="491a1-136">На странице **Новая фабрика данных** введите **ADFTutorialOnPremDF** в поле "Имя".</span><span class="sxs-lookup"><span data-stu-id="491a1-136">In the **New data factory** page, enter **ADFTutorialOnPremDF** for the Name.</span></span>

    ![Добавить на начальную панель](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="491a1-138">Имя фабрики данных Azure должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="491a1-138">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="491a1-139">Получив сообщение об ошибке **Имя фабрики данных "ADFTutorialOnPremDF" недоступно**, измените имя фабрики данных (например, на yournameADFTutorialOnPremDF) и попробуйте создать ее еще раз.</span><span class="sxs-lookup"><span data-stu-id="491a1-139">If you receive the error: **Data factory name “ADFTutorialOnPremDF” is not available**, change the name of the data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="491a1-140">Выполняя оставшиеся действия, описанные в этом руководстве, вместо ADFTutorialOnPremDF используйте именно это имя.</span><span class="sxs-lookup"><span data-stu-id="491a1-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="491a1-141">В будущем имя фабрики данных может быть зарегистрировано в качестве **DNS-имени** и, следовательно, стать отображаемым.</span><span class="sxs-lookup"><span data-stu-id="491a1-141">The name of the data factory may be registered as a **DNS** name in the future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="491a1-142">Выберите **подписку Azure** , в рамках которой вы хотите создать фабрику данных.</span><span class="sxs-lookup"><span data-stu-id="491a1-142">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="491a1-143">Выберите имеющуюся **группу ресурсов** или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="491a1-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="491a1-144">Для примера в этом руководстве создайте группу ресурсов с именем **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="491a1-144">For the tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="491a1-145">На странице **Новая фабрика данных** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="491a1-145">Click **Create** on the **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="491a1-146">Создавать экземпляры фабрики данных может пользователь с ролью [Участник фабрики данных](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) на уровне подписки или группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="491a1-146">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="491a1-147">После завершения процедуры создания фабрики данных появится страница **Фабрика данных**, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="491a1-147">After creation is complete, you see the **Data Factory** page as shown in the following image:</span></span>

   ![Домашняя страница фабрики данных](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="491a1-149">Создание шлюза</span><span class="sxs-lookup"><span data-stu-id="491a1-149">Create gateway</span></span>
1. <span data-ttu-id="491a1-150">На странице **Фабрика данных** щелкните плитку **Создать и развернуть**, чтобы запустить **редактор** для фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="491a1-150">In the **Data Factory** page, click **Author and deploy** tile to launch the **Editor** for the data factory.</span></span>

    ![Плитка "Создание и развертывание"](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="491a1-152">В редакторе фабрики данных нажмите кнопку **... More** (...Дополнительно) на панели инструментов, а затем — **Новый шлюз данных**.</span><span class="sxs-lookup"><span data-stu-id="491a1-152">In the Data Factory Editor, click **... More** on the toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="491a1-153">Кроме того, в представлении в виде дерева можно щелкнуть правой кнопкой мыши **Шлюзы данных** и выбрать пункт **Новый шлюз данных**.</span><span class="sxs-lookup"><span data-stu-id="491a1-153">Alternatively, you can right-click **Data Gateways** in the tree view, and click **New data gateway**.</span></span>

   ![«Новый шлюз данных» на панели инструментов](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="491a1-155">На странице **Создать** в поле **Имя** введите **adftutorialgateway** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="491a1-155">In the **Create** page, enter **adftutorialgateway** for the **name**, and click **OK**.</span></span>     

    ![Страница "Создать шлюз"](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="491a1-157">В этом пошаговом руководстве вы создадите логический шлюз с одним узлом (локальный компьютер с Windows).</span><span class="sxs-lookup"><span data-stu-id="491a1-157">In this walkthrough, you create the logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="491a1-158">Шлюз управления данными можно развернуть, сопоставив с ним несколько локальных компьютеров.</span><span class="sxs-lookup"><span data-stu-id="491a1-158">You can scale out a data management gateway by associating multiple on-premises machines with the gateway.</span></span> <span data-ttu-id="491a1-159">Чтобы увеличить масштаб, увеличьте число заданий перемещения данных, которые могут выполняться одновременно на узле.</span><span class="sxs-lookup"><span data-stu-id="491a1-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="491a1-160">Эта функция также доступна для логического шлюза с одним узлом.</span><span class="sxs-lookup"><span data-stu-id="491a1-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="491a1-161">Дополнительные сведения см. в статье [Шлюз управления данными: высокий уровень доступности и масштабируемость (предварительная версия)](data-factory-data-management-gateway-high-availability-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="491a1-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="491a1-162">На странице **Настройка** щелкните **Установка непосредственно на этот компьютер**.</span><span class="sxs-lookup"><span data-stu-id="491a1-162">In the **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="491a1-163">Это позволит скачать пакет установки для шлюза, а также установить, настроить и зарегистрировать шлюз на компьютере.</span><span class="sxs-lookup"><span data-stu-id="491a1-163">This action downloads the installation package for the gateway, installs, configures, and registers the gateway on the computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="491a1-164">Используйте Internet Explorer или другой веб-браузер, совместимый с Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="491a1-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="491a1-165">Если вы используете браузер Chrome, перейдите в [интернет-магазин Chrome](https://chrome.google.com/webstore/), введите ClickOnce в строке поиска, а затем выберите и установите одно из расширений ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="491a1-165">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="491a1-166">То же самое (установку надстройки) сделайте и в случае с браузером Firefox.</span><span class="sxs-lookup"><span data-stu-id="491a1-166">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="491a1-167">Нажмите кнопку **Открыть меню** на панели инструментов (**три горизонтальные линии** в правом верхнем углу), щелкните **Надстройки**, введите "ClickOnce" в строку поиска, выберите одно из расширений ClickOnce и установите его.</span><span class="sxs-lookup"><span data-stu-id="491a1-167">Click **Open Menu** button on the toolbar (**three horizontal lines** in the top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![Шлюз — страница "Настройка"](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="491a1-169">Это самый простой способ (одним щелчком) скачать, установить, настроить и зарегистрировать шлюз в один прием.</span><span class="sxs-lookup"><span data-stu-id="491a1-169">This way is the easiest way (one-click) to download, install, configure, and register the gateway in one single step.</span></span> <span data-ttu-id="491a1-170">Вы увидите, что на компьютере установлено приложение **Microsoft Data Management Gateway Configuration Manager** .</span><span class="sxs-lookup"><span data-stu-id="491a1-170">You can see the **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="491a1-171">Вы также можете найти исполняемый файл **ConfigManager.exe** в папке по следующему пути: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="491a1-171">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="491a1-172">Шлюз также можно скачать и установить вручную, используя ссылки на этой странице. Затем вы можете зарегистрировать его с помощью ключа, указанного в текстовом поле **Создать ключ**.</span><span class="sxs-lookup"><span data-stu-id="491a1-172">You can also download and install gateway manually by using the links in this page and register it using the key shown in the **NEW KEY** text box.</span></span>

    <span data-ttu-id="491a1-173">Все дополнительные сведения о шлюзе см. в статье [Шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="491a1-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="491a1-174">Для успешной установки шлюза управления данными и его настройки вы должны обладать правами администратора на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="491a1-174">You must be an administrator on the local computer to install and configure the Data Management Gateway successfully.</span></span> <span data-ttu-id="491a1-175">В локальную группу Windows **Пользователи шлюза управления данными** можно добавить дополнительных пользователей.</span><span class="sxs-lookup"><span data-stu-id="491a1-175">You can add additional users to the **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="491a1-176">Участники этой группы могут использовать диспетчер конфигурации шлюза управления данными для настройки шлюза.</span><span class="sxs-lookup"><span data-stu-id="491a1-176">The members of this group can use the Data Management Gateway Configuration Manager tool to configure the gateway.</span></span>
   >
   >
5. <span data-ttu-id="491a1-177">Подождите несколько минут или пока не появится следующее уведомление:</span><span class="sxs-lookup"><span data-stu-id="491a1-177">Wait for a couple of minutes or wait until you see the following notification message:</span></span>

    ![Установка шлюза успешно выполнена](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="491a1-179">Запустите на компьютере приложение **Диспетчер конфигурации шлюза управления данными**.</span><span class="sxs-lookup"><span data-stu-id="491a1-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="491a1-180">Для этого введите текст **шлюз управления данными** в окне **Поиск**.</span><span class="sxs-lookup"><span data-stu-id="491a1-180">In the **Search** window, type **Data Management Gateway** to access this utility.</span></span> <span data-ttu-id="491a1-181">Вы также можете найти исполняемый файл **ConfigManager.exe** в папке по следующему пути: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="491a1-181">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![Диспетчер конфигурации шлюза](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="491a1-183">Убедитесь, что отображается сообщение `adftutorialgateway is connected to the cloud service`.</span><span class="sxs-lookup"><span data-stu-id="491a1-183">Confirm that you see `adftutorialgateway is connected to the cloud service` message.</span></span> <span data-ttu-id="491a1-184">В строке состояния внизу отображается надпись **Подключение к облачной службе установлено** и **зеленая галочка**.</span><span class="sxs-lookup"><span data-stu-id="491a1-184">The status bar the bottom displays **Connected to the cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="491a1-185">На вкладке **Главная** можно также выполнить следующие операции:</span><span class="sxs-lookup"><span data-stu-id="491a1-185">On the **Home** tab, you can also do the following operations:</span></span>

   * <span data-ttu-id="491a1-186">**зарегистрировать** шлюз, используя ключ с портала Azure, с помощью кнопки "Зарегистрировать";</span><span class="sxs-lookup"><span data-stu-id="491a1-186">**Register** a gateway with a key from the Azure portal by using the Register button.</span></span>
   * <span data-ttu-id="491a1-187">**остановить** службу узла шлюза управления данными на компьютере шлюза;</span><span class="sxs-lookup"><span data-stu-id="491a1-187">**Stop** the Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="491a1-188">**запланировать** установку обновлений на определенное время суток;</span><span class="sxs-lookup"><span data-stu-id="491a1-188">**Schedule updates** to be installed at a specific time of the day.</span></span>
   * <span data-ttu-id="491a1-189">просмотреть, когда шлюз был **обновлен последний раз**;</span><span class="sxs-lookup"><span data-stu-id="491a1-189">View when the gateway was **last updated**.</span></span>
   * <span data-ttu-id="491a1-190">указать время для установки обновления в шлюзе.</span><span class="sxs-lookup"><span data-stu-id="491a1-190">Specify time at which an update to the gateway can be installed.</span></span>
8. <span data-ttu-id="491a1-191">Переключитесь на вкладку **Параметры** . Сертификат, указанный в разделе **Сертификат** , используется для шифрования и расшифровки учетных данных локального хранилища данных, указанного на портале.</span><span class="sxs-lookup"><span data-stu-id="491a1-191">Switch to the **Settings** tab. The certificate specified in the **Certificate** section is used to encrypt/decrypt credentials for the on-premises data store that you specify on the portal.</span></span> <span data-ttu-id="491a1-192">Щелкните **Изменить** , чтобы использовать собственный сертификат (необязательно).</span><span class="sxs-lookup"><span data-stu-id="491a1-192">(optional) Click **Change** to use your own certificate instead.</span></span> <span data-ttu-id="491a1-193">По умолчанию шлюз использует сертификат, который автоматически создан службой фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="491a1-193">By default, the gateway uses the certificate that is auto-generated by the Data Factory service.</span></span>

    ![Конфигурация сертификата шлюза](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="491a1-195">Кроме того, на вкладке **Параметры** можно:</span><span class="sxs-lookup"><span data-stu-id="491a1-195">You can also do the following actions on the **Settings** tab:</span></span>

   * <span data-ttu-id="491a1-196">просмотреть или экспортировать сертификат, используемый шлюзом;</span><span class="sxs-lookup"><span data-stu-id="491a1-196">View or export the certificate being used by the gateway.</span></span>
   * <span data-ttu-id="491a1-197">изменить конечную точку HTTPS, используемую шлюзом;</span><span class="sxs-lookup"><span data-stu-id="491a1-197">Change the HTTPS endpoint used by the gateway.</span></span>    
   * <span data-ttu-id="491a1-198">задать прокси-сервер HTTP, который будет использовать шлюз.</span><span class="sxs-lookup"><span data-stu-id="491a1-198">Set an HTTP proxy to be used by the gateway.</span></span>     
9. <span data-ttu-id="491a1-199">(Необязательно.) Для устранения проблем в работе шлюза вы можете использовать подробное ведение журнала. Чтобы включить эту функцию, перейдите на вкладку **Диагностика** и установите флажок **Включить запись подробных сведений в журнал**.</span><span class="sxs-lookup"><span data-stu-id="491a1-199">(optional) Switch to the **Diagnostics** tab, check the **Enable verbose logging** option if you want to enable verbose logging that you can use to troubleshoot any issues with the gateway.</span></span> <span data-ttu-id="491a1-200">Данные журналов можно изучить в средстве **Просмотр событий**, открыв узел **Журналы приложений и служб** -> **Шлюз управления данными**.</span><span class="sxs-lookup"><span data-stu-id="491a1-200">The logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![Вкладка «Диагностика»](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="491a1-202">На вкладке **Диагностика** можно также выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="491a1-202">You can also perform the following actions in the **Diagnostics** tab:</span></span>

   * <span data-ttu-id="491a1-203">Щелкните **Проверить подключение** , чтобы проверить подключение к локальному источнику данных через шлюз.</span><span class="sxs-lookup"><span data-stu-id="491a1-203">Use **Test Connection** section to an on-premises data source using the gateway.</span></span>
   * <span data-ttu-id="491a1-204">Щелкните **Просмотреть журналы** , чтобы просмотреть журнал шлюза управления данными в окне просмотра событий.</span><span class="sxs-lookup"><span data-stu-id="491a1-204">Click **View Logs** to see the Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="491a1-205">Щелкните **Оправить журналы**, чтобы передать ZIP-файл с журналами за последние семь дней в корпорацию Майкрософт. Это поможет упростить устранение неполадок, с которыми вы сталкиваетесь.</span><span class="sxs-lookup"><span data-stu-id="491a1-205">Click **Send Logs** to upload a zip file with logs of last seven days to Microsoft to facilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="491a1-206">На вкладке **Диагностика** в разделе **Проверка подключения** выберите **SqlServer** в качестве типа хранилища данных, введите имя сервера базы данных и имя базы данных, укажите тип проверки подлинности, введите имя пользователя и пароль и нажмите кнопку **Test** (Проверка), чтобы проверить возможность подключения шлюза к базе данных.</span><span class="sxs-lookup"><span data-stu-id="491a1-206">On the **Diagnostics** tab, in the **Test Connection** section, select **SqlServer** for the type of the data store, enter the name of the database server, name of the database, specify authentication type, enter user name, and password, and click **Test** to test whether the gateway can connect to the database.</span></span>
11. <span data-ttu-id="491a1-207">Перейдите в браузер и на **портале Azure** нажмите кнопку **ОК** на странице **Настройка**, а затем — на странице **Новый шлюз данных**.</span><span class="sxs-lookup"><span data-stu-id="491a1-207">Switch to the web browser, and in the **Azure portal**, click **OK** on the **Configure** page and then on the **New data gateway** page.</span></span>
12. <span data-ttu-id="491a1-208">В иерархической структуре слева найдите элемент **adftutorialgateway** в узле **Шлюзы данных**.</span><span class="sxs-lookup"><span data-stu-id="491a1-208">You should see **adftutorialgateway** under **Data Gateways** in the tree view on the left.</span></span>  <span data-ttu-id="491a1-209">Щелкните его, чтобы увидеть связанные файлы JSON.</span><span class="sxs-lookup"><span data-stu-id="491a1-209">If you click it, you should see the associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="491a1-210">Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="491a1-210">Create linked services</span></span>
<span data-ttu-id="491a1-211">На этом этапе вы создадите две связанные службы: **AzureStorageLinkedService** и **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="491a1-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="491a1-212">Служба **SqlServerLinkedService** связывает с фабрикой данных локальную базу данных SQL Server, а служба **AzureStorageLinkedService** — хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="491a1-212">The **SqlServerLinkedService** links an on-premises SQL Server database and the **AzureStorageLinkedService** linked service links an Azure blob store to the data factory.</span></span> <span data-ttu-id="491a1-213">Далее, это руководство поможет вам создать конвейер, который копирует данные из локальной базы данных SQL Server в службу хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="491a1-213">You create a pipeline later in this walkthrough that copies data from the on-premises SQL Server database to the Azure blob store.</span></span>

#### <a name="add-a-linked-service-to-an-on-premises-sql-server-database"></a><span data-ttu-id="491a1-214">Добавление связанной службы в локальную базу данных SQL Server</span><span class="sxs-lookup"><span data-stu-id="491a1-214">Add a linked service to an on-premises SQL Server database</span></span>
1. <span data-ttu-id="491a1-215">В **редакторе фабрики данных** щелкните **Создать хранилище данных** на панели инструментов и выберите **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="491a1-215">In the **Data Factory Editor**, click **New data store** on the toolbar and select **SQL Server**.</span></span>

   ![Создать связанную службу SQL Server](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="491a1-217">В **редакторе JSON** справа сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="491a1-217">In the **JSON editor** on the right, do the following steps:</span></span>

   1. <span data-ttu-id="491a1-218">Для параметра **gatewayName** укажите значение **adftutorialgateway**.</span><span class="sxs-lookup"><span data-stu-id="491a1-218">For the **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="491a1-219">В **connectionString** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="491a1-219">In the **connectionString**, do the following steps:</span></span>    

      1. <span data-ttu-id="491a1-220">В поле **servername** введите имя сервера, на котором размещены базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="491a1-220">For **servername**, enter the name of the server that hosts the SQL Server database.</span></span>
      2. <span data-ttu-id="491a1-221">В поле **databasename** введите имя базы данных.</span><span class="sxs-lookup"><span data-stu-id="491a1-221">For **databasename**, enter the name of the database.</span></span>
      3. <span data-ttu-id="491a1-222">На панели инструментов нажмите кнопку **Зашифровать**.</span><span class="sxs-lookup"><span data-stu-id="491a1-222">Click **Encrypt** button on the toolbar.</span></span> <span data-ttu-id="491a1-223">Отобразится приложение "Диспетчер учетных данных".</span><span class="sxs-lookup"><span data-stu-id="491a1-223">You see the Credentials Manager application.</span></span>

         ![Приложение "Диспетчер учетных данных"](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="491a1-225">В диалоговом окне **Настройка учетных данных** введите имя пользователя и пароль, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="491a1-225">In the **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="491a1-226">Если подключение установлено успешно, зашифрованные учетные данные сохраняются в JSON, а диалоговое окно закрывается.</span><span class="sxs-lookup"><span data-stu-id="491a1-226">If the connection is successful, the encrypted credentials are stored in the JSON and the dialog box closes.</span></span>
      5. <span data-ttu-id="491a1-227">Закройте пустую вкладку браузера, запустившую диалоговое окно, если она не закрылась автоматически, и вернитесь на вкладку портала Azure.</span><span class="sxs-lookup"><span data-stu-id="491a1-227">Close the empty browser tab that launched the dialog box if it is not automatically closed and get back to the tab with the Azure portal.</span></span>

         <span data-ttu-id="491a1-228">В компьютере шлюза учетные данные **зашифрованы** с помощью сертификата, который принадлежит службе фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="491a1-228">On the gateway machine, these credentials are **encrypted** by using a certificate that the Data Factory service owns.</span></span> <span data-ttu-id="491a1-229">Если вы хотите использовать вместо него сертификат, связанный со шлюзом управления данными, см. раздел, посвященный [безопасной настройке учетных данных](#set-credentials-and-security).</span><span class="sxs-lookup"><span data-stu-id="491a1-229">If you want to use the certificate that is associated with the Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="491a1-230">Нажмите кнопку **Развернуть** на панели команд, чтобы развернуть связанную службу SQL Server.</span><span class="sxs-lookup"><span data-stu-id="491a1-230">Click **Deploy** on the command bar to deploy the SQL Server linked service.</span></span> <span data-ttu-id="491a1-231">В представлении в виде дерева отобразится связанная служба.</span><span class="sxs-lookup"><span data-stu-id="491a1-231">You should see the linked service in the tree view.</span></span>

      ![Связанная служба SQL Server в представлении в виде дерева](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="491a1-233">Добавление связанной службы для учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="491a1-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="491a1-234">В **редакторе фабрики данных** щелкните **Создать хранилище данных** на панели команд и выберите **Служба хранилища Azure**.</span><span class="sxs-lookup"><span data-stu-id="491a1-234">In the **Data Factory Editor**, click **New data store** on the command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="491a1-235">В поле **Имя учетной записи**введите имя учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="491a1-235">Enter the name of your Azure storage account for the **Account name**.</span></span>
3. <span data-ttu-id="491a1-236">В поле **Ключ учетной записи**введите ключ учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="491a1-236">Enter the key for your Azure storage account for the **Account key**.</span></span>
4. <span data-ttu-id="491a1-237">Щелкните **Развернуть**, чтобы развернуть службу **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="491a1-237">Click **Deploy** to deploy the **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="491a1-238">Создание наборов данных</span><span class="sxs-lookup"><span data-stu-id="491a1-238">Create datasets</span></span>
<span data-ttu-id="491a1-239">На этом этапе вы создадите наборы входных и выходных данных, которые представляют собой входные и выходные данные для операции копирования (из локальной базы данных SQL Server в хранилище BLOB-объектов Azure).</span><span class="sxs-lookup"><span data-stu-id="491a1-239">In this step, you create input and output datasets that represent input and output data for the copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="491a1-240">Прежде чем создавать наборы данных, необходимо сделать следующее (подробное описание шагов приводится далее):</span><span class="sxs-lookup"><span data-stu-id="491a1-240">Before creating datasets, do the following steps (detailed steps follows the list):</span></span>

* <span data-ttu-id="491a1-241">В базе данных SQL Server, добавленной в фабрику данных в качестве связанной службы, создайте таблицу с именем **emp** и вставьте в нее пару записей в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="491a1-241">Create a table named **emp** in the SQL Server Database you added as a linked service to the data factory and insert a couple of sample entries into the table.</span></span>
* <span data-ttu-id="491a1-242">В учетной записи хранения BLOB-объектов Azure, которую вы добавили в качестве связанной службы в фабрику данных, создайте контейнер BLOB-объектов с именем **adftutorial** .</span><span class="sxs-lookup"><span data-stu-id="491a1-242">Create a blob container named **adftutorial** in the Azure blob storage account you added as a linked service to the data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-the-tutorial"></a><span data-ttu-id="491a1-243">Подготовка локальной связанной службы SQL Server для учебника</span><span class="sxs-lookup"><span data-stu-id="491a1-243">Prepare On-premises SQL Server for the tutorial</span></span>
1. <span data-ttu-id="491a1-244">В базе данных SQL Server, которую вы указали для локальных связанных служб (**SqlServerLinkedService**), используйте следующий сценарий SQL, чтобы создать в базе данных таблицу **emp**.</span><span class="sxs-lookup"><span data-stu-id="491a1-244">In the database you specified for the on-premises SQL Server linked service (**SqlServerLinkedService**), use the following SQL script to create the **emp** table in the database.</span></span>

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. <span data-ttu-id="491a1-245">Вставьте несколько образцов в таблицу:</span><span class="sxs-lookup"><span data-stu-id="491a1-245">Insert some sample into the table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="491a1-246">Создание входного набора данных</span><span class="sxs-lookup"><span data-stu-id="491a1-246">Create input dataset</span></span>

1. <span data-ttu-id="491a1-247">В **редакторе фабрики данных** нажмите кнопку **... More** (...Дополнительно), на панели команд щелкните **Новый набор данных** и выберите **Таблица SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="491a1-247">In the **Data Factory Editor**, click **... More**, click **New dataset** on the command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="491a1-248">Замените сценарий JSON в области справа на следующий текст:</span><span class="sxs-lookup"><span data-stu-id="491a1-248">Replace the JSON in the right pane with the following text:</span></span>

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   <span data-ttu-id="491a1-249">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="491a1-249">Note the following points:</span></span>

   * <span data-ttu-id="491a1-250">**type** имеет значение **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="491a1-250">**type** is set to **SqlServerTable**.</span></span>
   * <span data-ttu-id="491a1-251">**tablename** имеет значение **emp**.</span><span class="sxs-lookup"><span data-stu-id="491a1-251">**tableName** is set to **emp**.</span></span>
   * <span data-ttu-id="491a1-252">Для **linkedServiceName** задано значение **SqlServerLinkedService** (вы создали эту связанную службу ранее в этом руководстве).</span><span class="sxs-lookup"><span data-stu-id="491a1-252">**linkedServiceName** is set to **SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="491a1-253">Если входной набор данных не создается другим конвейером фабрики данных Azure, для параметра **external** следует задать значение **true**.</span><span class="sxs-lookup"><span data-stu-id="491a1-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** to **true**.</span></span> <span data-ttu-id="491a1-254">Это означает, что входные данные создаются вне службы фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="491a1-254">It denotes the input data is produced external to the Azure Data Factory service.</span></span> <span data-ttu-id="491a1-255">При необходимости можно указать любые внешние политики данных с помощью **externalData** в разделе **Policy**.</span><span class="sxs-lookup"><span data-stu-id="491a1-255">You can optionally specify any external data policies using the **externalData** element in the **Policy** section.</span></span>    

   <span data-ttu-id="491a1-256">Дополнительные сведения о свойствах файлов JSON см. в статье [Перемещение данных в базу данных SQL Server и обратно на локальных компьютерах и виртуальных машинах Azure IaaS с помощью фабрики данных Azure](data-factory-sqlserver-connector.md).</span><span class="sxs-lookup"><span data-stu-id="491a1-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="491a1-257">Нажмите кнопку **Развернуть** на панели команд, чтобы развернуть набор данных.</span><span class="sxs-lookup"><span data-stu-id="491a1-257">Click **Deploy** on the command bar to deploy the dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="491a1-258">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="491a1-258">Create output dataset</span></span>

1. <span data-ttu-id="491a1-259">В **редакторе фабрики данных** щелкните на панели команд **Создать набор данных** и выберите **Хранилище BLOB-объектов Azure**.</span><span class="sxs-lookup"><span data-stu-id="491a1-259">In the **Data Factory Editor**, click **New dataset** on the command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="491a1-260">Замените сценарий JSON в области справа на следующий текст:</span><span class="sxs-lookup"><span data-stu-id="491a1-260">Replace the JSON in the right pane with the following text:</span></span>

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   <span data-ttu-id="491a1-261">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="491a1-261">Note the following points:</span></span>

   * <span data-ttu-id="491a1-262">**type** имеет значение **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="491a1-262">**type** is set to **AzureBlob**.</span></span>
   * <span data-ttu-id="491a1-263">**linkedServiceName** имеет значение **AzureStorageLinkedService** (вы создали эту связанную службу на шаге 2).</span><span class="sxs-lookup"><span data-stu-id="491a1-263">**linkedServiceName** is set to **AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="491a1-264">**folderPath** имеет значение **adftutorial/outfromonpremdf**, где outfromonpremdf — это папка в контейнере adftutorial.</span><span class="sxs-lookup"><span data-stu-id="491a1-264">**folderPath** is set to **adftutorial/outfromonpremdf** where outfromonpremdf is the folder in the adftutorial container.</span></span> <span data-ttu-id="491a1-265">Если контейнер **adftutorial** еще не существует, создайте его.</span><span class="sxs-lookup"><span data-stu-id="491a1-265">Create the **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="491a1-266">Параметр **availability** имеет значение **hourly** (параметру **frequency** присваивается значение **hour**, а параметру **interval** — значение **1**).</span><span class="sxs-lookup"><span data-stu-id="491a1-266">The **availability** is set to **hourly** (**frequency** set to **hour** and **interval** set to **1**).</span></span>  <span data-ttu-id="491a1-267">Служба фабрики данных каждый час создает срез выходных данных в таблице **emp** в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="491a1-267">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL Database.</span></span>

   <span data-ttu-id="491a1-268">Если не указать **fileName** для **выходной таблицы**, то созданные в **folderPath** файлы получают имена в следующем формате: Data<Guid>.txt (например: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="491a1-268">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="491a1-269">Чтобы динамически установить параметры **folderPath** и **fileName** на основе времени **SliceStart**, используйте свойство partitionedBy.</span><span class="sxs-lookup"><span data-stu-id="491a1-269">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the partitionedBy property.</span></span> <span data-ttu-id="491a1-270">В следующем примере folderPath использует год, месяц и день из SliceStart (время начала обработки среза), а в fileName используется время (часы) из SliceStart.</span><span class="sxs-lookup"><span data-stu-id="491a1-270">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span></span> <span data-ttu-id="491a1-271">Например, если срез выполняется для временной отметки 2014-10-20T08:00:00, folderName получает значение wikidatagateway/wikisampledataout/2014/10/20, а fileName – 08.csv.</span><span class="sxs-lookup"><span data-stu-id="491a1-271">For example, if a slice is being produced for 2014-10-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2014/10/20 and the fileName is set to 08.csv.</span></span>

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    <span data-ttu-id="491a1-272">Дополнительные сведения о свойствах файлов JSON см. в статье [Перемещение данных в базу данных SQL Server и обратно на локальных компьютерах и виртуальных машинах Azure IaaS с помощью фабрики данных Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="491a1-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="491a1-273">Нажмите кнопку **Развернуть** на панели команд, чтобы развернуть набор данных.</span><span class="sxs-lookup"><span data-stu-id="491a1-273">Click **Deploy** on the command bar to deploy the dataset.</span></span> <span data-ttu-id="491a1-274">Оба набора данных должны отображаться в представлении в виде дерева.</span><span class="sxs-lookup"><span data-stu-id="491a1-274">Confirm that you see both the datasets in the tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="491a1-275">Создание конвейера</span><span class="sxs-lookup"><span data-stu-id="491a1-275">Create pipeline</span></span>
<span data-ttu-id="491a1-276">На этом шаге вы создадите **конвейер** одним **действием копирования**, для выполнения которого **EmpOnPremSQLTable** будет использоваться как входные данные, а **OutputBlobTable** — как выходные данные.</span><span class="sxs-lookup"><span data-stu-id="491a1-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="491a1-277">В редакторе фабрики данных нажмите кнопку **... Дополнительно** и **Новый конвейер**.</span><span class="sxs-lookup"><span data-stu-id="491a1-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="491a1-278">Замените сценарий JSON в области справа на следующий текст:</span><span class="sxs-lookup"><span data-stu-id="491a1-278">Replace the JSON in the right pane with the following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL to Azure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server to blob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > <span data-ttu-id="491a1-279">Замените значение свойства **start** текущей датой, а значение свойства **end** — датой следующего дня.</span><span class="sxs-lookup"><span data-stu-id="491a1-279">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span>
   >
   >

   <span data-ttu-id="491a1-280">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="491a1-280">Note the following points:</span></span>

   * <span data-ttu-id="491a1-281">В разделе действий есть только действие, для параметра **type** которого задано значение **Copy**.</span><span class="sxs-lookup"><span data-stu-id="491a1-281">In the activities section, there is only activity whose **type** is set to **Copy**.</span></span>
   * <span data-ttu-id="491a1-282">Для параметра действия **input** установлено значение **EmpOnPremSQLTable**, а для **output** — **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="491a1-282">**Input** for the activity is set to **EmpOnPremSQLTable** and **output** for the activity is set to **OutputBlobTable**.</span></span>
   * <span data-ttu-id="491a1-283">В разделе **typeProperties** в качестве **типа источника** указано значение **SqlSink**, а в качестве **типа приемника** — **BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="491a1-283">In the **typeProperties** section, **SqlSource** is specified as the **source type** and **BlobSink **is specified as the **sink type**.</span></span>
   * <span data-ttu-id="491a1-284">Для свойства **sqlReaderQuery** типа **SqlSource** задан тип SQL-запроса `select * from emp`.</span><span class="sxs-lookup"><span data-stu-id="491a1-284">SQL query `select * from emp` is specified for the **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="491a1-285">Даты начала и окончания должны быть в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="491a1-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="491a1-286">Например, 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="491a1-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="491a1-287">Время **окончания** указывать не обязательно, однако в этом примере мы будем его использовать.</span><span class="sxs-lookup"><span data-stu-id="491a1-287">The **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="491a1-288">Если не указать значение свойства **end**, оно вычисляется по формуле "**время начала + 48 часов**".</span><span class="sxs-lookup"><span data-stu-id="491a1-288">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="491a1-289">Чтобы запустить конвейер в течение неопределенного срока, укажите значение **9/9/9999** в качестве значения свойства **end**.</span><span class="sxs-lookup"><span data-stu-id="491a1-289">To run the pipeline indefinitely, specify **9/9/9999** as the value for the **end** property.</span></span>

   <span data-ttu-id="491a1-290">Вы определяете интервал времени, в рамках которого выполняются срезы данных на основе свойств **доступности**, определенных для каждого набора данных Azure.</span><span class="sxs-lookup"><span data-stu-id="491a1-290">You are defining the time duration in which the data slices are processed based on the **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="491a1-291">В этом примере получено 24 среза данных, так как они создаются каждый час.</span><span class="sxs-lookup"><span data-stu-id="491a1-291">In the example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="491a1-292">Нажмите кнопку **Развернуть** на панели команд, чтобы развернуть набор данных (таблица представляет собой прямоугольный набор данных).</span><span class="sxs-lookup"><span data-stu-id="491a1-292">Click **Deploy** on the command bar to deploy the dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="491a1-293">Убедитесь, что конвейер отображается в представлении в виде дерева в узле **Конвейеры**.</span><span class="sxs-lookup"><span data-stu-id="491a1-293">Confirm that the pipeline shows up in the tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="491a1-294">Нажмите кнопку **X** дважды, чтобы закрыть все страницы и вернуться к странице **Фабрика данных** для **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="491a1-294">Now, click **X** twice to close the page to get back to the **Data Factory** page for the **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="491a1-295">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="491a1-295">**Congratulations!**</span></span> <span data-ttu-id="491a1-296">Вы успешно создали фабрику данных Azure, связанные службы, наборы данных и конвейер, а также выполнили планирование конвейера.</span><span class="sxs-lookup"><span data-stu-id="491a1-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled the pipeline.</span></span>

#### <a name="view-the-data-factory-in-a-diagram-view"></a><span data-ttu-id="491a1-297">Просмотр фабрики данных в представлении схемы</span><span class="sxs-lookup"><span data-stu-id="491a1-297">View the data factory in a Diagram View</span></span>
1. <span data-ttu-id="491a1-298">На **портале Azure** щелкните элемент **Схема** на домашней странице фабрики данных **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="491a1-298">In the **Azure portal**, click **Diagram** tile on the home page for the **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="491a1-299">:</span><span class="sxs-lookup"><span data-stu-id="491a1-299">:</span></span>

    ![Ссылка на схему](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="491a1-301">Вы должны увидеть схему, аналогичную приведенной ниже:</span><span class="sxs-lookup"><span data-stu-id="491a1-301">You should see the diagram similar to the following image:</span></span>

    ![Представление схемы](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="491a1-303">Можно увеличивать и уменьшать масштаб, выбирать 100 %-ный масштаб или масштаб по размеру, автоматически размещать конвейеры и наборы данных, а также отображать сведения из журнала обращений и преобразований (выделение восходящих и нисходящих элементов для выбранных элементов).</span><span class="sxs-lookup"><span data-stu-id="491a1-303">You can zoom in, zoom out, zoom to 100%, zoom to fit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="491a1-304">Дважды щелкните объект (входной или выходной набор данных либо конвейер), чтобы просмотреть его свойства.</span><span class="sxs-lookup"><span data-stu-id="491a1-304">You can double-click an object (input/output dataset or pipeline) to see properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="491a1-305">Отслеживание конвейера</span><span class="sxs-lookup"><span data-stu-id="491a1-305">Monitor pipeline</span></span>
<span data-ttu-id="491a1-306">На этом шаге используется портал Azure для мониторинга фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="491a1-306">In this step, you use the Azure portal to monitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="491a1-307">Вы также можете использовать командлеты PowerShell для мониторинга наборов данных и конвейеров.</span><span class="sxs-lookup"><span data-stu-id="491a1-307">You can also use PowerShell cmdlets to monitor datasets and pipelines.</span></span> <span data-ttu-id="491a1-308">Дополнительные сведения о мониторинге см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="491a1-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="491a1-309">На схеме дважды щелкните **EmpOnPremSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="491a1-309">In the diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![Срезы EmpOnPremSQLTable](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="491a1-311">Обратите внимание, что для всех срезов данных выше установлено состояние **Готово**, так как в качестве значения продолжительности выполнения конвейера (от времени начала до времени окончания) указано значение в прошлом.</span><span class="sxs-lookup"><span data-stu-id="491a1-311">Notice that all the data slices up are in **Ready** state because the pipeline duration (start time to end time) is in the past.</span></span> <span data-ttu-id="491a1-312">Это также результат того, что вы вставили данные в базу данных SQL Server, и они находились там все время.</span><span class="sxs-lookup"><span data-stu-id="491a1-312">It is also because you have inserted the data in the SQL Server database and it is there all the time.</span></span> <span data-ttu-id="491a1-313">Убедитесь, что в разделе **Проблемные срезы** в нижней части окна не показаны срезы.</span><span class="sxs-lookup"><span data-stu-id="491a1-313">Confirm that no slices show up in the **Problem slices** section at the bottom.</span></span> <span data-ttu-id="491a1-314">Чтобы просмотреть все срезы, щелкните **Подробности** под списком срезов.</span><span class="sxs-lookup"><span data-stu-id="491a1-314">To view all the slices, click **See More** at the bottom of the list of slices.</span></span>
3. <span data-ttu-id="491a1-315">Затем на странице **Наборы данных** щелкните **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="491a1-315">Now, In the **Datasets** page, click **OutputBlobTable**.</span></span>

    ![Срезы OputputBlobTable](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="491a1-317">Щелкните любой срез данных в списке, чтобы отобразить страницу **Срез данных**.</span><span class="sxs-lookup"><span data-stu-id="491a1-317">Click any data slice from the list and you should see the **Data Slice** page.</span></span> <span data-ttu-id="491a1-318">Для этого среза отобразится раздел "Запуски операции".</span><span class="sxs-lookup"><span data-stu-id="491a1-318">You see activity runs for the slice.</span></span> <span data-ttu-id="491a1-319">Как правило, в этом разделе отображается только одно действие.</span><span class="sxs-lookup"><span data-stu-id="491a1-319">You see only one activity run usually.</span></span>  

    ![Колонка среза данных](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="491a1-321">Если срез не находится в состоянии **Готов**, вы можете увидеть восходящие срезы, которые не находятся в состоянии готовности и блокируют выполнение текущего среза в списке **Неготовые восходящие срезы**.</span><span class="sxs-lookup"><span data-stu-id="491a1-321">If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="491a1-322">Щелкните **выполненное действие** в нижней части списка, чтобы просмотреть **дополнительные сведения о выполнении операции**.</span><span class="sxs-lookup"><span data-stu-id="491a1-322">Click the **activity run** from the list at the bottom to see **activity run details**.</span></span>

   ![Страница "Подробности о выполнении операции"](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="491a1-324">Отобразятся такие сведения, как пропускная способность, продолжительность и шлюз, использованный для передачи данных.</span><span class="sxs-lookup"><span data-stu-id="491a1-324">You would see information such as throughput, duration, and the gateway used to transfer the data.</span></span>
6. <span data-ttu-id="491a1-325">Закройте все страницы, щелкая значок **X**, пока</span><span class="sxs-lookup"><span data-stu-id="491a1-325">Click **X** to close all the pages until you</span></span>
7. <span data-ttu-id="491a1-326">не вернетесь к домашней странице **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="491a1-326">get back to the home page for the **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="491a1-327">(Необязательно.) Щелкните **Конвейеры**, а затем — **ADFTutorialOnPremDF** и просмотрите параметры входных таблиц (**Использовано**) или выходных наборов данных (**Выполнено**).</span><span class="sxs-lookup"><span data-stu-id="491a1-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="491a1-328">Используйте инструменты, такие как [обозреватель хранилищ Microsoft](http://storageexplorer.com/), чтобы проверить, создается ли файл или большой двоичный объект каждый час.</span><span class="sxs-lookup"><span data-stu-id="491a1-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to verify that a blob/file is created for each hour.</span></span>

   ![обозреватель хранилищ Azure](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="491a1-330">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="491a1-330">Next steps</span></span>
* <span data-ttu-id="491a1-331">Все дополнительные сведения о шлюзе управления данными см. в статье [Шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="491a1-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the Data Management Gateway.</span></span>
* <span data-ttu-id="491a1-332">Чтобы узнать, как перемещать данные из исходного хранилища данных в приемник данных с помощью действия копирования, ознакомьтесь со статьей [Копирование данных из хранилища BLOB-объектов Azure в базу данных SQL с помощью фабрики данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .</span><span class="sxs-lookup"><span data-stu-id="491a1-332">See [Copy data from Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to learn about how to use Copy Activity to move data from a source data store to a sink data store.</span></span>
