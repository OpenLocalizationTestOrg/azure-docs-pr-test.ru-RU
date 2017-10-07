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
ms.openlocfilehash: 945eb4f9eff28c92ec963585d27cba73a7eb59bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="4ae9d-104">Краткий справочник по часто используемым командам для заданий импорта</span><span class="sxs-lookup"><span data-stu-id="4ae9d-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="4ae9d-105">Этот раздел содержит краткий справочник по часто используемым командам.</span><span class="sxs-lookup"><span data-stu-id="4ae9d-105">This section provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="4ae9d-106">Дополнительные сведения об использовании см. в разделе [Подготовка жестких дисков для задания импорта](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span><span class="sxs-lookup"><span data-stu-id="4ae9d-106">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-a-hard-drive-when-data-has-already-been-copied-toohello-hard-drive"></a><span data-ttu-id="4ae9d-107">Подготовка жесткого диска, когда данные уже были скопированы toohello жесткого диска</span><span class="sxs-lookup"><span data-stu-id="4ae9d-107">Prepare a hard drive when data has already been copied toohello hard drive</span></span>
 <span data-ttu-id="4ae9d-108">Hello следующую команду подготавливает жесткий диск, когда данные уже скопированные tooit, но еще не зашифрован с помощью BitLocker:</span><span class="sxs-lookup"><span data-stu-id="4ae9d-108">hello following command prepares a hard drive when data has already been copied tooit, but has not yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a><span data-ttu-id="4ae9d-109">Копирование на жесткий диск tooa один каталог</span><span class="sxs-lookup"><span data-stu-id="4ae9d-109">Copy a single directory tooa hard drive</span></span>  
 <span data-ttu-id="4ae9d-110">Привет, следующая команда копирует одного исходного каталога tooa жесткий диск, который еще не был зашифрован с помощью BitLocker:</span><span class="sxs-lookup"><span data-stu-id="4ae9d-110">hello following command copies a single source directory tooa hard drive that has not yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-two-directories-tooa-hard-drive"></a><span data-ttu-id="4ae9d-111">Копирования двух каталогов tooa жесткого диска</span><span class="sxs-lookup"><span data-stu-id="4ae9d-111">Copy two directories tooa hard drive</span></span>  
 <span data-ttu-id="4ae9d-112">toocopy два источника каталоги tooa диск, hello используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="4ae9d-112">toocopy two source directories tooa drive, use hello following commands:</span></span>  
  
 <span data-ttu-id="4ae9d-113">Hello первая команда задает каталог журнала hello, ключ учетной записи хранилища, букву целевого диска `format/encrypt` требования и общие параметры:</span><span class="sxs-lookup"><span data-stu-id="4ae9d-113">hello first command specifies hello log directory, storage account key, target drive letter, `format/encrypt` requirements, and common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="4ae9d-114">Вторая команда Hello указывает файл журнала hello, новый идентификатор сеанса и hello исходное и целевое расположение:</span><span class="sxs-lookup"><span data-stu-id="4ae9d-114">hello second command specifies hello journal file, a new session ID, and hello source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="4ae9d-115">Копирование большого файла tooa жесткий диск в рамках второго сеанса копирования</span><span class="sxs-lookup"><span data-stu-id="4ae9d-115">Copy a large file tooa hard drive in a second copy session</span></span>  
 <span data-ttu-id="4ae9d-116">Привет, следующая команда копирует один большой файл tooa жесткий диск, который был подготовлен в предыдущем сеансе копирования:</span><span class="sxs-lookup"><span data-stu-id="4ae9d-116">hello following command copies a single large file tooa hard drive that was prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="4ae9d-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4ae9d-117">Next steps</span></span>

* [<span data-ttu-id="4ae9d-118">Образец рабочего процесса tooprepare жесткие диски для задания импорта</span><span class="sxs-lookup"><span data-stu-id="4ae9d-118">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
