---
title: "данные aaaMove - шлюз управления данными | Документы Microsoft"
description: "Настройка шлюза данных toomove данных между локальными и hello облака. Используйте шлюз управления данными в toomove фабрики данных Azure данные."
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
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a><span data-ttu-id="0314a-105">Перемещение данных между локальным источникам и hello облако с помощью шлюза управления данными</span><span class="sxs-lookup"><span data-stu-id="0314a-105">Move data between on-premises sources and hello cloud with Data Management Gateway</span></span>
<span data-ttu-id="0314a-106">Эта статья содержит общие сведения об интеграции данных, хранящихся в локальных и облачных хранилищах данных, с помощью фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="0314a-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="0314a-107">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) других данных фабрики основных понятий статей: [наборы данных](data-factory-create-datasets.md) и [конвейеры](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="0314a-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="0314a-108">Шлюз управления данными</span><span class="sxs-lookup"><span data-stu-id="0314a-108">Data Management Gateway</span></span>
<span data-ttu-id="0314a-109">Шлюз управления данными необходимо установить на перемещение данных из хранилища данных в локальной машины tooenable вашей локальной система.</span><span class="sxs-lookup"><span data-stu-id="0314a-109">You must install Data Management Gateway on your on-premises machine tooenable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="0314a-110">можно установить шлюз Hello на приветствия же компьютера как hello хранилища данных или на другом компьютере, до тех пор, пока шлюз hello может подключаться toohello хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="0314a-110">hello gateway can be installed on hello same machine as hello data store or on a different machine as long as hello gateway can connect toohello data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0314a-111">Дополнительные сведения о шлюзе управления данными см. в статье [Шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="0314a-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="0314a-112">Hello следующем пошаговом руководстве показано, как toocreate фабрики данных с конвейером, который перемещает данные из локальной среды **SQL Server** tooan хранилище больших двоичных объектов базы данных.</span><span class="sxs-lookup"><span data-stu-id="0314a-112">hello following walkthrough shows you how toocreate a data factory with a pipeline that moves data from an on-premises **SQL Server** database tooan Azure blob storage.</span></span> <span data-ttu-id="0314a-113">В рамках пошагового руководства hello установите и настройте hello шлюз управления данными на компьютере.</span><span class="sxs-lookup"><span data-stu-id="0314a-113">As part of hello walkthrough, you install and configure hello Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-toocloud"></a><span data-ttu-id="0314a-114">Пошаговое руководство: копирование локальных данных toocloud</span><span class="sxs-lookup"><span data-stu-id="0314a-114">Walkthrough: copy on-premises data toocloud</span></span>
<span data-ttu-id="0314a-115">В этом пошаговом руководстве hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0314a-115">In this walkthrough you do hello following steps:</span></span> 

