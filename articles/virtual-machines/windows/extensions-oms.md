---
title: "Расширение виртуальной машины OMS Azure для Windows | Документация Майкрософт"
description: "Разверните агент OMS на виртуальной машине Windows, используя расширение виртуальной машины."
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
ms.openlocfilehash: d933f488fdda0c1d37892be65f2712cf0eb5694e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="c9d62-103">Расширение виртуальной машины OMS для Windows</span><span class="sxs-lookup"><span data-stu-id="c9d62-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="c9d62-104">Operations Management Suite (OMS) предоставляет возможности мониторинга, оповещений и внесения исправлений в соответствии с оповещениями для облачных и локальных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c9d62-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="c9d62-105">Расширение виртуальной машины агента OMS для Windows публикуется и поддерживается корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c9d62-105">The OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="c9d62-106">Это расширение устанавливает агент OMS на виртуальных машинах Azure и регистрирует виртуальные машины в существующей рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="c9d62-106">The extension installs the OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="c9d62-107">В этом документе подробно описаны поддерживаемые платформы, конфигурации и параметры развертывания для расширения виртуальной машины OMS для Windows.</span><span class="sxs-lookup"><span data-stu-id="c9d62-107">This document details the supported platforms, configurations, and deployment options for the OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9d62-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c9d62-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="c9d62-109">операционная система</span><span class="sxs-lookup"><span data-stu-id="c9d62-109">Operating system</span></span>
<span data-ttu-id="c9d62-110">Расширение агента OMS для Windows может выполняться для выпусков Windows Server 2008 R2, 2012, 2012 R2 и 2016.</span><span class="sxs-lookup"><span data-stu-id="c9d62-110">The OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="c9d62-111">Подключение к Интернету</span><span class="sxs-lookup"><span data-stu-id="c9d62-111">Internet connectivity</span></span>
<span data-ttu-id="c9d62-112">Для расширения агента OMS для Windows требуется, чтобы целевая виртуальная машина была подключена к Интернету.</span><span class="sxs-lookup"><span data-stu-id="c9d62-112">The OMS Agent extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="c9d62-113">Схема расширения</span><span class="sxs-lookup"><span data-stu-id="c9d62-113">Extension schema</span></span>

<span data-ttu-id="c9d62-114">В следующем объекте JSON показана схема для расширения агента OMS.</span><span class="sxs-lookup"><span data-stu-id="c9d62-114">The following JSON shows the schema for the OMS Agent extension.</span></span> <span data-ttu-id="c9d62-115">Расширение требует идентификатор и ключ из целевой рабочей области OMS, которые находятся на портале OMS.</span><span class="sxs-lookup"><span data-stu-id="c9d62-115">The extension requires the workspace Id and workspace key from the target OMS workspace, these can be found in the OMS portal.</span></span> <span data-ttu-id="c9d62-116">Так как ключ рабочей области должен рассматриваться в качестве конфиденциальных данных, его следует хранить в защищенной конфигурации параметров.</span><span class="sxs-lookup"><span data-stu-id="c9d62-116">Because the workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="c9d62-117">Данные защищенных параметров расширения виртуальной машины Azure зашифрованы. Они расшифровываются только на целевой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c9d62-117">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span> <span data-ttu-id="c9d62-118">Обратите внимание, что в **workspaceId** и **workspaceKey** учитывается регистр знаков.</span><span class="sxs-lookup"><span data-stu-id="c9d62-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

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
### <a name="property-values"></a><span data-ttu-id="c9d62-119">Значения свойств</span><span class="sxs-lookup"><span data-stu-id="c9d62-119">Property values</span></span>

| <span data-ttu-id="c9d62-120">Имя</span><span class="sxs-lookup"><span data-stu-id="c9d62-120">Name</span></span> | <span data-ttu-id="c9d62-121">Значение и пример</span><span class="sxs-lookup"><span data-stu-id="c9d62-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="c9d62-122">версия_API</span><span class="sxs-lookup"><span data-stu-id="c9d62-122">apiVersion</span></span> | <span data-ttu-id="c9d62-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="c9d62-123">2015-06-15</span></span> |
| <span data-ttu-id="c9d62-124">publisher</span><span class="sxs-lookup"><span data-stu-id="c9d62-124">publisher</span></span> | <span data-ttu-id="c9d62-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="c9d62-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="c9d62-126">type</span><span class="sxs-lookup"><span data-stu-id="c9d62-126">type</span></span> | <span data-ttu-id="c9d62-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="c9d62-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="c9d62-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="c9d62-128">typeHandlerVersion</span></span> | <span data-ttu-id="c9d62-129">1.0</span><span class="sxs-lookup"><span data-stu-id="c9d62-129">1.0</span></span> |
| <span data-ttu-id="c9d62-130">workspaceID (пример)</span><span class="sxs-lookup"><span data-stu-id="c9d62-130">workspaceId (e.g)</span></span> | <span data-ttu-id="c9d62-131">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="c9d62-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="c9d62-132">workspaceKey (пример)</span><span class="sxs-lookup"><span data-stu-id="c9d62-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="c9d62-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="c9d62-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="c9d62-134">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="c9d62-134">Template deployment</span></span>

