---
title: "aaaExporting групп ресурсов Azure, содержащего расширения ВМ | Документы Microsoft"
description: "Экспорт шаблонов Resource Manager, которые включают расширения виртуальной машины."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a><span data-ttu-id="d4cf9-103">Экспорт групп ресурсов, которые содержат расширения виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d4cf9-103">Exporting Resource Groups that contain VM extensions</span></span>

<span data-ttu-id="d4cf9-104">Вы можете экспортировать группы ресурсов Azure в новый шаблон Resource Manager, а затем развернуть этот шаблон.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-104">Azure Resource Groups can be exported into a new Resource Manager template that can then be redeployed.</span></span> <span data-ttu-id="d4cf9-105">Hello в процессе экспорта интерпретирует существующих ресурсов и создает шаблона диспетчера ресурсов, при развертывании приводит аналогичные группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-105">hello export process interprets existing resources, and creates a Resource Manager template that when deployed results in a similar Resource Group.</span></span> <span data-ttu-id="d4cf9-106">При использовании параметра экспорта hello группы ресурсов для группы ресурсов, содержащий расширения виртуальных машин, несколько элементов необходимость toobe считается например совместимости расширений и защищенные параметры.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-106">When using hello Resource Group export option against a Resource Group containing Virtual Machine extensions, several items need toobe considered such as extension compatibility and protected settings.</span></span>

<span data-ttu-id="d4cf9-107">Этот документ описывает, как работает hello группы ресурсов в процессе экспорта относительно расширения виртуальных машин, включая список поддерживаемых модулей и сведения об обработке защищенным данным.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-107">This document details how hello Resource Group export process works regarding virtual machine extensions, including a list of supported extensions, and details on handling secured data.</span></span>

## <a name="supported-virtual-machine-extensions"></a><span data-ttu-id="d4cf9-108">Поддерживаемые расширения виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d4cf9-108">Supported Virtual Machine Extensions</span></span>

<span data-ttu-id="d4cf9-109">Доступно много разных расширений виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-109">Many Virtual Machine extensions are available.</span></span> <span data-ttu-id="d4cf9-110">Не все расширения можно экспортировать в виде шаблона диспетчера ресурсов с помощью функции «Сценарий автоматизации» hello.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-110">Not all extensions can be exported into a Resource Manager template using hello “Automation Script” feature.</span></span> <span data-ttu-id="d4cf9-111">Если расширение виртуальной машины не поддерживается, он должен вручную помещаются обратно в экспортированный шаблон hello toobe.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-111">If a virtual machine extension is not supported, it needs toobe manually placed back into hello exported template.</span></span>

<span data-ttu-id="d4cf9-112">Hello следующие расширения можно экспортировать с помощью функции скрипта автоматизации hello.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-112">hello following extensions can be exported with hello automation script feature.</span></span>

