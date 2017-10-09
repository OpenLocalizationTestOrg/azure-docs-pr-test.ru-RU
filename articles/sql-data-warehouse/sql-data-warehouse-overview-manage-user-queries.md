---
title: "aaaMonitor пользователь запросов в хранилище данных SQL Azure | Документы Microsoft"
description: "Общие сведения о hello вопросы, рекомендации и задачи для отслеживания запросов пользователя в хранилище данных SQL Azure"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 1d0960db-5dcf-4a08-b1dc-6c5d3d5a616d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 67639e81b04635452e1ed844fe2d7245aa96a4fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-user-queries-in-azure-sql-data-warehouse"></a><span data-ttu-id="9bf88-103">Мониторинг запросов пользователей в хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="9bf88-103">Monitor user queries in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="9bf88-104">Обзор hello вопросы, рекомендации и задачи для отслеживания запросов пользователя в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="9bf88-104">Overview of hello considerations, best practices, and tasks for monitoring user queries in SQL Data Warehouse.</span></span>

| <span data-ttu-id="9bf88-105">Категория</span><span class="sxs-lookup"><span data-stu-id="9bf88-105">Category</span></span> | <span data-ttu-id="9bf88-106">Задача или рекомендация</span><span class="sxs-lookup"><span data-stu-id="9bf88-106">Task or consideration</span></span> | <span data-ttu-id="9bf88-107">Описание</span><span class="sxs-lookup"><span data-stu-id="9bf88-107">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="9bf88-108">Низкая производительность</span><span class="sxs-lookup"><span data-stu-id="9bf88-108">Slow performance</span></span> |<span data-ttu-id="9bf88-109">Поиск долго выполняющегося запроса пользователя</span><span class="sxs-lookup"><span data-stu-id="9bf88-109">Find a long-running user query</span></span> |<span data-ttu-id="9bf88-110">[Поиск долго выполняющихся запросов][Find long-running queries]</span><span class="sxs-lookup"><span data-stu-id="9bf88-110">[Find long-running queries][Find long-running queries]</span></span> |
| <span data-ttu-id="9bf88-111">Параллелизм</span><span class="sxs-lookup"><span data-stu-id="9bf88-111">Concurrency</span></span> |<span data-ttu-id="9bf88-112">Назначение ресурсов одновременных запросов toouser</span><span class="sxs-lookup"><span data-stu-id="9bf88-112">Assign concurrent resources toouser queries</span></span> |<span data-ttu-id="9bf88-113">[Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL][Concurrency and workload management]</span><span class="sxs-lookup"><span data-stu-id="9bf88-113">[Concurrency and workload management][Concurrency and workload management]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9bf88-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9bf88-114">Next steps</span></span>
<span data-ttu-id="9bf88-115">Дополнительные советы управления перейдите toohello [Общие сведения об управлении][Management overview].</span><span class="sxs-lookup"><span data-stu-id="9bf88-115">For more management tips, head over toohello [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Find long-running queries]: sql-data-warehouse-manage-monitor.md
[Concurrency and workload management]: sql-data-warehouse-develop-concurrency.md
[Management overview]: sql-data-warehouse-overview-manage.md

<!--MSDN references-->


<!--Other Web references-->
