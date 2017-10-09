---
title: "aaaDiscover, идентификации и распределить персональные данные в Microsoft Azure | Документы Microsoft"
description: "Узнайте о поиске, классификации, обнаружении и идентификации данных"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: af4ced1c57699dc751d55cfdf3229c7d294648a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="discover-identify-and-classify-personal-data-in-microsoft-azure"></a>Обнаружение, идентификация и классификация персональных данных в Microsoft Azure

В этой статье содержатся сведения о том, как toodiscover, идентификации, классифицировать персональные данные в нескольких инструментов Azure и служб, в том числе с помощью каталога данных Azure, Azure Active Directory, база данных SQL, Power Query для кластеров Hadoop в Azure HDInsight, Azure Запросы защиты информации, поиска Azure и SQL для Azure Cosmos DB.

## <a name="scenario-problem-statement-and-goal"></a>Сценарий, формулировка проблемы и цель

Компания США, ведущая деятельность в спортивной отрасли, осуществляет сбор различных персональных и других данных, таких как данные о сотрудниках и клиентах. Компания Hello сохраняется в нескольких базах данных и сохраняет его в нескольких разных местах в их среде Azure. Кроме tooselling спортивных оборудования, они также размещать и управлять ими регистрации для интеллектуальных соревнований событий вокруг Здравствуй, мир, включая в hello Европа, и в некоторых случаях hello данные клиента, которые они собирают медицинские сведения.

Поскольку компания hello содержит много международного bicycling обзоры каждый год и имеет временный персонал в точках земного шара hello, несколько наборов данных hello довольно велики. Hello компании также имеет встроенные разработчика приложений, используемых клиентами и сотрудниками.

Hello фирма hello tooaddress следующие проблемы:

- Клиентов и личные данные должны быть классификации и отличить от hello другие компании hello данных собирает данные в порядке tooensure права доступа и безопасности.
- Hello данных необходимыми tooeasily обнаружение hello расположение личных данных клиента в различных областях hello среды Azure.
- Клиентов и личные данные, отображаемые в Общие документы и сообщения электронной почты должен называться toohelp обеспечить надежно защищены.
- Разработчики приложения Hello компании должны tooeasily способ поиска клиентов и персональные данные в своих веб- и мобильных приложений.
- Разработчики также должны tooquery их базу данных документов для личных данных.

### <a name="company-goals"></a>Цели компании

- Все персональные данные клиентов и сотрудников должны быть помечены тегами или заметками в каталоге данных Azure для их быстрого поиска. В идеале персональные данные клиентов и сотрудников помечаются тегами или заметками по отдельности.
- Должна быть доступна возможность быстрого поиска персональных данных в профилях клиентов и сотрудников, а также сведений о работе в Azure Active Directory.
- Должна быть доступна возможность быстрого запроса персональных данных в нескольких базах данных SQL. 
- Некоторые компании hello больших наборов данных, управляемых с помощью Azure HDInsight и сохраняются в Hadoop. Должна быть доступна возможность их импорта в Excel, а также последующего запроса персональных данных.
- Персональные данные для общего доступа в документах и сообщениях электронной почты должны быть классифицированы, маркированы и защищены с помощью Azure Information Protection.
- Hello компании приложения несут разработчики могут toodiscover клиентов и персональные данные в приложения hello, которой они созданы, которым можно делать с поиском Azure.
- Разработчики должны быть может toofind персональные данные в их базе данных документа.

