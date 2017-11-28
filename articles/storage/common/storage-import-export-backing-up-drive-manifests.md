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
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a><span data-ttu-id="5ae5b-103">Архивация манифестов дисков для заданий импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="5ae5b-103">Backing up drive manifests for Azure Import/Export jobs</span></span>

<span data-ttu-id="5ae5b-104">Манифестов диска может быть автоматически резервное tooblobs с помощью параметра hello `BackupDriveManifest` свойство слишком`true` в hello [вставки задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) или [обновления свойств задания](/rest/api/storageimportexport/jobs#Jobs_Update) операции REST API.</span><span class="sxs-lookup"><span data-stu-id="5ae5b-104">Drive manifests can be automatically backed up tooblobs by setting hello `BackupDriveManifest` property too`true` in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API operations.</span></span> <span data-ttu-id="5ae5b-105">По умолчанию hello манифестов диска не копируются.</span><span class="sxs-lookup"><span data-stu-id="5ae5b-105">By default, hello drive manifests are not backed up.</span></span> <span data-ttu-id="5ae5b-106">резервные копии манифестов дисков Hello хранятся как блочные большие двоичные объекты в контейнере в учетной записи хранилища hello, связанный с заданием hello.</span><span class="sxs-lookup"><span data-stu-id="5ae5b-106">hello drive manifest backups are stored as block blobs in a container within hello storage account associated with hello job.</span></span> <span data-ttu-id="5ae5b-107">По умолчанию является имя контейнера hello `waimportexport`, но можно указать другое имя в hello `DiagnosticsPath` свойства при вызове hello `Put Job` или `Update Job Properties` операций.</span><span class="sxs-lookup"><span data-stu-id="5ae5b-107">By default, hello container name is `waimportexport`, but you can specify a different name in hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="5ae5b-108">Hello большого двоичного объекта манифеста именуются в hello следующий формат: `waies/jobname_driveid_timestamp_manifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="5ae5b-108">hello backup manifest blob are named in hello following format: `waies/jobname_driveid_timestamp_manifest.xml`.</span></span>

 <span data-ttu-id="5ae5b-109">Вы можете получить URI резервного копирования диска hello манифесты для задания, вызывающему Привет hello [получения задания](/rest/api/storageimportexport/jobs#Jobs_Get) операции.</span><span class="sxs-lookup"><span data-stu-id="5ae5b-109">You can retrieve hello URI of hello backup drive manifests for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="5ae5b-110">URI, возвращаемый в hello blob Hello `ManifestUri` свойство для каждого диска.</span><span class="sxs-lookup"><span data-stu-id="5ae5b-110">hello blob URI is returned in hello `ManifestUri` property for each drive.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ae5b-111">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5ae5b-111">Next steps</span></span>

* [<span data-ttu-id="5ae5b-112">С помощью REST API службы импорта и экспорта hello</span><span class="sxs-lookup"><span data-stu-id="5ae5b-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
