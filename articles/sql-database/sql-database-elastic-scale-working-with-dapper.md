---
title: "библиотека клиента aaaUsing эластичной базы данных с Dapper | Документы Microsoft"
description: "Использование клиентской библиотеки эластичной базы данных с Dapper."
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 463d2676-3b19-47c2-83df-f8c50492c9d2
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: c22ece2a977265e93850f0ad3f3ca48f0a8733ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-elastic-database-client-library-with-dapper"></a>Использование клиентской библиотеки эластичной базы данных с Dapper
Данный документ предназначен для разработчиков, которые используют Dapper toobuild приложений, но при этом tooembrace [эластичной базы данных средства](sql-database-elastic-scale-introduction.md) toocreate приложения, которые реализуют горизонтального tooscale сегментирования уровень данных.  Этот документ описывает hello изменений в приложениях на базе Dapper, необходимые toointegrate со средствами эластичной базы данных. Наши фокус на составление зависит от данных и управления сегментами hello эластичной базы данных маршрутизации с Dapper. 

**Пример кода.** [Elastic DB Tools for Azure SQL - Dapper Integration](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f) (Средства эластичной базы данных для базы данных SQL Azure — интеграция с Dapper).

Интеграция **Dapper** и **DapperExtensions** с hello несложно клиентской библиотеке эластичной базы данных для базы данных SQL Azure. Приложения могут использовать данные зависимой маршрутизации, изменив hello создания и открытия нового [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) объектов toouse hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) вызов из hello [клиента Библиотека](http://msdn.microsoft.com/library/azure/dn765902.aspx). Это ограничивает изменения в вашей tooonly приложения, где создается и открывается новые соединения. 

## <a name="dapper-overview"></a>Обзор Dapper
**Dapper** — это объектно-реляционный модуль сопоставления. Он был сопоставлен объектов .NET из реляционной базы данных приложения tooa (и наоборот). Hello первой части образца кода hello показано, как клиентская библиотека hello эластичной базы данных могут интегрироваться с Dapper-приложениям. во второй части Hello hello образец кода иллюстрирует способ toointegrate при использовании Dapper и DapperExtensions.  

функциональность сопоставления Hello в Dapper содержит методы расширения, упрощающие Отправка инструкций T-SQL для выполнения или запроса базы данных hello подключения к базе данных. Для экземпляра Dapper делает его легко toomap между объектов .NET и параметры hello инструкций SQL для **Execute** вызовы или tooconsume hello результаты запросов SQL в объекты .NET с помощью **запроса**вызовы из Dapper. 

При использовании DapperExtensions, больше не нужна инструкций SQL tooprovide hello. Методы расширения, например **GetList, выдающего** или **вставить** через подключение к базе данных hello создания hello инструкций SQL, фоновом hello.

Еще одним преимуществом Dapper, а также DapperExtensions — что элементы управления приложения hello hello создания подключения к базе данных hello. Это позволяет взаимодействовать с клиентской библиотеки hello эластичной базы данных, которой брокеры подключений, на основе сопоставления hello объекта Подсегменты toodatabases к базе данных.

tooget hello Dapper, см. [Dapper точка net](http://www.nuget.org/packages/Dapper/). Hello Dapper расширения, в разделе [DapperExtensions](http://www.nuget.org/packages/DapperExtensions).

## <a name="a-quick-look-at-hello-elastic-database-client-library"></a>Кратко рассмотрим клиентская библиотека hello эластичной базы данных
С помощью клиентской библиотеки hello эластичной базы данных, определить секции данных приложения вызывается *подсегментов* , сопоставьте их toodatabases и определить их по *ключи сегментирования*. Вы можете использовать любое количество баз данных и распределять свои шардлеты между этими базами данных. сопоставление Hello баз данных toohello значения ключа сегментирования хранится по карте сегментов, предоставляемые API-интерфейсы hello библиотеки. Эта функция называется **управление сопоставлением сегментов**. карта сегментов Hello также служит в качестве hello посредника подключений к базе данных для запросов, которые используются для передачи ключа сегментирования. Эта возможность является ссылка tooas **управляемой данными маршрутизацией**.

![Сопоставления сегментов и маршрутизация на основе данных][1]

диспетчера карты сегментов Hello помогает защитить пользователей от несогласованные представления данных подсегмента, может возникать, когда операции управления параллельных подсегмента выполняются операции в базах данных hello. Таким образом, toodo hello сегментов карты broker hello подключения к базе данных для приложения, созданного с помощью библиотеки hello. Операции управления сегментов может повлиять на hello подсегмента, обеспечит hello сегментов карты функциональность tooautomatically kill подключения к базе данных. 

Вместо соединения toocreate традиционным способом hello Dapper, нам нужно toouse hello [OpenConnectionForKey метод](http://msdn.microsoft.com/library/azure/dn824099.aspx). Это гарантирует, что все проверкой hello и подключениями должным образом при перемещении данных между сегментами.

### <a name="requirements-for-dapper-integration"></a>Требования к интеграции Dapper
При работе с клиентской библиотеке эластичной базы данных hello и hello Dapper интерфейсы API, мы хотим tooretain hello следующие свойства:

* **Горизонтального масштабирования**: мы должны tooadd или удалить базы данных с уровня данных hello сегментированных приложения hello согласно требованиям к емкости hello приложения hello. 
* **Согласованность**: поскольку наше приложение масштабирован с использованием сегментирования, нам нужно tooperform управляемой данными маршрутизацией. Таким образом мы хотим toouse hello зависимой маршрутизации возможностей данных toodo библиотеки hello. В частности мы хотим tooretain проверки hello и гарантирует согласованность, предоставляемые через диспетчера карты сегментов hello в порядке tooavoid повреждение или результаты запроса неправильный посредника подключений. Это гарантирует, что tooa, подключений, заданному подсегмента отклонен или останавливается, если (например) hello Подсегмент является в настоящее время перемещенный tooa другой сегмент с помощью интерфейсов API разделения или слияния.
* **Сопоставление объектов**: мы хотим tooretain удобства hello сопоставлений hello, предоставляемые Dapper tootranslate между классами в приложение hello и hello базовые структуры базы данных. 

Hello следующий раздел содержит инструкции для этих требований для приложений на основе **Dapper** и **DapperExtensions**.

## <a name="technical-guidance"></a>Техническое руководство
### <a name="data-dependent-routing-with-dapper"></a>Маршрутизация на основе данных с помощью Dapper
С Dapper приложение hello обычно отвечает за создание и открытие toohello подключений hello основной базы данных. Назначает ему тип T приложения hello, Dapper возвращает результаты запроса, как .NET коллекции типа T. Dapper выполняет сопоставление hello от hello T-SQL результат строк toohello объектов типа T. Аналогичным образом Dapper сопоставляет объекты .NET SQL значения или параметры для инструкции языка обработки данных. Dapper предоставляет эту функцию через методы расширения в hello регулярного [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) объекта из hello ADO .NET SQL клиентских библиотек. Hello соединения SQL, возвращенный hello API динамического масштабирования для DDR также регулярные [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) объектов. Это позволяет нам toodirectly используйте Dapper расширения через hello тип, возвращенный API DDR hello клиентской библиотеки, это простого подключения клиента SQL.

Эти данные позволяют простой toouse подключения через посредника клиентской библиотекой hello эластичной базы данных для Dapper.

Данный пример кода (из сообщения, сопровождающие образец hello) иллюстрирует hello подход, где ключ сегментирования hello обеспечивается hello приложения toohello библиотеки toobroker hello подключения toohello вправо сегментов.   

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                     key: tenantId1, 
                     connectionString: connStrBldr.ConnectionString, 
                     options: ConnectionOptions.Validate))
    {
        var blog = new Blog { Name = name };
        sqlconn.Execute(@"
                      INSERT INTO
                            Blog (Name)
                            VALUES (@name)", new { name = blog.Name }
                        );
    }

Hello вызовов toohello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) API заменяет создания по умолчанию hello и открытие подключения клиента SQL. Hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) hello аргументы, которые требуются для управляемой данными маршрутизацией принимает вызов: 