| <span data-ttu-id="d4cf9-113">Добавочный номер</span><span class="sxs-lookup"><span data-stu-id="d4cf9-113">Extension</span></span> ||||
|---|---|---|---|
| <span data-ttu-id="d4cf9-114">Резервное копирование Acronis</span><span class="sxs-lookup"><span data-stu-id="d4cf9-114">Acronis Backup</span></span> | <span data-ttu-id="d4cf9-115">Агент Datadog для Windows</span><span class="sxs-lookup"><span data-stu-id="d4cf9-115">Datadog Windows Agent</span></span> | <span data-ttu-id="d4cf9-116">Исправления для ОС Linux</span><span class="sxs-lookup"><span data-stu-id="d4cf9-116">OS Patching For Linux</span></span> | <span data-ttu-id="d4cf9-117">Моментальные снимки виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="d4cf9-117">VM Snapshot Linux</span></span>
| <span data-ttu-id="d4cf9-118">Резервное копирование Acronis для Linux</span><span class="sxs-lookup"><span data-stu-id="d4cf9-118">Acronis Backup Linux</span></span> | <span data-ttu-id="d4cf9-119">Расширение Docker</span><span class="sxs-lookup"><span data-stu-id="d4cf9-119">Docker Extension</span></span> | <span data-ttu-id="d4cf9-120">Агент Puppet</span><span class="sxs-lookup"><span data-stu-id="d4cf9-120">Puppet Agent</span></span> |
| <span data-ttu-id="d4cf9-121">Сведения о BG</span><span class="sxs-lookup"><span data-stu-id="d4cf9-121">Bg Info</span></span> | <span data-ttu-id="d4cf9-122">Расширение DSC</span><span class="sxs-lookup"><span data-stu-id="d4cf9-122">DSC Extension</span></span> | <span data-ttu-id="d4cf9-123">Site 24x7 для Apm Insight</span><span class="sxs-lookup"><span data-stu-id="d4cf9-123">Site 24x7 Apm Insight</span></span> |
| <span data-ttu-id="d4cf9-124">Агент BMC CTM для Linux</span><span class="sxs-lookup"><span data-stu-id="d4cf9-124">BMC CTM Agent Linux</span></span> | <span data-ttu-id="d4cf9-125">Dynatrace для Linux</span><span class="sxs-lookup"><span data-stu-id="d4cf9-125">Dynatrace Linux</span></span> | <span data-ttu-id="d4cf9-126">Site 24x7 для сервера Linux</span><span class="sxs-lookup"><span data-stu-id="d4cf9-126">Site 24x7 Linux Server</span></span> |
| <span data-ttu-id="d4cf9-127">Агент BMC CTM для Windows</span><span class="sxs-lookup"><span data-stu-id="d4cf9-127">BMC CTM Agent Windows</span></span> | <span data-ttu-id="d4cf9-128">Dynatrace для Windows</span><span class="sxs-lookup"><span data-stu-id="d4cf9-128">Dynatrace Windows</span></span> | <span data-ttu-id="d4cf9-129">Site 24x7 для сервера Windows Server</span><span class="sxs-lookup"><span data-stu-id="d4cf9-129">Site 24x7 Windows Server</span></span> |
| <span data-ttu-id="d4cf9-130">Клиент Chef</span><span class="sxs-lookup"><span data-stu-id="d4cf9-130">Chef Client</span></span> | <span data-ttu-id="d4cf9-131">Защитник приложений HPE Security</span><span class="sxs-lookup"><span data-stu-id="d4cf9-131">HPE Security Application Defender</span></span> | <span data-ttu-id="d4cf9-132">Trend Micro DSA</span><span class="sxs-lookup"><span data-stu-id="d4cf9-132">Trend Micro DSA</span></span> |
| <span data-ttu-id="d4cf9-133">Custom Script</span><span class="sxs-lookup"><span data-stu-id="d4cf9-133">Custom Script</span></span> | <span data-ttu-id="d4cf9-134">Защита от вредоносных программ IaaS</span><span class="sxs-lookup"><span data-stu-id="d4cf9-134">IaaS Antimalware</span></span> | <span data-ttu-id="d4cf9-135">Trend Micro DSA для Linux</span><span class="sxs-lookup"><span data-stu-id="d4cf9-135">Trend Micro DSA Linux</span></span> |
| <span data-ttu-id="d4cf9-136">Расширение пользовательских сценариев</span><span class="sxs-lookup"><span data-stu-id="d4cf9-136">Custom Script Extension</span></span> | <span data-ttu-id="d4cf9-137">Диагностика IaaS</span><span class="sxs-lookup"><span data-stu-id="d4cf9-137">IaaS Diagnostics</span></span> | <span data-ttu-id="d4cf9-138">VM Access для Linux</span><span class="sxs-lookup"><span data-stu-id="d4cf9-138">VM Access For Linux</span></span> |
| <span data-ttu-id="d4cf9-139">Custom Script для Linux</span><span class="sxs-lookup"><span data-stu-id="d4cf9-139">Custom Script for Linux</span></span> | <span data-ttu-id="d4cf9-140">Клиент Chef для Linux</span><span class="sxs-lookup"><span data-stu-id="d4cf9-140">Linux Chef Client</span></span> | <span data-ttu-id="d4cf9-141">VM Access для Linux</span><span class="sxs-lookup"><span data-stu-id="d4cf9-141">VM Access For Linux</span></span> |
| <span data-ttu-id="d4cf9-142">Агент Datadog для Linux</span><span class="sxs-lookup"><span data-stu-id="d4cf9-142">Datadog Linux Agent</span></span> | <span data-ttu-id="d4cf9-143">Диагностика Linux</span><span class="sxs-lookup"><span data-stu-id="d4cf9-143">Linux Diagnostic</span></span> | <span data-ttu-id="d4cf9-144">Моментальный снимок виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d4cf9-144">VM Snapshot</span></span> |

