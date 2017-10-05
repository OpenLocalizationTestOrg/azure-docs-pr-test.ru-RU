---
title: "Создание виртуальной сети | Шаблон Azure Resource Manager | Документация Майкрософт"
description: "Узнайте, как создать виртуальную сеть с использованием шаблона Azure Resource Manager."
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
ms.openlocfilehash: 81602766848a91331c8d811ea1c8ec3ffae44b96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a><span data-ttu-id="512e0-103">Создание виртуальной сети с использованием шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="512e0-103">Create a virtual network using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="512e0-104">Azure предоставляет две модели развертывания: с помощью Azure Resource Manager и классическую.</span><span class="sxs-lookup"><span data-stu-id="512e0-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="512e0-105">Для создания ресурсов корпорация Майкрософт рекомендует использовать модель развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="512e0-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="512e0-106">Дополнительные сведения о различиях между двумя моделями см. в статье [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](../azure-resource-manager/resource-manager-deployment-model.md) (Azure Resource Manager и классическое развертывание. Общие сведения о моделях развертывания и состоянии ресурсов).</span><span class="sxs-lookup"><span data-stu-id="512e0-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="512e0-107">В этой статье описывается создание виртуальной сети с помощью модели развертывания Resource Manager с использованием шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="512e0-107">This article explains how to create a VNet through the Resource Manager deployment model using an Azure Resource Manager template.</span></span> <span data-ttu-id="512e0-108">Виртуальную сеть также можно создать с помощью Resource Manager, используя другие инструменты, либо с помощью классической модели развертывания, выбрав другой вариант из следующего списка:</span><span class="sxs-lookup"><span data-stu-id="512e0-108">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
- [<span data-ttu-id="512e0-109">Портал</span><span class="sxs-lookup"><span data-stu-id="512e0-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
- [<span data-ttu-id="512e0-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="512e0-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
- [<span data-ttu-id="512e0-111">ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ</span><span class="sxs-lookup"><span data-stu-id="512e0-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
- [<span data-ttu-id="512e0-112">Шаблон</span><span class="sxs-lookup"><span data-stu-id="512e0-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
- [<span data-ttu-id="512e0-113">Портал (классический)</span><span class="sxs-lookup"><span data-stu-id="512e0-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
- [<span data-ttu-id="512e0-114">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="512e0-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [<span data-ttu-id="512e0-115">Интерфейс командной строки (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="512e0-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

<span data-ttu-id="512e0-116">Вы узнаете, как загружать и изменять существующий шаблон ARM из GitHub, а также как развернуть шаблон из GitHub, PowerShell и интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="512e0-116">You will learn how to download and modify and existing ARM template from GitHub, and deploy the template from GitHub, PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="512e0-117">Если вы разворачиваете шаблон ARM непосредственно из GitHub без внесения каких-либо изменений, перейдите к [развертыванию шаблона из github](#deploy-the-arm-template-by-using-click-to-deploy).</span><span class="sxs-lookup"><span data-stu-id="512e0-117">If you are simply deploying the ARM template directly from GitHub, without any changes, skip to [deploy a template from github](#deploy-the-arm-template-by-using-click-to-deploy).</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-the-azure-resource-manager-template"></a><span data-ttu-id="512e0-118">Скачивание и использование шаблона диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="512e0-118">Download and understand the Azure Resource Manager template</span></span>
<span data-ttu-id="512e0-119">Вы можете скачать уже имеющийся шаблон для создания виртуальной сети и двух подсетей из GitHub, внести в него желаемые изменения и применить.</span><span class="sxs-lookup"><span data-stu-id="512e0-119">You can download the existing template for creating a VNet and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="512e0-120">Для этого сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="512e0-120">To do so, complete the following steps:</span></span>

1. <span data-ttu-id="512e0-121">Перейдите к [странице примера шаблона](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="512e0-121">Navigate to [the sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="512e0-122">Щелкните **azuredeploy.json** и нажмите кнопку **RAW**.</span><span class="sxs-lookup"><span data-stu-id="512e0-122">Click **azuredeploy.json**, and then click **RAW**.</span></span>
3. <span data-ttu-id="512e0-123">Сохраните файл в локальную папку на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="512e0-123">Save the file to a a local folder on your computer.</span></span>
4. <span data-ttu-id="512e0-124">Если вы знакомы с шаблонами, перейдите к шагу 7.</span><span class="sxs-lookup"><span data-stu-id="512e0-124">If you are familiar with templates, skip to step 7.</span></span>
5. <span data-ttu-id="512e0-125">Откройте только что сохраненный файл и просмотрите содержимое раздела **parameters** в строке 5.</span><span class="sxs-lookup"><span data-stu-id="512e0-125">Open the file you just saved and look at the contents under **parameters** in line 5.</span></span> <span data-ttu-id="512e0-126">Параметры шаблона ARM предоставляют заполнитель для значений, которые могут заполняться во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="512e0-126">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span></span>
   
   | <span data-ttu-id="512e0-127">Параметр</span><span class="sxs-lookup"><span data-stu-id="512e0-127">Parameter</span></span> | <span data-ttu-id="512e0-128">Описание</span><span class="sxs-lookup"><span data-stu-id="512e0-128">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="512e0-129">**расположение**</span><span class="sxs-lookup"><span data-stu-id="512e0-129">**location**</span></span> |<span data-ttu-id="512e0-130">Регион Azure, в котором будет создана виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="512e0-130">Azure region where the VNet will be created</span></span> |
   | <span data-ttu-id="512e0-131">**vnetName**</span><span class="sxs-lookup"><span data-stu-id="512e0-131">**vnetName**</span></span> |<span data-ttu-id="512e0-132">Имя для новой виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="512e0-132">Name for the new VNet</span></span> |
   | <span data-ttu-id="512e0-133">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="512e0-133">**addressPrefix**</span></span> |<span data-ttu-id="512e0-134">Адресное пространство виртуальной сети в формате CIDR</span><span class="sxs-lookup"><span data-stu-id="512e0-134">Address space for the VNet, in CIDR format</span></span> |
   | <span data-ttu-id="512e0-135">**subnet1Name**</span><span class="sxs-lookup"><span data-stu-id="512e0-135">**subnet1Name**</span></span> |<span data-ttu-id="512e0-136">Имя первой виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="512e0-136">Name for the first VNet</span></span> |
   | <span data-ttu-id="512e0-137">**subnet1Prefix**</span><span class="sxs-lookup"><span data-stu-id="512e0-137">**subnet1Prefix**</span></span> |<span data-ttu-id="512e0-138">Блок CIDR для первой подсети</span><span class="sxs-lookup"><span data-stu-id="512e0-138">CIDR block for the first subnet</span></span> |
   | <span data-ttu-id="512e0-139">**subnet2Name**</span><span class="sxs-lookup"><span data-stu-id="512e0-139">**subnet2Name**</span></span> |<span data-ttu-id="512e0-140">Имя второй виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="512e0-140">Name for the second VNet</span></span> |
   | <span data-ttu-id="512e0-141">**subnet2Prefix**</span><span class="sxs-lookup"><span data-stu-id="512e0-141">**subnet2Prefix**</span></span> |<span data-ttu-id="512e0-142">Блок CIDR для второй подсети</span><span class="sxs-lookup"><span data-stu-id="512e0-142">CIDR block for the second subnet</span></span> |
   
   > [!IMPORTANT]
   > <span data-ttu-id="512e0-143">Шаблоны ARM, хранящиеся в GitHub, со временем могут изменяться.</span><span class="sxs-lookup"><span data-stu-id="512e0-143">Azure Resource Manager templates maintained in GitHub can change over time.</span></span> <span data-ttu-id="512e0-144">Перед использованием шаблона обязательно его проверьте.</span><span class="sxs-lookup"><span data-stu-id="512e0-144">Make sure you check the template before using it.</span></span>
   > 
   > 
6. <span data-ttu-id="512e0-145">Проверьте содержимое раздела **resources** и обратите внимание на следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="512e0-145">Check the content under **resources** and notice the following:</span></span>
   
   * <span data-ttu-id="512e0-146">**type**.</span><span class="sxs-lookup"><span data-stu-id="512e0-146">**type**.</span></span> <span data-ttu-id="512e0-147">Тип ресурса, созданного на основе шаблона.</span><span class="sxs-lookup"><span data-stu-id="512e0-147">Type of resource being created by the template.</span></span> <span data-ttu-id="512e0-148">В данном случае это тип **Microsoft.Network/virtualNetworks**, который представляют виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="512e0-148">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span></span>
   * <span data-ttu-id="512e0-149">**name**.</span><span class="sxs-lookup"><span data-stu-id="512e0-149">**name**.</span></span> <span data-ttu-id="512e0-150">Имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="512e0-150">Name for the resource.</span></span> <span data-ttu-id="512e0-151">Обратите внимание на фрагмент кода **[parameters('vnetName')]**, означающий, что имя будет предоставлено пользователем или файлом параметров в процессе развертывания.</span><span class="sxs-lookup"><span data-stu-id="512e0-151">Notice the use of **[parameters('vnetName')]**, which means the name will provided as input by the user or a parameter file during deployment.</span></span>
   * <span data-ttu-id="512e0-152">**properties**.</span><span class="sxs-lookup"><span data-stu-id="512e0-152">**properties**.</span></span> <span data-ttu-id="512e0-153">Список свойств для ресурса.</span><span class="sxs-lookup"><span data-stu-id="512e0-153">List of properties for the resource.</span></span> <span data-ttu-id="512e0-154">При создании виртуальной сети в этом шаблоне используется адресное пространство и свойства подсети.</span><span class="sxs-lookup"><span data-stu-id="512e0-154">This template uses the address space and subnet properties during VNet creation.</span></span>
7. <span data-ttu-id="512e0-155">Вернитесь на [страницу примера шаблона](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="512e0-155">Navigate back to [the sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
8. <span data-ttu-id="512e0-156">Щелкните **azuredeploy paremeters.json** и нажмите кнопку **RAW**.</span><span class="sxs-lookup"><span data-stu-id="512e0-156">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span></span>
9. <span data-ttu-id="512e0-157">Сохраните файл в локальную папку на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="512e0-157">Save the file to a a local folder on your computer.</span></span>
10. <span data-ttu-id="512e0-158">Откройте только что сохраненный файл и измените значения параметров.</span><span class="sxs-lookup"><span data-stu-id="512e0-158">Open the file you just saved and edit the values for the parameters.</span></span> <span data-ttu-id="512e0-159">Для развертывания виртуальной сети в этом сценарии используйте следующие значения.</span><span class="sxs-lookup"><span data-stu-id="512e0-159">Use the following values below to deploy the VNet described in the scenario:</span></span>

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

11. <span data-ttu-id="512e0-160">Сохраните файл .</span><span class="sxs-lookup"><span data-stu-id="512e0-160">Save the file.</span></span>


## <a name="deploy-the-template-using-powershell"></a><span data-ttu-id="512e0-161">Развертывание шаблона с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="512e0-161">Deploy the template using PowerShell</span></span>

<span data-ttu-id="512e0-162">Чтобы развернуть шаблон, скачанный с помощью PowerShell, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="512e0-162">Complete the following steps to deploy the template you downloaded by using PowerShell:</span></span>

1. <span data-ttu-id="512e0-163">Установите и настройте Azure PowerShell, выполнив действия, описанные в [этой статье](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="512e0-163">Install and configure Azure PowerShell by completing the steps in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="512e0-164">Выполните следующую команду, чтобы создать новую группу ресурсов:</span><span class="sxs-lookup"><span data-stu-id="512e0-164">Run the following command to create a new resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="512e0-165">Эта команда создает группу ресурсов с именем *TestRG* в регионе Azure *Центральная часть США*.</span><span class="sxs-lookup"><span data-stu-id="512e0-165">The command creates a resource group named *TestRG* in the *Central US* azure region.</span></span> <span data-ttu-id="512e0-166">Дополнительные сведения о группах ресурсов см. в разделе "Группы ресурсов" [обзора Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="512e0-166">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="512e0-167">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="512e0-167">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. <span data-ttu-id="512e0-168">Выполните следующую команду, чтобы развернуть новую виртуальную сеть с помощью файлов шаблонов и параметров, которые вы скачали и изменили раньше.</span><span class="sxs-lookup"><span data-stu-id="512e0-168">Run the following command to deploy the new VNet using the template and parameter files you downloaded and modified above:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    <span data-ttu-id="512e0-169">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="512e0-169">Expected output:</span></span>
   
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
4. <span data-ttu-id="512e0-170">Чтобы просмотреть свойства новой виртуальной сети, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="512e0-170">Run the following command to view the properties of the new VNet:</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    <span data-ttu-id="512e0-171">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="512e0-171">Expected output:</span></span>

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

## <a name="deploy-the-template-using-click-to-deploy"></a><span data-ttu-id="512e0-172">Развертывание шаблона с помощью кнопки развертывания</span><span class="sxs-lookup"><span data-stu-id="512e0-172">Deploy the template using click-to-deploy</span></span>

<span data-ttu-id="512e0-173">Вы можете использовать шаблоны Azure Resource Manager, уже настроенные и загруженные в репозиторий GitHub корпорации Майкрософт и доступные для всех.</span><span class="sxs-lookup"><span data-stu-id="512e0-173">You can reuse pre-defined Azure Resource Manager templates uploaded to a GitHub repository maintained by Microsoft and open to the community.</span></span> <span data-ttu-id="512e0-174">Эти шаблоны можно развернуть прямо из репозитория GitHub или скачать и внести необходимые изменения.</span><span class="sxs-lookup"><span data-stu-id="512e0-174">These templates can be deployed straight out of GitHub, or downloaded and modified to fit your needs.</span></span> <span data-ttu-id="512e0-175">Чтобы развернуть шаблон, создающий виртуальную сеть с двумя подсетями, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="512e0-175">To deploy a template that creates a VNet with two subnets, complete the following steps:</span></span>

1. <span data-ttu-id="512e0-176">В браузере откройте страницу [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="512e0-176">From a browser, navigate to [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
2. <span data-ttu-id="512e0-177">Прокрутите список шаблонов вниз и выберите шаблон **101-vnet-two-subnets**.</span><span class="sxs-lookup"><span data-stu-id="512e0-177">Scroll down the list of templates, and click **101-vnet-two-subnets**.</span></span> <span data-ttu-id="512e0-178">Просмотрите файл **README.md** , который будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="512e0-178">Check the **README.md** file, as shown below.</span></span>

    ![Файл README.md в Github](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. <span data-ttu-id="512e0-180">Нажмите кнопку **Развернуть в Azure**.</span><span class="sxs-lookup"><span data-stu-id="512e0-180">Click **Deploy to Azure**.</span></span> <span data-ttu-id="512e0-181">При необходимости введите учетные данные для входа в Azure.</span><span class="sxs-lookup"><span data-stu-id="512e0-181">If necessary, enter your Azure login credentials.</span></span> 
4. <span data-ttu-id="512e0-182">В колонке **Параметры** введите значения, которые нужно использовать для создания новой виртуальной сети, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="512e0-182">In the **Parameters** blade, enter the values you want to use to create your new VNet, and then click **OK**.</span></span> <span data-ttu-id="512e0-183">На следующем рисунке показаны значения для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="512e0-183">The following figure shows the values for the scenario:</span></span>
   
    ![Параметры шаблона ARM](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. <span data-ttu-id="512e0-185">Выберите параметр **Группа ресурсов** и укажите группу ресурсов, в которую нужно добавить виртуальную сеть, или щелкните **Создать**, чтобы добавить виртуальную сеть в новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="512e0-185">Click **Resource group** and select a resource group to add the VNet to, or click **Create new** to add the VNet to a new resource group.</span></span> <span data-ttu-id="512e0-186">На следующем рисунке показаны параметры новой группы ресурсов с именем **TestRG**.</span><span class="sxs-lookup"><span data-stu-id="512e0-186">The following figure shows the resource group settings for a new resource group called **TestRG**:</span></span>

    ![Группа ресурсов](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. <span data-ttu-id="512e0-188">При необходимости измените параметры **Подписка** и **Расположение** для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="512e0-188">If necessary, change the **Subscription** and **Location** settings for your VNet.</span></span>
7. <span data-ttu-id="512e0-189">Если вы не хотите, чтобы виртуальная сеть отображалась в виде плитки на **начальной панели**, снимите флажок **Закрепить на начальной панели**.</span><span class="sxs-lookup"><span data-stu-id="512e0-189">If you do not want to see the VNet as a tile in the **Startboard**, disable **Pin to Startboard**.</span></span>
8. <span data-ttu-id="512e0-190">Щелкните **Условия**, ознакомьтесь с ними и примите их, нажав кнопку **Купить**.</span><span class="sxs-lookup"><span data-stu-id="512e0-190">Click **Legal terms**, read the terms, and click **Buy** to agree.</span></span> 
9. <span data-ttu-id="512e0-191">Щелкните **Создать**, чтобы создать виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="512e0-191">Click **Create** to create the VNet.</span></span>
   
    ![Отправка элемента развертывания в портал предварительной версии](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. <span data-ttu-id="512e0-193">Когда развертывание будет завершено, на портале Azure щелкните **Больше служб** и введите в появившемся поле фильтра *виртуальные сети*. Затем щелкните "Виртуальные сети", чтобы открыть соответствующую колонку.</span><span class="sxs-lookup"><span data-stu-id="512e0-193">Once the deployment is complete, in the Azure portal click **More services**, type *virtual networks* in the filter box that appears, then click Virtual networks to see the Virtual networks blade.</span></span> <span data-ttu-id="512e0-194">В этой колонке щелкните *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="512e0-194">In the blade, click *TestVNet*.</span></span> <span data-ttu-id="512e0-195">В колонке *TestVNet* выберите **Подсети**, чтобы просмотреть созданные подсети, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="512e0-195">In the *TestVNet* blade, click **Subnets** to see the created subnets, as shown in the following picture:</span></span>
    
     ![Создание виртуальной сети в портале предварительной версии](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a><span data-ttu-id="512e0-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="512e0-197">Next steps</span></span>

<span data-ttu-id="512e0-198">Инструкции по подключению:</span><span class="sxs-lookup"><span data-stu-id="512e0-198">Learn how to connect:</span></span>

- <span data-ttu-id="512e0-199">Сведения о подключении виртуальной машины к виртуальной сети см. в статье [Создание первой виртуальной машины Windows на портале Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md) или [Создание виртуальной машины Linux в Azure с помощью портала](../virtual-machines/linux/quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="512e0-199">A virtual machine (VM) to a virtual network by reading the [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="512e0-200">Вместо создания виртуальной сети и подсети с помощью действий, описанных в этой статье, виртуальную машину можно подключить к имеющейся виртуальной сети и подсети.</span><span class="sxs-lookup"><span data-stu-id="512e0-200">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="512e0-201">Сведения об установке подключения между виртуальными сетями см. в статье [Настройка подключения между виртуальными сетями на портале Azure](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="512e0-201">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="512e0-202">Сведения о подключении виртуальной сети к локальной сети с использованием виртуальной частной сети типа "сеть — сеть" или канала ExpressRoute см. в</span><span class="sxs-lookup"><span data-stu-id="512e0-202">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="512e0-203">[этой статье](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) и в статье [Связывание виртуальной сети с каналом ExpressRoute](../expressroute/expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="512e0-203">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
