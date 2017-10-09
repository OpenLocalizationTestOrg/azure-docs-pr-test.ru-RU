---
title: "Настройка фильтров маршрутов для пиринга Azure ExpressRoute Microsoft с помощью PowerShell | Документация Майкрософт"
description: "В этой статье описывается, как фильтры tooconfigure маршрута для Пиринга Майкрософт с помощью PowerShell"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 395bcf7d6ad43c643ff041b154f8e4b797083e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a>Настройка фильтров маршрутов для пиринга Майкрософт

Фильтры маршрутов являются способом tooconsume подмножество поддерживаемых услуг через пиринг Майкрософт. Hello шаги, приведенные в этой статье справки можно настраивать и управлять фильтры маршрутов для каналов ExpressRoute.

Службы Dynamics 365 и службам Office 365, такие как Exchange Online, SharePoint Online и Скайп для бизнеса, доступны через пиринг Майкрософт hello. При настройке пиринг Майкрософт в канал ExpressRoute, через сеансов BGP hello, установленных объявления все префиксы toothese связанных служб. Значение сообщества BGP является hello вложенного tooevery префикс tooidentify службы, предлагаемые hello префикс. Список значений сообщества BGP hello и hello служб, они сопоставляются. в разделе [BGP сообщества](expressroute-routing.md#bgp).

Если необходимо использовать службы связи tooall, большое число префиксов разглашаемые BGP. Это значительно увеличивает размер hello таблиц маршрутов hello обслуживается маршрутизаторов в сети. Если планируется tooconsume только подмножество служб, предлагаемым через пиринг Майкрософт, можно уменьшить размер hello таблиц маршрутизации двумя способами. Вы можете:

- Отфильтровывать нежелательные префиксы путем применения фильтров маршрутов к сообществам BGP. Это стандартная сетевая практика и обычно используется во многих сетях.

- Определение фильтров маршрута и применить их tooyour канал ExpressRoute. Фильтр — новый ресурс, что позволяет выбрать hello список служб, которые планирование tooconsume через пиринг Майкрософт. ExpressRoute они передают лишь hello список префиксов, которые принадлежат toohello службы, определенные в фильтре hello маршрута.

### <a name="about"></a>О фильтрах маршрута

Когда пиринг Майкрософт настроена на ваш канал ExpressRoute, периметрическими маршрутизаторами Microsoft hello установить паре сеансов BGP с маршрутизаторами edge hello (вашим или поставщика услуг подключения). Маршруты, объявленные tooyour сети. tooenable объявления tooyour маршруте, необходимо связать фильтр маршрутов.

Фильтр позволяет выявить службы будут tooconsume через пиринг Майкрософт канал ExpressRoute. Это по сути белый список значений всех hello BGP сообщества. После определен и присоединенного tooan канал ExpressRoute ресурса фильтров маршрута, все префиксы, сопоставленные toohello BGP сообщества значения являются объявленной tooyour сети.

фильтры маршрутов может tooattach toobe со службами Office 365 на них, необходимо иметь авторизации служб Office 365 tooconsume через ExpressRoute. При отсутствии службы авторизованным tooconsume Office 365 с помощью ExpressRoute, фильтры маршрутов tooattach hello операция завершается ошибкой. Дополнительные сведения о процессе авторизации hello см. в разделе [ExpressRoute Azure для Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd). Службы 365 tooDynamics связи не требуется никакой предыдущих авторизации.

> [!IMPORTANT]
> Microsoft пиринг ExpressRoute каналов, которые были настроены предыдущих tooAugust 1, 2017 г. будет иметь все службы префиксов, объявленных через пиринг Майкрософт, даже если не определены фильтры маршрутов. Пиринг каналы ExpressRoute, настроенных в течение или после 1 августа 2017 г. Корпорация Майкрософт не будет иметь префиксы объявленных пока фильтр не будет подключено toohello канала.
> 
> 

### <a name="workflow"></a>Рабочий процесс

возможности toosuccessfully toobe подключение tooservices через пиринг Майкрософт, необходимо выполнить следующие действия по настройке hello:

- Необходимо иметь активный канал ExpressRoute с подготовленным пирингом Майкрософт. Эти задачи можно использовать следующие инструкции tooaccomplish hello:
  - [Создайте канал ExpressRoute](expressroute-howto-circuit-arm.md) и иметь цепи hello, предоставляемой поставщиком соединения, прежде чем продолжить. Hello канал ExpressRoute должны находиться в состоянии подготовлена и включен.
  - [Создайте пиринг Майкрософт](expressroute-circuit-peerings.md) при управлении hello непосредственно в сеансе BGP. или если у вашего поставщика услуг подключения подготовлен пиринг Майкрософт для вашего канала.

-  Необходимо создать и настроить фильтр маршрутов.
    - Определите hello сервисы tooconsume через пиринг Майкрософт
    - Определить hello список значений BGP сообщества, связанные со службами hello
    - Создать правило tooallow hello префикс список сопоставления hello значения BGP сообщества

-  Необходимо добавить канал ExpressRoute toohello фильтра маршрута hello.

## <a name="before-you-begin"></a>Перед началом работы

Перед началом настройки убедитесь, что соблюдены следующие условия hello:

 - Установите последнюю версию hello hello командлеты PowerShell диспетчера ресурсов Azure. Дополнительные сведения см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/install-azurerm-ps).

  > [!NOTE]
  > Загрузка последней версии hello из коллекции PowerShell hello, а не с помощью установщика hello. Hello установщика в настоящее время не поддерживает командлеты необходимые hello.
  > 

 - Просмотрите hello [необходимые компоненты](expressroute-prerequisites.md) и [рабочих процессов](expressroute-workflows.md) перед началом настройки.

 - Вам потребуется активный канал ExpressRoute. Следуйте инструкциям hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-arm.md) и иметь цепи hello, предоставляемой поставщиком соединения, прежде чем продолжить. Hello канал ExpressRoute должны находиться в состоянии подготовлена и включен.

 - Необходимо иметь активный пиринг Майкрософт. Следуйте инструкциям в статье [Создание и изменение канала ExpressRoute с помощью PowerShell](expressroute-circuit-peerings.md).

