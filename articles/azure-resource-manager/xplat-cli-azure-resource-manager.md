---
title: "Управление ресурсами с помощью интерфейса командной строки Azure | Документация Майкрософт"
description: "Используйте интерфейс командной строки Azure для управления ресурсами и группами ресурсов в Azure."
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3ad4e68b90979fd7f9d3ddf5278e65e19cb07152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-cli-to-manage-azure-resources-and-resource-groups"></a><span data-ttu-id="b43d3-103">Управление ресурсами и группами ресурсов Azure с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="b43d3-103">Use the Azure CLI to manage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b43d3-104">Портал</span><span class="sxs-lookup"><span data-stu-id="b43d3-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="b43d3-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="b43d3-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="b43d3-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b43d3-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="b43d3-107">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="b43d3-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="b43d3-108">Интерфейс командной строки Azure (Azure CLI) — это одно из нескольких средств для развертывания ресурсов, а также управления ими с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b43d3-108">The Azure Command-Line Interface (Azure CLI) is one of several tools you can use to deploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="b43d3-109">В этой статье описываются стандартные методы управления ресурсами и группами ресурсов Azure с помощью интерфейса командной строки Azure в режиме Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b43d3-109">This article introduces common ways to manage Azure resources and resource groups by using the Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="b43d3-110">Сведения о развертывании ресурсов с помощью интерфейса командной строки см. в статье [Развертывание ресурсов с использованием шаблонов Resource Manager и интерфейса командной строки Azure](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b43d3-110">For information about using the CLI to deploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="b43d3-111">Общие сведения о ресурсах Azure и Resource Manager см. в статье [Общие сведения об Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b43d3-111">For background about Azure resources and Resource Manager, visit the [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b43d3-112">Чтобы управлять ресурсами Azure с помощью интерфейса командной строки Azure, необходимо установить [интерфейс командной строки Azure](../cli-install-nodejs.md) и [войти в Azure](../xplat-cli-connect.md) с помощью команды `azure login`.</span><span class="sxs-lookup"><span data-stu-id="b43d3-112">To manage Azure resources with the Azure CLI, you need to [install the Azure CLI](../cli-install-nodejs.md), and [log in to Azure](../xplat-cli-connect.md) by using the `azure login` command.</span></span> <span data-ttu-id="b43d3-113">Убедитесь, что интерфейс командной строки работает в режиме Resource Manager (выполните команду `azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="b43d3-113">Make sure the CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="b43d3-114">Если все это уже сделано, у вас все готово для работы.</span><span class="sxs-lookup"><span data-stu-id="b43d3-114">If you've done these things, you're ready to go.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="b43d3-115">Получение сведений о ресурсах и группах ресурсов</span><span class="sxs-lookup"><span data-stu-id="b43d3-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="b43d3-116">Группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="b43d3-116">Resource groups</span></span>
<span data-ttu-id="b43d3-117">Чтобы получить список всех групп ресурсов в подписке и их расположения, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="b43d3-117">To get a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="b43d3-118">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="b43d3-118">Resources</span></span>
 <span data-ttu-id="b43d3-119">Чтобы получить список всех ресурсов в группе, например в группе *testRG*, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b43d3-119">To list all resources in a group, such as one with name *testRG*, use the following command:</span></span>

    azure resource list testRG

<span data-ttu-id="b43d3-120">Чтобы просмотреть отдельный ресурс в группе, например виртуальную машину *MyUbuntuVM*, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b43d3-120">To view an individual resource within the group, such as a VM named *MyUbuntuVM*, use a command like the following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="b43d3-121">Обратите внимание на параметр **Microsoft.Compute/virtualMachines**.</span><span class="sxs-lookup"><span data-stu-id="b43d3-121">Notice the **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="b43d3-122">Он указывает тип ресурса, для которого запрашивается информация.</span><span class="sxs-lookup"><span data-stu-id="b43d3-122">This parameter indicates the type of the resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="b43d3-123">При использовании команд **azure resource**, отличных от команды **list**, необходимо указать версию API ресурса с помощью параметра **-o**.</span><span class="sxs-lookup"><span data-stu-id="b43d3-123">When using the **azure resource** commands other than the **list** command, you must specify the API version of the resource with the **-o** parameter.</span></span> <span data-ttu-id="b43d3-124">Если вы не уверены, какая именно версия API используется, обратитесь к файлу шаблона и найдите поле apiVersion для этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="b43d3-124">If you're unsure about the API version, consult the template file and find the apiVersion field for the resource.</span></span> <span data-ttu-id="b43d3-125">Дополнительные сведения о версиях API в Resource Manager см. в статье о [поставщиках и типах ресурсов](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="b43d3-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="b43d3-126">При просмотре сведений о ресурсе часто бывает полезно использовать параметр `--json`.</span><span class="sxs-lookup"><span data-stu-id="b43d3-126">When viewing details on a resource, it is often useful to use the `--json` parameter.</span></span> <span data-ttu-id="b43d3-127">Он делает выходные данные более удобными для чтения, так как некоторые значения — это вложенные структуры или коллекции.</span><span class="sxs-lookup"><span data-stu-id="b43d3-127">This parameter makes the output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="b43d3-128">В следующем примере результаты команды **show** возвращаются в виде документа JSON.</span><span class="sxs-lookup"><span data-stu-id="b43d3-128">The following example demonstrates returning the results of the **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="b43d3-129">При желании сохраните данные JSON в файл, используя символ &gt; для перенаправления выходных данных в файл.</span><span class="sxs-lookup"><span data-stu-id="b43d3-129">If you want, save the JSON data to file by using the &gt; character to direct the output to a file.</span></span> <span data-ttu-id="b43d3-130">Например:</span><span class="sxs-lookup"><span data-stu-id="b43d3-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="b43d3-131">Теги</span><span class="sxs-lookup"><span data-stu-id="b43d3-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="b43d3-132">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="b43d3-132">Manage resources</span></span>
<span data-ttu-id="b43d3-133">Чтобы добавить ресурс, например учетную запись хранения, в группу ресурсов, выполните команду, аналогичную следующей.</span><span class="sxs-lookup"><span data-stu-id="b43d3-133">To add a resource such as a storage account to a resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="b43d3-134">Наряду с параметром **-o**, с помощью которого можно указать версию API, также можно использовать параметр **-p**, чтобы передать строку с любыми обязательными или дополнительными свойствами в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="b43d3-134">In addition to specifying the API version of the resource with the **-o** parameter, use the **-p** parameter to pass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="b43d3-135">Чтобы удалить имеющийся ресурс, например ресурс виртуальной машины, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b43d3-135">To delete an existing resource such as a virtual machine resource, use a command like the following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="b43d3-136">Чтобы переместить существующие ресурсы в другую группу или подписку, используйте команду **azure resource move** .</span><span class="sxs-lookup"><span data-stu-id="b43d3-136">To move existing resources to another resource group or subscription, use the **azure resource move** command.</span></span> <span data-ttu-id="b43d3-137">В следующем примере показано, как переместить кэш Redis в новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b43d3-137">The following example shows how to move a Redis Cache to a new resource group.</span></span> <span data-ttu-id="b43d3-138">В параметре **-i** укажите разделенный запятыми список идентификаторов ресурсов для перемещения.</span><span class="sxs-lookup"><span data-stu-id="b43d3-138">In the **-i** parameter, provide a comma-separated list of the resource id's to move.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-to-resources"></a><span data-ttu-id="b43d3-139">Управление доступом к ресурсам</span><span class="sxs-lookup"><span data-stu-id="b43d3-139">Control access to resources</span></span>
<span data-ttu-id="b43d3-140">Интерфейс командной строки Azure можно использовать, чтобы создавать политики управления доступом к ресурсам Azure, а также управлять ими.</span><span class="sxs-lookup"><span data-stu-id="b43d3-140">You can use the Azure CLI to create and manage policies to control access to Azure resources.</span></span> <span data-ttu-id="b43d3-141">Общие сведения об определениях политик и назначении политик ресурсам см. в статье [Применение политик для управления ресурсами и контроля доступа](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="b43d3-141">For background about policy definitions and assigning policies to resources, see [Use policy to manage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="b43d3-142">Например, чтобы отклонять все запросы, полученные не из региона "Западная часть США" или "Северо-центральный регион США", определите следующую политику и сохраните ее в файл определения политики policy.json.</span><span class="sxs-lookup"><span data-stu-id="b43d3-142">For example, define the following policy to deny all requests where location is not West US or North Central US, and save it to the policy definition file policy.json:</span></span>

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

<span data-ttu-id="b43d3-143">Затем выполните команду **policy definition create**.</span><span class="sxs-lookup"><span data-stu-id="b43d3-143">Then run the **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="b43d3-144">После выполнения команды должен появиться результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="b43d3-144">This command shows output similar to the following:</span></span>

    + <span data-ttu-id="b43d3-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="b43d3-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="b43d3-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span><span class="sxs-lookup"><span data-stu-id="b43d3-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="b43d3-147">Чтобы назначить политику в определенной области, используйте свойство **PolicyDefinitionId**, возвращенное в предыдущей команде.</span><span class="sxs-lookup"><span data-stu-id="b43d3-147">To assign a policy at the scope you want, use the **PolicyDefinitionId** returned from the previous command.</span></span> <span data-ttu-id="b43d3-148">В следующем примере в качестве этой области выступает подписка, но политику также можно назначить группе ресурсов или отдельным ресурсам.</span><span class="sxs-lookup"><span data-stu-id="b43d3-148">In the following example, this scope is the subscription, but you can scope to resource groups or individual resources:</span></span>

    <span data-ttu-id="b43d3-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span><span class="sxs-lookup"><span data-stu-id="b43d3-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="b43d3-150">С помощью команд **policy definition show**, **policy definition set** и **policy definition delete** можно получить, изменить или удалить определения политики.</span><span class="sxs-lookup"><span data-stu-id="b43d3-150">You can get, change, or remove policy definitions by using the **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="b43d3-151">Аналогичным образом с помощью команд **policy assignment show**, **policy assignment set** и **policy assignment delete** можно получить, изменить или удалить назначения политики.</span><span class="sxs-lookup"><span data-stu-id="b43d3-151">Similarly, you can get, change, or remove policy assignments by using the **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="b43d3-152">Экспорт группы ресурсов в виде шаблона</span><span class="sxs-lookup"><span data-stu-id="b43d3-152">Export a resource group as a template</span></span>
<span data-ttu-id="b43d3-153">Вы можете просмотреть шаблон Resource Manager для любой существующей группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b43d3-153">For an existing resource group, you can view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="b43d3-154">Экспорт шаблона обеспечивает два преимущества:</span><span class="sxs-lookup"><span data-stu-id="b43d3-154">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="b43d3-155">Последующие развертывания решения можно с легкостью автоматизировать, так как в шаблоне определены все компоненты инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="b43d3-155">You can easily automate future deployments of the solution because all the infrastructure is defined in the template.</span></span>
2. <span data-ttu-id="b43d3-156">Вы можете ознакомиться с синтаксисом шаблона, просмотрев представление JSON для своего решения.</span><span class="sxs-lookup"><span data-stu-id="b43d3-156">You can become familiar with template syntax by looking at the JSON that represents your solution.</span></span>

<span data-ttu-id="b43d3-157">С помощью интерфейса командной строки Azure вы можете экспортировать шаблон, который представляет текущее состояние группы ресурсов, или скачать шаблон, который использовался для конкретного развертывания.</span><span class="sxs-lookup"><span data-stu-id="b43d3-157">Using the Azure CLI, you can either export a template that represents the current state of your resource group, or download the template that was used for a particular deployment.</span></span>

* <span data-ttu-id="b43d3-158">**Экспорт шаблона для группы ресурсов** удобно использовать, если вы изменили группу ресурсов и хотите получить представление JSON ее текущего состояния.</span><span class="sxs-lookup"><span data-stu-id="b43d3-158">**Export the template for a resource group** - This is helpful when you made changes to a resource group, and need to retrieve the JSON representation of its current state.</span></span> <span data-ttu-id="b43d3-159">Однако созданный шаблон содержит только минимальное число параметров, и в нем не указаны какие-либо переменные.</span><span class="sxs-lookup"><span data-stu-id="b43d3-159">However, the generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="b43d3-160">Большая часть значений в шаблоне заданы жестко.</span><span class="sxs-lookup"><span data-stu-id="b43d3-160">Most of the values in the template are hard-coded.</span></span> <span data-ttu-id="b43d3-161">Прежде чем развертывать созданный шаблон, можно преобразовать дополнительные значения в параметры, чтобы настроить развертывание для разных сред.</span><span class="sxs-lookup"><span data-stu-id="b43d3-161">Before deploying the generated template, you may wish to convert more of the values into parameters so you can customize the deployment for different environments.</span></span>
  
    <span data-ttu-id="b43d3-162">Чтобы экспортировать шаблон для группы ресурсов в локальный каталог, выполните команду `azure group export`, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="b43d3-162">To export the template for a resource group to a local directory, run the `azure group export` command as shown in the following example.</span></span> <span data-ttu-id="b43d3-163">(Замените указанный в примере локальный каталог каталогом, используемым в вашей операционной системе.)</span><span class="sxs-lookup"><span data-stu-id="b43d3-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="b43d3-164">**Экспорт шаблона для конкретного развертывания** удобно использовать, если нужно просмотреть шаблон, с помощью которого были развернуты ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b43d3-164">**Download the template for a particular deployment** -- This is helpful when you need to view the actual template that was used to deploy resources.</span></span> <span data-ttu-id="b43d3-165">Этот шаблон содержит все параметры и переменные, определенные для исходного развертывания.</span><span class="sxs-lookup"><span data-stu-id="b43d3-165">The template includes all parameters and variables defined for the original deployment.</span></span> <span data-ttu-id="b43d3-166">Тем не менее если кто-то в организации внес изменения в группу ресурсов, в частности в параметры вне шаблона, этот шаблон не будет представлять текущее состояние группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b43d3-166">However, if someone in your organization made changes to the resource group outside of the definition in the template, this template doesn't represent the current state of the resource group.</span></span>
  
    <span data-ttu-id="b43d3-167">Чтобы скачать в локальный каталог шаблон для конкретного развертывания, выполните команду `azure group deployment template download`.</span><span class="sxs-lookup"><span data-stu-id="b43d3-167">To download the template used for a particular deployment to a local directory, run the `azure group deployment template download` command.</span></span> <span data-ttu-id="b43d3-168">Например:</span><span class="sxs-lookup"><span data-stu-id="b43d3-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="b43d3-169">Так как функция экспорта шаблона пока доступна в предварительной версии, поддерживаются не все типы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b43d3-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="b43d3-170">При попытке экспорта шаблона может появиться сообщение о том, что некоторые ресурсы не экспортированы.</span><span class="sxs-lookup"><span data-stu-id="b43d3-170">When attempting to export a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="b43d3-171">При необходимости эти ресурсы можно определить вручную после скачивания шаблона.</span><span class="sxs-lookup"><span data-stu-id="b43d3-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b43d3-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b43d3-172">Next steps</span></span>
* <span data-ttu-id="b43d3-173">Дополнительные сведения об операциях развертывания и устранении неполадок, связанных с развертыванием, см. в статье [Просмотр операций развертывания с помощью Azure Resource Manager](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="b43d3-173">To get details of deployment operations and troubleshoot deployment errors with the Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="b43d3-174">Сведения о настройке приложения или скрипта для доступа к ресурсам с помощью интерфейса командной строки см. в статье [Использование интерфейса командной строки Azure для создания субъекта-службы и доступа к ресурсам](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b43d3-174">If you want to use the CLI to set up an application or script to access resources, see [Use Azure CLI to create a service principal to access resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="b43d3-175">Руководство по использованию Resource Manager для эффективного управления подписками в организациях см [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Шаблон Azure для организаций. Рекомендуемая система управления подпиской).</span><span class="sxs-lookup"><span data-stu-id="b43d3-175">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

