---
title: "aaaFix ошибки подключения SQL, временная ошибка | Документы Microsoft"
description: "Узнайте, как tootroubleshoot, диагностика и предотвращение ошибок подключения SQL или временная ошибка в базе данных SQL Azure. "
keywords: "подключение sql,строка подключения,проблемы с подключением, временная ошибка,ошибка подключения"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a>Устранение, диагностика и предотвращение ошибок подключения SQL и временных ошибок для базы данных SQL
В этой статье описывается, как tooprevent, устранение неполадок, диагностики и устранения ошибок подключения и временные ошибки, возникшие клиентского приложения при работе с базой данных SQL Azure. Узнайте, как tooconfigure логику повторных попыток, создать строку соединения hello и настройка других параметров подключения.

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a>Временные ошибки (временные сбои)
Временные ошибки (или временные сбои) возникают из-за причин, которые вскоре устраняются автоматически. Случайные причина временных ошибок — когда hello системы Azure быстро перемещается аппаратных ресурсов toobetter балансировать различных рабочих нагрузок. Большинство этих событий перенастройки часто завершаются менее чем за 60 секунд. В течение этого интервала времени перенастройки имеется подключение выдает tooAzure базы данных SQL. Подключение базы данных SQL должен быть tooAzure построение приложений tooexpect эти временные ошибки дескриптор их, реализовав логику в своем коде, а не отображает их toousers как ошибки приложения повторных попыток.

Если клиентская программа использует ADO.NET, программа укажет о временная ошибка hello throw hello объекта **SqlException**. Hello **номер** свойства можно сравнивать с hello список временных ошибок верхней hello части статьи hello: [коды ошибок SQL для клиентских приложений баз данных SQL](sql-database-develop-error-messages.md).

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a>Подключения и команды
Будет повторять попытки соединения SQL hello или установить ее еще раз, в зависимости от следующих hello:

* **Временная ошибка возникает во время попытки подключения**: hello соединения следует повторить после задержки в течение нескольких секунд.
* **Временная ошибка возникает во время команда SQL-запроса**: hello команду следует повторить не сразу. Вместо этого после задержки, hello должен быть заново установить соединение. Затем можно повторить команду hello.

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a>Повтор логики для временных ошибок
Клиентские программы, в которых иногда происходят временные ошибки, являются более надежными, если используют логику повторных попыток.

Когда программа взаимодействует с базой данных SQL Azure через по промежуточного слоя сторонних производителей, запрос с поставщиком hello ли hello по промежуточного слоя содержит логику повторных попыток для временных ошибок.

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a>Принципы повторных попыток
* Следует повторить tooopen попытки подключения, если ошибка hello является временным.
* Выполнение инструкции SQL SELECT, которая закончилась временным сбоем, не нужно повторять непосредственно.
  
  * Вместо этого установить новое подключение, а затем повторите hello SELECT.
* При неудачном завершении инструкции SQL UPDATE с временной ошибкой перед hello повторная попытка обновления следует установить новое подключение.
  
  * Логика повторных попыток Hello необходимо убедиться, что hello всей базы данных транзакция завершена или что hello всей транзакции выполняется откат.

#### <a name="other-considerations-for-retry"></a>Другие соображения по поводу повторных попыток
* Пакетном, запускается автоматически после окончания рабочего дня и которого будет выполнена до утра, можете toovery пациента с интервалам времени между его повторных попыток.
* Запрос программы должны учитывать возможность toogive человека тенденцию hello копии после слишком много времени ожидания.
  
  * Однако решение hello должен отсутствовать tooretry каждые несколько секунд, так как эта политика может переполнить hello системы вместе с запросами.

#### <a name="interval-increase-between-retries"></a>Увеличение интервала между повторными попытками
Рекомендуется подождать 5 секунд, прежде чем выполнять первую повторную попытку. Повторять после задержки, меньше 5 секунд может просто огромным hello облачной службы. Для каждой последующей повторной попыткой hello задержки должен увеличиваться экспоненциально, копирование tooa максимальное 60 секунд.

