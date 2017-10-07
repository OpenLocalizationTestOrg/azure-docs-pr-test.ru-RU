---
title: "hello aaaUsing REST API службы импорта и экспорта Azure | Документы Microsoft"
description: "Узнайте, где toofind ресурсы для hello импорта и экспорта Azure с помощью службы REST API, включая обоих tooand как справочные материалы."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: a01c170b1bc9c2b2ce9086d39de78a39fafb2c8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a>С помощью REST API службы импорта и экспорта Azure hello

Hello службы импорта и экспорта Microsoft Azure предоставляет API-Интерфейс REST tooenable программное управление заданиями импорта и экспорта. Можно использовать API-Интерфейс REST hello tooperform все hello импорта и экспорта операций, которые можно выполнять с hello [портал Azure](https://portal.azure.com/). Кроме того можно использовать tooperform API-интерфейса REST hello определенных детализированных операций, таких как запрос hello процент завершения задания, которые в настоящее время недоступны в классическом портале hello.

В разделе [tooBlob hello импорта и экспорта Microsoft Azure службы tooTransfer данные хранилища с помощью](storage-import-export-service.md) Обзор службы импорта и экспорта hello и учебник, в котором показано, как toouse hello классического портала toocreate и управления импортом и задания экспорта.

## <a name="service-endpoints"></a>Конечные точки службы

Hello службы импорта и экспорта Azure — это поставщик ресурсов для диспетчера ресурсов Azure и предоставляет набор интерфейсов API REST в hello, следующая конечная точка HTTPS для управления заданиями импорта и экспорта:

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a>Управление версиями

Запросы, toohello службы импорта и экспорта необходимо указать hello `api-version` параметр и присвойте ему значение слишком`2016-11-01`.

## <a name="importexport-service-operations"></a>Операции службы импорта и экспорта

[Создание задания импорта](storage-import-export-creating-an-import-job.md)

[Создание задания экспорта](storage-import-export-creating-an-export-job.md)

[Получение сведений о состоянии задания](storage-import-export-retrieving-state-info-for-a-job.md)

[Перечисление заданий](storage-import-export-enumerating-jobs.md)

[Отмена и удаление заданий](storage-import-export-cancelling-and-deleting-jobs.md)

[Архивация манифестов дисков](storage-import-export-backing-up-drive-manifests.md)

[Диагностика и восстановление после ошибок для заданий импорта и экспорта](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a>Дальнейшие действия

* [Storage Import/Export REST](/rest/api/storageimportexport) (Справочник по API REST служб хранилища импорта и экспорта)
