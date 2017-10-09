---
title: "aaaUsing сегментов toofix диспетчера восстановления сопоставить проблемы | Документы Microsoft"
description: "Используйте hello RecoveryManager класса toosolve проблемы с картами сегментов"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 45520ca3-6903-4b39-88ba-1d41b22da9fe
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: ddove
ms.openlocfilehash: 2218fb15122f1df466e65483480461e366317f2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-recoverymanager-class-toofix-shard-map-problems"></a>С помощью карты проблем сегментов toofix hello RecoveryManager классов
Hello [RecoveryManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.aspx) класс предоставляет приложений ADO.Net tooeasily hello возможность обнаружить и исправить все несоответствия между hello сегментов глобальной карты (GSM) и карты сегментов локальной hello (LSM) в среде сегментированной базы данных. 

Hello GSM и LSM отслеживания hello сопоставление каждой базы данных в сегментированных среде. В некоторых случаях между hello GSM и hello LSM возникновении прерывания. В этом случае используйте toodetect класса RecoveryManager hello и восстановить hello break.

Hello RecoveryManager класс является частью hello [клиентской библиотеке эластичной базы данных](sql-database-elastic-database-client-library.md). 

![Карта сегментов][1]

Определения терминов см. в статье [Глоссарий по средствам работы с эластичными базами данных](sql-database-elastic-scale-glossary.md). как hello toounderstand **ShardMapManager** — это данные, используемые toomanage в решении сегментирования, в разделе [управления карты сегментов](sql-database-elastic-scale-shard-map-management.md).

## <a name="why-use-hello-recovery-manager"></a>Зачем использовать hello диспетчера восстановления?
В среде сегментированной базы данных на каждую базу данных приходится по одному клиенту и на каждый сервер — по несколько баз данных. Может существовать несколько серверов в среде hello. Каждая база данных определено в hello карта сегментов, так, чтобы вызовы перенаправленное toohello нужный сервер и базу данных. Базы данных, отслеживаются в соответствии с tooa **ключа сегментирования**, и назначить каждый сегмент **диапазон значений ключа**. Например ключ сегментирования может представлять hello имена заказчиков из «D» слишком «F.» Здравствуйте, сопоставление всех сегментов (также называемого баз данных) и их диапазоны сопоставления содержатся в hello **сегментов глобальной карты (GSM)**. Каждая база данных также содержит сопоставления диапазонов hello, содержащиеся на hello сегментов, известный как hello **карты локальной сегментов (LSM)**. Когда приложение подключается tooa сегментов, сопоставление hello кэшируется приложение hello для быстрого извлечения. Hello LSM — используется toovalidate кэшированные данные. 

Hello GSM и LSM могут стать синхронизированы для hello следующих причин:

1. Удаление Hello сегментов, чей диапазон считается toono больше времени, быть используется или переименование сегментом. Удаление сегмента приводит к **потере сопоставления сегментов**. Переименование базы данных точно так же может привести к потере сопоставления сегментов. В зависимости от hello целью изменения hello hello сегментов может потребоваться удалить toobe или расположение сегментов hello должно toobe обновлены. toorecover удаленной базы данных, в разделе [Восстановление удаленной базы данных](sql-database-recovery-using-backups.md).
2. Происходит событие географической отработки отказа. toocontinue, один необходимо обновить hello имя сервера и имя базы данных диспетчера карты сегментов в приложение hello, а затем сведения о сопоставлении сегментов hello обновления для всех сегментов в карте сегментов. Если географическая отработка отказа, такую логику восстановления следует автоматизировать в рабочем процессе отработки отказа hello. Автоматизация действий по восстановлению гарантирует удобную управляемость для баз данных с поддержкой определения географического расположения и позволяет избежать выполнение действий пользователем вручную. toolearn о toorecover параметры базы данных при наличии сбоя центра обработки данных. в разделе [непрерывности](sql-database-business-continuity.md) и [аварийного восстановления](sql-database-disaster-recovery.md).
3. Hello или сегментов ShardMapManager базы данных является восстановленной tooan ранее на момент времени. toolearn о моменту времени восстановления, использование резервных копий, в разделе [восстановление резервных копий с помощью](sql-database-recovery-using-backups.md).

Дополнительные сведения о инструментов эластичной базы данных базы данных SQL Azure, георепликация и восстановление см. в следующем hello: 

* [Обзор. Непрерывность облачных бизнес-процессов и аварийное восстановление баз данных с базой данных SQL](sql-database-business-continuity.md) 
* [Приступая к работе с инструментами эластичной базы данных](sql-database-elastic-scale-get-started.md)  
* [Управление ShardMap](sql-database-elastic-scale-shard-map-management.md)

## <a name="retrieving-recoverymanager-from-a-shardmapmanager"></a>Извлечение RecoveryManager из ShardMapManager
Hello первым шагом является toocreate экземпляра RecoveryManager. Hello [метод GetRecoveryManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getrecoverymanager.aspx) возвращает hello диспетчера восстановления для текущего hello [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) экземпляра. сопоставить несогласованностей в сегменте hello tooaddress, сначала необходимо получить hello RecoveryManager для hello определенного сегмента карты. 

   ```
    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString,  
             ShardMapManagerLoadPolicy.Lazy);
             RecoveryManager rm = smm.GetRecoveryManager(); 
   ```

