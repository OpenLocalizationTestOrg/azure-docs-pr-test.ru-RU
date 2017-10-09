---
title: "шаблоны toocheck aaaUse шаблона проверяющий элемент управления для Azure стек | Документы Microsoft"
description: "Проверьте шаблоны для развертывания tooAzure стека"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d9e6aee1-4cba-4df5-b5a3-6f38da9627a3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: helaw
ms.openlocfilehash: ee649f2ebf77486ca5036116dd73a45d66884704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="check-your-templates-for-azure-stack-with-template-validator"></a><span data-ttu-id="139c1-103">Проверьте свои шаблоны для стека Azure с помощью шаблона проверяющий элемент управления</span><span class="sxs-lookup"><span data-stu-id="139c1-103">Check your templates for Azure Stack with Template Validator</span></span>
<span data-ttu-id="139c1-104">Можно использовать toocheck средство проверки шаблона hello, если диспетчер ресурсов Azure [шаблоны](azure-stack-arm-templates.md) готовы для Azure стека.</span><span class="sxs-lookup"><span data-stu-id="139c1-104">You can use hello template validation tool toocheck if your Azure Resource Manager [templates](azure-stack-arm-templates.md) are ready for Azure Stack.</span></span> <span data-ttu-id="139c1-105">Средство проверки шаблона Hello доступен как часть средств Azure стека hello.</span><span class="sxs-lookup"><span data-stu-id="139c1-105">hello template validation tool is available as a part of hello Azure Stack tools.</span></span> <span data-ttu-id="139c1-106">Загрузить набор средств hello Azure стека с помощью hello действия, описанные в hello [загрузить набор средств из GitHub](azure-stack-powershell-download.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="139c1-106">Download hello Azure Stack tools by using hello steps described in hello [download tools from GitHub](azure-stack-powershell-download.md) article.</span></span> 

<span data-ttu-id="139c1-107">шаблоны toovalidate использовать следующие модули PowerShell hello и hello JSON-файл расположен в **TemplateValidator** и **CloudCapabilities** папок:</span><span class="sxs-lookup"><span data-stu-id="139c1-107">toovalidate templates, you use hello following PowerShell modules and hello JSON file located in **TemplateValidator** and **CloudCapabilities** folders:</span></span> 

 - <span data-ttu-id="139c1-108">AzureRM.CloudCapabilities.psm1 создает файл JSON возможности облака, представляющий службы hello и версии в облаке как стек Azure.</span><span class="sxs-lookup"><span data-stu-id="139c1-108">AzureRM.CloudCapabilities.psm1 creates a cloud capabilities JSON file representing hello services and versions in a cloud like Azure Stack.</span></span>
 - <span data-ttu-id="139c1-109">AzureRM.TemplateValidator.psm1 использует возможности облачной среды шаблонов tootest файлов JSON для развертывания в Azure стека.</span><span class="sxs-lookup"><span data-stu-id="139c1-109">AzureRM.TemplateValidator.psm1 uses a cloud capabilities JSON file tootest templates for deployment in Azure Stack.</span></span>
 - <span data-ttu-id="139c1-110">AzureStackCloudCapabilities_with_AddOns_20170627.json — это файл возможностей облака по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="139c1-110">AzureStackCloudCapabilities_with_AddOns_20170627.json is a default cloud capabilities file.</span></span>  <span data-ttu-id="139c1-111">Можно создавать собственные или использовать этот файл, tooget работы.</span><span class="sxs-lookup"><span data-stu-id="139c1-111">You can create your own, or use this file tooget started.</span></span> 

<span data-ttu-id="139c1-112">В этом разделе выполнить проверку шаблоны и при необходимости создайте файл возможностей облака.</span><span class="sxs-lookup"><span data-stu-id="139c1-112">In this topic, you run validation against your templates, and optionally build a cloud capabilities file.</span></span>

## <a name="validate-templates"></a><span data-ttu-id="139c1-113">Проверить шаблоны</span><span class="sxs-lookup"><span data-stu-id="139c1-113">Validate templates</span></span>
<span data-ttu-id="139c1-114">В этом пошаговом руководстве проверить шаблоны с помощью модуля AzureRM.TemplateValidator PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="139c1-114">In these steps, you validate templates by using hello AzureRM.TemplateValidator PowerShell module.</span></span> <span data-ttu-id="139c1-115">Можно использовать собственные шаблоны, или проверить hello [быстрый запуск Azure стека шаблоны](https://github.com/Azure/AzureStack-QuickStart-Templates).</span><span class="sxs-lookup"><span data-stu-id="139c1-115">You can use your own templates, or validate hello [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates).</span></span>

1.  <span data-ttu-id="139c1-116">Импортируйте модуль AzureRM.TemplateValidator.psm1 PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="139c1-116">Import hello AzureRM.TemplateValidator.psm1 PowerShell module:</span></span>
    
    ```PowerShell
    cd "c:\AzureStack-Tools-master\TemplateValidator"
    Import-Module .\AzureRM.TemplateValidator.psm1
    ```

2.  <span data-ttu-id="139c1-117">Выполните hello шаблона проверяющий элемент управления.</span><span class="sxs-lookup"><span data-stu-id="139c1-117">Run hello template validator:</span></span>

    ```PowerShell
    Test-AzureRMTemplate -TemplatePath <path tootemplate.json or template folder> `
    -CapabilitiesPath <path toocloudcapabilities.json> `
    -Verbose
    ```

<span data-ttu-id="139c1-118">Любой шаблон предупреждений и ошибок проверки являются toohello регистрируется консоли PowerShell и — журнал tooan HTML-файл в исходной папке hello.</span><span class="sxs-lookup"><span data-stu-id="139c1-118">Any template validation warnings or errors are logged toohello PowerShell console, and are also logged tooan HTML file in hello source directory.</span></span> <span data-ttu-id="139c1-119">Пример выходных данных отчетов проверки hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="139c1-119">An example of hello validation report output looks like this:</span></span>

![отчет о проверке образца](./media/azure-stack-validate-templates/image1.png)

### <a name="parameters"></a><span data-ttu-id="139c1-121">Параметры</span><span class="sxs-lookup"><span data-stu-id="139c1-121">Parameters</span></span>

| <span data-ttu-id="139c1-122">Параметр</span><span class="sxs-lookup"><span data-stu-id="139c1-122">Parameter</span></span> | <span data-ttu-id="139c1-123">Описание</span><span class="sxs-lookup"><span data-stu-id="139c1-123">Description</span></span> | <span data-ttu-id="139c1-124">Обязательно</span><span class="sxs-lookup"><span data-stu-id="139c1-124">Required</span></span> |
| ----- | -----| ----- |
| <span data-ttu-id="139c1-125">TemplatePath</span><span class="sxs-lookup"><span data-stu-id="139c1-125">TemplatePath</span></span> | <span data-ttu-id="139c1-126">Указывает путь toorecursively hello найти шаблоны диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="139c1-126">Specifies hello path toorecursively find Resource Manager templates</span></span> | <span data-ttu-id="139c1-127">Да</span><span class="sxs-lookup"><span data-stu-id="139c1-127">Yes</span></span> | 
| <span data-ttu-id="139c1-128">TemplatePattern</span><span class="sxs-lookup"><span data-stu-id="139c1-128">TemplatePattern</span></span> | <span data-ttu-id="139c1-129">Указывает имя hello toomatch файлы шаблона.</span><span class="sxs-lookup"><span data-stu-id="139c1-129">Specifies hello name of template files toomatch.</span></span> | <span data-ttu-id="139c1-130">Нет</span><span class="sxs-lookup"><span data-stu-id="139c1-130">No</span></span> |
| <span data-ttu-id="139c1-131">CapabilitiesPath</span><span class="sxs-lookup"><span data-stu-id="139c1-131">CapabilitiesPath</span></span> | <span data-ttu-id="139c1-132">Указывает hello путь toocloud возможности JSON-файла</span><span class="sxs-lookup"><span data-stu-id="139c1-132">Specifies hello path toocloud capabilities JSON file</span></span> | <span data-ttu-id="139c1-133">Да</span><span class="sxs-lookup"><span data-stu-id="139c1-133">Yes</span></span> | 
| <span data-ttu-id="139c1-134">IncludeComputeCapabilities</span><span class="sxs-lookup"><span data-stu-id="139c1-134">IncludeComputeCapabilities</span></span> | <span data-ttu-id="139c1-135">Включает в себя оценки IaaS ресурсов, таких как размеров ВМ и расширения ВМ</span><span class="sxs-lookup"><span data-stu-id="139c1-135">Includes evaluation of IaaS resources like VM Sizes and VM Extensions</span></span> | <span data-ttu-id="139c1-136">Нет</span><span class="sxs-lookup"><span data-stu-id="139c1-136">No</span></span> |
| <span data-ttu-id="139c1-137">IncludeStorageCapabilities</span><span class="sxs-lookup"><span data-stu-id="139c1-137">IncludeStorageCapabilities</span></span> | <span data-ttu-id="139c1-138">Включает в себя оценки ресурсов хранения, таких как типы SKU</span><span class="sxs-lookup"><span data-stu-id="139c1-138">Includes evaluation of storage resources like SKU types</span></span> | <span data-ttu-id="139c1-139">Нет</span><span class="sxs-lookup"><span data-stu-id="139c1-139">No</span></span> |
| <span data-ttu-id="139c1-140">Отчет</span><span class="sxs-lookup"><span data-stu-id="139c1-140">Report</span></span> | <span data-ttu-id="139c1-141">Указывает, что имя hello созданный отчет HTML</span><span class="sxs-lookup"><span data-stu-id="139c1-141">Specifies name of hello generated HTML report</span></span> | <span data-ttu-id="139c1-142">Нет</span><span class="sxs-lookup"><span data-stu-id="139c1-142">No</span></span> |
| <span data-ttu-id="139c1-143">Подробная информация</span><span class="sxs-lookup"><span data-stu-id="139c1-143">Verbose</span></span> | <span data-ttu-id="139c1-144">Журналы ошибок и предупреждений toohello консоли</span><span class="sxs-lookup"><span data-stu-id="139c1-144">Logs errors and warnings toohello console</span></span> | <span data-ttu-id="139c1-145">Нет</span><span class="sxs-lookup"><span data-stu-id="139c1-145">No</span></span>|


### <a name="examples"></a><span data-ttu-id="139c1-146">Примеры</span><span class="sxs-lookup"><span data-stu-id="139c1-146">Examples</span></span>
<span data-ttu-id="139c1-147">В этом примере проверяет все hello [быстрый запуск Azure стека шаблоны](https://github.com/Azure/AzureStack-QuickStart-Templates) загружен локально, а также проверяет hello размеров ВМ и расширения относительно возможностей Azure стека Development Kit.</span><span class="sxs-lookup"><span data-stu-id="139c1-147">This example validates all hello [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates) downloaded locally, and also validates hello VM sizes and extensions against Azure Stack Development Kit capabilities.</span></span>

```PowerShell
test-AzureRMTemplate -TemplatePath C:\AzureStack-Quickstart-Templates `
-CapabilitiesPath .\TemplateValidator\AzureStackCloudCapabilities_with_AddOns_20170627.json.json `
-TemplatePattern MyStandardTemplateName.json`
-IncludeComputeCapabilities`
-Report TemplateReport.html
```

## <a name="build-cloud-capabilities-file"></a><span data-ttu-id="139c1-148">Построение файла возможностей облака</span><span class="sxs-lookup"><span data-stu-id="139c1-148">Build cloud capabilities file</span></span>
<span data-ttu-id="139c1-149">Hello загруженные файлы включают значение по умолчанию *AzureStackCloudCapabilities_with_AddOns_20170627.json* файл, который описывает доступны в пакете средств разработки Azure стека hello службы версии с установленными службами PaaS.</span><span class="sxs-lookup"><span data-stu-id="139c1-149">hello downloaded files include a default *AzureStackCloudCapabilities_with_AddOns_20170627.json* file, which describes hello service versions available in Azure Stack Development Kit with PaaS services installed.</span></span>  <span data-ttu-id="139c1-150">Если установить дополнительные поставщики ресурсов, можно использовать hello toobuild модуль AzureRM.CloudCapabilities PowerShell JSON-файла, включая новые службы hello.</span><span class="sxs-lookup"><span data-stu-id="139c1-150">If you install additional Resource Providers, you can use hello AzureRM.CloudCapabilities PowerShell module toobuild a JSON file including hello new services.</span></span>  

1.  <span data-ttu-id="139c1-151">Убедитесь, что у вас есть подключение tooAzure стека.</span><span class="sxs-lookup"><span data-stu-id="139c1-151">Make sure you have connectivity tooAzure Stack.</span></span>  <span data-ttu-id="139c1-152">Эти шаги можно выполнить на узел комплект средств для разработки Azure стека hello, или можно использовать [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) tooconnect с рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="139c1-152">These steps can be performed from hello Azure Stack development kit host, or you can use [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) tooconnect from your workstation.</span></span> 
2.  <span data-ttu-id="139c1-153">Импортируйте модуль AzureRM.CloudCapabilities PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="139c1-153">Import hello AzureRM.CloudCapabilities PowerShell module:</span></span>

    ```PowerShell
    Import-Module .\CloudCapabilities\AzureRM.CloudCapabilities.psm1
    ``` 

3.  <span data-ttu-id="139c1-154">Используют версии обновления tooretrieve командлет Get-CloudCapabilities hello и создать файл JSON возможностей облака:</span><span class="sxs-lookup"><span data-stu-id="139c1-154">Use hello Get-CloudCapabilities cmdlet tooretrieve service versions and create a cloud capabilities JSON file:</span></span>

    ```PowerShell
    Get-AzureRMCloudCapabilities -Location 'local' -Verbose
    ```             


## <a name="next-steps"></a><span data-ttu-id="139c1-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="139c1-155">Next steps</span></span>
 - [<span data-ttu-id="139c1-156">Развертывание шаблонов tooAzure стека</span><span class="sxs-lookup"><span data-stu-id="139c1-156">Deploy templates tooAzure Stack</span></span>](azure-stack-arm-templates.md)
 - <span data-ttu-id="139c1-157">[Разработки шаблонов для стека Azure] (azure стека разрабатывать templates.md)</span><span class="sxs-lookup"><span data-stu-id="139c1-157">[Develop templates for Azure Stack] (azure-stack-develop-templates.md)</span></span>

