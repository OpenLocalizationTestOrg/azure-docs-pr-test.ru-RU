---
title: "aaaGet работы со средствами эластичной базы данных | Документы Microsoft"
description: "Общее объяснение hello эластичной базы данных средства для базы данных SQL Azure, включая приложения для выполнения образца."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: CarlRabeler
ms.assetid: b6911f8d-2bae-4d04-9fa8-f79a3db7129d
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: a84e05c39dffbaef440538602f898acee6e0483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-elastic-database-tools"></a>Приступая к работе с инструментами эластичных баз данных
В этом документе представлены toohello разработчиков, помогая пример приложения hello toorun. Образец Hello создается простое приложение сегментированных и рассматриваются ключевые возможности средств эластичной базы данных. Образец Hello демонстрирует функции hello [клиентской библиотеке эластичной базы данных](sql-database-elastic-database-client-library.md).

Библиотека tooinstall hello, перейдите в слишком[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). Hello библиотека устанавливается вместе с пример приложения hello, как описано в следующем разделе hello.

## <a name="prerequisites"></a>Предварительные требования
* Visual Studio 2012 или более поздней версии с C#. Загрузите бесплатную версию на странице [Загрузок Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).
* NuGet 2.7 или более поздней версии. tooget hello последнюю версию см. в разделе [Установка NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).

## <a name="download-and-run-hello-sample-app"></a>Загрузите и запустите пример приложения hello
Hello **эластичных БД средства для SQL Azure — начало работы** примере приложения показано наиболее важные аспекты hello hello опыт разработки для сегментированных приложений, использующих средства эластичной базы данных. В нем описаны основные варианты использования для [управления сопоставлениями сегментов](sql-database-elastic-scale-shard-map-management.md), [маршрутизации, зависящей от данных](sql-database-elastic-scale-data-dependent-routing.md), и [многосегментного формирования запросов](sql-database-elastic-scale-multishard-querying.md). toodownload и выполнения hello образец, выполните следующие действия. 

1. Загрузите hello [эластичных БД средства для SQL Azure — пример начала работы](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-a80d8dc6) с MSDN. Распакуйте hello образец tooa с выбранным местоположением.

2. toocreate проекта, откройте hello **ElasticScaleStarterKit.sln** решения из hello **C#** каталога.

3. В решении hello для hello образец проекта, откройте hello **app.config** файла. Имя сервера базы данных SQL Azure и данные входа в систему (имя пользователя и пароль), следуйте инструкциям hello в файл tooadd hello.

4. Постройте и запустите приложение hello. При появлении запроса включите пакеты NuGet Visual Studio toorestore hello hello решения. Это загружает последнюю версию клиентской библиотеке эластичной базы данных hello hello из NuGet.

5. Поэкспериментируйте с toolearn различные варианты hello Дополнительные сведения о возможности библиотеки клиентских hello. Обратите внимание, шаги hello hello принимает приложения в выходных данных консоли hello и считаете кода hello свободного tooexplore фоновом hello.
   
    ![Ход выполнения][4]

Поздравляем! Вы успешно создали и запустили свое первое сегментированное приложение с помощью инструментов эластичной базы данных SQL. Visual Studio или SQL Server Management Studio базы данных SQL tooconnect tooyour и кратко рассмотрим hello создан образец hello сегментов. Вы увидите новый сегмент образцы баз данных и базы данных диспетчера карты сегментов создал этого образца hello.

