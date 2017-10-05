---
title: "Создание автономного кластера из виртуальных машин Azure под управлением Windows | Документация Майкрософт"
description: "Узнайте, как создать кластер Azure Service Fabric на основе виртуальных машин Azure под управлением Windows Server и как управлять этим кластером."
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
ms.openlocfilehash: f8a0305a22c00f9bdbdb1bdb06dc299cccee23dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a><span data-ttu-id="7240e-103">Создание автономного кластера Service Fabric с тремя узлами на базе виртуальных машин Azure под управлением Windows Server</span><span class="sxs-lookup"><span data-stu-id="7240e-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span></span>
<span data-ttu-id="7240e-104">В этой статье описывается создание кластера виртуальных машин Azure под управлением Windows с помощью автономного установщика Service Fabric для Windows Server.</span><span class="sxs-lookup"><span data-stu-id="7240e-104">This article describes how to create a cluster on Windows-based Azure virtual machines (VMs), using the standalone Service Fabric installer for Windows Server.</span></span> <span data-ttu-id="7240e-105">Это частный случай [создания и администрирования кластера под управлением Windows Server](service-fabric-cluster-creation-for-windows-server.md), при котором в качестве виртуальных машин используются [виртуальные машины Azure под управлением Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), но не создается [облачный кластер Service Fabric в Azure](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7240e-105">The scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where the VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span></span> <span data-ttu-id="7240e-106">Важное различие заключается в том, что изолированным кластером Service Fabric, созданным с помощью следующей процедуры, полностью управляете вы, а облачные кластеры Service Fabric в Azure обновляет и администрирует поставщик ресурсов Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7240e-106">The distinction in following this pattern is that the standalone Service Fabric cluster created by the following steps is entirely managed by you, whereas the Azure cloud-based Service Fabric clusters are managed and upgraded by the Service Fabric resource provider.</span></span>

## <a name="steps-to-create-the-standalone-cluster"></a><span data-ttu-id="7240e-107">Процедура создания автономного кластера</span><span class="sxs-lookup"><span data-stu-id="7240e-107">Steps to create the standalone cluster</span></span>
1. <span data-ttu-id="7240e-108">Войдите на портал Azure и создайте виртуальную машину Windows Server 2012 R2 Datacenter или Windows Server 2016 Datacenter в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7240e-108">Sign in to the Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span></span> <span data-ttu-id="7240e-109">Подробнее этот процесс описан в статье [Создание первой виртуальной машины Windows на портале Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7240e-109">Read the article [Create a Windows VM in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span></span>
2. <span data-ttu-id="7240e-110">Добавьте еще несколько виртуальных машин в ту же группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7240e-110">Add a couple more VMs to the same resource group.</span></span> <span data-ttu-id="7240e-111">При создании каждой из них укажите одно и то же имя пользователя и пароль администратора.</span><span class="sxs-lookup"><span data-stu-id="7240e-111">Ensure that each of the VMs has the same administrator user name and password when created.</span></span> <span data-ttu-id="7240e-112">После создания все три виртуальные машины появятся в одной и той же виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="7240e-112">Once created you should see all three VMs in the same virtual network.</span></span>
3. <span data-ttu-id="7240e-113">Подключитесь к каждой из виртуальных машин и выключите брандмауэр Windows с помощью [диспетчера серверов и панели мониторинга локального сервера](https://technet.microsoft.com/library/jj134147.aspx).</span><span class="sxs-lookup"><span data-stu-id="7240e-113">Connect to each of the VMs and turn off the Windows Firewall using the [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span></span> <span data-ttu-id="7240e-114">Это гарантирует, что сетевой трафик может передаваться между компьютерами.</span><span class="sxs-lookup"><span data-stu-id="7240e-114">This ensures that the network traffic can communicate between the machines.</span></span> <span data-ttu-id="7240e-115">После входа на каждую из виртуальных машин узнайте ее IP-адрес, открыв командную строку и введя команду `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="7240e-115">While connected to each machine, get the IP address by opening a command prompt and typing `ipconfig`.</span></span> <span data-ttu-id="7240e-116">IP-адрес каждого компьютера можно также увидеть на портале, выбрав ресурс виртуальной сети для группы ресурсов и изучив сетевые интерфейсы, созданные для каждого из этих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="7240e-116">Alternatively you can see the IP address of each machine on the portal, by selecting the virtual network resource for the resource group and checking the network interfaces created for each of these machines.</span></span>
4. <span data-ttu-id="7240e-117">Подключитесь к одной из виртуальных машин и проверьте наличие связи с остальными двумя.</span><span class="sxs-lookup"><span data-stu-id="7240e-117">Connect to one of the VMs and test that you can ping the other two VMs successfully.</span></span>
5. <span data-ttu-id="7240e-118">Подключитесь к одной из виртуальных машин, [скачайте автономный пакет Service Fabric для Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) в новую папку и извлеките содержимое пакета.</span><span class="sxs-lookup"><span data-stu-id="7240e-118">Connect to one of the VMs and [download the standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on the machine and extract the package.</span></span>
6. <span data-ttu-id="7240e-119">Откройте файл *ClusterConfig.Unsecure.MultiMachine.json* в Блокноте и измените каждый узел, введя три IP-адреса своих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="7240e-119">Open the *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with the three IP addresses of the machines.</span></span> <span data-ttu-id="7240e-120">Измените имя кластера в начале файла и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="7240e-120">Change the cluster name at the top and save the file.</span></span>  <span data-ttu-id="7240e-121">Ниже приведен неполный пример манифеста кластера.</span><span class="sxs-lookup"><span data-stu-id="7240e-121">A partial example of the cluster manifest is shown below.</span></span>
   
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
7. <span data-ttu-id="7240e-122">Если планируется создать защищенный кластер, выберите меры безопасности, которые вы хотите использовать, и выполните инструкции, щелкнув соответствующую ссылку: [сертификат X509](service-fabric-windows-cluster-x509-security.md) или [система безопасности Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="7240e-122">If you intend this to be a secure cluster, decide the security measure you would like to use and follow the steps at the associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="7240e-123">В случае настройки кластера с помощью системы безопасности Windows необходимо установить контроллер домена для управления Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7240e-123">If setting up the cluster using Windows Security, you will need to set up a domain controller to manage Active Directory.</span></span> <span data-ttu-id="7240e-124">Обратите внимание, что использование компьютера контроллера домена в качестве узла Service Fabric не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="7240e-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span></span>
8. <span data-ttu-id="7240e-125">Откройте окно [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span><span class="sxs-lookup"><span data-stu-id="7240e-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span> <span data-ttu-id="7240e-126">Перейдите к папке, в которую вы ранее извлекли содержимое автономного пакета установщика и сохранили файл конфигурации кластера.</span><span class="sxs-lookup"><span data-stu-id="7240e-126">Navigate to the folder where you extracted the downloaded standalone installer package and saved the cluster configuration file.</span></span> <span data-ttu-id="7240e-127">Выполните следующую команду PowerShell, чтобы развернуть кластер.</span><span class="sxs-lookup"><span data-stu-id="7240e-127">Run the following PowerShell command to deploy the cluster:</span></span>
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

<span data-ttu-id="7240e-128">Сценарий удаленно настроит кластер Service Fabric и будет сообщать о ходе развертывания.</span><span class="sxs-lookup"><span data-stu-id="7240e-128">The script will remotely configure the Service Fabric cluster and should report progress as deployment rolls through.</span></span>

9. <span data-ttu-id="7240e-129">Примерно через минуту можно проверить, работает ли кластер, подключившись к Service Fabric Explorer по IP-адресу одной из виртуальных машин, например `http://10.1.0.5:19080/Explorer/index.html`.</span><span class="sxs-lookup"><span data-stu-id="7240e-129">After about a minute, you can check if the cluster is operational by connecting to the Service Fabric Explorer using one of the machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7240e-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7240e-130">Next steps</span></span>
* [<span data-ttu-id="7240e-131">Создание автономных кластеров Service Fabric в Windows Server или Linux</span><span class="sxs-lookup"><span data-stu-id="7240e-131">Create standalone Service Fabric clusters on Windows Server or Linux</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="7240e-132">Добавление узлов в автономный кластер Service Fabric под управлением Windows Server или удаление узлов из него</span><span class="sxs-lookup"><span data-stu-id="7240e-132">Add or remove nodes to a standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="7240e-133">Параметры конфигурации для автономного кластера Windows</span><span class="sxs-lookup"><span data-stu-id="7240e-133">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="7240e-134">Защита автономного кластера под управлением Windows с помощью системы безопасности Windows</span><span class="sxs-lookup"><span data-stu-id="7240e-134">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="7240e-135">Защита автономного кластера под управлением Windows с помощью сертификатов</span><span class="sxs-lookup"><span data-stu-id="7240e-135">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