В этом примере инициализируется hello RecoveryManager hello ShardMapManager. Hello ShardMapManager, содержащий ShardMap также уже инициализирован. 

Так как этот код приложения управляет hello саму карту сегментов, hello учетные данные, используемые в методе фабрики hello (в предыдущих примере hello smmConnectionString) должны быть учетные данные, имеющие разрешения на чтение запись в базе данных GSM hello, ссылается hello Строка подключения. Обычно эти учетные данные отличаются от соединений tooopen учетные данные, используемые для маршрутизации в зависимости от данных. Дополнительные сведения см. в разделе [с использованием учетных данных в клиенте hello эластичной базы данных](sql-database-elastic-scale-manage-credentials.md).

## <a name="removing-a-shard-from-hello-shardmap-after-a-shard-is-deleted"></a>Снятие hello ShardMap тот или иной сегмент после удаления сегментов
Hello [DetachShard метод](https://msdn.microsoft.com/library/azure/dn842083.aspx) отсоединяет hello даны сегментов карты сегментов hello и удаляет сопоставления, связанные с сегментом hello.  

* Параметр расположения Hello — расположение сегментов hello, в частности имя сервера и имя базы данных, сегментов hello и после отключения. 
* параметр shardMapName Hello является имя сопоставления сегментов hello. Это только требуется, если несколько карт сегментов управляются hello же диспетчера карты сегментов. необязательный параметр. 


> [!IMPORTANT]
> Этот способ следует используйте только в том случае, если вы уверены, что hello диапазона для hello обновить сопоставление является пустым. выше методов Hello не проверять данные для перемещения диапазона hello, поэтому лучше tooinclude проверяет в коде.
>

Этот пример удаляет сегменты из карты сегментов hello. 

   ```
   rm.DetachShard(s.Location, customerMap);
   ``` 

карта сегментов Hello отражает расположение сегментов hello в hello GSM перед удалением hello hello сегментов. Из-за удаления сегментов hello, предполагается, что это было намеренное действие, и диапазон ключа сегментирования hello больше не используется. Если это не так, можно выполнить восстановление до точки во времени, Сегмент hello toorecover из более ранней точке времени. (В этом случае просмотрите следующий раздел toodetect сегментов несоответствия hello). toorecover, в разделе [моменту времени восстановления](sql-database-recovery-using-backups.md).

Так, как предполагалось, что hello удаления баз данных было намеренное действие, hello действий административных завершающих — toodelete hello запись toohello сегментов в hello диспетчера карты сегментов. Это предотвращает приложения hello из случайная запись сведения tooa диапазон, который не ожидается.

## <a name="toodetect-mapping-differences"></a>различия toodetect сопоставления
Hello [DetectMappingDifferences метод](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.detectmappingdifferences.aspx) выбирает и возвращает одно из карт сегментов hello (локальных или глобальных) как источник достоверных hello и согласовывает сопоставления на обе карты сегментов (GSM и LSM).

   ```
   rm.DetectMappingDifferences(location, shardMapName);
   ```

* Hello *расположение* hello имя сервера и имя базы данных. 
* Hello *shardMapName* параметр является имя сопоставления сегментов hello. Это только требуется, если несколько карт сегментов управляются hello же диспетчера карты сегментов. необязательный параметр. 

## <a name="tooresolve-mapping-differences"></a>различия tooresolve сопоставления
Hello [ResolveMappingDifferences метод](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.resolvemappingdifferences.aspx) выбирает одну из карт сегментов hello (локальных или глобальных) как источник достоверных hello и согласовывает сопоставления на обе карты сегментов (GSM и LSM).

   ```
   ResolveMappingDifferences (RecoveryToken, MappingDifferenceResolution.KeepShardMapping);
   ```

* Hello *RecoveryToken* параметр перечисляет hello различия в сопоставлениях hello hello GSM и hello LSM для конкретных сегментов hello. 
* Hello [MappingDifferenceResolution перечисления](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.mappingdifferenceresolution.aspx) — метод hello tooindicate используется для разрешения hello различие между hello сопоставления сегментов. 
* **MappingDifferenceResolution.KeepShardMapping** рекомендуется, когда hello LSM содержит точное сопоставление hello и поэтому должны использоваться сопоставление hello в сегменте hello. Это обычно hello так, если происходит переход: hello сегмент теперь находится на новом сервере. Поскольку сегментов hello сначала должны быть удалены из hello GSM (с помощью метода RecoveryManager.DetachShard hello), сопоставление больше не существует в hello GSM. Поэтому hello LSM должен быть используется toore-Установка hello сопоставления сегментов.

## <a name="attach-a-shard-toohello-shardmap-after-a-shard-is-restored"></a>Присоединение сегментов toohello ShardMap после восстановления сегментом
Hello [AttachShard метод](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.attachshard.aspx) присоединяет hello карта сегментов toohello данного сегмента. Он обнаруживает несогласованностей карты сегментов и обновляет hello сопоставления toomatch hello сегментов в точке восстановления сегментов hello hello. Предполагается, что hello базы данных также переименованный tooreflect hello исходное имя базы данных (до была восстановлена hello сегментов), с момента восстановления на момент времени hello по умолчанию tooa дополненная hello timestamp новой базы данных. 

   ```
   rm.AttachShard(location, shardMapName)
   ``` 

* Hello *расположение* параметр является hello имя сервера и имя базы данных, сегментов hello и присоединения. 
* Hello *shardMapName* параметр является имя сопоставления сегментов hello. Это только требуется, если несколько карт сегментов управляются hello же диспетчера карты сегментов. необязательный параметр. 

В этом примере добавляется карта сегментов toohello сегментов, был недавно восстановлен из более ранних на момент времени. Поскольку восстановила приветствия сегментов (а именно: hello сопоставления для сегмента hello в hello LSM) потенциально несовместим с записью сегментов hello в hello GSM. За пределами этот пример кода hello сегментов была восстановлена и переименовывается toohello исходное имя базы данных hello. Так как она была восстановлена, предполагается, что сопоставление hello в hello LSM является доверенным сопоставления hello. 

   ```
   rm.AttachShard(s.Location, customerMap); 
   var gs = rm.DetectMappingDifferences(s.Location); 
      foreach (RecoveryToken g in gs) 
       { 
       rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
       } 
   ```

## <a name="updating-shard-locations-after-a-geo-failover-restore-of-hello-shards"></a>Обновление расположения сегментов после выполнена географическая отработка отказа (восстановление) hello сегментов
В случае географическая отработка отказа базы данных-получателя hello не будет доступна запись и становится новой первичной базы данных hello. Здравствуйте, имя сервера hello и, потенциально, hello базы данных (в зависимости от настройки), может отличаться от исходного основного hello. Поэтому hello записи сопоставления для сегментов hello в hello GSM и LSM должны быть исправлены. Аналогичным образом, если hello базы данных будет восстановленной tooa другое имя или расположение или tooan более раннего момента времени, это может привести к несогласованности в картах сегментов hello. Hello диспетчера карты сегментов обрабатывает hello распределение нужную базу данных toohello открытых соединений. Распределение основывается на данных hello в карте сегментов hello и hello значение ключа сегментирования hello, который является целевым объектом hello запроса приложения hello. После выполнена географическая отработка отказа необходимо обновить эти сведения с точным имя_сервера hello, имя базы данных и сопоставления сегментов hello восстановленной базы данных. 

## <a name="best-practices"></a>Рекомендации
Географическая отработка отказа и восстановления являются операциями, обычно управляется администратором облачные приложения hello намеренно использование одной из функций обеспечения непрерывности бизнеса баз данных SQL Azure. Для планирования непрерывности бизнеса требуется процессы, процедуры и меры tooensure, бизнес-операции можно продолжить работу без прерывания. Здравствуйте, методы доступны как часть hello RecoveryManager класса следует использовать в рамках этого рабочего потока tooensure hello GSM и LSM постоянно обновляются в зависимости от действий восстановления hello. Существует пять простых шагов tooproperly, обеспечивая hello GSM и LSM отражают hello точной информации после отработки отказа. Здравствуйте, tooexecute код приложения, эти действия могут быть интегрированы в существующих средств и рабочего процесса. 

1. Получить hello RecoveryManager из hello ShardMapManager. 
2. Отсоедините hello старый сегмент из карты сегментов hello.
3. Присоедините hello новых сегментов toohello карта сегментов, включая hello новое расположение сегментов.
4. Обнаружены несоответствия в сопоставление hello GSM и LSM hello. 
5. Устраните различия между hello GSM и hello LSM, доверяющих hello LSM. 

В этом примере выполняет следующие шаги hello.

1. Удаляет сегменты из hello карта сегментов, с учетом расположения сегментов перед hello отработки отказа.
2. Присоединяет сегментов toohello карта сегментов отражающей hello новых сегментов ячеек (hello параметр «Configuration.SecondaryServer» является hello нового имени сервера, но hello же имя базы данных).
3. Получает маркеры восстановления hello, обнаруживая сопоставления различия между hello GSM и hello LSM для каждого сегмента. 
4. Разрешает несоответствия hello, доверяющих сопоставление hello hello LSM для каждого сегмента. 
   
   ```
   var shards = smm.GetShards(); 
   foreach (shard s in shards) 
   { 
     if (s.Location.Server == Configuration.PrimaryServer) 
   
         { 
          ShardLocation slNew = new ShardLocation(Configuration.SecondaryServer, s.Location.Database); 
   
          rm.DetachShard(s.Location); 
   
          rm.AttachShard(slNew); 
   
          var gs = rm.DetectMappingDifferences(slNew); 
   
          foreach (RecoveryToken g in gs) 
            { 
               rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
            } 
        } 
    } 
   ```

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-database-recovery-manager/recovery-manager.png

