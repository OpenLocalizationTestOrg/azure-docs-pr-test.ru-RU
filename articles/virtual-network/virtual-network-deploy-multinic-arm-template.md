---
title: "aaaCreate виртуальной Машины с несколькими сетевыми картами - шаблона диспетчера ресурсов Azure | Документы Microsoft"
description: "Создание виртуальной машины с несколькими сетевыми картами с помощью шаблона Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5d9ffcbd40c72dc18ae6de38e739eb5e45bf669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a>Создание виртуальной машины с несколькими сетевыми интерфейсами с помощью шаблона
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).  В этой статье описывается использование модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello [классической модели развертывания](virtual-network-deploy-multinic-classic-ps.md).
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Hello Далее используется группа ресурсов с именем *IaaSStory* hello веб-серверов и группу ресурсов с именем *IaaSStory серверной* hello DB серверов.

## <a name="prerequisites"></a>Предварительные требования
Перед созданием hello DB серверы, необходимо toocreate hello *IaaSStory* группы ресурсов со всеми ресурсами hello необходимые для этого сценария. завершить эти ресурсы toocreate hello следующие действия:

1. Перейдите в слишком[страницы шаблона hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).
2. На странице шаблона hello, toohello справа от **родительской группы ресурсов**, нажмите кнопку **развертывание tooAzure**.
3. При необходимости измените значения параметров hello, а затем выполните действия hello в группе ресурсов hello toodeploy портала предварительной версии Azure hello.

> [!IMPORTANT]
> Имена учетных записей хранения должны быть уникальными. Они не могут повторяться в Azure.
> 

## <a name="understand-hello-deployment-template"></a>Понять шаблон развертывания hello
Прежде чем развертывать hello шаблона, поставляемого с этой документации, убедитесь, что вы понимаете, что он делает. следующие шаги Hello предоставляют хороший обзор hello шаблона:

