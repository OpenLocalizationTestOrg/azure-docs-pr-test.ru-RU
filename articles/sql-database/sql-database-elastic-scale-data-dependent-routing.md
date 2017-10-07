---
title: "aaaData зависимой маршрутизации с базой данных SQL Azure | Документы Microsoft"
description: "Как toouse hello класс ShardMapManager в приложениях .NET для зависящих от данных маршрутизации, функция сегментированных баз данных в базе данных SQL Azure"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: cad09e15-5561-4448-aa18-b38f54cda004
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: ddove
ms.openlocfilehash: 34014508ae01905686791fe096bb275cb84f53b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="data-dependent-routing"></a>Маршрутизация, зависящая от данных
**Управляемой данными маршрутизацией** hello возможность toouse hello в данных запроса tooroute hello запроса tooan соответствующие базы данных. Это основная модель при работе с сегментированными базами данных. контекст запроса Hello также может быть запроса используется tooroute hello, особенно в том случае, если ключ сегментирования hello не является частью запроса hello. Каждой определенный запрос или транзакции в приложении с помощью управляемой данными маршрутизацией является ограниченным tooaccessing одной базы данных на один запрос. Hello инструментов эластичной базы данных SQL Azure, это Маршрутизация осуществляется с помощью hello  **[класса ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)**  приложений ADO.NET.

приложение Hello не требует tootrack различные строки подключения или расположений базы данных, связанных с различные срезы данных в среде сегментированных hello. Вместо этого hello [диспетчера карты сегментов](sql-database-elastic-scale-shard-map-management.md) открывает подключения toohello правильный базы данных при необходимости на основании данных hello в карте сегментов hello и hello значение ключа сегментирования hello, который является целевым объектом hello запроса приложения hello. Hello ключ обычно является hello *customer_id*, *tenant_id*, *date_key*, или некоторые определенный идентификатор фундаментальные параметра запроса hello базы данных). 

Дополнительные сведения см. в статье [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx) (Масштабирование SQL Server с помощью маршрутизации на основе данных).

## <a name="download-hello-client-library"></a>Загрузка клиентской библиотеки hello
Класс tooget hello, установка hello [клиентской библиотеке эластичной базы данных](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a>Использование ShardMapManager при маршрутизации с зависимостью от данных
Приложения следует создать hello **ShardMapManager** во время инициализации, с помощью вызова фабрики hello  **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**. В этом примере инициализируются как диспетчер **ShardMapManager**, так и конкретное сопоставление **ShardMap**, которое он содержит. В этом примере показано hello GetSqlShardMapManager и [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) методы.

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-hello-shard-map"></a>Использовать наименьшее учетные прав доступа, данные можно для получения карты сегментов hello
Если приложение не имеет дело с hello саму карту сегментов, hello учетные данные, используемые в hello фабричный метод должен иметь разрешения только доступна только для чтения на hello **глобальной карты сегментов** базы данных. Обычно эти учетные данные отличаются от диспетчера карты сегментов toohello соединения учетные данные, используемые tooopen. См. также [учетные данные, используемые tooaccess hello эластичной базы данных клиентской библиотеки](sql-database-elastic-scale-manage-credentials.md). 

## <a name="call-hello-openconnectionforkey-method"></a>Вызовите метод OpenConnectionForKey hello
Hello  **[метод ShardMap.OpenConnectionForKey](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)**  возвращает соединение ADO.Net готов для выдачи toohello соответствующей команды базы данных, на основе значения hello hello **ключ**параметра. Сегмент информация кэшируется в приложения hello, hello **ShardMapManager**, поэтому эти запросы не включают в себя обычно поиск в базе данных для hello **глобальной карты сегментов** базы данных. 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* Hello **ключ** параметр используется как ключ поиска в hello сегментов карты toodetermine hello соответствующую базу данных для запроса hello. 
* Hello **connectionString** — используется toopass только учетные данные пользователя hello hello требуемого подключения. Нет имя базы данных или имя сервера включены в это *connectionString* , так как метод hello определит hello базы данных и сервера, с помощью hello **ShardMap**. 
* Hello  **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)**  должно быть задано слишком**ConnectionOptions.Validate** Если могут изменяться в среде, где сегмент соответствует и строк может перемещать базы данных в качестве tooother результат операции разбиения или слияния. Для этого необходимо сопоставление локальных сегментов toohello кратким запросом на hello целевой базы данных (не карта сегментов глобального toohello) перед подключением hello доставляется toohello приложения. 

