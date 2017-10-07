---
title: "toomanage aaaUsing PowerShell диспетчера трафика в Azure | Документы Microsoft"
description: "Использование PowerShell для диспетчера трафика в Azure Resource Manager"
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a>С помощью PowerShell toomanage диспетчера трафика

Диспетчер ресурсов Azure — интерфейс hello предпочтительный управления для служб в Azure. Профилями диспетчера трафика Azure можно управлять с помощью интерфейсов API и инструментов на основе Azure Resource Manager.

## <a name="resource-model"></a>Модель ресурсов

Для настройки диспетчера трафика используется набор параметров, которые называются профилем. Этот профиль содержит параметры DNS, параметры маршрутизации трафика, параметров мониторинга конечной точки, а перенаправляется список трафик toowhich конечных точек службы.

Каждый профиль диспетчера трафика представлен ресурсом типа TrafficManagerProfiles. В hello уровень REST API hello URI для каждого профиля выглядит следующим образом:

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a>Настройка Azure PowerShell

В данных инструкциях используется Microsoft Azure PowerShell. Hello следующей статье объясняется, как tooinstall и настройка Azure PowerShell.

* [Как tooinstall и настройка Azure PowerShell](/powershell/azure/overview)

Примеры Hello в этой статье предполагается, что существующая группа ресурсов. Можно создать группу ресурсов с помощью hello следующую команду:

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> Для Azure Resource Manager необходимо, чтобы все группы ресурсов имели расположение. Это расположение используется в качестве значения по умолчанию hello для ресурсов, созданных в этой группе ресурсов. Тем не менее поскольку ресурсы профиля диспетчера трафика глобального, не язык, выбор hello расположение группы ресурсов не оказывает влияния на диспетчера трафика Azure.

## <a name="create-a-traffic-manager-profile"></a>Создание профиля диспетчера трафика

использовать профиль диспетчера трафика toocreate hello `New-AzureRmTrafficManagerProfile` командлета:

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

Привет, в следующей таблице описаны параметры hello:

| Параметр | Описание |
| --- | --- |
| Имя |Имя ресурса Hello для hello ресурс профиля диспетчера трафика. Профили hello же группу ресурсов должны иметь уникальные имена. Это имя не зависит от hello DNS-имя DNS-запросы. |
| ResourceGroupName |Имя Hello hello ресурсов группы содержащего hello профиля ресурса. |
| TrafficRoutingMethod |Указывает toodetermine маршрутизации трафика метод, используемый hello, какая конечная точка возвращается в ответе DNS-запрос. Возможные значения: Performance (производительность), Weighted (взвешенный) и Priority (приоритетный). |
| RelativeDnsName |Задает hello часть имени узла DNS-имя hello, предоставляемые этим профилем диспетчера трафика. Это значение объединяется с hello доменное имя DNS диспетчера трафика Azure tooform hello полное доменное имя (FQDN) профиля hello. Например установка значения hello 'Contoso' становится «contoso.trafficmanager.net.» |
| Срок жизни |Указывает hello DNS время жизни (TTL), в секундах. Это TTL информирует hello локальным распознавателям DNS и DNS-клиенты, как долго toocache ответов DNS, для этого профиля диспетчера трафика. |
| MonitorProtocol |Указывает протокол toouse hello toomonitor-исправности конечной точки. Допустимые значения: HTTP и HTTPS. |
| MonitorPort |Указывает, что hello TCP-порт используется toomonitor исправности конечной точки. |
| MonitorPath |Указывает имя домена конечной точки toohello относительный путь hello tooprobe работоспособности конечной точки. |

