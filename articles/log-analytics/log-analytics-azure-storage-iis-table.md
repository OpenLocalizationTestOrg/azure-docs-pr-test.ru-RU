---
title: "aaaUse хранилища больших двоичных объектов для служб IIS и таблица хранения событий в службе анализа журналов Azure | Документы Microsoft"
description: "Аналитика журналов можно считывать hello журналы для служб Azure, которые записывают tootable хранилищ диагностики или журналы IIS записывались tooblob хранилища."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a>Использование хранилища BLOB-объектов Azure для IIS и хранилища таблиц Azure для событий в Azure Log Analytics

Служба аналитики журналов может читать журналы hello для следующих служб, которые записывают диагностики tootable хранилища или IIS, журналы хранения письменного tooblob hello:

* кластеры Service Fabric (предварительная версия);
* Виртуальные машины
* Веб-роль или рабочая роль.

Чтобы служба Log Analytics могла собирать данные для этих ресурсов, необходимо включить систему диагностики Azure.

После включения диагностики можно использовать портал Azure hello или PowerShell Настройка журналов hello toocollect анализа журналов.

Диагностика Azure — это расширение Azure, позволяющий toocollect диагностических данных из рабочей роли, веб-роли или виртуальной машины, работающей в Azure. Hello данные хранятся в учетной записи хранилища Azure и затем может быть собранные службой аналитики журналов.

Для анализа журналов toocollect эти журналы диагностики Azure hello журналы должны находиться в hello следующих элементов:

| Тип журнала | Тип ресурса | Расположение |
| --- | --- | --- |
| Журналы IIS |Виртуальные машины <br> Веб-роли <br> Рабочие роли |wad-iis-logfiles (хранилище BLOB-объектов) |
| syslog |Виртуальные машины |LinuxsyslogVer2v0 (хранилище таблиц) |
| Операционные события Service Fabric |Узлы Service Fabric |WADServiceFabricSystemEventTable |
| События субъектов Service Fabric Reliable Actors |Узлы Service Fabric |WADServiceFabricReliableActorEventTable |
| События надежных служб Service Fabric |Узлы Service Fabric |WADServiceFabricReliableServiceEventTable |
| Журналы событий Windows |Узлы Service Fabric <br> Виртуальные машины <br> Веб-роли <br> Рабочие роли |WADWindowsEventLogsTable (хранилище таблиц) |
| Журналы трассировки событий Windows |Узлы Service Fabric <br> Виртуальные машины <br> Веб-роли <br> Рабочие роли |WADETWEventTable (хранилище таблиц) |

> [!NOTE]
> Журналы IIS веб-сайтов Azure в настоящее время не поддерживаются.
>
>

Для виртуальных машин, у вас есть возможность установить hello hello [анализа журналов агента](log-analytics-azure-vm-extension.md) в вашей виртуальной машины tooenable дополнительные функции анализа. Кроме toobeing может tooanalyze IIS и журналов событий, можно выполнить дополнительный анализ, включая отслеживание изменений конфигурации, оценку SQL и оценку обновлений.

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a>Включение диагностики Azure в виртуальной машине для сбора журналов событий и журналов IIS
Hello используйте следующие процедуры tooenable диагностики Azure в виртуальной машине для сбора, с помощью портала Microsoft Azure hello журналов событий и журналов IIS.

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a>tooenable диагностики Azure в виртуальную машину с портала Azure hello
1. При создании виртуальной машины, установите агент ВМ hello. Если hello виртуальная машина уже существует, убедитесь, что приветствия уже установлен агент виртуальной Машины.

   * В hello портал Azure, перейдите toohello виртуальной машины, выберите **необязательная конфигурация**, затем **диагностики** и задайте **состояние** слишком**на**.

     По завершении hello виртуальных Машин с расширением hello диагностики Azure установлены и запущены. Это расширение отвечает за сбор диагностических данных.
2. На существующей виртуальной машине включите мониторинг и настройте ведение журнала событий. Можно включить диагностику на hello уровня виртуальной Машины. Диагностика tooenable и затем настроить ведение журнала событий, выполните следующие шаги hello:

   1. Выберите hello виртуальной Машины.
   2. Щелкните **Мониторинг**.
   3. Щелкните **Диагностика**.
   4. Набор hello **состояние** слишком**ON**.
   5. Выберите каждый журнал диагностики, которые должны toocollect.
   6. Нажмите кнопку **ОК**.

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a>Включение диагностики в веб-роли для сбора журналов IIS и событий
См. слишком[как tooEnable диагностики в облачной службе](../cloud-services/cloud-services-dotnet-diagnostics.md) общие инструкции о включении диагностики Azure. Приведенные ниже инструкции Hello эти сведения можно использовать и настройте его для использования с помощью аналитики журналов.

