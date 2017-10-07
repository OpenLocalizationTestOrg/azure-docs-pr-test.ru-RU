---
title: "aaaTag Azure ресурсы для логической организации | Документы Microsoft"
description: "Показано, как tooapply теги tooorganize Azure ресурсы для выставления счетов и управления ими."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 003a78e5-2ff8-4685-93b4-e94d6fb8ed5b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: AzurePortal
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tomfitz
ms.openlocfilehash: e07470463d160f8cefe5c80bc91e66a96af6ca45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-tags-tooorganize-your-azure-resources"></a><span data-ttu-id="3222a-103">Использовать теги tooorganize ресурсы Azure</span><span class="sxs-lookup"><span data-stu-id="3222a-103">Use tags tooorganize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="3222a-104">Можно применить только tooresources тегов, который поддерживает операции диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="3222a-104">You can apply tags only tooresources that support Azure Resource Manager operations.</span></span> <span data-ttu-id="3222a-105">При создании виртуальной машины, виртуальную сеть или учетной записи хранилища через hello классической модели развертывания (например, с помощью Здравствуйте, классический портал Azure), не удается применить toothat тега ресурса.</span><span class="sxs-lookup"><span data-stu-id="3222a-105">If you created a virtual machine, virtual network, or storage account through hello classic deployment model (such as through hello Azure classic portal), you cannot apply a tag toothat resource.</span></span> <span data-ttu-id="3222a-106">Добавление тегов, toosupport повторно развернуть эти ресурсы с помощью диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3222a-106">toosupport tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="3222a-107">Все остальные ресурсы поддерживают теги.</span><span class="sxs-lookup"><span data-stu-id="3222a-107">All other resources support tagging.</span></span>
> 
> 

## <a name="policies-for-tag-consistency"></a><span data-ttu-id="3222a-108">Политики для обеспечения согласованности тегов</span><span class="sxs-lookup"><span data-stu-id="3222a-108">Policies for tag consistency</span></span>

