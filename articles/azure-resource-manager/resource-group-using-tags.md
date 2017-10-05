---
title: "Добавление тегов к ресурсам Azure для их логической организации | Документация Майкрософт"
description: "Здесь описано, как применить теги, чтобы организовать ресурсы Azure для выставления счетов и управления."
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
ms.openlocfilehash: 4f52c30614ad39da8a34ff6ecfb707b75400517f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-tags-to-organize-your-azure-resources"></a><span data-ttu-id="5282f-103">Использование тегов для организации ресурсов в Azure</span><span class="sxs-lookup"><span data-stu-id="5282f-103">Use tags to organize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="5282f-104">Теги можно добавлять только к ресурсам, которые поддерживают операции Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5282f-104">You can apply tags only to resources that support Azure Resource Manager operations.</span></span> <span data-ttu-id="5282f-105">Если вы создали виртуальную машину, виртуальную сеть или учетную запись хранения при помощи классической модели развертывания (например, через классический портал Azure), то к таким ресурсам теги нельзя добавлять.</span><span class="sxs-lookup"><span data-stu-id="5282f-105">If you created a virtual machine, virtual network, or storage account through the classic deployment model (such as through the Azure classic portal), you cannot apply a tag to that resource.</span></span> <span data-ttu-id="5282f-106">Для поддержки тегов эти ресурсы необходимо развернуть повторно с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5282f-106">To support tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="5282f-107">Все остальные ресурсы поддерживают теги.</span><span class="sxs-lookup"><span data-stu-id="5282f-107">All other resources support tagging.</span></span>
> 
> 

## <a name="policies-for-tag-consistency"></a><span data-ttu-id="5282f-108">Политики для обеспечения согласованности тегов</span><span class="sxs-lookup"><span data-stu-id="5282f-108">Policies for tag consistency</span></span>

