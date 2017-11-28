---
title: "aaaAzure пакета аналитики | Документы Microsoft"
description: "Справочник по пакетной аналитике Azure."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 462fbad1ac522b485ae18c1e8891b9d2cabd45e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="batch-analytics"></a><span data-ttu-id="ec726-103">Пакетная аналитика</span><span class="sxs-lookup"><span data-stu-id="ec726-103">Batch Analytics</span></span>
<span data-ttu-id="ec726-104">разделы Hello в пакете аналитики содержатся справочные сведения по hello событий и предупреждений, доступных для ресурсов службы пакета.</span><span class="sxs-lookup"><span data-stu-id="ec726-104">hello topics in Batch Analytics contain reference information for hello events and alerts available for Batch service resources.</span></span>

<span data-ttu-id="ec726-105">Статья [Ведение журналов диагностики пакетной службы Azure](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) содержит дополнительные сведения о включении и использовании журналов диагностики пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="ec726-105">See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="ec726-106">Журналы диагностики</span><span class="sxs-lookup"><span data-stu-id="ec726-106">Diagnostic logs</span></span>

<span data-ttu-id="ec726-107">Hello пакетной службы Azure создает следующие события журнала диагностики во время существования hello определенных ресурсов пакета hello.</span><span class="sxs-lookup"><span data-stu-id="ec726-107">hello Azure Batch service emits hello following diagnostic log events during hello lifetime of certain Batch resources.</span></span>

<span data-ttu-id="ec726-108">**События журнала службы**</span><span class="sxs-lookup"><span data-stu-id="ec726-108">**Service Log events**</span></span>
* [<span data-ttu-id="ec726-109">Создание пула</span><span class="sxs-lookup"><span data-stu-id="ec726-109">Pool create</span></span>](batch-pool-create-event.md)
* [<span data-ttu-id="ec726-110">Начало удаления пула</span><span class="sxs-lookup"><span data-stu-id="ec726-110">Pool delete start</span></span>](batch-pool-delete-start-event.md)
* [<span data-ttu-id="ec726-111">Завершение удаления пула</span><span class="sxs-lookup"><span data-stu-id="ec726-111">Pool delete complete</span></span>](batch-pool-delete-complete-event.md)
* [<span data-ttu-id="ec726-112">Начало изменения размера пула</span><span class="sxs-lookup"><span data-stu-id="ec726-112">Pool resize start</span></span>](batch-pool-resize-start-event.md)
* [<span data-ttu-id="ec726-113">Завершение изменения размера пула</span><span class="sxs-lookup"><span data-stu-id="ec726-113">Pool resize complete</span></span>](batch-pool-resize-complete-event.md)
* [<span data-ttu-id="ec726-114">Начало выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="ec726-114">Task start</span></span>](batch-task-start-event.md)
* [<span data-ttu-id="ec726-115">Завершение выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="ec726-115">Task complete</span></span>](batch-task-complete-event.md)
* [<span data-ttu-id="ec726-116">Сбой выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="ec726-116">Task fail</span></span>](batch-task-fail-event.md)