<span data-ttu-id="c9d62-135">Расширения виртуальной машины Azure можно развернуть с помощью шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c9d62-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="c9d62-136">Для запуска расширения агента OMS во время развертывания шаблона Azure Resource Manager в нем можно использовать схему JSON, описанную в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="c9d62-136">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="c9d62-137">Пример шаблона, включающего в себя расширение виртуальной машины агента OMS, можно найти в [коллекции быстрого запуска Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="c9d62-137">A sample template that includes the OMS Agent VM extension can be found on the [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="c9d62-138">JSON для расширения виртуальной машины можно вложить в ресурс виртуальной машины или поместить в корень или на верхний уровень JSON-файла шаблона Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c9d62-138">The JSON for a virtual machine extension can be nested inside the virtual machine resource, or placed at the root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="c9d62-139">Размещение JSON влияет на значения имени и типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="c9d62-139">The placement of the JSON affects the value of the resource name and type.</span></span> <span data-ttu-id="c9d62-140">Дополнительные сведения см. в разделе [Указание имени и типа дочернего ресурса в шаблоне Resource Manager](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="c9d62-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="c9d62-141">В следующем примере предполагается, что расширение OMS вложено в ресурс виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c9d62-141">The following example assumes the OMS extension is nested inside the virtual machine resource.</span></span> <span data-ttu-id="c9d62-142">При вложении ресурса расширения JSON помещается в объект `"resources": []` виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c9d62-142">When nesting the extension resource, the JSON is placed in the `"resources": []` object of the virtual machine.</span></span>


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

<span data-ttu-id="c9d62-143">При размещении JSON расширения в корне шаблона имя ресурса содержит ссылку на родительскую виртуальную машину, а тип отражает вложенную конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="c9d62-143">When placing the extension JSON at the root of the template, the resource name includes a reference to the parent virtual machine, and the type reflects the nested configuration.</span></span> 

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

## <a name="powershell-deployment"></a><span data-ttu-id="c9d62-144">Развертывание с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9d62-144">PowerShell deployment</span></span>

<span data-ttu-id="c9d62-145">Команду `Set-AzureRmVMExtension` можно использовать для развертывания расширения виртуальной машины агента OMS на существующей виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c9d62-145">The `Set-AzureRmVMExtension` command can be used to deploy the OMS Agent virtual machine extension to an existing virtual machine.</span></span> <span data-ttu-id="c9d62-146">Перед выполнением команды необходимо сохранить открытые и закрытые конфигурации в хэш-таблице PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c9d62-146">Before running the command, the public and private configurations need to be stored in a PowerShell hash table.</span></span> 

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

## <a name="troubleshoot-and-support"></a><span data-ttu-id="c9d62-147">Устранение неполадок и поддержка</span><span class="sxs-lookup"><span data-stu-id="c9d62-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="c9d62-148">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="c9d62-148">Troubleshoot</span></span>

<span data-ttu-id="c9d62-149">Данные о состоянии развертывания расширения можно получить на портале Azure, а также с помощью модуля Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c9d62-149">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="c9d62-150">Чтобы просмотреть состояние развертывания расширений для определенной виртуальной машины, выполните следующую команду в модуле Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c9d62-150">To see the deployment state of extensions for a given VM, run the following command using the Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="c9d62-151">Выходные данные выполнения расширения регистрируются в файле, расположенном в следующем каталоге:</span><span class="sxs-lookup"><span data-stu-id="c9d62-151">Extension execution output is logged to files found in the following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="c9d62-152">Поддержка</span><span class="sxs-lookup"><span data-stu-id="c9d62-152">Support</span></span>

<span data-ttu-id="c9d62-153">Если в любой момент при изучении этой статьи вам потребуется дополнительная помощь, вы можете обратиться к экспертам по Azure на [форумах MSDN Azure и Stack Overflow](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="c9d62-153">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="c9d62-154">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="c9d62-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="c9d62-155">Перейдите на [сайт поддержки Azure](https://azure.microsoft.com/en-us/support/options/) и щелкните "Получить поддержку".</span><span class="sxs-lookup"><span data-stu-id="c9d62-155">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="c9d62-156">Дополнительные сведения об использовании службы поддержки Azure см. в статье [Часто задаваемые вопросы о поддержке Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="c9d62-156">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