1. Перейдите в слишком[страницы шаблона hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).
2. Нажмите кнопку **azuredeploy.json** tooopen файл шаблона hello.
3. Обратите внимание hello *osType* параметров, перечисленных ниже. Этот параметр не используется tooselect параметры, относящиеся к какой toouse образ виртуальной Машины для сервера базы данных hello, наряду с несколькими операционной системы.

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS toouse for VMs: Windows or Ubuntu."
      }
    },
    ```

4. Прокрутите вниз список toohello переменных и проверить определение hello для hello **dbVMSetting** переменные, перечисленные ниже. Он получает один из элементов массива hello в hello **dbVMSettings** переменной. Если вы знакомы с терминологией разработки программного обеспечения, можно просмотреть hello **dbVMSettings** переменной как хэш-таблицу или словарь.

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. Предположим, что вы решите toodeploy виртуальных машин Windows под управлением SQL в серверной части hello. Затем hello значение **osType** бы *Windows*и hello **dbVMSetting** переменной будет содержать элемент hello, перечисленные ниже, который представляет первое значение hello hello **dbVMSettings** переменной.

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. Обратите внимание hello **vmSize** содержит значение hello *Standard_DS3*. Только некоторые размеры виртуальной Машины позволяют использовать несколько сетевых адаптеров hello. Чтобы узнать, какие размеры виртуальных Машин поддерживает несколько сетевых адаптеров, считывая hello [размеры виртуальных Машин Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) и [размеры виртуальных Машин Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) статей.

7. Прокрутите список вниз слишком**ресурсов** и первый элемент hello уведомления. Он описывает учетную запись хранения. Эта учетная запись хранения будет дисков данных используется toomaintain hello, используемой каждой базой данных виртуальной Машины. В этом сценарии у каждой виртуальной машины баз данных есть диск ОС, который размещен в обычном хранилище, и два диска данных, размещенных в хранилище SSD (хранилище класса Premium).

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. Прокрутите страницу вниз toohello следующего ресурса, приведенные ниже. Этот ресурс представляет hello сетевых Адаптеров используются для доступа к базе данных в каждой базе данных виртуальной Машины. Использование уведомления hello hello **копирования** функция в этом ресурсе. Hello шаблон позволяет toodeploy много виртуальных машин необходимо, на основе hello **dbCount** параметра. Следовательно, вы должны быть toocreate hello того же количества сетевых адаптеров для доступа к базе данных, один для каждой виртуальной Машины.

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. Прокрутите страницу вниз toohello следующего ресурса, приведенные ниже. Этот ресурс представляет hello сетевых Адаптеров используются для управления в каждой базе данных виртуальной Машины. Опять же, для каждой виртуальной машины баз данных необходимо иметь один из этих сетевых адаптеров. Обратите внимание hello **networkSecurityGroup** элемент, связывание NSG, который позволяет доступ toothis tooRDP/SSH сетевой Адаптер только.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. Прокрутите страницу вниз toohello следующего ресурса, приведенные ниже. Этот ресурс представляет toobe набор доступности совместно используется всеми виртуальными машинами базы данных. Таким образом, вы гарантирует, что всегда будет существовать одна виртуальная машина в hello задать во время обслуживания.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. Прокрутите вниз toohello следующего ресурса. Этот ресурс представляет hello базы данных виртуальных машин, как показано в hello первые несколько строк, перечисленных ниже. Использование уведомления hello hello **копирования** функция, гарантируя, что создаются несколько виртуальных машин на основании hello **dbCount** параметра. Также Обратите внимание, hello **dependsOn** коллекции. В нем перечислены два сетевых адаптера, необходимые toobe создан до hello, развернутых виртуальных Машин вместе с набор доступности hello и hello учетной записи хранилища.

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. Прокрутите вниз toohello ресурсов виртуальной Машины hello **параметров масштабирования виртуальных** элемента, как показано ниже. Обратите внимание, что для каждой виртуальной машины используются два сетевых адаптера. При создании нескольких сетевых адаптеров для виртуальной Машины, необходимо задать hello **основной** свойство одного из сетевых адаптеров hello слишком*true*, и hello rest слишком*false*.

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a>Развертывание с помощью шаблона hello ARM щелкните toodeploy

> [!IMPORTANT]
> Убедитесь, что вы выполните hello [предварительным](#Pre-requisites) действия, прежде чем следовать приведенным ниже инструкциям hello.
> 

шаблон Образец Hello доступны в репозитории открытого hello использует параметр файл, содержащий сценарий hello по умолчанию значения, используемые toogenerate hello, описанный выше. toodeploy это с помощью шаблона щелкните toodeploy, выполните [эту ссылку](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello справа от **внутренний ресурс группы (см. документацию)** щелкните **развертывание tooAzure**, замените Здравствуйте, значения параметров по умолчанию, при необходимости и следуйте инструкциям hello hello портала.

на следующем рисунке Hello показано содержимое hello hello группы ресурсов, после развертывания.

![Внутренняя группа ресурсов](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a>Развертывание hello шаблона с помощью PowerShell
шаблон toodeploy hello, загруженный с помощью PowerShell, установите и настройте PowerShell, выполнив шаги hello в hello [установите и настройте PowerShell](/powershell/azure/overview) статьи, а затем выполните следующие шаги hello:

Запустите hello  **`New-AzureRmResourceGroup`**  toocreate командлет группы ресурсов с помощью hello шаблона.

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

Ожидаемые выходные данные:

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Развертывание hello шаблона с помощью hello Azure CLI
toodeploy hello шаблона с использованием hello Azure CLI, выполните шаги hello.

1. Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.
2. Запустите hello  **`azure config mode`**  tooswitch tooResource Manager режим команд, как показано ниже.

    ```azurecli
    azure config mode arm
    ```

    Hello ожидается вывод следующим образом:

        info:    New mode is arm

3. Откройте hello [файл параметров](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), выберите его содержимое и сохраните файл tooa на своем компьютере. В этом примере мы сохранить файл параметров hello слишком*parameters.json*.
4. Запустите hello  **`azure group deployment create`**  файлы новой виртуальной сети с помощью шаблонов hello и параметров командлета toodeploy hello вы загрузили и изменить выше. Список Hello отображаться после вывода hello объясняется hello параметров, используемых.

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    Ожидаемые выходные данные:
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

