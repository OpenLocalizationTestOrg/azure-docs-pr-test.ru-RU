---
title: "Добавление средств мониторинга и диагностики в виртуальную машину Azure | Документация Майкрософт"
description: "Используйте шаблон диспетчера ресурсов Azure, чтобы создать виртуальную машину Windows с помощью расширения системы диагностики Azure."
services: virtual-machines-windows
documentationcenter: 
author: sbtron
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8cde8fe7-977b-43d2-be74-ad46dc946058
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: saurabh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6955e3d8c7b032ee898be11e611080905b5069ba
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="use-monitoring-and-diagnostics-with-a-windows-vm-and-azure-resource-manager-templates"></a>Использование мониторинга и системы диагностики с виртуальной машиной Windows и шаблонами Azure Resource Manager
Расширение системы диагностики Azure позволяет использовать возможности мониторинга и диагностики в виртуальной машине Azure под управлением Windows. Чтобы использовать эти возможности на виртуальной машине, необходимо включить расширение в шаблон диспетчера ресурсов Azure. Дополнительные сведения о включении любого расширения в шаблон виртуальной машины см. в статье [Создание шаблонов диспетчера ресурсов Azure с расширениями виртуальных машин](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions). В этой статье описывается, как добавить расширение системы диагностики Azure в шаблон виртуальной машины Windows.  

## <a name="add-the-azure-diagnostics-extension-to-the-vm-resource-definition"></a>Добавление расширения системы диагностики Azure в определения ресурсов виртуальной машины
Чтобы использовать расширение системы диагностики в виртуальной машине Windows, необходимо добавить его в шаблон диспетчера ресурсов в качестве ресурса виртуальной машины.

Для простой виртуальной машины на основе диспетчера ресурсов добавьте конфигурацию расширения в массив *resources* для соответствующей виртуальной машины: 

    "resources": [
                {
                    "name": "Microsoft.Insights.VMDiagnosticsSettings",
                    "type": "extensions",
                    "location": "[resourceGroup().location]",
                    "apiVersion": "2015-06-15",
                    "dependsOn": [
                        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
                    ],
                    "tags": {
                        "displayName": "AzureDiagnostics"
                    },
                    "properties": {
                        "publisher": "Microsoft.Azure.Diagnostics",
                        "type": "IaaSDiagnostics",
                        "typeHandlerVersion": "1.5",
                        "autoUpgradeMinorVersion": true,
                        "settings": {
                            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
                            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
                        },
                        "protectedSettings": {
                            "storageAccountName": "[parameters('existingdiagnosticsStorageAccountName')]",
                            "storageAccountKey": "[listkeys(variables('accountid'), '2015-05-01-preview').key1]",
                            "storageAccountEndPoint": "https://core.windows.net"
                        }
                    }
                }
            ]


Другой распространенный способ — добавить конфигурацию расширения в корневой узел ресурсов шаблона, не определяя ее в узле ресурсов виртуальной машины. При таком подходе необходимо явно указать иерархические связи между расширением и виртуальной машиной с помощью значений *name* и *type*. Например: 

    "name": "[concat(variables('vmName'),'Microsoft.Insights.VMDiagnosticsSettings')]",
    "type": "Microsoft.Compute/virtualMachines/extensions",

Расширение всегда связано с виртуальной машиной. Его можно определить непосредственно в узле ресурсов виртуальной машины или на базовом уровне и связать его с виртуальной машиной с помощью соглашения об иерархическом именовании.

Для масштабируемых наборов виртуальных машин конфигурация расширений указывается в свойстве *extensionProfile* параметра *VirtualMachineProfile*.

Свойство *publisher* со значением **Microsoft.Azure.Diagnostics** и *type* со значением **IaaSDiagnostics** уникальным образом определяет расширение системы диагностики Azure.

Значение свойства *name* можно использовать для обращения к расширению в группе ресурсов. Если задать значение **Microsoft.Insights.VMDiagnosticsSettings**, портал Azure сможет легко определить это расширение и диаграммы мониторинга будут отображаться правильно на портале Azure.

Значение *typeHandlerVersion* указывает версию расширения, которую нужно использовать. Если задать для параметра дополнительного номера версии *autoUpgradeMinorVersion* значение **true** , вы будете получать последний доступный дополнительный номер версии расширения. Рекомендуется всегда указывать для параметра *autoUpgradeMinorVersion* значение **true** , чтобы иметь возможность использовать последнее доступное расширение системы диагностики со всеми новыми функциями и исправлениями ошибок. 

