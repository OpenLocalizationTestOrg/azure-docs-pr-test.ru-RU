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
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a>Создание виртуальной машины Windows с использованием шаблона Resource Manager

В этой статье показано, как диспетчер ресурсов Azure toodeploy шаблона с помощью PowerShell. Hello шаблон, который вы создаете развертывает одной виртуальной машины под управлением Windows Server в новую виртуальную сеть с одной подсетью.

Подробное описание hello ресурса виртуальной машины см. в разделе [виртуальные машины в шаблоне Azure Resource Manager](template-description.md). Дополнительные сведения обо всех ресурсах hello в шаблоне см. в разделе [Пошаговое руководство шаблона Azure Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Занимает около пяти минут, toodo hello шаги в этой статье.

## <a name="install-azure-powershell"></a>Установка Azure PowerShell

В разделе [как tooinstall и настройка Azure PowerShell](../../powershell-install-configure.md) сведения об установке hello последнюю версию Azure PowerShell, выбрав подписку и вход в учетную запись tooyour.

## <a name="create-a-resource-group"></a>Создание группы ресурсов

Все ресурсы должны развертываться в [группе ресурсов](../../azure-resource-manager/resource-group-overview.md).

1. Получите список доступных расположений, где можно создавать ресурсы.
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. Создание группы ресурсов hello в выбранного расположения hello. Этот пример показывает создание hello группы ресурсов с именем **myResourceGroup** в hello **Запад США** расположение:

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-hello-files"></a>Создание файлов hello

На этом шаге создается файл шаблона, которая развертывает hello ресурсы и файл параметров, который предоставляет шаблон toohello значения параметра. Можно также создать файла авторизации, который является используется tooperform операции диспетчера ресурсов Azure.

1. Создайте файл с именем *CreateVMTemplate.json* и добавьте этот tooit код JSON:

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

2. Создайте файл с именем *Parameters.json* и добавьте этот tooit код JSON:

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

3. Создайте учетную запись хранения и контейнер:

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. Отправьте файлы для hello toohello учетной записи хранилища.

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    Изменение hello - расположение toohello пути файла, где хранятся файлы hello.

## <a name="create-hello-resources"></a>Создать ресурсы hello

Развертывание шаблона hello, используя параметры hello:

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> Шаблоны и параметры можно также развернуть из локальных файлов. toolearn более, в разделе [с помощью Azure PowerShell с хранилищем Azure](../../storage/common/storage-powershell-guide-full.md).

## <a name="next-steps"></a>Дальнейшие действия

- Если возникли проблемы с развертыванием hello, может потребоваться рассмотреть [Устранение общих ошибок развертывания Azure с помощью диспетчера ресурсов Azure](../../resource-manager-common-deployment-errors.md).
- Узнайте, как toocreate и управлять ими на виртуальной машине в [Создание и управление виртуальными машинами Windows с помощью модуля Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

