---
title: "ресурсы aaaManage с hello Azure CLI | Документы Microsoft"
description: "Использовать toomanage Azure интерфейс командной строки (CLI) hello Azure ресурсов и групп"
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
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a><span data-ttu-id="3b96c-103">Использовать toomanage Azure CLI hello Azure ресурсов и групп ресурсов</span><span class="sxs-lookup"><span data-stu-id="3b96c-103">Use hello Azure CLI toomanage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3b96c-104">Портал</span><span class="sxs-lookup"><span data-stu-id="3b96c-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="3b96c-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="3b96c-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="3b96c-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b96c-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="3b96c-107">REST API</span><span class="sxs-lookup"><span data-stu-id="3b96c-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="3b96c-108">Hello Azure командной строки (CLI Azure) является одним из нескольких средств можно использовать toodeploy и управление ресурсами с помощью диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3b96c-108">hello Azure Command-Line Interface (Azure CLI) is one of several tools you can use toodeploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="3b96c-109">В этой статье описаны распространенные способы toomanage Azure ресурсов и групп ресурсов с помощью hello Azure CLI в режим диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3b96c-109">This article introduces common ways toomanage Azure resources and resource groups by using hello Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="3b96c-110">Сведения об использовании ресурсов toodeploy hello CLI см. в разделе [развертывания ресурсов с помощью шаблонов диспетчера ресурсов и Azure CLI](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3b96c-110">For information about using hello CLI toodeploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="3b96c-111">Дополнительные сведения о ресурсах Azure и диспетчер ресурсов посетите hello [Обзор диспетчера ресурсов Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b96c-111">For background about Azure resources and Resource Manager, visit hello [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3b96c-112">toomanage Azure ресурсы с hello Azure CLI требуется слишком[установить hello Azure CLI](../cli-install-nodejs.md), и [вход tooAzure](../xplat-cli-connect.md) с помощью hello `azure login` команды.</span><span class="sxs-lookup"><span data-stu-id="3b96c-112">toomanage Azure resources with hello Azure CLI, you need too[install hello Azure CLI](../cli-install-nodejs.md), and [log in tooAzure](../xplat-cli-connect.md) by using hello `azure login` command.</span></span> <span data-ttu-id="3b96c-113">Убедитесь, что hello CLI находится в режиме диспетчера ресурсов (запустить `azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="3b96c-113">Make sure hello CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="3b96c-114">Если вы сделали это, вы готовы toogo.</span><span class="sxs-lookup"><span data-stu-id="3b96c-114">If you've done these things, you're ready toogo.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="3b96c-115">Получение сведений о ресурсах и группах ресурсов</span><span class="sxs-lookup"><span data-stu-id="3b96c-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="3b96c-116">Группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="3b96c-116">Resource groups</span></span>
<span data-ttu-id="3b96c-117">tooget список всех групп ресурсов в подписке и их расположения, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="3b96c-117">tooget a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="3b96c-118">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="3b96c-118">Resources</span></span>
 <span data-ttu-id="3b96c-119">имя всех ресурсов в группе, например с toolist *testRG*, использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3b96c-119">toolist all resources in a group, such as one with name *testRG*, use hello following command:</span></span>

    azure resource list testRG

<span data-ttu-id="3b96c-120">отдельный ресурс в группе hello, такие как виртуальная машина с именем tooview *MyUbuntuVM*, используйте команду hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3b96c-120">tooview an individual resource within hello group, such as a VM named *MyUbuntuVM*, use a command like hello following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="3b96c-121">Обратите внимание hello **Microsoft.Compute/virtualMachines** параметра.</span><span class="sxs-lookup"><span data-stu-id="3b96c-121">Notice hello **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="3b96c-122">Этот параметр указывает тип hello hello ресурса, который вы запрашиваете сведения.</span><span class="sxs-lookup"><span data-stu-id="3b96c-122">This parameter indicates hello type of hello resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="3b96c-123">При использовании hello **ресурсов azure** команд, отличных от hello **списка** команды необходимо указать версию hello API hello ресурса с hello **-o** параметра.</span><span class="sxs-lookup"><span data-stu-id="3b96c-123">When using hello **azure resource** commands other than hello **list** command, you must specify hello API version of hello resource with hello **-o** parameter.</span></span> <span data-ttu-id="3b96c-124">Если вы знаете о версии API hello, просмотрите файл шаблона hello и найти поле apiVersion hello для ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="3b96c-124">If you're unsure about hello API version, consult hello template file and find hello apiVersion field for hello resource.</span></span> <span data-ttu-id="3b96c-125">Дополнительные сведения о версиях API в Resource Manager см. в статье о [поставщиках и типах ресурсов](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="3b96c-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="3b96c-126">При просмотре сведений о ресурсе, часто бывает полезно toouse hello `--json` параметра.</span><span class="sxs-lookup"><span data-stu-id="3b96c-126">When viewing details on a resource, it is often useful toouse hello `--json` parameter.</span></span> <span data-ttu-id="3b96c-127">Этот параметр становится вывода hello удобнее, так как некоторые значения являются вложенными структурами или коллекций.</span><span class="sxs-lookup"><span data-stu-id="3b96c-127">This parameter makes hello output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="3b96c-128">Hello следующем примере показано возвращение результатов hello hello **Показать** как документ JSON.</span><span class="sxs-lookup"><span data-stu-id="3b96c-128">hello following example demonstrates returning hello results of hello **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="3b96c-129">Если требуется, сохраните hello toofile данных JSON с помощью hello &gt; tooa выходной файл для символа toodirect hello.</span><span class="sxs-lookup"><span data-stu-id="3b96c-129">If you want, save hello JSON data toofile by using hello &gt; character toodirect hello output tooa file.</span></span> <span data-ttu-id="3b96c-130">Например:</span><span class="sxs-lookup"><span data-stu-id="3b96c-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="3b96c-131">Теги</span><span class="sxs-lookup"><span data-stu-id="3b96c-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="3b96c-132">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="3b96c-132">Manage resources</span></span>
<span data-ttu-id="3b96c-133">tooadd ресурсов, таких как группы ресурсов tooa учетной записи хранилища, выполните команду, подобную:</span><span class="sxs-lookup"><span data-stu-id="3b96c-133">tooadd a resource such as a storage account tooa resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="3b96c-134">В дополнение к этому toospecifying hello версии API-интерфейса hello ресурсов с hello **-o** параметр, используйте hello **-p** строку формата JSON toopass параметр с все необходимые или дополнительные свойства.</span><span class="sxs-lookup"><span data-stu-id="3b96c-134">In addition toospecifying hello API version of hello resource with hello **-o** parameter, use hello **-p** parameter toopass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="3b96c-135">toodelete существующий ресурс, например, ресурсы виртуальной машины, используйте команду hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3b96c-135">toodelete an existing resource such as a virtual machine resource, use a command like hello following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="3b96c-136">toomove существующую группу ресурсов tooanother ресурсов или подписку, используйте hello **перемещение ресурсов azure** команды.</span><span class="sxs-lookup"><span data-stu-id="3b96c-136">toomove existing resources tooanother resource group or subscription, use hello **azure resource move** command.</span></span> <span data-ttu-id="3b96c-137">Следующий пример показывает как Hello toomove tooa кэша Redis новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3b96c-137">hello following example shows how toomove a Redis Cache tooa new resource group.</span></span> <span data-ttu-id="3b96c-138">В hello **-i** параметр, укажите идентификатор ресурса hello toomove список разделенных запятыми.</span><span class="sxs-lookup"><span data-stu-id="3b96c-138">In hello **-i** parameter, provide a comma-separated list of hello resource id's toomove.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a><span data-ttu-id="3b96c-139">Tooresources управления доступом</span><span class="sxs-lookup"><span data-stu-id="3b96c-139">Control access tooresources</span></span>
<span data-ttu-id="3b96c-140">Можно использовать toocreate hello Azure CLI и управлять ресурсами tooAzure доступа toocontrol политики.</span><span class="sxs-lookup"><span data-stu-id="3b96c-140">You can use hello Azure CLI toocreate and manage policies toocontrol access tooAzure resources.</span></span> <span data-ttu-id="3b96c-141">Основные сведения о определения политик и назначение политики tooresources см. в разделе [использовать ресурсы toomanage политики и управления доступом](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="3b96c-141">For background about policy definitions and assigning policies tooresources, see [Use policy toomanage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="3b96c-142">Например определите следующие политики toodeny hello все запросы, где местоположение не Запад США или North Central US и сохраните его policy.json файла определения политики toohello:</span><span class="sxs-lookup"><span data-stu-id="3b96c-142">For example, define hello following policy toodeny all requests where location is not West US or North Central US, and save it toohello policy definition file policy.json:</span></span>

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

<span data-ttu-id="3b96c-143">Затем запустите hello **Создание определения политики** команды:</span><span class="sxs-lookup"><span data-stu-id="3b96c-143">Then run hello **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="3b96c-144">Эта команда показывает, как toohello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="3b96c-144">This command shows output similar toohello following:</span></span>

    + <span data-ttu-id="3b96c-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="3b96c-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="3b96c-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span><span class="sxs-lookup"><span data-stu-id="3b96c-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="3b96c-147">tooassign политику в области hello, требуется, используйте hello **PolicyDefinitionId** возвращенные hello предыдущей команды.</span><span class="sxs-lookup"><span data-stu-id="3b96c-147">tooassign a policy at hello scope you want, use hello **PolicyDefinitionId** returned from hello previous command.</span></span> <span data-ttu-id="3b96c-148">В следующем примере hello эта область является hello подписки, но вы можете задать область tooresource групп или отдельных ресурсов:</span><span class="sxs-lookup"><span data-stu-id="3b96c-148">In hello following example, this scope is hello subscription, but you can scope tooresource groups or individual resources:</span></span>

    <span data-ttu-id="3b96c-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span><span class="sxs-lookup"><span data-stu-id="3b96c-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="3b96c-150">Можно получить, изменение или удаление определения политики с помощью hello **Показать определения политики**, **набор определения политики**, и **удаление определения политики** команд.</span><span class="sxs-lookup"><span data-stu-id="3b96c-150">You can get, change, or remove policy definitions by using hello **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="3b96c-151">Аналогичным образом, можно получить, изменить или удалить назначения политики с помощью hello **показ назначения политики**, **набора назначения политики**, и **удалить назначение политики** команд .</span><span class="sxs-lookup"><span data-stu-id="3b96c-151">Similarly, you can get, change, or remove policy assignments by using hello **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="3b96c-152">Экспорт группы ресурсов в виде шаблона</span><span class="sxs-lookup"><span data-stu-id="3b96c-152">Export a resource group as a template</span></span>
<span data-ttu-id="3b96c-153">Для существующей группы ресурсов можно просмотреть hello шаблона диспетчера ресурсов для группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="3b96c-153">For an existing resource group, you can view hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="3b96c-154">Экспорт шаблона hello имеет два преимущества:</span><span class="sxs-lookup"><span data-stu-id="3b96c-154">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="3b96c-155">Можно легко автоматизировать будущих развертываний hello решения, поскольку всю инфраструктуру hello определен в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="3b96c-155">You can easily automate future deployments of hello solution because all hello infrastructure is defined in hello template.</span></span>
2. <span data-ttu-id="3b96c-156">Ознакомьтесь с синтаксисом шаблона, просмотрев hello JSON, представляющее решения.</span><span class="sxs-lookup"><span data-stu-id="3b96c-156">You can become familiar with template syntax by looking at hello JSON that represents your solution.</span></span>

<span data-ttu-id="3b96c-157">С помощью hello Azure CLI, можно либо экспортировать шаблон, который представляет текущее состояние группы ресурсов hello, или загрузите hello шаблона, который был использован для конкретного развертывания.</span><span class="sxs-lookup"><span data-stu-id="3b96c-157">Using hello Azure CLI, you can either export a template that represents hello current state of your resource group, or download hello template that was used for a particular deployment.</span></span>

* <span data-ttu-id="3b96c-158">**Экспорт шаблона hello для группы ресурсов** -это полезно, если были внесены изменения группы ресурсов tooa и требуется tooretrieve hello JSON-представление текущего состояния.</span><span class="sxs-lookup"><span data-stu-id="3b96c-158">**Export hello template for a resource group** - This is helpful when you made changes tooa resource group, and need tooretrieve hello JSON representation of its current state.</span></span> <span data-ttu-id="3b96c-159">Тем не менее созданный шаблон hello содержит минимальным числом параметров и переменных.</span><span class="sxs-lookup"><span data-stu-id="3b96c-159">However, hello generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="3b96c-160">Большинство значений hello в шаблоне hello жестко запрограммированы.</span><span class="sxs-lookup"><span data-stu-id="3b96c-160">Most of hello values in hello template are hard-coded.</span></span> <span data-ttu-id="3b96c-161">Перед развертыванием hello созданный шаблон, вы можете tooconvert несколько значений hello в параметры для настройки развертывания hello для различных сред.</span><span class="sxs-lookup"><span data-stu-id="3b96c-161">Before deploying hello generated template, you may wish tooconvert more of hello values into parameters so you can customize hello deployment for different environments.</span></span>
  
    <span data-ttu-id="3b96c-162">шаблон hello tooexport для ресурсов группы tooa локального каталога, запустите hello `azure group export` команды, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="3b96c-162">tooexport hello template for a resource group tooa local directory, run hello `azure group export` command as shown in hello following example.</span></span> <span data-ttu-id="3b96c-163">(Замените указанный в примере локальный каталог каталогом, используемым в вашей операционной системе.)</span><span class="sxs-lookup"><span data-stu-id="3b96c-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="3b96c-164">**Загрузите шаблон hello для конкретного развертывания** — это может оказаться полезным, когда требуется фактическое шаблон hello tooview, который используется toodeploy ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3b96c-164">**Download hello template for a particular deployment** -- This is helpful when you need tooview hello actual template that was used toodeploy resources.</span></span> <span data-ttu-id="3b96c-165">шаблон Hello включает все параметры и переменные, определенные для hello исходного развертывания.</span><span class="sxs-lookup"><span data-stu-id="3b96c-165">hello template includes all parameters and variables defined for hello original deployment.</span></span> <span data-ttu-id="3b96c-166">Тем не менее если кто-то в вашей организации группы ресурсов toohello изменений за пределами определения hello в шаблоне hello, этот шаблон не представляют Привет текущее состояние группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="3b96c-166">However, if someone in your organization made changes toohello resource group outside of hello definition in hello template, this template doesn't represent hello current state of hello resource group.</span></span>
  
    <span data-ttu-id="3b96c-167">шаблон toodownload hello, используемый для конкретного развертывания tooa локального каталога, запустите hello `azure group deployment template download` команды.</span><span class="sxs-lookup"><span data-stu-id="3b96c-167">toodownload hello template used for a particular deployment tooa local directory, run hello `azure group deployment template download` command.</span></span> <span data-ttu-id="3b96c-168">Например:</span><span class="sxs-lookup"><span data-stu-id="3b96c-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="3b96c-169">Так как функция экспорта шаблона пока доступна в предварительной версии, поддерживаются не все типы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3b96c-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="3b96c-170">При попытке tooexport шаблона, может появиться ошибка о том, что некоторые ресурсы не были экспортированы.</span><span class="sxs-lookup"><span data-stu-id="3b96c-170">When attempting tooexport a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="3b96c-171">При необходимости эти ресурсы можно определить вручную после скачивания шаблона.</span><span class="sxs-lookup"><span data-stu-id="3b96c-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3b96c-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3b96c-172">Next steps</span></span>
* <span data-ttu-id="3b96c-173">tooget сведения об операции развертывания и устранение ошибок при развертывании с hello Azure CLI см. в разделе [просмотреть операции развертывания](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="3b96c-173">tooget details of deployment operations and troubleshoot deployment errors with hello Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="3b96c-174">Tooset CLI hello toouse приложения или сценария tooaccess ресурсы см [toocreate использования Azure CLI участника службы ресурсы tooaccess](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3b96c-174">If you want toouse hello CLI tooset up an application or script tooaccess resources, see [Use Azure CLI toocreate a service principal tooaccess resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="3b96c-175">Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="3b96c-175">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

