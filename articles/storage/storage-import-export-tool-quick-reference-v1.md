---
title: "Справочник по aaaQuick для команд задания импорта средство импорта и экспорта Azure - v1 | Документы Microsoft"
description: "Справочник по командам инструмента импорта и экспорта Azure, которые наиболее часто используются для заданий импорта. Это относится toov1 из hello средство импорта и экспорта."
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
ms.openlocfilehash: e36f065e5d23268758cf6b6db9428fe8a8e1056d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="1e263-104">Краткий справочник по часто используемым командам для заданий импорта</span><span class="sxs-lookup"><span data-stu-id="1e263-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="1e263-105">В этом разделе приводится краткая справочная информация о некоторых часто используемых командах.</span><span class="sxs-lookup"><span data-stu-id="1e263-105">This section provides a quick references for some frequently used commands.</span></span> <span data-ttu-id="1e263-106">Дополнительные сведения об использовании см. в разделе [Подготовка жестких дисков для задания импорта](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span><span class="sxs-lookup"><span data-stu-id="1e263-106">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-hello-disks-when-data-already-copied-toohello-disks"></a><span data-ttu-id="1e263-107">Подготовка дисков hello при данных уже скопированы toohello дисков</span><span class="sxs-lookup"><span data-stu-id="1e263-107">Prepare hello disks when data already copied toohello disks</span></span>
 <span data-ttu-id="1e263-108">Ниже приведен пример команды tooprepare дисков при данных уже скопированы toohello жесткий диск, который еще не зашифрован BitLocker:</span><span class="sxs-lookup"><span data-stu-id="1e263-108">Here is a sample command tooprepare a disks when data already copied toohello hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a><span data-ttu-id="1e263-109">Копирование на жесткий диск tooa один каталог</span><span class="sxs-lookup"><span data-stu-id="1e263-109">Copy a single directory tooa hard drive</span></span>  
 <span data-ttu-id="1e263-110">Ниже приведен пример toocopy команд, один исходный жесткий диск tooa каталог, который еще не зашифрован BitLocker:</span><span class="sxs-lookup"><span data-stu-id="1e263-110">Here is a sample command toocopy a single source directory tooa hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-tooa-hard-drive"></a><span data-ttu-id="1e263-111">Скопируйте wwo каталоги tooa жесткого диска</span><span class="sxs-lookup"><span data-stu-id="1e263-111">Copy wwo directories tooa hard drive</span></span>  
 <span data-ttu-id="1e263-112">toocopy два источника каталоги tooa дисков, вам потребуется две команды.</span><span class="sxs-lookup"><span data-stu-id="1e263-112">toocopy two source directories tooa drive, you will need two commands.</span></span>  
  
 <span data-ttu-id="1e263-113">Hello первая команда задает каталог журнала hello, ключ учетной записи хранилища, букву целевого диска и `format/encrypt` требования в дополнение toohello Общие параметры:</span><span class="sxs-lookup"><span data-stu-id="1e263-113">hello first command specifies hello log directory, storage account key, target drive letter and `format/encrypt` requirements, in addition toohello common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="1e263-114">Вторая команда Hello указывает файл журнала hello, новый идентификатор сеанса и hello исходное и целевое расположение:</span><span class="sxs-lookup"><span data-stu-id="1e263-114">hello second command specifies hello journal file, a new session ID, and hello source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="1e263-115">Копирование большого файла tooa жесткий диск в рамках второго сеанса копирования</span><span class="sxs-lookup"><span data-stu-id="1e263-115">Copy a large file tooa hard drive in a second copy session</span></span>  
 <span data-ttu-id="1e263-116">Ниже приведен пример команды, который копирует диск tooa один большой файл, который был подготовлен в предыдущем сеансе копирования.</span><span class="sxs-lookup"><span data-stu-id="1e263-116">Here is a sample command that copies a single large file tooa drive that has been prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="1e263-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1e263-117">Next steps</span></span>

* [<span data-ttu-id="1e263-118">Образец рабочего процесса tooprepare жесткие диски для задания импорта</span><span class="sxs-lookup"><span data-stu-id="1e263-118">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
