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
# <a name="deploy-an-autoscaling-app-using-a-template"></a><span data-ttu-id="c1f67-103">Развертывание приложения автомасштабирования с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="c1f67-103">Deploy an autoscaling app using a template</span></span>

<span data-ttu-id="c1f67-104">[Шаблоны Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) — toodeploy хорошим способом группы связанных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c1f67-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="c1f67-105">Этот учебник построен на [развернуть набор простых масштабирования](virtual-machine-scale-sets-mvss-start.md) и описывает, как toodeploy задать с помощью шаблона Azure Resource Manager простой автоматического масштабирования приложения на шкале.</span><span class="sxs-lookup"><span data-stu-id="c1f67-105">This tutorial builds on [Deploy a simple scale set](virtual-machine-scale-sets-mvss-start.md) and describes how toodeploy a simple autoscaling application on a scale set using an Azure Resource Manager template.</span></span>  <span data-ttu-id="c1f67-106">Можно также настроить автоматическое масштабирование с помощью PowerShell, CLI или портала hello.</span><span class="sxs-lookup"><span data-stu-id="c1f67-106">You can also set up autoscaling using PowerShell, CLI, or hello portal.</span></span> <span data-ttu-id="c1f67-107">Дополнительные сведения см. в разделе [Как использовать автомасштабирование и масштабируемые наборы виртуальных машин](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c1f67-107">For more information, see [Autoscale overview](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

## <a name="two-quickstart-templates"></a><span data-ttu-id="c1f67-108">Два шаблона быстрого запуска</span><span class="sxs-lookup"><span data-stu-id="c1f67-108">Two quickstart templates</span></span>
<span data-ttu-id="c1f67-109">При развертывании масштабируемого набора вы можете установить новое программное обеспечение в образ платформы, используя [расширения виртуальной машины](../virtual-machines/virtual-machines-windows-extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="c1f67-109">When you deploy a scale set you can install new software on a platform image using a [VM Extension](../virtual-machines/virtual-machines-windows-extensions-features.md).</span></span> <span data-ttu-id="c1f67-110">Расширение виртуальной машины — это небольшое приложение, которое выполняет задачи настройки и автоматизации после развертывания виртуальных машин Azure, таких как развертывание приложения.</span><span class="sxs-lookup"><span data-stu-id="c1f67-110">A VM extension is a small application that provides post-deployment configuration and automation tasks on Azure virtual machines, such as deploying an app.</span></span> <span data-ttu-id="c1f67-111">Два разных образцах приведены в [Azure/azure-quickstart шаблоны](https://github.com/Azure/azure-quickstart-templates) которого Показать, как toodeploy автоматического масштабирования приложения на шкале задать использование расширений ВМ.</span><span class="sxs-lookup"><span data-stu-id="c1f67-111">Two different sample templates are provided in [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) which show how toodeploy an autoscaling application onto a scale set using VM extensions.</span></span>

### <a name="python-http-server-on-linux"></a><span data-ttu-id="c1f67-112">HTTP-сервер Python под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="c1f67-112">Python HTTP server on Linux</span></span>
<span data-ttu-id="c1f67-113">Hello [Python HTTP-сервера в Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) образец шаблона развертывает простой автоматического масштабирования приложения, работающего в наборе масштабирования Linux.</span><span class="sxs-lookup"><span data-stu-id="c1f67-113">hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) sample template deploys a simple autoscaling application running on a Linux scale set.</span></span>  <span data-ttu-id="c1f67-114">[Фляга для](http://bottlepy.org/docs/dev/), Python веб-framework и простого сервера HTTP, развернутых на каждой виртуальной Машины в hello масштабирования, заданные с помощью пользовательского скрипта расширения виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="c1f67-114">[Bottle](http://bottlepy.org/docs/dev/), a Python web framework, and a simple HTTP server are deployed on each VM in hello scale set using a custom script VM extension.</span></span> <span data-ttu-id="c1f67-115">Масштаб Hello настроить шкал среднее использование ЦП для всех виртуальных машин превышает 60%, а масштабируется, если hello средняя загрузка ЦП составляет менее 30%.</span><span class="sxs-lookup"><span data-stu-id="c1f67-115">hello scale set scales up when average CPU utilization across all VMs is greater than 60% and scales down when hello average CPU utilization is less than 30%.</span></span>

<span data-ttu-id="c1f67-116">В дополнение к этому toohello набора масштабирования ресурсов, hello *azuredeploy.json* образец шаблона также объявляет виртуальной сети, общедоступный IP-адрес, балансировки нагрузки и ресурсов параметров автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="c1f67-116">In addition toohello scale set resource, hello *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span>  <span data-ttu-id="c1f67-117">Дополнительные сведения о создании ресурсов в шаблоне см. в статье [Автоматическое масштабирование машин Linux в наборе масштабирования виртуальных машин](virtual-machine-scale-sets-linux-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="c1f67-117">For more information on creating these resources in a template, see [Linux scale set with autoscale](virtual-machine-scale-sets-linux-autoscale.md).</span></span>

<span data-ttu-id="c1f67-118">В hello *azuredeploy.json* шаблон, hello `extensionProfile` свойство hello `Microsoft.Compute/virtualMachineScaleSets` ресурс определяет расширение пользовательского скрипта.</span><span class="sxs-lookup"><span data-stu-id="c1f67-118">In hello *azuredeploy.json* template, hello `extensionProfile` property of hello `Microsoft.Compute/virtualMachineScaleSets` resource specifies a custom script extension.</span></span> <span data-ttu-id="c1f67-119">`fileUris`Указывает расположение пошагового hello.</span><span class="sxs-lookup"><span data-stu-id="c1f67-119">`fileUris` specifies hello script(s) location.</span></span> <span data-ttu-id="c1f67-120">В этом случае двух файлов: *workserver.py*, который определяет простой HTTP-сервера, и *installserver.sh*, которая устанавливается бутылка и запускает hello HTTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="c1f67-120">In this case, two files: *workserver.py*, which defines a simple HTTP server, and *installserver.sh*, which installs Bottle and starts hello HTTP server.</span></span> <span data-ttu-id="c1f67-121">`commandToExecute`Указывает команду toorun hello после развертывания hello набора масштабирования.</span><span class="sxs-lookup"><span data-stu-id="c1f67-121">`commandToExecute` specifies hello command toorun after hello scale set has been deployed.</span></span>

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

### <a name="aspnet-mvc-application-on-windows"></a><span data-ttu-id="c1f67-122">Приложение ASP.NET MVC для Windows</span><span class="sxs-lookup"><span data-stu-id="c1f67-122">ASP.NET MVC application on Windows</span></span>
<span data-ttu-id="c1f67-123">Hello [приложение ASP.NET MVC в Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) образец шаблона развертывает простое приложение ASP.NET MVC, работающего в IIS на набор масштабирования Windows.</span><span class="sxs-lookup"><span data-stu-id="c1f67-123">hello [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) sample template deploys a simple ASP.NET MVC app running in IIS on Windows scale set.</span></span>  <span data-ttu-id="c1f67-124">Службы IIS и hello приложения MVC развертываются с помощью hello [PowerShell настройкой требуемого состояния (DSC)](virtual-machine-scale-sets-dsc.md) расширения виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="c1f67-124">IIS and hello MVC app are deployed using hello [PowerShell desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) VM extension.</span></span>  <span data-ttu-id="c1f67-125">Масштаб Hello Настройка шкал (на экземпляре виртуальной Машины одновременно) Если загрузка ЦП больше 50% 5 минут.</span><span class="sxs-lookup"><span data-stu-id="c1f67-125">hello scale set scales up (on VM instance at a time) when CPU utilization is greater than 50% for 5 minutes.</span></span> 

<span data-ttu-id="c1f67-126">В дополнение к этому toohello набора масштабирования ресурсов, hello *azuredeploy.json* образец шаблона также объявляет виртуальной сети, общедоступный IP-адрес, балансировки нагрузки и ресурсов параметров автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="c1f67-126">In addition toohello scale set resource, hello *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span> <span data-ttu-id="c1f67-127">В этом шаблоне также показано обновление приложения.</span><span class="sxs-lookup"><span data-stu-id="c1f67-127">This template also demonstrates application upgrade.</span></span>  <span data-ttu-id="c1f67-128">Дополнительные сведения о создании ресурсов в шаблоне см. в статье [Автоматическое масштабирование ВМ в наборе масштабирования ВМ](virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="c1f67-128">For more information on creating these resources in a template, see [Windows scale set with autoscale](virtual-machine-scale-sets-windows-autoscale.md).</span></span>

<span data-ttu-id="c1f67-129">В hello *azuredeploy.json* шаблон, hello `extensionProfile` свойство hello `Microsoft.Compute/virtualMachineScaleSets` ресурс определяет [конфигурации требуемого состояния (DSC)](virtual-machine-scale-sets-dsc.md) расширения, которая устанавливает службы IIS и значение по умолчанию веб-приложение из пакета WebDeploy.</span><span class="sxs-lookup"><span data-stu-id="c1f67-129">In hello *azuredeploy.json* template, hello `extensionProfile` property of hello `Microsoft.Compute/virtualMachineScaleSets` resource specifies a [desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) extension which installs IIS and a default web app from a WebDeploy package.</span></span>  <span data-ttu-id="c1f67-130">Hello *IISInstall.ps1* сценарий Установка служб IIS на виртуальной машине hello и находится в hello *DSC* папки.</span><span class="sxs-lookup"><span data-stu-id="c1f67-130">hello *IISInstall.ps1* script installs IIS on hello virtual machine and is found in hello *DSC* folder.</span></span>  <span data-ttu-id="c1f67-131">веб-приложение MVC Hello находится в hello *WebDeploy* папки.</span><span class="sxs-lookup"><span data-stu-id="c1f67-131">hello MVC web app is found in hello *WebDeploy* folder.</span></span>  <span data-ttu-id="c1f67-132">сценарий установки toohello пути Hello и веб-приложения hello определяются в hello `powershelldscZip` и `webDeployPackage` параметров в hello *azuredeploy.parameters.json* файла.</span><span class="sxs-lookup"><span data-stu-id="c1f67-132">hello paths toohello install script and hello web app are defined in hello `powershelldscZip` and `webDeployPackage` parameters in hello *azuredeploy.parameters.json* file.</span></span> 

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

## <a name="deploy-hello-template"></a><span data-ttu-id="c1f67-133">Развертывание шаблона hello</span><span class="sxs-lookup"><span data-stu-id="c1f67-133">Deploy hello template</span></span>
<span data-ttu-id="c1f67-134">Hello простейший способ toodeploy hello [Python HTTP-сервера в Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) или [приложение ASP.NET MVC в Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) шаблона — toouse hello **развертывание tooAzure** кнопка найдена в hello в файлах readme hello в GitHub.</span><span class="sxs-lookup"><span data-stu-id="c1f67-134">hello simplest way toodeploy hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) template is toouse hello **Deploy tooAzure** button found in hello in hello readme files in GitHub.</span></span>  <span data-ttu-id="c1f67-135">Также можно использовать PowerShell или Azure CLI toodeploy hello образцы шаблонов.</span><span class="sxs-lookup"><span data-stu-id="c1f67-135">You can also use PowerShell or Azure CLI toodeploy hello sample templates.</span></span>

### <a name="powershell"></a><span data-ttu-id="c1f67-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1f67-136">PowerShell</span></span>
<span data-ttu-id="c1f67-137">Копировать hello [Python HTTP-сервера в Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) или [приложение ASP.NET MVC в Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) файлы из папки tooa репозитория GitHub hello на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="c1f67-137">Copy hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) files from hello GitHub repo tooa folder on your local computer.</span></span>  <span data-ttu-id="c1f67-138">Откройте hello *azuredeploy.parameters.json* файла и обновление значения по умолчанию hello объекта hello `vmssName`, `adminUsername`, и `adminPassword` параметров.</span><span class="sxs-lookup"><span data-stu-id="c1f67-138">Open hello *azuredeploy.parameters.json* file and update hello default values of hello `vmssName`, `adminUsername`, and `adminPassword` parameters.</span></span> <span data-ttu-id="c1f67-139">Сохраните следующий сценарий PowerShell слишком hello*deploy.ps1* в hello же папке, что hello *azuredeploy.json* шаблона.</span><span class="sxs-lookup"><span data-stu-id="c1f67-139">Save hello following PowerShell script too*deploy.ps1* in hello same folder as hello *azuredeploy.json* template.</span></span> <span data-ttu-id="c1f67-140">hello шаблона запустите образец hello toodeploy *deploy.ps1* сценарий в командном окне PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1f67-140">toodeploy hello sample template run hello *deploy.ps1* script from a PowerShell command window.</span></span>

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

### <a name="azure-cli"></a><span data-ttu-id="c1f67-141">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="c1f67-141">Azure CLI</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="c1f67-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c1f67-142">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
