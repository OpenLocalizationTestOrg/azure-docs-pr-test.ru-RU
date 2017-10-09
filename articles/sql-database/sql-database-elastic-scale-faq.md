---
title: "aaaAzure SQL эластичного масштабирования часто задаваемые вопросы о | Документы Microsoft"
description: "Часто задаваемые вопросы об эластичном масштабировании базы данных SQL Azure."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: e60dde9c-bb7b-4f2f-b52c-bdb506d49fcb
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 8c77902e8ce9cbbc5e081cd9d2c911d4c8dc9e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-faq"></a>Вопросы и ответы по инструментам эластичных баз данных
#### <a name="if-i-have-a-single-tenant-per-shard-and-no-sharding-key-how-do-i-populate-hello-sharding-key-for-hello-schema-info"></a>У одного клиента в сегменте и без ключа сегментирования, как я могу ввести ключ сегментирования hello hello сведения схемы?
только сценарии слияния используется toosplit является объект сведения схемы Hello. Если приложение является по своей природе одного клиента, не требуется средство слияния разбиение hello, и таким образом отсутствует объект сведения о необходимости toopopulate hello схемы.

#### <a name="ive-provisioned-a-database-and-i-already-have-a-shard-map-manager-how-do-i-register-this-new-database-as-a-shard"></a>База данных подготовлена, и уже назначен диспетчер Shard Map Manager. Как зарегистрировать эту новую базу данных как сегмент?
См. в разделе  **[добавление с помощью клиентской библиотеки hello эластичной базы данных приложения сегментов tooan](sql-database-elastic-scale-add-a-shard.md)**. 

#### <a name="how-much-do-elastic-database-tools-cost"></a>Какова стоимость инструментов эластичных баз данных
С помощью клиентской библиотеки hello эластичной базы данных не приводит к дополнительным затратам всех расходов. Только для баз данных Azure SQL hello, используемые с сегментами и hello диспетчера карты сегментов, а также hello рабочих и веб-роли, которые подготовки для средства разбиения слияния hello начисления затрат.

#### <a name="why-are-my-credentials-not-working-when-i-add-a-shard-from-a-different-server"></a>Почему мои учетные данные не работают при добавлении сегмента с другого сервера?
Не использовать учетные данные в форме hello» ИД пользователя =username@servername», вместо просто используйте «идентификатор пользователя = имя пользователя».  Кроме того убедитесь, что это имя входа «username» hello имеет разрешения на hello сегментов.

#### <a name="do-i-need-toocreate-a-shard-map-manager-and-populate-shards-every-time-i-start-my-applications"></a>Вы я требуется toocreate диспетчера карты сегментов и заполнить сегментов, каждый раз при запуске приложения?
Нет — hello Создание hello диспетчера карты сегментов (например,  **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) является единовременной операцией.  Приложение должно использовать вызов hello  **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)**  во время запуска приложения.  На один домен приложения должен приходиться один такой вызов.

#### <a name="i-have-questions-about-using-elastic-database-tools-how-do-i-get-them-answered"></a>У меня есть вопросы об использовании инструментов эластичной базы данных. Как найти ответы?
Проверьте направляться на hello toous [форум базы данных SQL Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted).

#### <a name="when-i-get-a-database-connection-using-a-sharding-key-i-can-still-query-data-for-other-sharding-keys-on-hello-same-shard--is-this-by-design"></a>При получении подключения к базе данных с помощью ключа сегментирования, я по-прежнему могут запрашивать данные для других сегментирования ключей на hello же сегментов.  Так и должно быть?
Hello API динамического масштабирования обеспечивают подключение toohello нужную базу данных ключа сегментирования, но не имеют ключей фильтрации сегментирования.  Добавить **ГДЕ** области предложения tooyour запроса toorestrict hello toohello предоставленный ключ сегментирования, при необходимости.

#### <a name="can-i-use-a-different-azure-database-edition-for-each-shard-in-my-shard-set"></a>Можно ли использовать разные выпуски базы данных Azure для каждого сегмента моего набора сегментов?
Да. Ваш сегмент является отдельной базой данных и поэтому один сегмент может быть выпуском Premium, тогда как другой — выпуском Standard. Кроме того несколько раз за время существования hello сегментов hello hello выпуск сегментом можно масштабировать вверх или вниз.

#### <a name="does-hello-split-merge-tool-provision-or-delete-a-database-during-a-split-or-merge-operation"></a>Hello разделения слияния средство подготовки (или удалить) базы данных во время операции разбиения или слияния?
Нет. Для **разбиение** операции, hello целевая база данных должна существовать с соответствующей схемой hello и зарегистрировать hello диспетчера карты сегментов.  Для **слияния** операций, необходимо удалить из диспетчера карты сегментов hello сегментов hello и затем удалите hello базы данных.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

