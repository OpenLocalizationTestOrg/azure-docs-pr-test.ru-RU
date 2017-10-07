---
title: "aaaAutomatic масштабирования и виртуальной машины масштабировать наборов | Документы Microsoft"
description: "Дополнительные сведения об использовании диагностики и автоматического масштабирования ресурсов tooautomatically масштабирования виртуальных машин в наборе масштабирования."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d29a3385-179e-4331-a315-daa7ea5701df
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: adegeo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 25f54b693e3c991577238242008c262023ed479c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a>Как автоматическое масштабирование toouse и наборы масштабирования виртуальных машин
Автоматическое масштабирование в наборе масштабирования виртуальных машин, — создание hello или удаления компьютеров в hello, задать в качестве требуются toomatch требований к производительности. По мере роста hello объем работ, приложению могут потребоваться дополнительные ресурсы tooenable его tooeffectively выполнения задач.

Автоматическое масштабирование — это автоматизированный процесс, который помогает упростить управление ресурсами. Уменьшение издержек, не требуется toocontinually наблюдение за производительностью системы и решить, каким образом ресурсы toomanage. Масштабирование — это эластичный процесс. Можно добавить дополнительные ресурсы при увеличении нагрузки hello. И как запросу уменьшается, удален toominimize затраты и ресурсам Ведение уровней производительности.

Настройте автоматическое масштабирование в масштабе, устанавливается с помощью диспетчера ресурсов Azure шаблона, Azure PowerShell, Azure CLI или hello портал Azure.