## <a name="export-hello-resource-group"></a><span data-ttu-id="d4cf9-145">Экспорт hello группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="d4cf9-145">Export hello Resource Group</span></span>

<span data-ttu-id="d4cf9-146">tooexport группу ресурсов в повторно используемый шаблон завершения hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="d4cf9-146">tooexport a Resource Group into a reusable template, complete hello following steps:</span></span>

1. <span data-ttu-id="d4cf9-147">Войдите в toohello портал Azure</span><span class="sxs-lookup"><span data-stu-id="d4cf9-147">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="d4cf9-148">Щелкните hello в главном меню, группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="d4cf9-148">On hello Hub Menu, click Resource Groups</span></span>
3. <span data-ttu-id="d4cf9-149">Выберите из списка hello hello целевой группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="d4cf9-149">Select hello target resource group from hello list</span></span>
4. <span data-ttu-id="d4cf9-150">В колонке hello группы ресурсов щелкните сценарий автоматизации</span><span class="sxs-lookup"><span data-stu-id="d4cf9-150">In hello Resource Group blade, click Automation Script</span></span>

![Экспорт шаблона](./media/extensions-export-templates/template-export.png)

<span data-ttu-id="d4cf9-152">Hello сценариев автоматизации Azure Resource Manager создает шаблона диспетчера ресурсов, файл параметров и несколько примеров сценариев развертывания, таких как Azure CLI и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-152">hello Azure Resource Manager automations script produces a Resource Manager template, a parameters file, and several sample deployment scripts such as PowerShell and Azure CLI.</span></span> <span data-ttu-id="d4cf9-153">На этом этапе hello экспортированный шаблон можно загрузить с помощью кнопки загрузки hello, добавляется новый библиотека шаблонов toohello шаблона или повторно развернуть с помощью hello кнопка "Развертывание".</span><span class="sxs-lookup"><span data-stu-id="d4cf9-153">At this point, hello exported template can be downloaded using hello download button, added as a new template toohello template library, or redeployed using hello deploy button.</span></span>

## <a name="configure-protected-settings"></a><span data-ttu-id="d4cf9-154">Настройка защищенных конфигураций</span><span class="sxs-lookup"><span data-stu-id="d4cf9-154">Configure protected settings</span></span>

<span data-ttu-id="d4cf9-155">Многие расширения виртуальной машины Azure поддерживают использование защищенных конфигураций, при котором шифруются конфиденциальные данные, например учетные данные и строки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-155">Many Azure virtual machine extensions include a protected settings configuration, that encrypts sensitive data such as credentials and configuration strings.</span></span> <span data-ttu-id="d4cf9-156">Защищенные параметры не экспортируются вместе с сценарий автоматизации hello.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-156">Protected settings are not exported with hello automation script.</span></span> <span data-ttu-id="d4cf9-157">При необходимости, защищенные параметры требуют toobe повторно hello экспортированный шаблон.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-157">If necessary, protected settings need toobe reinserted into hello exported templated.</span></span>

### <a name="step-1---remove-template-parameter"></a><span data-ttu-id="d4cf9-158">Шаг 1. Удаление параметра шаблона</span><span class="sxs-lookup"><span data-stu-id="d4cf9-158">Step 1 - Remove template parameter</span></span>

<span data-ttu-id="d4cf9-159">При создании tooprovide hello, который экспортируется группы ресурсов, один шаблон параметра toohello значение экспортированы защищенных параметров.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-159">When hello Resource Group is exported, a single template parameter is created tooprovide a value toohello exported protected settings.</span></span> <span data-ttu-id="d4cf9-160">Этот параметр можно удалить.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-160">This parameter can be removed.</span></span> <span data-ttu-id="d4cf9-161">параметр tooremove hello, просмотрите список параметров hello и удалить параметр hello, выполняющее аналогичный пример toothis JSON.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-161">tooremove hello parameter, look through hello parameter list and delete hello parameter that looks similar toothis JSON example.</span></span>

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a><span data-ttu-id="d4cf9-162">Шаг 2. Получение свойств защищенных конфигураций</span><span class="sxs-lookup"><span data-stu-id="d4cf9-162">Step 2 - Get protected settings properties</span></span>

