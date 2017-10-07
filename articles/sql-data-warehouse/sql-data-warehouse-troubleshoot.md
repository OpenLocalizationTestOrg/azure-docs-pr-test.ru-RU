---
title: "aaaTroubleshooting хранилище данных SQL Azure | Документы Microsoft"
description: "Диагностика и устранение неполадок хранилища данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 51f1e444-9ef7-4e30-9a88-598946c45196
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/30/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 3c53a39f77057fe0bcc053a0b896555abf397515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-sql-data-warehouse"></a>Устранение неполадок хранилища данных SQL Azure
Этом разделе перечислены некоторые из hello более часто задаваемые вопросы по устранению неполадок, мы получаем от наших клиентов.

## <a name="connecting"></a>Подключение
| Проблема | Способы устранения: |
|:--- |:--- |
| Ошибка входа пользователя "NT AUTHORITY\ANONYMOUS LOGON". (Microsoft SQL Server, ошибка: 18456) |Эта ошибка возникает, когда пользователь AAD пытается базы данных master toohello tooconnect, но не имеет пользователь в базе данных master.  эту проблему, либо указать toocorrect hello хранилище данных SQL необходимо время подключения tooat tooconnect или добавить базы данных master toohello hello пользователя.  Дополнительные сведения см. в статье [Защита базы данных в хранилище данных SQL][Security overview]. |
| Hello сервера участника «MyUserName» не может tooaccess hello базы данных «master» в текущем контексте безопасности hello. Не удается открыть пользовательскую базу данных по умолчанию. Вход в систему не выполнен. Пользователю "MyUserName" не удалось войти в систему. (Microsoft SQL Server, ошибка: 916) |Эта ошибка возникает, когда пользователь AAD пытается базы данных master toohello tooconnect, но не имеет пользователь в базе данных master.  эту проблему, либо указать toocorrect hello хранилище данных SQL необходимо время подключения tooat tooconnect или добавить базы данных master toohello hello пользователя.  Дополнительные сведения см. в статье [Защита базы данных в хранилище данных SQL][Security overview]. |
| Ошибка CTAIP |Эта ошибка может возникать при создании имени входа на hello главной базы данных SQL server, но не в базе данных хранилища данных SQL hello.  Если эта ошибка возникает, взгляните на hello [Общие сведения о безопасности] [ Security overview] статьи.  В этой статье объясняется, как toocreate создать имя входа и пользователя образец, а затем как toocreate пользователь в hello базы данных хранилища данных SQL. |
| Заблокировано брандмауэром |Базы данных SQL Azure, защищены с помощью tooensure брандмауэров уровня сервера и базы данных, известен только IP-адресов, которые имеют доступ к базе данных tooa. брандмауэры Hello являются безопасными по умолчанию, это означает, что необходимо явно включить и IP-адреса или диапазона адресов, перед подключением.  tooconfigure брандмауэра для доступа, следуйте шагам hello в [Настройка доступа к серверу брандмауэра для IP-адрес вашего клиента] [ Configure server firewall access for your client IP] в hello [подготовки инструкции] [Provisioning instructions]. |
| Не удается подключиться с помощью средства или драйвера |Хранилище данных SQL Корпорация Майкрософт рекомендует использовать [SSMS][SSMS], [SSDT для Visual Studio][SSDT for Visual Studio], или [sqlcmd] [ sqlcmd] tooquery данных. Дополнительные сведения о драйверы и tooSQL подключения хранилища данных. в разделе [драйверы для хранилища данных SQL Azure] [ Drivers for Azure SQL Data Warehouse] и [подключения хранилища данных SQL tooAzure] [ Connect tooAzure SQL Data Warehouse] статей. |