<span data-ttu-id="5282f-109">Политики ресурсов позволяют создавать стандартные правила для организации.</span><span class="sxs-lookup"><span data-stu-id="5282f-109">You can use resource policies to create standard rules for your organization.</span></span> <span data-ttu-id="5282f-110">Можно создать политики, обеспечивающие добавление к ресурсам тегов с соответствующими значениями.</span><span class="sxs-lookup"><span data-stu-id="5282f-110">You can create policies that ensure resources are tagged with the appropriate values.</span></span> <span data-ttu-id="5282f-111">Дополнительные сведения см. в разделе [Применение политик ресурсов для тегов](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="5282f-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="5282f-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5282f-112">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a><span data-ttu-id="5282f-113">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="5282f-113">Azure CLI</span></span>

<span data-ttu-id="5282f-114">Чтобы просмотреть существующие теги для *группы ресурсов*, используйте этот командлет:</span><span class="sxs-lookup"><span data-stu-id="5282f-114">To see the existing tags for a *resource group*, use:</span></span>

```azurecli
az group show -n examplegroup --query tags
```

<span data-ttu-id="5282f-115">Этот скрипт вернет ответ в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="5282f-115">That script returns the following format:</span></span>

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

<span data-ttu-id="5282f-116">Чтобы просмотреть существующие теги для *ресурса с указанным идентификатором ресурса*, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5282f-116">To see the existing tags for a *resource that has a specified resource ID*, use:</span></span>

```azurecli
az resource show --id {resource-id} --query tags
```

<span data-ttu-id="5282f-117">Чтобы просмотреть существующие теги для *ресурса с указанным именем, типом и группой ресурсов*, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5282f-117">Or, to see the existing tags for a *resource that has a specified name, type, and resource group*, use:</span></span>

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

<span data-ttu-id="5282f-118">Чтобы получить группы ресурсов с определенным тегом, используйте команду `az group list`:</span><span class="sxs-lookup"><span data-stu-id="5282f-118">To get resource groups that have a specific tag, use `az group list`:</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="5282f-119">Чтобы получить все ресурсы с определенным тегом и значением, используйте команду `az resource list`:</span><span class="sxs-lookup"><span data-stu-id="5282f-119">To get all the resources that have a particular tag and value, use `az resource list`:</span></span>

```azurecli
az resource list --tag Dept=Finance
```

<span data-ttu-id="5282f-120">Каждый раз, когда вы добавляете теги к ресурсу или группе ресурсов, вы перезаписываете существующие теги в этом ресурсе или группе.</span><span class="sxs-lookup"><span data-stu-id="5282f-120">Every time you apply tags to a resource or a resource group, you overwrite the existing tags on that resource or resource group.</span></span> <span data-ttu-id="5282f-121">Поэтому необходимо использовать другой подход, исходя из того, имеются ли теги в ресурсе или в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5282f-121">Therefore, you must use a different approach based on whether the resource or resource group has existing tags.</span></span> 

<span data-ttu-id="5282f-122">Чтобы добавить теги в *группу ресурсов без тегов*, используйте этот командлет:</span><span class="sxs-lookup"><span data-stu-id="5282f-122">To add tags to a *resource group without existing tags*, use:</span></span>

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="5282f-123">Чтобы добавить теги в *ресурс без тегов*, используйте этот командлет:</span><span class="sxs-lookup"><span data-stu-id="5282f-123">To add tags to a *resource without existing tags*, use:</span></span>

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

<span data-ttu-id="5282f-124">Чтобы добавить теги в ресурс, который уже содержит теги, извлеките существующие теги, переформатируйте это значение и еще раз добавьте существующие и новые теги:</span><span class="sxs-lookup"><span data-stu-id="5282f-124">To add tags to a resource that already has tags, retrieve the existing tags, reformat that value, and reapply the existing and new tags:</span></span> 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

<span data-ttu-id="5282f-125">Чтобы добавить все теги из группы ресурсов к ресурсам в этой группе, *не сохраняя существующие теги ресурсов*, используйте следующий сценарий.</span><span class="sxs-lookup"><span data-stu-id="5282f-125">To apply all tags from a resource group to its resources, and *not retain existing tags on the resources*, use the following script:</span></span>

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

<span data-ttu-id="5282f-126">Чтобы добавить все теги из группы ресурсов к ресурсам в этой группе и *сохранить существующие теги ресурсов*, используйте следующий сценарий:</span><span class="sxs-lookup"><span data-stu-id="5282f-126">To apply all tags from a resource group to its resources, and *retain existing tags on resources*, use the following script:</span></span>

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


## <a name="templates"></a><span data-ttu-id="5282f-127">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="5282f-127">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="5282f-128">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5282f-128">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a><span data-ttu-id="5282f-129">Интерфейс REST API</span><span class="sxs-lookup"><span data-stu-id="5282f-129">REST API</span></span>
<span data-ttu-id="5282f-130">Портал Azure и PowerShell используют [интерфейс REST API диспетчера ресурсов Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="5282f-130">The Azure portal and PowerShell both use the [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind the scenes.</span></span> <span data-ttu-id="5282f-131">Если вам нужно интегрировать теги в другую среду, их можно получить с помощью метода **GET** по идентификатору ресурса и обновить набор тегов с помощью вызова метода **PATCH**.</span><span class="sxs-lookup"><span data-stu-id="5282f-131">If you need to integrate tagging into another environment, you can get tags by using **GET** on the resource ID and update the set of tags by using a **PATCH** call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="5282f-132">Теги и выставление счетов</span><span class="sxs-lookup"><span data-stu-id="5282f-132">Tags and billing</span></span>
<span data-ttu-id="5282f-133">С помощью тегов можно группировать данные о выставлении счетов.</span><span class="sxs-lookup"><span data-stu-id="5282f-133">You can use tags to group your billing data.</span></span> <span data-ttu-id="5282f-134">Например, если вы используете несколько виртуальных машин для различных организаций, то с помощью тегов можно сгруппировать сведения об использовании по месту возникновения затрат.</span><span class="sxs-lookup"><span data-stu-id="5282f-134">For example, if you are running multiple VMs for different organizations, use the tags to group usage by cost center.</span></span> <span data-ttu-id="5282f-135">Кроме того, теги можно использовать для классификации затрат по среде выполнения (например, сведения о выставленных счетах за виртуальные машины, запущенные в рабочей среде).</span><span class="sxs-lookup"><span data-stu-id="5282f-135">You can also use tags to categorize costs by runtime environment, such as the billing usage for VMs running in the production environment.</span></span>


<span data-ttu-id="5282f-136">Сведения о тегах можно получить с помощью [интерфейсов API использования ресурсов Azure и RateCard](../billing/billing-usage-rate-card-overview.md) или файла сведений об использовании с разделителями-запятыми (CSV-файла).</span><span class="sxs-lookup"><span data-stu-id="5282f-136">You can retrieve information about tags through the [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or the usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="5282f-137">Этот файл можно скачать на [портале учетных записей Azure](https://account.windowsazure.com/) или на [портале Azure Enterprise Portal](https://ea.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5282f-137">You download the usage file from the [Azure account portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="5282f-138">Дополнительные сведения о программном доступе к данным для выставления счетов см. в статье [Получение ценных сведений о потреблении ресурсов Microsoft Azure](../billing/billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5282f-138">For more information about programmatic access to billing information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="5282f-139">Подробнее об операциях REST API см. в [справочнике по REST API для выставления счетов Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span><span class="sxs-lookup"><span data-stu-id="5282f-139">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="5282f-140">В скачанном CSV-файле со сведениями об использовании служб, поддерживающих теги выставления счетов, эти теги отображаются в столбце **Tags**.</span><span class="sxs-lookup"><span data-stu-id="5282f-140">When you download the usage CSV for services that support tags with billing, the tags appear in the **Tags** column.</span></span> <span data-ttu-id="5282f-141">Дополнительные сведения см. в статье [Расшифровка счета за использование Microsoft Azure](../billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="5282f-141">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![См. сведения об использовании тегов при выставлении счетов.](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="5282f-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5282f-143">Next steps</span></span>
* <span data-ttu-id="5282f-144">В подписку можно добавить ограничения и соглашения, используя настраиваемые политики.</span><span class="sxs-lookup"><span data-stu-id="5282f-144">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="5282f-145">Некоторые политики могут требовать, чтобы для всех ресурсов было задано значение определенного тега.</span><span class="sxs-lookup"><span data-stu-id="5282f-145">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="5282f-146">Дополнительные сведения см. в статье [Общие сведения о политике ресурсов](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="5282f-146">For more information, see [Use policies to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="5282f-147">Общие сведения об использовании Azure PowerShell для развертывания ресурсов см. в статье [Управление ресурсами с помощью Azure PowerShell и Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5282f-147">For an introduction to using Azure PowerShell when you're deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="5282f-148">Общие сведения об использовании Azure CLI для развертывания ресурсов см. в статье [Управление ресурсами и группами ресурсов Azure с помощью интерфейса командной строки Azure](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5282f-148">For an introduction to using the Azure CLI when you're deploying resources, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="5282f-149">Общие сведения об использовании портала см. в статье [Управление ресурсами Azure через портал](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5282f-149">For an introduction to using the portal, see [Using the Azure portal to manage your Azure resources](resource-group-portal.md).</span></span>  
* <span data-ttu-id="5282f-150">Инструкции по использованию Resource Manager для эффективного управления подписками в организациях см. в статье [Корпоративный каркас Azure: рекомендуемая система управления подписками](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="5282f-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

