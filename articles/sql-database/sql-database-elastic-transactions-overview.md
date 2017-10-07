---
title: "aaaDistributed транзакций между базами данных облака"
description: "Общие сведения о транзакциях эластичной базы данных в базе данных SQL Azure"
services: sql-database
documentationcenter: 
author: torsteng
manager: jhubbard
editor: torsteng
ms.assetid: e14df7a3-7788-4cfb-bcd1-7ad6433ef1f9
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: sql-database
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 9a18f2749108d337bf115b3dc21dd0c7828dd9c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-transactions-across-cloud-databases"></a>Распределенные транзакции по облачным базам данных
Транзакции эластичной базы данных для базы данных SQL Azure (база данных SQL) позволяют toorun транзакций, которые охватывают несколько баз данных в базу данных SQL. Транзакции эластичной базы данных для базы данных SQL доступны для приложений .NET с помощью ADO .NET и интегрировать hello знакомый программный интерфейс с помощью hello [System.Transaction](https://msdn.microsoft.com/library/system.transactions.aspx) классы. Библиотека tooget hello, в разделе [.NET Framework 4.6.1 (веб-установщик)](https://www.microsoft.com/download/details.aspx?id=49981).

При локальном выполнении такого сценария, как правило, требуется использовать координатор распределенных транзакций Майкрософт (MSDTC). Поскольку MSDTC не доступен для приложения платформа как служба в Azure, hello возможность toocoordinate распределенных транзакций теперь напрямую интегрирован в баз данных SQL Server. Приложения могут подключаться tooany базы данных SQL toolaunch распределенных транзакций и одной из баз данных hello прозрачно координирует hello распределенных транзакций, как показано в hello следующий рисунок. 

  ![Осуществление распределенных транзакций в базе данных SQL Azure с использованием транзакций эластичной базы данных ][1]

## <a name="common-scenarios"></a>Распространенные сценарии
Транзакции эластичной базы данных для баз данных SQL Server включите toodata atomic изменения toomake приложений, хранятся в нескольких базах данных SQL. Предварительный просмотр Hello основное внимание уделяется опыт разработки на стороне клиента в C# и .NET. В будущем планируется предоставить возможность такой работы на сервере с использованием T-SQL.  
Целевые объекты транзакций эластичных баз данных hello следующие сценарии:

* Приложения в Azure, использующие несколько баз данных. Этот сценарий предусматривает вертикальное секционирование данных между несколькими базами данных в базе данных SQL. В результате разные виды данных находятся в разных базах данных. Некоторые операции требуют изменения toodata, который находится в двух или нескольких баз данных. Hello приложение использует изменения hello toocoordinate транзакций эластичных баз данных между базами данных и обеспечения атомарности.
* Сегментированной базы данных приложения в Azure: В этом случае уровень данных hello использует hello [клиентской библиотеке эластичной базы данных](sql-database-elastic-database-client-library.md) или toohorizontally самостоятельное сегментирование секционирования данных hello многих базах данных в базу данных SQL. Один вариант использования Показательным при hello необходимость tooperform atomic изменения для сегментированной многопользовательского приложения изменения span клиентов. Для экземпляра представить перенаправление от одного клиента tooanother, находящихся на разных базах данных. Второй случай — потребностей в емкости tooaccommodate детальной сегментирования для больших клиента, который в свою очередь, обычно означает, что некоторые toostretch потребностей атомарных операций между несколькими базами данных, используемый для hello же клиента. Третий вариант — atomic tooreference те данные, которые реплицируются в базах данных. Atomic, с поддержкой транзакций, операции подобным образом можно координируемой теперь между несколькими базами данных с помощью предварительного просмотра hello.
  Транзакции, эластичной базы данных используют атомарность транзакции tooensure двухфазной фиксации между базами данных. Этот вариант прекрасно подходит для тех случаев, когда в одной транзакции одновременно участвует менее 100 баз данных. Эти ограничения не применяются, но один следует ожидать производительности и показатели успеха для toosuffer транзакций эластичных баз данных, при превышении этих ограничений.

## <a name="installation-and-migration"></a>Установка и миграция
возможности Hello транзакций эластичных баз данных в базы данных SQL доступны через обновления библиотек .NET toohello System.Data.dll и System.Transactions.dll. Hello DLL-библиотеки убедитесь, что двухфазной фиксации используется при необходимости tooensure атомарность. Установка toostart разработки приложений с помощью транзакций эластичных баз данных, [.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981) или более поздней версии. При работе в более ранней версии платформы hello .NET framework транзакции завершится ошибкой toopromote tooa распределенных транзакций и будет вызвано исключение.

После установки можно использовать hello распределенных транзакций API-интерфейсы System.Transactions с tooSQL подключения базы данных. При наличии существующих приложений MSDTC с помощью этих API, просто перестроения существующие приложения .NET 4.6 После установки hello 4.6.1 Framework. Если проекты платформы .NET 4.6, они будут автоматически использовать DLL-библиотеками hello обновлены hello новая версия .NET Framework и вызовы API распределенной транзакции в сочетании с tooSQL подключения базы данных теперь будут выполнены.

Учтите, что для выполнения транзакций эластичной базы данных не требуется установка MSDTC. Вместо этого управление такими транзакциями осуществляется непосредственно в базе данных SQL. Это значительно упрощает облачных сценариев, поскольку развертывание MSDTC не необходимые toouse распределенных транзакций с баз данных SQL Server. Раздел 4 более подробно объясняется, как транзакции toodeploy эластичной базы данных и hello требуется .NET framework вместе с вашей tooAzure облачных приложений.

## <a name="development-experience"></a>Разработка
### <a name="multi-database-applications"></a>Приложения, использующие несколько баз данных
Hello следующий образец кода использует знакомый интерфейс программирования hello с .NET System.Transactions. класс TransactionScope Hello устанавливает внешнюю транзакцию в .NET. («Внешней транзакции» является один, которая находится в текущем потоке hello.) Все соединения, открытые в hello TransactionScope участвовать в транзакции hello. Если участвует в разных базах данных, hello транзакция автоматически с повышенными привилегиями tooa распределенных транзакций. Hello результат транзакции hello задается с помощью tooindicate toocomplete область hello фиксации.

    using (var scope = new TransactionScope())
    {
        using (var conn1 = new SqlConnection(connStrDb1))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = new SqlConnection(connStrDb2))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T2 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }

