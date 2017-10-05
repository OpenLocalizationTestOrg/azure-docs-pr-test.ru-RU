---
title: "Автомасштабирование и масштабируемые наборы виртуальных машин | Документация Майкрософт"
description: "Узнайте о том, как использовать диагностику и ресурсы автоматического масштабирования для автоматического масштабирования виртуальных машин в наборе масштабирования."
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
ms.openlocfilehash: 06ff9d9ae1dd8256f0d22c1a60ed6a85554f1f17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-automatic-scaling-and-virtual-machine-scale-sets"></a><span data-ttu-id="4307f-103">Как использовать автомасштабирование и масштабируемые наборы виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="4307f-103">How to use automatic scaling and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="4307f-104">Автоматическое масштабирование виртуальных машин (ВМ) в наборе масштабирования — это процесс создания или удаления входящих в набор ВМ в соответствии требованиями к производительности.</span><span class="sxs-lookup"><span data-stu-id="4307f-104">Automatic scaling of virtual machines in a scale set is the creation or deletion of machines in the set as needed to match performance requirements.</span></span> <span data-ttu-id="4307f-105">По мере роста рабочей нагрузки для эффективного выполнения задач приложению могут потребоваться дополнительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="4307f-105">As the volume of work grows, an application may require additional resources to enable it to effectively perform tasks.</span></span>

<span data-ttu-id="4307f-106">Автоматическое масштабирование — это автоматизированный процесс, который помогает упростить управление ресурсами.</span><span class="sxs-lookup"><span data-stu-id="4307f-106">Automatic scaling is an automated process that helps ease management overhead.</span></span> <span data-ttu-id="4307f-107">Вы сможете снизить издержки, и при этом не вам не нужно постоянно отслеживать производительность системы или решать, как управлять ресурсами.</span><span class="sxs-lookup"><span data-stu-id="4307f-107">By reducing overhead, you don't need to continually monitor system performance or decide how to manage resources.</span></span> <span data-ttu-id="4307f-108">Масштабирование — это эластичный процесс.</span><span class="sxs-lookup"><span data-stu-id="4307f-108">Scaling is an elastic process.</span></span> <span data-ttu-id="4307f-109">По мере увеличения нагрузки можно добавлять дополнительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="4307f-109">More resources can be added as the load increases.</span></span> <span data-ttu-id="4307f-110">При уменьшении потребностей ресурсы можно удалять, что позволяет снизить затраты при сохранении требуемой производительности.</span><span class="sxs-lookup"><span data-stu-id="4307f-110">And as demand decreases, resources can be removed to minimize costs and maintain performance levels.</span></span>

<span data-ttu-id="4307f-111">Настроить автоматическое масштабирование набора ресурсов можно с помощью шаблона Azure Resource Manager, с помощью Azure PowerShell, интерфейса командной строки Azure или портала Azure.</span><span class="sxs-lookup"><span data-stu-id="4307f-111">Set up automatic scaling on a scale set by using an Azure Resource Manager template, Azure PowerShell, Azure CLI, or the Azure portal.</span></span>

