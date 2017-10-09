---
title: "aaaOMS расширение виртуальной машины Azure для Windows | Документы Microsoft"
description: "Разверните агент OMS hello на виртуальной машине Windows, с помощью расширения виртуальной машины."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: feae6176-2373-4034-b5d9-a32c6b4e1f10
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: 3000f66c0acdec1d1fad2125b8c6b72a92b1ec92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="85215-103">Расширение виртуальной машины OMS для Windows</span><span class="sxs-lookup"><span data-stu-id="85215-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="85215-104">Operations Management Suite (OMS) предоставляет возможности мониторинга, оповещений и внесения исправлений в соответствии с оповещениями для облачных и локальных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="85215-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="85215-105">расширение виртуальной машины агента OMS для Windows Hello публикации и поддерживается корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="85215-105">hello OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="85215-106">расширение Hello устанавливает агент OMS hello на виртуальных машинах Azure и регистрирует виртуальных машин в существующую рабочую область OMS.</span><span class="sxs-lookup"><span data-stu-id="85215-106">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="85215-107">Этот документ сведения hello поддерживается платформы, конфигурации и параметры развертывания для hello OMS расширение виртуальной машины для Windows.</span><span class="sxs-lookup"><span data-stu-id="85215-107">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85215-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="85215-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="85215-109">операционная система</span><span class="sxs-lookup"><span data-stu-id="85215-109">Operating system</span></span>
<span data-ttu-id="85215-110">Hello расширение OMS Agent для Windows, которые могут выполняться для Windows Server 2008 R2, 2012 и 2012 R2, 2016 освобождает.</span><span class="sxs-lookup"><span data-stu-id="85215-110">hello OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="85215-111">Подключение к Интернету</span><span class="sxs-lookup"><span data-stu-id="85215-111">Internet connectivity</span></span>
<span data-ttu-id="85215-112">расширение OMS Agent для Windows Hello требует hello целевой виртуальной машины подключенных toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="85215-112">hello OMS Agent extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="85215-113">Схема расширения</span><span class="sxs-lookup"><span data-stu-id="85215-113">Extension schema</span></span>

<span data-ttu-id="85215-114">Hello следующий JSON показана схема hello для hello расширение OMS Agent.</span><span class="sxs-lookup"><span data-stu-id="85215-114">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="85215-115">расширения Hello требуются hello ключ рабочей области идентификатора и рабочей области из рабочей области OMS целевой hello, их можно найти на портале OMS hello.</span><span class="sxs-lookup"><span data-stu-id="85215-115">hello extension requires hello workspace Id and workspace key from hello target OMS workspace, these can be found in hello OMS portal.</span></span> <span data-ttu-id="85215-116">Так как ключ рабочей области hello должны рассматриваться как конфиденциальные данные, его должны храниться в защищенном Настройка конфигурации.</span><span class="sxs-lookup"><span data-stu-id="85215-116">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="85215-117">Данных параметр расширение защищенных виртуальных Машин Azure шифруется и расшифрованы только hello целевой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="85215-117">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="85215-118">Обратите внимание, что в **workspaceId** и **workspaceKey** учитывается регистр знаков.</span><span class="sxs-lookup"><span data-stu-id="85215-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```
### <a name="property-values"></a><span data-ttu-id="85215-119">Значения свойств</span><span class="sxs-lookup"><span data-stu-id="85215-119">Property values</span></span>

| <span data-ttu-id="85215-120">Имя</span><span class="sxs-lookup"><span data-stu-id="85215-120">Name</span></span> | <span data-ttu-id="85215-121">Значение и пример</span><span class="sxs-lookup"><span data-stu-id="85215-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="85215-122">версия_API</span><span class="sxs-lookup"><span data-stu-id="85215-122">apiVersion</span></span> | <span data-ttu-id="85215-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="85215-123">2015-06-15</span></span> |
| <span data-ttu-id="85215-124">publisher</span><span class="sxs-lookup"><span data-stu-id="85215-124">publisher</span></span> | <span data-ttu-id="85215-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="85215-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="85215-126">type</span><span class="sxs-lookup"><span data-stu-id="85215-126">type</span></span> | <span data-ttu-id="85215-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="85215-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="85215-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="85215-128">typeHandlerVersion</span></span> | <span data-ttu-id="85215-129">1.0</span><span class="sxs-lookup"><span data-stu-id="85215-129">1.0</span></span> |
| <span data-ttu-id="85215-130">workspaceID (пример)</span><span class="sxs-lookup"><span data-stu-id="85215-130">workspaceId (e.g)</span></span> | <span data-ttu-id="85215-131">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="85215-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="85215-132">workspaceKey (пример)</span><span class="sxs-lookup"><span data-stu-id="85215-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="85215-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="85215-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="85215-134">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="85215-134">Template deployment</span></span>