## <a name="set-up-scaling-by-using-resource-manager-templates"></a>Настройка масштабирования с помощью шаблонов Resource Manager
Чтобы не развертывать (с последующим управлением) каждый ресурс для приложения по отдельности, вы можете создать шаблон Azure Resource Manager, который развертывает все нужные ресурсы в ходе одной скоординированной операции. В шаблоне hello определенных ресурсов приложения и указанных параметров развертывания для разных сред. шаблон Hello состоит из выражения, что tooconstruct значения можно использовать для развертывания и JSON. toolearn более, посмотрите на [шаблоны разработки Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

В шаблоне hello необходимо указать элемент hello емкости:

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

Емкость определяет hello количество виртуальных машин в наборе hello. Можно вручную изменить hello емкости путем развертывания шаблона с другим значением. При развертывании изменений hello шаблона tooonly емкостью можно включить только элемент SKU hello емкостью hello обновлены.

Hello емкость набора масштабирования может автоматически настраиваться с помощью комбинации hello **autoscaleSettings** ресурсов и hello расширения диагностики.

### <a name="configure-hello-azure-diagnostics-extension"></a>Настройка расширения системы диагностики Azure hello
Автоматическое масштабирование может выполняться только при успешном выполнении на каждую виртуальную машину в наборе масштабирования hello коллекция метрик. Hello расширения системы диагностики Azure предоставляет возможности мониторинга и диагностики hello, удовлетворяющих потребностям hello метрики коллекции hello автомасштабирования ресурса. Hello расширения можно установить как часть шаблона диспетчера ресурсов hello.

Этот пример показывает hello переменные, которые используются в расширения диагностики hello tooconfigure шаблона hello.

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

Параметры предоставляются при развертывании шаблона hello. В этом примере hello имя учетной записи хранения hello (где хранятся данные) и hello предоставляются имя набора масштабирования hello (где данные собираются). Также в этом примере Windows Server собираются только hello потока счетчик производительности. Здравствуйте, все доступные счетчики производительности в Windows или Linux, может быть сведения диагностики используется toocollect и может быть включено в конфигурации расширения hello.

В этом примере показано определение расширения hello hello в шаблоне hello:

```json
"extensionProfile": {
  "extensions": [
    {
      "name": "Microsoft.Insights.VMDiagnosticsSettings",
      "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
          "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
          "storageAccount": "[variables('diagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
          "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
          "storageAccountKey": "[listkeys(variables('accountid'), variables('apiVersion')).key1]",
          "storageAccountEndPoint": "https://core.windows.net"
        }
      }
    }
  ]
}
```

При выполнении расширения диагностики hello hello данные хранятся и собираются в таблицу в учетной записи хранения hello, указываемое. В hello **WADPerformanceCounters** таблицы, можно найти hello собранных данных:

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a>Настройка ресурсов autoScaleSettings hello
Hello autoscaleSettings ресурсов использует hello сведения из toodecide расширения диагностики hello, установлены ли tooincrease или уменьшении hello количество виртуальных машин на шкале hello.

В этом примере показана конфигурация hello hello ресурса в шаблоне hello:

```json
{
  "type": "Microsoft.Insights/autoscaleSettings",
  "apiVersion": "2015-04-01",
  "name": "[concat(parameters('resourcePrefix'),'as1')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
  ],
  "properties": {
    "enabled": true,
    "name": "[concat(parameters('resourcePrefix'),'as1')]",
    "profiles": [
      {
        "name": "Profile1",
        "capacity": {
          "minimum": "1",
          "maximum": "10",
          "default": "1"
        },
        "rules": [
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "GreaterThan",
              "threshold": 650
            },
            "scaleAction": {
              "direction": "Increase",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          },
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "LessThan",
              "threshold": 550
            },
            "scaleAction": {
              "direction": "Decrease",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          }
        ]
      }
    ],
    "targetResourceUri": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
  }
}
```

В приведенном выше примере hello создаются два правила для определения действий автоматического масштабирования hello. Первое правило Hello определяет действие масштабирования hello и hello второе правило определяет hello масштабирования в действие. Эти значения указаны в правилах hello:

| правило; | Описание |
| ---- | ----------- |
| metricName        | Это значение является hello то же, что счетчик производительности hello, определенный в переменной wadperfcounter hello для расширения диагностики hello. В приведенном выше примере hello используется hello счетчика потоков.    |
| metricResourceUri | Это значение является идентификатором ресурса hello hello набора масштабирования виртуальных машин. Этот идентификатор содержит hello имя группы ресурсов hello, имя поставщика ресурсов hello hello и имя hello tooscale набор масштабирования hello. |
| timeGrain         | Это значение является гранулярности hello hello метрик, которые собираются. В предыдущих пример hello данные собираются на интервал до одной минуты. Это значение используется вместе со значением timeWindow. |
| statistic         | Это значение определяет, как метрики hello hello объединенный tooaccommodate автоматического масштабирования действия. Возможные значения Hello: Average, Min, Max. |
| timeWindow        | Это значение является hello диапазон времени, в котором собираются данные экземпляра. Значение должно составлять от 5 минут до 12 часов. |
| timeAggregation   | Это значение определяет способ объединения собираемых данных hello со временем. значение по умолчанию Hello — среднее значение. Возможные значения Hello: среднее, минимальное, максимальное, конец, общее, число. |
| operator          | Это значение является hello оператор, который используется toocompare hello метрики данных и hello порогового значения. Hello возможными значениями являются: равно NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual. |
| threshold         | Это значение является hello значение, которое запускает действие масштабирования hello. Быть достаточная разница между hello пороговые значения для hello убедиться, что tooprovide **масштабирования** и **масштабирования в** действия. Если задать одинаковые значения для обоих этих действий hello hello системы можно предвидеть постоянное изменение, который препятствует его реализации действия масштабирования. Например установка обоих too600 потоков в предшествующий пример hello не работает. |
| direction         | Это значение определяет hello действие, которое предпринимается, когда достигается пороговое значение hello. Возможные значения Hello: увеличиваются или уменьшаются. |
| type              | Это значение является hello тип действия, которое должно выполняться и значением tooChangeCount. |
| value             | Это значение является hello число виртуальных машин, которые добавляются tooor удалены из набора масштабирования hello. Для этого параметра должно быть указано значение не меньше 1. |
| cooldown          | Это значение является hello объем toowait времени с момента последнего действия масштабирования hello, прежде чем произойдет следующее действие hello. Допустимые значения: от одной минуты до одной недели. |

В зависимости от счетчика производительности hello вы используете, некоторые элементы hello в hello шаблона конфигурации используются по-разному. В предшествующих пример hello, hello счетчика производительности — число потоков, hello пороговое значение — 650 для действия масштабирования; hello пороговое значение — 550 для hello масштабирования в действие. При использовании счетчиков, такие как % загруженности процессора hello пороговое значение toohello процент использования ЦП, которое определяет действия масштабирования.

При запуске действия масштабирования, например высокой нагрузки, емкость hello hello набора увеличивается на основе значения hello в шаблоне hello. Например на шкале задать где заданная too3 емкость hello, а значение действия масштабирования hello равно too1:

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

Когда hello текущей нагрузки причины hello потока среднее число toogo выше порогового значения hello объекта 650:

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

Объект **масштабирования** выполняется действие, причины hello емкость toobe набор hello увеличено на 1:

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

результат Hello — добавлении toohello набор масштабирования виртуальной машины:

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

После периода cooldown пять минут Если hello среднее число потоков на машинах hello остается более 600 другой компьютер добавляется набор toohello. Если hello потока среднее количество остается ниже 550, hello емкость набора масштабирования hello уменьшается на единицу и машина будет удалена из набора hello.

## <a name="set-up-scaling-using-azure-powershell"></a>Настройка масштабирования с помощью Azure PowerShell

Просмотрите примеры использования PowerShell tooset копирование автоматическое масштабирование, toosee [монитор Azure PowerShell быстрый запуск образцов](../monitoring-and-diagnostics/insights-powershell-samples.md).

## <a name="set-up-scaling-using-azure-cli"></a>Настройка масштабирования с помощью интерфейса командной строки Azure (Azure CLI)

Просмотрите примеры использования Azure CLI tooset копирование автоматическое масштабирование, toosee [монитора Azure кросс платформенных CLI быстрый запуск образцов](../monitoring-and-diagnostics/insights-cli-samples.md).

## <a name="set-up-scaling-using-hello-azure-portal"></a>Настройка масштабирования с помощью портала Azure hello

Пример использования toosee hello Azure портала tooset копирование автоматическое масштабирование, просмотрите в [создания набора масштабирования виртуальных машин с помощью портала Azure hello](virtual-machine-scale-sets-portal-create.md).

## <a name="investigate-scaling-actions"></a>Изучение действий масштабирования

* **Портал Azure**  
В настоящее время можно получить ограниченный объем информации с помощью портала hello.

* **Azure Resource Explorer**  
Это средство — hello, наилучшим образом подходит для изучения hello текущее состояние набора масштабирования. Выполните этот путь, и вы увидите набор, созданный представление экземпляра hello hello шкалы:  
**Subscriptions > {ваша подписка} > resourceGroups > {ваша группа ресурсов} > providers > Microsoft.Compute > virtualMachineScaleSets > {ваш масштабируемый набор} > virtualMachines**

* **Azure PowerShell**  
С помощью этой команды tooget некоторые данные.

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* Подключение toohello jumpbox виртуальной машины, так же, как и любой другой компьютер и затем позволяет осуществлять удаленный доступ hello виртуальных машин в отдельных процессах набор масштабирования toomonitor hello.

## <a name="next-steps"></a>Дальнейшие действия
* Посмотрите на [автоматически масштабировать машины в наборе масштабирования виртуальных машин](virtual-machine-scale-sets-windows-autoscale.md) toosee примером как toocreate шкале задать настройки автоматического масштабирования.

* Просмотрите примеры функций мониторинга Azure Monitor в статье [Примеры для быстрого запуска Azure Insights с помощью PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md).

* Дополнительные сведения о функции уведомлений в [используйте автомасштабирования действия toosend электронной почты и веб-перехватчика уведомлений о предупреждениях в мониторе Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).

* Дополнительные сведения о слишком[журналы аудита используйте toosend электронной почты и веб-перехватчика уведомлений о предупреждениях в мониторе Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)

* Узнайте больше о [расширенных сценариях автомасштабирования](virtual-machine-scale-sets-advanced-autoscale.md).
