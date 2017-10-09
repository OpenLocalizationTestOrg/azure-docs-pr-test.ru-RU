---
title: "aaaAdd мониторинг и диагностика tooan виртуальной машины Azure | Документы Microsoft"
description: "Используйте toocreate шаблона диспетчера ресурсов Azure новой виртуальной машины Windows с расширением диагностики Azure."
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
ms.openlocfilehash: d8a831421a0f9d38c09d51cf8c2e6dff913c77ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-monitoring-and-diagnostics-with-a-windows-vm-and-azure-resource-manager-templates"></a>Использование мониторинга и системы диагностики с виртуальной машиной Windows и шаблонами Azure Resource Manager
Hello расширения системы диагностики Azure обеспечивает мониторинг hello и возможности диагностики в Windows на основе виртуальной машины Azure. Вы можете включить эти возможности на виртуальной машине hello, включая расширение hello как часть шаблона диспетчера ресурсов azure hello. Дополнительные сведения о включении любого расширения в шаблон виртуальной машины см. в статье [Создание шаблонов диспетчера ресурсов Azure с расширениями виртуальных машин](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions). В этой статье рассматривается, как можно добавить windows hello Azure Diagnostics расширения tooa шаблона виртуальной машины.  

## <a name="add-hello-azure-diagnostics-extension-toohello-vm-resource-definition"></a>Добавьте определения ресурсов виртуальной Машины toohello расширения hello диагностики Azure
расширение системы диагностики hello tooenable на виртуальной машине Windows вы должны иметь расширение hello tooadd виртуальной Машины в качестве ресурса hello шаблона диспетчера ресурсов.

Для простых диспетчер ресурсов на основе виртуальной машины добавить hello расширения конфигурации toohello *ресурсов* массива для hello виртуальной машины: 

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


Другое соглашение о распространенных добавить конфигурацию расширения hello hello корневого узла ресурсов шаблона hello, вместо того чтобы определять его в узле ресурсы виртуальной машины hello. В этом случае у вас есть tooexplicitly укажите иерархические отношения между расширение hello и hello виртуальной машины с hello *имя* и *тип* значения. Например: 

    "name": "[concat(variables('vmName'),'Microsoft.Insights.VMDiagnosticsSettings')]",
    "type": "Microsoft.Compute/virtualMachines/extensions",

расширение Hello всегда связано с hello виртуальной машины, можно либо непосредственно определить ресурс в узле hello виртуальной машины напрямую или его определения на уровне базы hello и использовать hello иерархических именования tooassociate соглашение о его с виртуального hello компьютер.

Для расширения набора масштабирования виртуальной машины hello конфигурации указывается в hello *extensionProfile* свойство hello *VirtualMachineProfile*.

Hello *издатель* свойство со значением hello **Microsoft.Azure.Diagnostics** и hello *тип* свойство со значением hello **IaaSDiagnostics** уникальной идентификации hello расширения диагностики Azure.

Здравствуйте, значение hello *имя* свойство может иметь расширение toohello toorefer используется в группе ресурсов hello. Значения этого свойства специально слишком**Microsoft.Insights.VMDiagnosticsSettings** включит ее toobe легко идентифицировать по hello Azure гарантирует портала, hello мониторинга диаграммы отображаются правильно в hello портал Azure.

Hello *typeHandlerVersion* указывает версию hello расширения hello хотелось бы toouse. Установка *autoUpgradeMinorVersion* вспомогательная версии слишком**true** гарантирует, что будет получат hello последняя вспомогательная версия расширения hello, которая доступна. Настоятельно рекомендуется всегда устанавливать *autoUpgradeMinorVersion* быть tooalways **true** , чтобы всегда получать расширения hello последнюю toouse диагностики доступны все новые функции hello и ошибки исправления. 

