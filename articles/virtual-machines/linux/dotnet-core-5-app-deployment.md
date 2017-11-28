---
title: "aaaAutomating развертывания приложений с помощью расширения виртуальных машин | Документы Microsoft"
description: "Руководство по .NET Core для виртуальных машин Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 9fc8b1ba-60f5-410b-8190-9f1ff885e50e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 38a02a4271d6b9ba02a473a51794a7bd90ca3a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="c8288-103">Развертывание приложений с использованием шаблонов Azure Resource Manager для виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="c8288-103">Application deployment with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="c8288-104">После выявления и преобразовать в шаблон развертывания все требования для Azure инфраструктурных развертывания приложения hello должен обращаться toobe.</span><span class="sxs-lookup"><span data-stu-id="c8288-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, hello actual application deployment needs toobe addressed.</span></span> <span data-ttu-id="c8288-105">Развертывание приложения в данном ссылается двоичные файлы приложения hello tooinstalling на ресурсах Azure.</span><span class="sxs-lookup"><span data-stu-id="c8288-105">Application deployment here is referring tooinstalling hello actual application binaries onto Azure resources.</span></span> <span data-ttu-id="c8288-106">Образец hello Music Store, .net Core, NGINX и руководителя, потребуется toobe устанавливается и настраивается на каждой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c8288-106">For hello Music Store sample, .Net Core, NGINX, and Supervisor need toobe installed and configured on each virtual machine.</span></span> <span data-ttu-id="c8288-107">предварительно создать Hello Music Store двоичные файлы должны toobe установлена на виртуальной машине hello и hello Music Store базы данных.</span><span class="sxs-lookup"><span data-stu-id="c8288-107">hello Music Store binaries need toobe installed onto hello virtual machine, and hello Music Store database pre-created.</span></span>

<span data-ttu-id="c8288-108">В этом документе описаны как расширения виртуальных машин можно автоматизировать приложения развертывание и настройку tooAzure виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c8288-108">This document details how Virtual Machine extensions can automate application deployment and configuration tooAzure virtual machines.</span></span> <span data-ttu-id="c8288-109">Здесь будут описаны все зависимости и уникальные настройки.</span><span class="sxs-lookup"><span data-stu-id="c8288-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="c8288-110">Для получения наилучших результатов hello предварительно разверните экземпляр tooyour решения hello подписки Azure, работают вместе с hello шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="c8288-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="c8288-111">Полный шаблон Hello можно найти здесь — [музыка хранилища развертывания на Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="c8288-111">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="c8288-112">Скрипт настройки</span><span class="sxs-lookup"><span data-stu-id="c8288-112">Configuration script</span></span>
<span data-ttu-id="c8288-113">Расширения виртуальных машин — это специализированные программы, применяемыми автоматизации конфигурации tooprovide виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c8288-113">Virtual Machine extensions are specialized programs that execute against virtual machines tooprovide configuration automation.</span></span> <span data-ttu-id="c8288-114">Расширения используются в различных целях, например для автоматизации антивирусных программ, настройки ведения журнала и конфигурации Docker.</span><span class="sxs-lookup"><span data-stu-id="c8288-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="c8288-115">Расширение пользовательского скрипта можно использовать toorun любой скрипт от виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c8288-115">A custom script extension can be used toorun any script against a virtual machine.</span></span> <span data-ttu-id="c8288-116">Образец hello Music Store она до toohello расширение пользовательского скрипта tooconfigure hello Ubuntu виртуальных машин и установить приложение Music Store hello.</span><span class="sxs-lookup"><span data-stu-id="c8288-116">With hello Music Store sample, it is up toohello custom script extension tooconfigure hello Ubuntu virtual machines and install hello Music Store application.</span></span> 

<span data-ttu-id="c8288-117">Перед с подробным описанием объявлены как расширения виртуальных машин в шаблон диспетчера ресурсов Azure, изучите hello скрипт, который выполняется.</span><span class="sxs-lookup"><span data-stu-id="c8288-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine hello script that is run.</span></span> <span data-ttu-id="c8288-118">Этот скрипт настраивает hello Ubuntu виртуальной машины toohost hello приложение Music Store.</span><span class="sxs-lookup"><span data-stu-id="c8288-118">This script configures hello Ubuntu virtual machine toohost hello Music Store application.</span></span> <span data-ttu-id="c8288-119">При запуске hello скрипт устанавливает все необходимое программное обеспечение, установить приложение магазина музыка hello из системы управления версиями и подготовки hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="c8288-119">When run, hello script installs all needed software, install hello Music store application from source control, and prepare hello database.</span></span> 

