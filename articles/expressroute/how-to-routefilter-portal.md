---
title: "Настройка фильтров маршрутов для пиринга Azure ExpressRoute Майкрософт | Документация Майкрософт"
description: "В этой статье описывается, как фильтры маршрутов tooconfigure по использованию Microsoft Пиринга hello портал Azure"
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
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 2a47d465ec5f175d9510cef94606f70f036f0862
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
  - [Создайте канал ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) и иметь цепи hello, предоставляемой поставщиком соединения, прежде чем продолжить. Hello канал ExpressRoute должны находиться в состоянии подготовлена и включен.
  - [Создайте пиринг Майкрософт](expressroute-howto-routing-portal-resource-manager.md) при управлении hello непосредственно в сеансе BGP. или если у вашего поставщика услуг подключения подготовлен пиринг Майкрософт для вашего канала.

-  Необходимо создать и настроить фильтр маршрутов.
    - Определите hello сервисы tooconsume через пиринг Майкрософт
    - Определить hello список значений BGP сообщества, связанные со службами hello
    - Создать правило tooallow hello префикс список сопоставления hello значения BGP сообщества

-  Необходимо добавить канал ExpressRoute toohello фильтра маршрута hello.

## <a name="before-you-begin"></a>Перед началом работы

Перед началом настройки убедитесь, что соблюдены следующие условия hello:

 - Просмотрите hello [необходимые компоненты](expressroute-prerequisites.md) и [рабочих процессов](expressroute-workflows.md) перед началом настройки.

 - Вам потребуется активный канал ExpressRoute. Следуйте инструкциям hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) и иметь цепи hello, предоставляемой поставщиком соединения, прежде чем продолжить. Hello канал ExpressRoute должны находиться в состоянии подготовлена и включен.

 - Необходимо иметь активный пиринг Майкрософт. Следуйте инструкциям в статье [Создание и изменение канала ExpressRoute с помощью PowerShell](expressroute-howto-routing-portal-resource-manager.md).


## <a name="prefixes"></a>Шаг 1. Получение списка префиксов и значений сообщества BGP

### <a name="1-get-a-list-of-bgp-community-values"></a>1. Получение списка значений сообщества BGP

Значения BGP сообщества, связанные со службами, доступными через пиринг Майкрософт доступна в hello [требования к маршрутизации ExpressRoute](expressroute-routing.md) страницы.

### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a>2. Создайте список значений hello, которые должны toouse

Составьте список нужные значения сообщества BGP toouse в фильтре hello маршрута. Например значение сообщества BGP для службы Dynamics 365 hello — 12076:5040.

## <a name="filter"></a>Шаг 2. Создание фильтра маршрута и правила фильтрации

Фильтр может иметь только одно правило и hello правило должно иметь тип «Разрешить». С этим правилом может быть связан список значений сообщества BGP.

### <a name="1-create-a-route-filter"></a>1. Создание фильтра маршрута
Можно создать фильтр, выбрав параметр toocreate hello новый ресурс. Нажмите кнопку **New** > **сети** > **RouteFilter**, как показано в hello после изображения:

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

Фильтр маршрутов hello необходимо разместить в группе ресурсов. 

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a>2. Создание правила фильтрации

Можно добавить и на вкладке правила фильтра маршрута управление правила обновления, выбрав hello.

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


Вы можете выбрать hello службы будут tooconnect toofrom hello раскрывающегося списка и сохранить правило hello после завершения.

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <a name="attach"></a>Шаг 3. Присоединение канал ExpressRoute tooan фильтра маршрута hello

Можно присоединить hello маршрута фильтра tooa цепи, нужно нажать кнопку «Добавить канал» hello и выбрав канал ExpressRoute hello hello раскрывающегося списка.

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <a name="getproperties"></a>свойства hello tooget фильтра маршрута

При открытии ресурса hello hello портала можно просмотреть свойства фильтра маршрута.

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <a name="updateproperties"></a>свойства hello tooupdate фильтра маршрута

Нажав кнопку "hello «управление правило»" можно обновить список hello BGP сообщества значения вложенного tooa канала.


![Создание фильтра маршрута](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <a name="detach"></a>toodetach фильтр маршрутов из канала ExpressRoute

toodetach канала из фильтра маршрута hello, щелкните правой кнопкой мыши в цепи hello и выберите команду «Отменить связь».

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <a name="delete"></a>toodelete фильтр маршрутов

Фильтр можно удалить, нажав кнопку "Удалить" hello. 

![Создание фильтра маршрута](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения об ExpressRoute см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).
