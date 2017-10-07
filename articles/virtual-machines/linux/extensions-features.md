---
title: "aaaVirtual машины расширения и компоненты для Linux | Документы Microsoft"
description: "Узнайте о расширениях, доступных для виртуальных машин Azure и сгруппированных по предоставляемым функциям или улучшениям."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a><span data-ttu-id="65f57-103">Обзор расширений и компонентов виртуальных машин под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="65f57-103">Virtual machine extensions and features for Linux</span></span>

<span data-ttu-id="65f57-104">Расширения виртуальных машин Azure — это небольшие приложения, которые выполняют задачи настройки и автоматизации после развертывания виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="65f57-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="65f57-105">Например, если виртуальная машина требует установки программного обеспечения защиты от вирусов и конфигурации Docker, расширение ВМ может быть используется toocomplete этих задач.</span><span class="sxs-lookup"><span data-stu-id="65f57-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="65f57-106">Расширений ВМ Azure можно выполнить с помощью hello Azure CLI PowerShell шаблоны диспетчера ресурсов Azure и hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="65f57-106">Azure VM extensions can be run using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="65f57-107">Расширения могут предоставляться в рамках нового развертывания виртуальной машины и работать в любой из существующих систем.</span><span class="sxs-lookup"><span data-stu-id="65f57-107">Extensions can be bundled with a new virtual machine deployment, or run against any existing system.</span></span>

<span data-ttu-id="65f57-108">Этот документ предоставляет обзор расширений ВМ, предварительные условия для использования расширений ВМ Azure и руководство о предоставлении toodetect, управление и удаление расширений ВМ.</span><span class="sxs-lookup"><span data-stu-id="65f57-108">This document provides an overview of VM extensions, prerequisites for using Azure VM extensions, and guidance on how toodetect, manage, and remove VM extensions.</span></span> <span data-ttu-id="65f57-109">Этот документ содержит только обобщенные сведения, так как существует множество расширений виртуальной машины с разными параметрами настройки.</span><span class="sxs-lookup"><span data-stu-id="65f57-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="65f57-110">Сведения о различных модулей можно найти в каждое расширение отдельных toohello определенного документа.</span><span class="sxs-lookup"><span data-stu-id="65f57-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="65f57-111">Варианты использования и примеры</span><span class="sxs-lookup"><span data-stu-id="65f57-111">Use cases and samples</span></span>

<span data-ttu-id="65f57-112">Существует несколько разных расширений ВМ Azure, которые используются в определенных сценариях.</span><span class="sxs-lookup"><span data-stu-id="65f57-112">Several different Azure VM extensions are available, each with a specific use case.</span></span> <span data-ttu-id="65f57-113">Ниже приведены некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="65f57-113">Some examples are:</span></span>

