---
title: "Расширение виртуальной машины агента Наблюдателя за сетями Azure для Windows | Документация Майкрософт"
description: "Развертывание агента Наблюдателя за сетями на виртуальной машине Windows с помощью расширения виртуальной машины."
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
ms.openlocfilehash: b8d6a998bc86337b286a3434f44f762cca9b7e68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a><span data-ttu-id="f2e06-103">Расширение виртуальной машины агента Наблюдателя за сетями для Windows</span><span class="sxs-lookup"><span data-stu-id="f2e06-103">Network Watcher Agent virtual machine extension for Windows</span></span>

## <a name="overview"></a><span data-ttu-id="f2e06-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f2e06-104">Overview</span></span>

<span data-ttu-id="f2e06-105">[Наблюдатель за сетями Azure](https://review.docs.microsoft.com/en-us/azure/network-watcher/) — это служба мониторинга производительности, диагностики и анализа сети, позволяющая наблюдать за сетями Azure.</span><span class="sxs-lookup"><span data-stu-id="f2e06-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="f2e06-106">Расширение виртуальной машины агента Наблюдателя за сетями необходимо для некоторых функций Наблюдателя за сетями на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="f2e06-106">The Network Watcher Agent virtual machine extension is a requirement for some of the Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="f2e06-107">Сюда входит запись сетевого трафика по запросу и другие дополнительные функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="f2e06-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="f2e06-108">В этом документе подробно описаны поддерживаемые платформы и параметры развертывания для расширения виртуальной машины агента Наблюдателя за сетями для Windows.</span><span class="sxs-lookup"><span data-stu-id="f2e06-108">This document details the supported platforms and deployment options for the Network Watcher Agent virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2e06-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f2e06-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="f2e06-110">операционная система</span><span class="sxs-lookup"><span data-stu-id="f2e06-110">Operating system</span></span>

<span data-ttu-id="f2e06-111">Расширение агента Наблюдателя за сетями для Windows может выполняться в выпусках Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 и Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f2e06-111">The Network Watcher Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span> <span data-ttu-id="f2e06-112">Обратите внимание, что Nano Server в данный момент не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="f2e06-112">Note that the Nano Server is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="f2e06-113">Подключение к Интернету</span><span class="sxs-lookup"><span data-stu-id="f2e06-113">Internet connectivity</span></span>

<span data-ttu-id="f2e06-114">Для некоторых функциональных возможностей агента Наблюдателя за сетями требуется, чтобы целевая виртуальная машина была подключена к Интернету.</span><span class="sxs-lookup"><span data-stu-id="f2e06-114">Some of the Network Watcher Agent functionality requires that the target virtual machine be connected to the Internet.</span></span> <span data-ttu-id="f2e06-115">Без возможности установить исходящие подключения некоторые возможности агента Наблюдателя за сетями могут работать неправильно или стать недоступными.</span><span class="sxs-lookup"><span data-stu-id="f2e06-115">Without the ability to establish outgoing connections some of the Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="f2e06-116">Дополнительные сведения см. в [документации по Наблюдателю за сетями](../../network-watcher/network-watcher-monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f2e06-116">For more details, please see the [Network Watcher documentation](../../network-watcher/network-watcher-monitoring-overview.md).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="f2e06-117">Схема расширения</span><span class="sxs-lookup"><span data-stu-id="f2e06-117">Extension schema</span></span>

<span data-ttu-id="f2e06-118">В следующем коде JSON показана схема для расширения агента Наблюдателя за сетями.</span><span class="sxs-lookup"><span data-stu-id="f2e06-118">The following JSON shows the schema for the Network Watcher Agent extension.</span></span> <span data-ttu-id="f2e06-119">В настоящее время это расширение не требует вводить и не поддерживает какие-либо пользовательские параметры и зависит от конфигурации по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f2e06-119">The extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="f2e06-120">Значения свойств</span><span class="sxs-lookup"><span data-stu-id="f2e06-120">Property values</span></span>

| <span data-ttu-id="f2e06-121">Имя</span><span class="sxs-lookup"><span data-stu-id="f2e06-121">Name</span></span> | <span data-ttu-id="f2e06-122">Значение и пример</span><span class="sxs-lookup"><span data-stu-id="f2e06-122">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="f2e06-123">версия_API</span><span class="sxs-lookup"><span data-stu-id="f2e06-123">apiVersion</span></span> | <span data-ttu-id="f2e06-124">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="f2e06-124">2015-06-15</span></span> |
| <span data-ttu-id="f2e06-125">publisher</span><span class="sxs-lookup"><span data-stu-id="f2e06-125">publisher</span></span> | <span data-ttu-id="f2e06-126">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="f2e06-126">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="f2e06-127">type</span><span class="sxs-lookup"><span data-stu-id="f2e06-127">type</span></span> | <span data-ttu-id="f2e06-128">NetworkWatcherAgentWindows</span><span class="sxs-lookup"><span data-stu-id="f2e06-128">NetworkWatcherAgentWindows</span></span> |
| <span data-ttu-id="f2e06-129">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="f2e06-129">typeHandlerVersion</span></span> | <span data-ttu-id="f2e06-130">1.4</span><span class="sxs-lookup"><span data-stu-id="f2e06-130">1.4</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="f2e06-131">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="f2e06-131">Template deployment</span></span>

<span data-ttu-id="f2e06-132">Расширения виртуальной машины Azure можно развернуть с помощью шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f2e06-132">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="f2e06-133">Для запуска расширения агента Наблюдателя за сетями во время развертывания шаблона Azure Resource Manager в нем можно использовать схему JSON, описанную в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="f2e06-133">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="f2e06-134">Развертывание с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2e06-134">PowerShell deployment</span></span>

<span data-ttu-id="f2e06-135">Команду `Set-AzureRmVMExtension` можно использовать для развертывания расширения виртуальной машины агента Наблюдателя за сетями на существующей виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="f2e06-135">The `Set-AzureRmVMExtension` command can be used to deploy the Network Watcher Agent virtual machine extension to an existing virtual machine.</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="f2e06-136">Устранение неполадок и поддержка</span><span class="sxs-lookup"><span data-stu-id="f2e06-136">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="f2e06-137">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="f2e06-137">Troubleshooting</span></span>

<span data-ttu-id="f2e06-138">Данные о состоянии развертывания расширения можно получить на портале Azure, а также с помощью модуля Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2e06-138">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="f2e06-139">Чтобы просмотреть состояние развертывания расширений для определенной виртуальной машины, выполните следующую команду в модуле Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2e06-139">To see the deployment state of extensions for a given VM, run the following command using the Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

<span data-ttu-id="f2e06-140">Выходные данные выполнения расширения регистрируются в файле, расположенном в следующем каталоге:</span><span class="sxs-lookup"><span data-stu-id="f2e06-140">Extension execution output is logged to files found in the following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a><span data-ttu-id="f2e06-141">Поддержка</span><span class="sxs-lookup"><span data-stu-id="f2e06-141">Support</span></span>

<span data-ttu-id="f2e06-142">Если в любой момент при изучении этой статьи вам потребуется дополнительная помощь, вы можете ознакомиться с руководством пользователя для Наблюдателя за сетями или обратиться к экспертам по Azure на [форумах MSDN Azure и Stack Overflow](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="f2e06-142">If you need more help at any point in this article, you can refer to the Network Watcher User Guide documentation or contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="f2e06-143">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="f2e06-143">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="f2e06-144">Перейдите на [сайт поддержки Azure](https://azure.microsoft.com/en-us/support/options/) и щелкните "Получить поддержку".</span><span class="sxs-lookup"><span data-stu-id="f2e06-144">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="f2e06-145">Дополнительные сведения об использовании службы поддержки Azure см. в статье [Часто задаваемые вопросы о поддержке Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="f2e06-145">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