<span data-ttu-id="d4cf9-163">Поскольку каждого защищенного параметра имеет набор обязательных свойств, список этих свойств должны toobe сбора.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-163">Because each protected setting has a set of required properties, a list of these properties need toobe gathered.</span></span> <span data-ttu-id="d4cf9-164">Каждый параметр hello защищенные параметры конфигурации можно найти в hello [схемы диспетчера ресурсов Azure на GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span><span class="sxs-lookup"><span data-stu-id="d4cf9-164">Each parameter of hello protected settings configuration can be found in hello [Azure Resource Manager schema on GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span></span> <span data-ttu-id="d4cf9-165">Эта схема включает только hello наборов параметров для расширений hello, перечисленные в разделе Обзор hello этого документа.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-165">This schema only includes hello parameter sets for hello extensions listed in hello overview section of this document.</span></span> 

<span data-ttu-id="d4cf9-166">Из в репозитории схемы hello, поиск hello требуемого расширения, в этом примере `IaaSDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-166">From within hello schema repository, search for hello desired extension, for this example `IaaSDiagnostics`.</span></span> <span data-ttu-id="d4cf9-167">Один раз hello расширения `protectedSettings` обнаружен объект, запишите каждого параметра.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-167">Once hello extensions `protectedSettings` object has been located, take note of each parameter.</span></span> <span data-ttu-id="d4cf9-168">В приведенном примере hello hello `IaasDiagnostic` модуль, hello требует параметры `storageAccountName`, `storageAccountKey`, и `storageAccountEndPoint`.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-168">In hello example of hello `IaasDiagnostic` extension, hello require parameters are `storageAccountName`, `storageAccountKey`, and `storageAccountEndPoint`.</span></span>

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-hello-protected-configuration"></a><span data-ttu-id="d4cf9-169">Шаг 3. повторно создать конфигурацию защищенных hello</span><span class="sxs-lookup"><span data-stu-id="d4cf9-169">Step 3 - Re-create hello protected configuration</span></span>

<span data-ttu-id="d4cf9-170">В случае hello экспортированный шаблон — поиск `protectedSettings` и замените экспортированного защищенных установки hello объекта новый, который включает параметры hello необходимые расширения и значение для каждого из них.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-170">On hello exported template, search for `protectedSettings` and replace hello exported protected setting object with a new one that includes hello required extension parameters and a value for each one.</span></span>

<span data-ttu-id="d4cf9-171">В приведенном примере hello hello `IaasDiagnostic` расширения, новая конфигурация защищенного параметр hello выглядит следующим образом hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="d4cf9-171">In hello example of hello `IaasDiagnostic` extension, hello new protected setting configuration would look like hello following example:</span></span>

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

<span data-ttu-id="d4cf9-172">Hello окончательным расширением ресурсов выглядит примерно toohello следующий пример JSON:</span><span class="sxs-lookup"><span data-stu-id="d4cf9-172">hello final extension resource looks similar toohello following JSON example:</span></span>

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

<span data-ttu-id="d4cf9-173">При использовании значений свойств tooprovide параметры шаблона, они должны toobe создан.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-173">If using template parameters tooprovide property values, these need toobe created.</span></span> <span data-ttu-id="d4cf9-174">При создании параметров шаблона для защищенного задание значений убедитесь, что hello toouse `SecureString` параметра типа, чтобы защищаются конфиденциальные значения.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-174">When creating template parameters for protected setting values, make sure toouse hello `SecureString` parameter type so that sensitive values are secured.</span></span> <span data-ttu-id="d4cf9-175">Дополнительную информацию об использовании параметров см. в статье [Создание шаблонов Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d4cf9-175">For more information on using parameters, see [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="d4cf9-176">В приведенном примере hello hello `IaasDiagnostic` расширения, будут создаваться hello следующие параметры в разделе параметров hello hello шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-176">In hello example of hello `IaasDiagnostic` extension, hello following parameters would be created in hello parameters section of hello Resource Manager template.</span></span>

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

<span data-ttu-id="d4cf9-177">На этом этапе hello шаблона могут быть развернуты с любой метод развертывания шаблона.</span><span class="sxs-lookup"><span data-stu-id="d4cf9-177">At this point, hello template can be deployed using any template deployment method.</span></span>
