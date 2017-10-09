---
title: "aaaCreate Windows виртуальной Машины из шаблона в Azure | Документы Microsoft"
description: "Использование шаблона диспетчера ресурсов и PowerShell tooeasily создания новой виртуальной Машины Windows."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19129d61-8c04-4aa9-a01f-361a09466805
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 630111482c7dc046091632e2ed458ac143325d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a><span data-ttu-id="6456f-103">Создание виртуальной машины Windows с использованием шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6456f-103">Create a Windows virtual machine from a Resource Manager template</span></span>

<span data-ttu-id="6456f-104">В этой статье показано, как диспетчер ресурсов Azure toodeploy шаблона с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6456f-104">This article shows you how toodeploy an Azure Resource Manager template using PowerShell.</span></span> <span data-ttu-id="6456f-105">Hello шаблон, который вы создаете развертывает одной виртуальной машины под управлением Windows Server в новую виртуальную сеть с одной подсетью.</span><span class="sxs-lookup"><span data-stu-id="6456f-105">hello template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="6456f-106">Подробное описание hello ресурса виртуальной машины см. в разделе [виртуальные машины в шаблоне Azure Resource Manager](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="6456f-106">For a detailed description of hello virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="6456f-107">Дополнительные сведения обо всех ресурсах hello в шаблоне см. в разделе [Пошаговое руководство шаблона Azure Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="6456f-107">For more information about all hello resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="6456f-108">Занимает около пяти минут, toodo hello шаги в этой статье.</span><span class="sxs-lookup"><span data-stu-id="6456f-108">It should take about five minutes toodo hello steps in this article.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="6456f-109">Установка Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6456f-109">Install Azure PowerShell</span></span>

<span data-ttu-id="6456f-110">В разделе [как tooinstall и настройка Azure PowerShell](../../powershell-install-configure.md) сведения об установке hello последнюю версию Azure PowerShell, выбрав подписку и вход в учетную запись tooyour.</span><span class="sxs-lookup"><span data-stu-id="6456f-110">See [How tooinstall and configure Azure PowerShell](../../powershell-install-configure.md) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="6456f-111">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="6456f-111">Create a resource group</span></span>

<span data-ttu-id="6456f-112">Все ресурсы должны развертываться в [группе ресурсов](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6456f-112">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="6456f-113">Получите список доступных расположений, где можно создавать ресурсы.</span><span class="sxs-lookup"><span data-stu-id="6456f-113">Get a list of available locations where resources can be created.</span></span>
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. <span data-ttu-id="6456f-114">Создание группы ресурсов hello в выбранного расположения hello.</span><span class="sxs-lookup"><span data-stu-id="6456f-114">Create hello resource group in hello location that you select.</span></span> <span data-ttu-id="6456f-115">Этот пример показывает создание hello группы ресурсов с именем **myResourceGroup** в hello **Запад США** расположение:</span><span class="sxs-lookup"><span data-stu-id="6456f-115">This example shows hello creation of a resource group named **myResourceGroup** in hello **West US** location:</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-hello-files"></a><span data-ttu-id="6456f-116">Создание файлов hello</span><span class="sxs-lookup"><span data-stu-id="6456f-116">Create hello files</span></span>

<span data-ttu-id="6456f-117">На этом шаге создается файл шаблона, которая развертывает hello ресурсы и файл параметров, который предоставляет шаблон toohello значения параметра.</span><span class="sxs-lookup"><span data-stu-id="6456f-117">In this step, you create a template file that deploys hello resources and a parameters file that supplies parameter values toohello template.</span></span> <span data-ttu-id="6456f-118">Можно также создать файла авторизации, который является используется tooperform операции диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="6456f-118">You also create an authorization file that is used tooperform Azure Resource Manager operations.</span></span>

1. <span data-ttu-id="6456f-119">Создайте файл с именем *CreateVMTemplate.json* и добавьте этот tooit код JSON:</span><span class="sxs-lookup"><span data-stu-id="6456f-119">Create a file named *CreateVMTemplate.json* and add this JSON code tooit:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

2. <span data-ttu-id="6456f-120">Создайте файл с именем *Parameters.json* и добавьте этот tooit код JSON:</span><span class="sxs-lookup"><span data-stu-id="6456f-120">Create a file named *Parameters.json* and add this JSON code tooit:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

3. <span data-ttu-id="6456f-121">Создайте учетную запись хранения и контейнер:</span><span class="sxs-lookup"><span data-stu-id="6456f-121">Create a new storage account and container:</span></span>

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. <span data-ttu-id="6456f-122">Отправьте файлы для hello toohello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="6456f-122">Upload hello files toohello storage account:</span></span>

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    <span data-ttu-id="6456f-123">Изменение hello - расположение toohello пути файла, где хранятся файлы hello.</span><span class="sxs-lookup"><span data-stu-id="6456f-123">Change hello -File paths toohello location where you stored hello files.</span></span>

## <a name="create-hello-resources"></a><span data-ttu-id="6456f-124">Создать ресурсы hello</span><span class="sxs-lookup"><span data-stu-id="6456f-124">Create hello resources</span></span>

<span data-ttu-id="6456f-125">Развертывание шаблона hello, используя параметры hello:</span><span class="sxs-lookup"><span data-stu-id="6456f-125">Deploy hello template using hello parameters:</span></span>

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> <span data-ttu-id="6456f-126">Шаблоны и параметры можно также развернуть из локальных файлов.</span><span class="sxs-lookup"><span data-stu-id="6456f-126">You can also deploy templates and parameters from local files.</span></span> <span data-ttu-id="6456f-127">toolearn более, в разделе [с помощью Azure PowerShell с хранилищем Azure](../../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="6456f-127">toolearn more, see [Using Azure PowerShell with Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6456f-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6456f-128">Next Steps</span></span>

- <span data-ttu-id="6456f-129">Если возникли проблемы с развертыванием hello, может потребоваться рассмотреть [Устранение общих ошибок развертывания Azure с помощью диспетчера ресурсов Azure](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="6456f-129">If there were issues with hello deployment, you might take a look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="6456f-130">Узнайте, как toocreate и управлять ими на виртуальной машине в [Создание и управление виртуальными машинами Windows с помощью модуля Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6456f-130">Learn how toocreate and manage a virtual machine in [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

