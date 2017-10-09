---
title: "aaaCreate виртуальную Машину с статический общедоступный IP-адрес - шаблона диспетчера ресурсов Azure | Документы Microsoft"
description: "Узнайте, как toocreate виртуальную Машину с статический общедоступный IP-адрес решения с помощью шаблона диспетчера ресурсов Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d551085a-c7ed-4ec6-b4c3-e9e1cebb774c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a8640ed4fad06b0e09820e6114fd6789db73847
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a>Создание виртуальной машины со статическим общедоступным IP-адресом с помощью шаблона Azure Resource Manager

> [!div class="op_single_selector"]
> * [Портал Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Интерфейс командной строки Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [Шаблон](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (классическая модель)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md). В этой статье описан с помощью модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello классической модели развертывания.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a>Ресурсы общедоступного IP-адреса в файле шаблона
Можно просматривать и загружать hello [образец шаблона](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).

Hello ниже показано определение hello hello открытый IP ресурсу на основе hello сценарии выше:

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('webVMSetting').pipName]",
  "location": "[variables('location')]",
  "properties": {
    "publicIPAllocationMethod": "Static"
  },
  "tags": {
    "displayName": "PublicIPAddress - Web"
  }
},
```

Обратите внимание hello **publicIPAllocationMethod** свойство, которое задано слишком*статических*. Это свойство может иметь значение либо *Dynamic* (значение по умолчанию), либо *Static*. Настройка toostatic гарантии, которые никогда не изменяют общий IP-адрес hello.

Hello следующем разделе показано сопоставление hello hello общедоступного IP-адреса с сетевым интерфейсом:

```json
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('webVMSetting').nicName]",
    "location": "[variables('location')]",
    "tags": {
    "displayName": "NetworkInterface - Web"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('webVMSetting').pipName)]",
      "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
          "privateIPAllocationMethod": "Static",
          "privateIPAddress": "[variables('webVMSetting').ipAddress]",
          "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('webVMSetting').pipName)]"
          },
          "subnet": {
            "id": "[variables('frontEndSubnetRef')]"
          }
        }
      }
    ]
  }
},
```

Обратите внимание hello **publicIPAddress** свойство, указывающее toohello **идентификатор** ресурс с именем **variables('webVMSetting').pipName**. Это имя hello открытый IP-ресурс hello показано выше.

Наконец, выше hello сетевой интерфейс указан в hello **параметров масштабирования виртуальных** свойство hello создаваемой виртуальной Машины.

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Развертывание с помощью шаблона hello щелкните toodeploy

шаблон Образец Hello доступны в репозитории открытого hello использует параметр файл, содержащий сценарий hello по умолчанию значения, используемые toogenerate hello, описанный выше. toodeploy это с помощью шаблона щелкните toodeploy, нажмите кнопку **развертывание tooAzure** в файле Readme.md hello для hello [виртуальной Машины с помощью статических PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) шаблона. При необходимости замените значения параметров по умолчанию hello и введите значения для параметров пустой hello.  Следуйте инструкциям hello hello портала toocreate виртуальную машину с статический общедоступный IP-адрес.

## <a name="deploy-hello-template-by-using-powershell"></a>Развертывание hello шаблона с помощью PowerShell

toodeploy hello шаблона, загруженного с помощью PowerShell, выполните шаги hello.

1. Если ранее не пользовались Azure PowerShell, hello завершения шагов в hello [как tooInstall и настройка Azure PowerShell](/powershell/azure/overview) статьи.
2. В консоли PowerShell запустите hello `New-AzureRmResourceGroup` toocreate командлета новую группу ресурсов, при необходимости. Если уже созданы группы ресурсов, воспользуйтесь toostep 3.

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    Ожидаемые выходные данные:
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. В консоли PowerShell запустите hello `New-AzureRmResourceGroupDeployment` шаблон hello toodeploy командлета.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    Ожидаемые выходные данные:
   
        DeploymentName    : DeployVM
        ResourceGroupName : PIPTEST
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
                            Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/mas
                            ter/IaaS-Story/03-Static-public-IP/azuredeploy.json
                            ContentVersion : 1.0.0.0
   
        Parameters        :
                            Name                      Type                       Value     
                            ========================  =========================  ==========
                            vnetName                  String                     WTestVNet
                            vnetPrefix                String                     192.168.0.0/16
                            frontEndSubnetName        String                     FrontEnd  
                            frontEndSubnetPrefix      String                     192.168.1.0/24
                            storageAccountNamePrefix  String                     iaasestd  
                            stdStorageType            String                     Standard_LRS
                            osType                    String                     Windows   
                            adminUsername             String                     adminUser
                            adminPassword             SecureString                         
   
        Outputs           :

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Развертывание hello шаблона с помощью hello Azure CLI
toodeploy hello шаблона с использованием hello Azure CLI, полный hello, следующие шаги:

1. Если ранее не пользовались Azure CLI, выполните действия hello в hello [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) статью tooinstall и настройте его.
2. Запустите hello `azure config mode` tooswitch tooResource Manager режим команд, как показано ниже.

    ```azurecli
    azure config mode arm
    ```

    Hello ожидаемый результат для приведенных выше команд hello:

        info:    New mode is arm

3. Откройте hello [файл параметров](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), выберите его содержимое и сохраните файл tooa на своем компьютере. В этом примере hello параметры сохраняются в файл tooa с именем *parameters.json*. Изменить значения параметров hello в файле hello, при необходимости, но как минимум, рекомендуется установить значение hello для hello adminPassword параметр tooa уникальный сложный пароль.
4. Запустите hello `azure group deployment create` файлов новой виртуальной сети с помощью шаблона hello и параметр cmd toodeploy hello вы загрузили и изменить выше. В следующей команде hello, замените <path> hello путь был сохранен файл hello для. 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    Ожидаемый результат (перечисляются используемые значения параметров):

        info:    Executing command group create
        + Getting resource group PIPTEST2
        + Creating resource group PIPTEST2
        info:    Created resource group PIPTEST2
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/PIPTEST2
        data:    Name:                PIPTEST2
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

