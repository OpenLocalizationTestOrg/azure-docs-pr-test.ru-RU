---
title: "источники aaaData, поддерживаемые в Azure Analysis Services | Документы Microsoft"
description: "Описание источников данных, поддерживаемых для моделей данных в службах Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 6ec63319-ff9b-4b01-a1cd-274481dc8995
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2902d7d3c3bcf086419822fa826193bd247bde61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="data-sources-supported-in-azure-analysis-services"></a>Источники данных, поддерживаемые в службах Azure Analysis Services
Azure серверов служб Analysis Services поддерживают подключения toodata в hello облака и локально в вашей организации. Дополнительные поддерживаемые источники данных добавляются все время hello. Следите за обновлениями. 

в настоящее время поддерживаются следующие источники данных Hello:

| Облако  |
|---|
| Хранилище BLOB-объектов Azure*  |
| База данных SQL Azure  |
| Хранилище данных Azure |


| Локальная система  |   |   |   |
|---|---|---|---|
| База данных Access  | Папка* | База данных Oracle  | База данных Teradata |
| Active Directory*  | Документ JSON*  | База данных SQL Postgre*  |Таблица XML* |
| службы Analysis Services  | Строки из двоичного файла*  | SAP HANA*  |
| Система платформы аналитики  | База данных MySQL  | SAP Business Warehouse*  | |
| Dynamics CRM*  | Веб-канал OData*  | SharePoint*  |
| Книга Excel  | Запрос ODBC  | База данных SQL  |
| Exchange*  | OLE DB  | База данных Sybase  |

\* Только для табличных моделей 1400. 

> [!IMPORTANT]
> Подключения требуются источники данных локальной tooon [локального шлюза данных](analysis-services-gateway.md) установлен на компьютере в вашей среде.

## <a name="data-providers"></a>Поставщики данных

При подключении toocertain источники данных, моделей данных в Azure Analysis Services может потребоваться разных поставщиков данных. В некоторых случаях подключение toodata источников, используя собственные поставщики, например, собственный клиент SQL Server (SQLNCLI11) табличные модели могут возвращать ошибку.

Для моделей данных, подключение данных облака tooa источника таких как базы данных SQL Azure, если вы используете собственные поставщики, отличные от SQLOLEDB, может появиться сообщение об ошибке: **«hello provider «SQLNCLI11.1» не зарегистрирован».** Или, при наличии подключения tooon локальные источники данных, модели DirectQuery, при использовании собственные поставщики, может появиться сообщение об ошибке: **«ошибка при создании набора строк OLE DB. Incorrect syntax near 'LIMIT'"** (Ошибка при создании набора строк OLE DB. Неверный синтаксис рядом с "LIMIT").

следующие поставщики datasource Hello поддерживается в памяти или данных модели DirectQuery при подключении toodata источники в облаке hello или локальной:

### <a name="cloud"></a>Облако
| **Источник данных** | **В памяти** | **DirectQuery** |
|  --- | --- | --- |
| Хранилище данных SQL Azure |Поставщик данных .NET Framework для SQL Server |Поставщик данных .NET Framework для SQL Server |
| База данных SQL Azure |Поставщик данных .NET Framework для SQL Server |Поставщик данных .NET Framework для SQL Server | |

### <a name="on-premises-via-gateway"></a>Локально (через шлюз)
|**Источник данных** | **В памяти** | **DirectQuery** |
|  --- | --- | --- |
| SQL Server |SQL Server Native Client 11.0 |Поставщик данных .NET Framework для SQL Server |
| SQL Server |Поставщик Microsoft OLE DB для SQL Server |Поставщик данных .NET Framework для SQL Server | |
| SQL Server |Поставщик данных .NET Framework для SQL Server |Поставщик данных .NET Framework для SQL Server | |
| Oracle |Поставщик Microsoft OLE DB для Oracle |Поставщик данных Oracle для .NET | |
| Oracle |Поставщик данных Oracle для .NET |Поставщик данных Oracle для .NET | |
| Teradata |Поставщик OLE DB для Teradata |Поставщик данных Teradata для .NET | |
| Teradata |Поставщик данных Teradata для .NET |Поставщик данных Teradata для .NET | |
| Система платформы аналитики |Поставщик данных .NET Framework для SQL Server |Поставщик данных .NET Framework для SQL Server | |

> [!NOTE]
> При использовании локального шлюза убедитесь, что установлены 64-разрядные версии поставщиков.
> 
> 

При миграции локальных tooAzure табличной модели служб аналитики SQL Server Analysis Services, может быть необходимости toochange hello поставщика.

**toospecify поставщик источника данных**

1. В разделе SSDT > **Tabular Model Explorer (Обозреватель табличных моделей)** > **Data Sources (Источники данных)** щелкните правой кнопкой подключение к источнику данных и выберите **Edit Data Source (Изменить источник данных)**.
2. В **изменить соединение**, нажмите кнопку **Дополнительно** окно свойств авансового tooopen hello.
3. В **задание дополнительных свойств** > **поставщики**, а затем выберите hello соответствующий поставщик.

## <a name="impersonation"></a>Олицетворение
В некоторых случаях возможно необходимые toospecify олицетворение другой учетной записи. Учетную запись олицетворения можно указать в SSDT или SSMS.

Для локальных источников данных:

* При использовании проверки подлинности SQL олицетворением должна быть учетная запись службы.
* При использовании проверки подлинности Windows задайте пользователя и пароль Windows. Для SQL Server проверка подлинности Windows с использованием конкретной учетной записи олицетворения поддерживается только для моделей данных в памяти.

Для облачных источников данных

* При использовании проверки подлинности SQL олицетворением должна быть учетная запись службы.

## <a name="next-steps"></a>Дальнейшие действия
При работе с локальным источникам данных, нужно убедиться, что hello tooinstall [локального шлюза](analysis-services-gateway.md).   
toolearn Дополнительные сведения о управление сервером в SSDT и SSMS, в разделе [Управление данным сервером](analysis-services-manage.md).