1. <span data-ttu-id="0314a-116">Создадите фабрику данных.</span><span class="sxs-lookup"><span data-stu-id="0314a-116">Create a data factory.</span></span>
2. <span data-ttu-id="0314a-117">Создадите шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="0314a-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="0314a-118">Создадите связанные службы для хранилища данных-источника и приемника.</span><span class="sxs-lookup"><span data-stu-id="0314a-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="0314a-119">Создания наборов данных toorepresent входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="0314a-119">Create datasets toorepresent input and output data.</span></span>
5. <span data-ttu-id="0314a-120">Создайте конвейер данными hello toomove действия копирования.</span><span class="sxs-lookup"><span data-stu-id="0314a-120">Create a pipeline with a copy activity toomove hello data.</span></span>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="0314a-121">Необходимые условия для учебника hello</span><span class="sxs-lookup"><span data-stu-id="0314a-121">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="0314a-122">Прежде чем начать в данном пошаговом руководстве, необходимо иметь hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="0314a-122">Before you begin this walkthrough, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="0314a-123">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="0314a-123">**Azure subscription**.</span></span>  <span data-ttu-id="0314a-124">Если у вас нет подписки, вы можете создать бесплатную пробную версию учетной записи всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="0314a-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0314a-125">В разделе hello [бесплатной пробной версии](http://azure.microsoft.com/pricing/free-trial/) Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="0314a-125">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="0314a-126">**исходного**хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="0314a-126">**Azure Storage Account**.</span></span> <span data-ttu-id="0314a-127">Использовать хранилище больших двоичных объектов hello как **назначения и приемника** хранилище данных в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="0314a-127">You use hello blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="0314a-128">При отсутствии учетной записи хранилища Azure в разделе hello [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account) статьи для действия toocreate один.</span><span class="sxs-lookup"><span data-stu-id="0314a-128">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="0314a-129">**SQL Server.**</span><span class="sxs-lookup"><span data-stu-id="0314a-129">**SQL Server**.</span></span> <span data-ttu-id="0314a-130">В этом руководстве используйте локальную базу данных SQL Server в качестве **исходного** хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="0314a-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="0314a-131">Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="0314a-131">Create data factory</span></span>
<span data-ttu-id="0314a-132">На этом шаге используется hello Azure портала toocreate экземпляр фабрики данных Azure с именем **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="0314a-132">In this step, you use hello Azure portal toocreate an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="0314a-133">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0314a-133">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0314a-134">Щелкните **+ New** (+ Создать), **Аналитика**, а затем — **Фабрика данных**.</span><span class="sxs-lookup"><span data-stu-id="0314a-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![Создать -> Фабрика данных](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="0314a-136">В hello **новую фабрику данных** введите **ADFTutorialOnPremDF** для hello имя.</span><span class="sxs-lookup"><span data-stu-id="0314a-136">In hello **New data factory** page, enter **ADFTutorialOnPremDF** for hello Name.</span></span>

    ![Добавить tooStartboard](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="0314a-138">Имя фабрики данных Azure hello Hello должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="0314a-138">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="0314a-139">Если ошибка hello: **имя фабрики данных «ADFTutorialOnPremDF» недоступен**, измените имя hello hello фабрики данных (например, yournameADFTutorialOnPremDF) и повторите попытку создания.</span><span class="sxs-lookup"><span data-stu-id="0314a-139">If you receive hello error: **Data factory name “ADFTutorialOnPremDF” is not available**, change hello name of hello data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="0314a-140">Выполняя оставшиеся действия, описанные в этом руководстве, вместо ADFTutorialOnPremDF используйте именно это имя.</span><span class="sxs-lookup"><span data-stu-id="0314a-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="0314a-141">Имя фабрики данных hello Hello может быть зарегистрирован как **DNS** имя в будущем hello и поэтому становятся общедоступен.</span><span class="sxs-lookup"><span data-stu-id="0314a-141">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="0314a-142">Выберите hello **подписки Azure** место hello данных фабрики toobe создан.</span><span class="sxs-lookup"><span data-stu-id="0314a-142">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="0314a-143">Выберите имеющуюся **группу ресурсов** или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="0314a-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="0314a-144">Hello учебник, создать группу ресурсов с именем: **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="0314a-144">For hello tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="0314a-145">Нажмите кнопку **создать** на hello **новую фабрику данных** страницы.</span><span class="sxs-lookup"><span data-stu-id="0314a-145">Click **Create** on hello **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="0314a-146">экземпляры toocreate фабрики данных, необходимо быть членом hello [участника фабрики данных](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) роли на уровне группы hello подписки или ресурса.</span><span class="sxs-lookup"><span data-stu-id="0314a-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="0314a-147">После завершения создания вы видите hello **фабрики данных** страницы, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="0314a-147">After creation is complete, you see hello **Data Factory** page as shown in hello following image:</span></span>

   ![Домашняя страница фабрики данных](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="0314a-149">Создание шлюза</span><span class="sxs-lookup"><span data-stu-id="0314a-149">Create gateway</span></span>
1. <span data-ttu-id="0314a-150">В hello **фабрики данных** щелкните **автор и развернуть** hello toolaunch плитки **редактор** для фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-150">In hello **Data Factory** page, click **Author and deploy** tile toolaunch hello **Editor** for hello data factory.</span></span>

    ![Плитка "Создание и развертывание"](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="0314a-152">В hello редактор фабрики данных, нажмите кнопку **... Дополнительные** на hello панели инструментов, а затем нажмите кнопку **шлюз данных**.</span><span class="sxs-lookup"><span data-stu-id="0314a-152">In hello Data Factory Editor, click **... More** on hello toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="0314a-153">Кроме того, можно щелкнуть **шлюзы данных** в hello представление в виде дерева и нажмите кнопку **шлюз данных**.</span><span class="sxs-lookup"><span data-stu-id="0314a-153">Alternatively, you can right-click **Data Gateways** in hello tree view, and click **New data gateway**.</span></span>

   ![«Новый шлюз данных» на панели инструментов](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="0314a-155">В hello **создать** введите **adftutorialgateway** для hello **имя**и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0314a-155">In hello **Create** page, enter **adftutorialgateway** for hello **name**, and click **OK**.</span></span>     

    ![Страница "Создать шлюз"](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="0314a-157">В этом пошаговом руководстве создается логический шлюза hello с только один узел (Windows на локальном компьютере).</span><span class="sxs-lookup"><span data-stu-id="0314a-157">In this walkthrough, you create hello logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="0314a-158">Шлюз управления данными можно масштабировать, объединяя несколько локальных компьютеров с hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="0314a-158">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="0314a-159">Чтобы увеличить масштаб, увеличьте число заданий перемещения данных, которые могут выполняться одновременно на узле.</span><span class="sxs-lookup"><span data-stu-id="0314a-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="0314a-160">Эта функция также доступна для логического шлюза с одним узлом.</span><span class="sxs-lookup"><span data-stu-id="0314a-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="0314a-161">Дополнительные сведения см. в статье [Шлюз управления данными: высокий уровень доступности и масштабируемость (предварительная версия)](data-factory-data-management-gateway-high-availability-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="0314a-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="0314a-162">В hello **Настройка** щелкните **установки непосредственно на этом компьютере**.</span><span class="sxs-lookup"><span data-stu-id="0314a-162">In hello **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="0314a-163">Это действие загружает установочный пакет шлюза hello hello, устанавливает, настраивает и регистрирует hello шлюз на компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-163">This action downloads hello installation package for hello gateway, installs, configures, and registers hello gateway on hello computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="0314a-164">Используйте Internet Explorer или другой веб-браузер, совместимый с Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="0314a-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="0314a-165">При использовании Chrome go toohello [Chrome веб-хранилище](https://chrome.google.com/webstore/)поиска с ключевым словом «ClickOnce», выбрав один из модулей ClickOnce hello и установить его.</span><span class="sxs-lookup"><span data-stu-id="0314a-165">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="0314a-166">Здравствуйте же для Firefox (установка надстройки).</span><span class="sxs-lookup"><span data-stu-id="0314a-166">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="0314a-167">Нажмите кнопку **открыть меню** кнопку на панели инструментов hello (**три горизонтальные линии** в правом верхнем углу hello), нажмите кнопку **надстройки**, поиска с ключевым словом «ClickOnce», выберите один из hello Расширения ClickOnce и установить его.</span><span class="sxs-lookup"><span data-stu-id="0314a-167">Click **Open Menu** button on hello toolbar (**three horizontal lines** in hello top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![Шлюз — страница "Настройка"](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="0314a-169">Таким образом является наиболее простым способом (одним щелчком) toodownload hello, установить, настроить и зарегистрировать шлюз hello один один шаг.</span><span class="sxs-lookup"><span data-stu-id="0314a-169">This way is hello easiest way (one-click) toodownload, install, configure, and register hello gateway in one single step.</span></span> <span data-ttu-id="0314a-170">Вы увидите hello **диспетчера конфигурации шлюза управления данными Майкрософт** на вашем компьютере установлено приложение.</span><span class="sxs-lookup"><span data-stu-id="0314a-170">You can see hello **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="0314a-171">Можно также найти hello исполняемый **ConfigManager.exe** в папке hello: **C:\Program Files\Microsoft данных управления Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="0314a-171">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="0314a-172">Можно также загрузить и установить шлюз вручную, используя hello ссылки на этой странице и зарегистрируйте его с помощью ключа hello показано hello **новый ключ** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="0314a-172">You can also download and install gateway manually by using hello links in this page and register it using hello key shown in hello **NEW KEY** text box.</span></span>

    <span data-ttu-id="0314a-173">В разделе [шлюз управления данными](data-factory-data-management-gateway.md) статьи для всех hello сведения о шлюзе hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0314a-174">Необходимо иметь права администратора на локальном компьютере tooinstall hello и успешно настроить hello шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="0314a-174">You must be an administrator on hello local computer tooinstall and configure hello Data Management Gateway successfully.</span></span> <span data-ttu-id="0314a-175">Можно добавить дополнительных пользователей toohello **пользователи шлюза управления данными** локальной группе Windows.</span><span class="sxs-lookup"><span data-stu-id="0314a-175">You can add additional users toohello **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="0314a-176">Hello члены этой группы могут использовать hello диспетчера конфигурации шлюза управления данными средства tooconfigure hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="0314a-176">hello members of this group can use hello Data Management Gateway Configuration Manager tool tooconfigure hello gateway.</span></span>
   >
   >
5. <span data-ttu-id="0314a-177">Подождите несколько минут или подождать, пока вы видите hello следующие сообщения уведомления:</span><span class="sxs-lookup"><span data-stu-id="0314a-177">Wait for a couple of minutes or wait until you see hello following notification message:</span></span>

    ![Установка шлюза успешно выполнена](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="0314a-179">Запустите на компьютере приложение **Диспетчер конфигурации шлюза управления данными**.</span><span class="sxs-lookup"><span data-stu-id="0314a-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="0314a-180">В hello **поиска** введите **шлюз управления данными** tooaccess этом служебной программы.</span><span class="sxs-lookup"><span data-stu-id="0314a-180">In hello **Search** window, type **Data Management Gateway** tooaccess this utility.</span></span> <span data-ttu-id="0314a-181">Можно также найти hello исполняемый **ConfigManager.exe** в папке hello: **C:\Program Files\Microsoft данных управления Gateway\2.0\Shared**</span><span class="sxs-lookup"><span data-stu-id="0314a-181">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![Диспетчер конфигурации шлюза](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="0314a-183">Убедитесь, что отображается сообщение `adftutorialgateway is connected toohello cloud service`.</span><span class="sxs-lookup"><span data-stu-id="0314a-183">Confirm that you see `adftutorialgateway is connected toohello cloud service` message.</span></span> <span data-ttu-id="0314a-184">Здравствуйте, строка hello нижней отображает состояния **подключен toohello облачной службы** вместе с **зеленый**.</span><span class="sxs-lookup"><span data-stu-id="0314a-184">hello status bar hello bottom displays **Connected toohello cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="0314a-185">На hello **Главная** вкладку, можно также сделать hello следующие операции:</span><span class="sxs-lookup"><span data-stu-id="0314a-185">On hello **Home** tab, you can also do hello following operations:</span></span>

   * <span data-ttu-id="0314a-186">**Зарегистрировать** шлюз с помощью ключа из hello портал Azure с помощью кнопки регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-186">**Register** a gateway with a key from hello Azure portal by using hello Register button.</span></span>
   * <span data-ttu-id="0314a-187">**Остановить** hello служба шлюза управления данными узла выполняется на компьютере шлюза.</span><span class="sxs-lookup"><span data-stu-id="0314a-187">**Stop** hello Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="0314a-188">**Расписание обновления** toobe установлен в определенное время дня hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-188">**Schedule updates** toobe installed at a specific time of hello day.</span></span>
   * <span data-ttu-id="0314a-189">Просмотр момент шлюза hello **последнего обновления**.</span><span class="sxs-lookup"><span data-stu-id="0314a-189">View when hello gateway was **last updated**.</span></span>
   * <span data-ttu-id="0314a-190">Укажите время, можно установить шлюз toohello обновления.</span><span class="sxs-lookup"><span data-stu-id="0314a-190">Specify time at which an update toohello gateway can be installed.</span></span>
8. <span data-ttu-id="0314a-191">Переключение toohello **параметры** вкладку hello сертификат, указанный в hello **сертификат** раздел является используется tooencrypt и расшифровки учетных данных для хранилища данных в локальной среде hello, укажите на портале hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-191">Switch toohello **Settings** tab. hello certificate specified in hello **Certificate** section is used tooencrypt/decrypt credentials for hello on-premises data store that you specify on hello portal.</span></span> <span data-ttu-id="0314a-192">(необязательно) Нажмите кнопку **изменений** toouse собственный сертификат вместо него.</span><span class="sxs-lookup"><span data-stu-id="0314a-192">(optional) Click **Change** toouse your own certificate instead.</span></span> <span data-ttu-id="0314a-193">По умолчанию hello шлюз использует сертификат hello, автоматически создаваемое hello служба фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="0314a-193">By default, hello gateway uses hello certificate that is auto-generated by hello Data Factory service.</span></span>

    ![Конфигурация сертификата шлюза](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="0314a-195">Вы также можете выполнить следующие действия с hello hello **параметры** вкладки:</span><span class="sxs-lookup"><span data-stu-id="0314a-195">You can also do hello following actions on hello **Settings** tab:</span></span>

   * <span data-ttu-id="0314a-196">Просмотр или экспорт hello сертификата, используемого шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-196">View or export hello certificate being used by hello gateway.</span></span>
   * <span data-ttu-id="0314a-197">Изменить конечную точку HTTPS hello, используемый шлюзом hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-197">Change hello HTTPS endpoint used by hello gateway.</span></span>    
   * <span data-ttu-id="0314a-198">Задайте toobe прокси-сервера HTTP, используемый шлюзом hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-198">Set an HTTP proxy toobe used by hello gateway.</span></span>     
9. <span data-ttu-id="0314a-199">(необязательно) Переключение toohello **диагностики** проверьте hello **включите подробное ведение журнала** Если tooenable требуется расширенное ведение журнала, tootroubleshoot можно использовать любые проблемы с hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="0314a-199">(optional) Switch toohello **Diagnostics** tab, check hello **Enable verbose logging** option if you want tooenable verbose logging that you can use tootroubleshoot any issues with hello gateway.</span></span> <span data-ttu-id="0314a-200">Hello сведения о ведении журнала можно найти в **средство просмотра событий** под **журналы приложений и служб** -> **шлюз управления данными** узла.</span><span class="sxs-lookup"><span data-stu-id="0314a-200">hello logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![Вкладка «Диагностика»](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="0314a-202">Можно также выполнить следующие действия в hello hello **диагностики** вкладки:</span><span class="sxs-lookup"><span data-stu-id="0314a-202">You can also perform hello following actions in hello **Diagnostics** tab:</span></span>

   * <span data-ttu-id="0314a-203">Используйте **проверить подключение** раздел tooan на локальному источнику данных с помощью шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-203">Use **Test Connection** section tooan on-premises data source using hello gateway.</span></span>
   * <span data-ttu-id="0314a-204">Нажмите кнопку **Просмотр журналов** toosee hello шлюз управления данными журнала в окне просмотра событий.</span><span class="sxs-lookup"><span data-stu-id="0314a-204">Click **View Logs** toosee hello Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="0314a-205">Нажмите кнопку **отправить журналы** tooupload ZIP-файл с журналами последние семь дней tooMicrosoft toofacilitate устранения неполадок проблем.</span><span class="sxs-lookup"><span data-stu-id="0314a-205">Click **Send Logs** tooupload a zip file with logs of last seven days tooMicrosoft toofacilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="0314a-206">На hello **диагностики** hello на вкладке **проверить подключение** выберите **SqlServer** для типа hello hello данных хранения, введите имя сервера базы данных hello, имя hello Здравствуйте, базы данных, укажите тип проверки подлинности, введите имя пользователя и пароль и нажмите кнопку **тест** tootest ли шлюз hello может подключаться toohello базы данных.</span><span class="sxs-lookup"><span data-stu-id="0314a-206">On hello **Diagnostics** tab, in hello **Test Connection** section, select **SqlServer** for hello type of hello data store, enter hello name of hello database server, name of hello database, specify authentication type, enter user name, and password, and click **Test** tootest whether hello gateway can connect toohello database.</span></span>
11. <span data-ttu-id="0314a-207">Коммутатор toohello веб-браузер и в hello **портал Azure**, нажмите кнопку **ОК** на hello **Настройка** страницы и затем на hello **шлюз данных** страница.</span><span class="sxs-lookup"><span data-stu-id="0314a-207">Switch toohello web browser, and in hello **Azure portal**, click **OK** on hello **Configure** page and then on hello **New data gateway** page.</span></span>
12. <span data-ttu-id="0314a-208">Вы увидите **adftutorialgateway** под **шлюзы данных** в древовидном представлении hello слева hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-208">You should see **adftutorialgateway** under **Data Gateways** in hello tree view on hello left.</span></span>  <span data-ttu-id="0314a-209">Если щелкнуть его, вы увидите hello связанную JSON.</span><span class="sxs-lookup"><span data-stu-id="0314a-209">If you click it, you should see hello associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="0314a-210">Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="0314a-210">Create linked services</span></span>
<span data-ttu-id="0314a-211">На этом этапе вы создадите две связанные службы: **AzureStorageLinkedService** и **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="0314a-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="0314a-212">Hello **SqlServerLinkedService** локальной базы данных SQL Server и hello ссылок **AzureStorageLinkedService** фабрикой данных Azure BLOB-объекта хранилища toohello связывает связанной службы.</span><span class="sxs-lookup"><span data-stu-id="0314a-212">hello **SqlServerLinkedService** links an on-premises SQL Server database and hello **AzureStorageLinkedService** linked service links an Azure blob store toohello data factory.</span></span> <span data-ttu-id="0314a-213">Далее в этом руководстве, копирующего данные из хранилища BLOB-объектов Azure toohello базы данных SQL Server hello локальной создать конвейер.</span><span class="sxs-lookup"><span data-stu-id="0314a-213">You create a pipeline later in this walkthrough that copies data from hello on-premises SQL Server database toohello Azure blob store.</span></span>

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a><span data-ttu-id="0314a-214">Добавить tooan связанная служба локальной базы данных SQL Server</span><span class="sxs-lookup"><span data-stu-id="0314a-214">Add a linked service tooan on-premises SQL Server database</span></span>
1. <span data-ttu-id="0314a-215">В hello **редактор фабрики данных**, нажмите кнопку **новое хранилище данных** на hello и отметьте **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="0314a-215">In hello **Data Factory Editor**, click **New data store** on hello toolbar and select **SQL Server**.</span></span>

   ![Создать связанную службу SQL Server](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="0314a-217">В hello **редактор JSON** на правом hello, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0314a-217">In hello **JSON editor** on hello right, do hello following steps:</span></span>

   1. <span data-ttu-id="0314a-218">Для hello **gatewayName**, укажите **adftutorialgateway**.</span><span class="sxs-lookup"><span data-stu-id="0314a-218">For hello **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="0314a-219">В hello **connectionString**, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0314a-219">In hello **connectionString**, do hello following steps:</span></span>    

      1. <span data-ttu-id="0314a-220">Для **servername**, введите имя hello hello сервера, на котором размещена база данных SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-220">For **servername**, enter hello name of hello server that hosts hello SQL Server database.</span></span>
      2. <span data-ttu-id="0314a-221">Для **databasename**, введите имя hello hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="0314a-221">For **databasename**, enter hello name of hello database.</span></span>
      3. <span data-ttu-id="0314a-222">Нажмите кнопку **Encrypt** на инструментов «hello».</span><span class="sxs-lookup"><span data-stu-id="0314a-222">Click **Encrypt** button on hello toolbar.</span></span> <span data-ttu-id="0314a-223">Вы видите приложение hello диспетчер учетных данных.</span><span class="sxs-lookup"><span data-stu-id="0314a-223">You see hello Credentials Manager application.</span></span>

         ![Приложение "Диспетчер учетных данных"](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="0314a-225">В hello **задать учетные данные** диалоговое окно, укажите тип проверки подлинности, имя пользователя и пароль и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0314a-225">In hello **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="0314a-226">При успешном выполнении подключения hello hello зашифрованные учетные данные хранятся в hello JSON и закрывает диалоговое окно «hello».</span><span class="sxs-lookup"><span data-stu-id="0314a-226">If hello connection is successful, hello encrypted credentials are stored in hello JSON and hello dialog box closes.</span></span>
      5. <span data-ttu-id="0314a-227">Закрытие вкладки браузера пустой hello, запустить диалоговое окно «hello», если оно не закрывается автоматически и вернуть toohello вкладка с hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0314a-227">Close hello empty browser tab that launched hello dialog box if it is not automatically closed and get back toohello tab with hello Azure portal.</span></span>

         <span data-ttu-id="0314a-228">На компьютере шлюза hello, эти учетные данные являются **зашифрованные** с помощью сертификата, который hello фабрики данных является владельцем службы.</span><span class="sxs-lookup"><span data-stu-id="0314a-228">On hello gateway machine, these credentials are **encrypted** by using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="0314a-229">Toouse hello сертификат, связанный с hello шлюз управления данными, вместо этого, в статье [задать учетные данные безопасно](#set-credentials-and-security).</span><span class="sxs-lookup"><span data-stu-id="0314a-229">If you want toouse hello certificate that is associated with hello Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="0314a-230">Нажмите кнопку **развернуть** на панели toodeploy hello связанной службы SQL Server hello команд.</span><span class="sxs-lookup"><span data-stu-id="0314a-230">Click **Deploy** on hello command bar toodeploy hello SQL Server linked service.</span></span> <span data-ttu-id="0314a-231">Вы увидите службы hello связаны в представлении дерева hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-231">You should see hello linked service in hello tree view.</span></span>

      ![Связанной службы SQL Server в представлении дерева hello](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="0314a-233">Добавление связанной службы для учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="0314a-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="0314a-234">В hello **редактор фабрики данных**, нажмите кнопку **новое хранилище данных** hello панели команд и нажмите кнопку **хранилища Azure**.</span><span class="sxs-lookup"><span data-stu-id="0314a-234">In hello **Data Factory Editor**, click **New data store** on hello command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="0314a-235">Введите имя учетной записи хранилища Azure hello для hello **имя учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="0314a-235">Enter hello name of your Azure storage account for hello **Account name**.</span></span>
3. <span data-ttu-id="0314a-236">Введите ключ hello для вашей учетной записи хранилища Azure для hello **ключ учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="0314a-236">Enter hello key for your Azure storage account for hello **Account key**.</span></span>
4. <span data-ttu-id="0314a-237">Нажмите кнопку **развернуть** toodeploy hello **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="0314a-237">Click **Deploy** toodeploy hello **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="0314a-238">Создание наборов данных</span><span class="sxs-lookup"><span data-stu-id="0314a-238">Create datasets</span></span>
<span data-ttu-id="0314a-239">На этом шаге создания входных и выходных данных наборы данных, которые представляют входные и выходные данные для операции копирования hello (база данных SQL Server в локальной среде = > хранилище больших двоичных объектов).</span><span class="sxs-lookup"><span data-stu-id="0314a-239">In this step, you create input and output datasets that represent input and output data for hello copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="0314a-240">Прежде чем создавать наборы данных, hello следующие шаги (Подробное описание действий следует за списком hello):</span><span class="sxs-lookup"><span data-stu-id="0314a-240">Before creating datasets, do hello following steps (detailed steps follows hello list):</span></span>

* <span data-ttu-id="0314a-241">Создать таблицу с именем **emp** в hello был добавлен в качестве фабрики данных toohello связанной службы базы данных SQL Server и вставить несколько записей в таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-241">Create a table named **emp** in hello SQL Server Database you added as a linked service toohello data factory and insert a couple of sample entries into hello table.</span></span>
* <span data-ttu-id="0314a-242">Создание контейнера BLOB-объекта с именем **adftutorial** в hello Azure BLOB-объектов учетной записи хранилища, которые были добавлены в качестве фабрики данных toohello связанной службы.</span><span class="sxs-lookup"><span data-stu-id="0314a-242">Create a blob container named **adftutorial** in hello Azure blob storage account you added as a linked service toohello data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a><span data-ttu-id="0314a-243">Подготовка локального SQL Server для учебника hello</span><span class="sxs-lookup"><span data-stu-id="0314a-243">Prepare On-premises SQL Server for hello tutorial</span></span>
1. <span data-ttu-id="0314a-244">В базе данных hello, указанной для hello локального SQL Server связанная служба (**SqlServerLinkedService**), используйте следующие hello toocreate скрипт SQL hello **emp** таблицы в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-244">In hello database you specified for hello on-premises SQL Server linked service (**SqlServerLinkedService**), use hello following SQL script toocreate hello **emp** table in hello database.</span></span>

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
2. <span data-ttu-id="0314a-245">Некоторые образцы вставьте в таблицу hello:</span><span class="sxs-lookup"><span data-stu-id="0314a-245">Insert some sample into hello table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="0314a-246">Создание входного набора данных</span><span class="sxs-lookup"><span data-stu-id="0314a-246">Create input dataset</span></span>

1. <span data-ttu-id="0314a-247">В hello **редактор фабрики данных**, нажмите кнопку **... Дополнительные**, нажмите кнопку **новый набор данных** hello панели команд и нажмите кнопку **таблицы SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="0314a-247">In hello **Data Factory Editor**, click **... More**, click **New dataset** on hello command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="0314a-248">Замените hello JSON в правой области hello hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="0314a-248">Replace hello JSON in hello right pane with hello following text:</span></span>

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
   <span data-ttu-id="0314a-249">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="0314a-249">Note hello following points:</span></span>

   * <span data-ttu-id="0314a-250">**Тип** задано слишком**SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="0314a-250">**type** is set too**SqlServerTable**.</span></span>
   * <span data-ttu-id="0314a-251">**tableName** задано слишком**emp**.</span><span class="sxs-lookup"><span data-stu-id="0314a-251">**tableName** is set too**emp**.</span></span>
   * <span data-ttu-id="0314a-252">**linkedServiceName** задано слишком**SqlServerLinkedService** (эта связанная служба был создан ранее в этом руководстве.).</span><span class="sxs-lookup"><span data-stu-id="0314a-252">**linkedServiceName** is set too**SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="0314a-253">Для входного набора данных, которая не создается другой конвейера в фабрике данных Azure, необходимо задать **внешних** слишком**true**.</span><span class="sxs-lookup"><span data-stu-id="0314a-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** too**true**.</span></span> <span data-ttu-id="0314a-254">Он обозначает hello входные данные — производимых внешних toohello служба фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0314a-254">It denotes hello input data is produced external toohello Azure Data Factory service.</span></span> <span data-ttu-id="0314a-255">Можно указать любой политики внешних данных, с помощью hello **externalData** элемент в hello **политики** раздела.</span><span class="sxs-lookup"><span data-stu-id="0314a-255">You can optionally specify any external data policies using hello **externalData** element in hello **Policy** section.</span></span>    

   <span data-ttu-id="0314a-256">Дополнительные сведения о свойствах файлов JSON см. в статье [Перемещение данных в базу данных SQL Server и обратно на локальных компьютерах и виртуальных машинах Azure IaaS с помощью фабрики данных Azure](data-factory-sqlserver-connector.md).</span><span class="sxs-lookup"><span data-stu-id="0314a-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="0314a-257">Нажмите кнопку **развернуть** на панели наборов данных hello toodeploy hello команд.</span><span class="sxs-lookup"><span data-stu-id="0314a-257">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="0314a-258">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="0314a-258">Create output dataset</span></span>

1. <span data-ttu-id="0314a-259">В hello **редактор фабрики данных**, нажмите кнопку **новый набор данных** hello панели команд и нажмите кнопку **хранилища больших двоичных объектов Azure**.</span><span class="sxs-lookup"><span data-stu-id="0314a-259">In hello **Data Factory Editor**, click **New dataset** on hello command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="0314a-260">Замените hello JSON в правой области hello hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="0314a-260">Replace hello JSON in hello right pane with hello following text:</span></span>

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
   <span data-ttu-id="0314a-261">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="0314a-261">Note hello following points:</span></span>

   * <span data-ttu-id="0314a-262">**Тип** задано слишком**AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="0314a-262">**type** is set too**AzureBlob**.</span></span>
   * <span data-ttu-id="0314a-263">**linkedServiceName** задано слишком**AzureStorageLinkedService** (на шаге 2 был создан эта связанная служба).</span><span class="sxs-lookup"><span data-stu-id="0314a-263">**linkedServiceName** is set too**AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="0314a-264">**folderPath** задано слишком**adftutorial/outfromonpremdf** где outfromonpremdf — папка hello в контейнере adftutorial hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-264">**folderPath** is set too**adftutorial/outfromonpremdf** where outfromonpremdf is hello folder in hello adftutorial container.</span></span> <span data-ttu-id="0314a-265">Создать hello **adftutorial** контейнера, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="0314a-265">Create hello **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="0314a-266">Hello **доступности** задано слишком**каждый час** (**частоты** значение слишком**час** и **интервал** значение слишком **1**).</span><span class="sxs-lookup"><span data-stu-id="0314a-266">hello **availability** is set too**hourly** (**frequency** set too**hour** and **interval** set too**1**).</span></span>  <span data-ttu-id="0314a-267">Hello служба фабрики данных приводит к возникновению ошибки срез данных вывода каждый час в hello **emp** таблицы в hello базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0314a-267">hello Data Factory service generates an output data slice every hour in hello **emp** table in hello Azure SQL Database.</span></span>

   <span data-ttu-id="0314a-268">Если вы не укажете **fileName** для **выходной таблицы**, hello созданные файлы в hello **folderPath** именуются в кодировке hello: данные.<Guid>. txt (например:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="0314a-268">If you do not specify a **fileName** for an **output table**, hello generated files in hello **folderPath** are named in hello following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="0314a-269">tooset **folderPath** и **fileName** динамически на основании hello **SliceStart** время, используйте свойство partitionedBy hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-269">tooset **folderPath** and **fileName** dynamically based on hello **SliceStart** time, use hello partitionedBy property.</span></span> <span data-ttu-id="0314a-270">В следующем примере hello folderPath использует год, месяц и день из hello SliceStart (время начала среза hello обрабатывается) и имя файла использует час из hello SliceStart.</span><span class="sxs-lookup"><span data-stu-id="0314a-270">In hello following example, folderPath uses Year, Month, and Day from hello SliceStart (start time of hello slice being processed) and fileName uses Hour from hello SliceStart.</span></span> <span data-ttu-id="0314a-271">Например, если срез создается для 2014-10-20T08:00:00, hello имя папки имеет значение toowikidatagateway/wikisampledataout/2014-10-20 и hello fileName является too08.csv.</span><span class="sxs-lookup"><span data-stu-id="0314a-271">For example, if a slice is being produced for 2014-10-20T08:00:00, hello folderName is set toowikidatagateway/wikisampledataout/2014/10/20 and hello fileName is set too08.csv.</span></span>

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

    <span data-ttu-id="0314a-272">Дополнительные сведения о свойствах файлов JSON см. в статье [Перемещение данных в базу данных SQL Server и обратно на локальных компьютерах и виртуальных машинах Azure IaaS с помощью фабрики данных Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="0314a-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="0314a-273">Нажмите кнопку **развернуть** на панели наборов данных hello toodeploy hello команд.</span><span class="sxs-lookup"><span data-stu-id="0314a-273">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span> <span data-ttu-id="0314a-274">Подтвердите, что вы видите оба набора данных hello в представлении дерева hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-274">Confirm that you see both hello datasets in hello tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="0314a-275">Создание конвейера</span><span class="sxs-lookup"><span data-stu-id="0314a-275">Create pipeline</span></span>
<span data-ttu-id="0314a-276">На этом шаге вы создадите **конвейер** одним **действием копирования**, для выполнения которого **EmpOnPremSQLTable** будет использоваться как входные данные, а **OutputBlobTable** — как выходные данные.</span><span class="sxs-lookup"><span data-stu-id="0314a-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="0314a-277">В редакторе фабрики данных нажмите кнопку **... Дополнительно** и **Новый конвейер**.</span><span class="sxs-lookup"><span data-stu-id="0314a-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="0314a-278">Замените hello JSON в правой области hello hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="0314a-278">Replace hello JSON in hello right pane with hello following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
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
   > <span data-ttu-id="0314a-279">Замените значение hello hello **запустить** свойство с hello текущего дня и **окончания** значение с hello следующего дня.</span><span class="sxs-lookup"><span data-stu-id="0314a-279">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span>
   >
   >

   <span data-ttu-id="0314a-280">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="0314a-280">Note hello following points:</span></span>

   * <span data-ttu-id="0314a-281">В разделе "действия" hello, есть только у действия которого **тип** задано слишком**копирования**.</span><span class="sxs-lookup"><span data-stu-id="0314a-281">In hello activities section, there is only activity whose **type** is set too**Copy**.</span></span>
   * <span data-ttu-id="0314a-282">**Входные данные** для hello действия установлено слишком**EmpOnPremSQLTable** и **вывода** для hello действия установлено слишком**OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="0314a-282">**Input** for hello activity is set too**EmpOnPremSQLTable** and **output** for hello activity is set too**OutputBlobTable**.</span></span>
   * <span data-ttu-id="0314a-283">В hello **typeProperties** разделе **SqlSource** указывается как hello **тип источника** и ** BlobSink ** указывается как hello **типприемника**.</span><span class="sxs-lookup"><span data-stu-id="0314a-283">In hello **typeProperties** section, **SqlSource** is specified as hello **source type** and **BlobSink **is specified as hello **sink type**.</span></span>
   * <span data-ttu-id="0314a-284">SQL-запрос `select * from emp` указан для hello **sqlReaderQuery** свойство **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="0314a-284">SQL query `select * from emp` is specified for hello **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="0314a-285">Даты начала и окончания должны быть в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="0314a-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="0314a-286">Например, 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="0314a-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="0314a-287">Hello **окончания** времени является необязательным, но мы используем в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="0314a-287">hello **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="0314a-288">Если не указать значение для hello **окончания** свойство, оно вычисляется как «**start + 48 часов**».</span><span class="sxs-lookup"><span data-stu-id="0314a-288">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="0314a-289">конвейер hello toorun неопределенно долгое время, укажите **9/9/9999** как значение hello для hello **окончания** свойство.</span><span class="sxs-lookup"><span data-stu-id="0314a-289">toorun hello pipeline indefinitely, specify **9/9/9999** as hello value for hello **end** property.</span></span>

   <span data-ttu-id="0314a-290">Вы определяете hello продолжительность времени, в которой hello обрабатываются срезы данных основании hello **доступности** свойства, которые были определены для каждого набора данных фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0314a-290">You are defining hello time duration in which hello data slices are processed based on hello **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="0314a-291">В примере hello нет 24 срезы данных, как каждый срез данных создается каждый час.</span><span class="sxs-lookup"><span data-stu-id="0314a-291">In hello example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="0314a-292">Нажмите кнопку **развернуть** на панели наборов данных hello toodeploy hello команд (таблица представляет собой прямоугольный набор данных).</span><span class="sxs-lookup"><span data-stu-id="0314a-292">Click **Deploy** on hello command bar toodeploy hello dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="0314a-293">Подтвердите конвейера hello отображается в представлении дерева hello в **конвейеры** узла.</span><span class="sxs-lookup"><span data-stu-id="0314a-293">Confirm that hello pipeline shows up in hello tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="0314a-294">Теперь щелкните **X** дважды tooclose hello страницы tooget назад toohello **фабрики данных** страница hello **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="0314a-294">Now, click **X** twice tooclose hello page tooget back toohello **Data Factory** page for hello **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="0314a-295">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="0314a-295">**Congratulations!**</span></span> <span data-ttu-id="0314a-296">Успешно создана фабрикой данных Azure, связанные службы, наборы данных и конвейера и запланированных hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="0314a-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled hello pipeline.</span></span>

#### <a name="view-hello-data-factory-in-a-diagram-view"></a><span data-ttu-id="0314a-297">Фабрика данных hello представления в представлении диаграммы</span><span class="sxs-lookup"><span data-stu-id="0314a-297">View hello data factory in a Diagram View</span></span>
1. <span data-ttu-id="0314a-298">В hello **портал Azure**, нажмите кнопку **схема** плитки на домашней странице приветствия для hello **ADFTutorialOnPremDF** фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="0314a-298">In hello **Azure portal**, click **Diagram** tile on hello home page for hello **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="0314a-299">:</span><span class="sxs-lookup"><span data-stu-id="0314a-299">:</span></span>

    ![Ссылка на схему](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="0314a-301">Вы увидите примерно toohello hello диаграммы после изображения:</span><span class="sxs-lookup"><span data-stu-id="0314a-301">You should see hello diagram similar toohello following image:</span></span>

    ![Представление схемы](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="0314a-303">Увеличить масштаб, уменьшить масштаб масштаба too100% toofit масштаба, автоматически позиции конвейеры и наборы данных и отображения сведений журнала обращений и преобразований (выделяет восходящие и нисходящие для выбранных элементов).</span><span class="sxs-lookup"><span data-stu-id="0314a-303">You can zoom in, zoom out, zoom too100%, zoom toofit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="0314a-304">Его можно дважды щелкнуть свойства toosee объекта (набор данных ввода вывода или конвейера).</span><span class="sxs-lookup"><span data-stu-id="0314a-304">You can double-click an object (input/output dataset or pipeline) toosee properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="0314a-305">Отслеживание конвейера</span><span class="sxs-lookup"><span data-stu-id="0314a-305">Monitor pipeline</span></span>
<span data-ttu-id="0314a-306">На этом шаге используется hello Azure портала toomonitor, происходящем в фабрикой данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0314a-306">In this step, you use hello Azure portal toomonitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="0314a-307">Можно также использовать командлеты PowerShell toomonitor-наборы данных и конвейеры.</span><span class="sxs-lookup"><span data-stu-id="0314a-307">You can also use PowerShell cmdlets toomonitor datasets and pipelines.</span></span> <span data-ttu-id="0314a-308">Дополнительные сведения о мониторинге см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="0314a-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="0314a-309">В диаграмме hello, дважды щелкните **EmpOnPremSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="0314a-309">In hello diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![Срезы EmpOnPremSQLTable](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="0314a-311">Обратите внимание, что все данные hello срезы копии находятся в **готовности** состоянии, так как длительность конвейера hello (время начала время tooend) находится в прошлом hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-311">Notice that all hello data slices up are in **Ready** state because hello pipeline duration (start time tooend time) is in hello past.</span></span> <span data-ttu-id="0314a-312">Можно также из-за вставки данных hello в базе данных SQL Server hello и есть ли все время hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-312">It is also because you have inserted hello data in hello SQL Server database and it is there all hello time.</span></span> <span data-ttu-id="0314a-313">Убедитесь, что нет срезов показываться в hello **фрагменты проблема** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-313">Confirm that no slices show up in hello **Problem slices** section at hello bottom.</span></span> <span data-ttu-id="0314a-314">Щелкните все срезы hello tooview **разделе более** hello нижней части списка hello фрагментов.</span><span class="sxs-lookup"><span data-stu-id="0314a-314">tooview all hello slices, click **See More** at hello bottom of hello list of slices.</span></span>
3. <span data-ttu-id="0314a-315">Теперь в hello **наборы данных** щелкните **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="0314a-315">Now, In hello **Datasets** page, click **OutputBlobTable**.</span></span>

    ![Срезы OputputBlobTable](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="0314a-317">Щелкните любой сегмент данных из списка hello и вы увидите hello **срез данных** страницы.</span><span class="sxs-lookup"><span data-stu-id="0314a-317">Click any data slice from hello list and you should see hello **Data Slice** page.</span></span> <span data-ttu-id="0314a-318">Вы увидите, что действие выполняется срез hello.</span><span class="sxs-lookup"><span data-stu-id="0314a-318">You see activity runs for hello slice.</span></span> <span data-ttu-id="0314a-319">Как правило, в этом разделе отображается только одно действие.</span><span class="sxs-lookup"><span data-stu-id="0314a-319">You see only one activity run usually.</span></span>  

    ![Колонка среза данных](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="0314a-321">Если срез hello не hello **готовности** состояние, можно увидеть hello восходящие срезы, которые еще не готовы и блокируют hello текущего среза выполнения в hello **восходящие срезы, которые не готовы** списка.</span><span class="sxs-lookup"><span data-stu-id="0314a-321">If hello slice is not in hello **Ready** state, you can see hello upstream slices that are not Ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="0314a-322">Нажмите кнопку hello **при выполнении действия** из списка hello hello нижней toosee **сведения о выполнении действия**.</span><span class="sxs-lookup"><span data-stu-id="0314a-322">Click hello **activity run** from hello list at hello bottom toosee **activity run details**.</span></span>

   ![Страница "Подробности о выполнении операции"](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="0314a-324">Вы увидите сведения, например пропускную способность, продолжительность и шлюза hello использовать tootransfer hello данных.</span><span class="sxs-lookup"><span data-stu-id="0314a-324">You would see information such as throughput, duration, and hello gateway used tootransfer hello data.</span></span>
6. <span data-ttu-id="0314a-325">Нажмите кнопку **X** tooclose все Здравствуйте страниц, пока не будет</span><span class="sxs-lookup"><span data-stu-id="0314a-325">Click **X** tooclose all hello pages until you</span></span>
7. <span data-ttu-id="0314a-326">вернуться к домашней странице toohello hello **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="0314a-326">get back toohello home page for hello **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="0314a-327">(Необязательно.) Щелкните **Конвейеры**, а затем — **ADFTutorialOnPremDF** и просмотрите параметры входных таблиц (**Использовано**) или выходных наборов данных (**Выполнено**).</span><span class="sxs-lookup"><span data-stu-id="0314a-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="0314a-328">Использовать инструменты, такие как [обозреватель хранилищ Microsoft](http://storageexplorer.com/) tooverify, что большой двоичный объект или файл создается за каждый час.</span><span class="sxs-lookup"><span data-stu-id="0314a-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) tooverify that a blob/file is created for each hour.</span></span>

   ![обозреватель хранилищ Azure](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="0314a-330">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0314a-330">Next steps</span></span>
* <span data-ttu-id="0314a-331">В разделе [шлюз управления данными](data-factory-data-management-gateway.md) статьи для всех hello сведения о hello шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="0314a-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello Data Management Gateway.</span></span>
* <span data-ttu-id="0314a-332">В разделе [копирования данных из больших двоичных объектов Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn о как toouse действие копирования toomove данных из источника данных в хранилище tooa приемник данных.</span><span class="sxs-lookup"><span data-stu-id="0314a-332">See [Copy data from Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn about how toouse Copy Activity toomove data from a source data store tooa sink data store.</span></span>
