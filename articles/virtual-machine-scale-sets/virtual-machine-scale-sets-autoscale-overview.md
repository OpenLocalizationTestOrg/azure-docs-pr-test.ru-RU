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
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a><span data-ttu-id="9f1ab-103">Как автоматическое масштабирование toouse и наборы масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="9f1ab-103">How toouse automatic scaling and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="9f1ab-104">Автоматическое масштабирование в наборе масштабирования виртуальных машин, — создание hello или удаления компьютеров в hello, задать в качестве требуются toomatch требований к производительности.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-104">Automatic scaling of virtual machines in a scale set is hello creation or deletion of machines in hello set as needed toomatch performance requirements.</span></span> <span data-ttu-id="9f1ab-105">По мере роста hello объем работ, приложению могут потребоваться дополнительные ресурсы tooenable его tooeffectively выполнения задач.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-105">As hello volume of work grows, an application may require additional resources tooenable it tooeffectively perform tasks.</span></span>

<span data-ttu-id="9f1ab-106">Автоматическое масштабирование — это автоматизированный процесс, который помогает упростить управление ресурсами.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-106">Automatic scaling is an automated process that helps ease management overhead.</span></span> <span data-ttu-id="9f1ab-107">Уменьшение издержек, не требуется toocontinually наблюдение за производительностью системы и решить, каким образом ресурсы toomanage.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-107">By reducing overhead, you don't need toocontinually monitor system performance or decide how toomanage resources.</span></span> <span data-ttu-id="9f1ab-108">Масштабирование — это эластичный процесс.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-108">Scaling is an elastic process.</span></span> <span data-ttu-id="9f1ab-109">Можно добавить дополнительные ресурсы при увеличении нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-109">More resources can be added as hello load increases.</span></span> <span data-ttu-id="9f1ab-110">И как запросу уменьшается, удален toominimize затраты и ресурсам Ведение уровней производительности.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-110">And as demand decreases, resources can be removed toominimize costs and maintain performance levels.</span></span>

<span data-ttu-id="9f1ab-111">Настройте автоматическое масштабирование в масштабе, устанавливается с помощью диспетчера ресурсов Azure шаблона, Azure PowerShell, Azure CLI или hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-111">Set up automatic scaling on a scale set by using an Azure Resource Manager template, Azure PowerShell, Azure CLI, or hello Azure portal.</span></span>

