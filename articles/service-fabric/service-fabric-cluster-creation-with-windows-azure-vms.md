---
title: "aaaCreate отдельный кластер с виртуальными машинами Azure под управлением Windows | Документы Microsoft"
description: "Узнайте, как toocreate кластеру Azure Service Fabric на виртуальных машинах Azure под управлением Windows Server и управлять им."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a><span data-ttu-id="8af3d-103">Создание автономного кластера Service Fabric с тремя узлами на базе виртуальных машин Azure под управлением Windows Server</span><span class="sxs-lookup"><span data-stu-id="8af3d-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span></span>
<span data-ttu-id="8af3d-104">В этой статье описывается, как toocreate a кластера на основе Windows Azure виртуальных машин (ВМ) с помощью hello автономный установщик Service Fabric для Windows Server.</span><span class="sxs-lookup"><span data-stu-id="8af3d-104">This article describes how toocreate a cluster on Windows-based Azure virtual machines (VMs), using hello standalone Service Fabric installer for Windows Server.</span></span> <span data-ttu-id="8af3d-105">Hello сценария является особым случаем [Создание и управление ими в кластере под управлением Windows Server](service-fabric-cluster-creation-for-windows-server.md) которых виртуальные машины hello [виртуальные машины Azure под управлением Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), однако вы не создаете [Azure облачный кластер Service Fabric](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8af3d-105">hello scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where hello VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span></span> <span data-ttu-id="8af3d-106">различие Hello в следующих этот шаблон является этого кластера Service Fabric автономный hello созданные hello следующие шаги полностью управляется вами, тогда как hello фабрике Azure облачной службы кластеров, управляемых и обновляются по hello Service Fabric поставщик ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8af3d-106">hello distinction in following this pattern is that hello standalone Service Fabric cluster created by hello following steps is entirely managed by you, whereas hello Azure cloud-based Service Fabric clusters are managed and upgraded by hello Service Fabric resource provider.</span></span>

## <a name="steps-toocreate-hello-standalone-cluster"></a><span data-ttu-id="8af3d-107">Hello автономного действия toocreate кластера</span><span class="sxs-lookup"><span data-stu-id="8af3d-107">Steps toocreate hello standalone cluster</span></span>
1. <span data-ttu-id="8af3d-108">Войдите в портал Azure toohello и создания новой виртуальной Машины центра обработки данных Windows Server 2016 или Windows Server 2012 R2 Datacenter в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8af3d-108">Sign in toohello Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span></span> <span data-ttu-id="8af3d-109">Прочитать статью hello [создания ВМ Windows на портал Azure hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="8af3d-109">Read hello article [Create a Windows VM in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span></span>
2. <span data-ttu-id="8af3d-110">Добавьте пару дополнительные виртуальные машины toohello одну группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8af3d-110">Add a couple more VMs toohello same resource group.</span></span> <span data-ttu-id="8af3d-111">Убедитесь в каждой из виртуальных машин hello имеет hello же имя пользователя администратора и пароль при создании.</span><span class="sxs-lookup"><span data-stu-id="8af3d-111">Ensure that each of hello VMs has hello same administrator user name and password when created.</span></span> <span data-ttu-id="8af3d-112">После создания вы увидите все три виртуальные машины в hello одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="8af3d-112">Once created you should see all three VMs in hello same virtual network.</span></span>
3. <span data-ttu-id="8af3d-113">Подключение tooeach из hello виртуальных машин и отключение брандмауэра Windows с помощью hello hello [диспетчера сервера, локального сервера мониторинга](https://technet.microsoft.com/library/jj134147.aspx).</span><span class="sxs-lookup"><span data-stu-id="8af3d-113">Connect tooeach of hello VMs and turn off hello Windows Firewall using hello [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span></span> <span data-ttu-id="8af3d-114">Это гарантирует, что hello сетевой трафик может обмениваться данными между компьютерами hello.</span><span class="sxs-lookup"><span data-stu-id="8af3d-114">This ensures that hello network traffic can communicate between hello machines.</span></span> <span data-ttu-id="8af3d-115">При машины подключенных tooeach получить hello IP-адрес, откройте командную строку и введите `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="8af3d-115">While connected tooeach machine, get hello IP address by opening a command prompt and typing `ipconfig`.</span></span> <span data-ttu-id="8af3d-116">Также можно увидеть hello IP адрес каждого компьютера, на портале hello, выбрав hello ресурсов виртуальной сети для группы ресурсов hello и проверка hello сетевых интерфейсов, созданных для каждого из этих компьютеров.</span><span class="sxs-lookup"><span data-stu-id="8af3d-116">Alternatively you can see hello IP address of each machine on hello portal, by selecting hello virtual network resource for hello resource group and checking hello network interfaces created for each of these machines.</span></span>
4. <span data-ttu-id="8af3d-117">Подключите tooone из hello виртуальных машин и тест, который можно проверить связь hello другие две виртуальных машины успешно.</span><span class="sxs-lookup"><span data-stu-id="8af3d-117">Connect tooone of hello VMs and test that you can ping hello other two VMs successfully.</span></span>
5. <span data-ttu-id="8af3d-118">Подключение tooone из hello виртуальных машин и [загрузить hello изолированный пакет Service Fabric для Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) в новую папку на hello машинные и извлеките hello.</span><span class="sxs-lookup"><span data-stu-id="8af3d-118">Connect tooone of hello VMs and [download hello standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on hello machine and extract hello package.</span></span>
6. <span data-ttu-id="8af3d-119">Откройте hello *ClusterConfig.Unsecure.MultiMachine.json* в Блокноте и изменить каждый узел с IP-адресами hello трех машин hello.</span><span class="sxs-lookup"><span data-stu-id="8af3d-119">Open hello *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with hello three IP addresses of hello machines.</span></span> <span data-ttu-id="8af3d-120">Изменение имени кластера hello вверху hello и сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="8af3d-120">Change hello cluster name at hello top and save hello file.</span></span>  <span data-ttu-id="8af3d-121">Ниже показан частичного пример hello манифеста кластера.</span><span class="sxs-lookup"><span data-stu-id="8af3d-121">A partial example of hello cluster manifest is shown below.</span></span>
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. <span data-ttu-id="8af3d-122">Если необходимо реализовать этот toobe безопасного кластера, решить hello меры безопасности, необходимо будет toouse и выполнить инструкции раздела hello hello связанные ссылки: [сертификатов X509](service-fabric-windows-cluster-x509-security.md) или [безопасности Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="8af3d-122">If you intend this toobe a secure cluster, decide hello security measure you would like toouse and follow hello steps at hello associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="8af3d-123">Если установка hello кластера с помощью средств безопасности Windows, необходимо будет tooset копирование toomanage контроллера домена Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8af3d-123">If setting up hello cluster using Windows Security, you will need tooset up a domain controller toomanage Active Directory.</span></span> <span data-ttu-id="8af3d-124">Обратите внимание, что использование компьютера контроллера домена в качестве узла Service Fabric не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="8af3d-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span></span>
8. <span data-ttu-id="8af3d-125">Откройте окно [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span><span class="sxs-lookup"><span data-stu-id="8af3d-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span> <span data-ttu-id="8af3d-126">Перейдите в папку toohello, где извлечены hello загруженный автономный установщик пакет и сохранить файл конфигурации кластера hello.</span><span class="sxs-lookup"><span data-stu-id="8af3d-126">Navigate toohello folder where you extracted hello downloaded standalone installer package and saved hello cluster configuration file.</span></span> <span data-ttu-id="8af3d-127">Выполните hello, следуя кластера hello toodeploy команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8af3d-127">Run hello following PowerShell command toodeploy hello cluster:</span></span>
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

<span data-ttu-id="8af3d-128">Hello скрипта удаленно настраивает кластер Service Fabric hello и следует сообщать о ходе выполнения как развертывания выполняет накат до.</span><span class="sxs-lookup"><span data-stu-id="8af3d-128">hello script will remotely configure hello Service Fabric cluster and should report progress as deployment rolls through.</span></span>

9. <span data-ttu-id="8af3d-129">После около минуты, можно проверить, если hello кластер является работоспособным, подключившись toohello Service Fabric Explorer с помощью одного компьютера hello IP-адресов, например с помощью `http://10.1.0.5:19080/Explorer/index.html`.</span><span class="sxs-lookup"><span data-stu-id="8af3d-129">After about a minute, you can check if hello cluster is operational by connecting toohello Service Fabric Explorer using one of hello machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8af3d-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8af3d-130">Next steps</span></span>
* [<span data-ttu-id="8af3d-131">Создание автономных кластеров Service Fabric в Windows Server или Linux</span><span class="sxs-lookup"><span data-stu-id="8af3d-131">Create standalone Service Fabric clusters on Windows Server or Linux</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="8af3d-132">Добавление или удаление кластера Service Fabric автономные узлы tooa</span><span class="sxs-lookup"><span data-stu-id="8af3d-132">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="8af3d-133">Параметры конфигурации для автономного кластера Windows</span><span class="sxs-lookup"><span data-stu-id="8af3d-133">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="8af3d-134">Защита автономного кластера под управлением Windows с помощью системы безопасности Windows</span><span class="sxs-lookup"><span data-stu-id="8af3d-134">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="8af3d-135">Защита автономного кластера под управлением Windows с помощью сертификатов</span><span class="sxs-lookup"><span data-stu-id="8af3d-135">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

