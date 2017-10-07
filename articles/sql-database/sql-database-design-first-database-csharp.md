---
title: "aaaDesign вашей первой базы данных SQL Azure — C# | Документы Microsoft"
description: "Дополнительные сведения toodesign первой базы данных Azure SQL и подключения tooit программы на C# с помощью ADO.NET."
services: sql-database
documentationcenter: 
author: MightyPen
manager: craigg-msft
editor: CarlRabeler
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 07/31/2017
ms.author: genemi;carlrab
ms.openlocfilehash: 8161de24bff1ec2fa307efa93adab2bd1b761fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a>Проектирование базы данных SQL Azure и подключение к ней с помощью C# и ADO.NET

База данных SQL Azure — это реляционной базы данных как a служба (DBaaS) в hello облака Майкрософт («Azure»). В этом учебнике вы узнаете, как toouse hello портал Azure и ADO.NET с помощью Visual Studio: 

> [!div class="checklist"]
> * Создание базы данных в hello портал Azure
> * Настройка правила брандмауэра уровня сервера в hello портал Azure
> * Подключение toohello базы данных с помощью ADO.NET и Visual Studio
> * создать таблицы с помощью ADO.NET;
> * вставить, обновить и удалить данные с помощью ADO.NET; 
> * выполнить запрос данных с помощью ADO.NET.

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/), прежде чем начинать работу.

## <a name="prerequisites"></a>Предварительные требования

Убедитесь, что установлен [Visual Studio Community 2017, Visual Studio Professional 2017 или Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).

<!-- hello following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- hello following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы узнали, что базовые задачи базами данных, такие как создание базы данных и таблиц, загрузить и запрашивать данные и восстановить hello базы данных tooa предыдущий момент времени. Вы научились выполнять следующие задачи:
> [!div class="checklist"]
> * Создание базы данных
> * Настройка правила брандмауэра.
> * Соединения с базой данных, toohello [C# и Visual Studio](sql-database-connect-query-dotnet-visual-studio.md)
> * создание таблиц.
> * вставлять, обновлять и удалять данные;
> * Запрос данных

Переместить следующий учебник toolearn toohello о миграции данных.

> [!div class="nextstepaction"]
>[Перенос вашей tooAzure базы данных SQL Server база данных SQL](sql-database-migrate-your-sql-server-database.md)

