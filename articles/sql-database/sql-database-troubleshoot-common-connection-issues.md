---
title: "проблемы tooAzure aaaTroubleshoot общие подключения базы данных SQL"
description: "Действия tooidentify и устранение общих ошибок подключения для базы данных SQL Azure."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: ac463d1c-aec8-443d-b66e-fa5eadcccfa8
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: eb5f2d7b123a76942c7e4a84a7f475344fbcb144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connection-issues-tooazure-sql-database"></a>Устранение проблем подключения tooAzure базы данных SQL
При сбое tooAzure hello подключения базы данных SQL, вы получаете [сообщения об ошибках](sql-database-develop-error-messages.md). Эта статья представляет собой объединенный раздел, который поможет в устранении неполадок подключения к базе данных SQL Azure. Представляет [hello основные причины](#cause) проблем подключения рекомендует [средством устранения неполадок](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues) , помогает удостоверение hello проблему и предоставляет по устранению неполадок toosolve действия [ временные ошибки](#troubleshoot-transient-errors) и [постоянный или не является временной ошибки](#troubleshoot-persistent-errors). 

Если возникли проблемы с подключением hello, попробуйте hello устранения действия, описанные в этой статье.
[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="cause"></a>Причина:
Проблемы подключения может быть вызвано любой из следующих hello:

* Сбой tooapply, рекомендации и советы по разработке во время разработки приложения hello.  В разделе [Общие сведения о разработке базы данных SQL](sql-database-develop-overview.md) tooget работы.
* Перенастройка базы данных SQL Azure.
* Параметры брандмауэра
* Время ожидания подключения.
* Неправильные сведения для входа.
* Достигнуто максимальное ограничение для некоторых ресурсов базы данных SQL Azure.

Как правило tooAzure проблемы подключения базы данных SQL можно классифицировать следующим образом:

* [временные ошибки (кратковременные или возникающие периодически);](#troubleshoot-transient-errors)
* [постоянные или регулярно возникающие ошибки.](#troubleshoot-persistent-errors)

## <a name="try-hello-troubleshooter-for-azure-sql-database-connectivity-issues"></a>Повторите hello средство устранения неполадок проблем подключения к базе данных SQL Azure
При возникновении определенной ошибки подключения попробуйте [этот инструмент](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database), который поможет быстро выявить и устранить проблему.

## <a name="troubleshoot-transient-errors"></a>Устранение временных ошибок

При подключении базы данных Azure SQL tooan приложения, появляется сообщение об ошибке после hello:

```
Error code 40613: "Database <x> on server <y> is not currently available. Please retry hello connection later. If hello problem persists, contact customer support, and provide them hello session tracing ID of <z>"
```

> [!NOTE]
> Это сообщение об ошибке обычно временное (кратковременное).
> 
> 

Эта ошибка возникает при hello Azure база данных перемещена (или повторно настраивается) и приложение теряет свою базу данных SQL toohello соединения. События перенастройки базы данных SQL обычно происходят в запланированном случае (например, при обновлении программного обеспечения) или в незапланированном случае (например, при сбое процесса или балансировке нагрузки). Большей частью события перенастройки кратковременные и должны завершаться в течение 60 секунд максимум. Тем не менее эти события иногда может потребоваться toofinish больше времени, например когда большой транзакции приводит восстановления длительное время.

### <a name="steps-tooresolve-transient-connectivity-issues"></a>Действия tooresolve временных неполадок

1. Проверьте hello [панель мониторинга службы Microsoft Azure](https://azure.microsoft.com/status) для любого известных сбоев, произошедших во время hello, во время которого hello ошибки приложения hello.
2. Приложения, которые подключаются tooa облачной службы, такие как базы данных SQL Azure следует ожидать события периодических перенастройки и реализовать повторите toohandle логику эти ошибки, а не отображает их в качестве toousers ошибок приложения. Просмотрите hello [временных ошибок](sql-database-connectivity-issues.md) раздел и hello рекомендации и правила в разработки [Общие сведения о разработке базы данных SQL](sql-database-develop-overview.md) Дополнительные сведения и общие стратегиями повтора. Затем ознакомьтесь с примерами кода в [библиотеке подключений для базы данных SQL и SQL Server](sql-database-libraries.md).
3. По мере приближения его ограничения ресурсов базы данных может показаться toobe временная ошибка подключения. См. статью [Советы по настройке производительности базы данных SQL](sql-database-troubleshoot-performance.md).
4. Если продолжить проблемы с подключением, либо если hello длительность, для которой приложения, возникает ошибка hello превышает 60 секунд или несколько вхождений hello ошибки содержатся в конкретный день, файл запрос поддержки Azure, выбрав **получения поддержки** на hello [поддержки Azure](https://azure.microsoft.com/support/options) сайта.

## <a name="troubleshoot-persistent-errors"></a>Устранение постоянных ошибок
Если tooconnect tooAzure базы данных SQL постоянно происходит сбой приложения hello, обычно указывает на проблему с одним из следующих hello:

* Конфигурация брандмауэра. Azure SQL Hello базы данных или на клиентском компьютере брандмауэр блокирует подключения tooAzure базы данных SQL.
* Сетевые изменения конфигурации на стороне клиента hello: например, новый IP-адрес или прокси-сервер.
* Ошибка пользователя: например, ошибки при вводе параметры соединения, такие как имя сервера hello в строке подключения hello.

### <a name="steps-tooresolve-persistent-connectivity-issues"></a>Проблемы постоянного подключения tooresolve действия
1. Настройка [правила брандмауэра](sql-database-configure-firewall-settings.md) tooallow hello клиентского IP-адреса. Для временного тестирования можно настройте правило брандмауэра с помощью 0.0.0.0 как hello начиная диапазон IP-адресов, с помощью 255.255.255.255 как hello конечный диапазон IP-адресов. При этом откроется hello server tooall IP-адресов. Если это позволяет устранить проблемы с подключением, удалите это правило и создайте правило брандмауэра для надлежащим образом ограниченных IP-адресов или диапазона адресов. 
2. Убедитесь, что открыт порт 1433 для исходящих соединений на все брандмауэры между клиентом hello и hello Интернета. Просмотрите [Настройка брандмауэра Windows hello tooAllow доступа к SQL Server](https://msdn.microsoft.com/library/cc646023.aspx) и [гибридное удостоверение необходимые порты и протоколы](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports) для дополнительных указателей связанных tooadditional порты, необходимые tooopen для Проверка подлинности Azure Active Directory.
3. Проверьте строку подключения и другие параметры подключения. В разделе hello строка подключения раздела hello [разделе проблемы подключения к](sql-database-connectivity-issues.md#connections-to-azure-sql-database).
4. Проверьте работоспособность службы на панели мониторинга hello. Если вы считаете, что региональном сбое, см. раздел [восстановление после сбоя](sql-database-disaster-recovery.md) для новой области действия toorecover tooa.

## <a name="next-steps"></a>Дальнейшие действия
* [Устранение проблем производительности базы данных SQL Azure](sql-database-troubleshoot-performance.md)
* [Поиск документации hello в Microsoft Azure](http://azure.microsoft.com/search/documentation/)
* [Представление hello последние обновления службы toohello базы данных SQL Azure](http://azure.microsoft.com/updates/?service=sql-database)

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Общие сведения о разработке базы данных SQL](sql-database-develop-overview.md)
* [Общие рекомендации по повторным попыткам](../best-practices-retry-general.md)
* [Библиотеки подключений для Базы данных SQL и SQL Server](sql-database-libraries.md)