> [!IMPORTANT]
> Рекомендуется всегда использовать последнюю версию среды Management Studio hello оставались синхронизирован с tooAzure обновления и базы данных SQL. [Обновите среду SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

### <a name="key-pieces-of-hello-code-sample"></a>Основные образец кода hello
* **Управление сегментов и сегментов сопоставляет**: hello кода показано, как toowork с сегментами, диапазоны и сопоставления в файле hello **ShardManagementUtils.cs**. Дополнительные сведения см. в разделе [горизонтальное масштабирование баз данных с использованием диспетчера карты сегментов hello](http://go.microsoft.com/?linkid=9862595).  

* **Маршрутизации в зависимости от данных**: маршрутизацию правой сегментов toohello транзакций отображается в **DataDependentRoutingSample.cs**. Дополнительные сведения см. в статье [Маршрутизация, зависящая от данных](http://go.microsoft.com/?linkid=9862596). 

* **Запросы по нескольким сегментам**: запрос по сегментам проиллюстрирован в файле hello **MultiShardQuerySample.cs**. Дополнительные сведения см. в статье [Многосегментное формирование запросов](http://go.microsoft.com/?linkid=9862597).

* **Добавление пустой сегментов**: hello итерации, добавление новой пустой сегментов осуществляется hello код в файле hello **CreateShardSample.cs**. Дополнительные сведения см. в разделе [горизонтальное масштабирование баз данных с использованием диспетчера карты сегментов hello](http://go.microsoft.com/?linkid=9862595).

### <a name="other-elastic-scale-operations"></a>Другие операции, относящиеся к эластичному масштабированию
* **Разделение существующего сегмента**: hello возможность toosplit сегментами, предоставляемые hello **средством слияния разбиение**. Дополнительные сведения см. в статье [Перемещение данных между масштабируемыми облачными базами данных](sql-database-elastic-scale-overview-split-and-merge.md).

* **Слияние существующим сегментам**: слияний сегментов также выполняются с использованием hello **средством слияния разбиение**. Дополнительные сведения см. в статье [Перемещение данных между масштабируемыми облачными базами данных](sql-database-elastic-scale-overview-split-and-merge.md).   

## <a name="cost"></a>Стоимость
свободны Hello эластичной базы данных средства. При использовании инструментов эластичной базы данных, вы не будете получать любые дополнительные издержки на основе стоимости hello Azure использования. 

Например образец приложения hello создает новые базы данных. Hello стоимость зависит от выбранной версии базы данных SQL hello и hello Azure использования приложения.

Сведения о ценах см. на [странице с ценами на базу данных SQL](https://azure.microsoft.com/pricing/details/sql-database/).

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о средствах эластичной базы данных см. следующие страницы приветствия.

* Примеры кода: 
  * [Инструменты эластичной базы данных SQL Azure — приступая к работе](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-a80d8dc6?SRC=VSIDE)
  * [Инструменты эластичной базы данных SQL Azure — интеграция с Entity Framework](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-bae904ba?SRC=VSIDE).
  * [Эластичность сегментов в Центре сценариев](https://gallery.technet.microsoft.com/scriptcenter/Elastic-Scale-Shard-c9530cbe)
* Блог: [объявление, касающееся эластичного масштабирования](https://azure.microsoft.com/blog/2014/10/02/introducing-elastic-scale-preview-for-azure-sql-database/)
* Microsoft Virtual Academy: [реализации горизонтального масштабирования с использованием сегментирования с hello эластичной базы данных клиента библиотека видео](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554?l=lWyQhF1fC_6306218965) 
* Channel 9: [видеообзор технологии эластичного масштабирования](http://channel9.msdn.com/Shows/Data-Exposed/Azure-SQL-Database-Elastic-Scale)
* Форум для обсуждений: [форум по базам данных SQL Azure](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)
* производительность toomeasure: [счетчики производительности для диспетчера карты сегментов](sql-database-elastic-database-client-library.md)

<!--Anchors-->
[hello Elastic Scale Sample Application]: #The-Elastic-Scale-Sample-Application
[Download and Run hello Sample App]: #Download-and-Run-the-Sample-App
[Cost]: #Cost
[Next steps]: #next-steps

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-get-started/newProject.png
[2]: ./media/sql-database-elastic-scale-get-started/click-online.png
[3]: ./media/sql-database-elastic-scale-get-started/click-CSharp.png
[4]: ./media/sql-database-elastic-scale-get-started/output2.png

