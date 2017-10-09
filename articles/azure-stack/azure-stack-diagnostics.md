---
title: "aaaDiagnostics стека Azure | Документы Microsoft"
description: "Как файлы журнала toocollect для диагностики в стек Azure"
services: azure-stack
documentationcenter: 
author: adshar
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: adshar
ms.openlocfilehash: a4a5ddf29e75df710e9fae366d6ac16e6fb36d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-diagnostics-tools"></a>Средства диагностики Azure стека
 
Стек Azure имеет большое количество компонентов совместной работы и взаимодействия друг с другом. Все эти компоненты создают свои собственные уникальные журналы, это означает, что выявить проблемы, может быстро стать сложной задачи, особенно для ошибок, поступающих из нескольких взаимодействующих компонентов Azure стека. 

Наши средства диагностики помогают убедитесь, что механизм сбора журналов hello проста и эффективна. Hello следующей схеме показано влияние журнала средства сбора данных в работе стека Azure:

![Средства сбора данных журнала](media/azure-stack-diagnostics/image01.png)
 
 
## <a name="trace-collector"></a>Сборщиком трассировки
 
Hello сборщика трассировки включены по умолчанию. Он постоянно выполняется в фоновом режиме hello и собирает все журналы трассировки событий для Windows (ETW) из служб компонентов на стек Azure и сохраняет их на общие локальной общей папкой. 

Здесь представлены Hello tooknow важные вопросы о hello сборщика трассировки:
 
* Hello сбора данных выполняется постоянно с ограничениями размера по умолчанию. по умолчанию максимальный размер, допустимый для каждого файла (200 МБ): Hello **не** пороговый размер. Периодически происходит проверка размера (в настоящее время каждые 10 минут) и если hello текущий файл > = 200 МБ, оно сохраняется и создается новый файл. Также есть (8 ГБ настраиваемое) ограничение на размер файла общее hello, созданные для сеанса событий. По достижении этого предела hello старые файлы будут удалены при создании новых.
* О журналах hello ограничено возраст 5 дней. Это ограничение может быть настроен. 
* Каждый компонент определяет свойства конфигурации трассировки hello через JSON-файла. Hello файлы JSON хранятся в `C:\TraceCollector\Configuration`. При необходимости эти файлы можно редактировать toochange hello возраст и размер границы hello собираются журналы. Файлы toothese изменения требуют перезапуска hello *сборщик трассировки стека Microsoft Azure* tootake эффект изменения службы для hello.
* Hello ниже приведен файл трассировки конфигурации JSON для операций FabricRingServices от hello XRP виртуальной Машины: 

```
{
    "LogFile": 
    {
        "SessionName": "FabricRingServicesOperationsLogSession",
        "FileName": "\\\\SU1FileServer\\SU1_ManagementLibrary_1\\Diagnostics\\FabricRingServices\\Operations\\AzureStack.Common.Infrastructure.Operations.etl",
        "RollTimeStamp": "00:00:00",
        "MaxDaysOfFiles": "5",
        "MaxSizeInMB": "200",
        "TotalSizeInMB": "5120"
    },
    "EventSources":
    [
        {"Name": "Microsoft-AzureStack-Common-Infrastructure-ResourceManager" },
        {"Name": "Microsoft-OperationManager-EventSource" },
        {"Name": "Microsoft-Operation-EventSource" }
    ]
}
```

* **MaxDaysOfFiles**

    Этот параметр управляет hello возраст tookeep файлов. Старые файлы журнала будут удалены.
* **MaxSizeInMB**

    Этот параметр управляет hello пороговое значение размера для одного файла. При достижении размера hello создается новый ETL-файла.
* **TotalSizeInMB**

    Этот параметр управляет hello общий размер файлов .etl hello, созданного из сеанса событий. Если hello общий размер файлов превышает это значение параметра, старые файлы будут удалены.
  
## <a name="log-collection-tool"></a>Средство сбора журналов
 
Здравствуйте, команда PowerShell `Get-AzureStackLog` может быть используется toocollect журналы из всех компонентов hello в среде Azure стека. Она сохраняет их в ZIP-файлы в расположении определяемой пользователем. Если наш Техническая поддержка потребностями группы вашей toohelp журналы Устранение проблемы, они могут попросить вас toorun этого средства.

> [!CAUTION]
> Эти файлы журнала могут содержать личные сведения (PII). Это учитывать перед отправкой любых файлов журнала открыто.
 
В настоящее время мы собираем hello следующие типы журналов:
*   **Журналы развертывания Azure стека**
*   **Журналы событий Windows**
*   **Журналы panther**

     проблемы создания tootroubleshoot виртуальной Машины.