Элемент *settings* содержит свойства конфигураций для расширения, которые можно задать и считывать с расширения (иногда они называются открытой конфигурацией). Свойство *xmlcfg* содержит конфигурацию в формате XML для журналов диагностики, счетчиков производительности и т. д., данные которых будет собирать агент диагностики. Дополнительные сведения о схеме XML см. в разделе [Схема конфигурации системы диагностики](https://msdn.microsoft.com/library/azure/dn782207.aspx). Традиционно конфигурации в формате XML хранятся в качестве переменных в шаблоне диспетчера ресурсов Azure, после чего они объединяются и шифруются в кодировке base64, чтобы задать значение для *xmlcfg*. Дополнительные сведения о способах хранения конфигурации в формате XML в качестве переменных см. в разделе [Переменные конфигурации диагностики](#diagnostics-configuration-variables). Свойство *storageAccount* указывает имя учетной записи хранения, в которую будут передаваться диагностические данные. 

Свойства в параметре *protectedSettings* (иногда называются закрытой конфигурацией) можно задать, но затем невозможно считать. Благодаря тому, что параметр *protectedSettings* предназначен только для записи, он подходит для хранения секретных данных, например ключа учетной записи хранения, в которую будут записываться диагностические данные.    

## <a name="specifying-diagnostics-storage-account-as-parameters"></a>Указание учетной записи хранения диагностических данных в качестве параметра
Во фрагменте кода JSON расширения системы диагностики выше предполагается использование параметров *existingdiagnosticsStorageAccountName* и *existingdiagnosticsStorageAccountName* для указания учетной записи хранения диагностических данных. Если указать учетную запись хранения диагностических данных в качестве параметра, это упрощает процесс смены учетной записи хранения диагностических данных в различных средах. Например, может потребоваться использовать разные учетные записи хранения диагностических данных для тестирования и развертывания в рабочей среде.  

        "existingdiagnosticsStorageAccountName": {
            "type": "string",
            "metadata": {
        "description": "The name of an existing storage account to which diagnostics data will be transfered."
            }        
        },
        "existingdiagnosticsStorageResourceGroup": {
            "type": "string",
            "metadata": {
        "description": "The resource group for the storage account specified in existingdiagnosticsStorageAccountName"
              }
        }

Рекомендуется указать учетную запись хранения диагностических данных в группе ресурсов, отличной от группы ресурсов для виртуальной машины. Группа ресурсов может считаться единицей развертывания с отдельным временем существования, а виртуальную машину можно развернуть, а затем повторно развернуть после соответствующих обновлений конфигураций. Но диагностические данные можно продолжить хранить в одной учетной записи в этих развертываниях виртуальных машин. Если разместить учетную запись хранения в другом ресурсе, она может получать данные из различных развертываний виртуальных машин, что упрощает устранение неполадок в разных версиях.

> [!NOTE]
> При создании шаблона виртуальной машины Windows в Visual Studio для учетной записи хранения по умолчанию может быть настроено использование учетной записи хранения, в которую добавляется виртуальный жесткий диск виртуальной машины. Это позволяет упростить начальную настройку виртуальной машины. Чтобы использовать другую учетную запись хранения, которую можно передать в качестве параметра, следует выполнить рефакторинг шаблона. 
> 
> 

## <a name="diagnostics-configuration-variables"></a>Переменные конфигурации диагностики
Во фрагменте кода JSON расширения системы диагностики выше определена переменная *accountid* , позволяющая упростить получение ключа учетной записи хранения для хранилища диагностических данных:   

    "accountid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/',parameters('existingdiagnosticsStorageResourceGroup'), '/providers/','Microsoft.Storage/storageAccounts/', parameters('existingdiagnosticsStorageAccountName'))]"


Свойство *xmlcfg* расширения системы диагностики определено путем использования нескольких объединенных переменных. Значения этих переменных находятся в формате XML, поэтому при настройке переменных JSON их необходимо должным образом экранировать.

Во фрагменте кода ниже приведен XML-файл конфигурации диагностики, который собирает данные стандартных системных счетчиков производительности и некоторые журналы событий и инфраструктуры диагностики Windows. Он экранирован должным образом и написан в правильном формате, поэтому конфигурацию можно вставлять непосредственно в раздел переменных шаблона. Дополнительные примеры XML-файлов конфигурации в формате, удобном для чтения, см. в разделе [Схема конфигурации системы диагностики](https://msdn.microsoft.com/library/azure/dn782207.aspx).

        "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
        "wadperfcounters1": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Privileged Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU privileged time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% User Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU user time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor Information(_Total)\\Processor Frequency\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"CPU frequency\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\System\\Processes\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Processes\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Threads\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Handle Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Handles\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\% Committed Bytes In Use\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Memory usage\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Available Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory available\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Committed Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory committed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Commit Limit\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory commit limit\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active time\" locale=\"en-us\"/></PerformanceCounterConfiguration>",
        "wadperfcounters2": "<PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Read Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active read time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Write Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active write time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Transfers/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Reads/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk read operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Writes/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk write operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Read Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk read speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Write Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk write speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\LogicalDisk(_Total)\\% Free Space\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk free space (percentage)\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
        "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters1'), variables('wadperfcounters2'), '<Metrics resourceId=\"')]",
        "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name , '/providers/', 'Microsoft.Compute/virtualMachines/')]",
        "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>"

Узел определения метрик в формате XML в представленной выше конфигурации — важный элемент конфигурации, так как он определяет способ агрегирования и хранения счетчиков производительности, определенных ранее в XML в узле *PerformanceCounter* . 

> [!IMPORTANT]
> Эти метрики обеспечивают данными диаграммы мониторинга и оповещения на портале Azure.  Узел **Metrics** с *resourceID* и **MetricAggregation** должен быть включен в конфигурацию диагностики виртуальной машины, если вы хотите видеть на портале Azure данные мониторинга этой виртуальной машины. 
> 
> 

Ниже приведен пример XML-кода для определений метрик: 

        <Metrics resourceId="/subscriptions/subscription().subscriptionId/resourceGroups/resourceGroup().name/providers/Microsoft.Compute/virtualMachines/vmName">
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>

Свойство *resourceID* уникальным образом определяет виртуальную машину в подписке. Обязательно используйте функции subscription() и resourceGroup(), чтобы шаблон автоматически обновлял эти значения на основе подписки и группы ресурсов, в которых выполняется развертывание.

Если создается несколько виртуальных машин в цикле, необходимо указать функцию copyIndex() в значении *resourceID* , чтобы должным образом провести различия между каждой отдельной виртуальной машиной. Для поддержки такого сценария свойство *xmlCfg* можно обновить следующим образом.  

    "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), concat(parameters('vmNamePrefix'), copyindex()), variables('wadcfgxend')))]", 

Значение MetricAggregation *PT1H* и *PT1M* обозначает значение агрегирования за минуту и час.

## <a name="wadmetrics-tables-in-storage"></a>Таблицы WADMetrics в хранилище
Конфигурация метрик выше создаст таблицы в учетной записи хранения диагностических данных с использованием следующих соглашений об именовании.

* **WADMetrics** — стандартный префикс для всех таблиц WADMetrics.
* **PT1H** или **PT1M** — указывает, что таблица содержит сводные данные за 1 час и 1 минуту.
* **P10D** — указывает, что таблица будет содержать данные за 10 дней с момента, когда таблица начала собирать данные.
* **V2S** — строковая константа.
* **yyyymmdd** — дата начала сбора данных таблицей.

Например, таблица *WADMetricsPT1HP10DV2S20151108* будет содержать данные метрик, агрегированные за час в течение 10 дней, начиная с 11 ноября 2015 года.    

Каждая таблица WADMetrics будет содержать следующие столбцы:

* **PartitionKey**— ключ секции создается на основе значения *resourceID* , которое используется для определения ресурса виртуальной машины уникальным образом. например: 002Fsubscriptions:<subscriptionID>:002FresourceGroups:002F<ResourceGroupName>:002Fproviders:002FMicrosoft:002ECompute:002FvirtualMachines:002F<vmName>  
* **RowKey** — указывается в формате <Descending time tick>:<Performance Counter Name>. Такты времени вычисляются в порядке убывания следующим образом: от максимального количества тактов времени отнимается время начала периода агрегирования. Например:  если период выборки начался 10 ноября 2015 г. в 00:00 в формате UTC, вычисление выглядело бы следующим образом: DateTime.MaxValue.Ticks - (new DateTime(2015,11,10,0,0,0,DateTimeKind.Utc).Ticks). Для счетчика производительности доступных байтов памяти ряд будет выглядеть так: 2519551871999999999__:005CMemory:005CAvailable:0020Bytes.
* **CounterName** — имя счетчика производительности. Это значение соответствует *counterSpecifier* , определенному в XML-файле конфигурации.
* **Maximum** — максимальное значение счетчика производительности в течение периода сбора.
* **Minimum** — минимальное значение счетчика производительности в течение периода сбора.
* **Total** — сумма всех значений счетчика производительности, переданных в течение периода сбора.
* **Count** — общее количество значений, переданных для счетчика производительности.
* **Average** — среднее значение (сумма значений, деленная на общее количество значений) счетчика производительности в течение периода сбора.

## <a name="next-steps"></a>Дальнейшие действия
* Полный пример шаблона виртуальной машины Windows с расширением системы диагностики см. в разделе [201-vm-monitoring-diagnostics-extension](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-monitoring-diagnostics-extension).   
* Разверните шаблон диспетчера ресурсов с использованием [Azure PowerShell](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) или [командной строки Azure](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Узнайте больше о [создании шаблонов диспетчера ресурсов Azure](../../resource-group-authoring-templates.md)

