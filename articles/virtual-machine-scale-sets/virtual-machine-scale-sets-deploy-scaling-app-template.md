---
title: "aaaDeploy приложения для набора масштабирования виртуальной машины Azure | Документы Microsoft"
description: "Узнайте, toodeploy простой автоматического масштабирования приложения на наборе с помощью шаблона Azure Resource Manager масштабирования виртуальной машины."
services: virtual-machine-scale-sets
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 6fccc310312cabfcdddfcbcd2d154fc5cc440417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-autoscaling-app-using-a-template"></a>Развертывание приложения автомасштабирования с помощью шаблона

[Шаблоны Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) — toodeploy хорошим способом группы связанных ресурсов. Этот учебник построен на [развернуть набор простых масштабирования](virtual-machine-scale-sets-mvss-start.md) и описывает, как toodeploy задать с помощью шаблона Azure Resource Manager простой автоматического масштабирования приложения на шкале.  Можно также настроить автоматическое масштабирование с помощью PowerShell, CLI или портала hello. Дополнительные сведения см. в разделе [Как использовать автомасштабирование и масштабируемые наборы виртуальных машин](virtual-machine-scale-sets-autoscale-overview.md).

## <a name="two-quickstart-templates"></a>Два шаблона быстрого запуска
При развертывании масштабируемого набора вы можете установить новое программное обеспечение в образ платформы, используя [расширения виртуальной машины](../virtual-machines/virtual-machines-windows-extensions-features.md). Расширение виртуальной машины — это небольшое приложение, которое выполняет задачи настройки и автоматизации после развертывания виртуальных машин Azure, таких как развертывание приложения. Два разных образцах приведены в [Azure/azure-quickstart шаблоны](https://github.com/Azure/azure-quickstart-templates) которого Показать, как toodeploy автоматического масштабирования приложения на шкале задать использование расширений ВМ.

### <a name="python-http-server-on-linux"></a>HTTP-сервер Python под управлением Linux
Hello [Python HTTP-сервера в Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) образец шаблона развертывает простой автоматического масштабирования приложения, работающего в наборе масштабирования Linux.  [Фляга для](http://bottlepy.org/docs/dev/), Python веб-framework и простого сервера HTTP, развернутых на каждой виртуальной Машины в hello масштабирования, заданные с помощью пользовательского скрипта расширения виртуальной Машины. Масштаб Hello настроить шкал среднее использование ЦП для всех виртуальных машин превышает 60%, а масштабируется, если hello средняя загрузка ЦП составляет менее 30%.

В дополнение к этому toohello набора масштабирования ресурсов, hello *azuredeploy.json* образец шаблона также объявляет виртуальной сети, общедоступный IP-адрес, балансировки нагрузки и ресурсов параметров автоматического масштабирования.  Дополнительные сведения о создании ресурсов в шаблоне см. в статье [Автоматическое масштабирование машин Linux в наборе масштабирования виртуальных машин](virtual-machine-scale-sets-linux-autoscale.md).

В hello *azuredeploy.json* шаблон, hello `extensionProfile` свойство hello `Microsoft.Compute/virtualMachineScaleSets` ресурс определяет расширение пользовательского скрипта. `fileUris`Указывает расположение пошагового hello. В этом случае двух файлов: *workserver.py*, который определяет простой HTTP-сервера, и *installserver.sh*, которая устанавливается бутылка и запускает hello HTTP-сервера. `commandToExecute`Указывает команду toorun hello после развертывания hello набора масштабирования.

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "lapextension",
                "properties": {
                  "publisher": "Microsoft.Azure.Extensions",
                  "type": "CustomScript",
                  "typeHandlerVersion": "2.0",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "fileUris": [
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
                    ],
                    "commandToExecute": "bash installserver.sh"
                  }
                }
              }
            ]
          }