## <a name="tools"></a>Средства
| Проблема | Способы устранения: |
|:--- |:--- |
| В обозревателе объектов Visual Studio отсутствуют пользователи AAD |Это известная проблема.  Чтобы избежать этого, просмотра сведений о пользователях hello в [sys.database_principals][sys.database_principals].  В разделе [tooAzure проверки подлинности хранилища данных SQL] [ Authentication tooAzure SQL Data Warehouse] toolearn о применении с хранилищем данных SQL Azure Active Directory. |
|Руководства, сценарии, с помощью мастера создания скриптов hello или подключении с помощью SSMS — медленным, зависших или создание ошибки| Убедитесь, что пользователи были созданы в базе данных master hello. В параметрах создания скриптов также убедитесь в том, что выпуск ядра hello задано как «Microsoft Azure выпуск хранилища данных SQL» и тип компонента ядра СУБД — «Microsoft Azure SQL Database».|

## <a name="performance"></a>Производительность
| Проблема | Способы устранения: |
|:--- |:--- |
| Устранение проблем с производительностью запросов |Если вы пытаетесь tootroubleshoot конкретного запроса, начните с [обучения как toomonitor запросы][Learning how toomonitor your queries]. |
| Низкая производительность и неправильные планы запросов в результате отсутствия статистики |Hello наиболее распространенной причиной снижения производительности — отсутствие статистики на ваших таблицах.  . В разделе [статистики таблицы] [ Statistics] подробные сведения о том, как toocreate статистики и почему они являются критические tooyour производительности. |
| Низкий уровень параллелизма и помещение запросов в очередь |Основные сведения о [управления рабочей нагрузкой] [ Workload management] важен в порядке toounderstand как выделение памяти toobalance с параллелизмом. |
| Как tooimplement советы и рекомендации |Hello наилучшую производительность запросов tooimprove способов месте toostart toolearn — [рекомендации по хранилищу данных SQL] [ SQL Data Warehouse best practices] статьи. |
| Как tooimprove производительность при масштабировании |Иногда производительность tooimproving hello решения является toosimply Добавление дополнительных вычислительных операций запросов tooyour power [масштабирование хранилище данных SQL][Scaling your SQL Data Warehouse]. |
| Низкая производительность запросов как результат низкого качества индексов |Иногда выполнение запросов может замедляться из-за [низкого качества индекса columnstore][Poor columnstore index quality].  Дополнительные сведения см. в разделе и каким образом слишком[перестроения индексов качества сегмента tooimprove][Rebuild indexes tooimprove segment quality]. |

## <a name="system-management"></a>Управление системой
| Проблема | Способы устранения: |
|:--- |:--- |
| Msg 40847: Не удалось выполнить операцию hello, так как сервер достиг hello допускается 45000 квоты единицы транзакции базы данных. |Либо уменьшите hello [DWU] [ DWU] hello базы данных, которому вы пытаетесь toocreate или [запросить увеличение квоты][request a quota increase]. |
| Анализ использования пространства |В разделе [таблице размеров] [ Table sizes] toounderstand использования места hello системы. |
| Справка по управлению таблицами |В разделе hello [Общие сведения о таблицах] [ Overview] статьи для получения справки по управления таблицами.  Дополнительные сведения см. в статьях, посвященных [типам данных таблиц][Data types], [распределению][Distribute], [индексированию][Index], [секционированию][Partition], [управлению статистикой таблиц][Statistics] и [временным таблицам][Temporary]. |
|Прозрачное шифрование индикатор не обновляется в hello портала Azure|Можно просмотреть состояние hello прозрачного шифрования данных через [powershell](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption).|

## <a name="polybase"></a>PolyBase
| Проблема | Способы устранения: |
|:--- |:--- |
| Ошибка загрузки из-за большого размера строк |В настоящее время для Polybase не поддерживаются строки большого размера.  Это означает, что если таблица содержит VARCHAR(MAX), NVARCHAR(MAX) или VARBINARY(MAX), внешние таблицы не может быть tooload используемых данных.  Загружает для больших строк в данный момент поддерживаются только посредством фабрики данных Azure (с помощью программы BCP), Azure Stream Analytics, службы SSIS, BCP или класс .NET SQLBulkCopy hello. Поддержка строк большого размера для PolyBase будет добавлена в будущем выпуске. |
| Ошибка загрузки таблицы с типом данных MAX с использованием BCP |Имеется известная проблема, в которой должны располагаться, VARCHAR(MAX), NVARCHAR(MAX) или VARBINARY(MAX) в конце hello таблицы hello в некоторых сценариях.  Попробуйте переместить ваш MAX столбцы toohello конец hello таблицы. |