*   **Журнал кластера**
*   **Журналы диагностики хранилища**
*   **Журналы трассировки событий Windows**

    Они собираются по hello сборщика трассировки и сохраняются в общей папке, откуда `Get-AzureStackLog` извлекает их.
 
Здравствуйте, все журналы, которые собираются из всех компонентов hello tooidentify ссылаться toohello `<Logs>` теги в файле конфигурации клиента hello, расположенный в `C:\EceStore\<Guid>\<GuidWithMaxFileSize>`.
 
### <a name="toorun-get-azurestacklog"></a>toorun Get AzureStackLog
1.  Войдите в систему как AzureStack\AzureStackAdmin на узле hello.
2.  Откройте окно PowerShell от имени администратора.
3.  Запустите `Get-AzureStackLog`.  

    **Примеры**

    - Собирать все журналы для всех ролей:

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs`

    - Соберите журналы из VirtualMachines и BareMetal роли:

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal`

    - Соберите журналы из VirtualMachines и BareMetal роли, с датой фильтрации для файлов журналов для hello последние 8 часов:

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal -FromDate (Get-Date).AddHours(-8) -ToDate (Get-Date)`

Если hello `FromDate` и `ToDate` параметры не указаны, сбора журналов за hello последние 4 часа по умолчанию.

В настоящее время можно использовать hello `FilterByRole` параметр toofilter журнала коллекции с помощью hello следующих ролей:

|   |   |   |
| - | - | - |
| `ACSMigrationService`     | `ACSMonitoringService`   | `ACSSettingsService` |
| `ACS`                     | `ACSFabric`              | `ACSFrontEnd`        |
| `ACSTableMaster`          | `ACSTableServer`         | `ACSWac`             |
| `ADFS`                    | `ASAppGateway`           | `BareMetal`          |
| `BRP`                     | `CA`                     | `CPI`                |
| `CRP`                     | `DeploymentMachine`      | `DHCP`               |
|`Domain`                   | `ECE`                    | `ECESeedRing`        |        
| `FabricRing`              | `FabricRingServices`     | `FRP`                |
|` Gateway`                 | `HealthMonitoring`       | `HRP`                |               
| `IBC`                     | `InfraServiceController` | `KeyVaultAdminResourceProvider`|
| `KeyVaultControlPlane`    | `KeyVaultDataPlane`      | `NC`                 |            
| `NonPrivilegedAppGateway` | `NRP`                    | `SeedRing`           |
| `SeedRingServices`        | `SLB`                    | `SQL`                |     
| `SRP`                     | `Storage`                | `StorageController`  |
| `URP`                     | `UsageBridge`            | `VirtualMachines`    |  
| `WAS`                     | `WASPUBLIC`              | `WDS`                |


Toonote несколько вещей:

* Это команда принимает некоторое время для сбора журналов, в зависимости от роли, которую журналы собираются. Такие факторы, составляющей hello продолжительность времени, указанных для сбора журналов и hello количеством узлов в среде Azure стека hello.
* После завершения сбора журналов, проверьте hello новой папки, созданные в hello `-OutputPath` параметр, указанный в команде hello.
* Файл с именем `Get-AzureStackLog_Output.log` создается в папке hello, содержащий hello ZIP-файлов и включает выходные данные команды hello, который может использоваться для устранения сбоев сбор данных журналов.
* Каждая роль имеет журналов внутри отдельных ZIP-файл. 
* tooinvestigate конкретный сбой, журналы могут быть необходимы из более чем одного компонента.
    -   Журналы событий для всех виртуальных машин инфраструктуры и системы собираются в hello *VirtualMachines* роли.
    -   Системы и журналы событий для всех узлов сохраняются в hello *BareMetal* роли.
    -   Отказоустойчивый кластер и Hyper-V журналы событий сохраняются в hello *хранения* роли.
    -   ACS журналы собираются в hello *хранения* и *ACS* ролей.
* Дополнительные сведения можно ссылаться toohello файл конфигурации клиента. Исследовать hello `<Logs>` теги для различных ролей hello.

> [!NOTE]
> Мы задать размер и возраст ограничивает toohello журналы, собранные как основные tooensure эффективное использование вашей toomake места хранения, убедиться, что он не получает переполняющее с журналами. Вышесказанного, когда диагностики неполадок часто достаточно входит, больше не существует из-за ограничений toothese применяется принудительно. Следовательно, это **настоятельно рекомендуется** , вы разгрузить журналы tooan внешних дискового пространства (учетной записи хранилища в Azure открытый, дополнительные локальное устройство хранения данных и т.д.) каждые 8 часов too12 и сохранять их существует 1-3 месяцев в зависимости от требований.


## <a name="next-steps"></a>Дальнейшие действия
[Microsoft Azure Stack troubleshooting (Устранение неполадок, связанных с Microsoft Azure Stack)](azure-stack-troubleshooting.md)