Hello командлет создает профиль диспетчера трафика в Azure и возвращает соответствующий tooPowerShell объекта профиля. На этом этапе hello профиль не содержит конечные точки. Дополнительные сведения о добавлении профиля диспетчера трафика tooa конечных точек см. в разделе [Добавление конечных точек диспетчера трафика](#adding-traffic-manager-endpoints).

## <a name="get-a-traffic-manager-profile"></a>Получение профиля диспетчера трафика

использовать существующий объект профиля диспетчера трафика, tooretrieve hello `Get-AzureRmTrafficManagerProfle` командлета:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

Этот командлет возвращает профиль объекта трафика.

## <a name="update-a-traffic-manager-profile"></a>Изменение профиля диспетчера трафика

Изменение профилей диспетчера трафика выполняется в три этапа.

1. С помощью профиля hello получить `Get-AzureRmTrafficManagerProfile` или используйте профиль hello, возвращенных `New-AzureRmTrafficManagerProfile`.
2. Изменение профиля hello. Можно добавить и удалить конечные точки или изменить параметры профиля или конечной точки. Эти изменения выполняются в автономном режиме. Изменяются только hello локального объекта в памяти, представляющий профиль hello.
3. Фиксация изменений с помощью hello `Set-AzureRmTrafficManagerProfile` командлета.

За исключением RelativeDnsName hello профиль можно изменить все свойства профиля. toochange hello RelativeDnsName, необходимо удалить профиль и новый профиль с новым именем.

Hello в следующем примере показано, как toochange hello TTL профиля:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Существует три типа конечных точек диспетчера трафика.

1. **Конечные точки Azure** — это службы, размещенные в Azure.
2. **Внешние конечные точки** — службы, размещенные за пределами Azure.
3. **Вложенные конечные точки** представляют собой иерархии используется tooconstruct вложенных профилей диспетчера трафика. Вложенные конечные точки позволяют создавать расширенные конфигурации маршрутизации трафика для сложных приложений.

Конечные точки всех трех типов можно добавлять двумя способами.

1. С помощью описанных выше трех шагов. Преимущество этого метода Hello — несколько конечной точки может выполняться в одно обновление.
2. С помощью командлета New-AzureRmTrafficManagerEndpoint hello. Этот командлет добавляет конечную точку tooan существующего профиля диспетчера трафика в одной операции.

## <a name="adding-azure-endpoints"></a>Добавление конечных точек Azure

Конечные точки Azure ссылаются на службы, размещенные в Azure. Поддерживаются два типа конечных точек Azure.

1. Веб-приложения Azure.
2. Ресурсы Azure PublicIpAddress (которые могут быть вложенные tooa подсистемы балансировки нагрузки, или сетевого Адаптера виртуальной машины). Hello PublicIpAddress должен иметь имя DNS, назначенное toobe, используемый в диспетчере трафика.

В каждом случае:

* Hello службы задается с помощью параметра «с идентификатором targetResourceId» hello `Add-AzureRmTrafficManagerEndpointConfig` или `New-AzureRmTrafficManagerEndpoint`.
* Hello «Целевой объект» и «EndpointLocation» содержится в разрешении hello идентификатором TargetResourceId.
* Указание hello «Weight» является необязательным. Весовые коэффициенты используются только в том случае, если профиль hello настроенных toouse метод маршрутизации трафика «Взвешенное» hello. В остальных случаях этот параметр игнорируется. Если указано, hello значение должно быть числом от 1 до 1000. значение по умолчанию Hello — "1".
* Указание hello «Приоритет» не является обязательным. Приоритеты используются только в том случае, если профиль hello настроенных toouse метод маршрутизации трафика «Приоритет» hello. В остальных случаях этот параметр игнорируется. Допустимые значения: от 1 too1000 с более низкими значениями, указывающее, более высокий приоритет. Если приоритет указан для одной конечной точки, он должен указываться и для всех остальных конечных точек. Если не указано, по умолчанию значения, начинающиеся с "1" применяются в порядке hello, что перечислены конечные точки hello.

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a>Пример 1. Добавление конечных точек веб-приложения с помощью командлета `Add-AzureRmTrafficManagerEndpointConfig`

В этом примере мы создать профиль диспетчера трафика и добавьте две конечные точки веб-приложения с помощью hello `Add-AzureRmTrafficManagerEndpointConfig` командлета.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a>Пример 2. Добавление конечной точки publicIpAddress с помощью командлета `New-AzureRmTrafficManagerEndpoint`

В этом примере открытого ресурса IP-адреса добавляется toohello профиль диспетчера трафика. Hello общедоступный IP-адрес должен иметь имя DNS настроены и могут быть привязаны либо toohello сетевого Адаптера виртуальной Машины или tooa подсистемы балансировки нагрузки.

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a>Добавление внешних конечных точек

Трафик Manager использует tooservices трафика toodirect внешние конечные точки, размещенных за пределами Azure. Как и конечные точки Azure, внешние конечные точки можно добавить с помощью командлета `Add-AzureRmTrafficManagerEndpointConfig`, за которым следует командлет `Set-AzureRmTrafficManagerProfile` или `New-AzureRMTrafficManagerEndpoint`.

При добавлении внешних конечных точек:

* должно быть указано имя домена Hello конечной точки с помощью параметра «Целевой объект» hello
* При использовании hello метод маршрутизации трафика «Производительность» hello «EndpointLocation» является обязательным. В противном случае этот параметр является необязательным. Hello значение должно быть [имя допустимым регион Azure](https://azure.microsoft.com/regions/).
* Здравствуйте, «Вес» и «Приоритет» являются необязательными.

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Пример 1. Добавление внешних конечных точек с помощью командлетов `Add-AzureRmTrafficManagerEndpointConfig` и `Set-AzureRmTrafficManagerProfile`

В этом примере мы создать профиль диспетчера трафика, добавьте две внешние конечные точки и фиксации изменений hello.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Пример 2. Добавление внешних конечных точек с помощью командлета `New-AzureRmTrafficManagerEndpoint`

В этом примере мы добавить существующий профиль tooan внешней конечной точки. профиль Hello задается с помощью имен групп hello профиля и ресурсов.

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a>Добавление "вложенных" конечных точек

Каждый профиль диспетчера трафика определяет один метод маршрутизации трафика. Однако существуют сценарии, требующие более сложные маршрутизации трафика, чем hello маршрутизации, предоставляемые единый профиль диспетчера трафика. Можно вложить профилей диспетчера трафика toocombine преимущества hello более чем один метод маршрутизации трафика. Вложенные профили позволяют toooverride hello по умолчанию диспетчер трафика поведение toosupport больших и сложных развертываний приложений. Более подробные примеры см. в статье [Вложенные профили диспетчера трафика](traffic-manager-nested-profiles.md).

Вложенные конечные точки настраиваются на родительском профиле hello, с помощью типа конкретной конечной точки, «NestedEndpoints». При указании вложенных конечных точек:

* Hello конечной точки должен быть указан с помощью параметра «с идентификатором targetResourceId» hello
* При использовании hello метод маршрутизации трафика «Производительность» hello «EndpointLocation» является обязательным. В противном случае этот параметр является необязательным. Hello значение должно быть [имя допустимым регион Azure](http://azure.microsoft.com/regions/).
* Здравствуйте, «Вес» и «Приоритет» являются необязательными, как и для конечные точки Azure.
* параметр «MinChildEndpoints» Hello является необязательным. значение по умолчанию Hello — "1". Если число доступных конечных точек в hello падает ниже этого значения, hello родительским профилем считает hello дочернем профиле «Деградация» и в результате трафик toohello другим конечным точкам в родительском профиле hello.

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Пример 1. Добавление вложенных конечных точек с помощью командлетов `Add-AzureRmTrafficManagerEndpointConfig` и `Set-AzureRmTrafficManagerProfile`

В этом примере мы создать новый диспетчер трафика дочерней и родительской профили, добавить дочерний hello как родитель toohello вложенных конечной точки и фиксации изменений hello.

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Для краткости в этом примере мы не добавил другие конечные точки toohello дочерних или родительских профили.

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Пример 2. Добавление вложенных конечных точек с помощью командлета `New-AzureRmTrafficManagerEndpoint`

В этом примере мы добавить существующий профиль дочерних как родительский профиль существующих tooan вложенных конечной точки. профиль Hello задается с помощью имен групп hello профиля и ресурсов.

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a>Обновление конечной точки диспетчера трафика

Существует два способа tooupdate существующую конечную точку диспетчера трафика.

1. Получить с помощью профиля диспетчера трафика hello `Get-AzureRmTrafficManagerProfile`, обновить hello свойства конечной точки в профиле hello и фиксации изменений hello, с помощью `Set-AzureRmTrafficManagerProfile`. Этот метод имеет hello преимущество может tooupdate более одной конечной точки в одной операции.
2. Получить hello конечной точки диспетчера трафика с помощью `Get-AzureRmTrafficManagerEndpoint`, обновить свойства конечной точки hello и фиксации изменений hello, с помощью `Set-AzureRmTrafficManagerEndpoint`. Этот способ проще, так как он не требует индексирование в массиве hello конечных точек в профиле hello.

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a>Пример 1. Обновление конечных точек с помощью командлетов `Get-AzureRmTrafficManagerProfile` и `Set-AzureRmTrafficManagerProfile`

В этом примере мы изменение приоритета hello на две конечные точки в пределах существующего профиля.

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a>Пример 2. Обновление конечной точки с помощью командлетов `Get-AzureRmTrafficManagerEndpoint` и `Set-AzureRmTrafficManagerEndpoint`

В этом примере мы изменить вес hello одну конечную точку в существующий профиль.

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a>Включение и отключение конечных точек и профилей

Диспетчер трафика позволяет toobe отдельные конечные точки включенных и отключенных предоставлять Включение и отключение всего профилей.
Эти изменения можно внести ресурсами конечная точка либо профиль hello получения и обновления или установки. toostreamline этих общих операций, также поддерживаются через специализированные командлеты.

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a>Пример 1. Включение и отключение профиля диспетчера трафика

использовать профиль диспетчера трафика tooenable `Enable-AzureRmTrafficManagerProfile`. Hello профиля можно указать с помощью объекта профиля. Hello объекта профиля можно передать по конвейеру hello, или с помощью hello "-TrafficManagerProfile" параметра. В этом примере мы укажите профиль hello hello профиля и ресурсов групп по имени.

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

toodisable профиль диспетчера трафика:

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

командлет Disable-AzureRmTrafficManagerProfile Hello запрашивает подтверждение. Это предупреждение можно подавить при помощи hello '-Force "параметра.

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a>Пример 2. Включение и отключение конечной точки диспетчера трафика

использовать конечную точку диспетчера трафика, tooenable `Enable-AzureRmTrafficManagerEndpoint`. Существует два способа toospecify hello endpoint

1. С помощью TrafficManagerEndpoint объект, переданный через конвейер hello или hello "-TrafficManagerEndpoint" параметра
2. Использование имени конечной точки hello, тип конечной точки, имя профиля и имя группы ресурсов.

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

Аналогичным образом toodisable конечную точку диспетчера трафика:

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

Как и в `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` командлет запросит подтверждение. Это предупреждение можно подавить при помощи hello '-Force "параметра.

## <a name="delete-a-traffic-manager-endpoint"></a>Удаление конечной точки диспетчера трафика

использовать отдельные конечные точки tooremove hello `Remove-AzureRmTrafficManagerEndpoint` командлета:

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

Этот командлет запрашивает подтверждение. Это предупреждение можно подавить при помощи hello '-Force "параметра.

## <a name="delete-a-traffic-manager-profile"></a>Удаление профиля диспетчера трафика

использовать профиль диспетчера трафика toodelete hello `Remove-AzureRmTrafficManagerProfile` командлета, указание имен hello профиля и ресурсов группы:

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

Этот командлет запрашивает подтверждение. Это предупреждение можно подавить при помощи hello '-Force "параметра.

удалить toobe профиль Hello могут быть указаны с помощью объекта профиля:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

Эти операции также можно объединить в последовательность:

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a>Дальнейшие действия

[Мониторинг диспетчера трафика](traffic-manager-monitoring.md)

[Рекомендации по безопасности для диспетчера трафика](traffic-manager-performance-considerations.md)