Обсуждение hello *интервала блокирования* для клиентов, использующих ADO.NET доступна в [SQL пулов соединений Server (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).

Можно также tooset максимальное число попыток, прежде чем программа hello самостоятельно завершается.

#### <a name="code-samples-with-retry-logic"></a>Образцы кода с логикой повторных попыток
В этой статье доступны образцы кода с логикой повторных попыток на разных языках программирования:

* [Библиотеки подключений для Базы данных SQL и SQL Server](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a>Тестирование логики повторных попыток
tootest логику повторов должен имитировать или приводят к ошибке, не могут быть исправлены, пока выполняется приложение.

##### <a name="test-by-disconnecting-from-hello-network"></a>Проверьте, отключения от сети hello
Можно проверить логику повторов можно toodisconnect клиентского компьютера из hello сети во время программы hello. будет возвращена ошибка Hello:

* **SqlException.Number** = 11001
* Сообщение: "Данный узел неизвестен."

Как часть hello сначала повторной попытки, программы можно исправить ошибочное hello и повторить попытку tooconnect.

toomake этом практические отключении компьютера от сети hello перед запуском программы. Затем программа распознает параметр время выполнения, который вызывает программу hello.

1. Временно добавьте 11001 список tooits tooconsider ошибок в качестве временной.
2. Первый раз пытается подключиться как обычно.
3. После ошибки hello перехватывается, удалите 11001 из списка hello.
4. Отображать сообщение о том, tooplug hello hello пользователя компьютера в сети hello.
   * Дополнительно приостановку выполнения с помощью либо hello **Console.ReadLine** метода или диалоговое окно с помощью кнопки "ОК". Hello нажатии клавиши ВВОД hello после hello компьютер подключен к сети hello.
5. Повторите попытку tooconnect, ожидается успех.

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a>Тестирование ошибочное hello баз данных по имени при подключении
Программу можно специально опечатка hello имя пользователя, прежде чем hello первая попытка соединения. будет возвращена ошибка Hello:

* **SqlException.Number** = 18456
* Сообщение: "Ошибка входа пользователя WRONG_MyUserName."

Как часть hello сначала повторной попытки, программы можно исправить ошибочное hello и повторить попытку tooconnect.

этом практические toomake, программа может распознать параметр время выполнения, который вызывает программу hello:

1. Временно добавьте 18456 список tooits tooconsider ошибок в качестве временной.
2. Специально добавьте имя пользователя toohello «WRONG_».
3. После ошибки hello перехватывается, удалите 18456 из списка hello.
4. Удалите «WRONG_» из имени пользователя hello.
5. Повторите попытку tooconnect, ожидается успех.

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a>Параметры .NET SqlConnection для повторной попытки подключения
Если клиентская программа подключается tootooAzure базы данных SQL с помощью класса .NET Framework hello **System.Data.SqlClient.SqlConnection**, следует использовать .NET 4.6.1 или более поздней версии (или .NET Core), можно использовать его компонент повторных попыток подключения. Информация о функции hello [здесь](http://go.microsoft.com/fwlink/?linkid=393996).

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


При построении hello [строка подключения](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) для вашей **SqlConnection** объекта должен координировать hello значений между hello следующие параметры:

* ConnectRetryCount — &nbsp;&nbsp;*количество повторных попыток (значение по умолчанию — 1; диапазон — от 0 до 255).*
* ConnectRetryInterval — &nbsp;&nbsp;*интервал между повторными попытками (значение по умолчанию — 1 секунда; диапазон — от 1 до 60).*
* Connection Timeout — &nbsp;&nbsp;*время ожидания подключения (значение по умолчанию — 15 секунд; диапазон — от 0 до 2147483647).*

В частности выбранных значений необходимо внести следующие true равенства hello.

* Connection Timeout = ConnectRetryCount * ConnectionRetryInterval

Например, если hello count = 3 и интервала = 10 секунд, время ожидания составляет только 29 секунд не довольно придаст системы hello достаточное время для его третьей и последней попытки подключаться: 29 < 3 * 10.

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a>Подключения и команды
Hello **ConnectRetryCount** и **ConnectRetryInterval** параметры позволяют вашей **SqlConnection** hello объекта повторить операцию подключения без о том, или беспокоить вашей программу, например возвращение управления программы tooyour. повторные попытки Hello может произойти в следующих ситуациях hello.

* при вызове метода mySqlConnection.Open;
* при вызове метода mySqlConnection.Execute.

Есть один важный нюанс. Если возникает временная ошибка во время вашей *запроса* в ходе выполнения вашей **SqlConnection** объекта не hello повторить операцию подключения, и она определенно не повторить запрос. Тем не менее **SqlConnection** очень быстро проверок hello подключения перед отправкой запроса на выполнение. Если Быстрая проверка hello обнаруживает проблемы с подключением **SqlConnection** попыток hello операцию подключения. После успешного "Повторить" hello, то запрос отправляется для выполнения.

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a>Нужно ли сочетать ConnectRetryCount с логикой повторных попыток в приложении?
Предположим, что в вашем приложении реализована надежная настраиваемая логика повторных попыток. Она может повторить hello 4 раза в операции соединения. При добавлении **ConnectRetryInterval** и **ConnectRetryCount** = 3 строки подключения tooyour, увеличит too4 число повторных попыток hello * 3 = 12 повторных попыток. Вряд ли вам действительно нужно такое количество повторных попыток.

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a>TooAzure подключения базы данных SQL
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a>Подключение: строка подключения
Строка подключения Hello, необходимые для подключения tooAzure базы данных SQL несколько отличается от строку hello соединения tooMicrosoft SQL Server. Вы можете скопировать hello строку подключения для базы данных из hello [портал Azure](https://portal.azure.com/).

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a>Подключение: IP-адрес
Необходимо настроить hello базы данных SQL server tooaccept соединение с IP-адреса hello hello компьютера, на котором размещается клиентская программа. Это делается путем изменения параметров брандмауэра hello через hello [портал Azure](https://portal.azure.com/).

Если вы забыли tooconfigure hello IP-адрес, программа завершится с удобно сообщение hello необходимых IP-адрес.

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

Подробнее: [Настройка правила брандмауэра уровня сервера базы данных SQL Azure с помощью портала Azure](sql-database-configure-firewall-settings.md).

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a>Подключение: порты
Обычно требуется только tooensure, что порт 1433 открыт для исходящей связи, на компьютере hello, на котором размещается клиентская программа.

Например при размещении клиентскую программу на компьютер с Windows hello брандмауэра Windows на узле hello позволяет tooopen порт 1433:

1. Откройте панель управления hello
2. &gt; "Все элементы панели управления".
3. &gt; "Брандмауэр Windows".
4. &gt; "Дополнительные параметры".
5. &gt; "Правила для исходящего трафика".
6. &gt; "Действия".
7. &gt; "Создать правило".

Если клиентская программа установлена на виртуальной машине Azure, см. статью<br/>[Порты для ADO.NET 4.5, отличные от порта 1433](sql-database-develop-direct-route-ports-adonet-v12.md).

Основные сведения о конфигурации портов и IP-адресов собраны в статье [Настройка брандмауэра базы данных SQL Azure](sql-database-firewall-configure.md)

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a>Подключение: ADO.NET 4.6.1
Если программа использует классы ADO.NET как **System.Data.SqlClient.SqlConnection** tooAzure tooconnect базы данных SQL, мы рекомендуем использовать .NET Framework версии 4.6.1 или более поздней версии.

ADO.NET 4.6.1:

* Для базы данных SQL Azure имеется повышения надежности при открытии соединения с помощью hello **SqlConnection.Open** метод. Hello **откройте** метод теперь включает лучшие механизмов повтора усилий в ошибках tootransient ответа, для некоторых ошибок в течение периода ожидания соединения hello.
* Поддерживает работу с пулами подключений. Сюда входит проверка эффективный hello соединения объекта, он предоставляет программа работает.

При использовании объект соединения в пуле соединений, мы рекомендуем, программа временно закрыть соединение hello, при использовании в не сразу. Повторное открытие соединения не является ресурсоемким является способом hello, создав новое подключение.

Если вы используете ADO.NET 4.0 или более ранней версии, рекомендуется обновить toohello последнюю ADO.NET.

* С ноября 2015 года доступна [версия ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a>Диагностика
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a>Диагностика: проверяет, могут ли служебные программы подключаться
Если программа произошел сбой tooconnect tooAzure базы данных SQL, диагностики уже tooconnect tootry с помощью служебной программы. В идеале программа hello могут подключаться с помощью hello же библиотеке, используемого программой.

На компьютерах под управлением Windows можно использовать следующие служебные программы:

* SQL Server Management Studio (ssms.exe). Подключается с помощью ADO.NET.
* sqlcmd.exe. Подключается с помощью [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).

После подключения проверьте, работает ли короткий SQL-запрос SELECT.

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a>Диагностика: Проверьте Привет открыть порты
Предположим, что существует подозрение, что попытки подключения завершаются неудачей из-за проблем с tooport. На компьютере можно запускать программы, которая сообщает о конфигурации порта hello.

На Linux hello можно попробовать следующие программы:

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * (Изменить значение toobe hello пример IP-адреса).

В Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) программа может оказаться полезной. Ниже приведен пример выполнения, к которым запросы hello ситуации порта на сервере базы данных SQL Azure и которого была запущена на переносном компьютере.

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a>Диагностика: внесение ошибок в журнал
Эпизодические неисправности иногда лучше всего диагностировать, выявляя общий шаблон за несколько дней или недель подряд.

Клиент может помочь в диагностике. Для этого ему следует вносить в журнал все ошибки, с которыми он сталкивается. Может быть записи журнала могут toocorrelate hello с ошибочные данные самого внутреннего журналы базы данных SQL Azure.

Enterprise Library 6 (EntLib60) предлагает tooassist .NET управляемые классы с ведением журнала.

* [5 — как легко как неполадкой отключение журнала: с помощью hello функциональный блок ведения журнала](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a>Диагностика: проверка системных журналов на наличие ошибок
Ниже приведены некоторые Transact-SQL-инструкции SELECT, которые запрашивают в журналах сведения об ошибках и прочую информацию.

| Запрос у журнала | Описание |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |Hello [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) представление предоставляет сведения об отдельных событиях, включая некоторые, которая может вызвать временных ошибок или сбоев подключения к.<br/><br/>В идеальном случае вы можете соотнести hello **start_time** или **end_time** значения со сведениями о при клиентской программе возникших проблем.<br/><br/>**Совет:** необходимо подключить toohello **master** базы данных toorun это. |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |Hello [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) , то есть объединенное число типов событий, для дополнительной диагностики.<br/><br/>**Совет:** необходимо подключить toohello **master** базы данных toorun это. |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a>Диагностика: Поиск событий проблемы в журнале базы данных SQL hello
Можно выполнить поиск записей о событиях проблемы в журнале hello базы данных SQL Azure. Повторите hello, следующем за инструкцией Transact-SQL SELECT в hello **master** базы данных:

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a>Несколько возвращенных строк из sys.fn_xe_telemetry_blob_target_read_file
Ниже показано, как может выглядеть возвращенная строка. значения null Hello показано часто не имеют значение null, в других строках.

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a>Enterprise Library 6
Enterprise Library 6 (EntLib60) — это платформа классов .NET, поможет реализовать надежную клиентов облачных служб, он hello службы базы данных SQL Azure. Можно найти в котором EntLib60 может помочь, посетив первой области выделенной tooeach разделы:

* [Enterprise Library 6. Апрель, 2013 г.](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

Одна из областей, в которой может помочь EntLib60, — логика повторных попыток для обработки временных ошибок.

* [4 - perseverance, секрет все Triumphs: с помощью hello временных Fault Handling Application Block](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> Hello EntLib60 исходный код доступен для роли public [загрузить](http://go.microsoft.com/fwlink/p/?LinkID=290898). Корпорация Майкрософт предлагает дополнительные функции toomake нет планов обслуживания или обновления обновляет tooEntLib.
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a>Классы EntLib60 для временных ошибок и повторов
следующие классы EntLib60 Hello особенно полезны для логики повторных попыток. Здравствуйте, все они находятся в или более, пространство имен **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:

*В пространстве имен hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*

* **RetryPolicy** ;
  
  * **ExecuteAction** ;
* **ExponentialBackoff** ;
* **SqlDatabaseTransientErrorDetectionStrategy** ;
* **ReliableSqlConnection** ;
  
  * **ExecuteCommand** ;

В пространстве имен hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:

* **AlwaysTransientErrorDetectionStrategy** ;
* **NeverTransientErrorDetectionStrategy** ;

Ниже приведены ссылки tooinformation о EntLib60.

* Бесплатные [загрузки книги: tooMicrosoft руководство разработчика библиотеки Enterprise Library, второй выпуск](http://www.microsoft.com/download/details.aspx?id=41145)
* Рекомендации: в статье [Общие рекомендации по повторным попыткам](../best-practices-retry-general.md) содержится подробное обсуждение логики повторных попыток.
* Загрузка на сайте NuGet компонента [Enterprise Library 6.0: Transient Fault Handling application block](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a>EntLib60: ведение журнала блока hello
* блок Hello ведения журнала — гибкими и можно настроить решение, которое позволяет:
  
  * создавать и хранить сообщения журнала в разных расположениях;
  * классифицировать и фильтровать сообщения;
  * собирать контекстную информацию, полезную для отладки, трассировки, аудита и выполнения общих требований к ведению журнала.
* Hello ведения журнала блоков краткие описания hello ведения журнала функции hello место назначения журналов, чтобы код приложения hello согласована, независимо от расположения hello и ведения журнала хранилища hello целевого типа.

Дополнительные сведения см.: [5 — как легко как неполадкой отключение журнала: с помощью hello функциональный блок ведения журнала](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a>Исходный код метода EntLib60 IsTransient
Далее из hello **SqlDatabaseTransientErrorDetectionStrategy** класса, является исходный код hello C# для hello **IsTransient** метод. Hello исходного кода уточняет, какие ошибки рассматривались временной toobe и заслуживает повторных попыток, по состоянию на апрель 2013 г.

Многочисленные **//comment** строк были удалены из этой копии tooemphasize удобочитаемость.

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // hello instance of SQL Server you attempted tooconnect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a>Дальнейшие действия
* Сведения об устранении неполадок других распространенных проблем с подключением базы данных SQL Azure, посетите [Устранение неполадок подключения выдает tooAzure базы данных SQL](sql-database-troubleshoot-common-connection-issues.md).
* [Пул подключений SQL Server (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [*Повторная попытка* — лицензии Apache 2.0 общего назначения, повторная попытка библиотеки, написанные на **Python**, toosimplify задачу hello добавления toojust поведение повторных попыток, о чем-либо.](https://pypi.python.org/pypi/retrying)