При включении диагностики Azure происходит следующее.

* По умолчанию данные передаются через интервал передачи scheduledTransferPeriod hello хранятся журналы IIS.
* Журналы событий Windows по умолчанию не передаются.

### <a name="tooenable-diagnostics"></a>Диагностика tooenable
tooenable журналы событий Windows или toochange hello scheduledTransferPeriod, настройте диагностику Azure, с помощью hello XML-файл конфигурации (diagnostics.wadcfg), как показано в [шаг 4: Создание файла конфигурации диагностики и установка hello расширение](../cloud-services/cloud-services-dotnet-diagnostics.md)

Hello следующий файл конфигурации собирает журналы IIS и все события из приложения hello и системные журналы:

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

Убедитесь, что в параметре ConfigurationSettings указана учетная запись хранения, как следующий пример hello.

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

Hello **AccountName** и **AccountKey** значения находятся в hello портал Azure в мониторинга учетной записи хранения hello под управление ключами доступа. Hello для hello строки подключения должен использоваться протокол **https**.

После применения обновленная конфигурация диагностики hello tooyour облачной службы и он производит запись диагностики tooAzure хранилища, то будут готовы tooconfigure анализа журналов.

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a>Использовать журналы Azure портала toocollect hello из хранилища Azure
Hello Azure портала tooconfigure журнала toocollect hello журналы аналитики можно использовать для следующих служб Azure hello:

* Кластеры Service Fabric.
* Виртуальные машины
* Веб-роль или рабочая роль.

В hello портал Azure перейдите в рабочую область службы анализа журналов tooyour и выполните следующие задачи hello.

1. Щелкните *Storage accounts logs* (Журналы учетных записей хранения).
2. Нажмите кнопку hello *добавить* задач
3. Выберите учетную запись хранения hello, содержащий журналы диагностики hello
   * Это может быть классическая учетная запись хранения или учетная запись хранения Azure Resource Manager.
4. Выберите тип данных, который будет toocollect журналы для hello
   * Hello доступны журналы IIS; События; Syslog (Linux); Журналы трассировки событий Windows; События Service Fabric.
5. значение Hello источник заполняется автоматически основании hello данные типа и не может быть изменен
6. Нажмите кнопку ОК toosave hello конфигурации

Повторите шаги 2 – 6 для дополнительного хранилища учетных записей и типы данных, которые должны toocollect анализа журналов.

Около 30 минут, может toosee данные из учетной записи хранилища hello в службе анализа журналов. Вы увидите только данные, записываемые toostorage после применения конфигурации hello. Служба аналитики журналов не считывает hello существующих данных из учетной записи хранения hello.

> [!NOTE]
> портал Hello не проверяет, hello источника существует в учетной записи хранения hello, или если новые данные записываются.
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a>Включение диагностики Azure на виртуальной машине для сбора журналов событий и журналов IIS с помощью PowerShell
Используйте hello шагов в [tooindex Настройка аналитики журналов диагностики Azure](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse tooread PowerShell из службы диагностики Azure, написанных tootable хранилища.

С помощью Azure PowerShell можно более точно указать hello, события должны записываться tooAzure хранилища.
Дополнительную информацию см. в статье [Включение диагностики на виртуальных машинах Azure](../virtual-machines-dotnet-diagnostics.md).

Можно включить и обновить hello следующий сценарий PowerShell с помощью диагностики Azure.
Его также можно использовать с пользовательской конфигурацией ведения журналов.
Изменение учетной записи хранилища hello сценария tooset hello, имя службы и имя виртуальной машины.
Hello скрипт использует командлеты для классических виртуальных машин.

Просмотрите следующий образец скрипта hello, скопировать его, измените нужным образом, сохраните как файл скрипта PowerShell образец hello и затем запустите скрипт hello.

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a>Дальнейшие действия
* [Сбор журналов и метрик для поддерживаемых служб Azure](log-analytics-azure-storage.md).
* [Включить решения](log-analytics-add-solutions.md) tooprovide понимание данных hello.
* [Использовать запросы поиска](log-analytics-log-searches.md) tooanalyze hello данных.
