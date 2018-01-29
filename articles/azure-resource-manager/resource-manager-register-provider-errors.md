---
title: "Ошибки регистрации поставщика ресурсов Azure | Документация Майкрософт"
description: "В этой статье объясняется, как устранять ошибки регистрации поставщика ресурсов Azure."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: support-article
ms.date: 09/13/2017
ms.author: tomfitz
ms.openlocfilehash: d6a99917e732a3439a31cafa5608348694014054
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="resolve-errors-for-resource-provider-registration"></a>Устранение ошибок регистрации поставщика ресурсов

В этой статье описываются ошибки, которые могут возникнуть при использовании поставщика ресурсов, который вы ранее не использовали в своей подписке.

## <a name="symptom"></a>Симптом

При развертывании ресурсов вы можете получить следующий код ошибки и сообщение об ошибке:

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

Или может появиться похожее сообщение.

```
Code: MissingSubscriptionRegistration
Message: The subscription is not registered to use namespace {resource-provider-namespace}
```

## <a name="cause"></a>Причина:

Эти ошибки возникают по одной из следующих причин:

1. Для подписки не зарегистрирован поставщик ресурсов.
1. Версия API не поддерживается для выбранного типа ресурса.
1. Расположение не поддерживается для выбранного типа ресурса.

## <a name="solution"></a>Решение

В сообщении об ошибке должны быть указаны поддерживаемые расположения и версии API. Вы можете изменить шаблон, используя одно из предложенных значений. Большинство поставщиков, но не все, регистрируются автоматически порталом Azure или интерфейсом командной строки, который вы используете. Если ранее вы не использовали конкретный поставщик ресурсов, возможно, потребуется зарегистрировать такой поставщик. Дополнительные сведения о поставщиках ресурсов можно получить с помощью PowerShell или интерфейса командной строки Azure.

### <a name="solution-1"></a>Решение 1

Чтобы просмотреть состояние регистрации, используйте командлет PowerShell **Get-AzureRmResourceProvider**.

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

Чтобы зарегистрировать поставщик, используйте командлет **Register-AzureRmResourceProvider** и укажите имя поставщика ресурсов, который необходимо зарегистрировать.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

Чтобы получить поддерживаемые расположения для определенного типа ресурсов, используйте следующую команду:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

Чтобы получить поддерживаемые версии API для определенного типа ресурсов, используйте следующую команду:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

### <a name="solution-2"></a>Решение 2

**Интерфейс командной строки Azure**

Чтобы узнать, зарегистрирован ли поставщик, используйте команду `az provider list` .

```azurecli-interactive
az provider list
```

Чтобы зарегистрировать поставщик ресурсов, используйте команду `az provider register` и укажите *пространство имен* , которое следует зарегистрировать.

```azurecli-interactive
az provider register --namespace Microsoft.Cdn
```

Чтобы просмотреть поддерживаемые расположения и версии API для типа ресурса, используйте следующую команду.

```azurecli-interactive
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

### <a name="solution-3"></a>Решение 3

Просмотреть состояние регистрации и зарегистрировать пространство имен поставщика ресурсов можно на портале.

1. Для своей подписки выберите **Поставщики ресурсов**.

   ![Выбор поставщиков ресурсов](./media/resource-manager-register-provider-errors/select-resource-provider.png)

1. Просмотрите список поставщиков ресурсов и, при необходимости, щелкните ссылку **Зарегистрировать**, чтобы зарегистрировать поставщик ресурсов типа, который вы пытаетесь развернуть.

   ![список поставщиков ресурсов](./media/resource-manager-register-provider-errors/list-resource-providers.png)
