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
ms.openlocfilehash: 13456a8e7652850baacb53730cc7bb1520b0a4c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="b89dc-103">Отмена и удаление заданий службы импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="b89dc-103">Canceling and deleting Azure Import/Export jobs</span></span>

 <span data-ttu-id="b89dc-104">toorequest при отмене задания перед ним находится в hello `Packaging` состояние, вызов hello [обновления свойств задания](/rest/api/storageimportexport/jobs#Jobs_Update) операции и набор hello `CancelRequested` элемент слишком`true`.</span><span class="sxs-lookup"><span data-stu-id="b89dc-104">toorequest that a job be canceled before it is in hello `Packaging` state, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and set hello `CancelRequested` element too`true`.</span></span> <span data-ttu-id="b89dc-105">Hello задание отменено на наилучшим возможным образом.</span><span class="sxs-lookup"><span data-stu-id="b89dc-105">hello job is canceled on a best-effort basis.</span></span> <span data-ttu-id="b89dc-106">Если диски используются hello процесс передачи данных, данных может продолжиться toobe после получения запрошена отмена.</span><span class="sxs-lookup"><span data-stu-id="b89dc-106">If drives are in hello process of transferring data, data may continue toobe transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="b89dc-107">Отмененному заданию является перемещенный toohello `Completed` состояние и хранится в течение 90 дней, после чего она удаляется.</span><span class="sxs-lookup"><span data-stu-id="b89dc-107">A canceled job is moved toohello `Completed` state and is kept for 90 days, at which point it is deleted.</span></span>

 <span data-ttu-id="b89dc-108">toodelete задания hello вызовов [удалить задание](/rest/api/storageimportexport/jobs#Jobs_Delete) операции перед отправкой задания hello (то есть пока задание hello в hello `Creating` состояние).</span><span class="sxs-lookup"><span data-stu-id="b89dc-108">toodelete a job, call hello [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before hello job has shipped (that is, while hello job is in hello `Creating` state).</span></span> <span data-ttu-id="b89dc-109">Задание также можно удалить, когда он находится в hello `Completed` состояния.</span><span class="sxs-lookup"><span data-stu-id="b89dc-109">You can also delete a job when it is in hello `Completed` state.</span></span> <span data-ttu-id="b89dc-110">После удаления задания его данные и состояние больше не доступны через API-Интерфейс REST hello или hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b89dc-110">After a job is deleted, its information and status are no longer accessible via hello REST API or hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b89dc-111">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b89dc-111">Next steps</span></span>

* [<span data-ttu-id="b89dc-112">С помощью REST API службы импорта и экспорта hello</span><span class="sxs-lookup"><span data-stu-id="b89dc-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