### <a name="sharded-database-applications"></a>Приложения, использующие сегментированные базы данных
Транзакции эластичной базы данных для базы данных SQL поддерживает координацию распределенных транзакций, где для горизонтальным масштабированием данных используется метод OpenConnectionForKey hello hello эластичной базы данных клиентских библиотек tooopen подключений уровня. Рассмотрите возможность которых требуется согласованность транзакций tooguarantee для изменения через несколько значений ключа сегментирования различных случаях. Размещение значений ключа сегментирования различных hello сегментов toohello подключения являются посредника с помощью OpenConnectionForKey. В общем случае hello hello соединения может быть сегментов toodifferent таким образом, что обеспечение гарантии транзакций требует распределенной транзакции. Этот подход показан следующий образец кода Hello. Предположения, что переменная с именем shardmap является используется toorepresent из клиентской библиотеки hello эластичной базы данных по карте сегментов:

    using (var scope = new TransactionScope())
    {
        using (var conn1 = shardmap.OpenConnectionForKey(tenantId1, credentialsStr))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = shardmap.OpenConnectionForKey(tenantId2, credentialsStr))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T1 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }


## <a name="net-installation-for-azure-cloud-services"></a>Установка .NET для облачных служб Azure
Azure предоставляет несколько предложений toohost приложений .NET. Сравнение разных предложений hello доступна в [службе приложений Azure, облачных служб и виртуальных машин сравнения](../app-service-web/choose-web-site-cloud-service-vm.md). Если hello гостевой ОС предложения hello меньше, чем .NET 4.6.1, необходимые для эластичного транзакций, необходимо tooupgrade hello гостевой ОС too4.6.1. 

Для службы приложений Azure обновляет toohello гостевой ОС в настоящее время не поддерживается. Для виртуальных машин в Azure, просто войдите hello виртуальной Машины и запустите установщик hello для hello последнюю версию .NET framework. Для облачных служб Azure необходимо tooinclude установки более новой версии .NET hello в задачах запуска hello развертывания. Основные понятия Hello и шаги описаны в [установить .NET на роли облачной службы](../cloud-services/cloud-services-dotnet-install-dotnet.md).  

Обратите внимание, что hello установщика для .NET 4.6.1 может потребоваться несколько временного хранилища во время начальной загрузки процесса в облачных службах Azure, чем hello установщик .NET 4.6 hello. tooensure успешной установки требуется tooincrease временное хранилище для облачной службы Azure в файле ServiceDefinition.csdef в разделе LocalResources hello и параметры среды hello задачей запуска, как показано в следующих hello Пример:

    <LocalResources>
    ...
        <LocalStorage name="TEMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
        <LocalStorage name="TMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
        <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
            <Environment>
        ...
                <Variable name="TEMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TEMP']/@path" />
                </Variable>
                <Variable name="TMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TMP']/@path" />
                </Variable>
            </Environment>
        </Task>
    </Startup>