<span data-ttu-id="85215-135">Расширения виртуальной машины Azure можно развернуть с помощью шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="85215-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="85215-136">во время развертывания шаблона диспетчера ресурсов Azure можно использовать схему JSON Hello, описанные в предыдущем разделе hello в hello toorun шаблона диспетчера ресурсов Azure расширение OMS Agent.</span><span class="sxs-lookup"><span data-stu-id="85215-136">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="85215-137">Образец шаблона, включает в себя расширение виртуальной Машины агента OMS hello можно найти на hello [Azure быстрого запуска коллекции](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="85215-137">A sample template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="85215-138">Hello JSON для расширения виртуальной машины может быть вложена в ресурс виртуальной машины hello или помещается в корень hello или шаблон JSON диспетчера ресурсов верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="85215-138">hello JSON for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="85215-139">Размещение Hello hello JSON влияет значение hello hello ресурсов именем и типом.</span><span class="sxs-lookup"><span data-stu-id="85215-139">hello placement of hello JSON affects hello value of hello resource name and type.</span></span> <span data-ttu-id="85215-140">Дополнительные сведения см. в разделе [Указание имени и типа дочернего ресурса в шаблоне Resource Manager](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="85215-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="85215-141">Hello в примере предполагается, что расширение OMS hello вложен в hello ресурса виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="85215-141">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="85215-142">При вложении hello расширения ресурса, hello JSON помещается в hello `"resources": []` объекта hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="85215-142">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>


```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

<span data-ttu-id="85215-143">При помещении hello расширения JSON в корне hello hello шаблона, имя ресурса hello ссылка toohello родительской виртуальной машиной и тип hello отражает hello вложенных конфигурации.</span><span class="sxs-lookup"><span data-stu-id="85215-143">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span> 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

## <a name="powershell-deployment"></a><span data-ttu-id="85215-144">Развертывание с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="85215-144">PowerShell deployment</span></span>

<span data-ttu-id="85215-145">Hello `Set-AzureRmVMExtension` команда может быть используется toodeploy hello агента OMS виртуальную машину расширения tooan существующей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="85215-145">hello `Set-AzureRmVMExtension` command can be used toodeploy hello OMS Agent virtual machine extension tooan existing virtual machine.</span></span> <span data-ttu-id="85215-146">Перед выполнением команды hello, открытых и закрытых конфигураций hello должны toobe, хранящихся в хэш-таблицу PowerShell.</span><span class="sxs-lookup"><span data-stu-id="85215-146">Before running hello command, hello public and private configurations need toobe stored in a PowerShell hash table.</span></span> 

```powershell
$PublicSettings = @{"workspaceId" = "myWorkspaceId"}
$ProtectedSettings = @{"workspaceKey" = "myWorkspaceKey"}

Set-AzureRmVMExtension -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
    -ExtensionType "MicrosoftMonitoringAgent" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS ` 
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="85215-147">Устранение неполадок и поддержка</span><span class="sxs-lookup"><span data-stu-id="85215-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="85215-148">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="85215-148">Troubleshoot</span></span>

<span data-ttu-id="85215-149">Данные о состоянии hello развертываний расширения могут быть получены из hello портал Azure, а также с помощью модуля Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="85215-149">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="85215-150">Состояние развертывания hello toosee расширений для данной виртуальной Машины выполнения hello следующие команды, используя hello модуля Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="85215-150">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="85215-151">Модуль выполнения выходной журнал toofiles в hello следовать каталога:</span><span class="sxs-lookup"><span data-stu-id="85215-151">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="85215-152">Поддержка</span><span class="sxs-lookup"><span data-stu-id="85215-152">Support</span></span>

<span data-ttu-id="85215-153">Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello Azure экспертами hello [форумы MSDN Azure и переполнения стека](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="85215-153">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="85215-154">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="85215-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="85215-155">Go toohello [сайт поддержки Azure](https://azure.microsoft.com/en-us/support/options/) и выбрать получение поддержки.</span><span class="sxs-lookup"><span data-stu-id="85215-155">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="85215-156">Дополнительные сведения об использовании Azure поддерживает чтение hello [поддержки Microsoft Azure часто задаваемые вопросы о](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="85215-156">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