```

### <a name="aspnet-mvc-application-on-windows"></a>Приложение ASP.NET MVC для Windows
Hello [приложение ASP.NET MVC в Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) образец шаблона развертывает простое приложение ASP.NET MVC, работающего в IIS на набор масштабирования Windows.  Службы IIS и hello приложения MVC развертываются с помощью hello [PowerShell настройкой требуемого состояния (DSC)](virtual-machine-scale-sets-dsc.md) расширения виртуальной Машины.  Масштаб Hello Настройка шкал (на экземпляре виртуальной Машины одновременно) Если загрузка ЦП больше 50% 5 минут. 

В дополнение к этому toohello набора масштабирования ресурсов, hello *azuredeploy.json* образец шаблона также объявляет виртуальной сети, общедоступный IP-адрес, балансировки нагрузки и ресурсов параметров автоматического масштабирования. В этом шаблоне также показано обновление приложения.  Дополнительные сведения о создании ресурсов в шаблоне см. в статье [Автоматическое масштабирование ВМ в наборе масштабирования ВМ](virtual-machine-scale-sets-windows-autoscale.md).

В hello *azuredeploy.json* шаблон, hello `extensionProfile` свойство hello `Microsoft.Compute/virtualMachineScaleSets` ресурс определяет [конфигурации требуемого состояния (DSC)](virtual-machine-scale-sets-dsc.md) расширения, которая устанавливает службы IIS и значение по умолчанию веб-приложение из пакета WebDeploy.  Hello *IISInstall.ps1* сценарий Установка служб IIS на виртуальной машине hello и находится в hello *DSC* папки.  веб-приложение MVC Hello находится в hello *WebDeploy* папки.  сценарий установки toohello пути Hello и веб-приложения hello определяются в hello `powershelldscZip` и `webDeployPackage` параметров в hello *azuredeploy.parameters.json* файла. 

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Powershell.DSC",
                "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.9",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('powershelldscUpdateTagVersion')]",
                  "settings": {
                    "configuration": {
                      "url": "[variables('powershelldscZipFullPath')]",
                      "script": "IISInstall.ps1",
                      "function": "InstallIIS"
                    },
                    "configurationArguments": {
                      "nodeName": "localhost",
                      "WebDeployPackagePath": "[variables('webDeployPackageFullPath')]"
                    }
                  }
                }
              }
            ]
          }
```

## <a name="deploy-hello-template"></a>Развертывание шаблона hello
Hello простейший способ toodeploy hello [Python HTTP-сервера в Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) или [приложение ASP.NET MVC в Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) шаблона — toouse hello **развертывание tooAzure** кнопка найдена в hello в файлах readme hello в GitHub.  Также можно использовать PowerShell или Azure CLI toodeploy hello образцы шаблонов.

### <a name="powershell"></a>PowerShell
Копировать hello [Python HTTP-сервера в Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) или [приложение ASP.NET MVC в Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) файлы из папки tooa репозитория GitHub hello на локальном компьютере.  Откройте hello *azuredeploy.parameters.json* файла и обновление значения по умолчанию hello объекта hello `vmssName`, `adminUsername`, и `adminPassword` параметров. Сохраните следующий сценарий PowerShell слишком hello*deploy.ps1* в hello же папке, что hello *azuredeploy.json* шаблона. hello шаблона запустите образец hello toodeploy *deploy.ps1* сценарий в командном окне PowerShell.

