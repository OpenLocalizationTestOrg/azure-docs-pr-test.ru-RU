---
title: "Контрольный список безопасности базы данных aaaAzure | Документы Microsoft"
description: "В этой статье представлен контрольный список для обеспечения безопасности баз данных Azure."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: 5e3a69591df3c8508a8707a2d47068342863ce93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-checklist"></a>Контрольный список для обеспечения безопасности баз данных

toohelp повысить безопасность, база данных Azure включает ряд встроенных средств безопасности элементов управления, можно использовать toolimit и управления доступом.

В частности, описаны такие возможности:

-   Межсетевой экран, который позволяет toocreate [правила брандмауэра](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) ограничение подключение по IP-адресу
-   Доступен из портала Azure hello брандмауэра на уровне сервера
-   правила брандмауэра уровня базы данных, доступные в SSMS;
-   Базы данных tooyour безопасного подключения к сети, с помощью безопасного подключения
-   управление доступом;
-   Шифрование данных
-   аудит баз данных SQL;
-   обнаружение угроз для баз данных SQL.

## <a name="introduction"></a>Введение
Облачные вычисления требуется новый принципов безопасности пользователи знакомы toomany приложения, администраторы баз данных и программистам. В результате некоторые организации, не решаться tooimplement облачной инфраструктуры для управления данными из-за tooperceived угрозы безопасности. Большая часть этой проблемы можно облегчено через лучше понять возможности безопасности hello, встроенные в Microsoft Azure и базы данных SQL Microsoft Azure.

## <a name="checklist"></a>Контрольный список
Рекомендуется прочитать hello [рекомендации по обеспечению безопасности базы данных Azure](https://docs.microsoft.com/en-us/azure/security/azure-database-security-best-practices) статью предыдущих tooreviewing этот контрольный список. Поняв hello рекомендации, будет hello tooget может наиболее эффективно использовать этот контрольный список. Затем можно использовать этот контрольный список toomake том, что вы рассмотрели hello важные проблемы в системе безопасности базы данных SQL Azure.


|Категория контрольного списка| Описание|
| ------------ | -------- |
|**Защита данных**||
| <br> Шифрование данных при передаче| <ul><li>[Безопасность транспортного уровня](https://docs.microsoft.com/en-us/windows-server/security/tls/transport-layer-security-protocol), для шифрования данных при toohello сети это перенос данных.</li><li>Базы данных требуют безопасного соединения от клиентов, в зависимости от hello [TDS (поток табличных данных)](https://msdn.microsoft.com/en-in/library/dd357628.aspx) протокол TLS (Безопасность на уровне транспорта).</li></ul> |
|<br>Шифрование при хранении| <ul><li>[Прозрачное шифрование данных](http://go.microsoft.com/fwlink/?LinkId=526242). Используется при физическом хранении неактивных данных в любом цифровом виде.</li></ul>|
|**Контроль доступа**||  
|<br> Доступ к базе данных | <ul><li>[Аутентификация](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access) (Аутентификация Azure Active Directory). Используются удостоверения, управляемые Azure Active Directory.</li><li>[Авторизация](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access) предоставить пользователям hello наименьшими необходимыми правами.</li></ul> |
|<br>Доступ к приложениям| <ul><li>[Безопасность на уровне строк](https://msdn.microsoft.com/library/dn765131) (с помощью политики безопасности, в то же время, ограничения доступа на уровне строк на основе пользователя удостоверения, роли или выполнения контекста hello).</li><li>[Динамическое маскирование данных](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-dynamic-data-masking-get-started) (с помощью разрешений и политики, ограничивает возможность раскрытия конфиденциальных данных счет маскирования toonon пользователей)</li></ul>|
|**Упреждающий мониторинг**||  
| <br>Отслеживание и обнаружение| <ul><li>[Аудит](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing) отслеживает события базы данных и записывает их в журнал аудита tooan или в журнале активности вашей [учетной записи хранилища Azure](https://docs.microsoft.com/en-us/azure/storage/storage-create-storage-account).</li><li>Отслеживание работоспособности базы данных Azure с помощью [журналов действий Azure Monitor](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs).</li><li>[Обнаружение угроз](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-threat-detection) обнаруживает аномальные действия базы данных, указывающее базу данных toohello потенциальные угрозы безопасности. </li></ul> |
|<br>Центр безопасности Azure| <ul><li>[Мониторинг данных](https://docs.microsoft.com/en-us/azure/security-center/security-center-enable-auditing-on-sql-databases). Используйте центр безопасности Azure как централизованное решение мониторинга безопасности для SQL и других служб Azure.</li></ul>|     

## <a name="conclusion"></a>Заключение
База данных Azure — это надежная платформа базы данных с полным набором функций безопасности, которые удовлетворяют многим организационным и нормативным требованиям. Данные можно с легкостью защитить, управление hello физический доступ tooyour данных и с помощью различных вариантов для защиты данных в файл hello-, столбца или уровня строк с помощью прозрачного шифрования данных, шифрование на уровне ячейки или безопасность на уровне строк. Всегда Encrypted также позволяет операций, выполняемых зашифрованные данные, что упрощает процесс обновления приложения hello. В свою очередь журналы событий tooauditing действия базы данных SQL предоставляет hello необходимые сведения, позволяя tooknow, как и при доступе к данным.

## <a name="next-steps"></a>Дальнейшие действия
Можно улучшить защиту hello базы данных на соответствие пользователей-злоумышленников или несанкционированного доступа с помощью нескольких простых шагов. Из этого руководства вы узнаете, как выполнять такие задачи.

- Настройка [правил брандмауэра](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) для сервера и (или) базы данных.
- Защита данных с помощью [шифрования](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/sql-server-encryption).
- Включение [аудита базы данных SQL](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing).

