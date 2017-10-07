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
# <a name="use-tags-tooorganize-your-azure-resources"></a>Использовать теги tooorganize ресурсы Azure
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> Можно применить только tooresources тегов, который поддерживает операции диспетчера ресурсов Azure. При создании виртуальной машины, виртуальную сеть или учетной записи хранилища через hello классической модели развертывания (например, с помощью Здравствуйте, классический портал Azure), не удается применить toothat тега ресурса. Добавление тегов, toosupport повторно развернуть эти ресурсы с помощью диспетчера ресурсов. Все остальные ресурсы поддерживают теги.
> 
> 

## <a name="policies-for-tag-consistency"></a>Политики для обеспечения согласованности тегов

Можно использовать стандартные правила ресурсов политики toocreate для вашей организации. Могут создавать политики, убедитесь, что ресурсы, помеченные с соответствующими значениями hello. Дополнительные сведения см. в разделе [Применение политик ресурсов для тегов](resource-manager-policy-tags.md).

## <a name="powershell"></a>PowerShell
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a>Инфраструктура CLI Azure

существующие теги для hello toosee *группы ресурсов*, используйте:

```azurecli
az group show -n examplegroup --query tags
```

Этот скрипт возвращает hello следующий формат:

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

существующие теги для hello toosee *ресурс, который имеет идентификатор указанного ресурса*, использовать:

```azurecli
az resource show --id {resource-id} --query tags
```

Или toosee hello существующие теги для *ресурс, который имеет имя, тип и ресурсов указанной группы*, используйте:

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

использовать tooget групп ресурсов, которые имеют определенный тег `az group list`:

```azurecli
az group list --tag Dept=IT
```

использовать все ресурсы hello с определенным тегом, и значение, tooget `az resource list`:

```azurecli
az resource list --tag Dept=Finance
```

Каждый раз при применении теги tooa ресурс или группу ресурсов, вы перезаписать существующие теги hello на этот ресурс или группа ресурсов. Таким образом необходимо использовать другой подход, в зависимости от того, имеет ли hello ресурс или группа ресурсов существующие теги. 

tooadd теги tooa *группы ресурсов без существующие теги*, используйте:

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

tooadd теги tooa *ресурс без существующие теги*, используйте:

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

tooadd теги tooa ресурс, который уже имеет теги, получить существующие теги hello, переформатировать это значение и заново hello существующих и новых тегов: 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

tooapply все теги из ресурсов tooits группы ресурсов, и *не сохранять существующие теги ресурсов hello*, используйте следующий сценарий hello:

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

tooapply все теги из ресурсов tooits группы ресурсов, и *сохранить существующие теги ресурсов*, используйте следующий сценарий hello:

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


## <a name="templates"></a>Шаблоны

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a>Microsoft Azure
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a>Интерфейс REST API
Hello портал Azure, так и с помощью PowerShell используйте hello [REST API диспетчера ресурсов](https://docs.microsoft.com/rest/api/resources/) фоновом hello. При необходимости toointegrate, добавление тегов в другой среде тегов можно получить с помощью **получить** на hello ресурсов идентификатор и обновление hello набор тегов с помощью **PATCH** вызова.

## <a name="tags-and-billing"></a>Теги и выставление счетов
Можно использовать теги toogroup данные выставления счетов. Например если вы используете несколько виртуальных машин в разных организациях, использования hello теги toogroup центра затрат. Также можно использовать теги toocategorize затраты средой выполнения, например hello тарификации использования для виртуальных машин, работающих в рабочей среде hello.


Можно получить сведения о тегах через hello [использование ресурсов Azure и API-интерфейсы RateCard](../billing/billing-usage-rate-card-overview.md) или файл значений с разделителями запятыми (CSV) использования hello. Загрузить файл использования hello hello [портал учетных записей Azure](https://account.windowsazure.com/) или [портала EA](https://ea.azure.com). Дополнительные сведения о toobilling программный доступ. в разделе [анализировать потребления ресурсов Microsoft Azure](../billing/billing-usage-rate-card-overview.md). Подробнее об операциях REST API см. в [справочнике по REST API для выставления счетов Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).


При загрузке hello использования CSV для служб, поддерживающих теги с выставления счетов hello теги отображаются в hello **теги** столбца. Дополнительные сведения см. в статье [Расшифровка счета за использование Microsoft Azure](../billing/billing-understand-your-bill.md).

![См. сведения об использовании тегов при выставлении счетов.](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a>Дальнейшие действия
* В подписку можно добавить ограничения и соглашения, используя настраиваемые политики. Некоторые политики могут требовать, чтобы для всех ресурсов было задано значение определенного тега. Дополнительные сведения см. в разделе [использовать ресурсы toomanage политик и управления доступом](resource-manager-policy.md).
* Введение toousing Azure PowerShell при развертывании ресурсов в разделе [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure](powershell-azure-resource-manager.md).
* Введение toousing hello Azure CLI при развертывании ресурсов в разделе [использование hello Azure CLI для Mac, Linux и Windows с помощью диспетчера ресурсов Azure](xplat-cli-azure-resource-manager.md).
* На портале hello toousing введение в разделе [использование hello Azure портала toomanage ресурсам Azure](resource-group-portal.md).  
* Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).

