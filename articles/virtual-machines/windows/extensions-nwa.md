---
title: "aaaAzure расширение виртуальной машины агента Наблюдатель сети для Windows | Документы Microsoft"
description: "Развертывание hello агента Наблюдатель сети на виртуальной машине Windows, с помощью расширения виртуальной машины."
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a><span data-ttu-id="5561a-103">Расширение виртуальной машины агента Наблюдателя за сетями для Windows</span><span class="sxs-lookup"><span data-stu-id="5561a-103">Network Watcher Agent virtual machine extension for Windows</span></span>

## <a name="overview"></a><span data-ttu-id="5561a-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="5561a-104">Overview</span></span>

<span data-ttu-id="5561a-105">[Наблюдатель за сетями Azure](https://review.docs.microsoft.com/en-us/azure/network-watcher/) — это служба мониторинга производительности, диагностики и анализа сети, позволяющая наблюдать за сетями Azure.</span><span class="sxs-lookup"><span data-stu-id="5561a-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="5561a-106">Hello расширение виртуальной машины агента Наблюдатель сети является обязательным для некоторых функций hello Наблюдатель сети на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="5561a-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="5561a-107">Сюда входит запись сетевого трафика по запросу и другие дополнительные функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="5561a-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="5561a-108">Сведения этого документа hello поддерживается платформ и параметры развертывания для hello расширение агента Наблюдатель сети виртуальной машины для Windows.</span><span class="sxs-lookup"><span data-stu-id="5561a-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5561a-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5561a-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="5561a-110">операционная система</span><span class="sxs-lookup"><span data-stu-id="5561a-110">Operating system</span></span>

<span data-ttu-id="5561a-111">Hello расширение Agent Наблюдатель сети для Windows, которые могут выполняться для Windows Server 2008 R2, 2012 и 2012 R2, 2016 освобождает.</span><span class="sxs-lookup"><span data-stu-id="5561a-111">hello Network Watcher Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span> <span data-ttu-id="5561a-112">Обратите внимание, что hello Nano Server в настоящее время не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="5561a-112">Note that hello Nano Server is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="5561a-113">Подключение к Интернету</span><span class="sxs-lookup"><span data-stu-id="5561a-113">Internet connectivity</span></span>

<span data-ttu-id="5561a-114">Некоторые функциональные возможности агента Наблюдатель сети hello требует hello целевой виртуальной машины подключенных toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="5561a-114">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="5561a-115">Без hello возможность tooestablish исходящих подключений некоторых функций hello агента Наблюдатель сети может работать неправильно или становятся недоступными.</span><span class="sxs-lookup"><span data-stu-id="5561a-115">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="5561a-116">Дополнительные сведения см. в разделе hello [документации Наблюдатель сети](../../network-watcher/network-watcher-monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5561a-116">For more details, please see hello [Network Watcher documentation](../../network-watcher/network-watcher-monitoring-overview.md).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="5561a-117">Схема расширения</span><span class="sxs-lookup"><span data-stu-id="5561a-117">Extension schema</span></span>

<span data-ttu-id="5561a-118">Hello следующий JSON показана схема hello для hello расширение Agent Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="5561a-118">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="5561a-119">Hello расширение не требуется ни в настоящее время поддерживает все параметры, предоставленные пользователем и зависит от конфигурации по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5561a-119">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="5561a-120">Значения свойств</span><span class="sxs-lookup"><span data-stu-id="5561a-120">Property values</span></span>

| <span data-ttu-id="5561a-121">Имя</span><span class="sxs-lookup"><span data-stu-id="5561a-121">Name</span></span> | <span data-ttu-id="5561a-122">Значение и пример</span><span class="sxs-lookup"><span data-stu-id="5561a-122">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="5561a-123">версия_API</span><span class="sxs-lookup"><span data-stu-id="5561a-123">apiVersion</span></span> | <span data-ttu-id="5561a-124">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="5561a-124">2015-06-15</span></span> |
| <span data-ttu-id="5561a-125">publisher</span><span class="sxs-lookup"><span data-stu-id="5561a-125">publisher</span></span> | <span data-ttu-id="5561a-126">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="5561a-126">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="5561a-127">type</span><span class="sxs-lookup"><span data-stu-id="5561a-127">type</span></span> | <span data-ttu-id="5561a-128">NetworkWatcherAgentWindows</span><span class="sxs-lookup"><span data-stu-id="5561a-128">NetworkWatcherAgentWindows</span></span> |
| <span data-ttu-id="5561a-129">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="5561a-129">typeHandlerVersion</span></span> | <span data-ttu-id="5561a-130">1.4</span><span class="sxs-lookup"><span data-stu-id="5561a-130">1.4</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="5561a-131">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="5561a-131">Template deployment</span></span>

<span data-ttu-id="5561a-132">Расширения виртуальной машины Azure можно развернуть с помощью шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5561a-132">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="5561a-133">можно использовать схему JSON Hello, описанные в предыдущем разделе hello в hello toorun шаблона диспетчера ресурсов Azure расширение Agent Наблюдатель сети во время развертывания шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="5561a-133">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="5561a-134">Развертывание с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="5561a-134">PowerShell deployment</span></span>

<span data-ttu-id="5561a-135">Hello `Set-AzureRmVMExtension` команду можно использовать toodeploy hello агента Наблюдатель сети виртуальной машины расширения tooan существующей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5561a-135">hello `Set-AzureRmVMExtension` command can be used toodeploy hello Network Watcher Agent virtual machine extension tooan existing virtual machine.</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="5561a-136">Устранение неполадок и поддержка</span><span class="sxs-lookup"><span data-stu-id="5561a-136">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="5561a-137">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="5561a-137">Troubleshooting</span></span>

<span data-ttu-id="5561a-138">Данные о состоянии hello развертываний расширения могут быть получены из hello портал Azure, а также с помощью модуля Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="5561a-138">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="5561a-139">Состояние развертывания hello toosee расширений для данной виртуальной Машины выполнения hello следующие команды, используя hello модуля Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5561a-139">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

<span data-ttu-id="5561a-140">Модуль выполнения выходной журнал toofiles в hello следовать каталога:</span><span class="sxs-lookup"><span data-stu-id="5561a-140">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a><span data-ttu-id="5561a-141">Поддержка</span><span class="sxs-lookup"><span data-stu-id="5561a-141">Support</span></span>

<span data-ttu-id="5561a-142">Если вам нужна дополнительная помощь в любой момент в этой статье, можно см. документации toohello руководство пользователя Наблюдатель сети или обратитесь в службу hello Azure экспертами hello [форумы MSDN Azure и переполнения стека](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="5561a-142">If you need more help at any point in this article, you can refer toohello Network Watcher User Guide documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="5561a-143">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="5561a-143">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="5561a-144">Go toohello [сайт поддержки Azure](https://azure.microsoft.com/en-us/support/options/) и выбрать получение поддержки.</span><span class="sxs-lookup"><span data-stu-id="5561a-144">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="5561a-145">Дополнительные сведения об использовании Azure поддерживает чтение hello [поддержки Microsoft Azure часто задаваемые вопросы о](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="5561a-145">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
