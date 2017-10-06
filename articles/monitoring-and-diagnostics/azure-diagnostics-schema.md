---
title: "aaaAzure диагностики версий схемы конфигурации расширения и журнал | Документы Microsoft"
description: "Соответствующие toocollecting счетчиков производительности в виртуальных машинах Azure, набора масштабирования виртуальных Машин, Service Fabric и облачных служб."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/16/2017
ms.author: robb
ms.openlocfilehash: 854ad118f660810aa38703670284794d658142c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-extention-configuration-schema-versions-and-history"></a>Журнал и версии схемы конфигурации расширения системы диагностики Azure
Это страница индексы версий схемы расширения системы диагностики Azure поставляется как часть hello Microsoft Azure SDK.  

> [!NOTE]
> Hello расширения системы диагностики Azure — компонент hello используется toocollect счетчики производительности и другие статистические данные из:
> - Виртуальные машины Azure 
> - Наборы для масштабирования виртуальных машин
> - Service Fabric 
> - Облачные службы 
> - группы сетевой безопасности;
> 
> Данная страница применяется только в том случае, если вы используете одну из этих служб.

Hello расширения системы диагностики Azure используется с другими продуктами Майкрософт диагностики, как монитор Azure, Application Insights и анализа журналов. Дополнительные сведения см. в статье [Обзор мониторинга в Microsoft Azure](monitoring-overview.md).

## <a name="azure-sdk-and-diagnostics-versions-shipping-chart"></a>Диаграмма версий пакета SDK для Azure и системы диагностики  

|Версия пакета SDK для Azure | Версия расширения системы диагностики | Модель|  
|------------------|-------------------------------|------|  
|1.x               |1.0                            |Подключаемый модуль|  
|2.0–2.4         |1.0                            |Подключаемый модуль|  
|2.5               |1.2                            |Расширение|  
|2.6               |1,3                            |"|  
|2.7               |1.4                            |"|  
|2.8               |1.5                            |"|  
|2,9               |1.6                            |"|
|2.96              |1.7                            |"|
|2.96              |1.8                            |"|
|2.96              |1.8.1                          |"|
|2.96              |1.9                            |"|



 Система диагностики Azure версии 1.0 сначала поставляется в модель подключаемого модуля — это означает, что при установке hello Azure SDK вы получили версии hello диагностики Azure, поставляемых вместе с ним.  

 Начиная с пакета SDK 2.5 (diagnostics версии 1.2), система диагностики Azure был tooan расширения модели. новые функции Hello средства tooutilize ранее были доступны только в более новые пакеты SDK Azure, но любой службы, с помощью диагностики Azure может взять последнюю версию доставки hello непосредственно из Azure. Например любой пользователь по-прежнему используется SDK 2.5 бы производится загрузка последней версии hello показано в предыдущей таблице hello, независимо от того, если они используют более новые функции hello.  

## <a name="schemas-index"></a>Указатель схем  
Для разных версий системы диагностики Azure используются разные схемы конфигурации. 

[Схема конфигурации системы диагностики Azure 1.0](azure-diagnostics-schema-1dot0.md)  

[Схема конфигурации системы диагностики Azure 1.2](azure-diagnostics-schema-1dot2.md)  

[Схема конфигурации системы диагностики версии 1.3 и более поздние версии](azure-diagnostics-schema-1dot3-and-later.md)  

## <a name="version-history"></a>Журнал версий


### <a name="diagnostics-extension-19"></a>Расширение системы диагностики версии 1.9 
Добавлена поддержка Docker.


### <a name="diagnostics-extension-181"></a>Расширение системы диагностики версии 1.8.1 
Можно указать маркер SAS, а не ключа учетной записи хранения в частной конфигурации hello. Если предоставляется токен SAS, ключ учетной записи хранения hello учитывается.


```json
{
    "storageAccountName": "diagstorageaccount",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    }
}
```

```xml
<PrivateConfig>
    <StorageAccount name="diagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    <SecondaryStorageAccounts>
        <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
</PrivateConfig>
```