## <a name="set-up-scaling-by-using-resource-manager-templates"></a><span data-ttu-id="9f1ab-112">Настройка масштабирования с помощью шаблонов Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9f1ab-112">Set up scaling by using Resource Manager templates</span></span>
<span data-ttu-id="9f1ab-113">Чтобы не развертывать (с последующим управлением) каждый ресурс для приложения по отдельности, вы можете создать шаблон Azure Resource Manager, который развертывает все нужные ресурсы в ходе одной скоординированной операции.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-113">Rather than deploying and managing each resource of your application separately, use a template that deploys all resources in a single, coordinated operation.</span></span> <span data-ttu-id="9f1ab-114">В шаблоне hello определенных ресурсов приложения и указанных параметров развертывания для разных сред.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-114">In hello template, application resources are defined and deployment parameters are specified for different environments.</span></span> <span data-ttu-id="9f1ab-115">шаблон Hello состоит из выражения, что tooconstruct значения можно использовать для развертывания и JSON.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-115">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="9f1ab-116">toolearn более, посмотрите на [шаблоны разработки Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9f1ab-116">toolearn more, look at [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="9f1ab-117">В шаблоне hello необходимо указать элемент hello емкости:</span><span class="sxs-lookup"><span data-stu-id="9f1ab-117">In hello template, you specify hello capacity element:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

<span data-ttu-id="9f1ab-118">Емкость определяет hello количество виртуальных машин в наборе hello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-118">Capacity identifies hello number of virtual machines in hello set.</span></span> <span data-ttu-id="9f1ab-119">Можно вручную изменить hello емкости путем развертывания шаблона с другим значением.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-119">You can manually change hello capacity by deploying a template with a different value.</span></span> <span data-ttu-id="9f1ab-120">При развертывании изменений hello шаблона tooonly емкостью можно включить только элемент SKU hello емкостью hello обновлены.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-120">If you are deploying a template tooonly change hello capacity, you can include only hello SKU element with hello updated capacity.</span></span>

<span data-ttu-id="9f1ab-121">Hello емкость набора масштабирования может автоматически настраиваться с помощью комбинации hello **autoscaleSettings** ресурсов и hello расширения диагностики.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-121">hello capacity of your scale set can be automatically adjusted by using a combination of hello **autoscaleSettings** resource and hello diagnostics extension.</span></span>

### <a name="configure-hello-azure-diagnostics-extension"></a><span data-ttu-id="9f1ab-122">Настройка расширения системы диагностики Azure hello</span><span class="sxs-lookup"><span data-stu-id="9f1ab-122">Configure hello Azure Diagnostics extension</span></span>
<span data-ttu-id="9f1ab-123">Автоматическое масштабирование может выполняться только при успешном выполнении на каждую виртуальную машину в наборе масштабирования hello коллекция метрик.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-123">Automatic scaling can only be done if metrics collection is successful on each virtual machine in hello scale set.</span></span> <span data-ttu-id="9f1ab-124">Hello расширения системы диагностики Azure предоставляет возможности мониторинга и диагностики hello, удовлетворяющих потребностям hello метрики коллекции hello автомасштабирования ресурса.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-124">hello Azure Diagnostics Extension provides hello monitoring and diagnostics capabilities that meets hello metrics collection needs of hello autoscale resource.</span></span> <span data-ttu-id="9f1ab-125">Hello расширения можно установить как часть шаблона диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-125">You can install hello extension as part of hello Resource Manager template.</span></span>

<span data-ttu-id="9f1ab-126">Этот пример показывает hello переменные, которые используются в расширения диагностики hello tooconfigure шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-126">This example shows hello variables that are used in hello template tooconfigure hello diagnostics extension:</span></span>

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

<span data-ttu-id="9f1ab-127">Параметры предоставляются при развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-127">Parameters are provided when hello template is deployed.</span></span> <span data-ttu-id="9f1ab-128">В этом примере hello имя учетной записи хранения hello (где хранятся данные) и hello предоставляются имя набора масштабирования hello (где данные собираются).</span><span class="sxs-lookup"><span data-stu-id="9f1ab-128">In this example, hello name of hello storage account (where data is stored) and hello name of hello scale set (where data is collected) are provided.</span></span> <span data-ttu-id="9f1ab-129">Также в этом примере Windows Server собираются только hello потока счетчик производительности.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-129">Also in this Windows Server example, only hello Thread Count performance counter is collected.</span></span> <span data-ttu-id="9f1ab-130">Здравствуйте, все доступные счетчики производительности в Windows или Linux, может быть сведения диагностики используется toocollect и может быть включено в конфигурации расширения hello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-130">All hello available performance counters in Windows or Linux can be used toocollect diagnostics information and can be included in hello extension configuration.</span></span>

<span data-ttu-id="9f1ab-131">В этом примере показано определение расширения hello hello в шаблоне hello:</span><span class="sxs-lookup"><span data-stu-id="9f1ab-131">This example shows hello definition of hello extension in hello template:</span></span>

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

<span data-ttu-id="9f1ab-132">При выполнении расширения диагностики hello hello данные хранятся и собираются в таблицу в учетной записи хранения hello, указываемое.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-132">When hello diagnostics extension runs, hello data is stored and collected in a table, in hello storage account that you specify.</span></span> <span data-ttu-id="9f1ab-133">В hello **WADPerformanceCounters** таблицы, можно найти hello собранных данных:</span><span class="sxs-lookup"><span data-stu-id="9f1ab-133">In hello **WADPerformanceCounters** table, you can find hello collected data:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a><span data-ttu-id="9f1ab-134">Настройка ресурсов autoScaleSettings hello</span><span class="sxs-lookup"><span data-stu-id="9f1ab-134">Configure hello autoScaleSettings resource</span></span>
<span data-ttu-id="9f1ab-135">Hello autoscaleSettings ресурсов использует hello сведения из toodecide расширения диагностики hello, установлены ли tooincrease или уменьшении hello количество виртуальных машин на шкале hello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-135">hello autoscaleSettings resource uses hello information from hello diagnostics extension toodecide whether tooincrease or decrease hello number of virtual machines in hello scale set.</span></span>

<span data-ttu-id="9f1ab-136">В этом примере показана конфигурация hello hello ресурса в шаблоне hello:</span><span class="sxs-lookup"><span data-stu-id="9f1ab-136">This example shows hello configuration of hello resource in hello template:</span></span>

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

<span data-ttu-id="9f1ab-137">В приведенном выше примере hello создаются два правила для определения действий автоматического масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-137">In hello example above, two rules are created for defining hello automatic scaling actions.</span></span> <span data-ttu-id="9f1ab-138">Первое правило Hello определяет действие масштабирования hello и hello второе правило определяет hello масштабирования в действие.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-138">hello first rule defines hello scale-out action and hello second rule defines hello scale-in action.</span></span> <span data-ttu-id="9f1ab-139">Эти значения указаны в правилах hello:</span><span class="sxs-lookup"><span data-stu-id="9f1ab-139">These values are provided in hello rules:</span></span>

| <span data-ttu-id="9f1ab-140">правило;</span><span class="sxs-lookup"><span data-stu-id="9f1ab-140">Rule</span></span> | <span data-ttu-id="9f1ab-141">Описание</span><span class="sxs-lookup"><span data-stu-id="9f1ab-141">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="9f1ab-142">metricName</span><span class="sxs-lookup"><span data-stu-id="9f1ab-142">metricName</span></span>        | <span data-ttu-id="9f1ab-143">Это значение является hello то же, что счетчик производительности hello, определенный в переменной wadperfcounter hello для расширения диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-143">This value is hello same as hello performance counter that you defined in hello wadperfcounter variable for hello diagnostics extension.</span></span> <span data-ttu-id="9f1ab-144">В приведенном выше примере hello используется hello счетчика потоков.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-144">In hello example above, hello Thread Count counter is used.</span></span>    |
| <span data-ttu-id="9f1ab-145">metricResourceUri</span><span class="sxs-lookup"><span data-stu-id="9f1ab-145">metricResourceUri</span></span> | <span data-ttu-id="9f1ab-146">Это значение является идентификатором ресурса hello hello набора масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-146">This value is hello resource identifier of hello virtual machine scale set.</span></span> <span data-ttu-id="9f1ab-147">Этот идентификатор содержит hello имя группы ресурсов hello, имя поставщика ресурсов hello hello и имя hello tooscale набор масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-147">This identifier contains hello name of hello resource group, hello name of hello resource provider, and hello name of hello scale set tooscale.</span></span> |
| <span data-ttu-id="9f1ab-148">timeGrain</span><span class="sxs-lookup"><span data-stu-id="9f1ab-148">timeGrain</span></span>         | <span data-ttu-id="9f1ab-149">Это значение является гранулярности hello hello метрик, которые собираются.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-149">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="9f1ab-150">В предыдущих пример hello данные собираются на интервал до одной минуты.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-150">In hello preceding example, data is collected on an interval of one minute.</span></span> <span data-ttu-id="9f1ab-151">Это значение используется вместе со значением timeWindow.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-151">This value is used with timeWindow.</span></span> |
| <span data-ttu-id="9f1ab-152">statistic</span><span class="sxs-lookup"><span data-stu-id="9f1ab-152">statistic</span></span>         | <span data-ttu-id="9f1ab-153">Это значение определяет, как метрики hello hello объединенный tooaccommodate автоматического масштабирования действия.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-153">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="9f1ab-154">Возможные значения Hello: Average, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-154">hello possible values are: Average, Min, Max.</span></span> |
| <span data-ttu-id="9f1ab-155">timeWindow</span><span class="sxs-lookup"><span data-stu-id="9f1ab-155">timeWindow</span></span>        | <span data-ttu-id="9f1ab-156">Это значение является hello диапазон времени, в котором собираются данные экземпляра.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-156">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="9f1ab-157">Значение должно составлять от 5 минут до 12 часов.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-157">It must be between 5 minutes and 12 hours.</span></span> |
| <span data-ttu-id="9f1ab-158">timeAggregation</span><span class="sxs-lookup"><span data-stu-id="9f1ab-158">timeAggregation</span></span>   | <span data-ttu-id="9f1ab-159">Это значение определяет способ объединения собираемых данных hello со временем.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-159">This value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="9f1ab-160">значение по умолчанию Hello — среднее значение.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-160">hello default value is Average.</span></span> <span data-ttu-id="9f1ab-161">Возможные значения Hello: среднее, минимальное, максимальное, конец, общее, число.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-161">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span> |
| <span data-ttu-id="9f1ab-162">operator</span><span class="sxs-lookup"><span data-stu-id="9f1ab-162">operator</span></span>          | <span data-ttu-id="9f1ab-163">Это значение является hello оператор, который используется toocompare hello метрики данных и hello порогового значения.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-163">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="9f1ab-164">Hello возможными значениями являются: равно NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-164">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span> |
| <span data-ttu-id="9f1ab-165">threshold</span><span class="sxs-lookup"><span data-stu-id="9f1ab-165">threshold</span></span>         | <span data-ttu-id="9f1ab-166">Это значение является hello значение, которое запускает действие масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-166">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="9f1ab-167">Быть достаточная разница между hello пороговые значения для hello убедиться, что tooprovide **масштабирования** и **масштабирования в** действия.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-167">Be sure tooprovide a sufficient difference between hello threshold values for hello **scale-out** and **scale-in** actions.</span></span> <span data-ttu-id="9f1ab-168">Если задать одинаковые значения для обоих этих действий hello hello системы можно предвидеть постоянное изменение, который препятствует его реализации действия масштабирования.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-168">If you set hello same values for both actions, hello system anticipates constant change, which prevents it from implementing a scaling action.</span></span> <span data-ttu-id="9f1ab-169">Например установка обоих too600 потоков в предшествующий пример hello не работает.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-169">For example, setting both too600 threads in hello preceding example doesn't work.</span></span> |
| <span data-ttu-id="9f1ab-170">direction</span><span class="sxs-lookup"><span data-stu-id="9f1ab-170">direction</span></span>         | <span data-ttu-id="9f1ab-171">Это значение определяет hello действие, которое предпринимается, когда достигается пороговое значение hello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-171">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="9f1ab-172">Возможные значения Hello: увеличиваются или уменьшаются.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-172">hello possible values are Increase or Decrease.</span></span> |
| <span data-ttu-id="9f1ab-173">type</span><span class="sxs-lookup"><span data-stu-id="9f1ab-173">type</span></span>              | <span data-ttu-id="9f1ab-174">Это значение является hello тип действия, которое должно выполняться и значением tooChangeCount.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-174">This value is hello type of action that should occur and must be set tooChangeCount.</span></span> |
| <span data-ttu-id="9f1ab-175">value</span><span class="sxs-lookup"><span data-stu-id="9f1ab-175">value</span></span>             | <span data-ttu-id="9f1ab-176">Это значение является hello число виртуальных машин, которые добавляются tooor удалены из набора масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-176">This value is hello number of virtual machines that are added tooor removed from hello scale set.</span></span> <span data-ttu-id="9f1ab-177">Для этого параметра должно быть указано значение не меньше 1.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-177">This value must be 1 or greater.</span></span> |
| <span data-ttu-id="9f1ab-178">cooldown</span><span class="sxs-lookup"><span data-stu-id="9f1ab-178">cooldown</span></span>          | <span data-ttu-id="9f1ab-179">Это значение является hello объем toowait времени с момента последнего действия масштабирования hello, прежде чем произойдет следующее действие hello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-179">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="9f1ab-180">Допустимые значения: от одной минуты до одной недели.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-180">This value must be between one minute and one week.</span></span> |

<span data-ttu-id="9f1ab-181">В зависимости от счетчика производительности hello вы используете, некоторые элементы hello в hello шаблона конфигурации используются по-разному.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-181">Depending on hello performance counter, you are using, some of hello elements in hello template configuration are used differently.</span></span> <span data-ttu-id="9f1ab-182">В предшествующих пример hello, hello счетчика производительности — число потоков, hello пороговое значение — 650 для действия масштабирования; hello пороговое значение — 550 для hello масштабирования в действие.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-182">In hello preceding example, hello performance counter is Thread Count, hello threshold value is 650 for a scale-out action, and hello threshold value is 550 for hello scale-in action.</span></span> <span data-ttu-id="9f1ab-183">При использовании счетчиков, такие как % загруженности процессора hello пороговое значение toohello процент использования ЦП, которое определяет действия масштабирования.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-183">If you use a counter such as %Processor Time, hello threshold value is set toohello percentage of CPU usage that determines a scaling action.</span></span>

<span data-ttu-id="9f1ab-184">При запуске действия масштабирования, например высокой нагрузки, емкость hello hello набора увеличивается на основе значения hello в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-184">When a scaling action is triggered, such as a high load, hello capacity of hello set is increased based on hello value in hello template.</span></span> <span data-ttu-id="9f1ab-185">Например на шкале задать где заданная too3 емкость hello, а значение действия масштабирования hello равно too1:</span><span class="sxs-lookup"><span data-stu-id="9f1ab-185">For example, in a scale set where hello capacity is set too3 and hello scale action value is set too1:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

<span data-ttu-id="9f1ab-186">Когда hello текущей нагрузки причины hello потока среднее число toogo выше порогового значения hello объекта 650:</span><span class="sxs-lookup"><span data-stu-id="9f1ab-186">When hello current load causes hello average thread count toogo above hello threshold of 650:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

<span data-ttu-id="9f1ab-187">Объект **масштабирования** выполняется действие, причины hello емкость toobe набор hello увеличено на 1:</span><span class="sxs-lookup"><span data-stu-id="9f1ab-187">A **scale-out** action is triggered that causes hello capacity of hello set toobe increased by one:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

<span data-ttu-id="9f1ab-188">результат Hello — добавлении toohello набор масштабирования виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="9f1ab-188">hello result is a virtual machine is added toohello scale set:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

<span data-ttu-id="9f1ab-189">После периода cooldown пять минут Если hello среднее число потоков на машинах hello остается более 600 другой компьютер добавляется набор toohello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-189">After a cooldown period of five minutes, if hello average number of threads on hello machines stays over 600, another machine is added toohello set.</span></span> <span data-ttu-id="9f1ab-190">Если hello потока среднее количество остается ниже 550, hello емкость набора масштабирования hello уменьшается на единицу и машина будет удалена из набора hello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-190">If hello average thread count stays below 550, hello capacity of hello scale set is reduced by one and a machine is removed from hello set.</span></span>

## <a name="set-up-scaling-using-azure-powershell"></a><span data-ttu-id="9f1ab-191">Настройка масштабирования с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f1ab-191">Set up scaling using Azure PowerShell</span></span>

<span data-ttu-id="9f1ab-192">Просмотрите примеры использования PowerShell tooset копирование автоматическое масштабирование, toosee [монитор Azure PowerShell быстрый запуск образцов](../monitoring-and-diagnostics/insights-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9f1ab-192">toosee examples of using PowerShell tooset up autoscaling, look at [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span></span>

## <a name="set-up-scaling-using-azure-cli"></a><span data-ttu-id="9f1ab-193">Настройка масштабирования с помощью интерфейса командной строки Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="9f1ab-193">Set up scaling using Azure CLI</span></span>

<span data-ttu-id="9f1ab-194">Просмотрите примеры использования Azure CLI tooset копирование автоматическое масштабирование, toosee [монитора Azure кросс платформенных CLI быстрый запуск образцов](../monitoring-and-diagnostics/insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9f1ab-194">toosee examples of using Azure CLI tooset up autoscaling, look at [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md).</span></span>

## <a name="set-up-scaling-using-hello-azure-portal"></a><span data-ttu-id="9f1ab-195">Настройка масштабирования с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="9f1ab-195">Set up scaling using hello Azure portal</span></span>

<span data-ttu-id="9f1ab-196">Пример использования toosee hello Azure портала tooset копирование автоматическое масштабирование, просмотрите в [создания набора масштабирования виртуальных машин с помощью портала Azure hello](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="9f1ab-196">toosee an example of using hello Azure portal tooset up autoscaling, look at [Create a Virtual Machine Scale Set using hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="investigate-scaling-actions"></a><span data-ttu-id="9f1ab-197">Изучение действий масштабирования</span><span class="sxs-lookup"><span data-stu-id="9f1ab-197">Investigate scaling actions</span></span>

* <span data-ttu-id="9f1ab-198">**Портал Azure**</span><span class="sxs-lookup"><span data-stu-id="9f1ab-198">**Azure portal**</span></span>  
<span data-ttu-id="9f1ab-199">В настоящее время можно получить ограниченный объем информации с помощью портала hello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-199">You can currently get a limited amount of information using hello portal.</span></span>

* <span data-ttu-id="9f1ab-200">**Azure Resource Explorer**</span><span class="sxs-lookup"><span data-stu-id="9f1ab-200">**Azure Resource Explorer**</span></span>  
<span data-ttu-id="9f1ab-201">Это средство — hello, наилучшим образом подходит для изучения hello текущее состояние набора масштабирования.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-201">This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="9f1ab-202">Выполните этот путь, и вы увидите набор, созданный представление экземпляра hello hello шкалы:</span><span class="sxs-lookup"><span data-stu-id="9f1ab-202">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>  
<span data-ttu-id="9f1ab-203">**Subscriptions > {ваша подписка} > resourceGroups > {ваша группа ресурсов} > providers > Microsoft.Compute > virtualMachineScaleSets > {ваш масштабируемый набор} > virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="9f1ab-203">**Subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Compute > virtualMachineScaleSets > {your scale set} > virtualMachines**</span></span>

* <span data-ttu-id="9f1ab-204">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="9f1ab-204">**Azure PowerShell**</span></span>  
<span data-ttu-id="9f1ab-205">С помощью этой команды tooget некоторые данные.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-205">Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* <span data-ttu-id="9f1ab-206">Подключение toohello jumpbox виртуальной машины, так же, как и любой другой компьютер и затем позволяет осуществлять удаленный доступ hello виртуальных машин в отдельных процессах набор масштабирования toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-206">Connect toohello jumpbox virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f1ab-207">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9f1ab-207">Next Steps</span></span>
* <span data-ttu-id="9f1ab-208">Посмотрите на [автоматически масштабировать машины в наборе масштабирования виртуальных машин](virtual-machine-scale-sets-windows-autoscale.md) toosee примером как toocreate шкале задать настройки автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="9f1ab-208">Look at [Automatically scale machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-autoscale.md) toosee an example of how toocreate a scale set with automatic scaling configured.</span></span>

* <span data-ttu-id="9f1ab-209">Просмотрите примеры функций мониторинга Azure Monitor в статье [Примеры для быстрого запуска Azure Insights с помощью PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9f1ab-209">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>

* <span data-ttu-id="9f1ab-210">Дополнительные сведения о функции уведомлений в [используйте автомасштабирования действия toosend электронной почты и веб-перехватчика уведомлений о предупреждениях в мониторе Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="9f1ab-210">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span></span>

* <span data-ttu-id="9f1ab-211">Дополнительные сведения о слишком[журналы аудита используйте toosend электронной почты и веб-перехватчика уведомлений о предупреждениях в мониторе Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="9f1ab-211">Learn about how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

* <span data-ttu-id="9f1ab-212">Узнайте больше о [расширенных сценариях автомасштабирования](virtual-machine-scale-sets-advanced-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="9f1ab-212">Learn about [advanced autoscale scenarios](virtual-machine-scale-sets-advanced-autoscale.md).</span></span>
