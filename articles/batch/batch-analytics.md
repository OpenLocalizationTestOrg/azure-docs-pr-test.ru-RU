---
title: "Пакетная аналитика Azure | Документы Майкрософт"
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
ms.openlocfilehash: 7d634e1bb595a84b8af339e5bc5a483a7849e7f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="batch-analytics"></a><span data-ttu-id="9c8fa-103">Пакетная аналитика</span><span class="sxs-lookup"><span data-stu-id="9c8fa-103">Batch Analytics</span></span>
<span data-ttu-id="9c8fa-104">Статьи по пакетной аналитике содержат справочные сведения о событиях и оповещениях, доступных для ресурсов пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9c8fa-104">The topics in Batch Analytics contain reference information for the events and alerts available for Batch service resources.</span></span>

<span data-ttu-id="9c8fa-105">Статья [Ведение журналов диагностики пакетной службы Azure](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) содержит дополнительные сведения о включении и использовании журналов диагностики пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9c8fa-105">See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="9c8fa-106">Журналы диагностики</span><span class="sxs-lookup"><span data-stu-id="9c8fa-106">Diagnostic logs</span></span>

<span data-ttu-id="9c8fa-107">За время существования некоторых пакетных ресурсов пакетная служба Azure выдает приведенные ниже события журнала диагностики.</span><span class="sxs-lookup"><span data-stu-id="9c8fa-107">The Azure Batch service emits the following diagnostic log events during the lifetime of certain Batch resources.</span></span>

<span data-ttu-id="9c8fa-108">**События журнала службы**</span><span class="sxs-lookup"><span data-stu-id="9c8fa-108">**Service Log events**</span></span>
* [<span data-ttu-id="9c8fa-109">Создание пула</span><span class="sxs-lookup"><span data-stu-id="9c8fa-109">Pool create</span></span>](batch-pool-create-event.md)
* [<span data-ttu-id="9c8fa-110">Начало удаления пула</span><span class="sxs-lookup"><span data-stu-id="9c8fa-110">Pool delete start</span></span>](batch-pool-delete-start-event.md)
* [<span data-ttu-id="9c8fa-111">Завершение удаления пула</span><span class="sxs-lookup"><span data-stu-id="9c8fa-111">Pool delete complete</span></span>](batch-pool-delete-complete-event.md)
* [<span data-ttu-id="9c8fa-112">Начало изменения размера пула</span><span class="sxs-lookup"><span data-stu-id="9c8fa-112">Pool resize start</span></span>](batch-pool-resize-start-event.md)
* [<span data-ttu-id="9c8fa-113">Завершение изменения размера пула</span><span class="sxs-lookup"><span data-stu-id="9c8fa-113">Pool resize complete</span></span>](batch-pool-resize-complete-event.md)
* [<span data-ttu-id="9c8fa-114">Начало выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="9c8fa-114">Task start</span></span>](batch-task-start-event.md)
* [<span data-ttu-id="9c8fa-115">Завершение выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="9c8fa-115">Task complete</span></span>](batch-task-complete-event.md)
* [<span data-ttu-id="9c8fa-116">Сбой выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="9c8fa-116">Task fail</span></span>](batch-task-fail-event.md)