```powershell
param(
 [Parameter(Mandatory=$True)]
 [string]
 $subscriptionId,

 [Parameter(Mandatory=$True)]
 [string]
 $resourceGroupName,

 [string]
 $resourceGroupLocation,

 [Parameter(Mandatory=$True)]
 [string]
 $deploymentName,

 [string]
 $templateFilePath = "template.json",

 [string]
 $parametersFilePath = "parameters.json"
)

<#
.SYNOPSIS
    Registers RPs
#>
Function RegisterRP {
    Param(
        [string]$ResourceProviderNamespace
    )

    Write-Host "Registering resource provider '$ResourceProviderNamespace'";
    Register-AzureRmResourceProvider -ProviderNamespace $ResourceProviderNamespace;
}

#******************************************************************************
# Script body
# Execution begins here
#******************************************************************************
$ErrorActionPreference = "Stop"

# sign in
Write-Host "Logging in...";
Login-AzureRmAccount;

# select subscription
Write-Host "Selecting subscription '$subscriptionId'";
Select-AzureRmSubscription -SubscriptionID $subscriptionId;

# Register RPs
$resourceProviders = @("microsoft.compute","microsoft.insights","microsoft.network");
if($resourceProviders.length) {
    Write-Host "Registering resource providers"
    foreach($resourceProvider in $resourceProviders) {
        RegisterRP($resourceProvider);
    }
}

#Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $resourceGroupName -ErrorAction SilentlyContinue
if(!$resourceGroup)
{
    Write-Host "Resource group '$resourceGroupName' does not exist. toocreate a new resource group, please enter a location.";
    if(!$resourceGroupLocation) {
        $resourceGroupLocation = Read-Host "resourceGroupLocation";
    }
    Write-Host "Creating resource group '$resourceGroupName' in location '$resourceGroupLocation'";
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else{
    Write-Host "Using existing resource group '$resourceGroupName'";
}

# Start hello deployment
Write-Host "Starting deployment...";
if(Test-Path $parametersFilePath) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath -TemplateParameterFile $parametersFilePath;
} else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath;
}
```

### <a name="azure-cli"></a>Инфраструктура CLI Azure
```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely toocause confusing bugs when looping arrays or arguments (e.g. $@)

usage() { echo "Usage: $0 -i <subscriptionId> -g <resourceGroupName> -n <deploymentName> -l <resourceGroupLocation>" 1>&2; exit 1; }

declare subscriptionId=""
declare resourceGroupName=""
declare deploymentName=""
declare resourceGroupLocation=""

# Initialize parameters specified from command line
while getopts ":i:g:n:l:" arg; do
    case "${arg}" in
        i)
            subscriptionId=${OPTARG}
            ;;
        g)
            resourceGroupName=${OPTARG}
            ;;
        n)
            deploymentName=${OPTARG}
            ;;
        l)
            resourceGroupLocation=${OPTARG}
            ;;
        esac
done
shift $((OPTIND-1))

#Prompt for parameters is some required parameters are missing
if [[ -z "$subscriptionId" ]]; then
    echo "Subscription Id:"
    read subscriptionId
    [[ "${subscriptionId:?}" ]]
fi

if [[ -z "$resourceGroupName" ]]; then
    echo "ResourceGroupName:"
    read resourceGroupName
    [[ "${resourceGroupName:?}" ]]
fi

if [[ -z "$deploymentName" ]]; then
    echo "DeploymentName:"
    read deploymentName
fi

if [[ -z "$resourceGroupLocation" ]]; then
    echo "Enter a location below toocreate a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file toobe used
templateFilePath="template.json"

if [ ! -f "$templateFilePath" ]; then
    echo "$templateFilePath not found"
    exit 1
fi

#parameter file path
parametersFilePath="parameters.json"

if [ ! -f "$parametersFilePath" ]; then
    echo "$parametersFilePath not found"
    exit 1
fi

if [ -z "$subscriptionId" ] || [ -z "$resourceGroupName" ] || [ -z "$deploymentName" ]; then
    echo "Either one of subscriptionId, resourceGroupName, deploymentName is empty"
    usage
fi

#login tooazure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set hello default subscription id
az account set --name $subscriptionId

set +e

#Check for existing RG
az group show $resourceGroupName 1> /dev/null

if [ $? != 0 ]; then
    echo "Resource group with name" $resourceGroupName "could not be found. Creating new resource group.."
    set -e
    (
        set -x
        az group create --name $resourceGroupName --location $resourceGroupLocation 1> /dev/null
    )
    else
    echo "Using existing resource group..."
fi

#Start deployment
echo "Starting deployment..."
(
    set -x
    az group deployment create --name $deploymentName --resource-group $resourceGroupName --template-file $templateFilePath --parameters $parametersFilePath
)

if [ $?  == 0 ];
 then
    echo "Template has been successfully deployed"
fi
```

## <a name="next-steps"></a>Дальнейшие действия

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