## <a name="set-up-scaling-by-using-resource-manager-templates"></a><span data-ttu-id="4307f-112">Настройка масштабирования с помощью шаблонов Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4307f-112">Set up scaling by using Resource Manager templates</span></span>
<span data-ttu-id="4307f-113">Чтобы не развертывать (с последующим управлением) каждый ресурс для приложения по отдельности, вы можете создать шаблон Azure Resource Manager, который развертывает все нужные ресурсы в ходе одной скоординированной операции.</span><span class="sxs-lookup"><span data-stu-id="4307f-113">Rather than deploying and managing each resource of your application separately, use a template that deploys all resources in a single, coordinated operation.</span></span> <span data-ttu-id="4307f-114">В шаблоне определяются ресурсы приложения и указываются параметры развертывания для разных сред.</span><span class="sxs-lookup"><span data-stu-id="4307f-114">In the template, application resources are defined and deployment parameters are specified for different environments.</span></span> <span data-ttu-id="4307f-115">Шаблон состоит из JSON и выражений, на основе которых можно создавать значения для развертывания.</span><span class="sxs-lookup"><span data-stu-id="4307f-115">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="4307f-116">Узнайте больше о [создании шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4307f-116">To learn more, look at [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="4307f-117">В шаблоне необходимо указать элемент capacity.</span><span class="sxs-lookup"><span data-stu-id="4307f-117">In the template, you specify the capacity element:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

<span data-ttu-id="4307f-118">Элемент capacity определяет количество виртуальных машин в наборе.</span><span class="sxs-lookup"><span data-stu-id="4307f-118">Capacity identifies the number of virtual machines in the set.</span></span> <span data-ttu-id="4307f-119">Вы можете вручную изменить значение этого параметра, развернув шаблон с новым значением.</span><span class="sxs-lookup"><span data-stu-id="4307f-119">You can manually change the capacity by deploying a template with a different value.</span></span> <span data-ttu-id="4307f-120">Если вы развертываете шаблон только для изменения емкости набора, вам достаточно включить в шаблон только элемент SKU с новым значением capacity.</span><span class="sxs-lookup"><span data-stu-id="4307f-120">If you are deploying a template to only change the capacity, you can include only the SKU element with the updated capacity.</span></span>

<span data-ttu-id="4307f-121">Вы можете автоматически изменять емкость масштабируемого набора, используя ресурс **autoscaleSettings** и расширение системы диагностики.</span><span class="sxs-lookup"><span data-stu-id="4307f-121">The capacity of your scale set can be automatically adjusted by using a combination of the **autoscaleSettings** resource and the diagnostics extension.</span></span>

### <a name="configure-the-azure-diagnostics-extension"></a><span data-ttu-id="4307f-122">Настройка расширения системы диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="4307f-122">Configure the Azure Diagnostics extension</span></span>
<span data-ttu-id="4307f-123">Автоматическое масштабирование выполняется, только если для каждой виртуальной машины из масштабируемого набора собираются метрики.</span><span class="sxs-lookup"><span data-stu-id="4307f-123">Automatic scaling can only be done if metrics collection is successful on each virtual machine in the scale set.</span></span> <span data-ttu-id="4307f-124">Расширение системы диагностики Azure предусматривает возможности для мониторинга и диагностики, необходимые для автоматического масштабирования ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4307f-124">The Azure Diagnostics Extension provides the monitoring and diagnostics capabilities that meets the metrics collection needs of the autoscale resource.</span></span> <span data-ttu-id="4307f-125">Расширение можно установить в составе шаблона Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4307f-125">You can install the extension as part of the Resource Manager template.</span></span>

<span data-ttu-id="4307f-126">В следующем примере показано использование переменных в шаблоне для настройки расширения диагностики.</span><span class="sxs-lookup"><span data-stu-id="4307f-126">This example shows the variables that are used in the template to configure the diagnostics extension:</span></span>

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

<span data-ttu-id="4307f-127">Параметры предоставляются при развертывании шаблона.</span><span class="sxs-lookup"><span data-stu-id="4307f-127">Parameters are provided when the template is deployed.</span></span> <span data-ttu-id="4307f-128">В нашем примере это имя учетной записи хранения, в которой будут сохраняться данные, и имя масштабируемого набора, из которого нужно собирать данные.</span><span class="sxs-lookup"><span data-stu-id="4307f-128">In this example, the name of the storage account (where data is stored) and the name of the scale set (where data is collected) are provided.</span></span> <span data-ttu-id="4307f-129">В этом примере для Windows Server собираются только данные счетчика производительности (счетчика потоков).</span><span class="sxs-lookup"><span data-stu-id="4307f-129">Also in this Windows Server example, only the Thread Count performance counter is collected.</span></span> <span data-ttu-id="4307f-130">Для сбора диагностической информации можно включать в настройки расширения любые счетчики производительности, доступные в среде Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="4307f-130">All the available performance counters in Windows or Linux can be used to collect diagnostics information and can be included in the extension configuration.</span></span>

<span data-ttu-id="4307f-131">В этом примере показано определение расширения в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="4307f-131">This example shows the definition of the extension in the template:</span></span>

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

<span data-ttu-id="4307f-132">Когда выполняется расширение системы диагностики, данные собираются и сохраняются в таблице, которая расположена в указанной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="4307f-132">When the diagnostics extension runs, the data is stored and collected in a table, in the storage account that you specify.</span></span> <span data-ttu-id="4307f-133">Собранные данные помещаются в таблицу **WADPerformanceCounters**.</span><span class="sxs-lookup"><span data-stu-id="4307f-133">In the **WADPerformanceCounters** table, you can find the collected data:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-the-autoscalesettings-resource"></a><span data-ttu-id="4307f-134">Настройка ресурса autoScaleSettings</span><span class="sxs-lookup"><span data-stu-id="4307f-134">Configure the autoScaleSettings resource</span></span>
<span data-ttu-id="4307f-135">Ресурс AutoscaleSettings использует данные, собранные расширением системы диагностики, для принятия решений об увеличении или уменьшении числа ВМ в наборе масштабирования.</span><span class="sxs-lookup"><span data-stu-id="4307f-135">The autoscaleSettings resource uses the information from the diagnostics extension to decide whether to increase or decrease the number of virtual machines in the scale set.</span></span>

<span data-ttu-id="4307f-136">В этом примере показана конфигурация ресурса в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="4307f-136">This example shows the configuration of the resource in the template:</span></span>

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

<span data-ttu-id="4307f-137">В приведенном выше примере создаются два правила, определяющие действия автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="4307f-137">In the example above, two rules are created for defining the automatic scaling actions.</span></span> <span data-ttu-id="4307f-138">Первое правило определяет действие по увеличению масштаба, а второе — по его уменьшению.</span><span class="sxs-lookup"><span data-stu-id="4307f-138">The first rule defines the scale-out action and the second rule defines the scale-in action.</span></span> <span data-ttu-id="4307f-139">Для этих правил указаны значения следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="4307f-139">These values are provided in the rules:</span></span>

| <span data-ttu-id="4307f-140">правило;</span><span class="sxs-lookup"><span data-stu-id="4307f-140">Rule</span></span> | <span data-ttu-id="4307f-141">Описание</span><span class="sxs-lookup"><span data-stu-id="4307f-141">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="4307f-142">metricName</span><span class="sxs-lookup"><span data-stu-id="4307f-142">metricName</span></span>        | <span data-ttu-id="4307f-143">Здесь должно быть указано имя счетчика производительности, который вы указали в переменной wadperfcounter для расширения диагностики.</span><span class="sxs-lookup"><span data-stu-id="4307f-143">This value is the same as the performance counter that you defined in the wadperfcounter variable for the diagnostics extension.</span></span> <span data-ttu-id="4307f-144">В нашем примере это счетчик потоков (Thread Count).</span><span class="sxs-lookup"><span data-stu-id="4307f-144">In the example above, the Thread Count counter is used.</span></span>    |
| <span data-ttu-id="4307f-145">metricResourceUri</span><span class="sxs-lookup"><span data-stu-id="4307f-145">metricResourceUri</span></span> | <span data-ttu-id="4307f-146">В этом параметре указывается идентификатор ресурса масштабируемого набора виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="4307f-146">This value is the resource identifier of the virtual machine scale set.</span></span> <span data-ttu-id="4307f-147">Этот идентификатор содержит имя группы ресурсов, имя поставщика ресурсов и имя набора, который мы будем масштабировать.</span><span class="sxs-lookup"><span data-stu-id="4307f-147">This identifier contains the name of the resource group, the name of the resource provider, and the name of the scale set to scale.</span></span> |
| <span data-ttu-id="4307f-148">timeGrain</span><span class="sxs-lookup"><span data-stu-id="4307f-148">timeGrain</span></span>         | <span data-ttu-id="4307f-149">В этом параметре указывается степень детализации собираемых метрик.</span><span class="sxs-lookup"><span data-stu-id="4307f-149">This value is the granularity of the metrics that are collected.</span></span> <span data-ttu-id="4307f-150">В приведенном выше примере данные собираются с интервалами в одну минуту.</span><span class="sxs-lookup"><span data-stu-id="4307f-150">In the preceding example, data is collected on an interval of one minute.</span></span> <span data-ttu-id="4307f-151">Это значение используется вместе со значением timeWindow.</span><span class="sxs-lookup"><span data-stu-id="4307f-151">This value is used with timeWindow.</span></span> |
| <span data-ttu-id="4307f-152">statistic</span><span class="sxs-lookup"><span data-stu-id="4307f-152">statistic</span></span>         | <span data-ttu-id="4307f-153">Этот параметр определяет, как объединяются метрики для автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="4307f-153">This value determines how the metrics are combined to accommodate the automatic scaling action.</span></span> <span data-ttu-id="4307f-154">Возможные значения: Average (Среднее), Min (Минимальное), Max (Максимальное).</span><span class="sxs-lookup"><span data-stu-id="4307f-154">The possible values are: Average, Min, Max.</span></span> |
| <span data-ttu-id="4307f-155">timeWindow</span><span class="sxs-lookup"><span data-stu-id="4307f-155">timeWindow</span></span>        | <span data-ttu-id="4307f-156">В этом параметре указывается интервал, в пределах которого собираются данные об экземплярах.</span><span class="sxs-lookup"><span data-stu-id="4307f-156">This value is the range of time in which instance data is collected.</span></span> <span data-ttu-id="4307f-157">Значение должно составлять от 5 минут до 12 часов.</span><span class="sxs-lookup"><span data-stu-id="4307f-157">It must be between 5 minutes and 12 hours.</span></span> |
| <span data-ttu-id="4307f-158">timeAggregation</span><span class="sxs-lookup"><span data-stu-id="4307f-158">timeAggregation</span></span>   | <span data-ttu-id="4307f-159">Этот параметр определяет способ объединения собранных данных с течением времени.</span><span class="sxs-lookup"><span data-stu-id="4307f-159">This value determines how the data that is collected should be combined over time.</span></span> <span data-ttu-id="4307f-160">Значение по умолчанию — Average (Среднее).</span><span class="sxs-lookup"><span data-stu-id="4307f-160">The default value is Average.</span></span> <span data-ttu-id="4307f-161">Возможные значения: Average (Среднее), Minimum (Минимальное), Maximum (Максимальное), Last (Последнее), Total (Всего), Count (Количество).</span><span class="sxs-lookup"><span data-stu-id="4307f-161">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span> |
| <span data-ttu-id="4307f-162">operator</span><span class="sxs-lookup"><span data-stu-id="4307f-162">operator</span></span>          | <span data-ttu-id="4307f-163">Оператор, который используется для сравнения данных метрики с пороговым значением.</span><span class="sxs-lookup"><span data-stu-id="4307f-163">This value is the operator that is used to compare the metric data and the threshold.</span></span> <span data-ttu-id="4307f-164">Возможные значения: Equals (Равно), NotEquals (Не равно), GreaterThan (Больше), GreaterThanOrEqual (Больше или равно), LessThan (Меньше), LessThanOrEqual (Меньше или равно).</span><span class="sxs-lookup"><span data-stu-id="4307f-164">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span> |
| <span data-ttu-id="4307f-165">threshold</span><span class="sxs-lookup"><span data-stu-id="4307f-165">threshold</span></span>         | <span data-ttu-id="4307f-166">Значение этого параметра активирует действие масштабирования.</span><span class="sxs-lookup"><span data-stu-id="4307f-166">This value is the value that triggers the scale action.</span></span> <span data-ttu-id="4307f-167">Между пороговыми значениями, которые вы укажете для операций **увеличения** и **уменьшения масштаба**, должна быть достаточно большая разница.</span><span class="sxs-lookup"><span data-stu-id="4307f-167">Be sure to provide a sufficient difference between the threshold values for the **scale-out** and **scale-in** actions.</span></span> <span data-ttu-id="4307f-168">Если вы укажете для них одинаковые значения, то система будет постоянно ожидать изменений. В итоге действия масштабирования выполнены не будут.</span><span class="sxs-lookup"><span data-stu-id="4307f-168">If you set the same values for both actions, the system anticipates constant change, which prevents it from implementing a scaling action.</span></span> <span data-ttu-id="4307f-169">Например, если в предыдущем примере для двух параметров указать значение 600, масштабирование не будет выполнено.</span><span class="sxs-lookup"><span data-stu-id="4307f-169">For example, setting both to 600 threads in the preceding example doesn't work.</span></span> |
| <span data-ttu-id="4307f-170">direction</span><span class="sxs-lookup"><span data-stu-id="4307f-170">direction</span></span>         | <span data-ttu-id="4307f-171">Этот параметр определяет действие, которое запускается при достижении порогового значения.</span><span class="sxs-lookup"><span data-stu-id="4307f-171">This value determines the action that is taken when the threshold value is achieved.</span></span> <span data-ttu-id="4307f-172">Допустимые значения: Increase (Увеличить) или Decrease (Уменьшить).</span><span class="sxs-lookup"><span data-stu-id="4307f-172">The possible values are Increase or Decrease.</span></span> |
| <span data-ttu-id="4307f-173">Тип</span><span class="sxs-lookup"><span data-stu-id="4307f-173">type</span></span>              | <span data-ttu-id="4307f-174">В этом параметре указывается тип действия, которое должно выполняться. Для этого параметра должно быть установлено значение ChangeCount.</span><span class="sxs-lookup"><span data-stu-id="4307f-174">This value is the type of action that should occur and must be set to ChangeCount.</span></span> |
| <span data-ttu-id="4307f-175">value</span><span class="sxs-lookup"><span data-stu-id="4307f-175">value</span></span>             | <span data-ttu-id="4307f-176">Это число виртуальных машин, которые добавляются в масштабируемый набор или удаляются из него.</span><span class="sxs-lookup"><span data-stu-id="4307f-176">This value is the number of virtual machines that are added to or removed from the scale set.</span></span> <span data-ttu-id="4307f-177">Для этого параметра должно быть указано значение не меньше 1.</span><span class="sxs-lookup"><span data-stu-id="4307f-177">This value must be 1 or greater.</span></span> |
| <span data-ttu-id="4307f-178">cooldown</span><span class="sxs-lookup"><span data-stu-id="4307f-178">cooldown</span></span>          | <span data-ttu-id="4307f-179">В этом параметре указывается время ожидания с момента выполнения последнего действия масштабирования до начала следующего.</span><span class="sxs-lookup"><span data-stu-id="4307f-179">This value is the amount of time to wait since the last scaling action before the next action occurs.</span></span> <span data-ttu-id="4307f-180">Допустимые значения: от одной минуты до одной недели.</span><span class="sxs-lookup"><span data-stu-id="4307f-180">This value must be between one minute and one week.</span></span> |

<span data-ttu-id="4307f-181">В зависимости от выбранного счетчика производительности некоторые элементы в шаблоне конфигурации используются иначе.</span><span class="sxs-lookup"><span data-stu-id="4307f-181">Depending on the performance counter, you are using, some of the elements in the template configuration are used differently.</span></span> <span data-ttu-id="4307f-182">В приведенном примере в качестве счетчика производительности используется счетчик потоков. Установлено пороговое значение 650 для увеличения масштаба и 550 для уменьшения масштаба.</span><span class="sxs-lookup"><span data-stu-id="4307f-182">In the preceding example, the performance counter is Thread Count, the threshold value is 650 for a scale-out action, and the threshold value is 550 for the scale-in action.</span></span> <span data-ttu-id="4307f-183">Если вы будете использовать такие счетчики, как загруженность процессора в процентах, пороговое значение для действия масштабирования следует указать в процентах.</span><span class="sxs-lookup"><span data-stu-id="4307f-183">If you use a counter such as %Processor Time, the threshold value is set to the percentage of CPU usage that determines a scaling action.</span></span>

<span data-ttu-id="4307f-184">Когда активируется действие масштабирования, например при высокой нагрузке, емкость набора увеличивается в соответствии с параметром value, заданным в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="4307f-184">When a scaling action is triggered, such as a high load, the capacity of the set is increased based on the value in the template.</span></span> <span data-ttu-id="4307f-185">Рассмотрим пример, в котором для масштабируемого набора параметр capacity имеет значение 3, а параметр value для действия имеет значение 1.</span><span class="sxs-lookup"><span data-stu-id="4307f-185">For example, in a scale set where the capacity is set to 3 and the scale action value is set to 1:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

<span data-ttu-id="4307f-186">Предположим, текущая нагрузка приводит к повышению среднего количества потоков выше порогового значения 650.</span><span class="sxs-lookup"><span data-stu-id="4307f-186">When the current load causes the average thread count to go above the threshold of 650:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

<span data-ttu-id="4307f-187">Активируется действие **увеличения масштаба**: емкость набора увеличивается на единицу.</span><span class="sxs-lookup"><span data-stu-id="4307f-187">A **scale-out** action is triggered that causes the capacity of the set to be increased by one:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

<span data-ttu-id="4307f-188">В результате этого в масштабируемый набор добавляется виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="4307f-188">The result is a virtual machine is added to the scale set:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

<span data-ttu-id="4307f-189">Если по истечении периода ожидания (параметр cooldown) среднее количество потоков остается выше 600, в набор добавляется еще один компьютер.</span><span class="sxs-lookup"><span data-stu-id="4307f-189">After a cooldown period of five minutes, if the average number of threads on the machines stays over 600, another machine is added to the set.</span></span> <span data-ttu-id="4307f-190">Если среднее число потоков окажется ниже 550, размер масштабируемого набора уменьшается на единицу и один компьютер удаляется из набора.</span><span class="sxs-lookup"><span data-stu-id="4307f-190">If the average thread count stays below 550, the capacity of the scale set is reduced by one and a machine is removed from the set.</span></span>

## <a name="set-up-scaling-using-azure-powershell"></a><span data-ttu-id="4307f-191">Настройка масштабирования с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4307f-191">Set up scaling using Azure PowerShell</span></span>

<span data-ttu-id="4307f-192">Примеры использования PowerShell для настройки автоматического масштабирования см. в статье [Примеры для быстрого запуска Azure Insights с помощью PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4307f-192">To see examples of using PowerShell to set up autoscaling, look at [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span></span>

## <a name="set-up-scaling-using-azure-cli"></a><span data-ttu-id="4307f-193">Настройка масштабирования с помощью интерфейса командной строки Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="4307f-193">Set up scaling using Azure CLI</span></span>

<span data-ttu-id="4307f-194">Примеры использования интерфейса командной строки Azure для настройки автоматического масштабирования см. в статье [Примеры команд для межплатформенного интерфейса командной строки Azure Insights](../monitoring-and-diagnostics/insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4307f-194">To see examples of using Azure CLI to set up autoscaling, look at [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md).</span></span>

## <a name="set-up-scaling-using-the-azure-portal"></a><span data-ttu-id="4307f-195">Настройка масштабирования с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="4307f-195">Set up scaling using the Azure portal</span></span>

<span data-ttu-id="4307f-196">Примеры использования портала Azure для настройки автоматического масштабирования, см. в статье [Создание набора масштабирования с помощью портала Azure](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="4307f-196">To see an example of using the Azure portal to set up autoscaling, look at [Create a Virtual Machine Scale Set using the Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="investigate-scaling-actions"></a><span data-ttu-id="4307f-197">Изучение действий масштабирования</span><span class="sxs-lookup"><span data-stu-id="4307f-197">Investigate scaling actions</span></span>

* <span data-ttu-id="4307f-198">**Портал Azure**</span><span class="sxs-lookup"><span data-stu-id="4307f-198">**Azure portal**</span></span>  
<span data-ttu-id="4307f-199">Сейчас с помощью портала можно получить ограниченный объем сведений.</span><span class="sxs-lookup"><span data-stu-id="4307f-199">You can currently get a limited amount of information using the portal.</span></span>

* <span data-ttu-id="4307f-200">**Azure Resource Explorer**</span><span class="sxs-lookup"><span data-stu-id="4307f-200">**Azure Resource Explorer**</span></span>  
<span data-ttu-id="4307f-201">Это лучший инструмент для просмотра текущего состояния масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="4307f-201">This tool is the best for exploring the current state of your scale set.</span></span> <span data-ttu-id="4307f-202">Используйте этот путь, чтобы увидеть представление экземпляра созданного масштабируемого набора:</span><span class="sxs-lookup"><span data-stu-id="4307f-202">Follow this path and you should see the instance view of the scale set that you created:</span></span>  
<span data-ttu-id="4307f-203">**Subscriptions > {ваша подписка} > resourceGroups > {ваша группа ресурсов} > providers > Microsoft.Compute > virtualMachineScaleSets > {ваш масштабируемый набор} > virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="4307f-203">**Subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Compute > virtualMachineScaleSets > {your scale set} > virtualMachines**</span></span>

* <span data-ttu-id="4307f-204">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="4307f-204">**Azure PowerShell**</span></span>  
<span data-ttu-id="4307f-205">Используйте приведенную ниже команду, чтобы получить информацию.</span><span class="sxs-lookup"><span data-stu-id="4307f-205">Use this command to get some information:</span></span>

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* <span data-ttu-id="4307f-206">Подключитесь к основной виртуальной машине так же, как к любому другому компьютеру. Теперь вы сможете удаленно подключаться к виртуальным машинам в масштабируемом наборе, чтобы отслеживать отдельные процессы.</span><span class="sxs-lookup"><span data-stu-id="4307f-206">Connect to the jumpbox virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4307f-207">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4307f-207">Next Steps</span></span>
* <span data-ttu-id="4307f-208">Ознакомьтесь с примером того, как можно создать набор с настроенным автоматическим масштабированием, в статье [Автоматическое масштабирование машин в масштабируемом наборе виртуальных машин](virtual-machine-scale-sets-windows-autoscale.md) .</span><span class="sxs-lookup"><span data-stu-id="4307f-208">Look at [Automatically scale machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-autoscale.md) to see an example of how to create a scale set with automatic scaling configured.</span></span>

* <span data-ttu-id="4307f-209">Просмотрите примеры функций мониторинга Azure Monitor в статье [Примеры для быстрого запуска Azure Insights с помощью PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4307f-209">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>

* <span data-ttu-id="4307f-210">Узнайте о возможностях уведомлений в статье [Использование действий автомасштабирования для отправки электронной почты и уведомлений об оповещениях веб-перехватчика в Azure Insights](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="4307f-210">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span></span>

* <span data-ttu-id="4307f-211">Узнайте, как [использовать журналы аудита для отправки электронной почты и уведомлений об оповещениях веб-перехватчика в Azure Insights](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="4307f-211">Learn about how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

* <span data-ttu-id="4307f-212">Узнайте больше о [расширенных сценариях автомасштабирования](virtual-machine-scale-sets-advanced-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="4307f-212">Learn about [advanced autoscale scenarios](virtual-machine-scale-sets-advanced-autoscale.md).</span></span>