## <a name="transactions-across-multiple-servers"></a>Транзакции между несколькими серверами
Транзакции эластичной базы данных поддерживаются для разных логических серверов в базе данных SQL Azure. Если транзакции пересекает границы логического сервера, серверах-участниках hello сначала необходимо toobe, введенные в отношении взаимного обмена данными. После установления связи связи hello любой базы данных, в каком-либо hello два сервера может участвовать в эластичный операций с базами данных из hello другой сервер. С транзакциями, объединение более двух логических серверов связь связи должен toobe на месте для любой пары логических серверов.

Используйте hello следующие связи связи между серверами toomanage командлеты PowerShell для транзакций эластичных баз данных:

* **Новый AzureRmSqlServerCommunicationLink**: используйте этот командлет toocreate отношение связь между двумя логическими серверами в базу данных SQL Azure. связь Hello симметричный что означает, что на обоих серверах могут инициировать транзакции с hello другой сервер.
* **Get-AzureRmSqlServerCommunicationLink**: используйте этот командлет tooretrieve существующие связи отношений и их свойства.
* **Удаление AzureRmSqlServerCommunicationLink**: используйте этот командлет tooremove существующую связь связи. 

## <a name="monitoring-transaction-status"></a>Мониторинг состояния транзакций
Используйте динамические административные представления (DMV) в БД SQL toomonitor состояние и ход выполнения транзакций Текущих эластичной базы данных. Все динамические административные представления, связанные tootransactions важны для распределенных транзакций в базу данных SQL. Список можно найти hello соответствующих динамических административных представлений здесь: [транзакции динамические административные представления и функции (Transact-SQL)](https://msdn.microsoft.com/library/ms178621.aspx).

Особенно полезны следующие динамические административные представления.

* **sys.dm\_tran\_active\_transactions** — позволяет просматривать список активных транзакций и их состояние. Hello UOW (единица работы) столбца можно определить hello другим дочерним транзакции, которые принадлежат toohello же распределенной транзакции. Все транзакции в рамках одной распределенной транзакции выполнения hello hello UOW совпадают. В разделе hello [документации к динамическим административным Представлениям](https://msdn.microsoft.com/library/ms174302.aspx) Дополнительные сведения.
* **sys.DM\_tran\_базы данных\_транзакции**: Дополнительные сведения о транзакции, например размещения hello транзакции в журнале hello. В разделе hello [документации к динамическим административным Представлениям](https://msdn.microsoft.com/library/ms186957.aspx) Дополнительные сведения.
* **sys.DM\_tran\_блокировки**: содержит сведения о hello блокировки, удерживаемые в настоящее время текущей транзакции. В разделе hello [документации к динамическим административным Представлениям](https://msdn.microsoft.com/library/ms190345.aspx) Дополнительные сведения.

## <a name="limitations"></a>Ограничения
Привет, в настоящее время следующие ограничения применяются tooelastic транзакций базы данных в базу данных SQL.

* Поддерживаются только транзакции, выполняемые между базами данных в базе данных SQL. В них не могут участвовать поставщики ресурсов и базы данных [X или Open XA](https://en.wikipedia.org/wiki/X/Open_XA) , которые не принадлежат к базе данных SQL. Это означает, что транзакции эластичной базы данных не распространяются на локальные базы данных SQL Server и SQL Azure. Для распределенных транзакций на локальном компьютере по-прежнему toouse MSDTC. 
* Поддерживаются только транзакции, которые осуществляются с помощью приложения .NET и которые координирует клиент. Сейчас выполнение запросов T-SQL на серверах (например, BEGIN DISTRIBUTED TRANSACTION) не поддерживается, но в будущем мы планируем добавить эту возможность. 
* Транзакции между службами WCF не поддерживаются. Например, если у вас есть метод службы WCF, выполняющий транзакцию, Заключения вызова hello в области транзакции не удастся как [System.ServiceModel.ProtocolException](https://msdn.microsoft.com/library/system.servicemodel.protocolexception).

## <a name="next-steps"></a>Дальнейшие действия
Ответить на вопросы, пожалуйста направляться на hello toous [форум базы данных SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) и для запросов, компонент, добавьте их toohello [форуме обратной связи в базе данных SQL](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-transactions-overview/distributed-transactions.png