Hello *параметры* элемент содержит свойства конфигурации для расширения hello, которое можно задать и считывается расширения hello (который иногда ссылается tooas открытой конфигурации). Hello *xmlcfg* свойство содержит конфигурацию на основе xml для журналов диагностики hello, счетчиков производительности собираются агентом диагностики hello и т. д. В разделе [схема конфигурации службы диагностики](https://msdn.microsoft.com/library/azure/dn782207.aspx) Дополнительные сведения о hello саму схему xml. Распространенной практикой является toostore hello фактические XML-файл конфигурации, как переменную в шаблоне hello диспетчера ресурсов Azure и затем concatenate и base64 кодировать значение hello tooset *xmlcfg*. См. в разделе hello [переменных конфигурации диагностики](#diagnostics-configuration-variables) toounderstand Дополнительные сведения о как toostore hello xml в переменных. Hello *storageAccount* свойство указывает, будут передаваться данные диагностики toowhich учетной записи хранилища hello имя hello. 

Здравствуйте, свойства в *protectedSettings* (который иногда ссылается tooas закрытая конфигурация) можно установить, но не удается прочитать обратно после установки. Здравствуйте, только для записи характер *protectedSettings* позволяет использовать его для хранения секретов как ключ учетной записи хранения hello где hello диагностические данные будут записаны.    

## <a name="specifying-diagnostics-storage-account-as-parameters"></a>Указание учетной записи хранения диагностических данных в качестве параметра
Hello диагностики расширения json выше фрагменте предполагается два параметра *existingdiagnosticsStorageAccountName* и *existingdiagnosticsStorageResourceGroup* toospecify hello диагностики Учетная запись хранения, где будут храниться данные диагностики. Указание учетной записи хранения диагностики hello в параметр делает учетная запись хранения диагностики hello легко toochange различных средах например вы можете toouse учетной записи хранения различных диагностики для тестирования, а другой для вашей развертывание в рабочей среде.  

        "existingdiagnosticsStorageAccountName": {
            "type": "string",
            "metadata": {
        "description": "hello name of an existing storage account toowhich diagnostics data will be transfered."
            }        
        },
        "existingdiagnosticsStorageResourceGroup": {
            "type": "string",
            "metadata": {
        "description": "hello resource group for hello storage account specified in existingdiagnosticsStorageAccountName"
              }
        }

Это лучший подход toospecify учетная запись хранения диагностики в группе ресурсов, отличной от hello группы ресурсов для виртуальной машины hello. Группа ресурсов может рассматриваться как toobe домен имеет собственный жизненный цикл развертывания, можно развернуть и повторного развертывания при внесении новых обновлений конфигурации виртуальной машины tooit, но вы можете toocontinue хранение данных диагностики hello в hello учетную запись хранения для развертывания этих виртуальных машин. Наличие учетной записи хранилища hello в другой ресурс включает hello данные учетной записи хранилища tooaccept из различных развертывания виртуальных машин, что позволяет легко tootroubleshoot проблемы через hello различных версий.

> [!NOTE]
> При создании шаблона виртуальной машины windows из Visual Studio, может быть настроена учетная запись хранения по умолчанию hello toouse hello одной учетной записи хранения, где данные будут загружены hello виртуальный жесткий ДИСК виртуальной машины. Это toosimplify начальной настройки hello виртуальной Машины. Следует повторно оценить toouse шаблона hello другую учетную запись хранения, можно передать в качестве параметра. 
> 
> 

## <a name="diagnostics-configuration-variables"></a>Переменные конфигурации диагностики
Определяет Hello диагностики расширения json выше фрагменте *accountid* переменных toosimplify начало hello ключ учетной записи хранилища для хранения диагностики hello:   

    "accountid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/',parameters('existingdiagnosticsStorageResourceGroup'), '/providers/','Microsoft.Storage/storageAccounts/', parameters('existingdiagnosticsStorageAccountName'))]"


Hello *xmlcfg* для расширения диагностики hello определено несколько переменных, которые соединяются с помощью. значения этих переменных Hello возвращаются в формате xml, поэтому они должны toobe escape-знака корректно при задании переменных hello json.

Hello ниже описаны hello диагностики XML-файл конфигурации, сбор данных счетчиков производительности уровня стандартной системы вместе с некоторыми журналы событий windows и журналы инфраструктуры диагностики. Он escape-последовательность и правильный формат, чтобы hello конфигурации, можно напрямую вставить в разделе hello переменных шаблона. В разделе hello [схема конфигурации службы диагностики](https://msdn.microsoft.com/library/azure/dn782207.aspx) человеческих пример XML-файл конфигурации hello, доступной для чтения.

        "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
        "wadperfcounters1": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Privileged Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU privileged time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% User Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU user time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor Information(_Total)\\Processor Frequency\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"CPU frequency\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\System\\Processes\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Processes\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Threads\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Handle Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Handles\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\% Committed Bytes In Use\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Memory usage\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Available Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory available\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Committed Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory committed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Commit Limit\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory commit limit\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active time\" locale=\"en-us\"/></PerformanceCounterConfiguration>",
        "wadperfcounters2": "<PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Read Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active read time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Write Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active write time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Transfers/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Reads/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk read operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Writes/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk write operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Read Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk read speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Write Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk write speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\LogicalDisk(_Total)\\% Free Space\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk free space (percentage)\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
        "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters1'), variables('wadperfcounters2'), '<Metrics resourceId=\"')]",
        "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name , '/providers/', 'Microsoft.Compute/virtualMachines/')]",
        "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>"

Hello метрики определения XML-узел в hello выше конфигурации — это элемент важные настройки, как он определяет, как счетчики производительности hello, определенные ранее в xml hello в *PerformanceCounter* узла будут собраны и сохраняются. 

> [!IMPORTANT]
> Эти метрики диска hello мониторинга диаграммы и оповещений в hello портал Azure.  Hello **метрики** узел с hello *resourceID* и **MetricAggregation** должны быть включены в hello конфигурация диагностики для виртуальной Машины, если требуется, чтобы toosee hello виртуальной Машины Наблюдение за данными в hello портал Azure. 
> 
> 

Hello ниже приведен пример hello xml для определений метрик: 

        <Metrics resourceId="/subscriptions/subscription().subscriptionId/resourceGroups/resourceGroup().name/providers/Microsoft.Compute/virtualMachines/vmName">
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>

Hello *resourceID* атрибут однозначно определяет hello виртуальной машины в вашей подписке. Убедитесь, что subscription() toouse hello и resourceGroup() функции, чтобы hello шаблон автоматически обновляет эти значения на основе группы ресурса и подписки hello, которые развертываются на.

Если создается несколько виртуальных машин в цикле, то необходимо будет toopopulate hello *resourceID* значение с toocorrectly функция copyIndex() отличать каждого отдельных виртуальных Машин. Hello *xmlCfg* значение может быть обновленные toosupport это следующим образом:  

    "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), concat(parameters('vmNamePrefix'), copyindex()), variables('wadcfgxend')))]", 

Здравствуйте, значение MetricAggregation *PT1H* и *PT1M* обозначения агрегирование за минуту и агрегата более часа.

## <a name="wadmetrics-tables-in-storage"></a>Таблицы WADMetrics в хранилище
Hello показатели выше конфигурации будет создать таблицы в учетной записи хранения диагностики с hello соглашениям об именовании:

* **WADMetrics** — стандартный префикс для всех таблиц WADMetrics.
* **PT1H** или **PT1M** : обозначает этой таблицы hello содержит сводные данные более 1 часа или 1 минута
* **P10D** : обозначает hello таблицы будет содержать данные для 10 дней после начала сбора данных таблицы hello
* **V2S** — строковая константа.
* **ГГГГММДД** : hello даты, на какие hello таблицы начала сбор данных

Например, таблица *WADMetricsPT1HP10DV2S20151108* будет содержать данные метрик, агрегированные за час в течение 10 дней, начиная с 11 ноября 2015 года.    

Каждая таблица WADMetrics будет содержать hello следующие столбцы:

* **PartitionKey**: hello partitionkey создается на основании hello *resourceID* toouniquely значение идентификации hello ресурса виртуальной Машины. например: 002Fsubscriptions:<subscriptionID>:002FresourceGroups:002F<ResourceGroupName>:002Fproviders:002FMicrosoft:002ECompute:002FvirtualMachines:002F<vmName>  
* **RowKey** : формат hello следующим <Descending time tick>:<Performance Counter Name>. Hello по убыванию вычисление такт времени — max для времени тактах минус hello время начала hello периода hello статистической обработки. Например:  Если период выборки hello запущен на 10 ноября 2015 г. и расчет времени UTC, а затем hello 00:00Hrs будет выглядеть: DateTime.MaxValue.Ticks - (новый DateTime(2015,11,10,0,0,0,DateTimeKind.Utc). Такты). Для hello доступно байт памяти производительности, счетчик hello ключ строки будет выглядеть, таких как: 2519551871999999999__:005CMemory:005CAvailable:0020 байт
* **CounterName** : hello имя счетчика производительности "hello". Это соответствует hello *counterSpecifier* в файле конфигурации xml hello.
* **Максимальная** : hello максимальное значение счетчика производительности "hello" в течение периода hello статистической обработки.
* **Минимальное** : hello минимальное значение счетчика производительности "hello" в течение периода hello статистической обработки.
* **Общее** : hello сумму всех значений счетчика производительности "hello" сообщил о за период hello статистической обработки.
* **Число** : hello общее количество значений в отчеты для счетчика производительности hello.
* **Среднее** : hello среднее (общий или count) значение счетчика производительности "hello" в течение периода hello статистической обработки.

## <a name="next-steps"></a>Дальнейшие действия
* Полный пример шаблона виртуальной машины Windows с расширением системы диагностики см. в разделе [201-vm-monitoring-diagnostics-extension](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-monitoring-diagnostics-extension).   
* Развертывание с помощью hello resource manager шаблона [Azure PowerShell](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) или [командной строки Azure](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* Узнайте больше о [создании шаблонов диспетчера ресурсов Azure](../../resource-group-authoring-templates.md)

