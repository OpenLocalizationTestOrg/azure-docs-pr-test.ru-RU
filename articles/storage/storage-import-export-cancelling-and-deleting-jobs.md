---
title: "aaaCancel и удалить задание импорта и экспорта Azure | Документы Microsoft"
description: "Узнайте, каким образом задания toocancel и delete для hello службы импорта и экспорта Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 5d2aba510dafd0ca9a10f5643f721e7059a6a8f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="63f75-103">Отмена и удаление заданий службы импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="63f75-103">Canceling and deleting Azure Import/Export jobs</span></span>

<span data-ttu-id="63f75-104">Вы можете запросить отмену задания до ее hello `Packaging` состояния, вызывающему Привет [обновления свойств задания](/rest/api/storageimportexport/jobs#Jobs_Update) операции, а параметр hello `CancelRequested` элемент слишком`true`.</span><span class="sxs-lookup"><span data-stu-id="63f75-104">You can request that a job be cancelled before it is in hello `Packaging` state by calling hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and setting hello `CancelRequested` element too`true`.</span></span> <span data-ttu-id="63f75-105">Hello задание будет отменено на наилучшим возможным образом.</span><span class="sxs-lookup"><span data-stu-id="63f75-105">hello job will be cancelled on a best-effort basis.</span></span> <span data-ttu-id="63f75-106">Если диски используются hello процесс передачи данных, данных может продолжиться toobe после получения запрошена отмена.</span><span class="sxs-lookup"><span data-stu-id="63f75-106">If drives are in hello process of transferring data, data may continue toobe transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="63f75-107">Отмененное задание перейдет toohello `Completed` состояние и храниться в течение 90 дней, после чего она будет удалена.</span><span class="sxs-lookup"><span data-stu-id="63f75-107">A cancelled job will move toohello `Completed` state and be kept for 90 days, at which point it will be deleted.</span></span>

 <span data-ttu-id="63f75-108">toodelete задания hello вызовов [удалить задание](/rest/api/storageimportexport/jobs#Jobs_Delete) операции перед отправкой задания hello (*т. е.*, пока задание hello в hello `Creating` состояние).</span><span class="sxs-lookup"><span data-stu-id="63f75-108">toodelete a job, call hello [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before hello job has shipped (*i.e.*, while hello job is in hello `Creating` state).</span></span> <span data-ttu-id="63f75-109">Задание также можно удалить, когда он находится в hello `Completed` состояния.</span><span class="sxs-lookup"><span data-stu-id="63f75-109">You can also delete a job when it is in hello `Completed` state.</span></span> <span data-ttu-id="63f75-110">После удаления задания его данные и состояние больше не доступны через API-Интерфейс REST hello или hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="63f75-110">After a job has been deleted, its information and status are no longer accessible via hello REST API or hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63f75-111">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="63f75-111">Next steps</span></span>

* [<span data-ttu-id="63f75-112">С помощью REST API службы импорта и экспорта hello</span><span class="sxs-lookup"><span data-stu-id="63f75-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
