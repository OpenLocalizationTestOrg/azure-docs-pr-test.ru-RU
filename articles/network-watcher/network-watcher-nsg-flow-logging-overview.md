---
title: "Ведение журнала tooflow aaaIntroduction для группы безопасности сети с Наблюдатель сети Azure | Документы Microsoft"
description: "На этой странице объясняется, как поток NSG toouse регистрирует функцию Наблюдатель сети Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: da85e946147b14717144cb47d1c742057c6dfa24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooflow-logging-for-network-security-groups"></a>Ведение журнала tooflow введение для групп безопасности сети

Сетевая группа безопасности потока журналы являются возможностью Наблюдатель сети, который позволяет вам tooview сведения о входящего и исходящего IP-трафика через группу безопасности сети. Эти потока журналы записываются в формате json и Показать исходящих и входящих потоков на основе каждого правила hello потока hello сетевого Адаптера, применяется 5-фрагментному сведения о потоке hello (источник и назначение IP-адрес, порт источника или целевой Protocol) и если hello был разрешен трафик или запрещено.

![Обзор журналов потоков][1]

Хотя поток входит в целевые группы безопасности сети, они не отображаются hello же, как hello другие журналы. Поток журналы хранятся только в пределах учетной записи хранилища и следующий путь hello ведения журнала, как показано в следующий пример hello:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

Здравствуйте же политики хранения, как показано на другие журналы применить tooflow журналы. Журналы имеют политики хранения, может принимать значения от 1 дня too365 дней. Если политика хранения не задано, журналы hello сохраняются навсегда.

## <a name="log-file"></a>Файл журнала

Журналы потоков имеют несколько свойств. Hello ниже приведен перечень hello свойства, которые возвращаются в hello NSG потока журнала.

* **время** — время, когда было зарегистрировано событие hello
* **systemId** — идентификатор ресурса группы безопасности сети.
* **Категория** -категории hello hello события, это будет всегда быть NetworkSecurityGroupFlowEvent
* **ResourceId** -hello hello NSG идентификатор ресурса
* **operationName** — всегда имеет значение NetworkSecurityGroupFlowEvents.
* **свойства** -это коллекция свойств потока hello
    * **Версия** -номер версии схемы событий потока журнала hello
    * **flows** — набор потоков. Это свойство имеет несколько записей для различных ролей.
        * **правило** -правило, для которых hello перечислены потоки
            * **flows** — набор потоков.
                * **Mac** -hello MAC-адрес hello сетевой Адаптер для виртуальной Машины, где были собраны потока hello hello
                * **flowTuples** -строка, содержащая несколько свойств для hello кортежа поток в формате с разделителями запятыми
                    * **Штамп времени** -это значение равно hello отметку времени возникновения hello поток в формате ЭПОХИ UNIX
                    * **Исходный IP-адрес** - hello исходный IP-адрес
                    * **Конечный IP** -hello конечный IP-адрес
                    * **Исходный порт** - hello порт источника
                    * **Порт назначения** -hello порт назначения
                    * **Протокол** -hello протокола hello потока. Допустимые значения: **T** для протокола TCP и **U** для протокола UDP.
                    * **Поток трафика** -hello направление потока трафика hello. Допустимые значения: **I** для входящего трафика и **O** для исходящего трафика.
                    * **Traffic** — указывает, разрешен или запрещен трафик. Допустимые значения: **A**, если трафик разрешен, и **D**, если запрещен.


Hello ниже приведен пример журнала потока. Как видно, что имеется несколько записей, следующие за hello список свойств, описанных в предшествующих раздел hello. 

> [!NOTE]
> Значения в свойстве flowTuples hello: список с разделителями запятыми.
 
```json
{
    "records": 
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, каким образом ведет журнал tooenable потока, посетив [потока Включение ведения журнала](network-watcher-nsg-flow-logging-portal.md).

Дополнительные сведения о ведении журнала NSG см. в разделе [Аналитика журналов для групп безопасности сети](../virtual-network/virtual-network-nsg-manage-log.md).

Сведения о том, как узнать, разрешен или запрещен трафик на виртуальной машине, см. в разделе [Проверка состояния входящего и исходящего трафика виртуальной машины (разрешен или запрещен) путем проверки IP-потока (компонент Наблюдателя за сетями Azure)](network-watcher-check-ip-flow-verify-portal.md).

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