### <a name="diagnostics-extension-18"></a>Расширение системы диагностики версии 1.8 
Добавлены tooPublicConfig тип хранилища. StorageType может иметь значение*Table*, *Blob* и *TableAndBlob*. *Таблица* по умолчанию hello.


```json
{
    "WadCfg": {
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```xml
<PublicConfig>
    <WadCfg />
    <StorageAccount>diagstorageaccount</StorageAccount>
    <StorageType>TableAndBlob</StorageType>
</PublicConfig>
```


### <a name="diagnostics-extension-17"></a>Расширение системы диагностики версии 1.7 
TooEventHub tooroute возможности добавлены hello.

### <a name="diagnostics-extension-15"></a>Расширение системы диагностики версии 1.5
Добавлены hello приемники элемент и hello возможность toosend диагностические данные слишком[Application Insights](../application-insights/app-insights-cloudservices.md) выполняя проще проблемы toodiagnose через приложения, а также hello уровне системы и инфраструктуры.

### <a name="azure-sdk-26-and-diagnostics-extension-13"></a>Пакет SDK для Azure 2.6 и расширение системы диагностики версии 1.3 
Для проектов облачных служб в Visual Studio были внесены следующие изменения hello. (Эти изменения также применяются toolater версии пакета Azure SDK).

* Hello локальный эмулятор теперь поддерживает систему диагностики. Это означает, что можно собирать данные диагностики и убедитесь, что приложение создает hello правильные трассировки во время разработки и тестирования в Visual Studio. Здравствуйте, строка подключения `UseDevelopmentStorage=true` включает сбор данных диагностики при запуске проекта облачной службы в Visual Studio с помощью эмулятора хранилища Azure hello. Все диагностические данные собираются в учетной записи хранения hello (хранилище разработки).
* Строка подключения учетной записи хранения диагностики Hello (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) еще раз сохраняется в файле конфигурации (cscfg) службы hello. Пакет SDK Azure 2.5 учетная запись хранения диагностики hello был указан в файле diagnostics.wadcfgx hello.

Существуют некоторые важные различия между как строка подключения hello работает в Azure SDK 2.4 и более ранних версий и как он работает в Azure SDK 2.6 и более поздних версий.

* В пакете Azure SDK 2.4 и более ранних версиях строка подключения hello используемый как среда выполнения hello tooget подключаемого модуля диагностики hello данных учетной записи хранения для передачи журналов диагностики.
* В пакете Azure SDK 2.6 и более поздних версиях строка подключения диагностики hello используется модулем Visual Studio tooconfigure hello диагностики hello сведения о соответствующих дисковых учетной записи во время публикации. Строка подключения Hello позволяет определить разных учетных записей хранения для различных конфигураций службы, Visual Studio будет использоваться при публикации. Тем не менее поскольку hello подключаемый модуль диагностики больше не доступен (после Azure SDK 2.5), cscfg-файле hello сам по себе не удается включить hello расширения диагностики. У вас tooenable hello расширение отдельно с помощью средств, таких как Visual Studio или PowerShell.
* toosimplify hello процесс настройки расширения системы диагностики hello с помощью PowerShell, hello выходные данные пакета Visual Studio также содержит hello открытый XML-ФАЙЛ конфигурации для модуля диагностики hello для каждой роли. Visual Studio использует hello диагностики данные строки подключения toopopulate hello хранилища учетной записи в открытой конфигурации hello. файлы общедоступной конфигурации Hello создаются в папке расширений hello и следовать шаблону hello PaaSDiagnostics. <RoleName>. PubConfig.xml. Любые развертывания на основе PowerShell можно использовать этот шаблон toomap tooa каждой конфигурации роли.
* Hello строку подключения в cscfg-файле hello также используется hello Azure портала tooaccess hello диагностических данных, он может присутствовать в hello **мониторинг** строка подключения вкладку hello: необходимые tooconfigure hello службы tooshow подробных сведений Наблюдение за данными hello портала.

#### <a name="migrating-projects-tooazure-sdk-26-and-later"></a>Перенос проектов tooAzure SDK версии 2.6 и более поздних версий
При миграции из пакета Azure SDK 2.5 tooAzure SDK 2.6 или более поздней версии, если у вас есть учетная запись хранения диагностики, указанной в wadcfgx-файле hello, затем она останется там. преимущества tootake hello гибкость использования различных хранилища учетных записей для различных конфигураций хранилища, необходимо добавить проект tooyour строка подключения hello toomanually. При миграции проекта из пакета Azure SDK 2.4 или более ранних tooAzure SDK 2.6, затем hello диагностики сохраняются строки подключения. Тем не менее Обратите внимание, как строки подключения обрабатываются в пакете Azure SDK 2.6, указанное в предыдущем разделе hello изменения hello.

#### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Определение учетной записи хранения диагностики hello в Visual Studio
* Если строка подключения диагностики указана в cscfg-файле hello, Visual Studio использует его расширение диагностики hello tooconfigure при публикации, а также при создании XML-файлов общедоступной конфигурации hello во время упаковки.
* Если строка подключения диагностики указана в cscfg-файле hello, затем Visual Studio возвращается toousing hello указанную учетную запись хранения в hello .wadcfgx tooconfigure hello диагностики расширение файла при публикации и создания открытого hello XML-файлов конфигурации при упаковке.
* Строка подключения диагностики Hello в cscfg-файле hello имеет приоритет над hello учетной записи хранения в wadcfgx-файле hello. Если строка подключения диагностики указано в cscfg-файле hello, затем Visual Studio использует эти данные и игнорирует hello учетной записи хранения в wadcfgx-файле.

#### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>Что does Здравствуйте, «Обновить строки подключения хранилища разработки...» "Обновлять строки подключения хранилища разработки..."?
Здравствуйте, флажок для **обновить строки подключения хранилища разработки для диагностики и кэширования учетные данные учетной записи хранения Microsoft Azure при публикации tooMicrosoft Azure** предоставляет удобный способ tooupdate любое Учетная запись строки подключения хранилища разработки с помощью учетной записи хранилища Azure hello, указанной во время публикации.

Например, предположим, этот флажок установлен, и строка подключения диагностики hello указывает `UseDevelopmentStorage=true`. При публикации проекта tooAzure hello, Visual Studio автоматически обновит строки подключения диагностики hello hello учетную запись хранилища, заданных в мастере публикации hello. Тем не менее если как строка подключения диагностики hello была указана реальная учетная запись хранения, то этой учетной записи будет использоваться вместо этого.

### <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Функциональные различия диагностики в Azure SDK между более ранними (до 2.4 включительно) и более поздними (с 2.5 включительно) версиями
Если вы осуществили обновление проекта Azure SDK 2.4 tooAzure SDK 2.5 или более поздней версии, следует иметь в виду hello после диагностики функциональные различия.

* **API конфигурации больше не используются.** Программная конфигурация диагностики доступна в пакете SDK для Azure 2.4 и более ранних версий, но в дальнейших выпусках, начиная с версии SDK для Azure 2.5, она не используется. Если конфигурация системы диагностики определена в коде, вам потребуется tooreconfigure эти параметры с нуля в hello перенесенном проекте для работы tookeep диагностики. файл конфигурации диагностики Hello для Azure SDK 2.4 — diagnostics.wadcfg, а diagnostics.wadcfgx Azure SDK 2.5 и более поздних версий.
* **Диагностика для приложений облачных служб можно задавать только на уровне роли hello, а не на уровне экземпляра hello.**
* **Каждый раз при развертывании приложения hello конфигурация системы диагностики обновляется** — это может вызвать проблемы с контролем четности, если изменить конфигурацию диагностики из обозревателя серверов и затем повторно развернуть приложение.
* **В пакете Azure SDK 2.5 и более поздних версиях аварийные дампы настраиваются в файле конфигурации диагностики hello не в коде** — Если аварийные дампы настроены в коде, потребуется toomanually передачи hello конфигурации из файла конфигурации toohello кода Поскольку hello аварийные дампы не перемещаются во время миграции hello tooAzure SDK 2.6.

