---
title: "Клиентская библиотека aaaUpgrade toohello последние эластичной базы данных | Документы Microsoft"
description: "Обновление приложений и библиотек с помощью Nuget"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 0a546510-76e7-465e-9271-f15ff0cfa959
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: cc2c9179be4c53ca59cd24d832127cf277c6e695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-app-toouse-hello-latest-elastic-database-client-library"></a>Обновление приложения toouse hello последнюю эластичной базы данных клиентской библиотеки
Новые версии hello [клиентской библиотеке эластичной базы данных](sql-database-elastic-database-client-library.md) доступны через интерфейс диспетчера NuGetPackage NuGetand hello в Visual Studio. Обновления содержит исправления ошибок и поддержку новых возможностей hello клиентской библиотеки.

**Для последней версии hello:** Go слишком[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).

Перестройте приложение с новой библиотеки hello, а также изменить существующие метаданные диспетчера карты сегментов хранится в новые функции toosupport баз данных SQL Azure.

Выполнив эти действия в порядке гарантирует старых версий hello клиентской библиотеки, больше не присутствуют в вашей среде при обновлении объектов метаданных, это означает, что после обновления не будет создаваться объекты метаданных старой версии.   

## <a name="upgrade-steps"></a>Действия по обновлению
**1. Обновите свои приложения.** В Visual Studio, загрузки и ссылка hello последняя версия клиентской библиотеки во все проекты разработки, используйте библиотеку hello; затем перестроить и развернуть. 

* В Visual Studio выберите **Инструменты** --> **Диспетчер пакетов NuGet** -->  **Управление пакетами NuGet для решения...**. 
* (Visual Studio 2013) Hello левой панели выберите **обновления**и выберите hello **обновление** кнопку на пакет hello **Azure SQL базы данных эластичного масштабирования клиентская библиотека** , которая отображается в hello окно.
* (Visual Studio 2015 г.) Задать поле фильтра hello слишком**доступно ли обновление**. Выберите пакет tooupdate hello и нажмите кнопку hello **обновление** кнопки.
* (Visual Studio 2017 г.) Вверху hello hello диалогового окна выберите **обновления**. Выберите пакет tooupdate hello и нажмите кнопку hello **обновление** кнопки.
* Выполните сборку и развертывание. 

**2. Обновите свои сценарии.** При использовании **PowerShell** скрипты сегментов toomanage [Загрузите новую версию библиотеки hello](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) и скопируйте его в каталог hello, из которого выполнение скриптов. 

**3. Обновите свои службы разбиения и объединения.** Если вы используете hello эластичной базы данных средства слияния разбиение tooreorganize сегментированных данных [загрузить и установить последнюю версию средства hello hello](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/). Подробные шаги обновления по можно найти службу hello [здесь](sql-database-elastic-scale-overview-split-and-merge.md). 

**4. Обновите базы данных диспетчера карты сегментов**. Обновление метаданных hello поддержка картах сегментов в базе данных SQL Azure.  Это можно сделать двумя способами — с помощью PowerShell или C#. Ниже описаны оба этих способа.

***Вариант 1. Обновление метаданных с помощью PowerShell***

1. Загрузка hello последняя версия программы командной строки для NuGet из [здесь](http://nuget.org/nuget.exe) и tooa папку для сохранения. 
2. Откройте командную строку, toohello перейдите к папке, а команда hello проблемы:`nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`
3. Найдите toohello вложенной папкой, содержащей hello новой библиотеки DLL версии клиента, только что загруженный, например:`cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`
4. Загрузить обновления сценариев hello эластичной базы данных клиента из hello [центра сценариев](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), и сохраните его в hello же папку, содержащую hello DLL.
5. Из этой папки запустите «.\upgrade.ps1 PowerShell» из командной строки hello и следуйте появляющимся на hello.

***Вариант 2. Обновление метаданных с помощью C#***

Кроме того, создать приложение Visual Studio, открывающий вашей ShardMapManager, выполняет итерацию по всем сегментам и выполняет обновление метаданных hello путем вызова методов hello [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) и [ UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) как в следующем примере: 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

Эти методы обновления метаданных могут многократно применяться без каких-либо последствий. Например, если старая версия клиента случайно создает тот или иной сегмент после уже обновления, обновление можно запустить снова по всем сегментам tooensure, hello последнюю версию метаданных присутствует в инфраструктуре. 

**Примечание:** до даты публикации новых версий клиентской библиотеки hello продолжить toowork с предыдущими версиями hello диспетчера карты сегментов метаданных в базе данных SQL Azure и наоборот.   Тем не менее tootake преимуществами новых функций hello hello последнюю версию клиента, метаданные необходимо обновить toobe.   Обратите внимание, что обновление метаданных не повлияет на данные пользователя или данные приложения, созданные и используемые hello диспетчера карты сегментов только объекты.  И приложения по-прежнему toooperate через последовательность обновления hello, описанных выше. 

## <a name="elastic-database-client-version-history"></a>Журнал версий клиента эластичной базы данных
Журнал версий, см. слишком[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:./media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png