<span data-ttu-id="c8288-120">toolearn Дополнительные сведения о размещении .net Core приложения в Linux, в разделе [публикации tooa Linux рабочей среде](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span><span class="sxs-lookup"><span data-stu-id="c8288-120">toolearn more about hosting a .Net Core application on Linux, see [Publish tooa Linux production environment](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span></span>

> <span data-ttu-id="c8288-121">Этот пример предназначен только для демонстрации.</span><span class="sxs-lookup"><span data-stu-id="c8288-121">This sample is for demonstration purposes.</span></span>
> 
> 

```bash
#!/bin/bash

# install dotnet core
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
sudo apt-get update
sudo apt-get install -y dotnet-dev-1.0.0-preview2-003121

# download application
sudo wget https://raw.github.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/music-store-azure-demo-pub.tar /
sudo mkdir /opt/music
sudo tar -xf music-store-azure-demo-pub.tar -C /opt/music

# install nginx, update config file
sudo apt-get install -y nginx
sudo service nginx start
sudo touch /etc/nginx/sites-available/default
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/nginx-config/default -O /etc/nginx/sites-available/default
sudo cp /opt/music/nginx-config/default /etc/nginx/sites-available/
sudo nginx -s reload

# update and secure music config file
sed -i "s/<replaceserver>/$1/g" /opt/music/config.json
sed -i "s/<replaceuser>/$2/g" /opt/music/config.json
sed -i "s/<replacepass>/$3/g" /opt/music/config.json
sudo chown $2 /opt/music/config.json
sudo chmod 0400 /opt/music/config.json

# config supervisor
sudo apt-get install -y supervisor
sudo touch /etc/supervisor/conf.d/music.conf
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/supervisor/music.conf -O /etc/supervisor/conf.d/music.conf
sudo service supervisor stop
sudo service supervisor start

# pre-create music store database
/usr/bin/dotnet /opt/music/MusicStore.dll &
```

## <a name="vm-script-extension"></a><span data-ttu-id="c8288-122">Расширение скриптов виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c8288-122">VM Script Extension</span></span>
<span data-ttu-id="c8288-123">Расширения ВМ может выполняться от виртуальной машины во время сборки, включая расширения ресурсов hello в hello шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="c8288-123">VM Extensions can be run against a virtual machine at build time by including hello extension resource in hello Azure Resource Manager template.</span></span> <span data-ttu-id="c8288-124">Hello расширения можно добавить с помощью мастера добавления ресурсов Visual Studio hello, или путем вставки допустимых данных JSON в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="c8288-124">hello extension can be added with hello Visual Studio Add Resource wizard, or by inserting valid JSON into hello template.</span></span> <span data-ttu-id="c8288-125">Hello расширение сценария ресурса вложен в hello ресурса виртуальной машины; Это можно заметить в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="c8288-125">hello Script Extension resource is nested inside hello Virtual Machine resource; this can be seen in hello following example.</span></span>

<span data-ttu-id="c8288-126">Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [расширение ВМ сценария](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span><span class="sxs-lookup"><span data-stu-id="c8288-126">Follow this link toosee hello JSON sample within hello Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span></span> 

<span data-ttu-id="c8288-127">Обратите внимание на hello ниже JSON, hello сценарий хранится в GitHub.</span><span class="sxs-lookup"><span data-stu-id="c8288-127">Notice in hello below JSON that hello script is stored in GitHub.</span></span> <span data-ttu-id="c8288-128">Этот скрипт также может храниться в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="c8288-128">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="c8288-129">Кроме того шаблоны Azure Resource Manager разрешить выполнения строку hello сценария tooconstructed таким образом, что значения параметров шаблона, которая может использоваться в качестве параметров для выполнения скриптов.</span><span class="sxs-lookup"><span data-stu-id="c8288-129">Also, Azure Resource Manager templates allow hello script execution string tooconstructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="c8288-130">В этом случае данные предоставляются в развертывание шаблонов hello, и эти значения можно затем использовать при выполнении сценария hello.</span><span class="sxs-lookup"><span data-stu-id="c8288-130">In this case data is provided when deploying hello templates, and these values can then be used when executing hello script.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

<span data-ttu-id="c8288-131">Дополнительные сведения об использовании расширения пользовательского скрипта hello см. в разделе [пользовательских расширений сценария с помощью шаблонов диспетчера ресурсов](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c8288-131">For more information on using hello custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="c8288-132">Дальнейшее действие</span><span class="sxs-lookup"><span data-stu-id="c8288-132">Next Step</span></span>
<hr>

[<span data-ttu-id="c8288-133">Ознакомьтесь с другими шаблонами Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c8288-133">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

