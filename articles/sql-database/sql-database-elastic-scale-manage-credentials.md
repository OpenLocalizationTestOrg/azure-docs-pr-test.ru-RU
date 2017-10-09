---
title: "учетные данные aaaManaging в клиентской библиотеке эластичной базы данных hello | Документы Microsoft"
description: "Как tooset hello необходимого уровня учетные данные администратора, предназначенным только для tooread для эластичной базы данных приложений"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 72e0edaf-795e-4856-84a5-6594f735fb7e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 218783ca2a07e3c0a4b089aa92634f32c41386e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="credentials-used-tooaccess-hello-elastic-database-client-library"></a>Учетные данные, используемые tooaccess hello эластичной базы данных клиентской библиотеки
Hello [клиентской библиотеке эластичной базы данных](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) использует три типа учетных данных hello tooaccess [диспетчера карты сегментов](sql-database-elastic-scale-shard-map-management.md). В зависимости от необходимости hello используйте hello учетных данных с уровнем hello наименьший возможный уровень доступа.

* **Учетные данные управления** предназначены для создания диспетчера карты сегментов или операций с ним. (В разделе hello [Глоссарий](sql-database-elastic-scale-glossary.md).) 
* **Доступ к учетным данным**: tooaccess существующего сегмента сопоставления диспетчера tooobtain сведений о сегментов.
* **Учетные данные для подключения**: tooconnect tooshards. 

См. также статью [Проверка подлинности и авторизация в базе данных SQL: предоставление доступа](sql-database-manage-logins.md). 

## <a name="about-management-credentials"></a>Об учетных данных управления
Учетные данные управления, используемые toocreate [ **ShardMapManager** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) объекта для приложений, которые позволяют управлять карт сегментов. (Например, в разделе [Добавление сегментов, с помощью средств эластичной базы данных](sql-database-elastic-scale-add-a-shard.md) и [управляемой данными маршрутизацией](sql-database-elastic-scale-data-dependent-routing.md)) пользователя hello клиентской библиотеки гибкого масштабирования hello создает hello SQL пользователей и имена входа SQL и гарантирует, что каждый предоставлено hello разрешения чтения и записи на глобальные сегментов hello сопоставление базы данных и все базы данных для сегмента также. Эти учетные данные, используется toomaintain карты глобального сегментов hello и hello локального сегментов карты при выполнении изменения карты сегментов toohello. Например, использовать hello управления учетными данными toocreate hello сегментов карты объект диспетчера (с помощью [ **GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx): 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

переменная приветствия **smmAdminConnectionString** представляет собой строку соединения, который содержит учетные данные управления hello. Hello идентификатор пользователя и пароль обеспечивает чтение и запись tooboth сегментов карты базы данных access и отдельные сегменты. Строка соединения управления Hello также включает hello имя и базы данных имя tooidentify hello глобального сегментов карты базы данных сервера. Вот типичная строка подключения, используемая в таком случае:

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

Не следует использовать значения в форме hello «username@server» — вместо этого используйте значение «username» hello.  Это так, как учетные данные должны работать от базы данных диспетчера карты сегментов hello и отдельные сегменты, которые могут находиться на разных серверах.

## <a name="access-credentials"></a>Учетные данные для доступа
При создании диспетчера карты сегментов в приложении, которое нельзя управлять карт сегментов, используйте учетные данные, имеющие разрешения только для чтения на карте сегментов глобального hello. Hello информации, полученной от карты глобального сегментов hello в эти учетные данные используются для [маршрутизации в зависимости от данных](sql-database-elastic-scale-data-dependent-routing.md) и toopopulate hello сегментов сопоставить кэш на клиенте hello. Hello учетные данные предоставляются через hello же call шаблон слишком**GetSqlShardMapManager** как показано выше: 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

Обратите внимание на использование hello hello **smmReadOnlyConnectionString** tooreflect hello использования разных учетных данных для такой доступ от имени **без прав администратора** пользователей: эти учетные данные не нужно обеспечивать записи разрешения на карте сегментов глобального hello. 

## <a name="connection-credentials"></a>Учетные данные подключения
Дополнительные учетные данные необходимы при использовании hello [ **OpenConnectionForKey** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) tooaccess метод сегментов, связанное с ключом сегментирования. Эти учетные данные должны tooprovide разрешения для доступа только для чтения toohello локального сегментов карты таблиц на сегментов hello. Это необходимые tooperform проверки подключения для маршрутизации в зависимости от данных на hello сегментов. Этот фрагмент кода разрешает доступ к данным в контексте hello управляемой данными маршрутизацией: 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

В этом примере **smmUserConnectionString** содержит hello строку подключения для hello учетные данные пользователя. В базах данных SQL Azure обычно используется такая строка подключения для учетных данных пользователя: 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

С помощью учетных данных администратора hello значений не в виде hello «username@server». Вместо этого используйте просто «имя_пользователя@сервер».  Также Обратите внимание, что hello строка подключения не содержит имя сервера и имя базы данных. Причина этого заключается в hello **OpenConnectionForKey** вызова автоматически перенаправит hello подключения toohello правильный сегментов на основе hello ключа. Таким образом, имя базы данных hello и имя сервера не указаны. 

## <a name="see-also"></a>См. также
[Управление базами данных и именами входа в Базе данных SQL Azure](sql-database-manage-logins.md)

[Защита Базы данных SQL](sql-database-security-overview.md)

[Начало работы с заданиями обработки эластичных баз данных](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

