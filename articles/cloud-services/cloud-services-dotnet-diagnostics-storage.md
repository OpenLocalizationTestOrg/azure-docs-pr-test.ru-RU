---
title: "aaaStore и просмотра диагностических данных в хранилище Azure | Документы Microsoft"
description: "Получение и просмотр диагностических данных Azure в хранилище Azure"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a>Хранение и просмотр диагностических данных в хранилище Azure
Если передача toohello эмулятор хранилища Microsoft Azure или tooAzure хранилища диагностических данных не хранится без возможности восстановления. Поместив данные в хранилище, вы можете просматривать их с помощью одного из нескольких доступных средств.

## <a name="specify-a-storage-account"></a>Определение учетной записи хранения
Можно указать hello хранилища учетной записи, которую toouse в файле ServiceConfiguration.cscfg hello. сведения об учетной записи Hello определяется как строка подключения в параметре конфигурации. Hello ниже приведен пример создания нового проекта облачной службы в Visual Studio строка подключения по умолчанию hello.

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

Можно изменить данные этой строки соединения tooprovide учетной записи для учетной записи хранилища Azure.

В зависимости от типа диагностических данных, собираемых hello Диагностика Azure использует hello BLOB-объектов или службе таблиц hello. Hello следующей таблице показаны сохраняемые источники данных hello и их формат.

| Источник данных | Формат хранения |
| --- | --- |
| Журналы Azure |Таблица |
| Журналы IIS 7.0 |BLOB-объект |
| Журналы инфраструктуры системы диагностики Azure |Таблица |
| Журналы трассировки невыполненных запросов |BLOB-объект |
| Журналы событий Windows |Таблица |
| Счетчики производительности |Таблица |
| Аварийные дампы |BLOB-объект |
| Пользовательские журналы ошибок |BLOB-объект |

## <a name="transfer-diagnostic-data"></a>Передача диагностических данных
Для пакета SDK 2.5 и более поздних версиях hello запроса tootransfer диагностических данных может произойти через файл конфигурации hello. Данные диагностики можно переносить через запланированные промежутки времени, как указано в конфигурации hello.

Для пакета SDK 2.4 и предыдущим можно запросить tootransfer hello диагностических данных через hello файл конфигурации, а также программным способом. Hello программный подход также позволяет toodo передачи по запросу.

> [!IMPORTANT]
> При передаче диагностических данных tooan учетной записи хранилища Azure, вас взимается плата за ресурсы хранилища hello, используемые вашими диагностическими данными.
> 
> 

## <a name="store-diagnostic-data"></a>Хранение диагностических данных
Данные журнала хранятся в хранилище BLOB-объекта или таблицы с hello следующие имена:

**Таблицы**

* **WadLogsTable** - журналы, записываемые в коде с помощью прослушивателя трассировки hello.
* **WADDiagnosticInfrastructureLogsTable** : сведения об изменениях конфигурации и монитора диагностики.
* **WADDirectoriesTable** — каталоги наблюдает монитор диагностики, hello.  Сюда входят журналы IIS, журналы неудачно завершенных запросов IIS и пользовательские папки.  в поле RelativePath hello Hello расположение файла журнала большого двоичного объекта hello указано в поле hello контейнера и имя hello hello большого двоичного объекта.  поле AbsolutePath Hello указывает hello расположение и имя файла hello, находившимся hello виртуальной машины Azure.
* **WADPerformanceCountersTable** : данные счетчиков производительности.
* **WADWindowsEventLogsTable** : журналы событий Windows.

**BLOB-объекты**

* **wad-control-container** — (только для SDK 2.4 и предыдущих) содержит файлы конфигурации XML hello, управляющие hello диагностики Azure.
* **wad-iis-failedreqlogfiles** : содержит сведения журналов неудачно завершенных запросов IIS.
* **wad-iis-logfiles** : содержит сведения о журналах IIS.
* **«custom»** — пользовательский контейнер, основанный на каталогах, которые отслеживаются монитором диагностики hello настройки.  Hello имя этого контейнера больших двоичных объектов указываются в элементе WADDirectoriesTable.

## <a name="tools-tooview-diagnostic-data"></a>Средства tooview диагностических данных
Несколько инструментов, доступных tooview hello данных после toostorage переносятся. Например:

* Обозреватель серверов в Visual Studio — Если вы установили hello Azure Tools для Microsoft Visual Studio, можно использовать узел хранилища Azure hello в обозревателе серверов tooview только для чтения больших двоичных объектов и таблиц данных из учетных записей хранилища Azure. Вы можете отображать данные из своей локальной учетной записи эмулятора хранения, а также из учетных записей хранения, созданных для Azure. Дополнительные сведения см. в статье [Обзор ресурсов хранилища с помощью обозревателя сервера и управление ими](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).
* [Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) имеет отдельное приложение, позволяющее tooeasily работы с данными хранилища Azure для Windows, OSX и Linux.
* [Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) включает в себя Azure Diagnostics Manager служащее tooview, загрузки и управления ими hello диагностические данные, собранные hello приложений, работающих в Azure.

## <a name="next-steps"></a>Дальнейшие действия
[Поток hello трассировки в приложении облачные службы с помощью системы диагностики Azure](cloud-services-dotnet-diagnostics-trace-flow.md)

