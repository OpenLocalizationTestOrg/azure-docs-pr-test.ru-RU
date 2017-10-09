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
# <a name="upgrade-an-app-toouse-hello-latest-elastic-database-client-library"></a><span data-ttu-id="880fc-103">Обновление приложения toouse hello последнюю эластичной базы данных клиентской библиотеки</span><span class="sxs-lookup"><span data-stu-id="880fc-103">Upgrade an app toouse hello latest elastic database client library</span></span>
<span data-ttu-id="880fc-104">Новые версии hello [клиентской библиотеке эластичной базы данных](sql-database-elastic-database-client-library.md) доступны через интерфейс диспетчера NuGetPackage NuGetand hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="880fc-104">New versions of hello [Elastic Database client library](sql-database-elastic-database-client-library.md) are  available through NuGetand hello NuGetPackage Manager interface in Visual Studio.</span></span> <span data-ttu-id="880fc-105">Обновления содержит исправления ошибок и поддержку новых возможностей hello клиентской библиотеки.</span><span class="sxs-lookup"><span data-stu-id="880fc-105">Upgrades contain bug fixes and support for new capabilities of hello client library.</span></span>

<span data-ttu-id="880fc-106">**Для последней версии hello:** Go слишком[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span><span class="sxs-lookup"><span data-stu-id="880fc-106">**For hello latest version:** Go too[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span>

<span data-ttu-id="880fc-107">Перестройте приложение с новой библиотеки hello, а также изменить существующие метаданные диспетчера карты сегментов хранится в новые функции toosupport баз данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="880fc-107">Rebuild your application with hello new library, as well as change your existing Shard Map Manager metadata stored in your Azure SQL Databases toosupport new features.</span></span>

<span data-ttu-id="880fc-108">Выполнив эти действия в порядке гарантирует старых версий hello клиентской библиотеки, больше не присутствуют в вашей среде при обновлении объектов метаданных, это означает, что после обновления не будет создаваться объекты метаданных старой версии.</span><span class="sxs-lookup"><span data-stu-id="880fc-108">Performing these steps in order ensures that old versions of hello client library are no longer present in your environment when metadata objects are updated, which means that old-version metadata objects won’t be created after upgrade.</span></span>   

## <a name="upgrade-steps"></a><span data-ttu-id="880fc-109">Действия по обновлению</span><span class="sxs-lookup"><span data-stu-id="880fc-109">Upgrade steps</span></span>
<span data-ttu-id="880fc-110">**1. Обновите свои приложения.**</span><span class="sxs-lookup"><span data-stu-id="880fc-110">**1. Upgrade your applications.**</span></span> <span data-ttu-id="880fc-111">В Visual Studio, загрузки и ссылка hello последняя версия клиентской библиотеки во все проекты разработки, используйте библиотеку hello; затем перестроить и развернуть.</span><span class="sxs-lookup"><span data-stu-id="880fc-111">In Visual Studio, download and reference hello latest client library version into all of your development projects that use hello library; then rebuild and deploy.</span></span> 

* <span data-ttu-id="880fc-112">В Visual Studio выберите **Инструменты** --> **Диспетчер пакетов NuGet** -->  **Управление пакетами NuGet для решения...**.</span><span class="sxs-lookup"><span data-stu-id="880fc-112">In your Visual Studio solution, select **Tools** --> **NuGet Package Manager** -->  **Manage NuGet Packages for Solution**.</span></span> 
* <span data-ttu-id="880fc-113">(Visual Studio 2013) Hello левой панели выберите **обновления**и выберите hello **обновление** кнопку на пакет hello **Azure SQL базы данных эластичного масштабирования клиентская библиотека** , которая отображается в hello окно.</span><span class="sxs-lookup"><span data-stu-id="880fc-113">(Visual Studio 2013) In hello left panel, select **Updates**, and then select hello **Update** button on hello package **Azure SQL Database Elastic Scale Client Library** that appears in hello window.</span></span>
* <span data-ttu-id="880fc-114">(Visual Studio 2015 г.) Задать поле фильтра hello слишком**доступно ли обновление**.</span><span class="sxs-lookup"><span data-stu-id="880fc-114">(Visual Studio 2015) Set hello Filter box too**Upgrade available**.</span></span> <span data-ttu-id="880fc-115">Выберите пакет tooupdate hello и нажмите кнопку hello **обновление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="880fc-115">Select hello package tooupdate, and click hello **Update** button.</span></span>
* <span data-ttu-id="880fc-116">(Visual Studio 2017 г.) Вверху hello hello диалогового окна выберите **обновления**.</span><span class="sxs-lookup"><span data-stu-id="880fc-116">(Visual Studio 2017) At hello top of hello dialog, select **Updates**.</span></span> <span data-ttu-id="880fc-117">Выберите пакет tooupdate hello и нажмите кнопку hello **обновление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="880fc-117">Select hello package tooupdate, and click hello **Update** button.</span></span>
* <span data-ttu-id="880fc-118">Выполните сборку и развертывание.</span><span class="sxs-lookup"><span data-stu-id="880fc-118">Build and Deploy.</span></span> 

<span data-ttu-id="880fc-119">**2. Обновите свои сценарии.**</span><span class="sxs-lookup"><span data-stu-id="880fc-119">**2. Upgrade your scripts.**</span></span> <span data-ttu-id="880fc-120">При использовании **PowerShell** скрипты сегментов toomanage [Загрузите новую версию библиотеки hello](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) и скопируйте его в каталог hello, из которого выполнение скриптов.</span><span class="sxs-lookup"><span data-stu-id="880fc-120">If you are using **PowerShell** scripts toomanage shards, [download hello new library version](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) and copy it into hello directory from which you execute scripts.</span></span> 

<span data-ttu-id="880fc-121">**3. Обновите свои службы разбиения и объединения.**</span><span class="sxs-lookup"><span data-stu-id="880fc-121">**3. Upgrade your split-merge service.**</span></span> <span data-ttu-id="880fc-122">Если вы используете hello эластичной базы данных средства слияния разбиение tooreorganize сегментированных данных [загрузить и установить последнюю версию средства hello hello](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/).</span><span class="sxs-lookup"><span data-stu-id="880fc-122">If you use hello elastic database split-merge tool tooreorganize sharded data, [download and deploy hello latest version of hello tool](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/).</span></span> <span data-ttu-id="880fc-123">Подробные шаги обновления по можно найти службу hello [здесь](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="880fc-123">Detailed upgrade steps for hello Service can be found [here](sql-database-elastic-scale-overview-split-and-merge.md).</span></span> 

<span data-ttu-id="880fc-124">**4. Обновите базы данных диспетчера карты сегментов**.</span><span class="sxs-lookup"><span data-stu-id="880fc-124">**4. Upgrade your Shard Map Manager databases**.</span></span> <span data-ttu-id="880fc-125">Обновление метаданных hello поддержка картах сегментов в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="880fc-125">Upgrade hello metadata supporting your Shard Maps in Azure SQL Database.</span></span>  <span data-ttu-id="880fc-126">Это можно сделать двумя способами — с помощью PowerShell или C#.</span><span class="sxs-lookup"><span data-stu-id="880fc-126">There are two ways you can accomplish this, using PowerShell or C#.</span></span> <span data-ttu-id="880fc-127">Ниже описаны оба этих способа.</span><span class="sxs-lookup"><span data-stu-id="880fc-127">Both options are shown below.</span></span>

<span data-ttu-id="880fc-128">***Вариант 1. Обновление метаданных с помощью PowerShell***</span><span class="sxs-lookup"><span data-stu-id="880fc-128">***Option 1: Upgrade metadata using PowerShell***</span></span>

1. <span data-ttu-id="880fc-129">Загрузка hello последняя версия программы командной строки для NuGet из [здесь](http://nuget.org/nuget.exe) и tooa папку для сохранения.</span><span class="sxs-lookup"><span data-stu-id="880fc-129">Download hello latest command-line utility for NuGet from [here](http://nuget.org/nuget.exe) and save tooa folder.</span></span> 
2. <span data-ttu-id="880fc-130">Откройте командную строку, toohello перейдите к папке, а команда hello проблемы:`nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`</span><span class="sxs-lookup"><span data-stu-id="880fc-130">Open a Command Prompt, navigate toohello same folder, and issue hello command: `nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`</span></span>
3. <span data-ttu-id="880fc-131">Найдите toohello вложенной папкой, содержащей hello новой библиотеки DLL версии клиента, только что загруженный, например:`cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`</span><span class="sxs-lookup"><span data-stu-id="880fc-131">Navigate toohello subfolder containing hello new client DLL version you have just downloaded, for example: `cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`</span></span>
4. <span data-ttu-id="880fc-132">Загрузить обновления сценариев hello эластичной базы данных клиента из hello [центра сценариев](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), и сохраните его в hello же папку, содержащую hello DLL.</span><span class="sxs-lookup"><span data-stu-id="880fc-132">Download hello elastic database client upgrade scriptlet from hello [Script Center](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), and save it into hello same folder containing hello DLL.</span></span>
5. <span data-ttu-id="880fc-133">Из этой папки запустите «.\upgrade.ps1 PowerShell» из командной строки hello и следуйте появляющимся на hello.</span><span class="sxs-lookup"><span data-stu-id="880fc-133">From that folder, run “PowerShell .\upgrade.ps1” from hello command prompt and follow hello prompts.</span></span>

<span data-ttu-id="880fc-134">***Вариант 2. Обновление метаданных с помощью C#***</span><span class="sxs-lookup"><span data-stu-id="880fc-134">***Option 2: Upgrade metadata using C#***</span></span>

<span data-ttu-id="880fc-135">Кроме того, создать приложение Visual Studio, открывающий вашей ShardMapManager, выполняет итерацию по всем сегментам и выполняет обновление метаданных hello путем вызова методов hello [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) и [ UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="880fc-135">Alternatively, create a Visual Studio application that opens your ShardMapManager, iterates over all shards, and performs hello metadata upgrade by calling hello methods [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) and [UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) as in this example:</span></span> 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

<span data-ttu-id="880fc-136">Эти методы обновления метаданных могут многократно применяться без каких-либо последствий.</span><span class="sxs-lookup"><span data-stu-id="880fc-136">These techniques for metadata upgrades can be applied multiple times without harm.</span></span> <span data-ttu-id="880fc-137">Например, если старая версия клиента случайно создает тот или иной сегмент после уже обновления, обновление можно запустить снова по всем сегментам tooensure, hello последнюю версию метаданных присутствует в инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="880fc-137">For example, if an older client version inadvertently creates a shard after you have already updated, you can run upgrade again across all shards tooensure that hello latest metadata version is present throughout your infrastructure.</span></span> 

<span data-ttu-id="880fc-138">**Примечание:** до даты публикации новых версий клиентской библиотеки hello продолжить toowork с предыдущими версиями hello диспетчера карты сегментов метаданных в базе данных SQL Azure и наоборот.</span><span class="sxs-lookup"><span data-stu-id="880fc-138">**Note:**  New versions of hello client library published to-date continue toowork with prior versions of hello Shard Map Manager metadata on Azure SQL DB, and vice-versa.</span></span>   <span data-ttu-id="880fc-139">Тем не менее tootake преимуществами новых функций hello hello последнюю версию клиента, метаданные необходимо обновить toobe.</span><span class="sxs-lookup"><span data-stu-id="880fc-139">However tootake advantage of some of hello new features in hello latest client, metadata needs toobe upgraded.</span></span>   <span data-ttu-id="880fc-140">Обратите внимание, что обновление метаданных не повлияет на данные пользователя или данные приложения, созданные и используемые hello диспетчера карты сегментов только объекты.</span><span class="sxs-lookup"><span data-stu-id="880fc-140">Note that metadata upgrades will not affect any user-data or application-specific data, only objects created and used by hello Shard Map Manager.</span></span>  <span data-ttu-id="880fc-141">И приложения по-прежнему toooperate через последовательность обновления hello, описанных выше.</span><span class="sxs-lookup"><span data-stu-id="880fc-141">And applications continue toooperate through hello upgrade sequence described above.</span></span> 

## <a name="elastic-database-client-version-history"></a><span data-ttu-id="880fc-142">Журнал версий клиента эластичной базы данных</span><span class="sxs-lookup"><span data-stu-id="880fc-142">Elastic database client version history</span></span>
<span data-ttu-id="880fc-143">Журнал версий, см. слишком[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)</span><span class="sxs-lookup"><span data-stu-id="880fc-143">For version history, go too[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:./media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png