- <span data-ttu-id="65f57-114">Примените требуемого состояния PowerShell конфигураций tooa виртуальной машины с помощью hello расширение DSC для Linux.</span><span class="sxs-lookup"><span data-stu-id="65f57-114">Apply PowerShell Desired State configurations tooa virtual machine using hello DSC extension for Linux.</span></span> <span data-ttu-id="65f57-115">Подробнее см. [Общие сведения об обработчике расширения Desired State Configuration в Azure](https://github.com/Azure/azure-linux-extensions/tree/master/DSC);</span><span class="sxs-lookup"><span data-stu-id="65f57-115">For more information, see [Azure Desired State configuration extension](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span></span>
- <span data-ttu-id="65f57-116">Настройте наблюдение за виртуальную машину с hello расширения виртуальной Машины агента наблюдения Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="65f57-116">Configure monitoring of a virtual machine with hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="65f57-117">Дополнительные сведения см. в разделе [как toomonitor ВМ Linux](tutorial-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="65f57-117">For more information, see [How toomonitor a Linux VM](tutorial-monitoring.md).</span></span>
- <span data-ttu-id="65f57-118">Настройка мониторинга инфраструктуры Azure с hello Datadog расширения.</span><span class="sxs-lookup"><span data-stu-id="65f57-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="65f57-119">Дополнительные сведения см. в разделе hello [Datadog блог](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="65f57-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="65f57-120">Настройка узла Docker на виртуальной машине Azure с помощью расширения виртуальной Машины Docker hello.</span><span class="sxs-lookup"><span data-stu-id="65f57-120">Configure a Docker host on an Azure virtual machine using hello Docker VM extension.</span></span> <span data-ttu-id="65f57-121">Дополнительные сведения см. в статье [Использование расширения виртуальной машины Docker для развертывания среды](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="65f57-121">For more information, see [Docker VM extension](dockerextension.md).</span></span>

<span data-ttu-id="65f57-122">Кроме расширения tooprocess, расширение пользовательского скрипта доступен для виртуальных машин Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="65f57-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="65f57-123">Hello расширение пользовательского скрипта для Linux позволяет любой скрипт toobe Bash, выполните на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="65f57-123">hello Custom Script extension for Linux allows any Bash script toobe run on a virtual machine.</span></span> <span data-ttu-id="65f57-124">Пользовательские сценарии могут пригодиться при проектировании развертывания Azure, для которого требуется дополнительная настройка, ее невозможно выполнить собственными средствами Azure.</span><span class="sxs-lookup"><span data-stu-id="65f57-124">Custom scripts are useful for designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="65f57-125">Дополнительные сведения см. в статье [Использование расширения пользовательских сценариев Azure на виртуальных машинах Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="65f57-125">For more information, see [Linux VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="65f57-126">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="65f57-126">Prerequisites</span></span>

<span data-ttu-id="65f57-127">Для каждого расширения ВМ могут существовать свои требования.</span><span class="sxs-lookup"><span data-stu-id="65f57-127">Each virtual machine extension might have its own set of prerequisites.</span></span> <span data-ttu-id="65f57-128">К примеру hello расширение ВМ Docker обладает необходимым условием поддерживаемые ОС Linux.</span><span class="sxs-lookup"><span data-stu-id="65f57-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="65f57-129">Требования отдельных расширений, описаны в документации конкретного расширения hello.</span><span class="sxs-lookup"><span data-stu-id="65f57-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="65f57-130">Агент виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="65f57-130">Azure VM agent</span></span>

<span data-ttu-id="65f57-131">агент ВМ Azure Hello управляет взаимодействиями между виртуальной машины Azure и Azure fabric controller hello.</span><span class="sxs-lookup"><span data-stu-id="65f57-131">hello Azure VM agent manages interactions between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="65f57-132">агент виртуальной Машины Hello отвечает за многие аспекты работы развертывания и управления Azure виртуальные машины, включая выполнение расширений ВМ.</span><span class="sxs-lookup"><span data-stu-id="65f57-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="65f57-133">агент ВМ Azure Hello предустановлен на Azure Marketplace образов и можно установить вручную на поддерживаемых операционных системах.</span><span class="sxs-lookup"><span data-stu-id="65f57-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed manually on supported operating systems.</span></span>

<span data-ttu-id="65f57-134">Сведения о поддерживаемых операционных системах и инструкции по установке см. в статье [Обзор агента и расширений виртуальной машины](../windows/classic/agents-and-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="65f57-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](../windows/classic/agents-and-extensions.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="65f57-135">Поиск расширений ВМ</span><span class="sxs-lookup"><span data-stu-id="65f57-135">Discover VM extensions</span></span>

<span data-ttu-id="65f57-136">Существует множество различных расширений ВМ, которые можно использовать с виртуальными машинами Azure.</span><span class="sxs-lookup"><span data-stu-id="65f57-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="65f57-137">toosee полный список запуска hello следующую команду с hello Azure CLI, заменив пути hello hello местом по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="65f57-137">toosee a complete list, run hello following command with hello Azure CLI, replacing hello example location with hello location of your choice.</span></span>

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a><span data-ttu-id="65f57-138">Запуск расширений ВМ</span><span class="sxs-lookup"><span data-stu-id="65f57-138">Run VM extensions</span></span>

<span data-ttu-id="65f57-139">Расширения виртуальных машин Azure может выполняться на существующих виртуальных машин, которые могут быть полезны при необходимости изменения конфигурации toomake или восстановить подключение на уже развернутой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="65f57-139">Azure virtual machine extensions can be run on existing virtual machines, which are useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="65f57-140">Также расширения можно использовать при развертывании с помощью шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65f57-140">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="65f57-141">Используя расширения вместе с шаблонами Resource Manager, можно так развернуть и настроить виртуальные машины Azure, чтобы не после развертывания не требовались дополнительные действия.</span><span class="sxs-lookup"><span data-stu-id="65f57-141">By using extensions with Resource Manager templates, Azure virtual machines can be deployed and configured without post-deployment intervention.</span></span>

<span data-ttu-id="65f57-142">Hello следующие методы можно использовать toorun расширение для существующей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="65f57-142">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="65f57-143">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="65f57-143">Azure CLI</span></span>

<span data-ttu-id="65f57-144">Расширения виртуальных машин Azure, выполняемых над существующей виртуальной машины с помощью hello `az vm extension set` команды.</span><span class="sxs-lookup"><span data-stu-id="65f57-144">Azure virtual machine extensions can be run against an existing virtual machine by using hello `az vm extension set` command.</span></span> <span data-ttu-id="65f57-145">В этом примере выполняется расширение пользовательского скрипта hello от виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="65f57-145">This example runs hello custom script extension against a virtual machine.</span></span>

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

<span data-ttu-id="65f57-146">Здравствуйте, сценарий создает выходные данные примерно toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="65f57-146">hello script produces output similar toohello following text:</span></span>

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a><span data-ttu-id="65f57-147">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="65f57-147">Azure portal</span></span>

<span data-ttu-id="65f57-148">Расширения ВМ может быть применен tooan существующей виртуальной машины через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="65f57-148">VM extensions can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="65f57-149">toodo таким образом, выбрать hello виртуальную машину, выберите **расширения**и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="65f57-149">toodo so, select hello virtual machine, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="65f57-150">Выберите расширение hello из hello список доступных расширений и выполните инструкции мастера hello hello.</span><span class="sxs-lookup"><span data-stu-id="65f57-150">Select hello extension you want from hello list of available extensions and follow hello instructions in hello wizard.</span></span>

<span data-ttu-id="65f57-151">Hello следующем рисунке показана установка hello hello расширения Linux пользовательский сценарий из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="65f57-151">hello following image shows hello installation of hello Linux Custom Script extension from hello Azure portal.</span></span>

![Установка расширения пользовательских сценариев](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="65f57-153">Шаблоны диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="65f57-153">Azure Resource Manager templates</span></span>

<span data-ttu-id="65f57-154">Расширения ВМ может быть добавлено tooan шаблона диспетчера ресурсов Azure и выполняться hello развертывания шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="65f57-154">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="65f57-155">Развертывая расширение вместе с шаблоном, можно создать полностью настроенное развертывание Azure.</span><span class="sxs-lookup"><span data-stu-id="65f57-155">When you deploy an extension with a template, you can create fully configured Azure deployments.</span></span> <span data-ttu-id="65f57-156">Например следующий JSON hello берется из шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="65f57-156">For example, hello following JSON is taken from a Resource Manager template.</span></span> <span data-ttu-id="65f57-157">шаблон Hello развертывает набор с балансировкой нагрузки виртуальные машины и базы данных Azure SQL, а затем устанавливает приложение .NET Core на каждой виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="65f57-157">hello template deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="65f57-158">Установка программного обеспечения hello обеспечивает Hello расширения виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="65f57-158">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="65f57-159">Дополнительные сведения см. в разделе hello полного [шаблона диспетчера ресурсов](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="65f57-159">For more information, see hello full [Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

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

<span data-ttu-id="65f57-160">Дополнительные сведения см. в статье [Создание шаблонов Azure Resource Manager](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span><span class="sxs-lookup"><span data-stu-id="65f57-160">For more information, see [Authoring Azure Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="65f57-161">Защита данных в расширениях ВМ</span><span class="sxs-lookup"><span data-stu-id="65f57-161">Secure VM extension data</span></span>

<span data-ttu-id="65f57-162">При работе с расширением ВМ, может быть необходимо tooinclude конфиденциальные сведения, например учетные данные, имена учетных записей хранилища и ключи доступа к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="65f57-162">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="65f57-163">Множество расширений ВМ включают защищенной конфигурации, который шифрует данные и только расшифровывает его целевой виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="65f57-163">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="65f57-164">Каждое расширение имеет собственную схему защищенной конфигурации, которая описывается в документации по этим расширениям.</span><span class="sxs-lookup"><span data-stu-id="65f57-164">Each extension has a specific protected configuration schema, and each is detailed in extension-specific documentation.</span></span>

<span data-ttu-id="65f57-165">Привет, в следующем примере показан экземпляр hello расширение пользовательского скрипта для Linux.</span><span class="sxs-lookup"><span data-stu-id="65f57-165">hello following example shows an instance of hello Custom Script extension for Linux.</span></span> <span data-ttu-id="65f57-166">Обратите внимание, что команды, hello tooexecute включает в себя набор учетных данных.</span><span class="sxs-lookup"><span data-stu-id="65f57-166">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="65f57-167">В этом примере команда tooexecute hello не будут зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="65f57-167">In this example, hello command tooexecute will not be encrypted.</span></span>


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
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

<span data-ttu-id="65f57-168">Перемещение hello **tooexecute команда** toohello свойство **защищенных** конфигурации защищает строку hello выполнения.</span><span class="sxs-lookup"><span data-stu-id="65f57-168">Moving hello **command tooexecute** property toohello **protected** configuration secures hello execution string.</span></span>

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

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="65f57-169">Устранение неполадок с расширениями ВМ</span><span class="sxs-lookup"><span data-stu-id="65f57-169">Troubleshoot VM extensions</span></span>

<span data-ttu-id="65f57-170">Каждое расширение ВМ, возможно, устранение неполадок расширения toohello определенного действия.</span><span class="sxs-lookup"><span data-stu-id="65f57-170">Each VM extension may have troubleshooting steps specific toohello extension.</span></span> <span data-ttu-id="65f57-171">Например когда вы используете расширение пользовательского скрипта hello, сведения о выполнении скрипта можно найти локально на hello виртуальной машины, на котором был выполнен hello расширения.</span><span class="sxs-lookup"><span data-stu-id="65f57-171">For example, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="65f57-172">Действия по устранению неполадок для конкретных расширений описаны в документации по соответствующим расширениям.</span><span class="sxs-lookup"><span data-stu-id="65f57-172">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="65f57-173">следующие шаги по устранению неполадок Hello применяются tooall расширения виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="65f57-173">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="65f57-174">Просмотр состояния расширения</span><span class="sxs-lookup"><span data-stu-id="65f57-174">View extension status</span></span>

<span data-ttu-id="65f57-175">После завершения выполнения расширения виртуальной машины от виртуальной машины, используйте следующие состояния расширения tooreturn команды Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="65f57-175">After a virtual machine extension has been run against a virtual machine, use hello following Azure CLI command tooreturn extension status.</span></span> <span data-ttu-id="65f57-176">Замените в примере имена-параметры собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="65f57-176">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="65f57-177">Hello вывод выглядит следующим образом после текста hello.</span><span class="sxs-lookup"><span data-stu-id="65f57-177">hello output looks like hello following text:</span></span>

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

<span data-ttu-id="65f57-178">Состояние выполнения расширения можно найти также в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="65f57-178">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="65f57-179">состояние hello tooview расширение, выберите hello виртуальной машины, выберите **расширения**, и выберите hello нужное расширение.</span><span class="sxs-lookup"><span data-stu-id="65f57-179">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-a-vm-extension"></a><span data-ttu-id="65f57-180">Повторный запуск расширения ВМ</span><span class="sxs-lookup"><span data-stu-id="65f57-180">Rerun a VM extension</span></span>

<span data-ttu-id="65f57-181">Возможны ситуации, в которых расширение виртуальной машины должен toobe повторно.</span><span class="sxs-lookup"><span data-stu-id="65f57-181">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="65f57-182">Можно повторно запустить расширение, удалив и повторно запустив hello расширения с помощью метода выполнения по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="65f57-182">You can rerun an extension by removing it, and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="65f57-183">tooremove расширение, запустите следующую команду с hello Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="65f57-183">tooremove an extension, run hello following command with hello Azure CLI.</span></span> <span data-ttu-id="65f57-184">Замените в примере имена-параметры собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="65f57-184">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

<span data-ttu-id="65f57-185">Расширение можно удалить с помощью инструкций из портала Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="65f57-185">You can remove an extension by using hello following steps in hello Azure portal:</span></span>

1. <span data-ttu-id="65f57-186">Выберите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="65f57-186">Select a virtual machine.</span></span>
2. <span data-ttu-id="65f57-187">Выберите **Расширения**.</span><span class="sxs-lookup"><span data-stu-id="65f57-187">Choose **Extensions**.</span></span>
3. <span data-ttu-id="65f57-188">Выберите расширение требуемого hello.</span><span class="sxs-lookup"><span data-stu-id="65f57-188">Select hello desired extension.</span></span>
4. <span data-ttu-id="65f57-189">Выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="65f57-189">Choose **Uninstall**.</span></span>

## <a name="common-vm-extension-reference"></a><span data-ttu-id="65f57-190">Справочные материалы для всех расширений ВМ</span><span class="sxs-lookup"><span data-stu-id="65f57-190">Common VM extension reference</span></span>
| <span data-ttu-id="65f57-191">Имя расширения</span><span class="sxs-lookup"><span data-stu-id="65f57-191">Extension name</span></span> | <span data-ttu-id="65f57-192">Описание</span><span class="sxs-lookup"><span data-stu-id="65f57-192">Description</span></span> | <span data-ttu-id="65f57-193">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="65f57-193">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="65f57-194">Расширение пользовательских сценариев для Linux</span><span class="sxs-lookup"><span data-stu-id="65f57-194">Custom Script extension for Linux</span></span> |<span data-ttu-id="65f57-195">Выполняет сценарии на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="65f57-195">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="65f57-196">Расширение пользовательских сценариев для Linux</span><span class="sxs-lookup"><span data-stu-id="65f57-196">Custom Script extension for Linux</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="65f57-197">Расширение Docker</span><span class="sxs-lookup"><span data-stu-id="65f57-197">Docker extension</span></span> |<span data-ttu-id="65f57-198">Установите hello Docker daemon toosupport удаленных команд Docker.</span><span class="sxs-lookup"><span data-stu-id="65f57-198">Install hello Docker daemon toosupport remote Docker commands.</span></span> |[<span data-ttu-id="65f57-199">Расширение виртуальной машины Docker</span><span class="sxs-lookup"><span data-stu-id="65f57-199">Docker VM extension</span></span>](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="65f57-200">Расширение для доступа к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="65f57-200">VM Access extension</span></span> |<span data-ttu-id="65f57-201">Восстановить tooan доступа к виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="65f57-201">Regain access tooan Azure virtual machine</span></span> |[<span data-ttu-id="65f57-202">Расширение для доступа к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="65f57-202">VM Access extension</span></span>](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| <span data-ttu-id="65f57-203">Расширение системы диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="65f57-203">Azure Diagnostics extension</span></span> |<span data-ttu-id="65f57-204">Управляет системой диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="65f57-204">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="65f57-205">Расширение системы диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="65f57-205">Azure Diagnostics extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="65f57-206">Расширение Azure VM Access</span><span class="sxs-lookup"><span data-stu-id="65f57-206">Azure VM Access extension</span></span> |<span data-ttu-id="65f57-207">Управляет пользователями и учетными данными.</span><span class="sxs-lookup"><span data-stu-id="65f57-207">Manage users and credentials</span></span> |[<span data-ttu-id="65f57-208">Расширение VM Access для Linux</span><span class="sxs-lookup"><span data-stu-id="65f57-208">VM Access extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
