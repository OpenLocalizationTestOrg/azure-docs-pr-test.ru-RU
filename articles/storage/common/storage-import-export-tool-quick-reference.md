---
title: "aaaQuick Справочник по командам задания импорта средство импорта и экспорта Azure | Документы Microsoft"
description: "Справочник по командам инструмента импорта и экспорта Azure, которые наиболее часто используются для заданий импорта."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 35e46f24f764a5098ca465adb51badcab2d13e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="89cce-103">Краткий справочник по часто используемым командам для заданий импорта</span><span class="sxs-lookup"><span data-stu-id="89cce-103">Quick reference for frequently used commands for import jobs</span></span>

<span data-ttu-id="89cce-104">В этой статье приводится краткая справочная информация о некоторых часто используемых командах.</span><span class="sxs-lookup"><span data-stu-id="89cce-104">This article provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="89cce-105">Дополнительные сведения об использовании см. в разделе [Подготовка жестких дисков для задания импорта](../storage-import-export-tool-preparing-hard-drives-import.md).</span><span class="sxs-lookup"><span data-stu-id="89cce-105">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import.md).</span></span>

## <a name="first-session"></a><span data-ttu-id="89cce-106">Первый сеанс</span><span class="sxs-lookup"><span data-stu-id="89cce-106">First session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1 /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

## <a name="second-session"></a><span data-ttu-id="89cce-107">Второй сеанс</span><span class="sxs-lookup"><span data-stu-id="89cce-107">Second session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /DataSet:dataset-2.csv
```

## <a name="abort-latest-session"></a><span data-ttu-id="89cce-108">Прерывание последнего сеанса</span><span class="sxs-lookup"><span data-stu-id="89cce-108">Abort latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /AbortSession
```

## <a name="resume-latest-interrupted-session"></a><span data-ttu-id="89cce-109">Возобновление последнего прерванного сеанса</span><span class="sxs-lookup"><span data-stu-id="89cce-109">Resume latest interrupted session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /ResumeSession
```

## <a name="add-drives-toolatest-session"></a><span data-ttu-id="89cce-110">Добавление дисков toolatest сеанса</span><span class="sxs-lookup"><span data-stu-id="89cce-110">Add drives toolatest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /AdditionalDriveSet:driveset-2.csv
```

## <a name="next-steps"></a><span data-ttu-id="89cce-111">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="89cce-111">Next steps</span></span>

* [<span data-ttu-id="89cce-112">Образец рабочего процесса tooprepare жесткие диски для задания импорта</span><span class="sxs-lookup"><span data-stu-id="89cce-112">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