В случае hello проверки на соответствие сопоставление локальных сегментов hello (это означает, что кэш hello неправильный), hello диспетчера карты сегментов будет запрашивать hello глобального сегментов карты tooobtain hello новый правильное значение для поиска hello обновить кэш hello и получить и возвращают hello соединение с соответствующей базы данных. 

Используйте **ConnectionOptions.None** только в том случае, если внесение изменений в сопоставление сегментов не предполагается, т. е. когда приложение подключено к сети. В этом случае значения hello в кэше можно предположить, что tooalways верна и hello лишние приема-передачи вызовов toohello целевой базой данных проверки можно безопасно пропустить. Это позволяет снизить объем трафика базы данных. Hello **connectionOptions** также можно задать через значение в файле конфигурации tooindicate ожидаются изменения сегментирования или не в период времени.  

В этом примере используется значение hello целочисленный ключ **CustomerID**, с использованием **ShardMap** объект с именем **customerShardMap**.  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect toohello shard for that customer ID. No need toocall a SqlConnection 
    // constructor followed by hello Open method.
    using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId, 
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
    { 
        // Execute a simple command. 
        SqlCommand cmd = conn.CreateCommand(); 
        cmd.CommandText = @"UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID"; 

        cmd.Parameters.AddWithValue("@customerID", customerId); 
        cmd.Parameters.AddWithValue("@newPersonID", newPersonId); 
        cmd.ExecuteNonQuery(); 
    }  

Hello **OpenConnectionForKey** метод возвращает новую подключения уже открыта toohello правильный базу данных. Подключения, используемые в этом случае, по-прежнему имеют все преимущества объединенных подключений ADO.Net. При условии, что запросы и транзакции могут быть удовлетворены один сегмент одновременно, это должно быть hello только изменения, необходимые в приложении уже с использованием ADO.Net. 

Hello  **[метод OpenConnectionForKeyAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)**  также доступна, если приложение принимает использование асинхронного программирования с помощью ADO.Net. Его поведение не hello данных зависимых маршрутизации эквивалент ADO. NET  **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)**  метод.

## <a name="integrating-with-transient-fault-handling"></a>Интеграция с обработкой временных сбоев
При разработке приложений доступа к данным в облаке hello рекомендуется tooensure временных сбоев и перехватываются приложение hello и hello операций выполняется повторная попытка добавления несколько раз до возникновения ошибки. Обработка временных сбоев в облачных приложениях рассматривается в статье [4 - Perseverance, Secret of All Triumphs: Using the Transient Fault Handling Application Block](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx) (4. Настойчивость — секрет всех побед. Использование блока приложения для обработки временных ошибок). 

Обработки временных сбоев может сосуществовать с управляемой данными маршрутизацией шаблон Здравствуй естественным образом. Hello основным требованием является tooretry данных целиком hello доступ запроса, включая hello **с помощью** блок, который получен подключения маршрутизации в зависимости от данных hello. Hello примера можно переписать следующим образом (Обратите внимание, выделенная изменений). 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a>Пример. Маршрутизация, зависящая от данных, с обработкой временных сбоев
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect toohello shard for a customer ID. 
        using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId,  
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
        { 
            // Execute a simple command 
            SqlCommand cmd = conn.CreateCommand(); 

            cmd.CommandText = @&quot;UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID&quot;; 

            cmd.Parameters.AddWithValue(&quot;@customerID&quot;, customerId); 
            cmd.Parameters.AddWithValue(&quot;@newPersonID&quot;, newPersonId); 
            cmd.ExecuteNonQuery(); 

            Console.WriteLine(&quot;Update completed&quot;); 
        } 
<span style="background-color:  #FFFF00">    }); </span> 
</code></pre>


Автоматически загружать пакеты, необходимые tooimplement обработки временных сбоев при построении образца приложения hello эластичной базы данных. Пакеты также доступны по отдельности в библиотеке [Enterprise Library — блок приложений для обработки временных сбоев](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/). Используйте версию 6.0 или более позднюю. 

## <a name="transactional-consistency"></a>Согласованность транзакций
Свойства транзакций гарантируется для всех сегментов локальной tooa операций. Например транзакций, переданных через маршрутизации в зависимости от данных выполняются в области hello hello целевой сегментов для подключения hello. В данный момент нет возможности связывания нескольких подключений с транзакцией, поэтому невозможно гарантировать осуществление транзакций для операций, выполняемых через сегменты.

## <a name="next-steps"></a>Дальнейшие действия
toodetach сегментом или tooreattach сегментов, см. в разделе [с помощью карты проблем сегментов toofix hello RecoveryManager классов](sql-database-elastic-database-recovery-manager.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