## <a name="azure-active-directory-data-discovery"></a>Azure Active Directory: обнаружение данных

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) — это мультитенантный облачный каталог и служба управления удостоверениями Майкрософт. Вы можете найти клиентов и профилей пользователей и информация о работы пользователя, содержать персональные данные в вашей [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) среды (AAD), используя hello [портал Azure](https://portal.azure.com/).

Это особенно полезно, если требуется toofind или изменить личные данные для конкретного пользователя. Вы также можете добавить или изменить профиль пользователя и сведения о работе. Необходимо войти с учетной записью глобального администратора каталога hello.

### <a name="how-do-i-locate-or-view-user-profile-and-work-information"></a>Как я могу найти или просмотреть профиль пользователя и сведения о работе?

1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.

2. Выберите **дополнительные службы**, введите **пользователей и групп** в hello текстовое поле, а затем выберите **ввод**.

   ![поиск профиля пользователя и сведений о работе](media/how-to-discover-classify-personal-data-azure/user-profile.png)

3. На hello **пользователей и групп** колонке выберите **пользователей**.

  ![Открытие колонки пользователей и групп](media/how-to-discover-classify-personal-data-azure/users-groups.png)

4. На hello **пользователей и групп - Пользователи** колонке выберите пользователя из списка hello и выберите в колонке hello для выбранного пользователя hello, **профиль** сведения профиля пользователя tooview, которое может содержать персональные данные .

  ![выбрать пользователя](media/how-to-discover-classify-personal-data-azure/select-user.png)

5. Если необходимо tooadd или изменить сведения о профиле пользователя, сделать это и выберите на панели команд hello, **сохранить.**
6. В колонке hello для выбранного пользователя hello, выберите **сведения о работе** сведения о рабочих tooview пользователя, могут содержать персональные данные.

 ![просмотр сведений о работе](media/how-to-discover-classify-personal-data-azure/work-info.png)

7. Если необходимо tooadd или изменение рабочих сведений пользователя, сделать это и выберите на панели команд hello, **сохранить.**

## <a name="azure-sql-database-data-discovery"></a>База данных SQL Azure: обнаружение данных

[База данных SQL Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) — это облачная база данных, позволяющая разработчикам создавать приложения и управлять ими. Персональные данные можно найти в [базе данных SQL Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) с помощью стандартных запросов SQL. Azure эластичной запросов SQL (Предварительная версия) позволяет пользователям tooperform межбазовые запросы.

Подробные [базы данных SQL](../sql-database/sql-database-technical-overview.md) учебнике описано множество аспектов работы с базой данных SQL, включая то, как toobuild одно и как toorun запросы данных. Hello ниже приводится сводка hello информации, доступной в учебнике hello с разделами toospecific ссылки.

### <a name="how-do-i-build-a-sql-database"></a>Как создать базу данных SQL?

Существует три способа toodo его:

- Можно создать базу данных Azure SQL в hello [портал Azure](https://portal.azure.com/). В учебнике hello будет использовать специальный набор вычислений и хранения ресурсов в рамках группы ресурсов и логических серверов. Вы будете использовать пример данных вымышленной компании AdventureWorks. Вы также создадите правило брандмауэра на уровне сервера. toolearn как toodo, посетите hello [создать базу данных Azure SQL в hello портал Azure](../sql-database/sql-database-get-started-portal.md) учебника.

  ![Создание базы данных SQL Azure](media/how-to-discover-classify-personal-data-azure/create-database.png)
- База данных SQL также могут создаваться в hello [оболочки облако Azure](https://azure.microsoft.com/features/cloud-shell/) CLI, средство командной строки на основе браузера. Hello средство доступно в hello портал Azure и запускается непосредственно из него. В этом учебнике запустите средство hello, определения переменных сценария, создайте группу ресурсов и логических серверов и настроить правила брандмауэра для сервера. Затем вы создадите базу данных с примерами данных. toolearn как toocreate базы данных таким образом, посетите hello [создание одной базы данных Azure SQL с помощью Azure CLI hello](../sql-database/sql-database-get-started-cli.md) учебника.

  ![Руководство по созданию отдельной базы данных SQL Azure с помощью Azure CLI](media/how-to-discover-classify-personal-data-azure/cli-tutorial.png)

>[!NOTE]
Azure CLI часто используют администраторы и разработчики Linux. Некоторые пользователи считают Azure CLI более простым и интуитивно понятным средством по сравнению с PowerShell, использующимся в качестве третьего варианта.

- Наконец можно создать с помощью PowerShell, которая является toocreate средство командной строки или скрипта базы данных SQL и управления Azure и другие ресурсы. В этом учебнике запустите средство hello, определения переменных сценария, создайте группу ресурсов и логических серверов и настроить правила брандмауэра для сервера. Затем вы создадите базу данных с примерами данных.

Учебник Hello требует hello Azure PowerShell модуль версии 4.0 или более поздней версии. Запустите командлет Get-Module - ListAvailable AzureRM toofind вашей версии. Если требуется tooinstall или обновления, см. Установите Azure PowerShell модуль.

```PowerShell
New-AzureRmSQLDatabase -ResourceGroupName $resourcegroupname `
-ServerName $servername `
-DatabaseName $databasename `
-RequestedServiceObjectiveName "s0"
```

toolearn как toocreate базы данных таким образом, посетите hello [создание одной базы данных Azure SQL с помощью Powershell](../sql-database/sql-database-get-started-powershell.md) учебника.

>[!Note]
«Администраторы» Windows, как правило, toouse PowerShell, но некоторые из них предпочитают Azure CLI.

### <a name="how-do-i-search-for-personal-data-in-sql-database-in-hello-azure-portal"></a>Как поиск персональные данные в базе данных SQL в hello портал Azure? **

Можно использовать средство редактор hello встроенных запросов внутри hello Azure портала toosearch личных сведений. Будет войти toohello средство, используя имя входа администратора SQL server и пароль, а затем введите запрос.

  ![поиск с помощью портала hello sql](media/how-to-discover-classify-personal-data-azure/search-sql-portal.png)

Шаг 5 учебного курса hello показан пример запроса в hello окна редактора запросов, но он не нацелена на личных или конфиденциальных сведений (он также объединяет данные из двух таблиц и создаются псевдонимы для hello исходного столбца в наборе данных hello, возвращаемых). Hello следующем снимке экрана показан запрос hello в шаге 5, а также hello панель результатов, возвращаемый:

  ![редактор запросов](media/how-to-discover-classify-personal-data-azure/query-editor.png)

Для базы данных с именем MyTable пример запроса персональных сведений будет включать имя, номер социального страхования и идентификатор. Запрос будет выглядеть следующим образом:

"Выбор имени, номера социального страхования (SSN) и идентификатора из базы данных MyTable"

Вам потребуется выполнить запрос hello и затем просмотреть результаты hello в hello **результатов** области.

Дополнительные сведения о как tooquery SQL базы данных в hello портал Azure, посетите hello [hello запрос SQL к базе данных](../sql-database/sql-database-get-started-portal.md) разделе учебника hello.

### <a name="how-do-i-search-for-data-across-multiple-databases"></a>Как выполнить поиск данных по нескольким базам данных?

Эластичный запросов SQL (Предварительная версия) позволяет вам tooperform между базами данных и нескольких запросов к базе данных и получения единого результата. Hello [учебника Обзор](../sql-database/sql-database-elastic-query-overview.md) включает подробное описание сценариев и объясняется hello различие между базы данных вертикальное и горизонтальное секционирование. Горизонтальное секционирование называется сегментированием.

  ![Вертикальное секционирование](media/how-to-discover-classify-personal-data-azure/vertical-partition.png)

  ![горизонтальное секционирование](media/how-to-discover-classify-personal-data-azure/horizontal.png)

tooget к работе, посетите hello [Общие сведения о запросах эластичной базы данных SQL Azure (Предварительная версия)](../sql-database/sql-database-elastic-query-overview.md) страницы.

#### <a name="power-query-for-importing-azure-hdinsight-hadoop-clusters-data-discovery-for-large-data-sets"></a>Power Query (для импорта кластеров Hadoop в Azure HDInsight): обнаружение данных больших наборов данных

Hadoop является хранилищем Apache с открытым кодом и службой обработки больших наборов данных, анализируемых и хранящихся в кластерах Hadoop. [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) позволяет пользователям toowork с Hadoop кластеров в Azure. Power Query является надстройкой Excel, которая, помимо прочего, позволяет пользователям обнаруживать данные из различных источников.

Личные данные, связанные с кластерами Hadoop в Azure HDInsight может быть tooExcel, импортированные с помощью Power Query. После загрузки данных hello в Excel можно использовать tooidentify запроса его.

#### <a name="how-do-i-use-excel-power-query-tooimport-hadoop-clusters-in-azure-hdinsight-into-excel"></a>Как использовать кластеров Hadoop tooimport Excel Power Query в Azure HDInsight в Excel?

С помощью руководства по HDInsight вы можете подробно ознакомиться с этим процессом. Он описывается необходимые компоненты и включает tooa ссылку [Приступая к работе с Azure HDInsight](../hdinsight/hdinsight-hadoop-linux-tutorial-get-started.md) учебника. Инструкции охватывают Excel 2016, а также 2013 и 2010 (действия несколько различаются для более старых версий Excel hello). Если у вас нет надстройки hello Power Query для Excel, hello учебнике показано, как tooget его. Начнем учебника hello в Excel и требуется toohave учетную запись службы хранилища больших двоичных объектов Azure, связанной с кластером.

  ![Запрос в Excel](media/how-to-discover-classify-personal-data-azure/excel.png)

toolearn как toodo, посетите hello [tooHadoop Excel подключиться с помощью Power Query](../hdinsight/hdinsight-connect-excel-power-query.md) учебника.

Источник: [tooHadoop Excel подключиться с помощью Power Query](../hdinsight/hdinsight-connect-excel-power-query.md)

## <a name="azure-information-protection-personal-data-classification-for-documents-and-email"></a>Azure Information Protection: классификация персональных данных документов и электронной почты

[Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) может помочь клиентам Azure применяются tooclassify метки и защищать внутренне или внешне Общие документы и электронные связи. Некоторые из этих элементов могут содержать персональные данные клиентов или сотрудников. Правила и условия можно определить автоматически или вручную. Это могут сделать администраторы или пользователи. Например если пользователь сохраняет документ, содержащий сведения о кредитной карте, он или она бы увидеть рекомендации метки, которые настроена администратором hello.

### <a name="how-do-i-try-it"></a>Как использовать Azure Information Protection?

Если вы хотите toogive Azure Information Protection try toosee, если возможно, подойдет для вашей организации, посетите hello [краткого руководства](https://docs.microsoft.com/information-protection/get-started/infoprotect-quick-start-tutorial). Он поможет выполнить пять простых шагов — из установки tooconfiguring политики tooseeing классификации, пометки и совместное использование в действие — и займет меньше, чем полчаса.

### <a name="how-do-i-deploy-it"></a>Как выполнить развертывание?

Если вы хотите toodeploy Azure Information Protection вашей организации, посетите hello [стратегия развертывания для классификации, пометки и защиты](https://docs.microsoft.com/information-protection/plan-design/deployment-roadmap).

### <a name="is-there-anything-else-i-should-know"></a>Что еще необходимо знать?

Сведения, которые помогут продумайте как tooset его, посетите hello [готовый, задать, защитить!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
записи блога. И проверка hello Дополнительные ссылки, перечисленных ниже для получения дополнительных сведений об Azure Information Protection.

## <a name="azure-search-data-discovery-for-developer-apps"></a>Поиск Azure: обнаружение данных для приложений разработчиков

[Поиск Azure](https://azure.microsoft.com/services/search/) — это облачное решение поиска для разработчиков, предоставляющее обширный набор возможностей поиска данных для приложений. Поиск Azure позволяет toolocate данных между пользовательские индексы, источником для Azure Cosmo DB, база данных SQL Azure, хранилища больших двоичных объектов, хранилище таблиц Azure или клиент пользовательских данных JSON. Также можно структурировать Lucene запросы, использующие toosearch hello REST API поиска Azure для типов личные данные или персональные данные hello объекта для определенных пользователей. Возможности включают полнотекстовый поиск, простой синтаксис запросов и синтаксис запросов Lucene. 

## <a name="how-do-i-use-sql-tooquery-data"></a>Как использовать tooquery данных SQL?

toobegin с основами hello посетите hello [Azure CosmosD DB: как tooquery, с помощью SQL](../cosmos-db/tutorial-query-documentdb.md) учебника. Учебник образец документа и два образца SQL-запросов и результаты Hello.

Чтобы получить более подробные сведения о создании запросов SQL, ознакомьтесь со статьей [SQL-запросы для API DocumentDB в Azure Cosmos DB](../cosmos-db/documentdb-sql-query.md).

Если вы являетесь новый tooAzure Cosmos DB и как toolearn как toocreate базы данных, добавлять коллекции и добавить данные, посещать hello [Azure Cosmos DB: построение веб-приложения DocumentDB API](../cosmos-db/create-documentdb-dotnet.md) краткого руководства. При желании toodo в язык, отличный от .NET, например Java, Python, просто выберите предпочитаемый язык после передачи toohello сайта.

## <a name="next-steps"></a>Дальнейшие действия

[База данных SQL Azure;](https://azure.microsoft.com/services/sql-database/?v=16.50)

[Что такое база данных SQL?](../sql-database/sql-database-technical-overview.md)

[Редактор запросов базы данных SQL доступен на портале Azure] (https://azure.microsoft.com/blog/t-sql-query-editor-in-browser-azure-portal/)

[Что такое Azure Information Protection?](https://docs.microsoft.com/information-protection/understand-explore/what-is-information-protection)

[Что из себя представляет служба управления правами Azure](https://docs.microsoft.com/information-protection/understand-explore/what-is-azure-rms)

[Azure Information Protection: Ready, set, protect!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/) (Azure Information Protection: комплексное использование)
