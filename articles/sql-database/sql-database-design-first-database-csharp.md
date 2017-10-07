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
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a><span data-ttu-id="51fe7-103">Проектирование базы данных SQL Azure и подключение к ней с помощью C# и ADO.NET</span><span class="sxs-lookup"><span data-stu-id="51fe7-103">Design an Azure SQL database and connect with C&#x23; and ADO.NET</span></span>

<span data-ttu-id="51fe7-104">База данных SQL Azure — это реляционной базы данных как a служба (DBaaS) в hello облака Майкрософт («Azure»).</span><span class="sxs-lookup"><span data-stu-id="51fe7-104">Azure SQL Database is a relational database-as-a service (DBaaS) in hello Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="51fe7-105">В этом учебнике вы узнаете, как toouse hello портал Azure и ADO.NET с помощью Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="51fe7-105">In this tutorial, you learn how toouse hello Azure portal and ADO.NET with Visual Studio to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="51fe7-106">Создание базы данных в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="51fe7-106">Create a database in hello Azure portal</span></span>
> * <span data-ttu-id="51fe7-107">Настройка правила брандмауэра уровня сервера в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="51fe7-107">Set up a server-level firewall rule in hello Azure portal</span></span>
> * <span data-ttu-id="51fe7-108">Подключение toohello базы данных с помощью ADO.NET и Visual Studio</span><span class="sxs-lookup"><span data-stu-id="51fe7-108">Connect toohello database with ADO.NET and Visual Studio</span></span>
> * <span data-ttu-id="51fe7-109">создать таблицы с помощью ADO.NET;</span><span class="sxs-lookup"><span data-stu-id="51fe7-109">Create tables with ADO.NET</span></span>
> * <span data-ttu-id="51fe7-110">вставить, обновить и удалить данные с помощью ADO.NET;</span><span class="sxs-lookup"><span data-stu-id="51fe7-110">Insert, update, and delete data with ADO.NET</span></span> 
> * <span data-ttu-id="51fe7-111">выполнить запрос данных с помощью ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="51fe7-111">Query data ADO.NET</span></span>

<span data-ttu-id="51fe7-112">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="51fe7-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51fe7-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="51fe7-113">Prerequisites</span></span>

<span data-ttu-id="51fe7-114">Убедитесь, что установлен [Visual Studio Community 2017, Visual Studio Professional 2017 или Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="51fe7-114">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

<!-- hello following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- hello following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a><span data-ttu-id="51fe7-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="51fe7-115">Next steps</span></span>

<span data-ttu-id="51fe7-116">В этом учебнике вы узнали, что базовые задачи базами данных, такие как создание базы данных и таблиц, загрузить и запрашивать данные и восстановить hello базы данных tooa предыдущий момент времени.</span><span class="sxs-lookup"><span data-stu-id="51fe7-116">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore hello database tooa previous point in time.</span></span> <span data-ttu-id="51fe7-117">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="51fe7-117">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="51fe7-118">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="51fe7-118">Create a database</span></span>
> * <span data-ttu-id="51fe7-119">Настройка правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="51fe7-119">Set up a firewall rule</span></span>
> * <span data-ttu-id="51fe7-120">Соединения с базой данных, toohello [C# и Visual Studio](sql-database-connect-query-dotnet-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="51fe7-120">Connect toohello database with [Visual Studio and C#](sql-database-connect-query-dotnet-visual-studio.md)</span></span>
> * <span data-ttu-id="51fe7-121">создание таблиц.</span><span class="sxs-lookup"><span data-stu-id="51fe7-121">Create tables</span></span>
> * <span data-ttu-id="51fe7-122">вставлять, обновлять и удалять данные;</span><span class="sxs-lookup"><span data-stu-id="51fe7-122">Insert, update, and delete data</span></span>
> * <span data-ttu-id="51fe7-123">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="51fe7-123">Query data</span></span>

<span data-ttu-id="51fe7-124">Переместить следующий учебник toolearn toohello о миграции данных.</span><span class="sxs-lookup"><span data-stu-id="51fe7-124">Advance toohello next tutorial toolearn about migrating your data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="51fe7-125">Перенос вашей tooAzure базы данных SQL Server база данных SQL</span><span class="sxs-lookup"><span data-stu-id="51fe7-125">Migrate your SQL Server database tooAzure SQL Database</span></span>](sql-database-migrate-your-sql-server-database.md)

