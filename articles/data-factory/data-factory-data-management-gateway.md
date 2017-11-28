---
title: "Шлюз управления для фабрики данных aaaData | Документы Microsoft"
description: "Настройка шлюза данных toomove данных между локальными и hello облака. Используйте шлюз управления данными в toomove фабрики данных Azure данные."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a><span data-ttu-id="7f30a-104">Шлюз управления данными</span><span class="sxs-lookup"><span data-stu-id="7f30a-104">Data Management Gateway</span></span>
<span data-ttu-id="7f30a-105">Шлюз управления данными Hello установлен агент клиента, который необходимо установить в локальной среде toocopy данных между облачных и локальных хранилищ данных.</span><span class="sxs-lookup"><span data-stu-id="7f30a-105">hello Data management gateway is a client agent that you must install in your on-premises environment toocopy data between cloud and on-premises data stores.</span></span> <span data-ttu-id="7f30a-106">Hello локальных данных хранилища, поддерживаемый фабрики данных, перечислены в hello [поддерживаемых источников данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) раздела.</span><span class="sxs-lookup"><span data-stu-id="7f30a-106">hello on-premises data stores supported by Data Factory are listed in hello [Supported data sources](data-factory-data-movement-activities.md#supported-data-stores-and-formats) section.</span></span>

<span data-ttu-id="7f30a-107">В этой статье дополняет hello пошагового руководства hello [перемещение данных между локальными и облачными хранилищами данных](data-factory-move-data-between-onprem-and-cloud.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="7f30a-107">This article complements hello walkthrough in hello [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="7f30a-108">В примере hello Создание конвейера, который использует данные toomove шлюза hello tooan базы данных SQL Server в локальной среде BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="7f30a-108">In hello walkthrough, you create a pipeline that uses hello gateway toomove data from an on-premises SQL Server database tooan Azure blob.</span></span> <span data-ttu-id="7f30a-109">В этой статье подробно подробные hello шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="7f30a-109">This article provides detailed in-depth information about hello data management gateway.</span></span> 

<span data-ttu-id="7f30a-110">Шлюз управления данными можно масштабировать, объединяя несколько локальных компьютеров с hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="7f30a-110">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="7f30a-111">Чтобы увеличить масштаб, увеличьте число заданий перемещения данных, которые могут выполняться одновременно на узле.</span><span class="sxs-lookup"><span data-stu-id="7f30a-111">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="7f30a-112">Эта функция также доступна для логического шлюза с одним узлом.</span><span class="sxs-lookup"><span data-stu-id="7f30a-112">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="7f30a-113">Дополнительные сведения см. в статье [Шлюз управления данными: высокий уровень доступности и масштабируемость (предварительная версия)](data-factory-data-management-gateway-high-availability-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="7f30a-113">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>

> [!NOTE]
> <span data-ttu-id="7f30a-114">В настоящее время шлюз поддерживает только действие копирования hello и действие хранимой процедуры в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="7f30a-114">Currently, gateway supports only hello copy activity and stored procedure activity in Data Factory.</span></span> <span data-ttu-id="7f30a-115">Нет шлюза hello возможных toouse из источников данных в локальной tooaccess пользовательского действия.</span><span class="sxs-lookup"><span data-stu-id="7f30a-115">It is not possible toouse hello gateway from a custom activity tooaccess on-premises data sources.</span></span>      

## <a name="overview"></a><span data-ttu-id="7f30a-116">Обзор</span><span class="sxs-lookup"><span data-stu-id="7f30a-116">Overview</span></span>
### <a name="capabilities-of-data-management-gateway"></a><span data-ttu-id="7f30a-117">Возможности шлюза управления данными</span><span class="sxs-lookup"><span data-stu-id="7f30a-117">Capabilities of data management gateway</span></span>
<span data-ttu-id="7f30a-118">Шлюз управления данными предоставляет hello следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="7f30a-118">Data management gateway provides hello following capabilities:</span></span>

* <span data-ttu-id="7f30a-119">Модели локальные источники данных и облачных источников данных в пределах hello же фабрику данных и перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="7f30a-119">Model on-premises data sources and cloud data sources within hello same data factory and move data.</span></span>
* <span data-ttu-id="7f30a-120">Иметь унифицированного для мониторинга и управления с видимостью в состояние шлюза со страницы приветствия фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="7f30a-120">Have a single pane of glass for monitoring and management with visibility into gateway status from hello Data Factory page.</span></span>
* <span data-ttu-id="7f30a-121">Безопасно управлять доступа tooon локальные источники данных.</span><span class="sxs-lookup"><span data-stu-id="7f30a-121">Manage access tooon-premises data sources securely.</span></span>
  * <span data-ttu-id="7f30a-122">Изменения не требуется toocorporate брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="7f30a-122">No changes required toocorporate firewall.</span></span> <span data-ttu-id="7f30a-123">Исходящие подключения по протоколу HTTP tooopen только принимаются шлюзом Интернета.</span><span class="sxs-lookup"><span data-stu-id="7f30a-123">Gateway only makes outbound HTTP-based connections tooopen internet.</span></span>
  * <span data-ttu-id="7f30a-124">Учетные данные для ваших локальных хранилищ данных можно шифровать с помощью личного сертификата.</span><span class="sxs-lookup"><span data-stu-id="7f30a-124">Encrypt credentials for your on-premises data stores with your certificate.</span></span>
* <span data-ttu-id="7f30a-125">Эффективно перемещать данные: данные передаются в параллельных, надежных toointermittent проблемы с сетевым логику автоматического повтора.</span><span class="sxs-lookup"><span data-stu-id="7f30a-125">Move data efficiently – data is transferred in parallel, resilient toointermittent network issues with auto retry logic.</span></span>

### <a name="command-flow-and-data-flow"></a><span data-ttu-id="7f30a-126">Поток команд и поток данных</span><span class="sxs-lookup"><span data-stu-id="7f30a-126">Command flow and data flow</span></span>
<span data-ttu-id="7f30a-127">При использовании копирование действия toocopy данных между локальными и облачными hello использует tootransfer шлюз данных из источника toocloud локальных данных и наоборот.</span><span class="sxs-lookup"><span data-stu-id="7f30a-127">When you use a copy activity toocopy data between on-premises and cloud, hello activity uses a gateway tootransfer data from on-premises data source toocloud and vice versa.</span></span>

<span data-ttu-id="7f30a-128">Вот hello общий поток данных для и Сводка действий для копирования данных шлюза: ![потока данных с помощью шлюза](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span><span class="sxs-lookup"><span data-stu-id="7f30a-128">Here is hello high-level data flow for and summary of steps for copy with data gateway: ![Data flow using gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span></span>

1. <span data-ttu-id="7f30a-129">Данных разработчик создает шлюз для фабрики данных Azure, используя либо hello [портал Azure](https://portal.azure.com) или [командлета PowerShell](https://msdn.microsoft.com/library/dn820234.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f30a-129">Data developer creates a gateway for an Azure Data Factory using either hello [Azure portal](https://portal.azure.com) or [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).</span></span>
2. <span data-ttu-id="7f30a-130">Данных разработчик создает связанной службы локального хранилища данных, указав hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="7f30a-130">Data developer creates a linked service for an on-premises data store by specifying hello gateway.</span></span> <span data-ttu-id="7f30a-131">При настройке hello связанной службы, разработчик данных использует задать учетные данные приложения hello toospecify-типы проверки подлинности и учетные данные.</span><span class="sxs-lookup"><span data-stu-id="7f30a-131">As part of setting up hello linked service, data developer uses hello Setting Credentials application toospecify authentication types and credentials.</span></span>  <span data-ttu-id="7f30a-132">Параметр Hello учетные данные, которые диалоговое окно приложения взаимодействует с данными hello хранить tootest соединения и hello шлюза toosave учетные данные.</span><span class="sxs-lookup"><span data-stu-id="7f30a-132">hello Setting Credentials application dialog communicates with hello data store tootest connection and hello gateway toosave credentials.</span></span>
3. <span data-ttu-id="7f30a-133">Шлюз шифрует учетные данные hello сертификатом hello, связанной со шлюзом hello (указанного в данных разработчика), перед сохранением hello учетные данные в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-133">Gateway encrypts hello credentials with hello certificate associated with hello gateway (supplied by data developer), before saving hello credentials in hello cloud.</span></span>
4. <span data-ttu-id="7f30a-134">Служба фабрики данных взаимодействует с hello шлюз для планирования и управление заданиями через канал управления, который использует очередь общего Azure service bus.</span><span class="sxs-lookup"><span data-stu-id="7f30a-134">Data Factory service communicates with hello gateway for scheduling & management of jobs via a control channel that uses a shared Azure service bus queue.</span></span> <span data-ttu-id="7f30a-135">Когда задание копирования действие должно toobe запущена и фабрики данных очереди hello запроса, а также учетные данные.</span><span class="sxs-lookup"><span data-stu-id="7f30a-135">When a copy activity job needs toobe kicked off, Data Factory queues hello request along with credential information.</span></span> <span data-ttu-id="7f30a-136">Шлюз запускает задание hello после опроса очереди hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-136">Gateway kicks off hello job after polling hello queue.</span></span>
5. <span data-ttu-id="7f30a-137">шлюз Hello расшифровывает hello учетные данные с hello же сертификата, а затем подключается toohello к локальному хранилищу данных с типом надлежащую проверку подлинности и учетные данные.</span><span class="sxs-lookup"><span data-stu-id="7f30a-137">hello gateway decrypts hello credentials with hello same certificate and then connects toohello on-premises data store with proper authentication type and credentials.</span></span>
6. <span data-ttu-id="7f30a-138">шлюз Hello копирует данные из локального хранилища tooa облачного хранилища, или наоборот в зависимости от того, как hello действие копирования настроено в конвейере данных hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-138">hello gateway copies data from an on-premises store tooa cloud storage, or vice versa depending on how hello Copy Activity is configured in hello data pipeline.</span></span> <span data-ttu-id="7f30a-139">Для выполнения этого шага шлюз hello непосредственно взаимодействует со службами облачного хранилища таких как хранилище больших двоичных объектов Azure по безопасному каналу (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="7f30a-139">For this step, hello gateway directly communicates with cloud-based storage services such as Azure Blob Storage over a secure (HTTPS) channel.</span></span>

### <a name="considerations-for-using-gateway"></a><span data-ttu-id="7f30a-140">Рекомендации по использованию шлюза</span><span class="sxs-lookup"><span data-stu-id="7f30a-140">Considerations for using gateway</span></span>
* <span data-ttu-id="7f30a-141">Для нескольких локальных источников данных можно использовать один шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="7f30a-141">A single instance of data management gateway can be used for multiple on-premises data sources.</span></span> <span data-ttu-id="7f30a-142">Тем не менее **один экземпляр шлюза — одна фабрика данных Azure равноценных tooonly** и не может совместно использоваться другой фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="7f30a-142">However, **a single gateway instance is tied tooonly one Azure data factory** and cannot be shared with another data factory.</span></span>
* <span data-ttu-id="7f30a-143">На компьютере может быть установлен **только один экземпляр шлюза управления данными**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-143">You can have **only one instance of data management gateway** installed on a single machine.</span></span> <span data-ttu-id="7f30a-144">Предположим, что у вас есть два фабрик данных, требующих tooaccess локальных источников данных, необходимо tooinstall шлюзов на двух локальных компьютерах.</span><span class="sxs-lookup"><span data-stu-id="7f30a-144">Suppose, you have two data factories that need tooaccess on-premises data sources, you need tooinstall gateways on two on-premises computers.</span></span> <span data-ttu-id="7f30a-145">Другими словами шлюз является равноценных tooa конкретную фабрику данных</span><span class="sxs-lookup"><span data-stu-id="7f30a-145">In other words, a gateway is tied tooa specific data factory</span></span>
* <span data-ttu-id="7f30a-146">Hello **шлюз не требуется toobe на компьютер же, как источник данных hello hello**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-146">hello **gateway does not need toobe on hello same machine as hello data source**.</span></span> <span data-ttu-id="7f30a-147">Однако наличие источника данных toohello ближе шлюз уменьшает hello время для источника данных toohello tooconnect шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-147">However, having gateway closer toohello data source reduces hello time for hello gateway tooconnect toohello data source.</span></span> <span data-ttu-id="7f30a-148">Рекомендуется устанавливать hello шлюз на компьютере, который отличается от одного источника данных локальных узлов hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-148">We recommend that you install hello gateway on a machine that is different from hello one that hosts on-premises data source.</span></span> <span data-ttu-id="7f30a-149">Когда hello шлюз и источник данных находятся на разных компьютерах, hello шлюза не конкурируют за ресурсы с источником данных.</span><span class="sxs-lookup"><span data-stu-id="7f30a-149">When hello gateway and data source are on different machines, hello gateway does not compete for resources with data source.</span></span>
* <span data-ttu-id="7f30a-150">Может иметь **несколько шлюзов на разных компьютерах, соединение toohello одного источника данных в локальной**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-150">You can have **multiple gateways on different machines connecting toohello same on-premises data source**.</span></span> <span data-ttu-id="7f30a-151">Например имеется два шлюза, обслуживающий фабрики данных, но hello же локальному источнику данных, зарегистрированные с фабриками данных обоих hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-151">For example, you may have two gateways serving two data factories but hello same on-premises data source is registered with both hello data factories.</span></span>
* <span data-ttu-id="7f30a-152">Если вы уже установили шлюз на компьютер, который обслуживает сценарий **Power BI**, установите **отдельный шлюз для фабрики данных Azure** на другой компьютер.</span><span class="sxs-lookup"><span data-stu-id="7f30a-152">If you already have a gateway installed on your computer serving a **Power BI** scenario, install a **separate gateway for Azure Data Factory** on another machine.</span></span>
* <span data-ttu-id="7f30a-153">Шлюз необходимо использовать, даже если используется **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-153">Gateway must be used even when you use **ExpressRoute**.</span></span>
* <span data-ttu-id="7f30a-154">Источник данных следует считать локальным (то есть защищенным брандмауэром), даже если используется **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-154">Treat your data source as an on-premises data source (that is behind a firewall) even when you use **ExpressRoute**.</span></span> <span data-ttu-id="7f30a-155">Используйте hello шлюза tooestablish подключения между службой hello и hello источника данных.</span><span class="sxs-lookup"><span data-stu-id="7f30a-155">Use hello gateway tooestablish connectivity between hello service and hello data source.</span></span>
* <span data-ttu-id="7f30a-156">Вы должны **использовать шлюз hello** даже если hello, то хранилище данных в облаке hello на **ВМ IaaS Azure**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-156">You must **use hello gateway** even if hello data store is in hello cloud on an **Azure IaaS VM**.</span></span>

## <a name="installation"></a><span data-ttu-id="7f30a-157">Установка</span><span class="sxs-lookup"><span data-stu-id="7f30a-157">Installation</span></span>
### <a name="prerequisites"></a><span data-ttu-id="7f30a-158">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7f30a-158">Prerequisites</span></span>
* <span data-ttu-id="7f30a-159">Hello поддерживается **операционной системы** версии, Windows 7, Windows 8 и 8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="7f30a-159">hello supported **Operating System** versions are Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span></span> <span data-ttu-id="7f30a-160">Установка hello шлюз управления данными на контроллере домена в настоящее время не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="7f30a-160">Installation of hello data management gateway on a domain controller is currently not supported.</span></span>
* <span data-ttu-id="7f30a-161">Требуется .NET Framework 4.5.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7f30a-161">.NET Framework 4.5.1 or above is required.</span></span> <span data-ttu-id="7f30a-162">При установке шлюза на компьютере под управлением Windows 7 установите .NET Framework 4.5 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7f30a-162">If you are installing gateway on a Windows 7 machine, install .NET Framework 4.5 or later.</span></span> <span data-ttu-id="7f30a-163">Дополнительные сведения см. в разделе [Требования к системе для .NET Framework](https://msdn.microsoft.com/library/8z6watww.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f30a-163">See [.NET Framework System Requirements](https://msdn.microsoft.com/library/8z6watww.aspx) for details.</span></span>
* <span data-ttu-id="7f30a-164">Рекомендуется Hello **конфигурации** для hello компьютер шлюза имеет по крайней мере 2 ГГц, 4 ядра, 8 ГБ ОЗУ и диск 80 ГБ.</span><span class="sxs-lookup"><span data-stu-id="7f30a-164">hello recommended **configuration** for hello gateway machine is at least 2 GHz, 4 cores, 8-GB RAM, and 80-GB disk.</span></span>
* <span data-ttu-id="7f30a-165">Если хост-компьютере hello перейдет в спящий режим, hello шлюза не отвечает toodata запросов.</span><span class="sxs-lookup"><span data-stu-id="7f30a-165">If hello host machine hibernates, hello gateway does not respond toodata requests.</span></span> <span data-ttu-id="7f30a-166">Таким образом, настроить соответствующий **управления питанием** на компьютере hello перед установкой шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-166">Therefore, configure an appropriate **power plan** on hello computer before installing hello gateway.</span></span> <span data-ttu-id="7f30a-167">Если машина hello настроенных toohibernate, установка шлюза hello предлагает сообщение.</span><span class="sxs-lookup"><span data-stu-id="7f30a-167">If hello machine is configured toohibernate, hello gateway installation prompts a message.</span></span>
* <span data-ttu-id="7f30a-168">Необходимо иметь права администратора на машине tooinstall hello и настроить шлюз управления данными hello успешно.</span><span class="sxs-lookup"><span data-stu-id="7f30a-168">You must be an administrator on hello machine tooinstall and configure hello data management gateway successfully.</span></span> <span data-ttu-id="7f30a-169">Можно добавить дополнительных пользователей toohello **шлюз управления данными пользователей** локальной группе Windows.</span><span class="sxs-lookup"><span data-stu-id="7f30a-169">You can add additional users toohello **data management gateway Users** local Windows group.</span></span> <span data-ttu-id="7f30a-170">Hello члены этой группы являются hello может toouse **диспетчера конфигурации шлюза управления данными** средство tooconfigure hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="7f30a-170">hello members of this group are able toouse hello **Data Management Gateway Configuration Manager** tool tooconfigure hello gateway.</span></span>

<span data-ttu-id="7f30a-171">Копировать запуске действия происходят на тактовую частоту, hello использование ресурсов (ЦП, памяти) на компьютере hello также учитывает hello же шаблон с максимальной нагрузки и временем простоя.</span><span class="sxs-lookup"><span data-stu-id="7f30a-171">As copy activity runs happen on a specific frequency, hello resource usage (CPU, memory) on hello machine also follows hello same pattern with peak and idle times.</span></span> <span data-ttu-id="7f30a-172">Использование ресурсов также сильно зависит hello объем данных, перемещаемых.</span><span class="sxs-lookup"><span data-stu-id="7f30a-172">Resource utilization also depends heavily on hello amount of data being moved.</span></span> <span data-ttu-id="7f30a-173">Когда выполняется несколько заданий копирования, в пиковые периоды уровень использования ресурсов системы повышается.</span><span class="sxs-lookup"><span data-stu-id="7f30a-173">When multiple copy jobs are in progress, you see resource usage go up during peak times.</span></span>

### <a name="installation-options"></a><span data-ttu-id="7f30a-174">Параметры установки</span><span class="sxs-lookup"><span data-stu-id="7f30a-174">Installation options</span></span>
<span data-ttu-id="7f30a-175">Можно установить шлюз управления данными в hello следующих способов:</span><span class="sxs-lookup"><span data-stu-id="7f30a-175">Data management gateway can be installed in hello following ways:</span></span>

* <span data-ttu-id="7f30a-176">Загрузить пакет установки MSI из hello [центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="7f30a-176">By downloading an MSI setup package from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>  <span data-ttu-id="7f30a-177">Hello MSI-ФАЙЛ также может быть используется tooupgrade существующие данных управления шлюза toohello последнюю версию, обо всех параметрах, сохраняются.</span><span class="sxs-lookup"><span data-stu-id="7f30a-177">hello MSI can also be used tooupgrade existing data management gateway toohello latest version, with all settings preserved.</span></span>
* <span data-ttu-id="7f30a-178">Щелкнуть ссылку **Скачивание и установка шлюза данных** в разделе "Установка вручную" или ссылку **Установка непосредственно на этот компьютер** в разделе "Экспресс-установка".</span><span class="sxs-lookup"><span data-stu-id="7f30a-178">By clicking **Download and install data gateway** link under MANUAL SETUP or **Install directly on this computer** under EXPRESS SETUP.</span></span> <span data-ttu-id="7f30a-179">В разделе [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) приведены пошаговые инструкции по экспресс-установке.</span><span class="sxs-lookup"><span data-stu-id="7f30a-179">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on using express setup.</span></span> <span data-ttu-id="7f30a-180">выполнить ручное действие Hello принимает toohello центра загрузки.</span><span class="sxs-lookup"><span data-stu-id="7f30a-180">hello manual step takes you toohello download center.</span></span>  <span data-ttu-id="7f30a-181">в следующем разделе hello являются Hello инструкции по загрузке и установке шлюза hello из центра загрузки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="7f30a-181">hello instructions for downloading and installing hello gateway from download center are in hello next section.</span></span>

### <a name="installation-best-practices"></a><span data-ttu-id="7f30a-182">Рекомендации по установке</span><span class="sxs-lookup"><span data-stu-id="7f30a-182">Installation best practices:</span></span>
1. <span data-ttu-id="7f30a-183">Настройте схему управления питанием на хост-компьютере hello hello шлюза, чтобы hello компьютера не удается.</span><span class="sxs-lookup"><span data-stu-id="7f30a-183">Configure power plan on hello host machine for hello gateway so that hello machine does not hibernate.</span></span> <span data-ttu-id="7f30a-184">Если хост-компьютере hello перейдет в спящий режим, hello шлюза не отвечает toodata запросов.</span><span class="sxs-lookup"><span data-stu-id="7f30a-184">If hello host machine hibernates, hello gateway does not respond toodata requests.</span></span>
2. <span data-ttu-id="7f30a-185">Создайте резервную копию сертификата hello, связанной со шлюзом hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-185">Back up hello certificate associated with hello gateway.</span></span>

### <a name="install-hello-gateway-from-download-center"></a><span data-ttu-id="7f30a-186">Установить шлюз hello из центра загрузки Майкрософт</span><span class="sxs-lookup"><span data-stu-id="7f30a-186">Install hello gateway from download center</span></span>
1. <span data-ttu-id="7f30a-187">Перейдите в слишком[страницы загрузки шлюз управления данными Майкрософт](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="7f30a-187">Navigate too[Microsoft Data Management Gateway download page](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>
2. <span data-ttu-id="7f30a-188">Нажмите кнопку **загрузки**, выберите hello соответствующую версию (**32-разрядных** vs. **64-разрядную**) и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-188">Click **Download**, select hello appropriate version (**32-bit** vs. **64-bit**), and click **Next**.</span></span>
3. <span data-ttu-id="7f30a-189">Запустите hello **MSI** напрямую или сохранить его tooyour жесткий диск и запустите.</span><span class="sxs-lookup"><span data-stu-id="7f30a-189">Run hello **MSI** directly or save it tooyour hard disk and run.</span></span>
4. <span data-ttu-id="7f30a-190">На hello **приветствия** выберите **язык** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-190">On hello **Welcome** page, select a **language** click **Next**.</span></span>
5. <span data-ttu-id="7f30a-191">**Принять** hello лицензионное соглашение и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-191">**Accept** hello End-User License Agreement and click **Next**.</span></span>
6. <span data-ttu-id="7f30a-192">Выберите **папки** tooinstall hello шлюза и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-192">Select **folder** tooinstall hello gateway and click **Next**.</span></span>
7. <span data-ttu-id="7f30a-193">На hello **готовности tooinstall** щелкните **установить**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-193">On hello **Ready tooinstall** page, click **Install**.</span></span>
8. <span data-ttu-id="7f30a-194">Нажмите кнопку **Готово** toocomplete установки.</span><span class="sxs-lookup"><span data-stu-id="7f30a-194">Click **Finish** toocomplete installation.</span></span>
9. <span data-ttu-id="7f30a-195">Получение ключа hello из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7f30a-195">Get hello key from hello Azure portal.</span></span> <span data-ttu-id="7f30a-196">Hello следующего раздела приведены пошаговые инструкции в разделе.</span><span class="sxs-lookup"><span data-stu-id="7f30a-196">See hello next section for step-by-step instructions.</span></span>
10. <span data-ttu-id="7f30a-197">На hello **регистрации шлюза** страница **диспетчера конфигурации шлюза управления данными** выполняется на компьютере, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7f30a-197">On hello **Register gateway** page of **Data Management Gateway Configuration Manager** running on your machine, do hello following steps:</span></span>
    1. <span data-ttu-id="7f30a-198">Вставьте ключ hello в тексте hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-198">Paste hello key in hello text.</span></span>
    2. <span data-ttu-id="7f30a-199">При необходимости щелкните **Показать ключ шлюза** ключа текста hello toosee.</span><span class="sxs-lookup"><span data-stu-id="7f30a-199">Optionally, click **Show gateway key** toosee hello key text.</span></span>
    3. <span data-ttu-id="7f30a-200">Щелкните **Зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-200">Click **Register**.</span></span>

### <a name="register-gateway-using-key"></a><span data-ttu-id="7f30a-201">Регистрация шлюза с помощью ключа</span><span class="sxs-lookup"><span data-stu-id="7f30a-201">Register gateway using key</span></span>
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a><span data-ttu-id="7f30a-202">Если вы еще не создали логических шлюза hello портала</span><span class="sxs-lookup"><span data-stu-id="7f30a-202">If you haven't already created a logical gateway in hello portal</span></span>
<span data-ttu-id="7f30a-203">toocreate шлюз в ключе hello hello портал и get из hello **Настройка** страницы, повторите шаги с пошаговым руководством hello [перемещение данных между локальными и облачными](data-factory-move-data-between-onprem-and-cloud.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="7f30a-203">toocreate a gateway in hello portal and get hello key from hello **Configure** page, Follow steps from walkthrough in hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a><span data-ttu-id="7f30a-204">Если уже создали hello логических шлюза на портале hello</span><span class="sxs-lookup"><span data-stu-id="7f30a-204">If you have already created hello logical gateway in hello portal</span></span>
1. <span data-ttu-id="7f30a-205">На портале Azure перейдите toohello **фабрики данных** и нажмите кнопку **связанные службы** плитки.</span><span class="sxs-lookup"><span data-stu-id="7f30a-205">In Azure portal, navigate toohello **Data Factory** page, and click **Linked Services** tile.</span></span>

    ![Страница "Фабрика данных"](media/data-factory-data-management-gateway/data-factory-blade.png)
2. <span data-ttu-id="7f30a-207">В hello **связанные службы** страницы выберите hello логических **шлюза** вы создали на портале hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-207">In hello **Linked Services** page, select hello logical **gateway** you created in hello portal.</span></span>

    ![Логический шлюз](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. <span data-ttu-id="7f30a-209">В hello **шлюз данных** щелкните **загрузить и установить шлюз данных**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-209">In hello **Data Gateway** page, click **Download and install data gateway**.</span></span>

    ![Ссылка на портале hello для загрузки](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. <span data-ttu-id="7f30a-211">В hello **Настройка** щелкните **повторно создайте ключ**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-211">In hello **Configure** page, click **Recreate key**.</span></span> <span data-ttu-id="7f30a-212">Нажмите кнопку Да в предупреждающее сообщение hello после их считывания внимательно.</span><span class="sxs-lookup"><span data-stu-id="7f30a-212">Click Yes on hello warning message after reading it carefully.</span></span>

    ![Повторное создание ключа](media/data-factory-data-management-gateway/recreate-key-button.png)
5. <span data-ttu-id="7f30a-214">Нажмите кнопку Далее ключ toohello копирования кнопки.</span><span class="sxs-lookup"><span data-stu-id="7f30a-214">Click Copy button next toohello key.</span></span> <span data-ttu-id="7f30a-215">ключ Hello — скопированный toohello буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="7f30a-215">hello key is copied toohello clipboard.</span></span>

    ![Копирование ключа](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a><span data-ttu-id="7f30a-217">Значки и уведомления в области уведомлений</span><span class="sxs-lookup"><span data-stu-id="7f30a-217">System tray icons/ notifications</span></span>
<span data-ttu-id="7f30a-218">Hello следующем рисунке показаны некоторые hello значки, отображаемые на панели задач.</span><span class="sxs-lookup"><span data-stu-id="7f30a-218">hello following image shows some of hello tray icons that you see.</span></span>

![значки на панели задач](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

<span data-ttu-id="7f30a-220">Если навести курсор на панели задач значок/уведомления hello системного сообщения будут отображаться сведения о состоянии операции шлюза или обновления hello во всплывающем окне приветствия.</span><span class="sxs-lookup"><span data-stu-id="7f30a-220">If you move cursor over hello system tray icon/notification message, you see details about hello state of hello gateway/update operation in a popup window.</span></span>

### <a name="ports-and-firewall"></a><span data-ttu-id="7f30a-221">Порты и брандмауэр</span><span class="sxs-lookup"><span data-stu-id="7f30a-221">Ports and firewall</span></span>
<span data-ttu-id="7f30a-222">Существует два брандмауэры должны tooconsider: **корпоративного брандмауэра** под управлением центра маршрутизатора hello организации hello и **брандмауэра Windows** настроен как управляющая программа на локальном компьютере hello, где hello шлюз установлен.</span><span class="sxs-lookup"><span data-stu-id="7f30a-222">There are two firewalls you need tooconsider: **corporate firewall** running on hello central router of hello organization, and **Windows firewall** configured as a daemon on hello local machine where hello gateway is installed.</span></span>  

![брандмауэры](./media/data-factory-data-management-gateway/firewalls2.png)

<span data-ttu-id="7f30a-224">На уровне корпоративный брандмауэр, необходимо настроить следующие hello домены и исходящие порты:</span><span class="sxs-lookup"><span data-stu-id="7f30a-224">At corporate firewall level, you need configure hello following domains and outbound ports:</span></span>

| <span data-ttu-id="7f30a-225">Имена доменов</span><span class="sxs-lookup"><span data-stu-id="7f30a-225">Domain names</span></span> | <span data-ttu-id="7f30a-226">порты;</span><span class="sxs-lookup"><span data-stu-id="7f30a-226">Ports</span></span> | <span data-ttu-id="7f30a-227">Описание</span><span class="sxs-lookup"><span data-stu-id="7f30a-227">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7f30a-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="7f30a-228">*.servicebus.windows.net</span></span> |<span data-ttu-id="7f30a-229">443, 80</span><span class="sxs-lookup"><span data-stu-id="7f30a-229">443, 80</span></span> |<span data-ttu-id="7f30a-230">Используется для связи с серверной частью службы перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="7f30a-230">Used for communication with Data Movement Service backend</span></span> |
| <span data-ttu-id="7f30a-231">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="7f30a-231">*.core.windows.net</span></span> |<span data-ttu-id="7f30a-232">443</span><span class="sxs-lookup"><span data-stu-id="7f30a-232">443</span></span> |<span data-ttu-id="7f30a-233">Используется для промежуточного копирования с помощью большого двоичного объекта Azure (если оно настроено).</span><span class="sxs-lookup"><span data-stu-id="7f30a-233">Used for Staged copy using Azure Blob (if configured)</span></span>|
| <span data-ttu-id="7f30a-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="7f30a-234">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="7f30a-235">443</span><span class="sxs-lookup"><span data-stu-id="7f30a-235">443</span></span> |<span data-ttu-id="7f30a-236">Используется для связи с серверной частью службы перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="7f30a-236">Used for communication with Data Movement Service backend</span></span> |


<span data-ttu-id="7f30a-237">Эти исходящие порты, как правило, включены на уровне брандмауэра Windows.</span><span class="sxs-lookup"><span data-stu-id="7f30a-237">At Windows firewall level, these outbound ports are normally enabled.</span></span> <span data-ttu-id="7f30a-238">Если нет, можно настроить домены hello и порты соответствующим образом на компьютере шлюза.</span><span class="sxs-lookup"><span data-stu-id="7f30a-238">If not, you can configure hello domains and ports accordingly on gateway machine.</span></span>

> [!NOTE]
> 1. <span data-ttu-id="7f30a-239">В зависимости от источника или приемники, возможно, toowhitelist дополнительные домены и исходящие порты в брандмауэре организации или Windows.</span><span class="sxs-lookup"><span data-stu-id="7f30a-239">Based on your source/ sinks, you may have toowhitelist additional domains and outbound ports in your corporate/Windows firewall.</span></span>
> 2. <span data-ttu-id="7f30a-240">Для некоторых баз данных в облаке (например: [базы данных SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Озера данных Azure](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), т. д.), может потребоваться toowhitelist IP-адрес компьютера шлюза на их конфигурации брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="7f30a-240">For some Cloud Databases (For example: [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), you may need toowhitelist IP address of Gateway machine on their firewall configuration.</span></span>
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a><span data-ttu-id="7f30a-241">Копирование данных из хранилища данных приемник tooa источника данных хранилища</span><span class="sxs-lookup"><span data-stu-id="7f30a-241">Copy data from a source data store tooa sink data store</span></span>
<span data-ttu-id="7f30a-242">Убедитесь, что правильно включать hello правила брандмауэра на hello корпоративный брандмауэр, брандмауэр Windows на компьютере шлюза hello и самого хранилища данных hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-242">Ensure that hello firewall rules are enabled properly on hello corporate firewall, Windows firewall on hello gateway machine, and hello data store itself.</span></span> <span data-ttu-id="7f30a-243">Включение этих правил позволяет hello шлюза tooconnect tooboth источника и приемника успешно.</span><span class="sxs-lookup"><span data-stu-id="7f30a-243">Enabling these rules allows hello gateway tooconnect tooboth source and sink successfully.</span></span> <span data-ttu-id="7f30a-244">Включите правила для каждого хранилища данных, которая участвует в операции копирования hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-244">Enable rules for each data store that is involved in hello copy operation.</span></span>

<span data-ttu-id="7f30a-245">Например, toocopy из **приемник локальной tooan хранилище данных базы данных SQL Azure или приемника хранилища данных SQL Azure**, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7f30a-245">For example, toocopy from **an on-premises data store tooan Azure SQL Database sink or an Azure SQL Data Warehouse sink**, do hello following steps:</span></span>

* <span data-ttu-id="7f30a-246">Разрешите исходящий трафик **TCP** через порт **1433** для брандмауэра Windows и корпоративного брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="7f30a-246">Allow outbound **TCP** communication on port **1433** for both Windows firewall and corporate firewall.</span></span>
* <span data-ttu-id="7f30a-247">Настройте параметры брандмауэра hello Azure SQL tooadd hello IP-адрес сервера hello машины шлюза toohello список разрешенных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="7f30a-247">Configure hello firewall settings of Azure SQL server tooadd hello IP address of hello gateway machine toohello list of allowed IP addresses.</span></span>

> [!NOTE]
> <span data-ttu-id="7f30a-248">Если брандмауэр блокирует исходящий порт 1433, то шлюз не сможет напрямую получить доступ к SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7f30a-248">If your firewall does not allow outbound port 1433, Gateway can't access Azure SQL directly.</span></span> <span data-ttu-id="7f30a-249">В этом случае можно использовать [промежуточное копирования](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL базы данных SQL Azure и хранилища данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7f30a-249">In this case, you may use [Staged Copy](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL Azure Database/ SQL Azure DW.</span></span> <span data-ttu-id="7f30a-250">В этом сценарии вы только потребуется HTTPS (порт 443) для перемещения данных hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-250">In this scenario, you would only require HTTPS (port 443) for hello data movement.</span></span>
>
>


### <a name="proxy-server-considerations"></a><span data-ttu-id="7f30a-251">Рекомендации для прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="7f30a-251">Proxy server considerations</span></span>
<span data-ttu-id="7f30a-252">Если вашей организации сетевой среде используется прокси-сервер сервера tooaccess Здравствуйте Интернета, Настройка параметров шлюза toouse соответствующие прокси-сервера для данных управления.</span><span class="sxs-lookup"><span data-stu-id="7f30a-252">If your corporate network environment uses a proxy server tooaccess hello internet, configure data management gateway toouse appropriate proxy settings.</span></span> <span data-ttu-id="7f30a-253">Hello прокси-сервера можно задать во время этапа первоначальной регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-253">You can set hello proxy during hello initial registration phase.</span></span>

![Настройка прокси-сервера при регистрации](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

<span data-ttu-id="7f30a-255">Шлюз использует hello прокси-сервера tooconnect toohello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="7f30a-255">Gateway uses hello proxy server tooconnect toohello cloud service.</span></span> <span data-ttu-id="7f30a-256">Щелкните ссылку **Изменить** во время начальной настройки.</span><span class="sxs-lookup"><span data-stu-id="7f30a-256">Click **Change** link during initial setup.</span></span> <span data-ttu-id="7f30a-257">Вы видите hello **параметры прокси-сервера** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7f30a-257">You see hello **proxy setting** dialog.</span></span>

![Настройка прокси-сервера с помощью диспетчера конфигурации](media/data-factory-data-management-gateway/SetProxySettings.png)

<span data-ttu-id="7f30a-259">Доступны три варианта конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7f30a-259">There are three configuration options:</span></span>

* <span data-ttu-id="7f30a-260">**Не использовать прокси-сервер**: шлюза явным образом не используйте любой службы toocloud tooconnect прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="7f30a-260">**Do not use proxy**: Gateway does not explicitly use any proxy tooconnect toocloud services.</span></span>
* <span data-ttu-id="7f30a-261">**Использовать прокси-сервер системы**: шлюза использует hello прокси-сервер, то есть параметр настроены в diahost.exe.config и diawp.exe.config.  Если ни один прокси настроен в diahost.exe.config и diawp.exe.config, toocloud службы подключение шлюза напрямую без прохода через прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="7f30a-261">**Use system proxy**: Gateway uses hello proxy setting that is configured in diahost.exe.config and diawp.exe.config.  If no proxy is configured in diahost.exe.config and diawp.exe.config, gateway connects toocloud service directly without going through proxy.</span></span>
* <span data-ttu-id="7f30a-262">**Использовать пользовательский прокси-сервер**: Настройка toouse параметр hello HTTP прокси-сервера для шлюза, а не с помощью конфигураций в diahost.exe.config и diawp.exe.config.  Необходимо указать адрес и порт.</span><span class="sxs-lookup"><span data-stu-id="7f30a-262">**Use custom proxy**: Configure hello HTTP proxy setting toouse for gateway, instead of using configurations in diahost.exe.config and diawp.exe.config.  Address and Port are required.</span></span>  <span data-ttu-id="7f30a-263">Имя пользователя и пароль являются необязательными и указываются в зависимости от настроек аутентификации прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="7f30a-263">User Name and Password are optional depending on your proxy’s authentication setting.</span></span>  <span data-ttu-id="7f30a-264">Все параметры шифруются с hello сертификат учетных данных шлюза hello и хранятся локально на компьютере размещения шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-264">All settings are encrypted with hello credential certificate of hello gateway and stored locally on hello gateway host machine.</span></span>

<span data-ttu-id="7f30a-265">Шлюз управления данными Hello хост-служба автоматически перезапускается после сохранения параметров прокси-сервера обновлены hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-265">hello data management gateway Host Service restarts automatically after you save hello updated proxy settings.</span></span>

<span data-ttu-id="7f30a-266">После шлюз успешно зарегистрирован, если требуется tooview или обновить параметры прокси-сервера, используйте диспетчер конфигурации шлюза управления данными.</span><span class="sxs-lookup"><span data-stu-id="7f30a-266">After gateway has been successfully registered, if you want tooview or update proxy settings, use Data Management Gateway Configuration Manager.</span></span>

1. <span data-ttu-id="7f30a-267">Запустите **диспетчер конфигурации шлюза управления данными**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-267">Launch **Data Management Gateway Configuration Manager**.</span></span>
2. <span data-ttu-id="7f30a-268">Переключение toohello **параметры** вкладки.</span><span class="sxs-lookup"><span data-stu-id="7f30a-268">Switch toohello **Settings** tab.</span></span>
3. <span data-ttu-id="7f30a-269">Нажмите кнопку **изменений** ссылку в **прокси-сервера HTTP** hello раздел toolaunch **задать прокси-сервер HTTP** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7f30a-269">Click **Change** link in **HTTP Proxy** section toolaunch hello **Set HTTP Proxy** dialog.</span></span>  
4. <span data-ttu-id="7f30a-270">После нажатия кнопки hello **Далее** кнопку, отображается диалоговое окно с предупреждением, задать для параметра прокси hello toosave разрешение и перезапустите hello служба узла шлюза.</span><span class="sxs-lookup"><span data-stu-id="7f30a-270">After you click hello **Next** button, you see a warning dialog asking for your permission toosave hello proxy setting and restart hello Gateway Host Service.</span></span>

<span data-ttu-id="7f30a-271">При помощи диспетчера конфигурации можно просмотреть и обновить HTTP-прокси.</span><span class="sxs-lookup"><span data-stu-id="7f30a-271">You can view and update HTTP proxy by using Configuration Manager tool.</span></span>

![Настройка прокси-сервера с помощью диспетчера конфигурации](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> <span data-ttu-id="7f30a-273">Если настройка прокси-сервер с проверкой подлинности NTLM, служба узла шлюза выполняется под учетной записью домена hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-273">If you set up a proxy server with NTLM authentication, Gateway Host Service runs under hello domain account.</span></span> <span data-ttu-id="7f30a-274">Если изменить пароль hello hello учетной записи домена позже, помнить tooupdate параметры конфигурации для службы hello и перезапустите его соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="7f30a-274">If you change hello password for hello domain account later, remember tooupdate configuration settings for hello service and restart it accordingly.</span></span> <span data-ttu-id="7f30a-275">Из-за toothis требование мы рекомендуем использовать выделенной доменной учетной записи tooaccess hello прокси-сервер, не требует пароля hello tooupdate часто.</span><span class="sxs-lookup"><span data-stu-id="7f30a-275">Due toothis requirement, we suggest you use a dedicated domain account tooaccess hello proxy server that does not require you tooupdate hello password frequently.</span></span>
>
>

### <a name="configure-proxy-server-settings"></a><span data-ttu-id="7f30a-276">Настройка параметров прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="7f30a-276">Configure proxy server settings</span></span>
<span data-ttu-id="7f30a-277">При выборе **использовать прокси-сервер системы** Установка для прокси-сервера hello HTTP шлюз использует параметр в diahost.exe.config и diawp.exe.config hello прокси.  Если в diahost.exe.config и diawp.exe.config без прокси-сервера не указано, шлюз подключается toocloud службы непосредственно, без прохода через прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="7f30a-277">If you select **Use system proxy** setting for hello HTTP proxy, gateway uses hello proxy setting in diahost.exe.config and diawp.exe.config.  If no proxy is specified in diahost.exe.config and diawp.exe.config, gateway connects toocloud service directly without going through proxy.</span></span> <span data-ttu-id="7f30a-278">Hello следующей процедуре представлены инструкции по обновлению файла diahost.exe.config hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-278">hello following procedure provides instructions for updating hello diahost.exe.config file.</span></span>  

1. <span data-ttu-id="7f30a-279">В проводнике составляющих защищенной копии данных управления C:\Program Files\Microsoft Gateway\2.0\Shared\diahost.exe.config tooback hello исходного файла.</span><span class="sxs-lookup"><span data-stu-id="7f30a-279">In File Explorer, make a safe copy of C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config tooback up hello original file.</span></span>
2. <span data-ttu-id="7f30a-280">Запустите файл Notepad.exe с правами администратора и откройте текстовый файл с путем C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. Вы можете найти тег по умолчанию hello для system.net, как показано в hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="7f30a-280">Launch Notepad.exe running as administrator, and open text file “C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. You find hello default tag for system.net as shown in hello following code:</span></span>

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   <span data-ttu-id="7f30a-281">Затем можно добавить сведения о сервере прокси-сервера, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="7f30a-281">You can then add proxy server details as shown in hello following example:</span></span>

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   <span data-ttu-id="7f30a-282">Дополнительные свойства могут использоваться внутри hello тег toospecify hello требуется прокси-сервер как scriptLocation.</span><span class="sxs-lookup"><span data-stu-id="7f30a-282">Additional properties are allowed inside hello proxy tag toospecify hello required settings like scriptLocation.</span></span> <span data-ttu-id="7f30a-283">См. слишком[прокси-сервера (параметры сети) элемент](https://msdn.microsoft.com/library/sa91de1e.aspx) на синтаксис.</span><span class="sxs-lookup"><span data-stu-id="7f30a-283">Refer too[proxy Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on syntax.</span></span>

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. <span data-ttu-id="7f30a-284">Сохраните файл конфигурации hello в исходное расположение hello, а затем перезапустите службу узла шлюза управления данными, которая принимает изменения, внесенные hello hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-284">Save hello configuration file into hello original location, then restart hello Data Management Gateway Host service, which picks up hello changes.</span></span> <span data-ttu-id="7f30a-285">Служба hello toorestart: с помощью "службы" из панели управления hello или hello **диспетчера конфигурации шлюза управления данными** > щелкните hello **остановить службу** , а затем нажмите кнопку hello **Запуск службы**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-285">toorestart hello service: use services applet from hello control panel, or from hello **Data Management Gateway Configuration Manager** > click hello **Stop Service** button, then click hello **Start Service**.</span></span> <span data-ttu-id="7f30a-286">Если служба hello не запускается, вполне вероятно, что неправильный синтаксис тега XML был добавлен в файл конфигурации приложения hello, который был изменен.</span><span class="sxs-lookup"><span data-stu-id="7f30a-286">If hello service does not start, it is likely that an incorrect XML tag syntax has been added into hello application configuration file that was edited.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f30a-287">Не забудьте tooupdate **оба** diahost.exe.config и diawp.exe.config.</span><span class="sxs-lookup"><span data-stu-id="7f30a-287">Do not forget tooupdate **both** diahost.exe.config and diawp.exe.config.</span></span>  


<span data-ttu-id="7f30a-288">В дополнение к этому toothese точек, необходимо также toomake том, что Microsoft Azure в белом списке вашей компании.</span><span class="sxs-lookup"><span data-stu-id="7f30a-288">In addition toothese points, you also need toomake sure Microsoft Azure is in your company’s whitelist.</span></span> <span data-ttu-id="7f30a-289">Список Hello допустимым Microsoft IP-адресов Azure можно загрузить из hello [центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="7f30a-289">hello list of valid Microsoft Azure IP addresses can be downloaded from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a><span data-ttu-id="7f30a-290">Возможные признаки проблем, связанных с брандмауэром и прокси-сервером</span><span class="sxs-lookup"><span data-stu-id="7f30a-290">Possible symptoms for firewall and proxy server-related issues</span></span>
<span data-ttu-id="7f30a-291">При возникновении ошибки аналогичные toohello следующих областей, вполне вероятно, из-за конфигурации tooimproper hello брандмауэра или прокси-сервер, который блокирует шлюза из соединения tooauthenticate фабрики tooData сам.</span><span class="sxs-lookup"><span data-stu-id="7f30a-291">If you encounter errors similar toohello following ones, it is likely due tooimproper configuration of hello firewall or proxy server, which blocks gateway from connecting tooData Factory tooauthenticate itself.</span></span> <span data-ttu-id="7f30a-292">См. в разделе tooensure tooprevious, брандмауэра и прокси-сервера настроены правильно.</span><span class="sxs-lookup"><span data-stu-id="7f30a-292">Refer tooprevious section tooensure your firewall and proxy server are properly configured.</span></span>

1. <span data-ttu-id="7f30a-293">При попытке tooregister hello шлюза вы получаете hello следующая ошибка: «сбой tooregister hello шлюза ключ.</span><span class="sxs-lookup"><span data-stu-id="7f30a-293">When you try tooregister hello gateway, you receive hello following error: "Failed tooregister hello gateway key.</span></span> <span data-ttu-id="7f30a-294">Перед повторной попыткой ключ шлюза hello tooregister Подтверждение запуска шлюза управления данными находится в подключенном состоянии hello и hello служба узла шлюза управления данными.»</span><span class="sxs-lookup"><span data-stu-id="7f30a-294">Before trying tooregister hello gateway key again, confirm that hello data management gateway is in a connected state and hello Data Management Gateway Host Service is Started."</span></span>
2. <span data-ttu-id="7f30a-295">При открытии диспетчера конфигурации отображается состояние "Отключено" или "Подключение".</span><span class="sxs-lookup"><span data-stu-id="7f30a-295">When you open Configuration Manager, you see status as “Disconnected” or “Connecting.”</span></span> <span data-ttu-id="7f30a-296">При просмотре журналов событий Windows, в разделе «Просмотр событий» > «Журналы приложений и служб» > «Шлюз управления данными», вы видите сообщения об ошибках, таких как hello следующая ошибка:`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span><span class="sxs-lookup"><span data-stu-id="7f30a-296">When viewing Windows event logs, under “Event Viewer” > “Application and Services Logs” > “Data Management Gateway”, you see error messages such as hello following error: `Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span></span>

### <a name="open-port-8050-for-credential-encryption"></a><span data-ttu-id="7f30a-297">Открытие порта 8050 для шифрования учетных данных</span><span class="sxs-lookup"><span data-stu-id="7f30a-297">Open port 8050 for credential encryption</span></span>
<span data-ttu-id="7f30a-298">Hello **задать учетные данные** использует приложение hello входящий порт **8050** toorelay шлюза toohello учетные данные при настройке локальной связанной службы в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7f30a-298">hello **Setting Credentials** application uses hello inbound port **8050** toorelay credentials toohello gateway when you set up an on-premises linked service in hello Azure portal.</span></span> <span data-ttu-id="7f30a-299">Во время установки шлюза по умолчанию установка шлюза hello открывает его на компьютере шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-299">During gateway setup, by default, hello gateway installation opens it on hello gateway machine.</span></span>

<span data-ttu-id="7f30a-300">Если вы используете брандмауэр сторонних разработчиков, можно вручную открыть порт hello 8050.</span><span class="sxs-lookup"><span data-stu-id="7f30a-300">If you are using a third-party firewall, you can manually open hello port 8050.</span></span> <span data-ttu-id="7f30a-301">Если возникли проблемы брандмауэра во время установки шлюза, попробуйте использовать следующие команды tooinstall hello шлюза без настройки брандмауэра hello hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-301">If you run into firewall issue during gateway setup, you can try using hello following command tooinstall hello gateway without configuring hello firewall.</span></span>

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

<span data-ttu-id="7f30a-302">Если не tooopen hello порт 8050 на компьютере шлюза hello, использовать механизмы без использования hello **задать учетные данные** данные приложения tooconfigure хранить учетные данные.</span><span class="sxs-lookup"><span data-stu-id="7f30a-302">If you choose not tooopen hello port 8050 on hello gateway machine, use mechanisms other than using hello **Setting Credentials** application tooconfigure data store credentials.</span></span> <span data-ttu-id="7f30a-303">Например, можно использовать командлет PowerShell [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f30a-303">For example, you could use [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="7f30a-304">Дополнительные сведения о настройке учетных данных хранилища данных см. в разделе [Настройка учетных данных и безопасность](#set-credentials-and-securityy).</span><span class="sxs-lookup"><span data-stu-id="7f30a-304">See [Setting Credentials and Security](#set-credentials-and-securityy) section on how data store credentials can be set.</span></span>

## <a name="update"></a><span data-ttu-id="7f30a-305">Блокировка изменений</span><span class="sxs-lookup"><span data-stu-id="7f30a-305">Update</span></span>
<span data-ttu-id="7f30a-306">По умолчанию шлюз управления данными обновляется автоматически при доступна более новая версия шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-306">By default, data management gateway is automatically updated when a newer version of hello gateway is available.</span></span> <span data-ttu-id="7f30a-307">шлюз Hello не обновляется, пока все hello запланированных задач.</span><span class="sxs-lookup"><span data-stu-id="7f30a-307">hello gateway is not updated until all hello scheduled tasks are done.</span></span> <span data-ttu-id="7f30a-308">Последующие задачи не обрабатываются шлюзом hello до завершения операции обновления hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-308">No further tasks are processed by hello gateway until hello update operation is completed.</span></span> <span data-ttu-id="7f30a-309">В случае обновления hello шлюза выполняется откат toohello старую версию.</span><span class="sxs-lookup"><span data-stu-id="7f30a-309">If hello update fails, gateway is rolled back toohello old version.</span></span>

<span data-ttu-id="7f30a-310">Отображается время hello запланированные обновления в следующих местах hello:</span><span class="sxs-lookup"><span data-stu-id="7f30a-310">You see hello scheduled update time in hello following places:</span></span>

* <span data-ttu-id="7f30a-311">Страница свойств шлюза Hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7f30a-311">hello gateway properties page in hello Azure portal.</span></span>
* <span data-ttu-id="7f30a-312">Домашняя страница hello диспетчера конфигурации шлюза управления данными</span><span class="sxs-lookup"><span data-stu-id="7f30a-312">Home page of hello Data Management Gateway Configuration Manager</span></span>
* <span data-ttu-id="7f30a-313">сообщение в области уведомлений.</span><span class="sxs-lookup"><span data-stu-id="7f30a-313">System tray notification message.</span></span>

<span data-ttu-id="7f30a-314">Вкладка домашней Hello hello диспетчера конфигурации шлюза управления данными отображает расписание обновления hello и hello последнее время hello шлюза был установлен или обновлена.</span><span class="sxs-lookup"><span data-stu-id="7f30a-314">hello Home tab of hello Data Management Gateway Configuration Manager displays hello update schedule and hello last time hello gateway was installed/updated.</span></span>

![запланировать обновления](media/data-factory-data-management-gateway/UpdateSection.png)

<span data-ttu-id="7f30a-316">Можно сразу установить обновление hello или дождитесь toobe шлюза hello, автоматически обновляются во время запланированного hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-316">You can install hello update right away or wait for hello gateway toobe automatically updated at hello scheduled time.</span></span> <span data-ttu-id="7f30a-317">Например показано изображение hello уведомлений сообщение, показанное на hello диспетчера конфигурации шлюза вместе с hello кнопкой "Обновить", можно щелкнуть tooinstall его сразу же после hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-317">For example, hello following image shows you hello notification message shown in hello Gateway Configuration Manager along with hello Update button that you can click tooinstall it immediately.</span></span>

![Обновление диспетчера конфигураций DMG](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

<span data-ttu-id="7f30a-319">сообщение Hello уведомления hello панели задач будет выглядеть, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="7f30a-319">hello notification message in hello system tray would look as shown in hello following image:</span></span>

![Сообщение на панели задач](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

<span data-ttu-id="7f30a-321">Можно просмотреть состояние hello операции обновления (вручную или автоматически) hello панели задач.</span><span class="sxs-lookup"><span data-stu-id="7f30a-321">You see hello status of update operation (manual or automatic) in hello system tray.</span></span> <span data-ttu-id="7f30a-322">При запуске диспетчера конфигурации шлюза следующий раз появится сообщение на панель, шлюз hello уведомления hello была обновлена со ссылкой слишком[возможности новый раздел](data-factory-gateway-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="7f30a-322">When you launch Gateway Configuration Manager next time, you see a message on hello notification bar that hello gateway has been updated along with a link too[what's new topic](data-factory-gateway-release-notes.md).</span></span>

### <a name="toodisableenable-auto-update-feature"></a><span data-ttu-id="7f30a-323">функция toodisable Включение автоматического обновления</span><span class="sxs-lookup"><span data-stu-id="7f30a-323">toodisable/enable auto-update feature</span></span>
<span data-ttu-id="7f30a-324">Вы можете включить или отключить hello функция автоматического обновления, выполнив следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7f30a-324">You can disable/enable hello auto-update feature by doing hello following steps:</span></span>

<span data-ttu-id="7f30a-325">(Для шлюза с одним узлом)</span><span class="sxs-lookup"><span data-stu-id="7f30a-325">[For single node gateway]</span></span>
1. <span data-ttu-id="7f30a-326">Запустите Windows PowerShell на компьютере шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-326">Launch Windows PowerShell on hello gateway machine.</span></span>
2. <span data-ttu-id="7f30a-327">Перейдите в папку C:\Program Files\Microsoft данных управления Gateway\2.0\PowerShellScript toohello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-327">Switch toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="7f30a-328">Выполнения hello после автоматического обновления команда hello tooturn компонентов OFF (отключено).</span><span class="sxs-lookup"><span data-stu-id="7f30a-328">Run hello following command tooturn hello auto-update feature OFF (disable).</span></span>   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. <span data-ttu-id="7f30a-329">tooturn его обратно на:</span><span class="sxs-lookup"><span data-stu-id="7f30a-329">tooturn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
<span data-ttu-id="7f30a-330">([Для высокодоступного и масштабируемого шлюза с несколькими узлами (предварительная версия)](data-factory-data-management-gateway-high-availability-scalability.md))</span><span class="sxs-lookup"><span data-stu-id="7f30a-330">[[For multi-node highly available and scalable gateway (preview)](data-factory-data-management-gateway-high-availability-scalability.md)]</span></span>
1. <span data-ttu-id="7f30a-331">Запустите Windows PowerShell на компьютере шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-331">Launch Windows PowerShell on hello gateway machine.</span></span>
2. <span data-ttu-id="7f30a-332">Перейдите в папку C:\Program Files\Microsoft данных управления Gateway\2.0\PowerShellScript toohello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-332">Switch toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="7f30a-333">Выполнения hello после автоматического обновления команда hello tooturn компонентов OFF (отключено).</span><span class="sxs-lookup"><span data-stu-id="7f30a-333">Run hello following command tooturn hello auto-update feature OFF (disable).</span></span>   

    <span data-ttu-id="7f30a-334">Для шлюза с функцией высокой доступности (предварительная версия) требуется дополнительный параметр AuthKey.</span><span class="sxs-lookup"><span data-stu-id="7f30a-334">For gateway with high availability feature (preview), an extra AuthKey param is required.</span></span>
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. <span data-ttu-id="7f30a-335">tooturn его обратно на:</span><span class="sxs-lookup"><span data-stu-id="7f30a-335">tooturn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
<span data-ttu-id="7f30a-336">При доступе к hello портал с компьютера, отличном от компьютера шлюза hello, убедитесь, что приложение hello диспетчер учетных данных могут подключаться toohello компьютере шлюза.</span><span class="sxs-lookup"><span data-stu-id="7f30a-336">If you access hello portal from a machine that is different from hello gateway machine, you must make sure that hello Credentials Manager application can connect toohello gateway machine.</span></span> <span data-ttu-id="7f30a-337">Приложение hello не могут получить доступ на компьютере шлюза hello, он не позволяет tooset учетные данные для источника данных hello и источника данных toohello tootest соединения.</span><span class="sxs-lookup"><span data-stu-id="7f30a-337">If hello application cannot reach hello gateway machine, it does not allow you tooset credentials for hello data source and tootest connection toohello data source.</span></span>  

<span data-ttu-id="7f30a-338">При использовании hello **задать учетные данные** приложения, портал hello шифрует учетные данные hello hello сертификат, указанный в hello **сертификат** вкладка hello **шлюза Configuration Manager** на компьютере шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-338">When you use hello **Setting Credentials** application, hello portal encrypts hello credentials with hello certificate specified in hello **Certificate** tab of hello **Gateway Configuration Manager** on hello gateway machine.</span></span>

<span data-ttu-id="7f30a-339">Если вы ищете подход на основе API для шифрования учетных данных hello, можно использовать hello [New AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) учетные данные tooencrypt командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f30a-339">If you are looking for an API-based approach for encrypting hello credentials, you can use hello [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet tooencrypt credentials.</span></span> <span data-ttu-id="7f30a-340">Hello командлет использует hello сертификата, что шлюз находится настроенный toouse tooencrypt hello, учетные данные.</span><span class="sxs-lookup"><span data-stu-id="7f30a-340">hello cmdlet uses hello certificate that gateway is configured toouse tooencrypt hello credentials.</span></span> <span data-ttu-id="7f30a-341">Добавьте зашифрованные учетные данные toohello **EncryptedCredential** элемент hello **connectionString** в hello JSON.</span><span class="sxs-lookup"><span data-stu-id="7f30a-341">You add encrypted credentials toohello **EncryptedCredential** element of hello **connectionString** in hello JSON.</span></span> <span data-ttu-id="7f30a-342">Использовать hello JSON с hello [New AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) командлета или в hello редактор фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="7f30a-342">You use hello JSON with hello [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet or in hello Data Factory Editor.</span></span>

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

<span data-ttu-id="7f30a-343">Для настройки учетных данных при помощи редактора фабрики данных существует еще один способ.</span><span class="sxs-lookup"><span data-stu-id="7f30a-343">There is one more approach for setting credentials using Data Factory Editor.</span></span> <span data-ttu-id="7f30a-344">При создании связанного сервера SQL службы с помощью редактора hello и введите учетные данные в виде обычного текста, hello, учетные данные шифруются с помощью сертификата, которому принадлежит служба фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-344">If you create a SQL Server linked service by using hello editor and you enter credentials in plain text, hello credentials are encrypted using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="7f30a-345">Он не использует этот шлюз является настроенным toouse сертификатов hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-345">It does NOT use hello certificate that gateway is configured toouse.</span></span> <span data-ttu-id="7f30a-346">Хотя этот способ работает быстрее в некоторых случаях, он менее безопасен.</span><span class="sxs-lookup"><span data-stu-id="7f30a-346">While this approach might be a little faster in some cases, it is less secure.</span></span> <span data-ttu-id="7f30a-347">Поэтому мы рекомендуем использовать его только для целей разработки и тестирования.</span><span class="sxs-lookup"><span data-stu-id="7f30a-347">Therefore, we recommend that you follow this approach only for development/testing purposes.</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="7f30a-348">Командлеты PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f30a-348">PowerShell cmdlets</span></span>
<span data-ttu-id="7f30a-349">В этом разделе описываются как toocreate и зарегистрируйте шлюз с помощью командлетов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f30a-349">This section describes how toocreate and register a gateway using Azure PowerShell cmdlets.</span></span>

1. <span data-ttu-id="7f30a-350">Запустите модуль **Azure PowerShell** в режиме администратора.</span><span class="sxs-lookup"><span data-stu-id="7f30a-350">Launch **Azure PowerShell** in administrator mode.</span></span>
2. <span data-ttu-id="7f30a-351">Войдите в учетную запись Azure tooyour, выполнив hello следующую команду и введите учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="7f30a-351">Log in tooyour Azure account by running hello following command and entering your Azure credentials.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="7f30a-352">Используйте hello **New AzureRmDataFactoryGateway** toocreate командлет логических шлюза следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7f30a-352">Use hello **New-AzureRmDataFactoryGateway** cmdlet toocreate a logical gateway as follows:</span></span>

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    <span data-ttu-id="7f30a-353">**Пример команды и выходных данных**:</span><span class="sxs-lookup"><span data-stu-id="7f30a-353">**Example command and output**:</span></span>

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. <span data-ttu-id="7f30a-354">В Azure PowerShell, перейдите в папку toohello: **данных управления C:\Program Files\Microsoft Gateway\2.0\PowerShellScript\**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-354">In Azure PowerShell, switch toohello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**.</span></span> <span data-ttu-id="7f30a-355">Запустите **RegisterGateway.ps1** связанный с локальной переменной hello **$Key** как показано в hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="7f30a-355">Run **RegisterGateway.ps1** associated with hello local variable **$Key** as shown in hello following command.</span></span> <span data-ttu-id="7f30a-356">Этот сценарий регистрирует агента клиента hello установлены на компьютере со шлюзом логических hello, созданные ранее.</span><span class="sxs-lookup"><span data-stu-id="7f30a-356">This script registers hello client agent installed on your machine with hello logical gateway you create earlier.</span></span>

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    <span data-ttu-id="7f30a-357">Hello шлюза на удаленном компьютере можно зарегистрировать с помощью параметра IsRegisterOnRemoteMachine hello.</span><span class="sxs-lookup"><span data-stu-id="7f30a-357">You can register hello gateway on a remote machine by using hello IsRegisterOnRemoteMachine parameter.</span></span> <span data-ttu-id="7f30a-358">Пример:</span><span class="sxs-lookup"><span data-stu-id="7f30a-358">Example:</span></span>

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. <span data-ttu-id="7f30a-359">Можно использовать hello **Get AzureRmDataFactoryGateway** командлет tooget hello список шлюзов в вашей фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="7f30a-359">You can use hello **Get-AzureRmDataFactoryGateway** cmdlet tooget hello list of Gateways in your data factory.</span></span> <span data-ttu-id="7f30a-360">Здравствуйте, когда **состояние** показывает **online**, это означает, что ваш шлюз является готов toouse.</span><span class="sxs-lookup"><span data-stu-id="7f30a-360">When hello **Status** shows **online**, it means your gateway is ready toouse.</span></span>

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
<span data-ttu-id="7f30a-361">Можно удалить шлюз с помощью hello **удаление AzureRmDataFactoryGateway** описание командлета и обновления для шлюза, используя hello **AzureRmDataFactoryGateway набор** командлетов.</span><span class="sxs-lookup"><span data-stu-id="7f30a-361">You can remove a gateway using hello **Remove-AzureRmDataFactoryGateway** cmdlet and update description for a gateway using hello **Set-AzureRmDataFactoryGateway** cmdlets.</span></span> <span data-ttu-id="7f30a-362">Дополнительную информацию о синтаксисе и другую информацию об этих командлетах см. в "Справочных материалах по командлетам фабрики данных".</span><span class="sxs-lookup"><span data-stu-id="7f30a-362">For syntax and other details about these cmdlets, see Data Factory Cmdlet Reference.</span></span>  

### <a name="list-gateways-using-powershell"></a><span data-ttu-id="7f30a-363">Вывод списка шлюзов с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f30a-363">List gateways using PowerShell</span></span>

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a><span data-ttu-id="7f30a-364">Удаление шлюза с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f30a-364">Remove gateway using PowerShell</span></span>

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a><span data-ttu-id="7f30a-365">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7f30a-365">Next steps</span></span>
* <span data-ttu-id="7f30a-366">В разделе [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="7f30a-366">See [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="7f30a-367">В примере hello Создание конвейера, который использует данные toomove шлюза hello tooan базы данных SQL Server в локальной среде BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="7f30a-367">In hello walkthrough, you create a pipeline that uses hello gateway toomove data from an on-premises SQL Server database tooan Azure blob.</span></span>  
