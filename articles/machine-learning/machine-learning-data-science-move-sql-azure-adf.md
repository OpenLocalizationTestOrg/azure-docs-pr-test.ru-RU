---
title: "aaaMove данные из локального SQL Server tooSQL Azure с фабрикой данных Azure | Документы Microsoft"
description: "Настройка конвейер ADF, которая состоит из двух действий миграции данных, которые совместно перемещают данные ежедневно между базами данных в локальной среде и в облаке hello."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a><span data-ttu-id="67379-103">Перемещение данных из локальной tooSQL сервера SQL Azure с фабрикой данных Azure</span><span class="sxs-lookup"><span data-stu-id="67379-103">Move data from an on-premises SQL server tooSQL Azure with Azure Data Factory</span></span>
<span data-ttu-id="67379-104">В этом разделе показано, как toomove данные из локальной базы данных SQL Server tooa база данных SQL Azure через хранилище больших двоичных объектов Azure с помощью hello фабрики данных Azure (ADF).</span><span class="sxs-lookup"><span data-stu-id="67379-104">This topic shows how toomove data from an on-premises SQL Server Database tooa SQL Azure Database via Azure Blob Storage using hello Azure Data Factory (ADF).</span></span>

<span data-ttu-id="67379-105">Для таблицы, перечислены различные параметры для перемещения данных tooan базы данных SQL Azure, в разделе [перемещение данных tooan базы данных SQL Azure для машинного обучения Azure](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="67379-105">For a table that summarizes various options for moving data tooan Azure SQL Database, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

## <span data-ttu-id="67379-106"><a name="intro"></a>Общие сведения: Что такое ADF и когда он должен быть используется toomigrate данных?</span><span class="sxs-lookup"><span data-stu-id="67379-106"><a name="intro"></a>Introduction: What is ADF and when should it be used toomigrate data?</span></span>
<span data-ttu-id="67379-107">Фабрика данных Azure — это служба интеграции полностью управляемая данных на основе облака, координирует и автоматизирует процессы hello перемещения и преобразования данных.</span><span class="sxs-lookup"><span data-stu-id="67379-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="67379-108">Ключевым принципом Hello hello ADF модели является конвейера.</span><span class="sxs-lookup"><span data-stu-id="67379-108">hello key concept in hello ADF model is pipeline.</span></span> <span data-ttu-id="67379-109">Конвейер — это логическое группирование действий, каждое из которых определяет действия tooperform hello на hello данные, содержащиеся в наборах данных.</span><span class="sxs-lookup"><span data-stu-id="67379-109">A pipeline is a logical grouping of Activities, each of which defines hello actions tooperform on hello data contained in Datasets.</span></span> <span data-ttu-id="67379-110">Связанные службы, используемые toodefine hello сведения, необходимые для фабрики данных tooconnect toohello данных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="67379-110">Linked services are used toodefine hello information needed for Data Factory tooconnect toohello data resources.</span></span>

<span data-ttu-id="67379-111">С ADF существующие службы обработки данных могут быть включены в конвейерах данных, которые высокодоступной и управляемой в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="67379-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in hello cloud.</span></span> <span data-ttu-id="67379-112">Конвейеры этих данных может быть запланированных tooingest, подготовка, преобразование, анализ и публиковать данные и управляет hello сложных данных и обработки зависимости и управляет им ADF.</span><span class="sxs-lookup"><span data-stu-id="67379-112">These data pipelines can be scheduled tooingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates hello complex data and processing dependencies.</span></span> <span data-ttu-id="67379-113">Решения могут быть hello быстро встроенного и развернутого в облаке, подключение все большее число локальных и облачных источников данных.</span><span class="sxs-lookup"><span data-stu-id="67379-113">Solutions can be quickly built and deployed in hello cloud, connecting a growing number of on-premises and cloud data sources.</span></span>

<span data-ttu-id="67379-114">ADF стоит использовать в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="67379-114">Consider using ADF:</span></span>

* <span data-ttu-id="67379-115">Когда данные toobe потребности постоянно перенесены в гибридном сценарии, который обращается к оба локальные и облачные ресурсы</span><span class="sxs-lookup"><span data-stu-id="67379-115">when data needs toobe continually migrated in a hybrid scenario that accesses both on-premises and cloud resources</span></span>
* <span data-ttu-id="67379-116">добавить при переносе tooit при транзакции данных hello или toobe потребностей изменен или иметь бизнес-логики.</span><span class="sxs-lookup"><span data-stu-id="67379-116">when hello data is transacted or needs toobe modified or have business logic added tooit when being migrated.</span></span>

<span data-ttu-id="67379-117">ADF позволяет hello планирования и отслеживания заданий, используя простые сценарии JSON, управлять hello перемещение данных на периодической основе.</span><span class="sxs-lookup"><span data-stu-id="67379-117">ADF allows for hello scheduling and monitoring of jobs using simple JSON scripts that manage hello movement of data on a periodic basis.</span></span> <span data-ttu-id="67379-118">ADF также обладает другими возможностями, такими как поддержка сложных операций.</span><span class="sxs-lookup"><span data-stu-id="67379-118">ADF also has other capabilities such as support for complex operations.</span></span> <span data-ttu-id="67379-119">Дополнительные сведения о ADF документации hello в [фабрики данных Azure (ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="67379-119">For more information on ADF, see hello documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span></span>

## <span data-ttu-id="67379-120"><a name="scenario"></a>Hello сценария</span><span class="sxs-lookup"><span data-stu-id="67379-120"><a name="scenario"></a>hello Scenario</span></span>
<span data-ttu-id="67379-121">Мы настраиваем конвейер ADF, который объединяет два действия переноса данных.</span><span class="sxs-lookup"><span data-stu-id="67379-121">We set up an ADF pipeline that composes two data migration activities.</span></span> <span data-ttu-id="67379-122">Вместе они перемещаются данные ежедневно между локальной базы данных SQL и базы данных SQL Azure в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="67379-122">Together they move data on a daily basis between an on-premises SQL database and an Azure SQL Database in hello cloud.</span></span> <span data-ttu-id="67379-123">Hello два действия являются:</span><span class="sxs-lookup"><span data-stu-id="67379-123">hello two activities are:</span></span>

* <span data-ttu-id="67379-124">копирование данных из tooan базы данных SQL Server в локальной учетной записи хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="67379-124">copy data from an on-premises SQL Server database tooan Azure Blob Storage account</span></span>
* <span data-ttu-id="67379-125">Копирует данные из tooan учетной записи хранилища больших двоичных объектов hello базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="67379-125">copy data from hello Azure Blob Storage account tooan Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="67379-126">Здравствуйте, описанного здесь было адаптировать из более подробные учебник, обеспечиваемый hello ADF hello: [перемещения данных между локальным источникам и облако с помощью шлюза управления данными](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) ссылается на toohello соответствующие разделы этой статьи предоставляются, когда это необходимо.</span><span class="sxs-lookup"><span data-stu-id="67379-126">hello steps shown here have been adapted from hello more detailed tutorial provided by hello ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) References toohello relevant sections of that topic are provided when appropriate.</span></span>
>
>

## <span data-ttu-id="67379-127"><a name="prereqs"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="67379-127"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="67379-128">Для выполнения действий, описанных в этом учебнике, вам необходимо следующее.</span><span class="sxs-lookup"><span data-stu-id="67379-128">This tutorial assumes you have:</span></span>

* <span data-ttu-id="67379-129"><seg>
  **Подписка Azure**.</seg></span><span class="sxs-lookup"><span data-stu-id="67379-129">An **Azure subscription**.</span></span> <span data-ttu-id="67379-130">Если у вас нет подписки, вы можете зарегистрироваться для получения [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="67379-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="67379-131">**Azure storage account**.</span><span class="sxs-lookup"><span data-stu-id="67379-131">An **Azure storage account**.</span></span> <span data-ttu-id="67379-132">Использовать учетную запись хранилища Azure для хранения данных hello в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="67379-132">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="67379-133">При отсутствии учетной записи хранилища Azure в разделе hello [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account) статьи.</span><span class="sxs-lookup"><span data-stu-id="67379-133">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="67379-134">После создания учетной записи хранилища hello необходимо tooobtain hello от имени учетной записи хранилища hello tooaccess использования ключа.</span><span class="sxs-lookup"><span data-stu-id="67379-134">After you have created hello storage account, you need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="67379-135">Ознакомьтесь с разделом [Управление ключами доступа к хранилищу](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="67379-135">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="67379-136">Доступ tooan **базы данных SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="67379-136">Access tooan **Azure SQL Database**.</span></span> <span data-ttu-id="67379-137">Если необходимо настроить базы данных SQL Azure, hello tpoic [Приступая к работе с базой данных SQL Microsoft Azure ](../sql-database/sql-database-get-started.md) предоставляет сведения о том, как tooprovision новый экземпляр базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="67379-137">If you must set up an Azure SQL Database, hello tpoic [Getting Started with Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) provides information on how tooprovision a new instance of an Azure SQL Database.</span></span>
* <span data-ttu-id="67379-138">Установленная и настроенная локальная среда **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="67379-138">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="67379-139">Инструкции см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="67379-139">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!NOTE]
> <span data-ttu-id="67379-140">В этой процедуре используется hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="67379-140">This procedure uses hello [Azure portal](https://portal.azure.com/).</span></span>
>
>

## <span data-ttu-id="67379-141"><a name="upload-data"></a>Отправка hello данных tooyour локального SQL Server</span><span class="sxs-lookup"><span data-stu-id="67379-141"><a name="upload-data"></a> Upload hello data tooyour on-premises SQL Server</span></span>
<span data-ttu-id="67379-142">Мы используем hello [NYC такси dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) процесс миграции toodemonstrate hello.</span><span class="sxs-lookup"><span data-stu-id="67379-142">We use hello [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) toodemonstrate hello migration process.</span></span> <span data-ttu-id="67379-143">Hello такси NYC набор данных доступен, описанных в этой записи в хранилище больших двоичных объектов [NYC такси данных](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="67379-143">hello NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="67379-144">Hello данные содержат два файла, файл trip_data.csv hello, который содержит сведения о пути, и hello trip_far.csv файл, содержащий сведения о тариф авиакомпании hello платная для каждого маршрута.</span><span class="sxs-lookup"><span data-stu-id="67379-144">hello data has two files, hello trip_data.csv file, which contains trip details, and hello  trip_far.csv file, which contains details of hello fare paid for each trip.</span></span> <span data-ttu-id="67379-145">Пример и описание этих файлов приведены в [описании набора данных «Поездки такси Нью-Йорка»](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span><span class="sxs-lookup"><span data-stu-id="67379-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span></span>

<span data-ttu-id="67379-146">Можно адаптировать hello процедуры, описанные здесь tooa набор данных или действуйте hello, как описано с помощью hello такси NYC набора данных.</span><span class="sxs-lookup"><span data-stu-id="67379-146">You can either adapt hello procedure provided here tooa set of your own data or follow hello steps as described by using hello NYC Taxi dataset.</span></span> <span data-ttu-id="67379-147">hello tooupload такси NYC набора данных в базу данных SQL Server в локальной среде, выполните процедуру hello, описанные в [массового импорта данных в базу данных SQL Server](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span><span class="sxs-lookup"><span data-stu-id="67379-147">tooupload hello NYC Taxi dataset into your on-premises SQL Server database, follow hello procedure outlined in [Bulk Import Data into SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span></span> <span data-ttu-id="67379-148">Эти инструкции относятся к SQL Server на виртуальной машине Azure, но hello процедур для передачи toohello находится на локальном сервере SQL Server hello таким же.</span><span class="sxs-lookup"><span data-stu-id="67379-148">These instructions are for a SQL Server on an Azure Virtual Machine, but hello procedure for uploading toohello on-premises SQL Server is hello same.</span></span>

## <span data-ttu-id="67379-149"><a name="create-adf"></a> Создание фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="67379-149"><a name="create-adf"></a> Create an Azure Data Factory</span></span>
<span data-ttu-id="67379-150">Здравствуйте, инструкции по созданию новой фабрики данных Azure и группы ресурсов в hello [портал Azure](https://portal.azure.com/) предоставляются [создания фабрики данных Azure](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span><span class="sxs-lookup"><span data-stu-id="67379-150">hello instructions for creating a new Azure Data Factory and a resource group in hello [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span></span> <span data-ttu-id="67379-151">Новый экземпляр ADF имя hello *adfdsp* и создание группы ресурсов имя hello *adfdsprg*.</span><span class="sxs-lookup"><span data-stu-id="67379-151">Name hello new ADF instance *adfdsp* and name hello resource group created *adfdsprg*.</span></span>

## <a name="install-and-configure-up-hello-data-management-gateway"></a><span data-ttu-id="67379-152">Установить и настроить шлюз управления данными hello</span><span class="sxs-lookup"><span data-stu-id="67379-152">Install and configure up hello Data Management Gateway</span></span>
<span data-ttu-id="67379-153">tooenable конвейеры toowork фабрики данных Azure с SQL Server в локальной среде, необходимо tooadd его как фабрика данных toohello связанной службы.</span><span class="sxs-lookup"><span data-stu-id="67379-153">tooenable your pipelines in an Azure data factory toowork with an on-premises SQL Server, you need tooadd it as a Linked Service toohello data factory.</span></span> <span data-ttu-id="67379-154">toocreate связанной службы локального сервера SQL Server, необходимо выполнить следующее:</span><span class="sxs-lookup"><span data-stu-id="67379-154">toocreate a Linked Service for an on-premises SQL Server, you must:</span></span>

* <span data-ttu-id="67379-155">Загрузите и установите шлюз управления данными Майкрософт на hello на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="67379-155">download and install Microsoft Data Management Gateway onto hello on-premises computer.</span></span>
* <span data-ttu-id="67379-156">Настройте службу hello связаны для hello локального источника данных toouse hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="67379-156">configure hello linked service for hello on-premises data source toouse hello gateway.</span></span>

<span data-ttu-id="67379-157">Шлюз управления данными Hello сериализует и десериализует данные источника и приемника hello, на компьютере hello, в котором она размещена.</span><span class="sxs-lookup"><span data-stu-id="67379-157">hello Data Management Gateway serializes and deserializes hello source and sink data on hello computer where it is hosted.</span></span>

<span data-ttu-id="67379-158">Инструкции по установке и сведения о шлюзе управления данными см. в статье [Перемещение данных между локальными источниками и облаком при помощи шлюза управления данными](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="67379-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span></span>

## <span data-ttu-id="67379-159"><a name="adflinkedservices"></a>Создание связанных служб tooconnect toohello ресурсы данных</span><span class="sxs-lookup"><span data-stu-id="67379-159"><a name="adflinkedservices"></a>Create linked services tooconnect toohello data resources</span></span>
<span data-ttu-id="67379-160">Связанная служба определяет hello сведения, необходимые для ресурса данных tooa tooconnect фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="67379-160">A linked service defines hello information needed for Azure Data Factory tooconnect tooa data resource.</span></span> <span data-ttu-id="67379-161">Hello пошаговые инструкции для создания связанных служб предоставляется в [создания связанных служб](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span><span class="sxs-lookup"><span data-stu-id="67379-161">hello step-by-step procedure for creating linked services is provided in [Create linked services](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span></span>

<span data-ttu-id="67379-162">В данном сценарии есть три ресурса, для которых требуются связанные службы.</span><span class="sxs-lookup"><span data-stu-id="67379-162">We have three resources in this scenario for which linked services are needed.</span></span>

1. [<span data-ttu-id="67379-163">Связанная служба для локального SQL Server</span><span class="sxs-lookup"><span data-stu-id="67379-163">Linked service for on-premises SQL Server</span></span>](#adf-linked-service-onprem-sql)
2. [<span data-ttu-id="67379-164">Связанная служба для хранилища больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="67379-164">Linked service for Azure Blob Storage</span></span>](#adf-linked-service-blob-store)
3. [<span data-ttu-id="67379-165">Связанная служба для базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="67379-165">Linked service for Azure SQL database</span></span>](#adf-linked-service-azure-sql)

### <span data-ttu-id="67379-166"><a name="adf-linked-service-onprem-sql"></a>Связанная служба для базы данных локального SQL Server</span><span class="sxs-lookup"><span data-stu-id="67379-166"><a name="adf-linked-service-onprem-sql"></a>Linked service for on-premises SQL Server database</span></span>
<span data-ttu-id="67379-167">Служба hello связаны toocreate для hello локального SQL Server:</span><span class="sxs-lookup"><span data-stu-id="67379-167">toocreate hello linked service for hello on-premises SQL Server:</span></span>

* <span data-ttu-id="67379-168">Нажмите кнопку hello **хранилище данных** в hello ADF целевая страница на классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="67379-168">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="67379-169">Выберите **SQL** и введите hello *username* и *пароль* учетные данные для hello локального SQL Server.</span><span class="sxs-lookup"><span data-stu-id="67379-169">select **SQL** and enter hello *username* and *password* credentials for hello on-premises SQL Server.</span></span> <span data-ttu-id="67379-170">Требуется servername hello tooenter как **имени экземпляра обратную косую черту полное доменное имя сервера (имя_сервера\имя_экземпляра)**.</span><span class="sxs-lookup"><span data-stu-id="67379-170">You need tooenter hello servername as a **fully qualified servername backslash instance name (servername\instancename)**.</span></span> <span data-ttu-id="67379-171">Hello имя связанной службы *adfonpremsql*.</span><span class="sxs-lookup"><span data-stu-id="67379-171">Name hello linked service *adfonpremsql*.</span></span>

### <span data-ttu-id="67379-172"><a name="adf-linked-service-blob-store"></a>Связанная служба для больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="67379-172"><a name="adf-linked-service-blob-store"></a>Linked service for Blob</span></span>
<span data-ttu-id="67379-173">toocreate hello связанной службы для учетной записи хранилища больших двоичных объектов hello:</span><span class="sxs-lookup"><span data-stu-id="67379-173">toocreate hello linked service for hello Azure Blob Storage account:</span></span>

* <span data-ttu-id="67379-174">Нажмите кнопку hello **хранилище данных** в hello ADF целевая страница на классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="67379-174">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="67379-175">выберите **Учетная запись хранения Azure**</span><span class="sxs-lookup"><span data-stu-id="67379-175">select **Azure Storage Account**</span></span>
* <span data-ttu-id="67379-176">Введите hello хранилища больших двоичных объектов Azure имя учетной записи ключа и контейнера.</span><span class="sxs-lookup"><span data-stu-id="67379-176">enter hello Azure Blob Storage account key and container name.</span></span> <span data-ttu-id="67379-177">Hello имя связанной службы *adfds*.</span><span class="sxs-lookup"><span data-stu-id="67379-177">Name hello Linked Service *adfds*.</span></span>

### <span data-ttu-id="67379-178"><a name="adf-linked-service-azure-sql"></a>Связанная служба для базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="67379-178"><a name="adf-linked-service-azure-sql"></a>Linked service for Azure SQL database</span></span>
<span data-ttu-id="67379-179">toocreate hello связанной службы для hello базы данных SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="67379-179">toocreate hello linked service for hello Azure SQL Database:</span></span>

* <span data-ttu-id="67379-180">Нажмите кнопку hello **хранилище данных** в hello ADF целевая страница на классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="67379-180">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="67379-181">Выберите **Azure SQL** и введите hello *username* и *пароль* учетные данные для hello базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="67379-181">select **Azure SQL** and enter hello *username* and *password* credentials for hello Azure SQL Database.</span></span> <span data-ttu-id="67379-182">Hello *username* должен быть указан как  *user@servername* .</span><span class="sxs-lookup"><span data-stu-id="67379-182">hello *username* must be specified as *user@servername*.</span></span>   

## <span data-ttu-id="67379-183"><a name="adf-tables"></a>Определение и создание таблиц toospecify как tooaccess hello наборов данных</span><span class="sxs-lookup"><span data-stu-id="67379-183"><a name="adf-tables"></a>Define and create tables toospecify how tooaccess hello datasets</span></span>
<span data-ttu-id="67379-184">Создание таблиц, задающих структуры hello, расположение и доступность hello наборов данных с помощью следующих процедур на основе сценария hello.</span><span class="sxs-lookup"><span data-stu-id="67379-184">Create tables that specify hello structure, location, and availability of hello datasets with hello following script-based procedures.</span></span> <span data-ttu-id="67379-185">Файлы JSON — это таблицы используется toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="67379-185">JSON files are used toodefine hello tables.</span></span> <span data-ttu-id="67379-186">Дополнительные сведения о структуре hello этих файлов см. в разделе [наборы данных](../data-factory/data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="67379-186">For more information on hello structure of these files, see [Datasets](../data-factory/data-factory-create-datasets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="67379-187">Необходимо выполнить hello `Add-AzureAccount` командлет перед выполнением hello [New AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) tooconfirm командлета, hello подписки справа Azure установлен для выполнения команды hello.</span><span class="sxs-lookup"><span data-stu-id="67379-187">You should execute hello `Add-AzureAccount` cmdlet before executing hello [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet tooconfirm that hello right Azure subscription is selected for hello command execution.</span></span> <span data-ttu-id="67379-188">Документацию по этим командлетам см. в статье [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="67379-188">For documentation of this cmdlet, see [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span></span>
>
>

<span data-ttu-id="67379-189">определения на основе JSON Hello в таблицах hello использовать hello следующие имена:</span><span class="sxs-lookup"><span data-stu-id="67379-189">hello JSON-based definitions in hello tables use hello following names:</span></span>

* <span data-ttu-id="67379-190">Hello **имя таблицы** в hello в локальной среде SQL server — *nyctaxi_data*</span><span class="sxs-lookup"><span data-stu-id="67379-190">hello **table name** in hello on-premises SQL server is *nyctaxi_data*</span></span>
* <span data-ttu-id="67379-191">Hello **имя контейнера** в hello хранилища больших двоичных объектов учетная запись является *имя_контейнера*</span><span class="sxs-lookup"><span data-stu-id="67379-191">hello **container name** in hello Azure Blob Storage account is *containername*</span></span>  

<span data-ttu-id="67379-192">Для этого конвейера ADF необходимо определить три таблицы:</span><span class="sxs-lookup"><span data-stu-id="67379-192">Three table definitions are needed for this ADF pipeline:</span></span>

1. <span data-ttu-id="67379-193">[Локальная таблица SQL](#adf-table-onprem-sql).</span><span class="sxs-lookup"><span data-stu-id="67379-193">[SQL on-premises Table](#adf-table-onprem-sql)</span></span>
2. [<span data-ttu-id="67379-194">таблица больших двоичных объектов; </span><span class="sxs-lookup"><span data-stu-id="67379-194">Blob Table </span></span>](#adf-table-blob-store)
3. [<span data-ttu-id="67379-195">таблица SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="67379-195">SQL Azure Table</span></span>](#adf-table-azure-sql)

> [!NOTE]
> <span data-ttu-id="67379-196">Эти процедуры используйте toodefine Azure PowerShell и создайте hello ADF действий.</span><span class="sxs-lookup"><span data-stu-id="67379-196">These procedures use Azure PowerShell toodefine and create hello ADF activities.</span></span> <span data-ttu-id="67379-197">Однако эти задачи можно также выполнить при помощи hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="67379-197">But these tasks can also be accomplished using hello Azure portal.</span></span> <span data-ttu-id="67379-198">Дополнительные сведения см. в разделе [Создание наборов данных](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span><span class="sxs-lookup"><span data-stu-id="67379-198">For details, see [Create datasets](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span></span>
>
>

### <span data-ttu-id="67379-199"><a name="adf-table-onprem-sql"></a>Локальная таблица SQL</span><span class="sxs-lookup"><span data-stu-id="67379-199"><a name="adf-table-onprem-sql"></a>SQL on-premises Table</span></span>
<span data-ttu-id="67379-200">Определение таблицы Hello для hello локального SQL Server, указанного в hello следующий JSON-файла:</span><span class="sxs-lookup"><span data-stu-id="67379-200">hello table definition for hello on-premises SQL Server is specified in hello following JSON file:</span></span>

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

<span data-ttu-id="67379-201">имена столбцов Hello не были включены здесь.</span><span class="sxs-lookup"><span data-stu-id="67379-201">hello column names were not included here.</span></span> <span data-ttu-id="67379-202">Можно подзапроса select на приветствия имен столбцов, включая их здесь (сведений проверьте hello [документации ADF](../data-factory/data-factory-data-movement-activities.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="67379-202">You can sub-select on hello column names by including them here (for details check hello [ADF documentation](../data-factory/data-factory-data-movement-activities.md) topic.</span></span>

<span data-ttu-id="67379-203">Копирование определения JSON hello hello таблицы в файл с именем *onpremtabledef.json* файл и сохраните его tooa известно расположение (здесь предполагается, что toobe *C:\temp\onpremtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="67379-203">Copy hello JSON definition of hello table into a file called *onpremtabledef.json* file and save it tooa known location (here assumed toobe *C:\temp\onpremtabledef.json*).</span></span> <span data-ttu-id="67379-204">Создайте таблицу hello в ADF с hello, выполнив командлет Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="67379-204">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <span data-ttu-id="67379-205"><a name="adf-table-blob-store"></a>таблица больших двоичных объектов;</span><span class="sxs-lookup"><span data-stu-id="67379-205"><a name="adf-table-blob-store"></a>Blob Table</span></span>
<span data-ttu-id="67379-206">Определение таблицы hello для hello выходные данные больших двоичных объектов находятся в следующих hello (сопоставляет полученный hello данных из большого двоичного объекта в локальной tooAzure):</span><span class="sxs-lookup"><span data-stu-id="67379-206">Definition for hello table for hello output blob location is in hello following (this maps hello ingested data from on-premises tooAzure blob):</span></span>

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

<span data-ttu-id="67379-207">Копирование определения JSON hello hello таблицы в файл с именем *bloboutputtabledef.json* файл и сохраните его tooa известно расположение (здесь предполагается, что toobe *C:\temp\bloboutputtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="67379-207">Copy hello JSON definition of hello table into a file called *bloboutputtabledef.json* file and save it tooa known location (here assumed toobe *C:\temp\bloboutputtabledef.json*).</span></span> <span data-ttu-id="67379-208">Создайте таблицу hello в ADF с hello, выполнив командлет Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="67379-208">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <span data-ttu-id="67379-209"><a name="adf-table-azure-sq"></a>таблица SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="67379-209"><a name="adf-table-azure-sq"></a>SQL Azure Table</span></span>
<span data-ttu-id="67379-210">Определение таблицы hello для приветствия выходных данных SQL Azure имеет следующие hello (Эта схема сопоставляет hello данные поступают из hello больших двоичных объектов):</span><span class="sxs-lookup"><span data-stu-id="67379-210">Definition for hello table for hello SQL Azure output is in hello following (this schema maps hello data coming from hello blob):</span></span>

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

<span data-ttu-id="67379-211">Копирование определения JSON hello hello таблицы в файл с именем *AzureSqlTable.json* файл и сохраните его tooa известно расположение (здесь предполагается, что toobe *C:\temp\AzureSqlTable.json*).</span><span class="sxs-lookup"><span data-stu-id="67379-211">Copy hello JSON definition of hello table into a file called *AzureSqlTable.json* file and save it tooa known location (here assumed toobe *C:\temp\AzureSqlTable.json*).</span></span> <span data-ttu-id="67379-212">Создайте таблицу hello в ADF с hello, выполнив командлет Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="67379-212">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <span data-ttu-id="67379-213"><a name="adf-pipeline"></a>Определение и создание конвейера hello</span><span class="sxs-lookup"><span data-stu-id="67379-213"><a name="adf-pipeline"></a>Define and create hello pipeline</span></span>
<span data-ttu-id="67379-214">Укажите hello действиями, которые входят toohello конвейера и создать конвейер hello с помощью следующих процедур на основе сценария hello.</span><span class="sxs-lookup"><span data-stu-id="67379-214">Specify hello activities that belong toohello pipeline and create hello pipeline with hello following script-based procedures.</span></span> <span data-ttu-id="67379-215">Файл JSON, используется toodefine hello конвейера свойства.</span><span class="sxs-lookup"><span data-stu-id="67379-215">A JSON file is used toodefine hello pipeline properties.</span></span>

* <span data-ttu-id="67379-216">Hello сценарий предполагает, что hello **имя конвейера** — *AMLDSProcessPipeline*.</span><span class="sxs-lookup"><span data-stu-id="67379-216">hello script assumes that hello **pipeline name** is *AMLDSProcessPipeline*.</span></span>
* <span data-ttu-id="67379-217">Также Обратите внимание, что мы устанавливаем hello периодичности toobe конвейера hello выполнена на ежедневно основы и использование hello по умолчанию время выполнения для задания hello (12: 00 UTC).</span><span class="sxs-lookup"><span data-stu-id="67379-217">Also note that we set hello periodicity of hello pipeline toobe executed on daily basis and use hello default execution time for hello job (12 am UTC).</span></span>

> [!NOTE]
> <span data-ttu-id="67379-218">Hello следующие процедуры используйте toodefine Azure PowerShell и создать конвейер ADF hello.</span><span class="sxs-lookup"><span data-stu-id="67379-218">hello following procedures use Azure PowerShell toodefine and create hello ADF pipeline.</span></span> <span data-ttu-id="67379-219">Однако эту задачу также можно выполнить на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="67379-219">But this task can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="67379-220">Дополнительные сведения см. в разделе [Создание конвейера](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span><span class="sxs-lookup"><span data-stu-id="67379-220">For details, see [Create pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span></span>
>
>

<span data-ttu-id="67379-221">С помощью определения таблиц hello ранее приведено определение конвейера hello для hello ADF задается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="67379-221">Using hello table definitions provided previously, hello pipeline definition for hello ADF is specified as follows:</span></span>

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data tooSql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

<span data-ttu-id="67379-222">Скопировать это определение JSON конвейера hello в файл с именем *pipelinedef.json* файл и сохраните его tooa известно расположение (здесь предполагается, что toobe *C:\temp\pipelinedef.json*).</span><span class="sxs-lookup"><span data-stu-id="67379-222">Copy this JSON definition of hello pipeline into a file called *pipelinedef.json* file and save it tooa known location (here assumed toobe *C:\temp\pipelinedef.json*).</span></span> <span data-ttu-id="67379-223">Создайте конвейер hello в ADF с hello, выполнив командлет Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="67379-223">Create hello pipeline in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

<span data-ttu-id="67379-224">Убедитесь, что вы может конвейера hello на hello ADF в hello классическом портале Azure отображаются следующим образом (при нажатии кнопки hello схемы)</span><span class="sxs-lookup"><span data-stu-id="67379-224">Confirm that you can see hello pipeline on hello ADF in hello Azure Classic Portal show up as following (when you click hello diagram)</span></span>

![Конвейер ADF](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <span data-ttu-id="67379-226"><a name="adf-pipeline-start"></a>Запуск конвейера hello</span><span class="sxs-lookup"><span data-stu-id="67379-226"><a name="adf-pipeline-start"></a>Start hello Pipeline</span></span>
<span data-ttu-id="67379-227">конвейер Hello можно запустить с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="67379-227">hello pipeline can now be run using hello following command:</span></span>

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

<span data-ttu-id="67379-228">Hello *startdate* и *enddate* значения параметров необходимо заменить фактические даты hello, между которыми требуется hello конвейера toorun toobe.</span><span class="sxs-lookup"><span data-stu-id="67379-228">hello *startdate* and *enddate* parameter values need toobe replaced with hello actual dates between which you want hello pipeline toorun.</span></span>

<span data-ttu-id="67379-229">После выполняется конвейера hello, можно будет toosee hello данные отображались в контейнере hello, выбранных для большого двоичного объекта hello, один файл в день.</span><span class="sxs-lookup"><span data-stu-id="67379-229">Once hello pipeline executes, you should be able toosee hello data show up in hello container selected for hello blob, one file per day.</span></span>

<span data-ttu-id="67379-230">Обратите внимание, что мы не использовались hello функциональные возможности, предоставляемые данные toopipe ADF, постепенно.</span><span class="sxs-lookup"><span data-stu-id="67379-230">Note that we have not leveraged hello functionality provided by ADF toopipe data incrementally.</span></span> <span data-ttu-id="67379-231">Дополнительные сведения о toodo это и другие возможности, предоставляемые ADF, в статье hello [документации ADF](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="67379-231">For more information on how toodo this and other capabilities provided by ADF, see hello [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span></span>
