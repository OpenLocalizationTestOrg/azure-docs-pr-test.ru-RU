---
title: "aaaUse хранилища Azure Premium с SQL Server | Документы Microsoft"
description: "В этой статье использует ресурсы, созданные с помощью hello классической модели развертывания и дает рекомендации по использованию хранилища Azure Premium с SQL Server, работающий на виртуальных машинах Azure."
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/01/2017
ms.author: jroth
ms.openlocfilehash: 393ea2020b39ea686302ae632e1049935c24af00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a><span data-ttu-id="a8781-103">Использование хранилища Azure Premium Storage с SQL Server на виртуальных машинах</span><span class="sxs-lookup"><span data-stu-id="a8781-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span></span>
## <a name="overview"></a><span data-ttu-id="a8781-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a8781-104">Overview</span></span>
<span data-ttu-id="a8781-105">[Хранилище Azure Premium](../../../storage/common/storage-premium-storage.md) hello следующего поколения хранилище, обеспечивающее малая задержка и высокая пропускная способность ввода-ВЫВОДА.</span><span class="sxs-lookup"><span data-stu-id="a8781-105">[Azure Premium Storage](../../../storage/common/storage-premium-storage.md) is hello next generation of storage that provides low latency and high throughput IO.</span></span> <span data-ttu-id="a8781-106">Данное хранилище лучше справляется с интенсивными нагрузками ввода-вывода, как, например, SQL Server на [виртуальных машинах](https://azure.microsoft.com/services/virtual-machines/)IaaS.</span><span class="sxs-lookup"><span data-stu-id="a8781-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8781-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a8781-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a8781-108">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="a8781-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="a8781-109">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a8781-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="a8781-110">В этой статье приведены планированию и рекомендации по переносу виртуальной машины под управлением SQL Server toouse хранилище Premium.</span><span class="sxs-lookup"><span data-stu-id="a8781-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server toouse Premium Storage.</span></span> <span data-ttu-id="a8781-111">Она включает описание этапов работы с инфраструктурой Azure (сеть, хранилище) и гостевой виртуальной машиной Windows.</span><span class="sxs-lookup"><span data-stu-id="a8781-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span></span> <span data-ttu-id="a8781-112">пример Hello в hello [приложение](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) показано полное комплексное tooend миграции как улучшить toomove больше виртуальных машин tootake преимуществами локальной SSD-хранилище с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a8781-112">hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) shows a full comprehensive end tooend migration of how toomove larger VMs tootake advantage of improved local SSD storage with PowerShell.</span></span>

<span data-ttu-id="a8781-113">Это важные toounderstand процедура конца в конец hello используя хранилища Azure Premium с SQL Server на виртуальных машинах IAAS.</span><span class="sxs-lookup"><span data-stu-id="a8781-113">It is important toounderstand hello end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span></span> <span data-ttu-id="a8781-114">А именно:</span><span class="sxs-lookup"><span data-stu-id="a8781-114">This includes:</span></span>

* <span data-ttu-id="a8781-115">Идентификация hello предварительные требования toouse хранилище Premium.</span><span class="sxs-lookup"><span data-stu-id="a8781-115">Identification of hello prerequisites toouse Premium Storage.</span></span>
* <span data-ttu-id="a8781-116">Примеры развертывания SQL Server в IaaS tooPremium хранилища для нового развертывания.</span><span class="sxs-lookup"><span data-stu-id="a8781-116">Examples of deploying SQL Server on IaaS tooPremium Storage for new deployments.</span></span>
* <span data-ttu-id="a8781-117">Примеры миграции существующих развернутых служб — как отдельных серверов, так и развернутых служб, использующих группы доступности AlwaysOn SQL.</span><span class="sxs-lookup"><span data-stu-id="a8781-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span></span>
* <span data-ttu-id="a8781-118">Возможные подходы при миграции.</span><span class="sxs-lookup"><span data-stu-id="a8781-118">Possible migration approaches.</span></span>
* <span data-ttu-id="a8781-119">Пример полной конца в конец действия Azure, Windows и SQL Server для миграции hello существующую реализацию Always On.</span><span class="sxs-lookup"><span data-stu-id="a8781-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for hello migration of an existing Always On implementation.</span></span>

<span data-ttu-id="a8781-120">Более детальные дополнительные сведения о сервере SQL Server в виртуальных машинах Azure содержатся в статье [SQL Server в виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a8781-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

<span data-ttu-id="a8781-121">**Автор:** Дэниэл Сол (Daniel Sol) **Технические рецензенты:** Луис Карлос Варгас Херринг (Luis Carlos Vargas Herring), Санджай Мишра (Sanjay Mishra), Правин Митал (Pravin Mital), Юрген Томас (Juergen Thomas), Гонсало Руис (Gonzalo Ruiz).</span><span class="sxs-lookup"><span data-stu-id="a8781-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span></span>

## <a name="prerequisites-for-premium-storage"></a><span data-ttu-id="a8781-122">Необходимые условия для использования хранилища Premium Storage</span><span class="sxs-lookup"><span data-stu-id="a8781-122">Prerequisites for Premium Storage</span></span>
<span data-ttu-id="a8781-123">Существует несколько предварительных условий для использования Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="a8781-123">There are several prerequisites for using Premium Storage.</span></span>

### <a name="machine-size"></a><span data-ttu-id="a8781-124">Размер машины</span><span class="sxs-lookup"><span data-stu-id="a8781-124">Machine size</span></span>
<span data-ttu-id="a8781-125">Для использования хранилища Premium вам потребуется серии toouse DS виртуальные машины (VM).</span><span class="sxs-lookup"><span data-stu-id="a8781-125">For using Premium Storage you will need toouse DS series Virtual Machines (VM).</span></span> <span data-ttu-id="a8781-126">Если ранее не пользовались серии DS машин в облачной службе до, необходимо удалить существующие ВМ hello, исключить hello присоединенные диски и затем создать новую облачную службу, прежде чем повторно создавать виртуальную Машину в качестве доменных служб Active Directory роли размера hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-126">If you have not used DS Series machines in your cloud service before, you must delete hello existing VM, keep hello attached disks, and then create a new cloud service before recreating hello VM as DS* role size.</span></span> <span data-ttu-id="a8781-127">Дополнительные сведения о размерах виртуальных машин см. в статье [Размеры виртуальных машин и облачных служб для Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a8781-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="cloud-services"></a><span data-ttu-id="a8781-128">Облачные службы</span><span class="sxs-lookup"><span data-stu-id="a8781-128">Cloud services</span></span>
<span data-ttu-id="a8781-129">Виртуальные машины DS* можно использовать с хранилищем Premium Storage, только если они были созданы в новой облачной службе.</span><span class="sxs-lookup"><span data-stu-id="a8781-129">You can only use DS* VMs with Premium Storage when they are created in a new cloud service.</span></span> <span data-ttu-id="a8781-130">При использовании SQL Server Always On в Azure, hello всегда на прослушиватель будет ссылаться toohello Azure внутренний или внешний IP-адрес подсистемы балансировки нагрузки адрес, связанный с облачной службой.</span><span class="sxs-lookup"><span data-stu-id="a8781-130">If you are using SQL Server Always On in Azure, hello Always On Listener will refer toohello Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span></span> <span data-ttu-id="a8781-131">В этой статье основное внимание уделено toomigrate, сохраняя доступность в этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="a8781-131">This article focuses on how toomigrate while maintaining availability in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="a8781-132">Серии DS * необходимо hello первой виртуальной Машины, развернутой toohello новой облачной службы.</span><span class="sxs-lookup"><span data-stu-id="a8781-132">A DS* Series must be hello first VM that is deployed toohello new Cloud Service.</span></span>
>
>

### <a name="regional-vnets"></a><span data-ttu-id="a8781-133">Региональные виртуальные сети</span><span class="sxs-lookup"><span data-stu-id="a8781-133">Regional VNETS</span></span>
<span data-ttu-id="a8781-134">Для доменных служб Active Directory * виртуальных машин, необходимо настроить hello виртуальной сети (VNET) размещение ваш язык toobe виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a8781-134">For DS* VMs you must configure hello Virtual Network (VNET) hosting your VMs toobe regional.</span></span> <span data-ttu-id="a8781-135">Этот «может быть расширен» hello виртуальной сети является tooallow hello больше виртуальных машин toobe подготовлены в других кластерах и разрешить связь между ними.</span><span class="sxs-lookup"><span data-stu-id="a8781-135">This “widens” hello VNET is tooallow hello larger VMs toobe provisioned in other clusters and allow communication between them.</span></span> <span data-ttu-id="a8781-136">В следующий снимок экрана приветствия hello выделенное расположение показывает региональных виртуальных сетей, в то время как первый результат hello показывает «узких» виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a8781-136">In hello following screenshot, hello highlighted Location shows regional VNETs, whereas hello first result shows a “narrow” VNET.</span></span>

![RegionalVNET][1]

<span data-ttu-id="a8781-138">Можно вызвать tooa toomigrate службу поддержки Майкрософт региональной виртуальной сети, корпорация Майкрософт будут внесены изменения, то toocomplete hello миграции tooregional виртуальных сетей, изменив hello территориальная группа в конфигурации сети hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-138">You can raise a Microsoft support ticket toomigrate tooa regional VNET, Microsoft will make a change, then toocomplete hello migration tooregional VNETs, change hello property AffinityGroup in hello network configuration.</span></span> <span data-ttu-id="a8781-139">Экспортировать hello конфигурации сети в PowerShell, а затем замените hello **AffinityGroup** свойство в hello **VirtualNetworkSite** элемент с **расположение** свойство.</span><span class="sxs-lookup"><span data-stu-id="a8781-139">First export hello Network Configuration in PowerShell, and then replace hello **AffinityGroup** property in hello **VirtualNetworkSite** element with a **Location** property.</span></span> <span data-ttu-id="a8781-140">Укажите `Location = XXXX`, где `XXXX` регион Azure.</span><span class="sxs-lookup"><span data-stu-id="a8781-140">Specify `Location = XXXX` where `XXXX` is an Azure region.</span></span> <span data-ttu-id="a8781-141">Затем импортируйте новую конфигурацию hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-141">Then import hello new configuration.</span></span>

<span data-ttu-id="a8781-142">Например учитывая hello следующая конфигурация виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="a8781-142">For example, considering hello following VNET configuration:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

<span data-ttu-id="a8781-143">toomove этот tooa региональной виртуальной сети в Западной Европе изменить toohello конфигурации hello следующие:</span><span class="sxs-lookup"><span data-stu-id="a8781-143">toomove this tooa regional VNET in West Europe, change hello configuration toohello following:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a><span data-ttu-id="a8781-144">учетные записи хранения;</span><span class="sxs-lookup"><span data-stu-id="a8781-144">Storage accounts</span></span>
<span data-ttu-id="a8781-145">Вам потребуется toocreate новой учетной записи хранения, настроенной для хранения Premium.</span><span class="sxs-lookup"><span data-stu-id="a8781-145">You will need toocreate a new storage account that is configured for Premium Storage.</span></span> <span data-ttu-id="a8781-146">Обратите внимание, что использование hello хранилища Premium задается в учетной записи хранилища hello не для отдельных виртуальных жестких дисков, однако при использовании ВМ серии DS * можно присоединить виртуальные жесткие ДИСКИ из Premium и стандартное хранилище учетных записей.</span><span class="sxs-lookup"><span data-stu-id="a8781-146">Note that hello use of Premium Storage is set at hello storage account, not on individual VHDs, however when using a DS* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span></span> <span data-ttu-id="a8781-147">Это можно использовать, если tooplace hello виртуального жесткого диска операционной системы на toohello учетной записи хранения Premium не требуется.</span><span class="sxs-lookup"><span data-stu-id="a8781-147">You may consider this if you do not want tooplace hello OS VHD on toohello Premium Storage account.</span></span>

<span data-ttu-id="a8781-148">следующие Hello **New AzureStorageAccountPowerShell** с hello «Premium_LRS» **тип** создает учетную запись хранения Premium:</span><span class="sxs-lookup"><span data-stu-id="a8781-148">hello following **New-AzureStorageAccountPowerShell** command with hello "Premium_LRS" **Type** creates a Premium Storage Account:</span></span>

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a><span data-ttu-id="a8781-149">Настройки кэша виртуальных жестких дисков</span><span class="sxs-lookup"><span data-stu-id="a8781-149">VHDs Cache Settings</span></span>
<span data-ttu-id="a8781-150">Hello основное различие между созданием диски, которые являются частью учетной записи хранения Premium — параметр кэша диска hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-150">hello main difference between creating disks that are part of a Premium Storage account is hello disk cache setting.</span></span> <span data-ttu-id="a8781-151">Для дисков томов данных SQL Server рекомендуется использовать**кэширование чтения**.</span><span class="sxs-lookup"><span data-stu-id="a8781-151">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span></span> <span data-ttu-id="a8781-152">Тома журналов транзакций, параметр кэша диска hello следует установить слишком "**нет**".</span><span class="sxs-lookup"><span data-stu-id="a8781-152">For Transaction log volumes, hello disk cache setting should be set too‘**None**’.</span></span> <span data-ttu-id="a8781-153">Это отличается от hello рекомендаций для учетных записей стандартного хранилища.</span><span class="sxs-lookup"><span data-stu-id="a8781-153">This is different from hello recommendations for Standard Storage accounts.</span></span>

<span data-ttu-id="a8781-154">После присоединения виртуальных жестких дисков hello hello в кэше не могут быть изменены.</span><span class="sxs-lookup"><span data-stu-id="a8781-154">Once hello VHDs have been attached, hello cache setting cannot be altered.</span></span> <span data-ttu-id="a8781-155">Будет необходимо toodetach и заново присоединить hello виртуального жесткого диска с помощью параметра обновленным кэшем.</span><span class="sxs-lookup"><span data-stu-id="a8781-155">You would need toodetach and reattach hello VHD with an updated cache setting.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="a8781-156">Дисковое пространство Windows</span><span class="sxs-lookup"><span data-stu-id="a8781-156">Windows storage spaces</span></span>
<span data-ttu-id="a8781-157">Можно использовать [дисковые пространства Windows](https://technet.microsoft.com/library/hh831739.aspx) так же предыдущих стандартное хранилище, это позволит вам toomigrate виртуальной Машины, которая уже использует дисковые пространства.</span><span class="sxs-lookup"><span data-stu-id="a8781-157">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this will allow you toomigrate a VM that is already utilizing Storage Spaces.</span></span> <span data-ttu-id="a8781-158">пример Hello в [приложение](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (шаг 9 и далее) демонстрирует hello tooextract кода Powershell и Импорт виртуальной Машины с помощью нескольких подключенных виртуальных жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="a8781-158">hello example in [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (step 9 and forward) demonstrates hello Powershell code tooextract and import a VM with multiple attached VHDs.</span></span>

<span data-ttu-id="a8781-159">Пулы носителей использовались в пропускной способности tooenhance учетной записи хранилища Azure, Standard и уменьшить задержку.</span><span class="sxs-lookup"><span data-stu-id="a8781-159">Storage Pools were used with Standard Azure storage account tooenhance throughput and reduce latency.</span></span> <span data-ttu-id="a8781-160">Возможно, вам интересно будет попробовать пулы носителей в Premium Storage для новых развертываний, однако они создают дополнительные сложности при настройке хранилища.</span><span class="sxs-lookup"><span data-stu-id="a8781-160">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span></span>

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a><span data-ttu-id="a8781-161">Как toofind виртуальные диски Azure сопоставить toostorage пулы</span><span class="sxs-lookup"><span data-stu-id="a8781-161">How toofind which Azure Virtual Disks map toostorage pools</span></span>
<span data-ttu-id="a8781-162">Как рекомендации параметр отдельного кэша для подключенных виртуальных жестких дисков, вы можете toocopy hello виртуальные жесткие диски tooa учетной записи хранения Premium.</span><span class="sxs-lookup"><span data-stu-id="a8781-162">As there are different cache setting recommendations for attached VHDs, you might decide toocopy hello VHDs tooa Premium Storage account.</span></span> <span data-ttu-id="a8781-163">Тем не менее при повторном присоединении их новой серии DS toohello виртуальной Машины, может потребоваться параметры кэша tooalter hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-163">However, when you reattach them toohello new DS series VM, you might need tooalter hello cache settings.</span></span> <span data-ttu-id="a8781-164">Это проще приветствия tooapply хранилище Premium рекомендуемые параметры кэша, при наличии отдельных виртуальных жестких дисков для hello SQL данных файлов и журнала файлов (а не один виртуальный жесткий ДИСК, содержащий оба).</span><span class="sxs-lookup"><span data-stu-id="a8781-164">It is simpler tooapply hello Premium Storage recommended cache settings when you have separate VHDs for hello SQL Data files and log files (rather than a single VHD that contains both).</span></span>

> [!NOTE]
> <span data-ttu-id="a8781-165">Если у вас есть файлы данных и журналов SQL Server на hello одном томе, выбрать параметр кэширования hello зависит от hello шаблоны доступа к операции ввода-ВЫВОДА для базы данных рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="a8781-165">If you have SQL Server data and log files on hello same volume, hello caching option you choose depends on hello IO access patterns for your database workloads.</span></span> <span data-ttu-id="a8781-166">Только тестирование может показать, какой параметр кэширования лучше всего подходит для данного сценария.</span><span class="sxs-lookup"><span data-stu-id="a8781-166">Only testing can demonstrate which caching option is best for this scenario.</span></span>
>
>

<span data-ttu-id="a8781-167">Однако при использовании Windows дискового пространства, который состоит из нескольких виртуальных жестких дисков, необходимо будет toolook в вашей исходной tooidentify скрипты, связанные VHD, в какие конкретного пула таким образом можно затем задать параметры кэша hello соответствующим образом для каждого диска.</span><span class="sxs-lookup"><span data-stu-id="a8781-167">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you will need toolook at your original scripts tooidentify which attached VHDs are in what specific pool, so you can then set hello cache settings accordingly for each disk.</span></span>

<span data-ttu-id="a8781-168">Если нет исходного доступных tooshow сценария вы сопоставляющие виртуальные жесткие диски toohello пула носителей, можно использовать после действия toodetermine hello диска и хранилища пула сопоставления hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-168">If you do not have original script available tooshow you which VHDs map toohello storage pool, you can use hello following steps toodetermine hello disk/storage pool mapping.</span></span>

<span data-ttu-id="a8781-169">Для каждого диска используйте следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a8781-169">For each disk, use hello following steps:</span></span>

1. <span data-ttu-id="a8781-170">Получение списка дисков присоединенного tooVM с hello **Get-AzureVM** команды:</span><span class="sxs-lookup"><span data-stu-id="a8781-170">Get list of disks attached tooVM with hello **Get-AzureVM** command:</span></span>

    <span data-ttu-id="a8781-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span><span class="sxs-lookup"><span data-stu-id="a8781-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span></span>
2. <span data-ttu-id="a8781-172">Обратите внимание, hello Diskname и LUN.</span><span class="sxs-lookup"><span data-stu-id="a8781-172">Note hello Diskname and LUN.</span></span>

    ![DisknameAndLUN][2]
3. <span data-ttu-id="a8781-174">Удаленный рабочий стол в hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a8781-174">Remote desktop into hello VM.</span></span> <span data-ttu-id="a8781-175">Затем перейдите слишком**Управление компьютером** | **диспетчер устройств** | **дисков**.</span><span class="sxs-lookup"><span data-stu-id="a8781-175">Then go too**Computer Management** | **Device Manager** | **Disk Drives**.</span></span> <span data-ttu-id="a8781-176">Просмотрите свойства hello каждого hello «Microsoft виртуальных дисков»</span><span class="sxs-lookup"><span data-stu-id="a8781-176">Look at hello properties of each of hello ‘Microsoft Virtual Disks’</span></span>

    ![VirtualDiskProperties][3]
4. <span data-ttu-id="a8781-178">Hello здесь номер LUN является номер LUN toohello ссылки, указываемые при присоединении toohello hello виртуального жесткого диска виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a8781-178">hello LUN number here is a reference toohello LUN number you specify when attaching hello VHD toohello VM.</span></span>
5. <span data-ttu-id="a8781-179">Для hello «Виртуальный диск Microsoft» go toohello **сведения** на вкладке выберите hello **свойство** списка, перейдите в слишком**раздел реестра**.</span><span class="sxs-lookup"><span data-stu-id="a8781-179">For hello ‘Microsoft Virtual Disk’ go toohello **Details** tab, then in hello **Property** list, go too**Driver Key**.</span></span> <span data-ttu-id="a8781-180">В hello **значение**, Примечание hello **смещение**, который является 0002 в следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="a8781-180">In hello **Value**, note hello **Offset**, which is 0002 in hello following screenshot.</span></span> <span data-ttu-id="a8781-181">Hello 0002 обозначает hello PhysicalDisk2 hello ссылки пула носителей.</span><span class="sxs-lookup"><span data-stu-id="a8781-181">hello 0002 denotes hello PhysicalDisk2 that hello storage pool references.</span></span>

    ![VirtualDiskPropertyDetails][4]
6. <span data-ttu-id="a8781-183">Для каждого пула носителей выгрузите hello связанные диски:</span><span class="sxs-lookup"><span data-stu-id="a8781-183">For each storage pool, dump out hello associated disks:</span></span>

    <span data-ttu-id="a8781-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span><span class="sxs-lookup"><span data-stu-id="a8781-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span></span>

    ![GetStoragePool][5]

<span data-ttu-id="a8781-186">Теперь вы можете использовать этот tooassociate сведения присоединенных дисков tooPhysical виртуальные жесткие диски в пулы носителей.</span><span class="sxs-lookup"><span data-stu-id="a8781-186">Now you can use this information tooassociate attached VHDs tooPhysical Disks in Storage Pools.</span></span>

<span data-ttu-id="a8781-187">После сопоставления дисков tooPhysical виртуальные жесткие диски в пулы носителей можно отсоединить и скопировать tooa учетной записи хранения Premium присоедините их с правильный кэш hello задание.</span><span class="sxs-lookup"><span data-stu-id="a8781-187">Once you have mapped VHDs tooPhysical Disks in Storage Pools you can then detach and copy them over tooa Premium Storage account, then attach them with hello correct cache setting.</span></span> <span data-ttu-id="a8781-188">См. в разделе Пример hello в hello [приложение](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), шаги 8 – 12.</span><span class="sxs-lookup"><span data-stu-id="a8781-188">Please see hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), steps 8 through 12.</span></span> <span data-ttu-id="a8781-189">Следующие действия показывают, как tooextract VHD ВМ присоединенного диска tooa CSV файл конфигурации, скопируйте VHD hello, изменить настройки кэша диска hello и наконец повторного развертывания виртуальной Машины hello как серии DS виртуальной Машины с hello все подключенные диски.</span><span class="sxs-lookup"><span data-stu-id="a8781-189">These steps show how tooextract a VM-attached VHD disk configuration tooa CSV file, copy hello VHDs, alter hello disk configuration cache settings, and finally redeploy hello VM as a DS series VM with all hello attached disks.</span></span>

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a><span data-ttu-id="a8781-190">Пропускная способность хранилища виртуальной машины и хранилища VHD</span><span class="sxs-lookup"><span data-stu-id="a8781-190">VM storage bandwidth and VHD storage throughput</span></span>
<span data-ttu-id="a8781-191">Hello производительность хранилища зависит hello размер виртуальной Машины DS * указан и hello размер виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="a8781-191">hello amount of storage performance depends on hello DS* VM size specified and hello VHD sizes.</span></span> <span data-ttu-id="a8781-192">виртуальные машины Hello имели разные ограничения по производительности для hello количество виртуальных жестких дисков, которые можно подключить и максимальная пропускная способность (МБ/с), они будут поддерживать hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-192">hello VMs have different allowances for hello number of VHDs that can be attached and hello maximum bandwidth they will support (MB/s).</span></span> <span data-ttu-id="a8781-193">Номера hello используемой пропускной способности, см. [виртуальной машины размеры и облачных служб для Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a8781-193">For hello specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="a8781-194">Повышенная производительность диска достигается при увеличении размеров диска.</span><span class="sxs-lookup"><span data-stu-id="a8781-194">Increased IOPS are achieved with larger disk sizes.</span></span> <span data-ttu-id="a8781-195">Это следует учитывать при планировании миграции.</span><span class="sxs-lookup"><span data-stu-id="a8781-195">You should consider this when you think about your migration path.</span></span> <span data-ttu-id="a8781-196">Дополнительные сведения [см hello таблицы для операций ввода-ВЫВОДА и типы дисков](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="a8781-196">For details, [see hello table for IOPS and Disk Types](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span></span>

<span data-ttu-id="a8781-197">Наконец, следует помнить, что виртуальные машины имеют различную максимальную пропускную способность, которую они будут поддерживать для всех подключенных дисков.</span><span class="sxs-lookup"><span data-stu-id="a8781-197">Finally, consider that VMs have different maximum disk bandwidths they will support for all disks attached.</span></span> <span data-ttu-id="a8781-198">В условиях высокой нагрузки может перегрузке hello максимальное число дисковых пропускную способность, доступную для заданного размера роли виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a8781-198">Under high load, you could saturate hello maximum disk bandwidth available for that VM role size.</span></span> <span data-ttu-id="a8781-199">Например Standard_DS14 будет поддерживать too512MB в секунду; Таким образом с помощью трех дисков P30 удалось перегрузке пропускную способность диска hello hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a8781-199">For example a Standard_DS14 will support up too512MB/s; therefore, with three P30 disks you could saturate hello disk bandwidth of hello VM.</span></span> <span data-ttu-id="a8781-200">Однако в этом примере удалось превышен предел пропускной способности hello в зависимости от сочетание hello чтения и записи операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="a8781-200">But in this example, hello throughput limit could be exceeded depending on hello mix of read and write IOs.</span></span>

## <a name="new-deployments"></a><span data-ttu-id="a8781-201">Новые развертывания</span><span class="sxs-lookup"><span data-stu-id="a8781-201">New deployments</span></span>
<span data-ttu-id="a8781-202">Hello следующих двух разделах показано, как можно развернуть виртуальные машины SQL Server tooPremium хранилища.</span><span class="sxs-lookup"><span data-stu-id="a8781-202">hello next two sections demonstrate how you can deploy SQL Server VMs tooPremium Storage.</span></span> <span data-ttu-id="a8781-203">Как упоминалось ранее, вам не обязательно диска ОС hello tooplace на хранилище Premium.</span><span class="sxs-lookup"><span data-stu-id="a8781-203">As mentioned before, you do not necessarily need tooplace hello OS disk onto Premium storage.</span></span> <span data-ttu-id="a8781-204">Вы можете toodo это если планируется tooplace любой рабочей нагрузки, большим объемом операций ввода-ВЫВОДА на hello виртуального жесткого диска операционной системы.</span><span class="sxs-lookup"><span data-stu-id="a8781-204">You might choose toodo this if you are intending tooplace any intensive IO workloads on hello OS VHD.</span></span>

<span data-ttu-id="a8781-205">Hello в первом примере показано использование существующих образов коллекции Azure.</span><span class="sxs-lookup"><span data-stu-id="a8781-205">hello first example demonstrates utilizing existing Azure Gallery Images.</span></span> <span data-ttu-id="a8781-206">Hello во втором примере показано, как изображения toouse пользовательских виртуальных Машин, у вас есть учетная запись хранения Standard.</span><span class="sxs-lookup"><span data-stu-id="a8781-206">hello second example shows how toouse a custom VM image that you have in an existing Standard storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="a8781-207">В этих примерах предполагается, что вы уже создали региональную виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="a8781-207">These examples assume that you have already created a Regional VNET.</span></span>
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a><span data-ttu-id="a8781-208">Создание новой виртуальной машины с хранилищем Premium Storage с помощью образа из Коллекции</span><span class="sxs-lookup"><span data-stu-id="a8781-208">Create a new VM with Premium Storage with Gallery Image</span></span>
<span data-ttu-id="a8781-209">Hello приведенном ниже примере показано, как tooplace hello виртуального жесткого диска операционной системы на хранилище premium и подключить виртуальные жесткие диски для хранения Premium.</span><span class="sxs-lookup"><span data-stu-id="a8781-209">hello example below shows how tooplace hello OS VHD onto premium storage and attach Premium Storage VHDs.</span></span> <span data-ttu-id="a8781-210">Тем не менее можно также разместить диска ОС hello в стандартном хранилище учетной записи и затем подключить виртуальные жесткие диски, которые находятся в учетной записи хранения Premium.</span><span class="sxs-lookup"><span data-stu-id="a8781-210">However, you can also place hello OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span></span> <span data-ttu-id="a8781-211">Мы продемонстрируем оба сценария.</span><span class="sxs-lookup"><span data-stu-id="a8781-211">Both scenarios are demonstrated.</span></span>

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a><span data-ttu-id="a8781-212">Шаг 1. Создайте учетную запись хранения Premium</span><span class="sxs-lookup"><span data-stu-id="a8781-212">Step 1: Create a Premium Storage Account</span></span>
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a><span data-ttu-id="a8781-213">Шаг 2. Создайте новую облачную службу</span><span class="sxs-lookup"><span data-stu-id="a8781-213">Step 2: Create a New Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a><span data-ttu-id="a8781-214">Шаг 3. Зарезервируйте VIP облачной службы (необязательно)</span><span class="sxs-lookup"><span data-stu-id="a8781-214">Step 3: Reserve a Cloud Service VIP (Optional)</span></span>
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a><span data-ttu-id="a8781-215">Шаг 4. Создайте контейнер виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="a8781-215">Step 4: Create a VM Container</span></span>
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a><span data-ttu-id="a8781-216">Шаг 5. Разместите виртуальный жесткий диск операционной системы в хранилище Standard или Premium </span><span class="sxs-lookup"><span data-stu-id="a8781-216">Step 5: Placing OS VHD on Standard or Premium Storage</span></span>
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a><span data-ttu-id="a8781-217">Шаг 6. Создайте виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="a8781-217">Step 6: Create VM</span></span>
    #Get list of available SQL Server Images from hello Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember toochange tooDS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks tooVM Config
    #Note hello size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising hello Premium Storage enabled Storage account

    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-data1.vhd"
    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "logDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-log1.vhd"

    #Create VM
    $vmConfigsl  | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)  

    #Add RDP Endpoint
    $EndpointNameRDPInt = "3389"
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Add-AzureEndpoint -Name "EndpointNameRDP" -Protocol "TCP" -PublicPort "53385" -LocalPort $EndpointNameRDPInt  | Update-AzureVM

    #Check VHD storage account, these should be in $newxiostorageaccountname
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Get-AzureDataDisk
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName |Get-AzureOSDisk


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a><span data-ttu-id="a8781-218">Создать новый toouse ВМ хранилища Premium с помощью пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="a8781-218">Create a new VM toouse Premium Storage with a custom image</span></span>
<span data-ttu-id="a8781-219">В этом сценарии показана ситуация, где у вас есть существующие настраиваемые образы, хранящиеся в учетной записи хранения Standard.</span><span class="sxs-lookup"><span data-stu-id="a8781-219">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span></span> <span data-ttu-id="a8781-220">Как уже упоминалось, следует ли tooplace hello виртуального жесткого диска операционной системы на хранилище Premium, вам потребуется toocopy hello образ, который существует в hello Стандартная учетная запись хранения и передачи tooa хранилище Premium, прежде чем можно будет использовать.</span><span class="sxs-lookup"><span data-stu-id="a8781-220">As mentioned if you want tooplace hello OS VHD on Premium Storage you will need toocopy hello image that exists in hello Standard Storage account and transfer them tooa Premium Storage before it can be used.</span></span> <span data-ttu-id="a8781-221">Если у вас есть образ в локальной среде, можно также использовать этот метод toocopy, прямо toohello учетной записи хранения Premium.</span><span class="sxs-lookup"><span data-stu-id="a8781-221">If you have an image on-premises, you can also use this method toocopy that directly toohello Premium Storage account.</span></span>

#### <a name="step-1-create-storage-account"></a><span data-ttu-id="a8781-222">Шаг 1. Создайте учетную запись хранения</span><span class="sxs-lookup"><span data-stu-id="a8781-222">Step 1: Create Storage Account</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a><span data-ttu-id="a8781-223">Шаг 2. Создайте облачную службу</span><span class="sxs-lookup"><span data-stu-id="a8781-223">Step 2 Create Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a><span data-ttu-id="a8781-224">Шаг 3. Используйте существующий образ</span><span class="sxs-lookup"><span data-stu-id="a8781-224">Step 3: Use existing image</span></span>
<span data-ttu-id="a8781-225">Вы можете использовать существующий образ.</span><span class="sxs-lookup"><span data-stu-id="a8781-225">You can use an existing image.</span></span> <span data-ttu-id="a8781-226">Вы также можете [взять образ имеющегося компьютера](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a8781-226">Or, you can [take an image of an existing machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="a8781-227">Созданием образа компьютера hello Примечание не имеет toobe DS * машины.</span><span class="sxs-lookup"><span data-stu-id="a8781-227">Note hello machine you image does not have toobe DS* machine.</span></span> <span data-ttu-id="a8781-228">После получения изображений hello hello следующие шаги Показать как toocopy его toohello учетной записи хранения Premium с hello **AzureStorageBlobCopy начала** командлетов PowerShell для.</span><span class="sxs-lookup"><span data-stu-id="a8781-228">Once you have hello image, hello following steps show how toocopy it toohello Premium Storage account with hello **Start-AzureStorageBlobCopy** PowerShell commandlet.</span></span>

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a><span data-ttu-id="a8781-229">Шаг 4. Скопируйте BLOB-объект между учетными записями хранения</span><span class="sxs-lookup"><span data-stu-id="a8781-229">Step 4: Copy Blob between Storage Accounts</span></span>
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a><span data-ttu-id="a8781-230">Шаг 5. Регулярно проверяйте состояние копирования:</span><span class="sxs-lookup"><span data-stu-id="a8781-230">Step 5: Regularly check copy status:</span></span>
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a><span data-ttu-id="a8781-231">Шаг 6: Добавление образа диска tooAzure диск хранилища в подписке</span><span class="sxs-lookup"><span data-stu-id="a8781-231">Step 6: Add Image disk tooAzure disk Repository in Subscription</span></span>
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> <span data-ttu-id="a8781-232">Вы можете обнаружить, несмотря на то, что отчеты о состоянии hello как успех, по-прежнему получение аренды ошибка диска.</span><span class="sxs-lookup"><span data-stu-id="a8781-232">You may find that even though hello status reports as success, you could still get a disk lease error.</span></span> <span data-ttu-id="a8781-233">В этом случае подождите около 10 минут.</span><span class="sxs-lookup"><span data-stu-id="a8781-233">In this case, wait about 10 minutes.</span></span>
>
>

#### <a name="step-7--build-hello-vm"></a><span data-ttu-id="a8781-234">Шаг 7: Построение hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="a8781-234">Step 7:  Build hello VM</span></span>
<span data-ttu-id="a8781-235">Здесь вы создаете hello виртуальной Машины из образа и присоединения два виртуальных жестких дисков хранилища Premium:</span><span class="sxs-lookup"><span data-stu-id="a8781-235">Here you are building hello VM from your image and attaching two Premium Storage VHDs:</span></span>

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need toobe a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use tooDS Series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS3"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "theM)stC0mplexP@ssw0rd!”


    #Create VM Config
    $vmConfigsl2 = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $newimageName  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-Datadisk-1.vhd"
    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "LogDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-logdisk-1.vhd"



    $vmConfigsl2 | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a><span data-ttu-id="a8781-236">Существующие развернутые службы, не использующие группы доступности AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="a8781-236">Existing deployments that do not use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="a8781-237">Для существующих развертываний сначала узнать hello [необходимые компоненты](#prerequisites-for-premium-storage) этого раздела.</span><span class="sxs-lookup"><span data-stu-id="a8781-237">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="a8781-238">Существуют различные рекомендации относительно развертывания SQL Server — как без использования групп доступности AlwaysOn, так и с их использованием.</span><span class="sxs-lookup"><span data-stu-id="a8781-238">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span></span> <span data-ttu-id="a8781-239">Если вы не используете Always On и иметь существующий изолированный экземпляр SQL Server, вы можете обновить tooPremium хранилища с помощью облачной службы и хранилища учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a8781-239">If you are not using Always On and have an existing standalone SQL Server, you can upgrade tooPremium Storage by using a new cloud service and storage account.</span></span> <span data-ttu-id="a8781-240">Рассмотрим следующие варианты hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-240">Consider hello following options:</span></span>

* <span data-ttu-id="a8781-241">**Создать новую виртуальную машину SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a8781-241">**Create a new SQL Server VM**.</span></span> <span data-ttu-id="a8781-242">Вы можете создать новую виртуальную машину сервера SQL Server, использующую учетную запись хранения Premium, согласно описанию в пункте «Новые развертывания».</span><span class="sxs-lookup"><span data-stu-id="a8781-242">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span></span> <span data-ttu-id="a8781-243">Затем выполните резервное копирование и восстановление конфигурации сервера SQL Server и баз данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="a8781-243">Then backup and restore your SQL Server configuration and user databases.</span></span> <span data-ttu-id="a8781-244">Hello приложения потребуется обновить toobe tooreference hello нового SQL Server при доступе внутренне или внешне.</span><span class="sxs-lookup"><span data-stu-id="a8781-244">hello application will need toobe updated tooreference hello new SQL Server if it is being accessed internally or externally.</span></span> <span data-ttu-id="a8781-245">Вы должны были toocopy всех объектов «за пределы базы данных» как если бы вы занимались миграции (SxS) SQL Server на одном компьютере.</span><span class="sxs-lookup"><span data-stu-id="a8781-245">You would need toocopy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span></span> <span data-ttu-id="a8781-246">Это относится к таким объектам как имена входа, сертификаты и связанные серверы.</span><span class="sxs-lookup"><span data-stu-id="a8781-246">This includes objects such as logins, certificates, and linked servers.</span></span>
* <span data-ttu-id="a8781-247">**Миграция существующей виртуальной машины SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a8781-247">**Migrate an existing SQL Server VM**.</span></span> <span data-ttu-id="a8781-248">Для этого потребуется, отключая hello виртуальной Машине SQL Server, а затем передавая его новой облачной службы tooa, которая включает копирование всех его вложенных toohello VHD учетной записи хранения Premium.</span><span class="sxs-lookup"><span data-stu-id="a8781-248">This will require taking hello SQL Server VM offline, then transferring it tooa new cloud service, which includes copying all of its attached VHDs toohello Premium Storage account.</span></span> <span data-ttu-id="a8781-249">При hello виртуальная машина переходит в оперативный режим, имя узла сервера hello как перед будет ссылки на приложение hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-249">When hello VM comes online, hello application will reference hello server host name as before.</span></span> <span data-ttu-id="a8781-250">Имейте в виду, что влияет на размер hello hello существующий диск hello характеристики производительности.</span><span class="sxs-lookup"><span data-stu-id="a8781-250">Be aware that hello size of hello existing disk will affect hello performance characteristics.</span></span> <span data-ttu-id="a8781-251">Например 400 ГБ дискового возвращает округленное tooa P20.</span><span class="sxs-lookup"><span data-stu-id="a8781-251">For example, a 400 GB disk gets rounded up tooa P20.</span></span> <span data-ttu-id="a8781-252">Если вы знаете, не требуется, производительность диска, может повторно создать виртуальную Машину в качестве виртуальной Машины серии DS hello и подключить виртуальные жесткие диски спецификация размера и производительности hello, требуемую для хранения Premium.</span><span class="sxs-lookup"><span data-stu-id="a8781-252">If you know that you do not require that disk performance, then you could recreate hello VM as a DS Series VM, and attach Premium Storage VHDs of hello size/performance specification you require.</span></span> <span data-ttu-id="a8781-253">Затем можно отсоединить и заново присоединить hello файлы баз данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8781-253">Then you could detach and reattach hello SQL DB files.</span></span>

> [!NOTE]
> <span data-ttu-id="a8781-254">При копирования дисков VHD hello, следует иметь в виду hello размера, в зависимости от размера hello означает тип диска хранилища Premium они подразделяются, определяет спецификации производительности диска.</span><span class="sxs-lookup"><span data-stu-id="a8781-254">When copying hello VHD disks you should be aware of hello size, depending on hello size will mean what Premium Storage Disk type they fall into, this determines disk performance specification.</span></span> <span data-ttu-id="a8781-255">Размер Azure будет округление вверх toohello ближайшего диск, поэтому при наличии 400 ГБ дискового, это будет округляться tooa P20.</span><span class="sxs-lookup"><span data-stu-id="a8781-255">Azure will round up toohello nearest disk size, so if you have a 400GB disk, this will be rounded up tooa P20.</span></span> <span data-ttu-id="a8781-256">В зависимости от требований операции ввода-ВЫВОДА существующего объекта hello виртуального жесткого диска операционной системы может не потребоваться toomigrate этот tooa учетной записи хранения Premium.</span><span class="sxs-lookup"><span data-stu-id="a8781-256">Depending on your existing IO requirements of hello OS VHD, you might not need toomigrate this tooa Premium Storage account.</span></span>
>
>

<span data-ttu-id="a8781-257">Если SQL Server осуществляется извне, hello облачной службы VIP изменится.</span><span class="sxs-lookup"><span data-stu-id="a8781-257">If your SQL Server is accessed externally, then hello cloud service VIP will change.</span></span> <span data-ttu-id="a8781-258">Вы также будете иметь tooupdate конечных точек, списки управления доступом и DNS параметров.</span><span class="sxs-lookup"><span data-stu-id="a8781-258">You will also have tooupdate end points, ACLs, and DNS settings.</span></span>

## <a name="existing-deployments-that-use-always-on-availability-groups"></a><span data-ttu-id="a8781-259">Существующие развернутые службы, использующие группы доступности AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="a8781-259">Existing deployments that use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="a8781-260">Для существующих развертываний сначала узнать hello [необходимые компоненты](#prerequisites-for-premium-storage) этого раздела.</span><span class="sxs-lookup"><span data-stu-id="a8781-260">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="a8781-261">В начале этого раздела мы рассмотрим, как AlwaysOn взаимодействует с сетью Azure.</span><span class="sxs-lookup"><span data-stu-id="a8781-261">Initially in this section we will look at how Always On interacts with Azure Networking.</span></span> <span data-ttu-id="a8781-262">Затем мы произойдет сбой миграции в сценариях tootwo: где которое должно пройти некоторое время простоя миграций и миграций, где необходимо достичь минимальным временем простоя.</span><span class="sxs-lookup"><span data-stu-id="a8781-262">We will then break down migrations in tootwo scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span></span>

<span data-ttu-id="a8781-263">Локальные группы доступности AlwaysOn сервера SQL Server используют прослушиватель локально, при этом он регистрирует виртуальное имя DNS и IP-адрес, который разделяется между одним или несколькими серверами SQL.</span><span class="sxs-lookup"><span data-stu-id="a8781-263">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span></span> <span data-ttu-id="a8781-264">При подключении клиентов они маршрутизируются через hello прослушивателя IP toohello основного сервера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8781-264">When clients connect they are routed through hello listener IP toohello Primary SQL Server.</span></span> <span data-ttu-id="a8781-265">Это сервер hello, которому принадлежит hello всегда на IP-ресурс в это время.</span><span class="sxs-lookup"><span data-stu-id="a8781-265">This is hello server that owns hello Always On IP resource at that time.</span></span>

![DeploymentsUseAlways On][6]

<span data-ttu-id="a8781-267">В Microsoft Azure может иметь tooa только один IP-адрес сетевого Адаптера на hello виртуальной Машины, в заказ tooachieve Здравствуйте же уровень абстракции как локальной, Azure использует hello IP-адрес, назначенный toohello внутренний или внешний подсистемы балансировки нагрузки (ILB/ELB).</span><span class="sxs-lookup"><span data-stu-id="a8781-267">In Microsoft Azure you can have only one IP address assigned tooa NIC on hello VM, so in order tooachieve hello same layer of abstraction as on-premises, Azure utilizes hello IP address that is assigned toohello Internal/External Load Balancers (ILB/ELB).</span></span> <span data-ttu-id="a8781-268">Hello IP-ресурс, с которым между серверами hello задано toohello же IP-адрес как hello ILB/ELB.</span><span class="sxs-lookup"><span data-stu-id="a8781-268">hello IP resource that is shared between hello servers is set toohello same IP as hello ILB/ELB.</span></span> <span data-ttu-id="a8781-269">Он опубликован в hello DNS и клиентский трафик передается через hello ILB/ELB toohello основной реплику SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8781-269">This is published in hello DNS, and client traffic is passed through hello ILB/ELB toohello Primary SQL Server replica.</span></span> <span data-ttu-id="a8781-270">Hello ILB/ELB знает, что SQL Server является первичным, поскольку он использует зонды tooprobe hello всегда на IP-ресурс.</span><span class="sxs-lookup"><span data-stu-id="a8781-270">hello ILB/ELB knows which SQL Server is primary since it uses probes tooprobe hello Always On IP resource.</span></span> <span data-ttu-id="a8781-271">В предыдущем примере hello он проверяет каждый узел, содержащий конечную точку ссылается hello ELB/ILB, какое значение отвечает является hello основного сервера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8781-271">In hello previous example, it probes each node that has an endpoint referenced by hello ELB/ILB, whichever responds is hello Primary SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="a8781-272">Hello ILB и ELB оба назначаются tooa определенной Azure облачной службы, поэтому любой миграции в облако в Azure скорее всего повлечет за приветствия, приведет к изменению IP подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="a8781-272">hello ILB and ELB are both assigned tooa particular Azure cloud service, therefore any cloud migration in Azure will most likely mean that hello Load Balancer IP will change.</span></span>
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a><span data-ttu-id="a8781-273">Миграция развернутых служб AlwaysOn, допускающая некоторое время простоя</span><span class="sxs-lookup"><span data-stu-id="a8781-273">Migrating Always On deployments that can allow some downtime</span></span>
<span data-ttu-id="a8781-274">Имеются две стратегии toomigrate Always On развертывания, которая позволяет некоторое время простоя:</span><span class="sxs-lookup"><span data-stu-id="a8781-274">There are two strategies toomigrate Always On deployments that allow for some downtime:</span></span>

1. <span data-ttu-id="a8781-275">**Добавьте дополнительные tooan вторичных реплик в существующих всегда на кластер**</span><span class="sxs-lookup"><span data-stu-id="a8781-275">**Add more secondary replicas tooan existing Always On Cluster**</span></span>
2. <span data-ttu-id="a8781-276">**Перенос tooa новый всегда на кластер**</span><span class="sxs-lookup"><span data-stu-id="a8781-276">**Migrate tooa new Always On Cluster**</span></span>

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a><span data-ttu-id="a8781-277">1. Добавьте дополнительные вторичные реплики tooan существующий всегда на кластер</span><span class="sxs-lookup"><span data-stu-id="a8781-277">1. Add more Secondary Replicas tooan Existing Always On Cluster</span></span>
<span data-ttu-id="a8781-278">Одной из стратегий является tooadd toohello дополнительные базы данных-получатели группы доступности AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="a8781-278">One strategy is tooadd more secondaries toohello Always On Availability Group.</span></span> <span data-ttu-id="a8781-279">Требуется tooadd их в новой облачной службы и добавьте прослушиватель hello hello новый нагрузки балансировки IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a8781-279">You need tooadd these into a new cloud service and update hello listener with hello new load balancer IP.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="a8781-280">Точки простоя:</span><span class="sxs-lookup"><span data-stu-id="a8781-280">Points of downtime:</span></span>
* <span data-ttu-id="a8781-281">Проверка кластера.</span><span class="sxs-lookup"><span data-stu-id="a8781-281">Cluster Validation.</span></span>
* <span data-ttu-id="a8781-282">Тестирование отработки отказа AlwaysOn для новых вторичных реплик.</span><span class="sxs-lookup"><span data-stu-id="a8781-282">Testing Always On failovers for New Secondaries.</span></span>

<span data-ttu-id="a8781-283">При использовании пулов хранения Windows в рамках hello виртуальной Машины более высокую пропускную способность ввода-ВЫВОДА, то они будут отключены во время полной проверки кластера.</span><span class="sxs-lookup"><span data-stu-id="a8781-283">If you are using Windows Storage Pools within hello VM for higher IO throughput, then these will be taken offline during a Full Cluster Validation.</span></span> <span data-ttu-id="a8781-284">При добавлении кластера узлов toohello, Hello проверочный тест является обязательным.</span><span class="sxs-lookup"><span data-stu-id="a8781-284">hello validation test is required when you add nodes toohello cluster.</span></span> <span data-ttu-id="a8781-285">время Hello toorun hello теста может меняться, поэтому следует проверить это в вашей репрезентативной тестовой среды tooget приблизительное время сколько времени это займет.</span><span class="sxs-lookup"><span data-stu-id="a8781-285">hello time it takes toorun hello test can vary, so you should test this in your representative test environment tooget an approximate time of how long this will take.</span></span>

<span data-ttu-id="a8781-286">Когда выполняется переход на другой ресурс вручную и хаоса тестирование hello вновь добавлены функции высокой доступности AlwaysOn tooensure узлы должным образом необходимо выполнить подготовку.</span><span class="sxs-lookup"><span data-stu-id="a8781-286">You should provision time where you can perform manual failover and chaos testing on hello newly added nodes tooensure Always On High Availability functions as expected.</span></span>

![DeploymentUseAlways On2][7]

> [!NOTE]
> <span data-ttu-id="a8781-288">Следует остановить все экземпляры SQL Server, где используются пулы носителей hello перед hello проверка выполняется.</span><span class="sxs-lookup"><span data-stu-id="a8781-288">You should stop all instances of SQL Server where hello Storage Pools are used before hello Validation runs.</span></span>
>
> ##### <a name="high-level-steps"></a><span data-ttu-id="a8781-289">Пошаговые действия</span><span class="sxs-lookup"><span data-stu-id="a8781-289">High-level steps</span></span>
>

1. <span data-ttu-id="a8781-290">Создайте два новых сервера SQL в новой облачной службе с присоединенным хранилищем Premium.</span><span class="sxs-lookup"><span data-stu-id="a8781-290">Create two new SQL Servers in new cloud service with attached Premium Storage.</span></span>
2. <span data-ttu-id="a8781-291">Скопируйте ПОЛНЫЕ резервные копии и восстановите их с помощью **NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="a8781-291">Copy over FULL backups and restore with **NORECOVERY**.</span></span>
3. <span data-ttu-id="a8781-292">Скопируйте зависимые объекты «не из базы данных пользователя», например имена входа и т. д.</span><span class="sxs-lookup"><span data-stu-id="a8781-292">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span></span>
4. <span data-ttu-id="a8781-293">Создайте новую внутреннюю подсистему балансировки нагрузки (ILB) или используйте внешнюю подсистему балансировки нагрузки (ELB), а затем настройте конечные точки с балансировкой нагрузки на обоих новых узлах.</span><span class="sxs-lookup"><span data-stu-id="a8781-293">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a8781-294">Убедитесь, что все узлы имеют hello правильной конфигурации конечной точки, прежде чем продолжить</span><span class="sxs-lookup"><span data-stu-id="a8781-294">Check all Nodes have hello correct Endpoint configuration before you continue</span></span>
   >
   >
5. <span data-ttu-id="a8781-295">Остановите toohello доступ пользователя или приложения SQL Server (если используются пулы носителей).</span><span class="sxs-lookup"><span data-stu-id="a8781-295">Stop User/Application Access toohello SQL Server (if using Storage Pools).</span></span>
6. <span data-ttu-id="a8781-296">Остановите службы ядра SQL Server на всех узлах (если используются пулы носителей).</span><span class="sxs-lookup"><span data-stu-id="a8781-296">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span></span>
7. <span data-ttu-id="a8781-297">Добавить новые узлы toocluster и запустить полную проверку.</span><span class="sxs-lookup"><span data-stu-id="a8781-297">Add new Nodes toocluster and run full validation.</span></span>
8. <span data-ttu-id="a8781-298">Если проверка прошла успешно, запустите все службы SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8781-298">Once Validation is successful, start all SQL Server Services.</span></span>
9. <span data-ttu-id="a8781-299">Выполните резервное копирование журналов транзакций и восстановление баз данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="a8781-299">Backup Transaction logs, and restore user databases.</span></span>
10. <span data-ttu-id="a8781-300">Добавление новых узлов в группы доступности AlwaysOn hello и поместите репликации в **синхронной**.</span><span class="sxs-lookup"><span data-stu-id="a8781-300">Add new nodes into hello Always On Availability Group and place replication into **Synchronous**.</span></span>
11. <span data-ttu-id="a8781-301">Добавить IP-адрес hello адрес ресурса hello новой облачной службы ILB/ELB через PowerShell для AlwaysOn на основании hello несколькими сайтами примера в hello [приложение](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="a8781-301">Add hello IP address resource of hello new Cloud Service ILB/ELB through PowerShell for Always On based on hello Multi-site example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span> <span data-ttu-id="a8781-302">В кластерах Windows установите hello **возможных владельцев** из hello **IP-адрес** toohello новые узлы ресурсов старого.</span><span class="sxs-lookup"><span data-stu-id="a8781-302">In Windows clustering, set hello **Possible owners** of hello **IP Address** resource toohello new nodes old.</span></span> <span data-ttu-id="a8781-303">Обратитесь к разделу «Добавление ресурса IP-адреса в одной подсети» hello hello [приложение](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="a8781-303">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
12. <span data-ttu-id="a8781-304">Переход на другой ресурс tooone hello новых узлов.</span><span class="sxs-lookup"><span data-stu-id="a8781-304">Failover tooone of hello new nodes.</span></span>
13. <span data-ttu-id="a8781-305">Внесите hello новых узлов партнеров автоматического перехода на другой ресурс и тестовые отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="a8781-305">Make hello new nodes Auto Failover Partners and test failovers.</span></span>
14. <span data-ttu-id="a8781-306">Удалите исходные узлы из группы доступности.</span><span class="sxs-lookup"><span data-stu-id="a8781-306">Remove original nodes from Availability Group.</span></span>

##### <a name="advantages"></a><span data-ttu-id="a8781-307">Преимущества</span><span class="sxs-lookup"><span data-stu-id="a8781-307">Advantages</span></span>
* <span data-ttu-id="a8781-308">Новые серверы SQL можно проверить (SQL Server и приложений) перед добавлением на tooAlways.</span><span class="sxs-lookup"><span data-stu-id="a8781-308">New SQL Servers can be tested (SQL Server and Application) before they are added tooAlways On.</span></span>
* <span data-ttu-id="a8781-309">Можно изменить размер виртуальной Машины hello и настроить hello хранилища tooyour точные требования.</span><span class="sxs-lookup"><span data-stu-id="a8781-309">You can change hello VM size and customize hello storage tooyour exact requirements.</span></span> <span data-ttu-id="a8781-310">Однако было бы полезно tookeep все пути к файлам SQL hello hello таким же.</span><span class="sxs-lookup"><span data-stu-id="a8781-310">However, it would be beneficial tookeep all hello SQL file paths hello same.</span></span>
* <span data-ttu-id="a8781-311">Можно управлять начала передачи hello toohello резервные копии БД hello вторичных реплик.</span><span class="sxs-lookup"><span data-stu-id="a8781-311">You can control when hello transfer of hello DB backups toohello Secondary Replicas are started.</span></span> <span data-ttu-id="a8781-312">Это отличается от использования Azure **AzureStorageBlobCopy начала** toocopy командлетов для виртуальных жестких дисков, так как это асинхронную копию.</span><span class="sxs-lookup"><span data-stu-id="a8781-312">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet toocopy VHDs, because that is an asynchronous copy.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="a8781-313">Недостатки</span><span class="sxs-lookup"><span data-stu-id="a8781-313">Disadvantages</span></span>
* <span data-ttu-id="a8781-314">При использовании пулов хранения Windows, происходит во время hello полной проверки кластеров для hello новые дополнительные узлы кластера простой.</span><span class="sxs-lookup"><span data-stu-id="a8781-314">When using Windows Storage Pools, there is Cluster downtime during hello Full Cluster Validation for hello new additional nodes.</span></span>
* <span data-ttu-id="a8781-315">В зависимости от версии SQL Server hello и hello существующих число вторичных реплик, может не быть может tooadd несколько вторичных реплик, не удаляя существующих баз данных-получателей.</span><span class="sxs-lookup"><span data-stu-id="a8781-315">Depending on hello SQL Server Version and hello existing number of secondary replicas, you might not be able tooadd more secondary replicas without removing existing secondaries.</span></span>
* <span data-ttu-id="a8781-316">Может быть много времени передачи данных SQL при настройке баз данных-получателей hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-316">There could be long SQL data transfer time while setting up hello secondaries.</span></span>
* <span data-ttu-id="a8781-317">В случае параллельной работы новых машин это может повлечь дополнительные расходы при миграции.</span><span class="sxs-lookup"><span data-stu-id="a8781-317">There is additional cost during migration while you have new machines running in parallel.</span></span>

#### <a name="2-migrate-tooa-new-always-on-cluster"></a><span data-ttu-id="a8781-318">2. Перенос tooa новый всегда на кластер</span><span class="sxs-lookup"><span data-stu-id="a8781-318">2. Migrate tooa new Always On Cluster</span></span>
<span data-ttu-id="a8781-319">Другая стратегия — toocreate совершенно новый всегда на кластере с совершенно новые узлы в новой облачной службы, а затем перенаправления hello клиентов toouse его.</span><span class="sxs-lookup"><span data-stu-id="a8781-319">Another strategy is toocreate a brand new Always On Cluster with brand new nodes in new cloud service and then redirect hello clients toouse it.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="a8781-320">Точки простоя</span><span class="sxs-lookup"><span data-stu-id="a8781-320">Points of downtime</span></span>
<span data-ttu-id="a8781-321">Нет простоев при переносе приложений и пользователей toohello Always On прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="a8781-321">There is downtime when you transfer applications and users toohello new Always On listener.</span></span> <span data-ttu-id="a8781-322">зависит от времени простоя Hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-322">hello downtime depends on:</span></span>

* <span data-ttu-id="a8781-323">Hello время toodatabases резервные копии журнала транзакций toorestore на новых серверах.</span><span class="sxs-lookup"><span data-stu-id="a8781-323">hello time taken toorestore final transaction log backups toodatabases on new servers.</span></span>
* <span data-ttu-id="a8781-324">Hello время, затраченное tooupdate клиентских приложений toouse Always On прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="a8781-324">hello time taken tooupdate client applications toouse new Always On listener.</span></span>

##### <a name="advantages"></a><span data-ttu-id="a8781-325">Преимущества</span><span class="sxs-lookup"><span data-stu-id="a8781-325">Advantages</span></span>
* <span data-ttu-id="a8781-326">Можно проверить hello реальной производственной среде, SQL Server, и изменения сборки операционной системы.</span><span class="sxs-lookup"><span data-stu-id="a8781-326">You can test hello actual production environment, SQL Server, and OS build changes.</span></span>
* <span data-ttu-id="a8781-327">У вас есть hello параметр toocustomize hello хранилище и toopotentially уменьшить размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a8781-327">You have hello option toocustomize hello storage and toopotentially reduce size of VM.</span></span> <span data-ttu-id="a8781-328">Это может способствовать снижению затрат.</span><span class="sxs-lookup"><span data-stu-id="a8781-328">This could result in cost reduction.</span></span>
* <span data-ttu-id="a8781-329">Во время этого процесса можно обновить сборку или версию SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8781-329">You can update your SQL Server build or version during this process.</span></span> <span data-ttu-id="a8781-330">Можно также обновить hello операционной системы.</span><span class="sxs-lookup"><span data-stu-id="a8781-330">You can also upgrade hello Operating System.</span></span>
* <span data-ttu-id="a8781-331">Здравствуйте, предыдущие всегда на кластер может выступать в качестве целевой сплошной отката.</span><span class="sxs-lookup"><span data-stu-id="a8781-331">hello previous Always On Cluster can act as a solid rollback target.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="a8781-332">Недостатки</span><span class="sxs-lookup"><span data-stu-id="a8781-332">Disadvantages</span></span>
* <span data-ttu-id="a8781-333">Требуется toochange hello DNS-имя прослушивателя hello, если требуются оба кластера Always On, работающими одновременно.</span><span class="sxs-lookup"><span data-stu-id="a8781-333">You need toochange hello DNS name of hello listener if you want both Always On clusters running simultaneously.</span></span> <span data-ttu-id="a8781-334">Это добавляет администрирования нагрузку во время миграции hello строк клиентского приложения должен содержать hello новое имя прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="a8781-334">This adds administration overhead during hello migration as client application strings must reflect hello new Listener name.</span></span>
* <span data-ttu-id="a8781-335">Необходимо реализовать механизм синхронизации между двух сред tookeep hello их как закрыть как возможные toominimize hello финальная синхронизация требований перед миграцией.</span><span class="sxs-lookup"><span data-stu-id="a8781-335">You must implement a synchronization mechanism between hello two environments tookeep them as close as possible toominimize hello final synchronization requirements before migration.</span></span>
* <span data-ttu-id="a8781-336">Во время миграции будет добавлен затрат, при наличии hello новой среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="a8781-336">There is added cost during migration while you have hello new environment running.</span></span>

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a><span data-ttu-id="a8781-337">Миграция развернутых служб AlwaysOn для минимального времени простоя</span><span class="sxs-lookup"><span data-stu-id="a8781-337">Migrating Always On Deployments for minimal downtime</span></span>
<span data-ttu-id="a8781-338">Существуют две стратегии миграции развернутых служб AlwaysOn для минимального времени простоя:</span><span class="sxs-lookup"><span data-stu-id="a8781-338">There are two strategies for migrating Always On deployments for minimal downtime:</span></span>

1. <span data-ttu-id="a8781-339">**Использование существующей вторичной реплики: один узел**</span><span class="sxs-lookup"><span data-stu-id="a8781-339">**Utilize an Existing Secondary: Single-Site**</span></span>
2. <span data-ttu-id="a8781-340">**Использование существующей вторичной реплики (реплик): несколько узлов**</span><span class="sxs-lookup"><span data-stu-id="a8781-340">**Utilize Existing Secondary Replica(s): Multi-Site**</span></span>

#### <a name="1-utilize-an-existing-secondary-single-site"></a><span data-ttu-id="a8781-341">1. Использование существующей вторичной реплики: один узел</span><span class="sxs-lookup"><span data-stu-id="a8781-341">1. Utilize an existing secondary: Single-Site</span></span>
<span data-ttu-id="a8781-342">Стратегия минимальным временем простоя tootake вторичной существующее облако и удалить ее из hello текущего облачной службы.</span><span class="sxs-lookup"><span data-stu-id="a8781-342">One strategy for minimal downtime is tootake an existing cloud secondary and remove it from hello current cloud service.</span></span> <span data-ttu-id="a8781-343">Затем скопируйте hello виртуальные жесткие диски toohello новой Premium учетной записи хранилища и создать hello виртуальной Машины в новой облачной службе hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-343">Then copy hello VHDs toohello new Premium Storage account, and create hello VM in hello new cloud service.</span></span> <span data-ttu-id="a8781-344">Затем обновите прослушивателя hello в кластеризации и переход на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="a8781-344">Then update hello listener in clustering and failover.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="a8781-345">Точки простоя</span><span class="sxs-lookup"><span data-stu-id="a8781-345">Points of downtime</span></span>
* <span data-ttu-id="a8781-346">Нет времени простоя при обновлении конечной точки с балансировкой нагрузки hello hello конечный узел.</span><span class="sxs-lookup"><span data-stu-id="a8781-346">There is downtime when you update hello final node with hello Load Balanced endpoint.</span></span>
* <span data-ttu-id="a8781-347">Повторное подключение вашего клиента может задерживаться в зависимости от конфигурации клиента/DNS.</span><span class="sxs-lookup"><span data-stu-id="a8781-347">Your client reconnection might be delayed depending on your client/DNS configuration.</span></span>
* <span data-ttu-id="a8781-348">Нет дополнительных время простоя при выборе tootake hello всегда на кластере группы вне сети tooswap out hello IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="a8781-348">There is additional downtime if you choose tootake hello Always On Cluster group offline tooswap out hello IP addresses.</span></span> <span data-ttu-id="a8781-349">Этого можно избежать с помощью или зависимостей и возможных владельцев для hello добавлен ресурс IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="a8781-349">You can avoid this by using an OR dependency and Possible Owners for hello added IP Address resource.</span></span> <span data-ttu-id="a8781-350">Обратитесь к разделу «Добавление ресурса IP-адреса в одной подсети» hello hello [приложение](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="a8781-350">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>

> [!NOTE]
> <span data-ttu-id="a8781-351">При необходимости hello toopartake добавленный узел в качестве всегда на переход на другой ресурс партнера необходимо tooadd конечная точка Azure с toohello ссылки, задать нагрузки балансировки.</span><span class="sxs-lookup"><span data-stu-id="a8781-351">When you want hello added node toopartake in as an Always On Failover Partner, you need tooadd an Azure Endpoint with a reference toohello Load Balanced Set.</span></span> <span data-ttu-id="a8781-352">При запуске hello **Add-AzureEndpoint** команды toodo, текущего подключения tooremain открыть, но новый прослушиватель toohello подключения не будет возможности toobe установлено, пока не был обновлен hello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="a8781-352">When you run hello **Add-AzureEndpoint** command toodo this, current connections tooremain open, but new connections toohello listener will not be able toobe established until hello load balancer has updated.</span></span> <span data-ttu-id="a8781-353">При тестировании это замеченный toolast 90-120секунд, это следует проверить.</span><span class="sxs-lookup"><span data-stu-id="a8781-353">In testing this was seen toolast 90-120seconds, this should be tested.</span></span>
>
>

##### <a name="advantages"></a><span data-ttu-id="a8781-354">Преимущества</span><span class="sxs-lookup"><span data-stu-id="a8781-354">Advantages</span></span>
* <span data-ttu-id="a8781-355">Дополнительные затраты при миграции не возникают.</span><span class="sxs-lookup"><span data-stu-id="a8781-355">No extra cost incurred during migration.</span></span>
* <span data-ttu-id="a8781-356">Миграция один к одному.</span><span class="sxs-lookup"><span data-stu-id="a8781-356">A one-to-one migration.</span></span>
* <span data-ttu-id="a8781-357">Меньший уровень сложности.</span><span class="sxs-lookup"><span data-stu-id="a8781-357">Reduced complexity.</span></span>
* <span data-ttu-id="a8781-358">Позволяет увеличить операции ввода-вывода из SKU хранилища Premium.</span><span class="sxs-lookup"><span data-stu-id="a8781-358">Allows for increased IOPS from Premium Storage SKUs.</span></span> <span data-ttu-id="a8781-359">Если hello диски отсоединения от hello виртуальной Машины и скопировать toohello новой облачной службе сторонний средство можно размер виртуального жесткого диска используется tooincrease hello, предоставляющий выше пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="a8781-359">When hello disks are detached from hello VM and copied toohello new cloud service, a 3rd party tool can be used tooincrease hello VHD size, which provides higher throughputs.</span></span> <span data-ttu-id="a8781-360">Для увеличения размера виртуального жесткого диска ознакомьтесь с комментариями на [форуме](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span><span class="sxs-lookup"><span data-stu-id="a8781-360">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="a8781-361">Недостатки</span><span class="sxs-lookup"><span data-stu-id="a8781-361">Disadvantages</span></span>
* <span data-ttu-id="a8781-362">Возникают временные потери в высокой доступности и аварийном восстановлении во время миграции.</span><span class="sxs-lookup"><span data-stu-id="a8781-362">There is a temporary loss of HA and DR during migration.</span></span>
* <span data-ttu-id="a8781-363">Как это миграции 1:1, будет иметь toouse минимальный размер виртуальной Машины, который будет поддерживать ваш номер виртуальных жестких дисков, не будет возможности toodownsize виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a8781-363">As this is a 1:1 migration, you will have toouse a minimum VM size that will support your number of VHDs, so you might not be able toodownsize your VMs.</span></span>
* <span data-ttu-id="a8781-364">Этот сценарий будет использовать hello Azure **AzureStorageBlobCopy начала** командлет, который является асинхронным.</span><span class="sxs-lookup"><span data-stu-id="a8781-364">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="a8781-365">Соглашение об уровне обслуживания после завершения копирования отсутствует.</span><span class="sxs-lookup"><span data-stu-id="a8781-365">There is no SLA on copy completion.</span></span> <span data-ttu-id="a8781-366">время Hello hello копий зависит, тогда это зависит от ожидания в очереди, к которой он также зависит от объема hello tootransfer данных.</span><span class="sxs-lookup"><span data-stu-id="a8781-366">hello time of hello copies varies, while this depends on wait in queue it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="a8781-367">Hello время копирования увеличивается, если происходит передача hello tooanother центр обработки данных Azure, поддерживающий хранение Premium в другой области.</span><span class="sxs-lookup"><span data-stu-id="a8781-367">hello copy time increases if hello transfer is going tooanother Azure data center that supports Premium Storage in another region.</span></span> <span data-ttu-id="a8781-368">При наличии только 2 узлов, рассмотрите возможности по устранению рисков в случае копирования hello требуется больше времени, чем при тестировании.</span><span class="sxs-lookup"><span data-stu-id="a8781-368">If you just have 2 nodes, consider a possible mitigation in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="a8781-369">Сюда могут входить следующие идеи hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-369">This could include hello following ideas.</span></span>
  * <span data-ttu-id="a8781-370">Добавьте временный сторонних узел SQL Server для обеспечения высокой ДОСТУПНОСТИ перед миграцией hello согласованный простоев.</span><span class="sxs-lookup"><span data-stu-id="a8781-370">Add a temporary 3rd SQL Server node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="a8781-371">Выполните миграцию hello за пределами Azure запланированного обслуживания.</span><span class="sxs-lookup"><span data-stu-id="a8781-371">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="a8781-372">Убедиться, что кворум кластера настроен правильно.</span><span class="sxs-lookup"><span data-stu-id="a8781-372">Ensure you have configured your cluster quorum correctly.</span></span>  

##### <a name="high-level-steps"></a><span data-ttu-id="a8781-373">Пошаговые действия</span><span class="sxs-lookup"><span data-stu-id="a8781-373">High-level steps</span></span>
<span data-ttu-id="a8781-374">В этом документе не демонстрирует завершения tooend пример, однако hello [приложение](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) предоставляет сведения, которые можно использовать tooperform это.</span><span class="sxs-lookup"><span data-stu-id="a8781-374">This document does not demonstrate a complete end tooend example, however hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) provides details that can be leveraged tooperform this.</span></span>

![MinimalDowntime][8]

* <span data-ttu-id="a8781-376">Конфигурация диска сбора и удалить узел hello (не удаляйте подключенных виртуальных жестких дисков).</span><span class="sxs-lookup"><span data-stu-id="a8781-376">Gather disk configuration, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="a8781-377">Создайте учетную запись хранения Premium и скопируйте виртуальные жесткие диски из hello Стандартная учетная запись хранения</span><span class="sxs-lookup"><span data-stu-id="a8781-377">Create a Premium Storage account and copy VHDs from hello Standard Storage account</span></span>
* <span data-ttu-id="a8781-378">Создать новую облачную службу и повторно развернуть hello SQL2 виртуальной Машины в этой облачной службе.</span><span class="sxs-lookup"><span data-stu-id="a8781-378">Create new cloud service and redeploy hello SQL2 VM in that cloud service.</span></span> <span data-ttu-id="a8781-379">Создать hello виртуальной Машины с помощью hello копируется исходный виртуальный жесткий ДИСК операционной системы и присоединение hello копирования виртуальных жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="a8781-379">Create hello VM using hello copied original OS VHD and attaching hello copied VHDs.</span></span>
* <span data-ttu-id="a8781-380">Настройте ILB/ELB и добавьте конечные точки.</span><span class="sxs-lookup"><span data-stu-id="a8781-380">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="a8781-381">Обновите прослушиватель одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="a8781-381">Update Listener by either:</span></span>
  * <span data-ttu-id="a8781-382">Получение группы AlwaysOn hello вне сети и обновление hello всегда в прослушиватель, с новой ILB / ELB IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a8781-382">Taking hello Always On Group offline and updating hello Always On Listener with new ILB / ELB IP address.</span></span>
  * <span data-ttu-id="a8781-383">Или добавление hello ресурс IP-адреса из новой облачной службы ILB/ELB через PowerShell в кластеризации Windows.</span><span class="sxs-lookup"><span data-stu-id="a8781-383">Or adding hello IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span></span> <span data-ttu-id="a8781-384">Затем набор hello возможных владельцев ресурса toohello hello IP-адрес узла, SQL2 миграцию и настроить его как или зависимость в hello сетевое имя.</span><span class="sxs-lookup"><span data-stu-id="a8781-384">Then set hello Possible owners of hello IP Address resource toohello migrated node, SQL2, and set this as OR dependency in hello Network Name.</span></span> <span data-ttu-id="a8781-385">Обратитесь к разделу «Добавление ресурса IP-адреса в одной подсети» hello hello [приложение](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="a8781-385">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
* <span data-ttu-id="a8781-386">Проверка DNS-клиенты toohello конфигурации и распространение.</span><span class="sxs-lookup"><span data-stu-id="a8781-386">Check DNS configuration/propogation toohello clients.</span></span>
* <span data-ttu-id="a8781-387">Перенесите виртуальную машину SQL1 и выполните шаги 2—4.</span><span class="sxs-lookup"><span data-stu-id="a8781-387">Migrate SQL1 VM, and go through steps 2 – 4.</span></span>
* <span data-ttu-id="a8781-388">При использовании 5ii действия, затем добавьте SQL1 как возможного владельца для hello добавить ресурс IP-адреса</span><span class="sxs-lookup"><span data-stu-id="a8781-388">If using steps 5ii, then add SQL1 as a Possible Owner for hello added IP Address Resource</span></span>
* <span data-ttu-id="a8781-389">Проверьте отработку отказа.</span><span class="sxs-lookup"><span data-stu-id="a8781-389">Test failovers.</span></span>

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a><span data-ttu-id="a8781-390">2) Использование существующей вторичной реплики (реплик): несколько узлов</span><span class="sxs-lookup"><span data-stu-id="a8781-390">2. Utilize existing secondary replica(s): Multi-Site</span></span>
<span data-ttu-id="a8781-391">При наличии узлов в более одного центра обработки данных Azure (DC), или у вас гибридная среда, можно использовать конфигурации Always On в это время простоя toominimize среды.</span><span class="sxs-lookup"><span data-stu-id="a8781-391">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment toominimize downtime.</span></span>

<span data-ttu-id="a8781-392">Hello подход является toochange hello Always On синхронизации tooSynchronous hello в локальной или дополнительный контроллер домена в Azure, а затем перехода на другой ресурс по toothat SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8781-392">hello approach is toochange hello Always On synchronization tooSynchronous for hello on-premises or secondary Azure DC, and then failover over toothat SQL Server.</span></span> <span data-ttu-id="a8781-393">Затем скопируйте VHD hello tooa учетной записи хранения Premium и повторного развертывания hello машины в новой облачной службы.</span><span class="sxs-lookup"><span data-stu-id="a8781-393">Then copy hello VHDs tooa Premium Storage account, and redeploy hello machine into a new cloud service.</span></span> <span data-ttu-id="a8781-394">Обновите прослушивателя hello и затем восстановить после сбоя.</span><span class="sxs-lookup"><span data-stu-id="a8781-394">Update hello listener, and then fail back.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="a8781-395">Точки простоя</span><span class="sxs-lookup"><span data-stu-id="a8781-395">Points of downtime</span></span>
<span data-ttu-id="a8781-396">время простоя Hello состоит из hello время toofailover toohello альтернативой контроллера домена и обратно.</span><span class="sxs-lookup"><span data-stu-id="a8781-396">hello downtime consists of hello time toofailover toohello alternative DC and back.</span></span> <span data-ttu-id="a8781-397">Время простоя также зависит от конфигурации клиента/DNS: повторное подключение вашего клиента может задерживаться.</span><span class="sxs-lookup"><span data-stu-id="a8781-397">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span></span>
<span data-ttu-id="a8781-398">Рассмотрим следующий пример конфигурации AlwaysOn в гибридной hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-398">Consider hello following example of a hybrid Always On configuration:</span></span>

![MultiSite1][9]

##### <a name="advantages"></a><span data-ttu-id="a8781-400">Преимущества</span><span class="sxs-lookup"><span data-stu-id="a8781-400">Advantages</span></span>
* <span data-ttu-id="a8781-401">Можно использовать существующую инфраструктуру.</span><span class="sxs-lookup"><span data-stu-id="a8781-401">You can utilize existing infrastructure.</span></span>
* <span data-ttu-id="a8781-402">У вас есть hello параметр обновления toopre hello хранилища Azure hello DC аварийного восстановления Azure сначала.</span><span class="sxs-lookup"><span data-stu-id="a8781-402">You have hello option toopre-upgrade hello Azure storage on hello DR Azure DC first.</span></span>
* <span data-ttu-id="a8781-403">можно перенастроить Hello хранилища Azure для аварийного восстановления контроллера домена.</span><span class="sxs-lookup"><span data-stu-id="a8781-403">hello DR Azure DC storage can be reconfigured.</span></span>
* <span data-ttu-id="a8781-404">Во время миграции выполняются как минимум два перехода на другой ресурс, не считая тестовых переходов.</span><span class="sxs-lookup"><span data-stu-id="a8781-404">There is a minimum of two failovers during migration, excluding test failovers.</span></span>
* <span data-ttu-id="a8781-405">Не требуется toomove данных SQL Server с помощью резервного копирования и восстановления.</span><span class="sxs-lookup"><span data-stu-id="a8781-405">You do not need toomove SQL Server data with backup and restore.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="a8781-406">Недостатки</span><span class="sxs-lookup"><span data-stu-id="a8781-406">Disadvantages</span></span>
* <span data-ttu-id="a8781-407">В зависимости от tooSQL доступа клиента сервер может возникнуть увеличивают задержку при в приложении toohello альтернативный контроллер домена работает SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8781-407">Depending on client access tooSQL Server, there might be increased latency when SQL Server is running in an alternative DC toohello application.</span></span>
* <span data-ttu-id="a8781-408">может занять длительное время копирования Hello tooPremium хранилища виртуальных жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="a8781-408">hello copy time of VHDs tooPremium storage could be long.</span></span> <span data-ttu-id="a8781-409">Это может повлиять на решение о ли tookeep hello узел в hello группы доступности.</span><span class="sxs-lookup"><span data-stu-id="a8781-409">This might affect your decision on whether tookeep hello node in hello Availability Group.</span></span> <span data-ttu-id="a8781-410">Следует считать это когда журнала вычислительных операций, выполняемых загружает во время миграции hello фактором является обязательным, поскольку hello первичного узла будет иметь tookeep hello нереплицированные транзакции в журнале транзакций.</span><span class="sxs-lookup"><span data-stu-id="a8781-410">Consider this for when log intensive work loads are running during hello migration is required, since hello Primary node will have tookeep hello unreplicated transactions in its transaction log.</span></span> <span data-ttu-id="a8781-411">Это может привести к значительному увеличению размера журнала.</span><span class="sxs-lookup"><span data-stu-id="a8781-411">Therefore this could grow significantly.</span></span>
* <span data-ttu-id="a8781-412">Этот сценарий будет использовать hello Azure **AzureStorageBlobCopy начала** командлет, который является асинхронным.</span><span class="sxs-lookup"><span data-stu-id="a8781-412">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="a8781-413">Соглашение об уровне обслуживания после завершения отсутствует.</span><span class="sxs-lookup"><span data-stu-id="a8781-413">There is no SLA on completion.</span></span> <span data-ttu-id="a8781-414">Hello время hello копий зависит, тогда это зависит от ожидания в очереди, он также зависит от объема hello tootransfer данных.</span><span class="sxs-lookup"><span data-stu-id="a8781-414">hello time of hello copies varies, while this depends on wait in queue, it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="a8781-415">Таким образом, достаточно одного узла в 2-й центре обработки данных, в случае, если копия hello требуется больше времени, чем при тестировании необходимо принять меры по устранению рисков.</span><span class="sxs-lookup"><span data-stu-id="a8781-415">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="a8781-416">Сюда могут входить следующие идеи hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-416">This could include hello following ideas.</span></span>
  * <span data-ttu-id="a8781-417">Добавьте временный второй узел SQL для обеспечения высокой ДОСТУПНОСТИ перед миграцией hello согласованный простоев.</span><span class="sxs-lookup"><span data-stu-id="a8781-417">Add a temporary 2nd SQL node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="a8781-418">Выполните миграцию hello за пределами Azure запланированного обслуживания.</span><span class="sxs-lookup"><span data-stu-id="a8781-418">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="a8781-419">Убедиться, что кворум кластера настроен правильно.</span><span class="sxs-lookup"><span data-stu-id="a8781-419">Ensure you have configured your cluster quorum correctly.</span></span>

<span data-ttu-id="a8781-420">Этот сценарий предполагает документированы установки и знать, как hello хранения сопоставляется в порядке toomake изменения параметров кэша оптимальной диска.</span><span class="sxs-lookup"><span data-stu-id="a8781-420">This scenario assumes that you have documented your install and know how hello storage is mapped in order toomake changes for optimal disk cache settings.</span></span>

##### <a name="high-level-steps"></a><span data-ttu-id="a8781-421">Пошаговые действия</span><span class="sxs-lookup"><span data-stu-id="a8781-421">High-level steps</span></span>
![Multisite2][10]

* <span data-ttu-id="a8781-423">Делает hello локальной / альтернативные hello Azure контроллер домена первичного сервера SQL и сделать его hello других автоматического перехода на другой ресурс партнера (AFP).</span><span class="sxs-lookup"><span data-stu-id="a8781-423">Make hello on-premises / alternate Azure DC hello SQL Server Primary, and make it hello other Auto Failover Partner (AFP).</span></span>
* <span data-ttu-id="a8781-424">Сбор данных о конфигурации дисков SQL2 и удалить узел hello (не удаляйте подключенных виртуальных жестких дисков).</span><span class="sxs-lookup"><span data-stu-id="a8781-424">Gather disk configuration information from SQL2, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="a8781-425">Создайте учетную запись хранения Premium и скопируйте виртуальные жесткие диски из hello Стандартная учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="a8781-425">Create a Premium Storage account and copy VHDs from hello Standard Storage account.</span></span>
* <span data-ttu-id="a8781-426">Создать новую облачную службу и создайте hello SQL2 ВМ с его дисков хранилища вознаграждения.</span><span class="sxs-lookup"><span data-stu-id="a8781-426">Create a new cloud service and create hello SQL2 VM with its Premiums Storage disks attached.</span></span>
* <span data-ttu-id="a8781-427">Настройте ILB/ELB и добавьте конечные точки.</span><span class="sxs-lookup"><span data-stu-id="a8781-427">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="a8781-428">Обновление hello всегда в прослушиватель, с новой ILB / ELB IP адрес и тестирования перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="a8781-428">Update hello Always On Listener with new ILB / ELB IP address and test failover.</span></span>
* <span data-ttu-id="a8781-429">Проверьте конфигурацию DNS hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-429">Check hello DNS configuration.</span></span>
* <span data-ttu-id="a8781-430">Изменить AFP tooSQL2 hello и перенести SQL1 и выполните шаги 2 – 5.</span><span class="sxs-lookup"><span data-stu-id="a8781-430">Change hello AFP tooSQL2, and then migrate SQL1 and go through steps 2 – 5.</span></span>
* <span data-ttu-id="a8781-431">Проверьте отработку отказа.</span><span class="sxs-lookup"><span data-stu-id="a8781-431">Test failovers.</span></span>
* <span data-ttu-id="a8781-432">Перейдите назад tooSQL1 hello AFP и SQL2</span><span class="sxs-lookup"><span data-stu-id="a8781-432">Switch hello AFP back tooSQL1 and SQL2</span></span>

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a><span data-ttu-id="a8781-433">Приложение: Миграция tooPremium многосайтового всегда на кластера хранилища</span><span class="sxs-lookup"><span data-stu-id="a8781-433">Appendix: Migrating a Multisite Always On Cluster tooPremium Storage</span></span>
<span data-ttu-id="a8781-434">Hello оставшейся части этого раздела предоставляет подробный пример преобразования с несколькими сайтами Always On tooPremium хранения данных кластера.</span><span class="sxs-lookup"><span data-stu-id="a8781-434">hello remainder of this topic provides a detailed example of converting a multi-site Always On cluster tooPremium storage.</span></span> <span data-ttu-id="a8781-435">Также преобразует hello прослушивателя с помощью балансировки нагрузки внутренней tooan подсистемы балансировки нагрузки (ILB).</span><span class="sxs-lookup"><span data-stu-id="a8781-435">It also converts hello Listener from using an external load balancer (ELB) tooan internal load balancer (ILB).</span></span>

### <a name="environment"></a><span data-ttu-id="a8781-436">Среда</span><span class="sxs-lookup"><span data-stu-id="a8781-436">Environment</span></span>
* <span data-ttu-id="a8781-437">Windows 2k12 / SQL 2k12</span><span class="sxs-lookup"><span data-stu-id="a8781-437">Windows 2k12 / SQL 2k12</span></span>
* <span data-ttu-id="a8781-438">1 файл БД на SP </span><span class="sxs-lookup"><span data-stu-id="a8781-438">1 DB Files on SP</span></span>
* <span data-ttu-id="a8781-439">2 x пулы носителей на каждом узле</span><span class="sxs-lookup"><span data-stu-id="a8781-439">2 x Storage Pools per Node</span></span>

![Приложение1][11]

### <a name="vm"></a><span data-ttu-id="a8781-441">ВМ:</span><span class="sxs-lookup"><span data-stu-id="a8781-441">VM:</span></span>
<span data-ttu-id="a8781-442">В этом примере мы будем toodemonstrate переход от tooILB ELB.</span><span class="sxs-lookup"><span data-stu-id="a8781-442">In this example we are going toodemonstrate moving from an ELB tooILB.</span></span> <span data-ttu-id="a8781-443">ELB обладал перед ILB, поэтому в следующем примере показано, как toothis tooswitch во время hello миграции.</span><span class="sxs-lookup"><span data-stu-id="a8781-443">ELB was available before ILB, so this shows how tooswitch toothis during hello migration.</span></span>

![Приложение2][12]

### <a name="pre-steps-connect-toosubscription"></a><span data-ttu-id="a8781-445">Действия по предварительной подключения tooSubscription</span><span class="sxs-lookup"><span data-stu-id="a8781-445">Pre Steps: Connect tooSubscription</span></span>
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a><span data-ttu-id="a8781-446">Шаг 1. Создайте новую учетную запись хранения и облачную службу</span><span class="sxs-lookup"><span data-stu-id="a8781-446">Step 1: Create New Storage Account and Cloud Service</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where hello vm toomigrate resides
    $origstorageaccountname = "danstdams"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Generate storage keys for later
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Generate storage acc contexts
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $xioContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $origstorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #CREATE NEW CLOUD SVC
    $vnet = "dansvnetwesteur"

    ##Existing cloud service
    $sourceSvc="dansolSrcAms"

    ##Create new cloud service
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a><span data-ttu-id="a8781-447">Шаг 2: Увеличьте hello разрешенных ошибок на ресурсы<Optional></span><span class="sxs-lookup"><span data-stu-id="a8781-447">Step 2: Increase hello permitted failures on resources <Optional></span></span>
<span data-ttu-id="a8781-448">На некоторые ресурсы, принадлежащие tooyour группы доступности AlwaysOn существуют ограничения на количество сбоев, которые могут возникнуть в течение которых служба кластеров hello попытается группы ресурсов toorestart hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-448">On certain resources that belong tooyour Always On Availability Group there are limits on how many failures that can occur in a period, where hello cluster service will attempt toorestart hello resource group.</span></span> <span data-ttu-id="a8781-449">Рекомендуется хотя проходу с этой процедурой, так как при отсутствии вручную отработки отказа перехода на другой ресурс и триггер, завершение работы компьютеров может получить ограничения закрыть toothis увеличить.</span><span class="sxs-lookup"><span data-stu-id="a8781-449">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close toothis limit.</span></span>

<span data-ttu-id="a8781-450">Она бы быть hello сбоя оправданным toodouble скидка, toodo это в диспетчере отказоустойчивости кластеров, go toohello свойства hello Always On группы ресурсов:</span><span class="sxs-lookup"><span data-stu-id="a8781-450">It would be prudent toodouble hello failure allowance, toodo this in Failover Cluster Manager, go toohello Properties of hello Always On resource group:</span></span>

![Приложение3][13]

<span data-ttu-id="a8781-452">Измените hello too6 максимум сбоев.</span><span class="sxs-lookup"><span data-stu-id="a8781-452">Change hello Maximum Failures too6.</span></span>

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a><span data-ttu-id="a8781-453">Шаг 3. Добавление ресурса IP-адреса для группы кластера <Optional></span><span class="sxs-lookup"><span data-stu-id="a8781-453">Step 3: Addition IP Address resource for Cluster Group <Optional></span></span>
<span data-ttu-id="a8781-454">Если у вас есть только один IP-адрес для hello группы кластера и подсети выровненных toohello облака, учтите, что, если вы случайно перевод в автономный режим все узлы кластера в облаке hello что сети затем hello IP-ресурс кластера и сетевое имя кластера не будет возможности toocome Онлайн.</span><span class="sxs-lookup"><span data-stu-id="a8781-454">If you have only one IP address for hello Cluster Group and this is aligned toohello cloud subnet, beware, if you accidentally take offline all cluster nodes in hello cloud on that network then hello Cluster IP resource and Cluster Network Name will not be able toocome online.</span></span> <span data-ttu-id="a8781-455">В hello события объекта, это приведет к тому обновляет tooother ресурсы кластера.</span><span class="sxs-lookup"><span data-stu-id="a8781-455">In hello event of this it will prevent updates tooother cluster resources.</span></span>

#### <a name="step-4-dns-configuration"></a><span data-ttu-id="a8781-456">Шаг 4. Настройка DNS</span><span class="sxs-lookup"><span data-stu-id="a8781-456">Step 4: DNS configuration</span></span>
<span data-ttu-id="a8781-457">плавный переход зависит от того, каким образом производится DNS tooimplement загруженные и обновлены.</span><span class="sxs-lookup"><span data-stu-id="a8781-457">tooimplement a smooth transition depends on how DNS is being utilized and updated.</span></span>
<span data-ttu-id="a8781-458">При установке Always On, он создает группу ресурсов кластера Windows, при открытии диспетчера отказоустойчивости кластеров, вы увидите, как минимум, он будет иметь три ресурса, hello два hello документа относится tooare:</span><span class="sxs-lookup"><span data-stu-id="a8781-458">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you will see that at a minimum it will have three resources, hello two that hello document refers tooare:</span></span>

* <span data-ttu-id="a8781-459">Имя виртуальной сети (VNN) — это hello DNS-имя, клиент подключения toowhen Желательное tooconnect tooSQL серверах с помощью Always On.</span><span class="sxs-lookup"><span data-stu-id="a8781-459">Virtual Network Name (VNN) – This is hello DNS name that client connect toowhen wanting tooconnect tooSQL Servers via Always On.</span></span>
* <span data-ttu-id="a8781-460">Ресурс IP-адреса — это IP-адрес, связанный с виртуальной сети hello hello и может иметь несколько в многосайтовой конфигурации будет иметь IP-адрес каждого сайта и подсеть.</span><span class="sxs-lookup"><span data-stu-id="a8781-460">IP Address Resource – This is hello IP address that associated with hello VNN, you can have more than one, and in a multisite configuration you will have an IP address per site/subnet.</span></span>

<span data-ttu-id="a8781-461">При подключении tooSQL Server, драйвер SQL Server Client hello будет извлечь hello записей DNS, связанных с прослушивателем hello и повторите tooconnect tooeach всегда на связанные IP-адрес, ниже обсуждаются некоторые факторы, которые могут повлиять на это.</span><span class="sxs-lookup"><span data-stu-id="a8781-461">When connecting tooSQL Server, hello SQL Server Client driver will retrieve hello DNS records associated with hello listener and try tooconnect tooeach Always On associated IP address, below we discuss some factors that can influence this.</span></span>

<span data-ttu-id="a8781-462">Hello число параллельных записей DNS, которые связаны с именем прослушивателя hello зависит не только от hello число связанных IP-адреса, но hello "RegisterAllIpProviders'setting в отказоустойчивой кластеризации для hello ресурсов всегда ON имя виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a8781-462">hello number of concurrent DNS records that are associated with hello listener name depends not only on hello number of IP addresses associated, but hello ‘RegisterAllIpProviders’setting in Failover Clustering for hello Always ON VNN resource.</span></span>

<span data-ttu-id="a8781-463">При развертывании Always On в Azure hello toocreate различных этапов прослушивателя и IP-адресов, у вас есть toomanually Настройка too1 «RegisterAllIpProviders» hello, это разные tooan локального Always On развертывания где оно уже установлено too1.</span><span class="sxs-lookup"><span data-stu-id="a8781-463">When you deploy Always On in Azure there are different steps toocreate hello Listener and IP Addresses, you have toomanually configure hello ‘RegisterAllIpProviders’ too1, this is different tooan on-premises Always On deployment where it is already set too1.</span></span>

<span data-ttu-id="a8781-464">Если «RegisterAllIpProviders» равно 0, то вы увидите только в DNS запись DNS, связанную с hello прослушиватель:</span><span class="sxs-lookup"><span data-stu-id="a8781-464">If ‘RegisterAllIpProviders’ is 0, then you will only see one DNS record in DNS associated with hello Listener:</span></span>

![Приложение4][14]

<span data-ttu-id="a8781-466">Если RegisterAllIpProviders равен 1:</span><span class="sxs-lookup"><span data-stu-id="a8781-466">If ‘RegisterAllIpProviders’ is 1:</span></span>

![Приложение5][15]

<span data-ttu-id="a8781-468">Приведенный ниже код Hello будет дампа out hello параметры виртуальной сети и установите ее, выполните Примечание для hello изменения tootake эффекта, вам потребуется tootake hello VNN автономный режим и включить его обратно в оперативный режим, этот ведения hello прослушивателя вне сети может вызвать клиент подключения перебоев в работе.</span><span class="sxs-lookup"><span data-stu-id="a8781-468">hello code below will dump out hello VNN settings and set it for you, please note, for hello change tootake effect you will need tootake hello VNN offline and turn it back online, this taking hello Listener offline causing client connectivity disruption.</span></span>

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

<span data-ttu-id="a8781-469">На более позднем этапе миграции необходимо будет tooupdate hello Always On прослушиватель с обновление IP-адреса, который будет ссылаться на подсистему балансировки нагрузки, это будет включать в себя удаление IP-адрес ресурса и добавление.</span><span class="sxs-lookup"><span data-stu-id="a8781-469">In a later migration step you will need tooupdate hello Always On listener with an updated IP address that will reference a load balancer, this will involve an IP Address resource removal and addition.</span></span> <span data-ttu-id="a8781-470">После обновления hello IP необходимо tooensure hello новый IP-адрес уже был обновлен в зоне DNS, и что hello клиенты обновляют их локального кэша DNS.</span><span class="sxs-lookup"><span data-stu-id="a8781-470">After hello IP update, you need tooensure hello new IP address has been updated in DNS Zone and that hello clients are updating their local DNS cache.</span></span>

<span data-ttu-id="a8781-471">Если клиенты находятся в разных сегментах и ссылаться на другой DNS-сервер, необходимо tooconsider как обстоят дела передачи зоны DNS в ходе миграции hello как hello приложение подключиться будет ограничен времени, по крайней мере hello время передачи зоны все новые IP-адресов для прослушивателя hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-471">If your clients reside in a different network segment and reference a different DNS server, you need tooconsider what happens about DNS Zone Transfer during hello migration, as hello application reconnect time will be constrained by at least hello Zone Transfer Time of any new IP addresses for hello listener.</span></span> <span data-ttu-id="a8781-472">Находясь в рамках здесь ограничения времени, следует обсудить и проверить принудительное Добавочная архивация с помощью команд Windows, а также поместить hello DNS tooa записей узла снизить время tooLive (TTL), чтобы обновлять клиенты hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-472">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put hello DNS host record tooa lower Time tooLive (TTL), so hello clients update.</span></span> <span data-ttu-id="a8781-473">Дополнительные сведения см. в статье [Добавочные передачи зоны](https://technet.microsoft.com/library/cc958973.aspx) и [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8781-473">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span></span>

<span data-ttu-id="a8781-474">По умолчанию hello срок ЖИЗНИ для записи DNS, которая связана с hello прослушивателя в Always On в Azure составляет 1200 секунд.</span><span class="sxs-lookup"><span data-stu-id="a8781-474">By default hello TTL for DNS Record that is associated with hello Listener in Always On in Azure is 1200 seconds.</span></span> <span data-ttu-id="a8781-475">Вы можете tooreduce это при работе в рамках ограничения времени во время обновления клиентов миграции tooensure hello их DNS с hello обновить IP-адрес для прослушивателя hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-475">You may wish tooreduce this if you are under time constraint during your migration tooensure hello clients update their DNS with hello updated IP address for hello listener.</span></span> <span data-ttu-id="a8781-476">Можно просматривать и изменить конфигурацию hello записи конфигурации hello объекта hello виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="a8781-476">You can see and modify hello configuration by dumping out hello configuration of hello VNN:</span></span>

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

<span data-ttu-id="a8781-477">Обратите внимание, нижний hello hello «HostRecordTTL» будет выполняться большего объема трафика DNS.</span><span class="sxs-lookup"><span data-stu-id="a8781-477">Please note, hello lower hello ‘HostRecordTTL’, a higher amount of DNS traffic will occur.</span></span>

##### <a name="client-application-settings"></a><span data-ttu-id="a8781-478">Параметры клиентского приложения</span><span class="sxs-lookup"><span data-stu-id="a8781-478">Client application settings</span></span>
<span data-ttu-id="a8781-479">Если Здравствуйте, поддерживаемых приложением SQL клиента .net 4.5 SQLClient, то можно использовать "MULTISUBNETFAILOVER = TRUE" ключевое слово, рекомендуется применять, так как она позволяет быстрее tooSQL соединения группы доступности AlwaysOn во время отработки отказа toobe.</span><span class="sxs-lookup"><span data-stu-id="a8781-479">If your SQL client application supports hello .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword, this is recommended toobe applied as it allows for faster connection tooSQL Always On Availability Group during failover.</span></span> <span data-ttu-id="a8781-480">Перечисление всех IP-адресов, связанных с hello Always On прослушивателя в параллельном режиме и выполняется более интенсивная скорости повтора подключения TCP во время отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="a8781-480">It enumerates through all IP addresses associated with hello Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span></span>

<span data-ttu-id="a8781-481">Дополнительные сведения о hello параметры, приведенные выше, см. в разделе [MultiSubnetFailover ключевое слово и связанные компоненты](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span><span class="sxs-lookup"><span data-stu-id="a8781-481">For more information regarding hello settings above, please see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span></span> <span data-ttu-id="a8781-482">Ознакомьтесь также со статьей [Поддержка SqlClient для высокого уровня доступности и аварийного восстановления](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="a8781-482">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span></span>

#### <a name="step-5-cluster-quorum-settings"></a><span data-ttu-id="a8781-483">Шаг 5. Параметры кворума кластера</span><span class="sxs-lookup"><span data-stu-id="a8781-483">Step 5: Cluster quorum settings</span></span>
<span data-ttu-id="a8781-484">Как будет toobe снятия хотя бы один сервер SQL вниз одновременно, следует изменять приветствия кворума кластера, при 2 узлов с помощью файла общей папке следящего сервера (FSW), следует задать большинство узлов tooallow кворума hello и использовать динамические голосования, и это tooallow для постоянные tooremain один узел.</span><span class="sxs-lookup"><span data-stu-id="a8781-484">As you are going toobe taking out at least one SQL Server down at a time, you should modify hello cluster quorum setting, if using File Share Witness (FSW) with 2 nodes, you should set hello quorum tooallow node majority and utilize dynamic voting, and this is tooallow for a single node tooremain standing.</span></span>

    Set-ClusterQuorum -NodeMajority  

<span data-ttu-id="a8781-485">Дополнительные сведения об управлении и настройке кворума кластера hello см. в разделе [Здравствуйте кворума в отказоустойчивом кластере Windows Server 2012, настройке и управлении](https://technet.microsoft.com/library/jj612870.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8781-485">For more information on managing and configuring hello cluster quorum, please see [Configure and Manage hello Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span></span>

#### <a name="step-6-extract-existing-endpoints-and-acls"></a><span data-ttu-id="a8781-486">Шаг 6. Извлеките существующие конечные точки и списки управления доступом</span><span class="sxs-lookup"><span data-stu-id="a8781-486">Step 6: Extract Existing Endpoints and ACLs</span></span>
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

<span data-ttu-id="a8781-487">Сохраните эти tooa текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="a8781-487">Save these tooa text file.</span></span>

#### <a name="step-7-change-failover-partners-and-replication-modes"></a><span data-ttu-id="a8781-488">Шаг 7. Измените партнеров перехода на другой ресурс и режимы репликации</span><span class="sxs-lookup"><span data-stu-id="a8781-488">Step 7: Change Failover Partners and Replication Modes</span></span>
<span data-ttu-id="a8781-489">При наличии более чем 2 серверами SQL можно следует изменить hello отработки отказа другой базы данных-получателя в другой контроллер домена или локальной too'Synchronous и сделать ее автоматического участника отработки отказа (AFP), поэтому поддержания высокого уровня ДОСТУПНОСТИ в процессе внесения изменений.</span><span class="sxs-lookup"><span data-stu-id="a8781-489">If you have more than 2 SQL Servers, you should change hello failover of another secondary in another DC or on-premises too‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span></span> <span data-ttu-id="a8781-490">Это можно сделать через TSQL или изменить при помощи SSMS:</span><span class="sxs-lookup"><span data-stu-id="a8781-490">You can do this through TSQL of modify though SSMS:</span></span>

![Приложение6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a><span data-ttu-id="a8781-492">Шаг 8. Удалите дополнительную виртуальную машину из облачной службы</span><span class="sxs-lookup"><span data-stu-id="a8781-492">Step 8: Remove Secondary VM from cloud service</span></span>
<span data-ttu-id="a8781-493">Следует планирования toomigrate дополнительного узла облака во-первых, если в данный момент первичной, необходимо запустить отработку отказа вручную.</span><span class="sxs-lookup"><span data-stu-id="a8781-493">You should be planning toomigrate a cloud secondary node first, if this is currently primary, you should initiate a manual failover.</span></span>

    $vmNameToMigrate="dansqlams2"

    #Check machine status
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Shutdown secondary VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM


    #Extract disk configuration

    ##Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk config, make sure below returns hello disks associated with hello VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="a8781-494">Шаг 9. Измените параметры кэширования диска в файле CSV и сохраните</span><span class="sxs-lookup"><span data-stu-id="a8781-494">Step 9: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="a8781-495">Для томов с данными они должны устанавливаться tooREADONLY.</span><span class="sxs-lookup"><span data-stu-id="a8781-495">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="a8781-496">Для тома журнала Отслеживания этих должно быть равно tooNONE.</span><span class="sxs-lookup"><span data-stu-id="a8781-496">For TLOG volumes these should be set tooNONE.</span></span>

![Приложение7][17]

#### <a name="step-10-copy-vhds"></a><span data-ttu-id="a8781-498">Шаг 10. Скопируйте виртуальные жесткие диски</span><span class="sxs-lookup"><span data-stu-id="a8781-498">Step 10: Copy VHDS</span></span>
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname.blob.core.windows.net/vhds/$vhdname" `
    -SrcContext $origContext `
    -DestContainer $containerName `
    -DestBlob $vhdname `
    -DestContext $xioContext
       }



<span data-ttu-id="a8781-499">Можно проверить состояние копирования hello toohello VHD hello учетной записи хранения Premium:</span><span class="sxs-lookup"><span data-stu-id="a8781-499">You can check hello copy status of hello VHDs toohello Premium Storage account:</span></span>

    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContext
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Приложение8][18]

<span data-ttu-id="a8781-501">Подождите, пока все они будут успешно сохранены.</span><span class="sxs-lookup"><span data-stu-id="a8781-501">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="a8781-502">Информация об отдельных больших двоичных объектах.</span><span class="sxs-lookup"><span data-stu-id="a8781-502">For information for individual blobs:</span></span>

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a><span data-ttu-id="a8781-503">Шаг 11. Зарегистрируйте диск ОС</span><span class="sxs-lookup"><span data-stu-id="a8781-503">Step 11: Register OS disk</span></span>
    #Change storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

#### <a name="step-12-import-secondary-into-new-cloud-service"></a><span data-ttu-id="a8781-504">Шаг 12. Импортируйте вторичную реплику в новую облачную службу</span><span class="sxs-lookup"><span data-stu-id="a8781-504">Step 12: Import secondary into new cloud service</span></span>
<span data-ttu-id="a8781-505">Hello кода ниже также использует hello добавлен параметр здесь вы можете импортировать машины hello и использовать hello retainable виртуальных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="a8781-505">hello code below also uses hello added option here you can import hello machine and use hello retainable VIP.</span></span>

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember toochange tooXIO
    $newInstanceSize = "Standard_DS13"
    $subnet = "SQL"

    #Create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###Attaching disks tooa VM during a deploy tooa new cloud service and new storage account is different from just attaching VHDs toojust a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="a8781-506">Шаг 13. Создайте ILB в новой облачной службе, добавьте конечные точки с балансировкой нагрузки и списки управления доступом</span><span class="sxs-lookup"><span data-stu-id="a8781-506">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span></span>
    #Check for existing ILB
    GET-AzureInternalLoadBalancer -ServiceName $destcloudsvc

    $ilb="sqlIntIlbDest"
    $subnet = "SQL"
    $IP="192.168.0.25"
    Add-AzureInternalLoadBalancer -ServiceName $destcloudsvc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP

    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM

    #SET Azure ACLs or Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

    ####WAIT FOR FULL AlwaysOn RESYNCRONISATION!!!!!!!!!#####

#### <a name="step-14-update-always-on"></a><span data-ttu-id="a8781-507">Шаг 14. Обновите AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="a8781-507">Step 14: Update Always On</span></span>
    #Code toobe executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # hello azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency tooListener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Приложение9][19]

<span data-ttu-id="a8781-509">Теперь можно Удалите старые облачную службу hello IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a8781-509">Now remove hello old cloud service IP Address.</span></span>

![Приложение10][20]

#### <a name="step-15-dns-update-check"></a><span data-ttu-id="a8781-511">Шаг 15. Проверка обновлений DNS</span><span class="sxs-lookup"><span data-stu-id="a8781-511">Step 15: DNS update check</span></span>
<span data-ttu-id="a8781-512">Теперь необходимо проверить DNS-серверов в сети клиента SQL Server и убедитесь, что кластеризации добавил hello запись дополнительный узел для hello добавить IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a8781-512">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added hello extra host record for hello added IP address.</span></span> <span data-ttu-id="a8781-513">Если эти DNS-серверы не обновлялись, можно воспользоваться режимом вынужденного передачи зоны DNS и убедитесь, что hello клиентов в подсети отсутствует, может tooresolve tooboth всегда на IP-адреса, поэтому нет необходимости toowait для автоматической репликации DNS.</span><span class="sxs-lookup"><span data-stu-id="a8781-513">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that hello clients in there subnet are able tooresolve tooboth Always On IP Addresses, this is so you do not need toowait for automatic DNS replication.</span></span>

#### <a name="step-16-reconfigure-always-on"></a><span data-ttu-id="a8781-514">Шаг 16. Перенастройте AlwaysOn </span><span class="sxs-lookup"><span data-stu-id="a8781-514">Step 16: Reconfigure Always On</span></span>
<span data-ttu-id="a8781-515">На этом этапе дождитесь hello получателей, этот узел, который был перенесенных toofully повторную синхронизацию с локальным узлом hello и переключение toosynchronous узел репликации и сделать его hello AFP.</span><span class="sxs-lookup"><span data-stu-id="a8781-515">At this point you wait for hello secondary that node that was migrated toofully resynchronize with hello on-premises node and switch toosynchronous replication node and make it hello AFP.</span></span>  

#### <a name="step-17-migrate-second-node"></a><span data-ttu-id="a8781-516">Шаг 17. Перенесите второй узел</span><span class="sxs-lookup"><span data-stu-id="a8781-516">Step 17: Migrate second node</span></span>
    $vmNameToMigrate="dansqlams1"

    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Get endpoint information
    $endpoint = Get-AzureVM -ServiceName $sourceSvc  -Name $vmNameToMigrate | Get-AzureEndpoint

    #Shutdown VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM

    #Get disk config

    #Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk configuration
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machine is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="a8781-517">Шаг 18. Измените параметры кэширования диска в файле CSV и сохраните</span><span class="sxs-lookup"><span data-stu-id="a8781-517">Step 18: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="a8781-518">Для томов с данными они должны устанавливаться tooREADONLY.</span><span class="sxs-lookup"><span data-stu-id="a8781-518">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="a8781-519">Для тома журнала Отслеживания этих должно быть равно tooNONE.</span><span class="sxs-lookup"><span data-stu-id="a8781-519">For TLOG volumes these should be set tooNONE.</span></span>

![Приложение11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a><span data-ttu-id="a8781-521">Шаг 19. Создайте новую независимую учетную запись хранения для дополнительного узла</span><span class="sxs-lookup"><span data-stu-id="a8781-521">Step 19: Create New Independent Storage Account for Secondary Node</span></span>
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset hello storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a><span data-ttu-id="a8781-522">Шаг 20. Скопируйте виртуальные жесткие диски</span><span class="sxs-lookup"><span data-stu-id="a8781-522">Step 20: Copy VHDS</span></span>
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname2nd.blob.core.windows.net/vhds/$vhdname" `
        -SrcContext $origContext `
        -DestContainer $containerName `
        -DestBlob $vhdname `
        -DestContext $xioContextnode2
       }

    #Check for copy progress

    #check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContext


<span data-ttu-id="a8781-523">Можно проверить состояние копирования hello виртуального жесткого диска для всех виртуальных жестких дисков: ForEach ($disk в $diskobjects) {$lun = $disk. LUN $vhdname = $disk.vhdname $cacheoption = $disk. HostCaching $disklabel = $disk. DiskLabel $diskName = $disk. DiskName</span><span class="sxs-lookup"><span data-stu-id="a8781-523">You can check hello VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span></span>

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Приложение12][22]

<span data-ttu-id="a8781-525">Подождите, пока все они будут успешно сохранены.</span><span class="sxs-lookup"><span data-stu-id="a8781-525">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="a8781-526">Информация об отдельных больших двоичных объектах.</span><span class="sxs-lookup"><span data-stu-id="a8781-526">For information for individual blobs:</span></span>

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a><span data-ttu-id="a8781-527">Шаг 21. Зарегистрируйте диск ОС</span><span class="sxs-lookup"><span data-stu-id="a8781-527">Step 21: Register OS disk</span></span>
    #change storage account toohello new XIO storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

    #Build VM Config
    $ipaddr = "192.168.0.4"
    $newInstanceSize = "Standard_DS13"

    #Join tooexisting Avaiability Set

    #Build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###This is different toojust a straight cloud service change
    #note if you do not have a disk label hello command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="a8781-528">Шаг 22. Добавьте конечные точки с балансировкой нагрузки и списки управления доступом</span><span class="sxs-lookup"><span data-stu-id="a8781-528">Step 22: Add Load Balanced Endpoints and ACLs</span></span>
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a><span data-ttu-id="a8781-529">Шаг 23. Проверьте отработку отказа</span><span class="sxs-lookup"><span data-stu-id="a8781-529">Step 23: Test failover</span></span>
<span data-ttu-id="a8781-530">Теперь должен сообщить hello перенесенных узел синхронизации с локальным hello всегда на узел, поместите его в режиме репликации toosynchronous и подождите, пока он не будет синхронизирована.</span><span class="sxs-lookup"><span data-stu-id="a8781-530">You should now let hello migrated node synchronize with hello on-premises Always On node, place it in toosynchronous replication mode and wait until it is synchronized.</span></span> <span data-ttu-id="a8781-531">Затем отработку отказа из локальной toohello первый узел миграция, который является hello AFP.</span><span class="sxs-lookup"><span data-stu-id="a8781-531">Then failover from on-prem toohello first node migrated, which is hello AFP.</span></span> <span data-ttu-id="a8781-532">После, работал, изменение hello последнего переноса AFP toohello узла.</span><span class="sxs-lookup"><span data-stu-id="a8781-532">Once that has worked, change hello last migrated node toohello AFP.</span></span>

<span data-ttu-id="a8781-533">Следует тестовые отработки отказа между всеми узлами и запустить на то, что ожидается хаоса тесты, которые tooensure переход на другой ресурс может использоваться в качестве и своевременно манор.</span><span class="sxs-lookup"><span data-stu-id="a8781-533">You should test failovers between all nodes and run though chaos tests tooensure failovers work as expected and in a timely manor.</span></span>

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a><span data-ttu-id="a8781-534">Шаг 24. Верните исходные параметры кворума кластера, DNS TTL, параметры перехода на другой ресурс и параметры синхронизации</span><span class="sxs-lookup"><span data-stu-id="a8781-534">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span></span>
##### <a name="adding-ip-address-resource-on-same-subnet"></a><span data-ttu-id="a8781-535">Добавление ресурса IP-адреса в одной подсети</span><span class="sxs-lookup"><span data-stu-id="a8781-535">Adding IP Address Resource on Same Subnet</span></span>
<span data-ttu-id="a8781-536">Если только двух серверов SQL Server и хотите toomigrate их новых tooa облачной службы, но, чтобы tookeep их на Здравствуйте одной подсети, можно избежать создания прослушивателя hello автономного toodelete всегда hello исходный IP-адрес и добавить новый IP-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="a8781-536">If you have only 2 SQL Servers and want toomigrate them tooa new cloud service, but want tookeep them on hello same subnet, you can avoid taking hello listener offline toodelete hello original Always On IP Address and add hello New IP Address.</span></span> <span data-ttu-id="a8781-537">Если вы переносите hello виртуальные машины tooanother подсети, он не потребуется toodo как сеть дополнительных кластера, которая будет ссылаться в этой подсети.</span><span class="sxs-lookup"><span data-stu-id="a8781-537">If you are migrating hello VMs tooanother subnet you will not need toodo this as there will be an additional cluster network that will reference that subnet.</span></span>

<span data-ttu-id="a8781-538">После возможно восстановление hello миграции получателя и были добавлены в hello новый ресурс IP-адрес для новой облачной службе hello до перехода на другой ресурс hello существующий первичный, следует выполните следующие действия в пределах hello Диспетчер отказоустойчивости кластеров:</span><span class="sxs-lookup"><span data-stu-id="a8781-538">Once you have brought up hello migrated secondary and added in hello new IP Address resource for hello new cloud service before failover hello existing Primary, you should take these steps within hello Cluster Failover Manager:</span></span>

<span data-ttu-id="a8781-539">tooadd IP-адрес в разделе hello [приложение](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), шаг 14.</span><span class="sxs-lookup"><span data-stu-id="a8781-539">tooadd in IP Address, see hello [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span></span>

1. <span data-ttu-id="a8781-540">Hello текущий ресурс IP-адреса, измените too'Existing возможного владельца hello основного сервера SQL Server ", в примере hello ниже «dansqlams4»:</span><span class="sxs-lookup"><span data-stu-id="a8781-540">For hello current IP Address resource, change hello possible owner too‘Existing Primary SQL Server’, in hello example below, ‘dansqlams4’:</span></span>

    ![Приложение13][23]
2. <span data-ttu-id="a8781-542">Hello новый ресурс IP-адреса, измените too'Migrated hello возможного владельца сервера-получателя SQL ", в примере hello ниже «dansqlams5»:</span><span class="sxs-lookup"><span data-stu-id="a8781-542">For hello new IP Address resource, change hello possible owner too‘Migrated secondary SQL Server’, in hello example below, ‘dansqlams5’:</span></span>

    ![Приложение14][24]
3. <span data-ttu-id="a8781-544">После этого вы можете отработки отказа, когда последний узел hello переносится hello возможных владельцев следует изменять, этот узел добавляется в качестве возможного владельца:</span><span class="sxs-lookup"><span data-stu-id="a8781-544">Once this is set you can failover, and when hello last node is migrated hello Possible Owners should be edited so that node is added as a Possible Owner:</span></span>

    ![Приложение15][25]

## <a name="additional-resources"></a><span data-ttu-id="a8781-546">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a8781-546">Additional resources</span></span>
* [<span data-ttu-id="a8781-547">Хранилище Azure Premium</span><span class="sxs-lookup"><span data-stu-id="a8781-547">Azure Premium Storage</span></span>](../../../storage/common/storage-premium-storage.md)
* [<span data-ttu-id="a8781-548">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="a8781-548">Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/)
* [<span data-ttu-id="a8781-549">SQL Server в виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="a8781-549">SQL Server in Azure Virtual Machines</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png
