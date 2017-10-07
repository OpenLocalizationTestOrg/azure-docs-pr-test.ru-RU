---
title: "aaaMove ресурсы Azure toonew подписка или группа ресурсов | Документы Microsoft"
description: "С помощью диспетчера ресурсов Azure toomove ресурсов tooa новую группу ресурсов или подписки."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a>Переместить группу ресурсов toonew ресурсов или подписку
В этом разделе показано, как ресурсы tooeither toomove новую подписку или новый ресурс в группы hello одной подписке. Можно использовать портал hello, PowerShell, Azure CLI или hello ресурс toomove REST API. операции перемещения Hello в этом разделе, доступны tooyou безо всякой помощи со службой поддержки Azure.

При перемещении ресурсов, исходная группа hello и целевая группа hello блокируются во время операции hello. Записи и удаления операций заблокированы для групп ресурсов hello до завершения перемещения hello. Эта блокировка означает невозможно добавить, обновить или удалить ресурсов в группах ресурсов hello, но это означает, что ресурсы hello, зафиксированы. Например при перемещении SQL Server и его базы данных tooa группы ресурсов, приложение, использующее hello базы данных приложений без простоев. Он по-прежнему могут читать и записывать toohello базы данных.

Невозможно изменить расположение hello hello ресурса. Перемещение ресурса только перемещение его tooa новую группу ресурсов. Hello группы ресурсов может иметь другое расположение, но не изменяет расположение hello hello ресурса.

> [!NOTE]
> В этой статье описывается, как toomove ресурсов в Azure существующей учетной записи предложения. См. учетную запись Azure предложения (например, обновление с оплатой по мере использования toopre зарплаты), продолжая toowork с существующие ресурсы, если требуется фактически toochange [переключения вашего предложения подписки Azure tooanother](../billing/billing-how-to-switch-azure-offer.md).
>
>

## <a name="checklist-before-moving-resources"></a>Рекомендации перед перемещением ресурсов
Существуют некоторые важные действия tooperform перед перемещением ресурса. Проверив эти условия, можно избежать ошибок.