## <a name="differences-from-sql-database"></a>Отличия от базы данных SQL
| Проблема | Способы устранения: |
|:--- |:--- |
| Неподдерживаемые функции базы данных SQL |Ознакомьтесь с разделом [Неподдерживаемые функции таблиц][Unsupported table features]. |
| Неподдерживаемые типы данных базы данных SQL |Ознакомьтесь с разделом [Неподдерживаемые типы данных][Unsupported data types]. |
| Ограничения относительно инструкций DELETE и UPDATE |В разделе [обходные пути обновления][UPDATE workarounds], [удалить обходные пути] [ DELETE workarounds] и [toowork с помощью CTAS вокруг не поддерживается обновление и Синтаксис инструкции DELETE][Using CTAS toowork around unsupported UPDATE and DELETE syntax]. |
| Инструкция MERGE не поддерживается |Ознакомьтесь с [обходными решениями для инструкции MERGE][MERGE workarounds]. |
| Ограничения хранимых процедур |В разделе [хранимой процедуры ограничения] [ Stored procedure limitations] toounderstand некоторые ограничения hello хранимых процедур. |
| Определяемые пользователем функции не поддерживают инструкции SELECT |Это текущее ограничение определяемых пользователем функций.  В разделе [CREATE FUNCTION] [ CREATE FUNCTION] Корпорация Майкрософт поддерживает синтаксис hello. |

## <a name="next-steps"></a>Дальнейшие действия
Если были невозможно toofind tooyour решение проблемы выше, ниже приведены некоторые ресурсы, можно попробовать.

* [Блоги]
* [Запросы функций]
* [Видеоролики]
* [Блоги группы CAT]
* [Создание запроса в службу поддержки]
* [Форум MSDN]
* [Форум Stack Overflow]
* [Twitter]

<!--Image references-->

<!--Article references-->
[Security overview]: ./sql-data-warehouse-overview-manage-security.md
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx
[SSDT for Visual Studio]: ./sql-data-warehouse-install-visual-studio.md
[Drivers for Azure SQL Data Warehouse]: ./sql-data-warehouse-connection-strings.md
[Connect tooAzure SQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Создание запроса в службу поддержки]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Scaling your SQL Data Warehouse]: ./sql-data-warehouse-manage-compute-overview.md
[DWU]: ./sql-data-warehouse-overview-what-is.md
[request a quota increase]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Learning how toomonitor your queries]: ./sql-data-warehouse-manage-monitor.md
[Provisioning instructions]: ./sql-data-warehouse-get-started-provision.md
[Configure server firewall access for your client IP]: ./sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[Table sizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries
[Unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuild indexes tooimprove segment quality]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Using CTAS toowork around unsupported UPDATE and DELETE syntax]: ./sql-data-warehouse-develop-ctas.md#using-ctas-to-work-around-unsupported-features
[UPDATE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[DELETE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[MERGE workarounds]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[Stored procedure limitations]: ./sql-data-warehouse-develop-stored-procedures.md#limitations
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md
[Working around hello PolyBase UTF-8 requirement]: ./sql-data-warehouse-load-polybase-guide.md#working-around-the-polybase-utf-8-requirement

<!--MSDN references-->
[sys.database_principals]: https://msdn.microsoft.com/library/ms187328.aspx
[CREATE FUNCTION]: https://msdn.microsoft.com/library/mt203952.aspx
[sqlcmd]: https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-get-started-connect-sqlcmd/

<!--Other Web references-->
[Блоги]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[Блоги группы CAT]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Запросы функций]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Форум MSDN]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse
[Форум Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Видеоролики]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
