---
title: "политики aaaAzure ресурсов для соглашения об именовании | Документы Microsoft"
description: "В этой статье описываются политики Azure Resource Manager для соглашений об именовании ресурсов."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a>Применение политик ресурсов для имен и текста
В этом разделе показано несколько [политики ресурсов](resource-manager-policy.md) можно применить tooestablish соглашения об именовании и текста. Эти политики обеспечивают согласованность данных в именах ресурсов и в значениях тегов. 

## <a name="set-naming-convention-with-wildcard"></a>Соглашение об именовании с символами подстановки
Hello следующем примере показано использование подстановочных знаков, которая поддерживается hello hello **как** условие. Hello условие указано, что если hello имя соответствовать шаблону упомянутых hello (namePrefix\*nameSuffix) затем отклонить запрос hello:

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a>Соглашение об именовании с шаблоном

toospecify, что ресурс имена которых соответствуют шаблону, используйте hello соответствуют условию. Hello следующего примера требуется toostart имена с `contoso` и содержать буквы шесть дополнительных:

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a>Настройка шаблона даты для значения тега

toorequire шаблон даты, используйте две цифры, тире, три буквы, тире и четыре цифры:

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a>Дальнейшие действия
* После определения правила политики (как показано в предыдущих примерах hello), требуется определение политики toocreate hello и назначьте его tooa области. Hello область может быть подписки, группы ресурсов или ресурсов. политики tooassign через портал hello см. [tooassign портала используйте Azure и управление политиками ресурсов](resource-manager-policy-portal.md). политики tooassign через API-Интерфейс REST, PowerShell или Azure CLI см. [назначение политики и управлять ими через сценарий](resource-manager-policy-create-assign.md). 
* Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).