* tooaccess карты сегментов Hello hello зависимых интерфейсов маршрутизации данных
* Подсегмент hello tooidentify ключа сегментирования Hello
* Hello учетные данные (имя пользователя и пароль) tooconnect toohello сегментов

Объект карты сегментов Hello создает подключение toohello сегмент, содержащий hello Подсегмент для заданного ключа сегментирования hello. Hello эластичной базы данных клиентские API также тега tooimplement подключения hello гарантирует ее согласованности. С момента hello вызвать слишком[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) возвращает обычный объект подключения клиента SQL, последующий вызов toohello hello **Execute** метод расширения из Dapper следующим hello Стандартная Dapper практика.

Запросы рабочих сильно hello таким же, каким образом - первом открытии соединения с помощью hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) из API клиента hello. Затем с помощью hello регулярное расширение Dapper методы toomap hello результаты SQL-запроса в объекты .NET:

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId1, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate ))
    {    
           // Display all Blogs for tenant 1
           IEnumerable<Blog> result = sqlconn.Query<Blog>(@"
                                SELECT * 
                                FROM Blog
                                ORDER BY Name");

           Console.WriteLine("All blogs for tenant id {0}:", tenantId1);
           foreach (var item in result)
           {
                Console.WriteLine(item.Name);
            }
    }

Обратите внимание, что hello **с помощью** блок с областями подключения DDR hello всех операций базы данных в пределах hello блока toohello один сегмент хранения tenantId1. Hello запрос возвращает только блоги, хранящиеся на текущий сегмент hello, но не hello тех, которые хранятся на любые другие сегменты. 

## <a name="data-dependent-routing-with-dapper-and-dapperextensions"></a>Маршрутизация на основе данных с помощью Dapper и DapperExtensions
Dapper поставляется с экосистемы Дополнительные расширения, которые могут предоставить дополнительные удобства и абстракции из базы данных hello при разработке приложений баз данных. И примером таких расширений является DapperExtensions. 

При использовании DapperExtensions в приложении способ создания подключений к базе данных и управления ими не меняется. Она по-прежнему tooopen подключения приложения hello ответственность, а обычных объектов подключения клиента SQL ожидаются методами расширения hello. Мы можно положиться на hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) как описано выше. Как hello приведенных ниже примерах кода показаны программы, hello единственным изменением является то, что мы больше не toowrite hello T-SQL инструкции:

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           var blog = new Blog { Name = name2 };
           sqlconn.Insert(blog);
    }

