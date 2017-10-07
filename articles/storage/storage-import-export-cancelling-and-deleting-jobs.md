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
# <a name="canceling-and-deleting-azure-importexport-jobs"></a>Отмена и удаление заданий службы импорта и экспорта Azure

Вы можете запросить отмену задания до ее hello `Packaging` состояния, вызывающему Привет [обновления свойств задания](/rest/api/storageimportexport/jobs#Jobs_Update) операции, а параметр hello `CancelRequested` элемент слишком`true`. Hello задание будет отменено на наилучшим возможным образом. Если диски используются hello процесс передачи данных, данных может продолжиться toobe после получения запрошена отмена.

 Отмененное задание перейдет toohello `Completed` состояние и храниться в течение 90 дней, после чего она будет удалена.

 toodelete задания hello вызовов [удалить задание](/rest/api/storageimportexport/jobs#Jobs_Delete) операции перед отправкой задания hello (*т. е.*, пока задание hello в hello `Creating` состояние). Задание также можно удалить, когда он находится в hello `Completed` состояния. После удаления задания его данные и состояние больше не доступны через API-Интерфейс REST hello или hello портал Azure.

## <a name="next-steps"></a>Дальнейшие действия

* [С помощью REST API службы импорта и экспорта hello](storage-import-export-using-the-rest-api.md)