1. Hello источника и назначения подписки должен существовать внутри hello же [клиента Azure Active Directory](../active-directory/active-directory-howto-tenant.md). toocheck, что обе подписки имеют hello таким же Идентификатором клиента, с помощью Azure PowerShell или Azure CLI.

  Для Azure PowerShell:

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  В Azure CLI 2.0 используйте следующую команду.

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  Если идентификаторы клиента hello hello исходный и целевой подписки не же hello, можно попытаться каталога hello toochange для hello подписки. Тем не менее это может быть только доступные tooService Администраторы, выполнившие вход с учетной записью Майкрософт (не учетная запись организации). Изменение каталога hello, вход toohello tooattempt [классический портал](https://manage.windowsazure.com/)и выберите **параметры**и выберите подписку hello. Если hello **изменить каталог** значок, выберите его toochange hello связанные Azure Active Directory.

  ![Изменение каталога](./media/resource-group-move-resources/edit-directory.png)

  Если этот значок недоступен, необходимо обратитесь в службу поддержки toomove hello ресурсы tooa новым клиентом.

2. Hello службы необходимо включить hello возможность toomove ресурсов. В этом разделе перечислено, какие службы позволяют перемещать ресурсы, а какие — нет.
3. Hello назначения подписки должны быть зарегистрированы для поставщика ресурсов hello перемещения ресурса hello. Если нет, появится сообщение о том, что hello **подписка не зарегистрирована для типа ресурса**. Этой проблемы могут возникнуть при перемещении ресурсов tooa новую подписку, но никогда не использовалось этой подписки с этим типом ресурса. toolearn toocheck hello состояние регистрации и регистрации поставщиков ресурсов разделе [поставщиков ресурсов и типы](resource-manager-supported-services.md).

## <a name="when-toocall-support"></a>Когда поддержка toocall
Можно переместить больше всего ресурсов через операции самообслуживания hello, приведенные в этом разделе. Используйте hello самообслуживания операций:

* перемещение ресурсов Resource Manager;
* Переместить классические ресурсы в соответствии с toohello [ограничения классического развертывания](#classic-deployment-limitations).

Обратитесь в службу поддержки, если необходимо выполнить такие действия:

* Перемещение ресурсов tooa новую учетную запись Azure (и клиент Azure Active Directory).
* Переместить классические ресурсы, но возникают проблемы с ограничениями hello.

## <a name="services-that-enable-move"></a>Службы, поддерживающие перемещение
Пока используются следующие службы hello, позволяющие выполнять перемещение tooboth новую группу ресурсов и подписки:

* Управление API
* Приложения службы приложений (веб-приложения) — см. раздел [Ограничения службы приложений](#app-service-limitations).
* Application Insights
* Автоматизация
* Пакетная служба
* Карты Bing
* CDN
* Облачные службы — см. раздел [Ограничения классического развертывания](#classic-deployment-limitations).
* Cognitive Services
* Content Moderator
* Каталог данных
* Фабрика данных
* Аналитика озера данных
* Хранилище озера данных
* DNS
* Azure Cosmos DB
* Концентраторы событий
* Кластеры HDInsight — см. раздел [Ограничения HDInsight](#hdinsight-limitations).
* Центры Интернета вещей;
* Хранилище ключей
* Балансировщики нагрузки
* Приложения логики
* Машинное обучение
* Службы мультимедиа
* Службы мобильного взаимодействия
* Центры уведомлений
* Operational Insights;
* Пакет Operations Management
* Power BI
* Кэш Redis
* Планировщик
* Поиск
* Управление сервером
* Служебная шина
* Service Fabric
* Хранилище
* Служба хранилища (классическая) — см. раздел [Ограничения классического развертывания](#classic-deployment-limitations).
* Stream Analytics — задание Stream Analytics в состоянии выполнения нельзя переместить.
* Сервер базы данных SQL - hello базы данных и сервер должны находиться в hello одну группу ресурсов. При перемещении сервера SQL Server все его базы данных также перемещаются.
* Диспетчер трафика
* Виртуальные машины
* Виртуальные машины с сертификатом, который хранится в хранилище ключей — перемещение группы ресурсов toonew в той же подписке включена, но перемещения перекрестного подписки не включен.
* Виртуальные машины (классические) — см. раздел [Ограничения классического развертывания](#classic-deployment-limitations).
* Наборы для масштабирования виртуальных машин
* Виртуальные сети. В настоящее время невозможно переместить пиринговую виртуальную сеть, пока не будет отключен ее пиринг. После отключения hello виртуальной сети успешно перенести и пиринг hello виртуальной сети можно включить. Кроме того виртуальной сети не может быть перемещенный tooa другую подписку, если какой-либо подсети с ссылками для перехода ресурса содержит hello виртуальной сети. Например, подсеть виртуальной сети содержит ссылку перехода к ресурсу, когда ресурс Redis Microsoft.Cache развертывается в этой подсети.
* VPN-шлюз


## <a name="services-that-do-not-enable-move"></a>Службы, не поддерживающие перемещение
Hello службы, которые в настоящее время не включайте Перемещение ресурса:

* доменные службы Active Directory;
* служба работоспособности гибридного AD;
* Шлюз приложений
* Группы доступности, содержащие виртуальные машины с управляемыми дисками.
* Службы BizTalk
* Служба контейнеров
* ExpressRoute
* DevTest Labs - переместить группу ресурсов toonew в той же подписке включена, но кросс-перемещение подписки не включен.
* Dynamics LCS.
* Образы, созданные из управляемых дисков.
* Управляемые диски
* Управляемые приложения.
* Хранилище служб восстановления — также не перемещения hello вычисления, сети и хранилища ресурсы, связанные с подстроку hello служб восстановления хранилище см. в разделе [ограничения службы восстановления](#recovery-services-limitations).
* Безопасность
* Моментальные снимки, созданные из управляемых дисков.
* Диспетчер устройств StorSimple
* Виртуальные машины с Управляемыми дисками
* Виртуальные сети (классические) — см. раздел [Ограничения классического развертывания](#classic-deployment-limitations).
* Виртуальные машины, созданные из ресурсов Marketplace, невозможно переместить между подписками. Ресурс должен toobe отозваны в текущей подписке hello и выполнить развертывание повторно в новой подписки hello

## <a name="app-service-limitations"></a>Ограничения службы приложений
При работе с приложениями службы приложений невозможно переместить только план службы приложений. приложения служб приложений toomove, имеются следующие возможности:

* Переместите hello план служб приложений и остальные ресурсы службы приложения, ресурсов группы tooa группы ресурсов, не имеет ресурсы службы приложений. Это требование, что означает, что необходимо переместить даже hello ресурсов приложения службы, не связаны с hello план служб приложений.
* Переместить hello приложений tooa другой группе ресурсов, но сохранить все планы служб приложений в hello исходной группы ресурсов.

Hello необязательно tooreside в плане служб приложений hello же группе ресурсов, что приложение hello для toofunction приложения hello правильно.

Например, если группа ресурсов содержит:

* ресурс **web-a**, связанный с **plan-a**;
* ресурс **web-b**, связанный с **plan-b**.

Вам доступны следующие действия:

* перемещение **web-a**, **plan-a**, **web-b**, и **plan-b**;
* перемещение **web-a** и **web-b**;
* перемещение **web-a**
* перемещение **web-b**

Все другие сочетания включают необходимость оставить тип ресурса, который нельзя оставлять при перемещении плана службы приложений (любой тип ресурса службы приложений).

Если веб-приложение находится в группе ресурсов, отличной от его план служб приложений, но требуется toomove оба tooa группы ресурсов, необходимо выполнить перемещение hello в два этапа. Например:

* **web-a** находится в группе **web-group**;
* **plan-a** находится в группе **plan-group**;
* Вы хотите **веб a** и **плана a** tooreside в **объединять группы**

tooaccomplish необходимо переместить, выполнять операции два отдельных перемещения в hello следующая последовательность:

1. Переместить hello **веб a** слишком**группа планов**
2. Переместить **веб a** и **плана a** слишком**объединять группы**.

Можно переместить сертификат службы приложения tooa группы ресурсов или подписку без проблем. Тем не менее если веб-приложение включает сертификат SSL, приобретенных извне и отправлены toohello приложения, необходимо удалить сертификат hello до перемещения веб-приложения hello. Например можно выполнить hello следующие шаги:

1. Удалить сертификат hello загружен из веб-приложения hello
2. Перемещение веб-приложения hello
3. Отправка hello сертификат toohello веб-приложения

## <a name="recovery-services-limitations"></a>Ограничения служб восстановления
Перемещение не включена для хранилища, сети, или вычислительные ресурсы используются tooset настройки аварийного восстановления с помощью Azure Site Recovery.

Например предположим, что вы настроили репликации из локальной машины tooa учетной записи хранения (Storage1) и хотите hello защищенные машины toocome копии после отработки отказа tooAzure как виртуальной машины (VM1) подключенные tooa виртуальной сети (Network1). Не удается переместить любой из этих ресурсов Azure - Storage1, VM1, и Network1 - через ресурсов группирует в hello же подписки или в подписках.

## <a name="hdinsight-limitations"></a>Ограничения HDInsight

Можно переместить HDInsight кластеры tooa новую подписку или группу ресурсов. Однако не удалось переместить между подписками hello сети кластера HDInsight toohello связанные ресурсы (например, «hello виртуальной сети, Сетевых или подсистемы балансировки нагрузки). Кроме того невозможно переместить tooa группы ресурсов сетевого Адаптера, подключенных tooa виртуальной машины для hello кластера.

При перемещении кластера HDInsight tooa новую подписку, необходимо сначала переместите другие ресурсы (например, учетная запись хранения hello). Затем переместите кластера HDInsight hello сам по себе.

## <a name="classic-deployment-limitations"></a>Ограничения классического развертывания
Hello параметры перемещения ресурсов, развернутые с помощью классической модели hello зависят от перемещаемой hello ресурсов в подписке или tooa новую подписку.

### <a name="same-subscription"></a>Та же подписка
При перемещении ресурсов из одной группы tooanother ресурсов группы ресурсов в одной подписке, hello следующие ограничения применяются hello:

* Нельзя перемещать виртуальные сети (классические).
* Виртуальные машины (классические) должны быть перемещены hello облачной службе.
* Облачные службы могут перемещаться только в тех случаях, когда перемещения hello включает все виртуальные машины.
* Одновременно можно перемещать только одну облачную службу.
* Одновременно можно перемещать только одну учетную запись хранения (классическую).
* Учетная запись хранения (классические) не может быть перемещен в hello одной операции с виртуальной машины или облачной службы.

toomove классические ресурсы tooa группы ресурсов в hello той же подписке, используйте стандартный hello перемещении через hello [портала](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), или [API-интерфейса REST](#use-rest-api). Вы используете hello и те же операции, как использовать для перемещения ресурсов диспетчера ресурсов.

### <a name="new-subscription"></a>Новая подписка
При перемещении ресурсов tooa новую подписку, применяются следующие ограничения hello.

* Необходимо переместить все классические ресурсы в подписке hello в hello одной операции.
* Hello целевой подписки не должен содержать классические ресурсы.
* Перемещение Hello можно запросить только через отдельный API REST для классического переход. Hello стандартные команды перемещения диспетчер ресурсов не работают при перемещении классические ресурсы tooa новую подписку.

toomove классические ресурсы tooa новую подписку, используйте hello REST операции, которые будут tooclassic определенных ресурсов. toouse REST, выполните следующие шаги hello.

1. Проверка, если исходная подписка hello могут участвовать в разных подписок переместить. Используйте следующую операцию hello.

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     В тексте запроса hello включают:

  ```json
  {
    "role": "source"
  }
  ```

     Hello ответ для операции проверки hello имеет hello следующий формат:

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. Флажок, если hello конечная подписка может участвовать в разных подписок переместить. Используйте следующую операцию hello.

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     В тексте запроса hello включают:

  ```json
  {
    "role": "target"
  }
  ```

     Hello ответа находится в том же формате, как проверка подписки источника hello hello.
3. Если обе подписки проходят проверку, перемещение всех классических ресурсов из одной подписки tooanother подписки с hello следующую операцию:

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    В тексте запроса hello включают:

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

Hello операция может занять несколько минут.

## <a name="use-portal"></a>С помощью портала
ресурсы toomove выбрать группу ресурсов hello, содержащие эти ресурсы, а затем выберите hello **переместить** кнопки.

![перемещение ресурсов](./media/resource-group-move-resources/select-move.png)

Выберите, будут ли перемещении hello ресурсы tooa группы ресурсов или новую подписку.

Выберите toomove hello ресурсы и группы ресурсов целевой hello. Подтвердить необходимость tooupdate скрипты для этих ресурсов и выберите **ОК**. Если вы выбрали hello Правка подписки на предыдущем шаге hello, необходимо выбрать hello конечная подписка.

![выбор места назначения](./media/resource-group-move-resources/select-destination.png)

В **уведомления**, вы видите, hello перемещение выполняется операция.

![отображение состояния перемещения](./media/resource-group-move-resources/show-status.png)

После ее завершения, получают уведомления hello результата.

![отображение результата перемещения](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a>Использование PowerShell
toomove существующую группу ресурсов tooanother ресурсов или подписку, используйте hello `Move-AzureRmResource` команды.

Hello в первом примере показан способ toomove один ресурс tooa группы ресурсов.

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

Hello второй пример показывает, как toomove несколько ресурсов tooa новую группу ресурсов.

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

toomove tooa новую подписку, добавьте значение hello `DestinationSubscriptionId` параметра.

Будет предложено ресурсов, указанных tooconfirm, что требуется toomove hello.

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a>Использование Azure CLI 2.0
toomove существующую группу ресурсов tooanother ресурсов или подписку, используйте hello `az resource move` команды. Укажите идентификаторы ресурсов toomove hello hello ресурса. Идентификаторы ресурсов можно получить с hello следующую команду:

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

Следующий пример Hello показано, как toomove хранилища учетной записи tooa новую группу ресурсов. В hello `--ids` параметр, укажите разделенный пробелами список toomove идентификаторы ресурсов hello.

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

toomove tooa новую подписку, укажите hello `--destination-subscription-id` параметра.

## <a name="use-azure-cli-10"></a>Использование Azure CLI 1.0
toomove существующую группу ресурсов tooanother ресурсов или подписку, используйте hello `azure resource move` команды. Укажите идентификаторы ресурсов toomove hello hello ресурса. Идентификаторы ресурсов можно получить с hello следующую команду:

```azurecli
azure resource list -g sourceGroup --json
```

Выдаются hello следующий формат:

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

Следующий пример Hello показано, как toomove хранилища учетной записи tooa новую группу ресурсов. В hello `-i` параметр, укажите список разделенных запятыми toomove идентификаторы ресурсов hello.

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

Будет предложено нужных toomove hello tooconfirm указанный ресурс.

## <a name="use-rest-api"></a>Использование REST API
toomove существующие ресурсы tooanother группу ресурсов или подписку, запустите:

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

В тексте запроса hello укажите hello целевая группа ресурсов и ресурсов toomove hello. Дополнительные сведения об операции REST перемещения hello см. в разделе [перемещение ресурсов](https://msdn.microsoft.com/library/azure/mt218710.aspx).

## <a name="next-steps"></a>Дальнейшие действия
* в разделе toolearn о командлетах PowerShell для управления подпиской, [с помощью Azure PowerShell с помощью диспетчера ресурсов](powershell-azure-resource-manager.md).
* в разделе toolearn о командах Azure CLI для управления подпиской, [использование hello Azure CLI с помощью диспетчера ресурсов](xplat-cli-azure-resource-manager.md).
* toolearn портала возможности для управления подпиской, в разделе [использование ресурсов Azure портала toomanage hello](resource-group-portal.md).
* toolearn о применении ресурсов tooyour логическую организацию, в разделе [использование теги tooorganize ресурсов](resource-group-using-tags.md).
