---
title: "aaaCreate виртуальная сеть | Шаблон диспетчера ресурсов Azure | Документы Microsoft"
description: "Узнайте, как toocreate в виртуальной сети с помощью шаблона диспетчера ресурсов Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 69530861-2f97-4a6e-b336-a7baf2690044
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b9c289433ff2a84bec19eac25fa28ab40d131c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a><span data-ttu-id="179b1-103">Создание виртуальной сети с использованием шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="179b1-103">Create a virtual network using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="179b1-104">Azure предоставляет две модели развертывания: с помощью Azure Resource Manager и классическую.</span><span class="sxs-lookup"><span data-stu-id="179b1-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="179b1-105">Корпорация Майкрософт рекомендует создать ресурсы с помощью модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="179b1-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="179b1-106">Дополнительные сведения о toolearn hello различий между моделями hello двух чтения hello [модели развертывания Azure понять](../azure-resource-manager/resource-manager-deployment-model.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="179b1-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="179b1-107">В этой статье объясняется, как toocreate виртуальной сети путем развертывания диспетчера ресурсов hello модели с помощью шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="179b1-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using an Azure Resource Manager template.</span></span> <span data-ttu-id="179b1-108">Также можно создать виртуальную сеть через диспетчер ресурсов с помощью других средств или создайте виртуальную сеть через hello классической модели развертывания, выбрав другой вариант hello после списка:</span><span class="sxs-lookup"><span data-stu-id="179b1-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
- [<span data-ttu-id="179b1-109">Портал</span><span class="sxs-lookup"><span data-stu-id="179b1-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
- [<span data-ttu-id="179b1-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="179b1-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
- [<span data-ttu-id="179b1-111">ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ</span><span class="sxs-lookup"><span data-stu-id="179b1-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
- [<span data-ttu-id="179b1-112">Шаблон</span><span class="sxs-lookup"><span data-stu-id="179b1-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
- [<span data-ttu-id="179b1-113">Портал (классический)</span><span class="sxs-lookup"><span data-stu-id="179b1-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
- [<span data-ttu-id="179b1-114">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="179b1-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [<span data-ttu-id="179b1-115">Интерфейс командной строки (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="179b1-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

<span data-ttu-id="179b1-116">Вы узнаете, как toodownload и изменить существующий шаблон ARM из GitHub и развертывания шаблона hello из GitHub, PowerShell и hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="179b1-116">You will learn how toodownload and modify and existing ARM template from GitHub, and deploy hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="179b1-117">При развертывании шаблона hello ARM непосредственно из GitHub, без изменений, просто пропустите слишком[развертывания шаблона из github](#deploy-the-arm-template-by-using-click-to-deploy).</span><span class="sxs-lookup"><span data-stu-id="179b1-117">If you are simply deploying hello ARM template directly from GitHub, without any changes, skip too[deploy a template from github](#deploy-the-arm-template-by-using-click-to-deploy).</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="179b1-118">Загрузите и понять hello шаблона диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="179b1-118">Download and understand hello Azure Resource Manager template</span></span>
<span data-ttu-id="179b1-119">Можно загрузить hello существующего шаблона для создания виртуальной сети и две подсети из GitHub, внесите изменения можно будет и использовать его.</span><span class="sxs-lookup"><span data-stu-id="179b1-119">You can download hello existing template for creating a VNet and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="179b1-120">toodo таким образом, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="179b1-120">toodo so, complete hello following steps:</span></span>

1. <span data-ttu-id="179b1-121">Перейдите в слишком[страницы шаблона образец hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="179b1-121">Navigate too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="179b1-122">Щелкните **azuredeploy.json** и нажмите кнопку **RAW**.</span><span class="sxs-lookup"><span data-stu-id="179b1-122">Click **azuredeploy.json**, and then click **RAW**.</span></span>
3. <span data-ttu-id="179b1-123">Сохраните файл tooa hello локальную папку на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="179b1-123">Save hello file tooa a local folder on your computer.</span></span>
4. <span data-ttu-id="179b1-124">Если вы знакомы с шаблонами, пропустите toostep 7.</span><span class="sxs-lookup"><span data-stu-id="179b1-124">If you are familiar with templates, skip toostep 7.</span></span>
5. <span data-ttu-id="179b1-125">Откройте только что сохраненный файл hello и просмотрите содержимое hello под **параметры** в строке 5.</span><span class="sxs-lookup"><span data-stu-id="179b1-125">Open hello file you just saved and look at hello contents under **parameters** in line 5.</span></span> <span data-ttu-id="179b1-126">Параметры шаблона ARM предоставляют заполнитель для значений, которые могут заполняться во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="179b1-126">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span></span>
   
   | <span data-ttu-id="179b1-127">Параметр</span><span class="sxs-lookup"><span data-stu-id="179b1-127">Parameter</span></span> | <span data-ttu-id="179b1-128">Описание</span><span class="sxs-lookup"><span data-stu-id="179b1-128">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="179b1-129">**расположение**</span><span class="sxs-lookup"><span data-stu-id="179b1-129">**location**</span></span> |<span data-ttu-id="179b1-130">Регион Azure, где будут создаваться hello виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="179b1-130">Azure region where hello VNet will be created</span></span> |
   | <span data-ttu-id="179b1-131">**vnetName**</span><span class="sxs-lookup"><span data-stu-id="179b1-131">**vnetName**</span></span> |<span data-ttu-id="179b1-132">Имя для hello новой виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="179b1-132">Name for hello new VNet</span></span> |
   | <span data-ttu-id="179b1-133">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="179b1-133">**addressPrefix**</span></span> |<span data-ttu-id="179b1-134">Адресное пространство для hello виртуальной сети, в формате CIDR</span><span class="sxs-lookup"><span data-stu-id="179b1-134">Address space for hello VNet, in CIDR format</span></span> |
   | <span data-ttu-id="179b1-135">**subnet1Name**</span><span class="sxs-lookup"><span data-stu-id="179b1-135">**subnet1Name**</span></span> |<span data-ttu-id="179b1-136">Имя для hello первой виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="179b1-136">Name for hello first VNet</span></span> |
   | <span data-ttu-id="179b1-137">**subnet1Prefix**</span><span class="sxs-lookup"><span data-stu-id="179b1-137">**subnet1Prefix**</span></span> |<span data-ttu-id="179b1-138">Блок CIDR для hello первая подсеть</span><span class="sxs-lookup"><span data-stu-id="179b1-138">CIDR block for hello first subnet</span></span> |
   | <span data-ttu-id="179b1-139">**subnet2Name**</span><span class="sxs-lookup"><span data-stu-id="179b1-139">**subnet2Name**</span></span> |<span data-ttu-id="179b1-140">Имя для hello второй виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="179b1-140">Name for hello second VNet</span></span> |
   | <span data-ttu-id="179b1-141">**subnet2Prefix**</span><span class="sxs-lookup"><span data-stu-id="179b1-141">**subnet2Prefix**</span></span> |<span data-ttu-id="179b1-142">Блок CIDR для второй подсети hello</span><span class="sxs-lookup"><span data-stu-id="179b1-142">CIDR block for hello second subnet</span></span> |
   
   > [!IMPORTANT]
   > <span data-ttu-id="179b1-143">Шаблоны ARM, хранящиеся в GitHub, со временем могут изменяться.</span><span class="sxs-lookup"><span data-stu-id="179b1-143">Azure Resource Manager templates maintained in GitHub can change over time.</span></span> <span data-ttu-id="179b1-144">Убедитесь, что проверка hello шаблона перед его использованием.</span><span class="sxs-lookup"><span data-stu-id="179b1-144">Make sure you check hello template before using it.</span></span>
   > 
   > 
6. <span data-ttu-id="179b1-145">Проверьте содержимое hello в **ресурсов** и обратите внимание, hello следующее:</span><span class="sxs-lookup"><span data-stu-id="179b1-145">Check hello content under **resources** and notice hello following:</span></span>
   
   * <span data-ttu-id="179b1-146">**type**.</span><span class="sxs-lookup"><span data-stu-id="179b1-146">**type**.</span></span> <span data-ttu-id="179b1-147">Тип ресурса, создаваемого шаблоном hello.</span><span class="sxs-lookup"><span data-stu-id="179b1-147">Type of resource being created by hello template.</span></span> <span data-ttu-id="179b1-148">В данном случае это тип **Microsoft.Network/virtualNetworks**, который представляют виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="179b1-148">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span></span>
   * <span data-ttu-id="179b1-149">**name**.</span><span class="sxs-lookup"><span data-stu-id="179b1-149">**name**.</span></span> <span data-ttu-id="179b1-150">Имя ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="179b1-150">Name for hello resource.</span></span> <span data-ttu-id="179b1-151">Использование уведомления hello **[parameters('vnetName')]**, который означает hello имя будут указаны во входных данных hello пользователем или в файле параметров во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="179b1-151">Notice hello use of **[parameters('vnetName')]**, which means hello name will provided as input by hello user or a parameter file during deployment.</span></span>
   * <span data-ttu-id="179b1-152">**properties**.</span><span class="sxs-lookup"><span data-stu-id="179b1-152">**properties**.</span></span> <span data-ttu-id="179b1-153">Список свойств для ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="179b1-153">List of properties for hello resource.</span></span> <span data-ttu-id="179b1-154">Этот шаблон использует свойства пространства и подсети адреса hello во время создания виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="179b1-154">This template uses hello address space and subnet properties during VNet creation.</span></span>
7. <span data-ttu-id="179b1-155">Переход назад слишком[страницы шаблона образец hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="179b1-155">Navigate back too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
8. <span data-ttu-id="179b1-156">Щелкните **azuredeploy paremeters.json** и нажмите кнопку **RAW**.</span><span class="sxs-lookup"><span data-stu-id="179b1-156">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span></span>
9. <span data-ttu-id="179b1-157">Сохраните файл tooa hello локальную папку на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="179b1-157">Save hello file tooa a local folder on your computer.</span></span>
10. <span data-ttu-id="179b1-158">Откройте только что сохраненный файл hello и отредактируйте hello значения для параметров hello.</span><span class="sxs-lookup"><span data-stu-id="179b1-158">Open hello file you just saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="179b1-159">Используйте следующие значения ниже toodeploy hello виртуальной сети в сценарии hello hello.</span><span class="sxs-lookup"><span data-stu-id="179b1-159">Use hello following values below toodeploy hello VNet described in hello scenario:</span></span>

    ```json
        {
          "location": {
            "value": "Central US"
          },
          "vnetName": {
              "value": "TestVNet"
          },
          "addressPrefix": {
              "value": "192.168.0.0/16"
          },
          "subnet1Name": {
              "value": "FrontEnd"
          },
          "subnet1Prefix": {
            "value": "192.168.1.0/24"
          },
          "subnet2Name": {
              "value": "BackEnd"
          },
          "subnet2Prefix": {
              "value": "192.168.2.0/24"
          }
        }
    ```

11. <span data-ttu-id="179b1-160">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="179b1-160">Save hello file.</span></span>


## <a name="deploy-hello-template-using-powershell"></a><span data-ttu-id="179b1-161">Развертывание шаблона hello, с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="179b1-161">Deploy hello template using PowerShell</span></span>

<span data-ttu-id="179b1-162">Выполните следующие шаги toodeploy hello загруженный шаблон с помощью PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="179b1-162">Complete hello following steps toodeploy hello template you downloaded by using PowerShell:</span></span>

1. <span data-ttu-id="179b1-163">Установка и настройка Azure PowerShell, выполнив шаги hello в hello [как tooInstall и настройка Azure PowerShell](/powershell/azure/overview) статьи.</span><span class="sxs-lookup"><span data-stu-id="179b1-163">Install and configure Azure PowerShell by completing hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="179b1-164">Выполните следующие команды toocreate hello новой группы ресурсов:</span><span class="sxs-lookup"><span data-stu-id="179b1-164">Run hello following command toocreate a new resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="179b1-165">Команда Hello создает группу ресурсов с именем *TestRG* в hello *центральной части США* регион azure.</span><span class="sxs-lookup"><span data-stu-id="179b1-165">hello command creates a resource group named *TestRG* in hello *Central US* azure region.</span></span> <span data-ttu-id="179b1-166">Дополнительные сведения о группах ресурсов см. в разделе "Группы ресурсов" [обзора Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="179b1-166">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="179b1-167">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="179b1-167">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. <span data-ttu-id="179b1-168">Выполните следующую команду, toodeploy hello новой виртуальной сети с помощью hello файлы шаблонов и параметров загрузки и изменения выше hello.</span><span class="sxs-lookup"><span data-stu-id="179b1-168">Run hello following command toodeploy hello new VNet using hello template and parameter files you downloaded and modified above:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    <span data-ttu-id="179b1-169">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="179b1-169">Expected output:</span></span>
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. <span data-ttu-id="179b1-170">Выполнения hello следующая команда свойства hello tooview hello новой виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="179b1-170">Run hello following command tooview hello properties of hello new VNet:</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    <span data-ttu-id="179b1-171">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="179b1-171">Expected output:</span></span>

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="deploy-hello-template-using-click-to-deploy"></a><span data-ttu-id="179b1-172">Развертывание с помощью нажмите кнопку развертывания шаблона hello</span><span class="sxs-lookup"><span data-stu-id="179b1-172">Deploy hello template using click-to-deploy</span></span>

<span data-ttu-id="179b1-173">Можно повторно использовать поддерживается корпорацией Майкрософт и сообщества откройте toohello репозитории отправленного tooa GitHub предварительно определенных диспетчера ресурсов Azure шаблонов.</span><span class="sxs-lookup"><span data-stu-id="179b1-173">You can reuse pre-defined Azure Resource Manager templates uploaded tooa GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="179b1-174">Эти шаблоны можно развертывать из GitHub, или загружаются и изменить toofit вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="179b1-174">These templates can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> <span data-ttu-id="179b1-175">toodeploy шаблон, который создает виртуальную сеть с двумя подсетями завершения hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="179b1-175">toodeploy a template that creates a VNet with two subnets, complete hello following steps:</span></span>

1. <span data-ttu-id="179b1-176">В браузере перейдите слишком[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="179b1-176">From a browser, navigate too[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
2. <span data-ttu-id="179b1-177">Прокрутите вниз список шаблонов hello и нажмите **101 виртуальной сети 2 подсети**.</span><span class="sxs-lookup"><span data-stu-id="179b1-177">Scroll down hello list of templates, and click **101-vnet-two-subnets**.</span></span> <span data-ttu-id="179b1-178">Проверьте hello **README.md** файла, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="179b1-178">Check hello **README.md** file, as shown below.</span></span>

    ![Файл README.md в Github](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. <span data-ttu-id="179b1-180">Нажмите кнопку **развертывание tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="179b1-180">Click **Deploy tooAzure**.</span></span> <span data-ttu-id="179b1-181">При необходимости введите учетные данные для входа в Azure.</span><span class="sxs-lookup"><span data-stu-id="179b1-181">If necessary, enter your Azure login credentials.</span></span> 
4. <span data-ttu-id="179b1-182">В hello **параметры** колонки, введите значения hello вы toouse toocreate в новую виртуальную сеть и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="179b1-182">In hello **Parameters** blade, enter hello values you want toouse toocreate your new VNet, and then click **OK**.</span></span> <span data-ttu-id="179b1-183">Hello на этом рисунке показаны значения hello для hello сценария:</span><span class="sxs-lookup"><span data-stu-id="179b1-183">hello following figure shows hello values for hello scenario:</span></span>
   
    ![Параметры шаблона ARM](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. <span data-ttu-id="179b1-185">Нажмите кнопку **группы ресурсов** и выберите tooadd группы ресурсов виртуальной сети для hello, или нажмите кнопку **создать новый** tooadd hello виртуальной сети tooa новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="179b1-185">Click **Resource group** and select a resource group tooadd hello VNet to, or click **Create new** tooadd hello VNet tooa new resource group.</span></span> <span data-ttu-id="179b1-186">Hello на этом рисунке показан hello ресурс группы параметры для новой группы ресурсов с именем **TestRG**:</span><span class="sxs-lookup"><span data-stu-id="179b1-186">hello following figure shows hello resource group settings for a new resource group called **TestRG**:</span></span>

    ![Группа ресурсов](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. <span data-ttu-id="179b1-188">При необходимости измените hello **подписки** и **расположение** параметры для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="179b1-188">If necessary, change hello **Subscription** and **Location** settings for your VNet.</span></span>
7. <span data-ttu-id="179b1-189">Если требуется запретить toosee hello виртуальной сети в качестве плитки в hello **начальной панели**, отключите **tooStartboard ПИН-кода**.</span><span class="sxs-lookup"><span data-stu-id="179b1-189">If you do not want toosee hello VNet as a tile in hello **Startboard**, disable **Pin tooStartboard**.</span></span>
8. <span data-ttu-id="179b1-190">Нажмите кнопку **условия**, ознакомьтесь с условиями hello и нажмите кнопку **купить** tooagree.</span><span class="sxs-lookup"><span data-stu-id="179b1-190">Click **Legal terms**, read hello terms, and click **Buy** tooagree.</span></span> 
9. <span data-ttu-id="179b1-191">Нажмите кнопку **создать** toocreate hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="179b1-191">Click **Create** toocreate hello VNet.</span></span>
   
    ![Отправка элемента развертывания в портал предварительной версии](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. <span data-ttu-id="179b1-193">После завершения развертывания hello в hello портал Azure нажмите кнопку **дополнительные службы**, тип *виртуальных сетей* hello поле фильтра, которое появляется, а затем нажмите кнопку виртуальных сетей toosee hello виртуальных сетей колонку.</span><span class="sxs-lookup"><span data-stu-id="179b1-193">Once hello deployment is complete, in hello Azure portal click **More services**, type *virtual networks* in hello filter box that appears, then click Virtual networks toosee hello Virtual networks blade.</span></span> <span data-ttu-id="179b1-194">В колонке hello щелкните *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="179b1-194">In hello blade, click *TestVNet*.</span></span> <span data-ttu-id="179b1-195">В hello *TestVNet* колонка, щелкните **подсетей** toosee hello создан подсетях, как показано в следующий рисунок hello:</span><span class="sxs-lookup"><span data-stu-id="179b1-195">In hello *TestVNet* blade, click **Subnets** toosee hello created subnets, as shown in hello following picture:</span></span>
    
     ![Создание виртуальной сети в портале предварительной версии](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a><span data-ttu-id="179b1-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="179b1-197">Next steps</span></span>

<span data-ttu-id="179b1-198">Узнайте, как tooconnect:</span><span class="sxs-lookup"><span data-stu-id="179b1-198">Learn how tooconnect:</span></span>

- <span data-ttu-id="179b1-199">Виртуальная сеть виртуальной машины (VM) tooa путем чтения hello [создания виртуальной Машины Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) или [создания виртуальной Машины Linux](../virtual-machines/linux/quick-create-portal.md) статей.</span><span class="sxs-lookup"><span data-stu-id="179b1-199">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="179b1-200">Вместо создания виртуальной сети и подсети в шагах hello hello статей, можно выбрать существующей виртуальной сети и подсети tooconnect для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="179b1-200">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="179b1-201">Здравствуйте, считывая hello виртуальных сетей в виртуальной сети tooother [подключение виртуальных сетей](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="179b1-201">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="179b1-202">tooan Hello виртуальной сети в локальной сети с помощью виртуальной частной сети сеть сеть (VPN) или канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="179b1-202">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="179b1-203">Дополнительные сведения в разделе hello [подключения локальной сети tooan виртуальной сети с помощью VPN сайтами](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) и [связывание виртуальной сети tooan канал ExpressRoute](../expressroute/expressroute-howto-linkvnet-arm.md) статей.</span><span class="sxs-lookup"><span data-stu-id="179b1-203">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