А Вот пример кода hello для hello запроса: 

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           // Display all Blogs for tenant 2
           IEnumerable<Blog> result = sqlconn.GetList<Blog>();
           Console.WriteLine("All blogs for tenant id {0}:", tenantId2);
           foreach (var item in result)
           {
               Console.WriteLine(item.Name);
           }
    }

### <a name="handling-transient-faults"></a>Обработка временных сбоев
Hello шаблонов и практик Майкрософт team опубликованных hello [временных Fault Handling Application Block](http://msdn.microsoft.com/library/hh680934.aspx) toohelp разработчикам устранить распространенные временная ошибка возникла при выполнении в облаке hello. Дополнительные сведения см. в разделе [Perseverance, секрет все Triumphs: с помощью hello временных Fault Handling Application Block](http://msdn.microsoft.com/library/dn440719.aspx).

Образец кода Hello использует hello временных сбоев библиотека tooprotect от временных сбоев. 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
    {
       using (SqlConnection sqlconn = 
          shardingLayer.ShardMap.OpenConnectionForKey(tenantId2, connStrBldr.ConnectionString, ConnectionOptions.Validate))
          {
              var blog = new Blog { Name = name2 };
              sqlconn.Insert(blog);
          }
    });

**SqlDatabaseUtils.SqlRetryPolicy** в hello приведенный выше код определяется как **SqlDatabaseTransientErrorDetectionStrategy** с числом повторов, равным 10 и 5 секунд время ожидания между повторными попытками. При использовании транзакций убедитесь, что в данной области повтора вновь переходит toohello начало транзакции hello в случае, когда hello временных ошибок.

## <a name="limitations"></a>Ограничения
Hello подходов, описанных в этом документе включают несколько ограничений:

* Hello образцы кода для этого документа не показано, как схема toomanage по сегментам.
* Получает запрос, мы предполагаем, что его обработку базы данных содержится в одном сегменте, идентифицируемый hello сегментирования ключ, указанный в запросе hello. Тем не менее это предположение не всегда удерживает, например, если она не возможные toomake ключ сегментирования доступны. tooaddress, hello клиентской библиотеке эластичной базы данных включает в себя hello [MultiShardQuery класса](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx). Hello класс реализует абстракцию подключения для выполнения запросов через несколько сегментов. С помощью MultiShardQuery в сочетании с Dapper выходит за рамки данного документа hello.

## <a name="conclusion"></a>Заключение
Приложения, использующие Dapper и DapperExtensions, могут легко использовать преимущества средств эластичной базы данных SQL Azure. Через hello шаги, описанные в этом документе, эти приложения можно использовать средство hello возможность для данных зависимой маршрутизации, изменив hello создания и открытия нового [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) объектов toouse hello [ OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) вызов hello эластичной базы данных клиентской библиотеки. Это ограничивает изменения требуется toothose приложения hello местах, где создается и открывается новые соединения. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-working-with-dapper/dapperimage1.png
