---
title: "aaaBacking копии манифестов дисков для импорта и экспорта Azure | Документы Microsoft"
description: "Узнайте, как toohave дисковод манифесты для службы импорта и экспорта Microsoft Azure hello автоматическое резервное."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 594abd80-b834-4077-a474-d8a0f4b7928a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: f48b97a2cce62714aace2b30a393305202c7ecd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a>Архивация манифестов дисков для заданий импорта и экспорта Azure

Манифестов диска может быть автоматически резервное tooblobs с помощью параметра hello `BackupDriveManifest` свойство слишком`true` в hello [вставки задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) или [обновления свойств задания](/rest/api/storageimportexport/jobs#Jobs_Update) операции REST API. По умолчанию hello манифестов диска не копируются. резервные копии манифестов дисков Hello хранятся как блочные большие двоичные объекты в контейнере в учетной записи хранилища hello, связанный с заданием hello. По умолчанию является имя контейнера hello `waimportexport`, но можно указать другое имя в hello `DiagnosticsPath` свойства при вызове hello `Put Job` или `Update Job Properties` операций. Hello большого двоичного объекта манифеста именуются в hello следующий формат: `waies/jobname_driveid_timestamp_manifest.xml`.

 Вы можете получить URI резервного копирования диска hello манифесты для задания, вызывающему Привет hello [получения задания](/rest/api/storageimportexport/jobs#Jobs_Get) операции. URI, возвращаемый в hello blob Hello `ManifestUri` свойство для каждого диска.

## <a name="next-steps"></a>Дальнейшие действия

* [С помощью REST API службы импорта и экспорта hello](storage-import-export-using-the-rest-api.md)