### <a name="log-in-tooyour-azure-account"></a>Войдите в tooyour учетная запись Azure

Перед началом этой конфигурации, необходимо войти в tooyour учетная запись Azure. Hello командлет запросит hello учетные данные входа для учетной записи Azure. После входа в систему, он загружает параметры учетной записи, таким образом, они будут доступны tooAzure PowerShell.

Откройте консоль PowerShell с повышенными привилегиями и подключите tooyour учетную запись. Используйте следующий пример toohelp подключении hello.

```powershell
Login-AzureRmAccount
```

Если у вас несколько подписок Azure, проверьте hello подписки для учетной записи hello.

```powershell
Get-AzureRmSubscription
```

Укажите требуемый toouse подписки hello.

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <a name="prefixes"></a>Шаг 1. Получение списка префиксов и значений сообщества BGP

### <a name="1-get-a-list-of-bgp-community-values"></a>1. Получение списка значений сообщества BGP

Используйте следующий командлет tooget hello список значений BGP сообщества, связанные со службами, доступными через пиринг Майкрософт hello и hello список префиксов, связанные с ними:

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a>2. Создайте список значений hello, которые должны toouse

Составьте список нужные значения сообщества BGP toouse в фильтре hello маршрута. Например значение сообщества BGP для службы Dynamics 365 hello — 12076:5040.

## <a name="filter"></a>Шаг 2. Создание фильтра маршрута и правила фильтрации

Фильтр может иметь только одно правило и hello правило должно иметь тип «Разрешить». С этим правилом может быть связан список значений сообщества BGP.

### <a name="1-create-a-route-filter"></a>1. Создание фильтра маршрута

Сначала создайте фильтр маршрутов hello. Команда Hello «New-AzureRmRouteFilter» только создает ресурс фильтра маршрута. После создания ресурса hello, необходимо создать правило и присоединить его объект filter toohello маршрута. Запустите следующие команды toocreate hello ресурс фильтра маршрута:

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a>2. Создание правила фильтрации

Можно указать набор сообщества BGP как список с разделителями запятыми, как показано в примере hello. Выполните следующие команды toocreate hello новое правило.
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-hello-rule-toohello-route-filter"></a>3. Добавить фильтр маршрутов toohello правило hello

Следующая команда tooadd hello правило toohello маршрута фильтр выполнения hello:
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <a name="attach"></a>Шаг 3. Присоединение канал ExpressRoute tooan фильтра маршрута hello

Выполните следующие команды tooattach hello маршрута фильтра toohello канал ExpressRoute, при условии, что у вас есть только пиринг Майкрософт hello.

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="getproperties"></a>свойства hello tooget фильтра маршрута

свойства hello tooget фильтр маршрутов hello используйте следующие шаги:

1. Следующая команда tooget hello маршрута фильтр ресурсов выполнения hello:

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. Получите правила фильтрации hello маршрута для ресурса hello фильтра маршрутов, выполнив следующую команду hello:

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <a name="updateproperties"></a>свойства hello tooupdate фильтра маршрута

Если фильтр маршрутов hello уже присоединен tooa цепи, список сообщества BGP toohello обновления автоматически распространяет изменения объявления соответствующий префикс при помощи сеансов BGP hello установлено. Можно обновить список сообщества BGP hello фильтра маршрута с помощью hello следующую команду:

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <a name="detach"></a>toodetach фильтр маршрутов из канала ExpressRoute

Как только фильтр отсоединяется от hello канал ExpressRoute, отсутствуют префиксы объявления через сеанс BGP hello. Можно отсоединить фильтр маршрутов из канала ExpressRoute с помощью hello следующую команду:
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="delete"></a>toodelete фильтр маршрутов

Можно только удалить фильтр маршрута, если он не присоединен tooany канала. Убедитесь, этот фильтр маршрута hello не присоединен tooany схемы перед выполнением toodelete его. Можно удалить фильтр с помощью hello следующую команду:

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения об ExpressRoute см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).