<span data-ttu-id="3222a-109">Можно использовать стандартные правила ресурсов политики toocreate для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="3222a-109">You can use resource policies toocreate standard rules for your organization.</span></span> <span data-ttu-id="3222a-110">Могут создавать политики, убедитесь, что ресурсы, помеченные с соответствующими значениями hello.</span><span class="sxs-lookup"><span data-stu-id="3222a-110">You can create policies that ensure resources are tagged with hello appropriate values.</span></span> <span data-ttu-id="3222a-111">Дополнительные сведения см. в разделе [Применение политик ресурсов для тегов](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="3222a-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="3222a-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3222a-112">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a><span data-ttu-id="3222a-113">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="3222a-113">Azure CLI</span></span>

<span data-ttu-id="3222a-114">существующие теги для hello toosee *группы ресурсов*, используйте:</span><span class="sxs-lookup"><span data-stu-id="3222a-114">toosee hello existing tags for a *resource group*, use:</span></span>

```azurecli
az group show -n examplegroup --query tags
```

<span data-ttu-id="3222a-115">Этот скрипт возвращает hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="3222a-115">That script returns hello following format:</span></span>

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

<span data-ttu-id="3222a-116">существующие теги для hello toosee *ресурс, который имеет идентификатор указанного ресурса*, использовать:</span><span class="sxs-lookup"><span data-stu-id="3222a-116">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```azurecli
az resource show --id {resource-id} --query tags
```

<span data-ttu-id="3222a-117">Или toosee hello существующие теги для *ресурс, который имеет имя, тип и ресурсов указанной группы*, используйте:</span><span class="sxs-lookup"><span data-stu-id="3222a-117">Or, toosee hello existing tags for a *resource that has a specified name, type, and resource group*, use:</span></span>

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

<span data-ttu-id="3222a-118">использовать tooget групп ресурсов, которые имеют определенный тег `az group list`:</span><span class="sxs-lookup"><span data-stu-id="3222a-118">tooget resource groups that have a specific tag, use `az group list`:</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="3222a-119">использовать все ресурсы hello с определенным тегом, и значение, tooget `az resource list`:</span><span class="sxs-lookup"><span data-stu-id="3222a-119">tooget all hello resources that have a particular tag and value, use `az resource list`:</span></span>

```azurecli
az resource list --tag Dept=Finance
```

<span data-ttu-id="3222a-120">Каждый раз при применении теги tooa ресурс или группу ресурсов, вы перезаписать существующие теги hello на этот ресурс или группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3222a-120">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="3222a-121">Таким образом необходимо использовать другой подход, в зависимости от того, имеет ли hello ресурс или группа ресурсов существующие теги.</span><span class="sxs-lookup"><span data-stu-id="3222a-121">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="3222a-122">tooadd теги tooa *группы ресурсов без существующие теги*, используйте:</span><span class="sxs-lookup"><span data-stu-id="3222a-122">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="3222a-123">tooadd теги tooa *ресурс без существующие теги*, используйте:</span><span class="sxs-lookup"><span data-stu-id="3222a-123">tooadd tags tooa *resource without existing tags*, use:</span></span>

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

<span data-ttu-id="3222a-124">tooadd теги tooa ресурс, который уже имеет теги, получить существующие теги hello, переформатировать это значение и заново hello существующих и новых тегов:</span><span class="sxs-lookup"><span data-stu-id="3222a-124">tooadd tags tooa resource that already has tags, retrieve hello existing tags, reformat that value, and reapply hello existing and new tags:</span></span> 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

<span data-ttu-id="3222a-125">tooapply все теги из ресурсов tooits группы ресурсов, и *не сохранять существующие теги ресурсов hello*, используйте следующий сценарий hello:</span><span class="sxs-lookup"><span data-stu-id="3222a-125">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    az resource tag --tags $t --id $resid
  done 
done
```

<span data-ttu-id="3222a-126">tooapply все теги из ресурсов tooits группы ресурсов, и *сохранить существующие теги ресурсов*, используйте следующий сценарий hello:</span><span class="sxs-lookup"><span data-stu-id="3222a-126">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources*, use hello following script:</span></span>

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    jsonrtag=$(az resource show --id $resid --query tags)
    rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
    az resource tag --tags $t$rt --id $resid
  done 
done
```


## <a name="templates"></a><span data-ttu-id="3222a-127">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="3222a-127">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="3222a-128">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3222a-128">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a><span data-ttu-id="3222a-129">Интерфейс REST API</span><span class="sxs-lookup"><span data-stu-id="3222a-129">REST API</span></span>
<span data-ttu-id="3222a-130">Hello портал Azure, так и с помощью PowerShell используйте hello [REST API диспетчера ресурсов](https://docs.microsoft.com/rest/api/resources/) фоновом hello.</span><span class="sxs-lookup"><span data-stu-id="3222a-130">hello Azure portal and PowerShell both use hello [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind hello scenes.</span></span> <span data-ttu-id="3222a-131">При необходимости toointegrate, добавление тегов в другой среде тегов можно получить с помощью **получить** на hello ресурсов идентификатор и обновление hello набор тегов с помощью **PATCH** вызова.</span><span class="sxs-lookup"><span data-stu-id="3222a-131">If you need toointegrate tagging into another environment, you can get tags by using **GET** on hello resource ID and update hello set of tags by using a **PATCH** call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="3222a-132">Теги и выставление счетов</span><span class="sxs-lookup"><span data-stu-id="3222a-132">Tags and billing</span></span>
<span data-ttu-id="3222a-133">Можно использовать теги toogroup данные выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="3222a-133">You can use tags toogroup your billing data.</span></span> <span data-ttu-id="3222a-134">Например если вы используете несколько виртуальных машин в разных организациях, использования hello теги toogroup центра затрат.</span><span class="sxs-lookup"><span data-stu-id="3222a-134">For example, if you are running multiple VMs for different organizations, use hello tags toogroup usage by cost center.</span></span> <span data-ttu-id="3222a-135">Также можно использовать теги toocategorize затраты средой выполнения, например hello тарификации использования для виртуальных машин, работающих в рабочей среде hello.</span><span class="sxs-lookup"><span data-stu-id="3222a-135">You can also use tags toocategorize costs by runtime environment, such as hello billing usage for VMs running in hello production environment.</span></span>


<span data-ttu-id="3222a-136">Можно получить сведения о тегах через hello [использование ресурсов Azure и API-интерфейсы RateCard](../billing/billing-usage-rate-card-overview.md) или файл значений с разделителями запятыми (CSV) использования hello.</span><span class="sxs-lookup"><span data-stu-id="3222a-136">You can retrieve information about tags through hello [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or hello usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="3222a-137">Загрузить файл использования hello hello [портал учетных записей Azure](https://account.windowsazure.com/) или [портала EA](https://ea.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3222a-137">You download hello usage file from hello [Azure account portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="3222a-138">Дополнительные сведения о toobilling программный доступ. в разделе [анализировать потребления ресурсов Microsoft Azure](../billing/billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3222a-138">For more information about programmatic access toobilling information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="3222a-139">Подробнее об операциях REST API см. в [справочнике по REST API для выставления счетов Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span><span class="sxs-lookup"><span data-stu-id="3222a-139">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="3222a-140">При загрузке hello использования CSV для служб, поддерживающих теги с выставления счетов hello теги отображаются в hello **теги** столбца.</span><span class="sxs-lookup"><span data-stu-id="3222a-140">When you download hello usage CSV for services that support tags with billing, hello tags appear in hello **Tags** column.</span></span> <span data-ttu-id="3222a-141">Дополнительные сведения см. в статье [Расшифровка счета за использование Microsoft Azure](../billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="3222a-141">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![См. сведения об использовании тегов при выставлении счетов.](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="3222a-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3222a-143">Next steps</span></span>
* <span data-ttu-id="3222a-144">В подписку можно добавить ограничения и соглашения, используя настраиваемые политики.</span><span class="sxs-lookup"><span data-stu-id="3222a-144">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="3222a-145">Некоторые политики могут требовать, чтобы для всех ресурсов было задано значение определенного тега.</span><span class="sxs-lookup"><span data-stu-id="3222a-145">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="3222a-146">Дополнительные сведения см. в разделе [использовать ресурсы toomanage политик и управления доступом](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="3222a-146">For more information, see [Use policies toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="3222a-147">Введение toousing Azure PowerShell при развертывании ресурсов в разделе [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="3222a-147">For an introduction toousing Azure PowerShell when you're deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="3222a-148">Введение toousing hello Azure CLI при развертывании ресурсов в разделе [использование hello Azure CLI для Mac, Linux и Windows с помощью диспетчера ресурсов Azure](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="3222a-148">For an introduction toousing hello Azure CLI when you're deploying resources, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="3222a-149">На портале hello toousing введение в разделе [использование hello Azure портала toomanage ресурсам Azure](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3222a-149">For an introduction toousing hello portal, see [Using hello Azure portal toomanage your Azure resources](resource-group-portal.md).</span></span>  
* <span data-ttu-id="3222a-150">Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="3222a-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

